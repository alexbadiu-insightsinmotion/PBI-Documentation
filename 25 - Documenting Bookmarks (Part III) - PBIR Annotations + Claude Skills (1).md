
<img width="1464" height="971" alt="Group 48095444" src="https://github.com/user-attachments/assets/e860d4d2-16bf-4b62-b3ed-dd63a69b0f27" />



# Power BI Bookmarks Documentation (Part III): PBIR Annotations + Claude Skills

In [Part II](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/23%20-%20Documenting%20Bookmarks%20(part%20II)%20-%20Why%20External%20Documentation%20Fails.md) of this series, I identified three structural problems with external documentation: it requires too much discipline to maintain, produces inconsistent quality across developers, and is invisible to the AI tools increasingly used to build and evolve Power BI solutions. External markdown files and spreadsheets were the right instinct but the wrong location.

The solution is to embed the business context directly in the PBIR source file using annotations, and use a Claude Skill to make that process repeatable without relying on memory or individual discipline. This article shows exactly how that works, and adds a Mintlify (user friendly documentation website) layer on top to turn those source-file annotations into a searchable, human-readable documentation site.


## What PBIR Annotations are

PBIR bookmark JSON supports an `annotations` array. This is not a workaround or an undocumented trick. It is a [standard mechanism](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-report?tabs=v2%2Cdesktop#pbir-annotations) built into the PBIR format for storing structured metadata alongside any object.

The annotation for a bookmark looks like this:

```json
{
  "name": "Documentation",
  "value": "{\"businessPurpose\": \"Enable sales managers to investigate specific regions when unusual performance patterns are detected during monthly review meetings.\", \"userScenario\": \"After spotting an anomaly in the overview, click FocusSpecific to drill into regional detail without losing the overall filter context.\", \"documentedDate\": \"2025-12-24T10:30:00Z\", \"documentedBy\": \"Alexandru BADIU\", \"maintenanceNotes\": \"FocusSpecific does not control Ribbon Chart visibility. Behavior is state-dependent based on the previously active bookmark.\"}"
}
```

In the bookmark file, the `annotations` array sits at the same level as `options` and `explorationState`:

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/fabric/item/report/definition/bookmark/1.4.0/schema.json",
  "displayName": "FocusSpecific",
  "name": "a87d1123fc3c1c928935",
  "options": { ... },
  "explorationState": { ... },
  "annotations": [
    {
      "name": "Documentation",
      "value": "{ ... }"
    }
  ]
}
```

This annotation travels with the bookmark in git. When the bookmark JSON is committed, the business context is committed alongside it. When Claude Code opens the PBIP project, it reads both the technical behavior from `explorationState` and the intent from the annotation, without requiring you to paste any additional context.

> [!NOTE]
> The `annotations` array is the same mechanism Power BI Desktop uses internally to store display properties. It is part of the schema, not an extension of it.

---

## The scalability problems, now Solved

The three problems from Part II map are now solved:

| Problem (Part II) | Solution (Part III) |
|---|---|
| Too much to remember | `@pbir-documentation` skill guides you through a structured workflow |
| Inconsistent quality | Same 5 interview questions, same output format, every time |
| Invisible to AI | Annotations live in the PBIR file the AI already reads |

None of this requires discipline. You invoke the skill; it handles the structure.
-->>> **The skill is accessible [HERE](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Skills/pbir-documentation.md)**

---

## The Skill Workflow

The `pbir-documentation` skill is invoked with `@pbir-documentation` inside Claude Code. It handles five distinct operations:

**1. Discover and Inventory**

Scans the PBIP folder structure and produces a documentation inventory: how many bookmarks exist, how many have annotations, which ones are missing documentation. This is always the starting point for a new or inherited report.

**2. Document Bookmark**

This is the core operation. The skill:
- Reads the bookmark JSON and extracts all technical details (settings, visual mappings, filter states, scope)
- Asks you five structured questions to capture business context
- Generates a markdown documentation file at `documentation/bookmarks/[BookmarkName].md`
- Generates the annotation JSON and presents it for review
- Writes the approved annotation back to the PBIR file

The five interview questions are:

```
1. Business Purpose: Why was this bookmark created? What business scenario does it address?
2. User Scenario: When should end users apply this bookmark?
3. Expected Behavior: What should users see or experience when they activate it?
4. Dependencies: Are there prerequisites or specific states that must exist before using it?
5. Related Bookmarks: Does this interact with other bookmarks? If so, how?
```

<img width="2000" height="1200" alt="VSC_BookmarkQuestions" src="https://github.com/user-attachments/assets/da439369-acbe-44a6-8643-a30576850625" />



For legacy reports where the context is unknown, "Unknown - legacy report" is a valid answer. The skill does not block on missing business context.

**3. Document Visual Calculation**

The same workflow is applied to visuals containing visual calculations: the DAX is extracted, the measure dependencies are mapped, and the reasoning as to why a visual calculation was chosen over a model measure is captured.

**4. Validate Documentation**

Runs three levels of validation checks against all documented objects:
- **Level 1 (Critical):** All bookmarks have annotations, all visual references exist, no placeholder text
- **Level 2 (Recommended):** Business purpose documented, user scenarios described, measure dependencies listed
- **Level 3 (Optional):** Performance notes, alternative approaches, testing procedures

**5. Refresh All**

A full sweep for maintenance cycles. Checks all existing documentation against current JSON, updates where the technical state has changed, and preserves the business context where it hasn't.


## What the Output looks like

I used this skill on the same DemoDataset PBIP project used in the previous articles to document all four bookmarks. Here is the executive summary the skill produced:

| Bookmark | ID | Purpose | Complexity | Year Filter |
|---|---|---|---|---|
| **Ribbon Chart** | 3c04be006f1ebff4ddc5 | Toggle to Ribbon Chart view | Simple | 2019 |
| **Clustered Chart** | 5977e1c788aabf285a32 | Value comparison view | Simple | 2019 |
| **FocusSpecific** | a87d1123fc3c1c928935 | Advanced state-dependent highlighting | **Complex** | 2019 |
| **Reset Filters** | 77f6391b96f7c17022ed | Reset to baseline | Moderate | 2023 |

The skill also produced a bookmark interaction map that revealed something I was not fully aware of before running the full documentation pass:

```
Reset Filters (Baseline)
    │
    ├──> Ribbon Chart <──> Clustered Chart (Toggle Pair)
    │         │                    │
    │         └────────┬───────────┘
    │                  │
    └──────────────> FocusSpecific (State-dependent)
                         ↓
                   (Different result based on previous!)
