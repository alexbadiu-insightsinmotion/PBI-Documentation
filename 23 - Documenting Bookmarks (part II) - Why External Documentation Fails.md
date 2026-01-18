
<img width="2553" height="1272" alt="Pasted image 20260113113538" src="https://github.com/user-attachments/assets/601f0c65-0a0c-40d3-971a-3586a00bd35d" />

<br>
<br>


# Power BI Bookmarks Documentation (Part II): Why External Documentation Fails

<br>

> [!NOTE]  
>**TL;DR**: Article 21 showed how to extract technical details from bookmarks using AI, but left the business justification problem unsolved. External documentation doesn't scale, it requires too much discipline, produces inconsistent quality, and stays disconnected from the tools AI assistants use. This article identifies three critical scalability problems that make external documentation impractical for teams. Part III will introduce the solution: PBIR annotations + Claude Skills.
>


---

In my [previous article on documenting Power BI bookmarks](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/21%20-%20Documenting%20Bookmarks%20with%20PBIR.md), I shared some important discoveries about how bookmarks actually work and how you can extract technical documentation from bookmark PBIR JSON files using AI with smart prompting.

<br>

**But I did not provide a scalable solution for the hardest part that needs to be documented.**
<br>


At the end of that article, I wrote:

> [!NOTE] 
> "What am I missing here is the **why**. It's beyond the technical part. It's understanding the problem we need to solve and the approach we decided to take."

<br>

**I did propose an improvement** that I believe could permanently solve this issue and not just for bookmarks, but for any visual in Power BI. This approach could add immense value not only to the documentation itself, but also provide the necessary context for AI to deliver more qualitative answers when working with semantic models.
<br>

