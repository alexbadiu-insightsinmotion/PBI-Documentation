
<img width="1950" height="1068" alt="Issue #300" src="https://github.com/user-attachments/assets/09516213-c1d3-425e-8aac-ee266d1710b6" />



A common challenge persists across many organizations: **the inability to effectively collaborate on Power BI semantic models or track changes** with meaningful version control. 

Too often, development teams rely on passing PBIX files back and forth, hoping no one overwrites someone else's work. Teams also end up building file naming conventions like "SalesReport_v3_Final_FINAL_Alex_Updated.pbix" and crossing their fingers.

And how is this PBIX different than "SalesReport_v2_FIN_Alex_Draft.PBIX" ? We don't know, but usually we save at regular periods of time and we store it "just in case".<br>

> [!TIP]
> As a best practice, it is recommended (and still is for users not using Fabric Capacities) to store PBIX files in SharePoint or OneDrive to take advantage of automatic version history, eliminating the need for manual version naming conventions like v1, v2, v3. 

<br>
This first article of the series explores how TMDL (Tabular Model Definition Language) addresses these fundamental limitations by introducing a human-readable, text-based format for Power BI semantic models. We will define what TMDL is and how it enables professional development practices including version control, team collaboration, and code reusability.

## What is TMDL?

**TMDL is a human-readable format for defining Power BI semantic models. Think of it as three related concepts:**

1. **TMDL Language** : This refers to the actual syntax (like JSON or YAML) used to describe tables, measures, and relationships in plain text. it's accessible and easy to read for everyone. Main advantage: easy to follow tracking and see all properties in one screen.
2. **TMDL Format** : A file storage option for Power BI Projects (PBIP) that organizes your model into separate, readable files instead of one large JSON file. It's ideal for version control with Git and collaborative work on the same report.
3. **TMDL View** : This is a new interactive code editor screen in Power BI Desktop where you can drag objects, and take actions like making bulk changes with find-and-replace, and scripting your model without clicking through menus. This is what we call TMDL scripting.


**In simple terms:** TMDL lets you work with Power BI models as readable code in one place rather than distributed through the visual interface. You can use TMDL View for quick bulk edits inside Power BI Desktop, or save your entire project in TMDL format for better collaboration and version control. They work together but serve different purposes: One is for editing, one for storing.


### The origin story

TMDL didn't actually emerge from Microsoft's product roadmap. It came directly from the community through the Power BI Contributor Program, with significant contributions from Mathias Thierbach. 

Microsoft recognized this potential and made TMDL an official part of the platform. This is Power BI growing up. It allows adopting professional practices that software development teams have relied on for decades.

## Why TMDL matters

The traditional Power BI development workflow presents several critical limitations:

- **No meaningful version control**: PBIX files are binary, making Git diffs useless
- **Single-developer bottleneck**: Only one person can work on a model at a time
- **No code reviews**: No visibility on changes. 
- **Manual repetitive tasks**: Some tasks require clicking through dialogs dozens of times.
- **Knowledge silos**: Best practices and reusable patterns stay locked in individual developer's heads -> This reduces the scalability, potential acceleration, and quality standardization of Power BI development

TMDL fundamentally addresses these challenges by transforming Power BI development from isolated activities into collaborative, professional development practices.

### Key Characteristics

**Human-Readable Syntax**  
TMDL uses a YAML-like syntax with minimal delimiters. No escaped quotes. No nested brackets. Just clean, readable code as it can be shown in the image below.

_format before TMDL_
**TMSL (JSON-based)**:

```json
{
  "name": "Total Sales",
  "expression": "SUM(Sales[Amount])",
  "formatString": "\"$\"#,0.00",
  "displayFolder": "Sales Metrics"
}
```

**TMDL**:

```
measure 'Total Sales' = 
    SUM(Sales[Amount])
    formatString: "$"#,0.00
    displayFolder: Sales Metrics
```


**Folder-Based Structure**  
Instead of one large JSON file, TMDL organizes semantic models into separate files:

```
SemanticModel/
├── definition/
│   ├── cultures
│   ├── tables/
│   │   ├── Sales.tmdl
│   │   ├── Customer.tmdl
│   │   └── Product.tmdl
│   ├── database.tmdl
│   ├── expressions.tmdl
│   ├── model.tmdl
│   └── relationships.tmdl
```
<br>

> [!IMPORTANT]  
> This modular structure **enables parallel development**. For example, one developer edits the Sales table while another works on the Customer table. There are no conflicts, no waiting times.