```

**FocusSpecific produces a different visual result depending on which bookmark was active before it.** The JSON for FocusSpecific does not explicitly control the Ribbon Chart's visibility, so whether the ribbon chart is visible or hidden when FocusSpecific activates depends on what the previous bookmark did to it.

```
Reset Filters  → FocusSpecific = Result A (Clustered Bar visible)
Ribon Chart    → FocusSpecific = Result B (Ribbon Chart visible)
Clustered Chart → FocusSpecific = Result C (Clustered Bar sorted differently)
```

This finding was not visible from reading any single bookmark JSON in isolation. It only became apparent when the skill documented all four bookmarks and mapped their interactions together. That is exactly the kind of insight that justifies the documentation effort.

The skill also flagged an inconsistency I had not noticed: the demo bookmarks (Ribon Chart, Clustered Chart, FocusSpecific) reference `Sales[Sales]` and `Sales[Sales PY]`, while Reset Filters references `_Measures[Sales]` and `_Measures[Sales PY]`. This indicates a measure table refactoring that was applied inconsistently across bookmarks.

> [!IMPORTANT]
> The skill found two issues that were invisible from the Power BI Desktop UI: the state-dependent behavior of FocusSpecific, and the measure table inconsistency across bookmarks. Both were discovered by reading all bookmark JSON files together and cross-referencing them, which is exactly what the Discover and Inventory operation does.

The output file structure after running the skill:

```
documentation/
├── bookmarks/
│   ├── ResetFilters.md
│   ├── FocusSpecific.md
│   ├── RibbonChart.md
│   └── ClusteredChart.md
└── visual_calculations/
    └── ...
```

Each markdown file follows a consistent structure: business purpose, user scenario, technical overview, affected visuals, filter states, behavior description, dependencies, and change history.

---

## Mintlify: How to make documentation human-readable

The `documentation/` folder lives inside the PBIP git repository. Developers using VS Code can read it directly, but business stakeholders and QA teams cannot be expected to browse a git repository. Mintlify turns those markdown files into a searchable, versioned documentation site that updates automatically on every push.


Here’s an example of Bookmark Documentation on Mintlify - white background
<img width="1944" height="1328" alt="Mintlyfy White" src="https://github.com/user-attachments/assets/63481a29-37d7-4295-89f0-a4bfdb6c4db2" />


Here’s an example of Bookmark Documentation on Mintlify - dark background
<img width="1986" height="1339" alt="Mintlyfy Dark" src="https://github.com/user-attachments/assets/4f531bf0-f068-4c4c-87be-d2dceee9b991" />


Here’s an example of Bookmark Documentation on Mintlify - built-in AI 
<img width="2054" height="1289" alt="Mintlyfy AI" src="https://github.com/user-attachments/assets/39292778-b50c-4086-af55-7fb1c36b7bfb" />



Have a look at the user-friendly and dynamic documentation here: https://decilia.mintlify.app/documentation/bookmarks/RibonChart

### Step 1: Add `docs.json` to the PBIP root

This is the Mintlify configuration file. Note the required `$schema` and `theme` fields — Mintlify's current format (v2) will not deploy without them.

```json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "mint",
  "name": "Demo Dataset",
  "colors": {
    "primary": "#F2C811"
  },
  "navigation": {
    "groups": [
      {
        "group": "Overview",
        "pages": ["index", "BOOKMARKS_DOCUMENTATION"]
      },
      {
        "group": "Bookmarks",
        "pages": [
          "documentation/bookmarks/ResetFilters",
          "documentation/bookmarks/ClusteredChart",
          "documentation/bookmarks/RibonChart",
          "documentation/bookmarks/FocusSpecific"
        ]
      }
    ]
  }
}
```

### Step 2: How to structure each markdown file for Mintlify

Mintlify uses `title` and `description` from frontmatter for navigation labels and search. Add this block at the top of each bookmark documentation file:

```yaml
---
title: "Reset Filters"
description: "Resets the report to baseline state with 2023 data and default visual configuration."
---
```

### Step 3: Add an `index.mdx` homepage

```mdx
---
title: "Demo Dataset Documentation"
description: "Technical and business documentation generated from PBIR source files."
---