> [!NOTE] 
> **When using bookmarks, we don't store a description field anywhere**. I believe this presents a phenomenal opportunity to create this type of field when generating bookmarks from the Power BI Desktop UI and store the definition in PBIR. While it would still require manual input, this documentation would be created directly in the source system, which is the best and most accessible kind of documentation. **I've submitted a Power BI idea here**: [Add Description field for Bookmarks in Power BI Desktop and PBIR Format](https://community.fabric.microsoft.com/t5/Fabric-Ideas/Add-Description-field-for-Bookmarks-in-Power-BI-Desktop-and-PBIR/idi-p/4818843#M163577). If this concept resonates with you, please vote.

<br>

I submitted this idea, but unfortunately it didn't gain the traction I was hoping for.

If you're reading this blog and this idea resonates with you, **please vote for it**. This is the type of improvement Power BI needs. It may not be spectacular, or "game-changing", but it would significantly enhance the maturity and quality of Power BI solutions.

My hot take for the years to come and the rise of AI:
<br>

> [!TIP] 
> **In the era of AI, planning, organizing, following proven frameworks and documentation plays a critical role.**

<br>
If you do not get better with documentation, you will not be successful in leveraging AI.
<br>
In the meantime, I recommended creating separate documentation manually like a markdown file where you'd document the business context that AI couldn't extract from JSON.
<br>
<br>

**That recommendation was correct. But incomplete.**
<br>

Let's do a recap of what I wrote in the previous blog and build on it.
<br><br>

## What Issue 21 Solved (and what it didn't)

### Successful Technical Extraction
<br>

Issue 21's AI shared prompt gave us excellent technical extraction from PBIR JSON:
<br>

✅ **Bookmark metadata** - Name, group membership, settings (Data/Display/Current Page)  
✅ **Visual mappings** - Which visuals are affected, their visibility states  
✅ **Filter analysis** - Report-level and visual-level filters with values  
✅ **State behavior** - What the bookmark does technically  
✅ **Hidden mechanics discovery** - The "All Visuals" vs "Selected Visuals" revelation
<br>
<br>

For the "FocusSpecific" bookmark examples showcased, we got comprehensive technical documentation: visual IDs mapped to names, filter states for each visual, highlight selections, and complete behavioral analysis.

**This was valuable.** Significantly better than having no documentation or trying to reverse-engineer bookmark behavior from the Power BI UI alone.

### The Key Discovery from Issue 21

Remember what we learned about bookmark scope:

- **True "All Visuals"**: No `targetVisualNames` property in JSON affects all current **AND** future visuals
- **"Selected Visuals"**: `targetVisualNames` property present **only affects listed visuals**, even if you selected all current visuals when creating it

This discovery alone justified the PBIR JSON analysis approach. The Power BI UI can be misleading about actual bookmark behavior.

### What Issue 21 Left Unsolved

AI cannot answer from JSON alone:

- **Did we create this bookmark behavior on purpose?**
- **Was it part of the Definition of Done?**
- **Why did we create this bookmark in the first place?**
- **When was it created, what problem was it intended to solve?**
- **Were other solutions envisaged?**
- **Was it signed off?**
- **Where can I find the documentation of the request or the Definition of Done?**

<br>
My solution in Article 21 was:

> [!NOTE] 
> "Create separate documentation for the 'why' outside Power BI (Excel spreadsheet, markdown file, etc.) where you manually add descriptions for each bookmark."

<br>


**That's where the problems started.**
## The three scalability problems I discovered

After recommending in Issue 21 that teams "create separate documentation for the 'why' outside Power BI," I tried to teach other developers implement this technique and asked for feedback. I learned that while the idea is interesting, it could be difficult to standardize and scale beyond my own work.


<img width="1213" height="1035" alt="Pasted image 20260114073122" src="https://github.com/user-attachments/assets/cf56cc2c-547c-4114-aa45-e892e0d914a5" />


### **Problem 1: Scalability - Too Much to Remember**

The process worked well... for me. Because I created it. I knew:

- Which questions to ask
- What level of detail to capture
- How to structure the documentation
- Where to save different pieces of information
  <br>

**But when I tried to hand this off to other developers:**
<br>

"So I need to:
<br>

1. **Run the AI prompt** to extract technical details
2. **Remember to create the context spreadsheet or markdown file**
3. **Save it** in the right location
4. **Fill in all the questions** you mentioned
5. Remember to **keep it updated** when bookmarks change
6. Make sure the JSON extraction and my notes **stay in sync**?
<br>

That's a lot to remember. Can you write down the exact process?"
<br>

**I created documentation _about_ the documentation process. Then developers needed to reference that documentation _while_ documenting.**
<br>

**This is the scalability problem:** A process that requires remembering multiple steps, saving scripts, keeping notes available, and following a specific workflow will not scale easily beyond the person who created it. It's just too much work, too much discipline.

> [!NOTE] 
> **It's difficult to make others follow your process when the process involves too much remembering.**

<br><br>

### **Problem 2: Standardization - Inconsistent Business Justification**

Even when developers followed the process, the quality varied dramatically.

**Developer A's documentation could be:**

```
Bookmark: FocusSpecific
Purpose: Shows focused view for analysis
```

**Developer B's documentation could be:**

```
Bookmark: FocusSpecific

Business Purpose: Enable sales managers to investigate specific regions when 
unusual performance patterns are detected during monthly review meetings. This 
supports the quarterly planning process by providing quick access to regional 
detail without losing position in the overall workflow.

Created: 2024-07-15
Requested by: Sales Operations team
Approved by: Head of Sales Analytics
Related to: JIRA-1234 - Regional Analysis Enhancement
Alternatives Considered: Drill-through page (rejected due to filter context loss)
```

**Same bookmark. Drastically different documentation quality.**

**The problem:** Some developers don't place the same importance on business justification. They stay too general or explain it in just couple of words. They think "shows focused view" is sufficient because technically, it's accurate.

**And they're not wrong from their perspective.** If you're building the report, you know the context. The documentation feels redundant. The business justification seems obvious.

**What I found myself doing:** Following behind developers, checking their documentation, asking for more details, explaining why we need business context, not just technical description.

**This doesn't scale.** I can't be the quality control checkpoint for every bookmark in every report across every project.

> [!NOTE] 
> **The uniformity and standardization problem:** Without structured enforcement, documentation quality depends entirely on individual developer judgment and discipline. And individual judgment varies wildly.

<br><br>

### **Problem 3: Documentation needs to live in the tool**

This is the most important realization, and it took me too long to understand all the reasons.

**I initially thought:** "Documentation for visual elements like bookmarks, visual calculations in a separate Excel/markdown file is fine. Developers can reference it when needed."

**What I missed:** We're moving toward AI-assisted development. And AI-assisted development changes _where_ documentation needs to live.

**Here's a scenario to make this clear:**

I'm working in VS Code with Claude Code on a Power BI report. I ask:

```
"Claude, I need to modify the FocusSpecific bookmark to also reset 
the product category slicer. What's the impact?"
```

**Without the business justification we could have this reply (ideally):**

```
Claude: "I can see the technical structure of FocusSpecific in the JSON. 
It currently affects the Gender slicer and Clustered Bar Chart. 

To understand the full impact, I'd need to know:
- What's the business purpose of this bookmark?
- Why were only those specific visuals included?
- Are there other bookmarks that depend on the current behavior?

Do you have this context documented somewhere?"
```

Then I need to:

1. **Find the Excel or markdown file**
2. **Look up the bookmark**
3. **Read** the context
4. Make sure the **documentation is updated**
5. **Copy/paste it to Claude**
6. Claude analyzes with that context
7. I get my answer

**With documentation inside the tool itself Claude can provide this answer:**

```
Claude: "I can see FocusSpecific is designed to 'enable sales managers to 
investigate specific regions during monthly review meetings.' 

Looking at the annotations and referenced markdown files, this bookmark is part of a navigation flow:
Overview → FocusSpecific → DetailView

The Gender slicer and Clustered Bar Chart were specifically chosen because 
they need to reset to a clean state for focused analysis, while other visuals 
provide context and should stay.

Adding product category slicer reset would impact:
1. User workflow: Currently product context persists through focus → detail flow
2. Related bookmarks: DetailView expects product filter to be maintained
3. Business logic: Per annotations, Sales Ops requested this specific behavior

Recommendation: Before making this change, verify with Sales Ops whether 
product context should persist or reset. The current design appears intentional."
```
<br>

> [!IMPORTANT]   
>**The difference is dramatic.**


<br>

**When documentation lives in the tool:**
<br>

- AI can read it **without me providing additional context**
- AI **understands not just _what_ the bookmark does, but _why_**
- AI can **assess impact of changes** against business intent
- AI can **warn me when modifications conflict** with documented purpose
<br>

## What these three problems revealed
<br>

Looking at these three problems together, the solution became clear:
<br>

**The process must:**
<br>

1. **Require minimal effort** - Guided workflow, not memorized steps
2. **Enforce uniformity** - Structured questions, not freeform documentation
3. **Live in the source** - PBIR annotations too, not only external files

<br>

**This is why Claude Skills + Claude Code became the answer:**
<br>

- **Scalability**: Developers can simply invoke a skill (in my case`@pbir-documentation` ), the Skill guides them through the complete process
- **Uniformity**: Same structured questions for everyone, same output format
- **AI-ready**: Documentation embedded in PBIR where AI can leverage it

<br>

**Not "try to remember my process."**  
**Not "hope developers document consistently."**  
**Not "maintain separate documentation files."**
<br>

> [!IMPORTANT]  
> **Result: A framework that travels with you, guides you through structured capture, and outputs directly to the source system.**
<br>


But wait, how can we document in the tool when I just said this feature does not exist in Power BI?
<br>

> [!IMPORTANT]
>  While it's not possible to document within Power BI's existing UI, **IT IS POSSIBLE** to leverage **annotations inside the PBIR format**!
<br>


And this changes quite a lot.
<br>
### Why this deserves attention now
<br>

This is not just about incremental documentation improvements. **The underlying format and tooling are already changing.**
<br>

Starting in **January 2026**, PBIR becomes the default format in Power BI:
<br>

- All new reports created in the Power BI Service use PBIR
- Existing reports convert to PBIR when edited and saved
<br>

At the same time, **VS Code, Git, and GitHub/Azure DevOps are becoming the standard environment** for professional Power BI development.
<br>

Importantly, **you are not _forced_ to actively work with PBIR**. You can continue using Power BI Desktop and PBIX files as before.
<br>

However, that choice has consequences.
<br>

**What changes regardless:**
<br>

- Your reports are stored in PBIR format either way
- The underlying capabilities are present, even if you don’t surface or use them
- AI tooling increasingly operates on these code-level artifacts
<br>

**What you miss by ignoring them:**
<br>

- Structured annotations that AI can read and reason over
- Integrated documentation that evolves with the report
- Version-controlled context explaining _why_ decisions were made

<br>

### The emerging productivity gap
<br>

Teams that adopt PBIP/PBIR workflows and AI-assisted tooling are beginning to see **multiplicative effects over time**, particularly in:
<br>

- Documentation coverage and consistency
- Change impact analysis
- Onboarding and maintainability
- Decision quality when modifying existing reports

<br>

This is not about instant “10x productivity.”  
It’s about **compounding advantages** as AI can increasingly assist with analysis, refactoring, and governance **_because the context is available in the source artifacts_**.
<br>

**Opportunity cost over time:**
<br>

- PBIR annotations: *available but unused*
- AI agents: *capable, but context-blind*
- Version control: *present, but under-leveraged*
- Business intent: *known by people, invisible to tools*

<br>

### Two reasonable paths forward
<br>

Most teams will naturally fall somewhere on a spectrum, but broadly speaking:
<br>

1. **Maintain current practices**  
    Continue working primarily in Power BI Desktop, rely on external documentation, and adopt new tooling gradually as required.

<br>

2. **Intentionally adopt PBIP/PBIR workflows**  
    Learn how PBIR works, introduce in-source documentation practices, and enable AI-assisted development in a controlled, deliberate way.

<br>

This is not about being “forced” versus “resisting change.”  
It is about whether you choose to **surface and leverage capabilities that already exist**.
<br>

> [!WARNING]
>  Teams that don’t adapt will increasingly struggle to match velocity and maintainability, even if the gap isn’t immediately visible.


<br>

## AI-assisted BI development is no longer theoretical

Several developments over the past months point in the same direction:
<br>

**November 2025 – Microsoft Ignite**
<br>

- Introduction of the **Power BI Modeling MCP Server**
- Early but official AI integration paths for Power BI semantic model
- AI tools can inspect and interact with Power BI artifacts under controlled conditions

<br>

**December 2025**
<br>

- Anthropic introduced **Claude Skills** as an open standard
- OpenAI adopted similar patterns for **Codex CLI**
- Reusable, structured AI workflows become portable across environments

<br>

**January 2026**
<br>

- PBIR becomes the default report format
- Code-first Power BI artifacts become the norm, not the exception

<br>

Taken together, the **building blocks are now in place**:
<br>

- Code-friendly artifacts (PBIR / PBIP)
- Tool-level access (MCP)
- Portable AI workflows (Agent Skills)

<br>

What remains is not technology, but **governance, conventions, and team practices**.
<br>

This shift is already underway. The Power BI community is only beginning to adapt.
<br>

---
<br>

## What this means for your career
<br>

Over the next 12–18 months, the difference between Power BI developers will increasingly come down to **how they work**, not just what they build.
<br>

Some will:
<br>

- Use AI as a genuine development partner
- Maintain context-rich, evolvable solutions
- Build reusable systems that improve over time

<br>

Others will:
<br>

- Rely primarily on manual workflows
- Struggle to reason about legacy reports
- Spend more time maintaining than evolving solutions

<br>

The skills that enable the first path: **PBIR literacy, in-source documentation, AI-assisted workflows** are not niche. They are on track to become **baseline expectations**.
<br>

Learning them early doesn’t make you radical.  
It makes you prepared.
<br>

### The ROI is practical, not theoretical
<br>

Even without full AI automation, **in-tool documentation already delivers tangible returns**, primarily by reducing friction, rework, and uncertainty.
<br>

**Observed benefits in practice:**
<br>

**Time & Effort**
<br>

- Structured PBIR annotations drastically reduce the overhead of documenting bookmarks
- Developers spend minutes capturing intent _once_, instead of repeatedly rediscovering it later
- Manual documentation steps (separate files, context switching, syncing) largely disappear

<br>

> [!TIP]
> **Documentation moves from being “extra work” to being part of the development flow.**
<br>
---
<br>

**Quality & Coverage**
<br>

- Documentation coverage increases significantly because capture is guided and embedded
- Output becomes consistent across developers, regardless of experience
- Business intent is preserved alongside technical definition
<br>
---
<br>

**Operational Impact**
<br>

- Faster and safer changes to existing reports
- Reduced onboarding time for new team members
- Fewer regressions caused by misunderstood bookmarks
- More reliable AI assistance because intent is visible
<br>

These benefits **compound over time**:
<br>

- Each documented bookmark reduces future investigation effort
- Each annotation improves AI’s ability to reason about impact
- Each report becomes easier to evolve instead of rewrite

<br>

> [!IMPORTANT]
>The real return is not just time saved today, but **maintenance effort avoided tomorrow**.

<br>

---
<br>

### Why this matters long-term
<br>

As AI becomes more embedded in Power BI development workflows, **solutions with embedded context will benefit disproportionately**:
<br>

- AI can explain, warn, and suggest, not just generate
- Teams spend less time re-learning old decisions
- Architecture becomes more intentional, not accidental

<br>

This is not about chasing short-term productivity gains.  
It’s about **building systems that scale with people, tooling, and time**.
<br>

## Conclusion
<br>

I’ve identified three fundamental issues with external documentation for Power BI bookmarks:
<br>

1. **Scalability** – Processes that rely on memory, discipline, and manual steps do not scale across teams
2. **Standardization** – Documentation quality varies widely depending on individual judgment
3. **AI visibility** – External files remain invisible to the tools increasingly used to build and evolve solutions

<br>

These are not minor inconveniences.  
They are **structural limitations** that prevent documentation from scaling beyond individual developers.
<br>

Traditional approaches like spreadsheets, markdown files, shared folders can still work in certain contexts:
<br>

- Small teams
- Limited report complexity
- Minimal AI involvement
- Documentation treated as a purely human activity
<br>

However, these assumptions are becoming harder and harder to rely on.
<br>

Power BI is moving toward **code-based artifacts**, **source control**, and **AI-assisted development**. As that happens, documentation that lives _outside_ the system becomes harder to maintain, harder to trust, and harder for both humans and AI to use effectively.
<br>

The question is no longer whether documentation matters.  
It’s **where it should live and how it should be captured**.
<br>

In **Part III**, I’ll walk through a concrete solution using **PBIR annotations combined with Claude Skills**, including:
<br>

- How annotations work in PBIR and why they’re well suited to this problem
- A guided documentation framework that enforces consistency without relying on discipline
- Real-world annotation structures and example
- Practical guidance for introducing this approach into a team

<br>
The problems are now clear.  
The tooling is available.  
What remains is adopting practices that align with how Power BI development is actually evolving.
<br>

**Let’s build something that scales.**

<br>

---
<br>

**Next**: [Part III: The Solution - PBIR Annotations + Claude Skills](link-to-part-3)

<br>
---
<br>

**For questions or comments about this article, contact:** Alexandru BADIU
<br>
**If you found this valuable, please:**
<br>

- Vote for the [bookmark description field idea](https://community.fabric.microsoft.com/t5/Fabric-Ideas/Add-Description-field-for-Bookmarks-in-Power-BI-Desktop-and-PBIR/idi-p/4818843#M163577)
- Share this article with your Power BI team
- Follow my work on [GitHub](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation)