<br>

TMDL exposes every property in the Tabular Object Model (TOM), **including advanced features not available through the Power BI Desktop UI**. This gives developers complete control and transparency over their semantic models and make them less dependent on external third party tools.

### Main advantages of TMDL

**Modular file structure**  
Each table gets its own file. When two developers work on different tables, they edit different files. When done like this, Git can merge the changes automatically with no conflicts.

**Clear and readable syntax**  
DAX and M expressions preserve their natural formatting with no escaped quotes. What you see in Power BI Desktop is what you see in the file.

**Git-Friendly Changes**  
Diffs show exactly what changed:

```diff
// In Sales.tmdl
  measure 'Total Revenue' =
-     SUM(Sales[Amount])
+     SUMX(Sales, Sales[Quantity] * Sales[UnitPrice])
      formatString: "$"#,##0
```

This is immediately understandable. No additional JSON noise. No guessing.

**AI & Automation ready**
As AI becomes increasingly integrated into report development, TMDL's readable format makes it easier for AI tools and automation scripts to understand and modify models. This human-readable structure is **an enabler for the future of AI-assisted development**, where we'll delegate many tasks and save significant time.

## Enabling TMDL 

There are two approaches

### Approach 1: TMDL View as a new tab in Power BI Desktop

TMDL View provides an integrated code editor directly in Power BI Desktop for interactive scripting and bulk operations.

**How to enable:** 

If you are using a Power BI Desktop update older than September 2025

1. File > Options and Settings > Options
2. Preview features > Check "TMDL View"
3. Restart Power BI Desktop

TMDL View was announced GA **late September 2025**. As of the September 2025 release, TMDL View will appear by default in PBI Desktop because it's now a standard, permanent feature.

<img width="493" height="335" alt="Pasted image 20251006145117" src="https://github.com/user-attachments/assets/8d6c2e95-8ec1-4e1c-829c-43a29ddf3898" />


**When to Use TMDL View:**

- Making bulk changes to multiple objects (e.g., updating 50 measure descriptions)
- Quick scripting and testing BEFORE committing to version control
- Learning TMDL syntax by dragging objects into the editor
- Verifying model properties not visible in the standard UI

**Key Features:**

- Drag objects from Data pane to generate TMDL code automatically
- Multi-cursor editing and regex find-replace for bulk operations
- Preview changes before applying (shows diff view)
- Scripts saved with your PBIX/PBIP file for reuse

### Approach 2: TMDL Format for PBIP Files

TMDL as a file format transforms how you save and manage Power BI projects, enabling true version control and team collaboration.

**How to Enable:**

1. File > Options and Settings > Options
2. Preview features > Check "Store semantic model using TMDL format"
3. When saving as PBIP, select "Upgrade" to TMDL

<img width="584" height="465" alt="Pasted image 20251006145435" src="https://github.com/user-attachments/assets/f57f3464-e316-42d3-a3a4-2edef673e743" />


**When to Use TMDL Format:**

- Setting up Git repositories for version control
- Multi-developer projects requiring parallel work
- CI/CD pipelines and automated deployments
- Sharing reusable semantic model components across projects

> [!IMPORTANT]  
> Converting from TMSL to TMDL is a one-way direction. Always backup your files before upgrading.

