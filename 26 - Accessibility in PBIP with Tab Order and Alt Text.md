<img width="1429" height="952" alt="Group 48095443" src="https://github.com/user-attachments/assets/7981e7ad-ee9b-4a86-868b-fb9d2e3e7fe2" />
<br>
<br>

**Accessibility is a prerequisite for good design.** I believe the community has made meaningful progress on these topics in recent years, particularly in improving colour contrast, font sizing, and the use of accessible colour palettes. This progress is clearly reflected in report competitions, blog posts, portfolios, and shared community examples.

However, accessibility is a much broader topic. For example, if you participate in the Microsoft Data Visualization Championships, you’ll notice two criteria that most developers have rarely, if ever, implemented: **Tab order** and **Alt text**.

Why is that? I don’t think the issue is that developers are unaware of these features. I think most know they exist, at least at a high level. The real problem is that the Power BI Desktop interface makes accessibility features difficult to locate and difficult to test. There’s no enforcement mechanism and no validation feedback. You often only discover issues when a keyboard user navigates the report and ends up in the wrong place.

Moving to the PBIR format changes the equation. Accessibility properties that were previously hidden in the interface become auditable, automatable, and enforceable.
<br>

> [!NOTE]
>**That’s the goal of this blog post: to explore whether accessibility can shift from a “nice to have” to a true standard driven by automation.**

<br>

Let's dive in.


### What Tab Order and Alt Text actually do

**Tab order** is the sequence in which keyboard focus moves through the visuals on a report page when a user presses the Tab key. For someone navigating without a mouse, a screen reader user, or anyone relying on keyboard-only interaction, tab order is the only navigation mechanism available. Without it set explicitly, Power BI assigns focus in an arbitrary sequence based on the order visuals were added to the canvas. That sequence rarely matches the intended reading flow.
<br>

<img width="180" height="241" alt="image" src="https://github.com/user-attachments/assets/fa5f0fde-b544-46f8-aa10-94651a9af61d" />

<br>

> [!TIP]
> Did you know that if you go to Selection > Tab Order and click the button highlighted in the image “Have tab order match visual order” it will automatically reorder the tab sequence of elements on the page?

<br>

**Alt text** is the description a screen reader reads aloud when it lands on a visual. With it set correctly, the user hears "Bar chart showing monthly sales by region for FY2024. North America leads at $4.2M." That is the difference between a report that works for everyone and one that works only for sighted users with a mouse.
<br>

<img width="172" height="447" alt="image" src="https://github.com/user-attachments/assets/7b399fc6-5065-4f57-aadd-daf123359568" />

<br>
Both properties serve the same purpose: they make a report navigable and interpretable for users who experience it differently. 

<br>

### What happens when you try to do it right in PBIR

Implementing accessibility in your reports is not a question of effort. It is not a bullet point to check before publishing. It is a question of architecture. A developer who treats accessibility as a last-minute task will miss entire categories of it. A developer whose workflow produces accessibility properties as a structural output will always perform better.

Here is the experience I encountered when I implement Tab Order and Alt Text through PBIR and using PowerBI-modelling-mcp.  

The real experience.

**Alt text is easy.** You edit the visual JSON, add the `altText` property under `visualContainerObjects`, and Power BI Desktop picks it up immediately. No issues. Commit, push, done. The structure is clean and predictable.

<img width="1375" height="582" alt="image" src="https://github.com/user-attachments/assets/d2530434-91b9-4866-a574-ec4e990bb01b" />


**Tab order broke the first time.** The first attempt to add `tabOrder` properties to visual JSON triggered schema validation errors in Power BI Desktop. The property exists in the file but Power BI ignored it, without warning, without error, without any indication that something is wrong. I discover the problem only when I opened the report and keyboard navigation still did not work. I removed the properties and started again.

**The re-implementation surfaces two behaviour that are not documented clearly anywhere.**

**The descending order rule:** tabOrder operates in reverse. A higher numeric value means earlier in the keyboard sequence. A visual with `tabOrder: 6000` receives focus first. A visual with `tabOrder: 1000` receives focus last. This is the opposite of what most developers assume. If you implement it the intuitive way, lowest value first, your tab sequence runs backwards through the page.

**The z synchronization rule:** the `z` property (which controls layer stacking) and `tabOrder` are not independent. They must move proportionally in the same direction. If z values do not scale in alignment with tabOrder values, layer rendering breaks independently of keyboard order. You end up with a report where tab navigation works correctly but visuals overlap in the wrong stacking sequence.

```json
// First tab stop: KPI visual, top-left of the page
{
  "position": {
    "z": 4000,
    "tabOrder": 5000
  }
}

// Second tab stop: bar chart
{
  "position": {
    "z": 3800,
    "tabOrder": 4000
  }
}

// Last tab stop: matrix at the bottom
{
  "position": {
    "z": 1000,
    "tabOrder": 1000
  }
}
```

tabOrder 5000 fires first. tabOrder 1000 fires last. z scales proportionally downward alongside tabOrder. **This behaviuor is real and personally, I do not find it that obvious**