# Demo Dataset

This site documents the bookmarks in the Demo Dataset Power BI report.
Documentation is generated from PBIR source files using the `pbir-documentation`
Claude Skill and maintained in version control alongside the report.
```

### Step 4: Commit and push to GitHub

```bash
git add docs.json index.mdx documentation/
git commit -m "Add Mintlify documentation site configuration"
git push
```
No need to worry if these steps aren’t fully clear. An LLM assistant can handle them for you. This is simply an overview of what it does.

### Step 5: Connect to Mintlify

1. Create a free account at [mintlify.com](https://mintlify.com)
2. When asked how to set up your docs, choose **Try the manual setup instead** (not Auto-generate as that option rewrites your content with AI)
3. Install the Mintlify GitHub App when prompted, authorize it for your repo
4. Go to **Settings > Git settings** in the Mintlify dashboard
5. Set repository, branch (`main`), and leave docs directory empty (root)
6. Save - Mintlify deploys automatically

From this point forward, every `git push` updates the site. No manual publishing step.

> [!TIP]
> If your PBIP project is in a subfolder of a larger repository, set the docs directory in Git settings to the subfolder path where `docs.json` lives.

---

## The Complete Picture

Part I - [Issue 21](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/21%20-%20Documenting%20Bookmarks%20with%20PBIR.md) showed that PBIR bookmark JSON is structured and rich: visual IDs, filter states, scope settings, and display properties are all there to be read by an AI or a developer with VS Code.

Part II - [Issue 23](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/23%20-%20Documenting%20Bookmarks%20(part%20II)%20-%20Why%20External%20Documentation%20Fails.md) showed that extracting that information is not enough. Without a consistent capture process and an accessible location, business context does not survive team handoffs, report refactors, or the passage of time.

This part III closes the loop. The annotation embeds the "why" directly in the source. The skill enforces structure and removes the memory burden. The Mintlify site makes the result accessible to anyone with a browser, not just developers with VS Code.

When Claude Code opens a PBIP project with annotations in place, it reads both the technical behavior in `explorationState` and the intent in the annotation in one pass. You do not need to paste context. You do not need to explain what the bookmark was built to do; that information is already there.

---

## Conclusion

This series started with a simple question: can we extract useful documentation from PBIR JSON? The answer is yes, clearly and immediately. PBIR stores enough structure to reconstruct what a bookmark does with good precision.

But that question quickly revealed a harder one: where does the "why" live? The JSON can tell you that FocusSpecific applies a North America highlight and a Male gender filter. It cannot tell you that this was requested by the Sales Operations team to support monthly review meetings, or that the state-dependent behavior with the Ribbon Chart was not caught in testing and has been confusing users ever since.

The annotation approach does not require a new tool or a new format. The `annotations` array is already in the schema. The Claude Skill wraps a structured workflow around it so that the quality of the output does not depend on which developer runs it. Mintlify makes the result readable by the people who care most about it but are least likely to open a JSON file.

The broader principle applies beyond bookmarks. As AI becomes a genuine participant in Power BI development, not just an assistant that generates code on request, the value of in-source context compounds. Every annotation written today becomes context that a future AI-assisted change can reason over. Documentation stops being a compliance exercise and becomes infrastructure.

The building blocks are in place. The format supports it. The tooling exists. What remains is the decision to treat documentation as part of the development workflow rather than something that happens after the report ships.

---

**Next steps:**

- Vote for the [Add Description field for Bookmarks in Power BI Desktop and PBIR Format](https://community.fabric.microsoft.com/t5/Fabric-Ideas/Add-Description-field-for-Bookmarks-in-Power-BI-Desktop-and-PBIR/idi-p/4818843#M163577) idea on the Fabric community
- Try the `pbir-documentation` skill on a report you own
- Share your findings in the comments

**For questions or comments about this article, contact:** Alexandru BADIU

**If you found this valuable, please:**
- Share this article with your Power BI team
- Follow Greg’s and my work on [GitHub](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation)