**What is this new "Store PBIX reports using enhanced metadata format (PBIR)" ?**
[MicrosoftSource](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-report?tabs=v2%2Cdesktop#enable-pbir-format-preview-feature)

**What it does:** Embeds the modern PBIR format inside traditional PBIX files, so you get the benefits of structured JSON files without needing to fully switch to PBIP folders.

**Should you activate it?** Yes for new development work, but note it's still in preview and once enabled, you can't easily revert back.<br>

> [!IMPORTANT]  
> While TMDL View is GA, the full PBIP ecosystem (file format, TMDL for models, PBIR for reports) remains in preview but is stable enough for production use by many teams. GA for PBIP likely coming soon (1-3 months), so most probably Q4 2025.


## Version control: A Game-Changer for Professional Developers

Version control integration is where TMDL delivers its most significant impact on professional development.

Working with PBIX files used to be a bit of a nightmare when it came to collaboration. You couldn't just open one up in a text editor and see what was going on inside.

This created some real headaches:

Git couldn't show  meaningful differences between versions. If you wanted to know "what changed?", you had to open both files in Power BI Desktop and play detective, manually comparing tables, measures, and relationships, or use external tools like ALM Toolkit to compare versions. It was not really fun!

Also, rolling back to a previous version meant searching through  backup files hoping you'd saved the right one at the right time. 

As for collaboration? Well, it was pretty much a game of "save, send the file, and wait for the other person to finish before you could work again."

Now with TMDL, everything changes. We finally get **real source control** for our semantic models.
Every single change gets tracked. You can see who made the change, what exactly they modified (whether it's a specific measure, a relationship, or just a property tweak) and why they made it (thanks to commit messages). <br>

> [!IMPORTANT]  
> You can even link user stories to branches in Azure DevOps. **This is considered a best practice**

<br>

So, to summarize:
### Before TMDL


- Git can't show meaningful diffs
- "What changed?" requires opening the file and manually comparing
- Rolling back to a previous version means finding the right backup file
- Collaboration means "save, send, wait for the other person to finish"

### With TMDL + Git

**Every change is tracked:**

- Who made the change
- What exactly changed (specific measures, relationships, properties)
- Why the change was made (commit message)
- When it happened

**Any version is recoverable:**

- Roll back to last week's version with one Git command
- Create branches for more professional dev approaches

**Code reviews become possible:**

- Pull requests show exactly what's being changed
- Team leads can review DAX logic before it goes to production
- Standards and best practices can be enforced systematically

This is more than a "nice to have", it's the difference between amateur development and professional software engineering practices. So is it game changer ? For sure! <br>


> [!WARNING]  
> This represents a significant change in how we develop Power BI solutions. 
> Concepts like Git, Visual Studio Code, commits, pull requests, merges, and branches are likely new territory for many Power BI developers. Beyond the technical tools, this shift requires adapting and embracing new development and collaborative habits.


## The big picture

TMDL represents Microsoft's recognition that Power BI has evolved towards an enterprise development platform. With that evolution comes the need for professional development practices

**Parallel Development**  
Multiple developers work simultaneously on different parts of the model. No more taking turns. No more overwriting each other's work. 
This can also enable role specialization within the Power BI ecosystem: backend developers focus on data modeling and DAX optimization, while frontend developers concentrate on report design and user experience. This mirroring modern software development team structures. 

**Code Reviews**  
Pull requests with clear diffs enable systematic review BEFORE changes reach production. This creates healthy pressure for better documentation, promotes standardization across projects, and enforces adherence to organizational best practices through peer review.

**Reusable Components**  
Create a perfect date table once, share it across every project. Build standard time intelligence calculation groups and distribute them via internal Git repositories or SharePoint. This library approach to semantic model development will be the focus of upcoming articles in this series. We will see practical patterns for building and maintaining reusable TMDL scripts.

**Knowledge Transfer**  
What previously lived in one senior developer's head is now visible in version-controlled files that anyone can review, learn from, and improve upon.

### For Organizations

**Audit for compliance**  
History of who changed what, when, and why. 

**Quality Assurance**  
Automated testing in CI/CD pipelines validates changes BEFORE deployment to production. This allows one to catch errors early, in an automatic way and reduce production incidents.

**Building Standards**  
You can build and implement organizational standards programmatically. For example "All measures must have descriptions" can become an automated check, not a manual review.

**Disaster Recovery**  
Reduces drastically the point of failure. Repositories can be backed up and replicated.


## Minimal investment, maximum return

"But I'm not a developer!" some might say.

The good news is that TMDL is remarkably approachable. If you understand a Power BI measure in the UI, you can read TMDL. The syntax is intuitive, and Power BI Desktop generates it for you, just drag and drop.

Most developers become comfortable with TMDL basics within hours, not weeks. The return on investment is immediate: bulk operations that previously took an hour now can take 30 seconds.

## Conclusion

TMDL isn't just a new feature, it's Power BI's evolution into a professional development platform. It enables the practices that software development teams have relied on for decades, like: version control, code reviews, parallel development, and reusable components.

You don't have to adopt everything immediately. Start with TMDL View for bulk operations. This will be the focus of this series. Add version control when you're ready. Build your first reusable script when the opportunity arises. Each step delivers value.

The tools are here. The community is building amazing things. The question isn't "Should I learn TMDL?" but "When will I start?"


---

💬 **Let's discuss:**  
Drop your thoughts in the LinkedIn post discussion. Share your TMDL adoption challenges, success stories, or questions. We'd love to keep the conversation going and learn from the community's experiences.