> [!NOTE]
> tabOrder was silently invalid in Power BI Desktop 2.147.x. The property existed in the file but was ignored without error. Always verify your PBI Desktop version supports the schema version referenced in your visual JSON files before building a tab order workflow around it.

The full development arc I used across five commits tells the same story every developer will live through: add alt text (works), add tabOrder (schema failure, forced rollback), re-implement with descending logic (works), discover z synchronization is required (update all z values), apply the validated pattern to the remaining pages.

Three hours of iteration. Two non-obvious behaviours. One repeatable pattern at the end.

<br>

### PBIR format makes accessibility auditable

Here is what PBIR unlocks that the `.pbix` binary cannot: because PBIR stores report metadata as JSON files in a folder structure, you can grep every visual for a missing `altText` property in one command. You can validate that all tabOrder values follow the correct descending sequence before opening Power BI Desktop.

When someone edits a report in the interface and overwrites an alt text property, it shows up as a changed line in Git. One line. Reviewable. Revertible. Traceable to a commit message.

The alt text structure in PBIR is consistent across all visual types. Both a static literal and a dynamic DAX measure variant are supported:

```json
// Static alt text
"visualContainerObjects": {
  "general": [{
    "properties": {
      "altText": {
        "expr": {
          "Literal": {
            "Value": "'Scatter chart analyzing the relationship between Margin (x-axis) and Sales (y-axis) by City. Each bubble represents a city, showing profitability versus revenue correlation.'"
          }
        }
      }
    }
  }]
}
```

```json
// Dynamic alt text via DAX measure
"altText": {
  "expr": {
    "Measure": {
      "Expression": { "SourceRef": { "Entity": "_Measures" } },
      "Property": "Alt Text - Sales Visual"
    }
  }
}
```

The static variant is straightforward. The DAX variant requires a measure in your semantic model, but that measure can reference filter context, selected values, and calculated summaries. The result is alt text that reads "Sales for FY2024 in North America: $4.2M, up 12% vs prior year" instead of something like "Bar chart showing sales." This is the difference between a label and a description. That distinction is what accessibility is all about.

<br>

### AI and Modeling MCP Server can generate accessibility properties automatically

A modeling MCP server connected to your PBIR folder can read a visual's type, position, data bindings, and page context. From that information, it can generate a meaningful alt text string and a correct `tabOrder` value that respects the visual reading hierarchy. PBIR is structured JSON. An AI model with file access can parse it reliably and apply well-defined rules against it.

The workflow is direct. You point an AI tool at your PBIR report folder. It reads the visual files, identifies which visuals are missing alt text, and produces contextually appropriate descriptions for each one. The output is a set of JSON patch objects: review, diff, and commit like any other code change. No interface interaction required.

This is the right abstraction boundary. You define visual intent and data context at design time. The AI handles the mechanical translation of that intent into WCAG-compliant descriptions. Separating those responsibilities is good engineering.

To run this on your own report, open Visual Studio Code and a Claude or GitHub copilot session with file access to your PBIR folder, then paste this prompt:

```
For each visual in this PBIR report folder:

1. Read the visual type (visualType), title (from visualContainerObjects),
   and data bindings (from the query object: field names, measure names).
2. Read the position object: x, y coordinates indicate where the visual
   sits on the page.
3. Check whether altText is defined under
   visualContainerObjects > general > properties.
4. If altText is missing, generate a descriptive alt text string that:
   • Names the chart type
   • Names the primary measure and dimension
   • Describes the user question the visual answers
   • Stays under 150 characters
5. Output a JSON patch object for each visual using the PBIR altText
   structure under visualContainerObjects.
6. For tab order: assign descending tabOrder values in multiples of 1000,
   following left-to-right, top-to-bottom reading sequence based on x/y.
   Set z values to scale proportionally downward with tabOrder.
   Output the updated position objects for every visual on the page.

Do not modify any other properties. Output only the patch objects,
grouped by page, with the visual name as the key.
```

> [!TIP]
> The prompt works because PBIR is structured data, not a compiled binary. The AI is parsing visual type, chart fields, and coordinates, then applying rules the format makes explicit. The reliability comes from the structure, not from the model's general knowledge.

<img width="946" height="670" alt="image" src="https://github.com/user-attachments/assets/af3e54d9-fcd2-43a0-ad10-fbd9e10b1ee9" />

<br>
<img width="957" height="785" alt="image" src="https://github.com/user-attachments/assets/ea0ae4d2-90d0-41f7-a2d1-4706b0a6e633" />

<br>


### Conclusion


Accessibility applied through the interface at the end of a project is fragile. It does not survive report restructuring, visual additions under time pressure, or a competition sprint where the last hour goes to polishing charts. Accessibility embedded in PBIR structure, tracked in Git, and enforced through an AI-driven audit survives all of that. It is part of the architecture, not painted on top of it.


<br>

💬 Drop your thoughts in the **[LinkedIn post](#)**.
✅ Scripts available in the **[GitHub repo](#)**.

### I'll be back! ⌛
