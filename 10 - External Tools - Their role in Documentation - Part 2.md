
<img width="1920" alt="Issue 10" src="https://github.com/user-attachments/assets/e161a459-db94-4207-88d8-81300a6291ca" />

##### Table of Contents  
[External Tools - Their Role in Documentation - part 2]() <br>
	&nbsp;&nbsp;[1. Measure Killer](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/10%20-%20External%20Tools%20-%20Their%20role%20in%20Documentation%20-%20Part%202.md#1-measure-killer) <br>
	&nbsp;&nbsp;[2. PowerOps](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/10%20-%20External%20Tools%20-%20Their%20role%20in%20Documentation%20-%20Part%202.md#2-powerops) <br>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.1 Bookmark Documentation](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/10%20-%20External%20Tools%20-%20Their%20role%20in%20Documentation%20-%20Part%202.md#bookmark-documentation) <br>
    	&nbsp;&nbsp;[3. TMDL Explorer](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/10%20-%20External%20Tools%20-%20Their%20role%20in%20Documentation%20-%20Part%202.md#3-tmdl-explorer) <br>
        &nbsp;&nbsp;[4. SQL Server Profiler](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/10%20-%20External%20Tools%20-%20Their%20role%20in%20Documentation%20-%20Part%202.md#4-visualize-model-refresh---sql-server-profiler) <br>
	&nbsp;&nbsp;[Quick Recap](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/10%20-%20External%20Tools%20-%20Their%20role%20in%20Documentation%20-%20Part%202.md#quick-recap) <br>
<br><br><br>

   


If you're in charge of Power BI development and documentation is "your territory", **you're the one** who makes things happen. You need the right tools to keep your things clean, efficient and under control. 

A reminder from the previous post:  
| :exclamation:  When we finalize documentation, we document excellence.   |
|-----------------------------------------|


To achieve this, we need the right:

- **Mindset**
- **Knowledge**
- **Tools**
- **Approach**

*This sequence is intentional. The primary driver is mindset paired with business knowledge and needs. While technical discussions about methods and tools are valuable, organizations invariably follow a **BUSINESS - PROCESS - PEOPLE** hierarchy. Business needs create the foundation for processes, and only then do people require tools and actions to support them.*

This week, we continue our conversation about the role of external tools in documentation. **We'll review other external tools we have at our disposal, examine various options, and explore how to leverage them** to create not only more polished reports, but also enhance visual documentation, or simply assess our current progress.
<br><br>

>[!Warning]
>**A word of caution**: Don't expect an exhaustive list of all tools available —there are many other tools inside or outside the Microsoft ecosystem. I have no allegiances, no strings attached. The opinions are entirely my own. What I'm sharing are practical insights drawn from my actual field experience, deliberately focusing on a highly curated selection of tools.
<br><br>

Before diving in, I must emphasize **the golden rule: Process is king! No tool performs miracles without a solid process behind it.**

Let's be honest: Expecting developers to maintain documentation solely out of goodwill is simply unrealistic. **We require strong, well-defined processes.**
<br><br>
### Robust processes: The documentation enforcer

One example of a typical process to enforce documentation is the **code review process**. It is typically part of a broader CI/CD ( [Continuous Integration/Continuous Deployment](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-build-pipelines) workflow triggered by Pull Requests. This is where documentation transforms from a nice to have to a critical requirement. 

No documentation? Bye bye Go to Prod. Straightforward and non-negotiable.

| :exclamation:  **It's not personal, it's strictly business**   |
|-----------------------------------------|

This being clarified, let's meet our "team".
### 1. Measure Killer

This external tool doesn't negotiate - **it eliminates!
And what's the target? The Power BI threat is the Data Clutter.**

In the world of Power BI, clutter is one of the main enemies. It's always there, waiting to sneak inside the projects. 

Unnecessary elements always have the habit of creeping into the semantic model, and gradually:

- **Slow down report performance**
- **Complicate the development process**
- **Make semantic models difficult to understand**
- **Create a snowball effect of complexity**

Without a strong hand to control it, this clutter can transform your once-efficient project into a nightmare that ultimately costs you money.
<br><br>
**Why Measure Killer?** 

Measure Killer helps keep your Power BI environment clean and efficient. Its main purpose is to identify and remove unnecessary measures, columns, and tables from your semantic model.

During code reviews, having only essential elements in your model is a key requirement. This is especially important in self-service semantic model datasets, because removing unused elements becomes much harder once reports are built on your dataset.

*While Measure Killer's free version provides fundamental cleanup capabilities, their paid version offering delivers advanced features addressing, among others, the before mentioned challenges.*
[Measure Killer | Brunner BI](https://en.brunner.bi/measurekiller)

*An example of "Measure Killer" audit.*<br><br>
<img width="634" alt="Pasted image 20250405154916" src="https://github.com/user-attachments/assets/94ccd58a-01bf-4698-a9bd-dc17fbe82eab" />



Another feature I appreciate using is the integration and the scoring methodology built on top of Best Practice Analyzer.  
Ensure your reports avoid the "blood red" classification of "Power BI criminal"! ;)

<img width="388" alt="Pasted image 20250405155427" src="https://github.com/user-attachments/assets/efa6c3bb-1f08-4b05-a255-c21524f7c1fd" />


<img width="374" alt="Pasted image 20250405155614" src="https://github.com/user-attachments/assets/1a43a3d8-c534-4a0d-bab1-29ba05eab173" />




<br><br>


>[!NOTE]
>One of the main advantages of Measure Killer is its ability to pinpoint inconsistencies and unused elements in your Power BI report. This makes it an excellent tool for managing your work effectively. The premium version expands these capabilities to cover your entire Power BI Service environment.
<br><br>

### 2. PowerOps

*Overview of the external tool*
[Powerops](https://powerops.app/downloads)
<img width="1274" alt="Pasted image 20250405161028" src="https://github.com/user-attachments/assets/d8e983e0-4cae-445f-8ba6-2b1e1017aec3" />



**Learn more** - *I recommend reading the following article for a more in depth overview:* [Meet Powerops - Your New Best Power BI "External Friend"! - Data Mozart](https://data-mozart.com/meet-powerops-your-new-best-power-bi-external-friend/)


This tool functions as your "intelligence agent". Imagine inheriting a report with zero documentation and needing to understand its entire ecosystem quickly. That's where PowerOps becomes your secret weapon. It helps you visually and intuitively find the information you are searching for.
<br><br>
>[!TIP]
>In my assessment, this external tool is **excellent to enhance your documentation visually**. By incorporating well-defined visual analyses in addition to text, you improve documentation readability by making key elements more prominent and memorable, facilitating easier reference when seeking specific data later.
>
<br><br>
Consider the following jobs: 

- **Visualize Measure Dependencies**: Discover measure branching patterns and measure-to-column relationships
<img width="581" alt="Pasted image 20250405161513" src="https://github.com/user-attachments/assets/501015de-be29-400a-a2a5-26d081ea0844" />


<br><br>
>[!Warning]
>**Measure branching** is a powerful strategy to **break down complex calculations into smaller, more reusable parts**. It typically improves readability and maintainability, but if taken to an extreme, it can become a maze of dependencies that’s difficult to troubleshoot and optimize.
>
>There’s no “official” rule from Microsoft or the community stating a strict limit. A common recommendation is to **keep branching at a max of 2–3 layers deep**. Beyond that, you risk confusion and performance overhead if measures are heavily nested.
>
>**Why keep it modest:**
>
>1. **Performance**: Each measure reference can add overhead, especially in complex or large models.
>2. **Readability**: Deeply nested measure references become difficult for other developers (and even you, months later) to follow.
>3. **Debugging & Optimization**: Tracing an issue through multiple layers of measures is time-consuming.
<br><br>

>[!TIP]
>**Recommendations:**
>- Group common logic into “base measures” that are used repeatedly (e.g., “Base Sales,” “Base Costs,” etc.).
>- Build a second layer of measures that do simple transformations on those base measures (e.g., YTD, MTD, Growth Rate, etc.). Consider building calculation groups if the pattern is often used.
>  Reserve a third layer for exceptional scenarios only.
>
<br><br>

*Example of more complex measure branching*
<img width="739" alt="Pasted image 20250405162624" src="https://github.com/user-attachments/assets/23f03956-83ed-42d1-b56b-2b56e310875f" />


>
- **Trace Measure Usage**: Identify which measures power each graph or page 

<img width="894" alt="Pasted image 20250405161657" src="https://github.com/user-attachments/assets/e3c19bda-13d3-4952-a3ee-da870f16fc48" />


- **Understand Power Query Dependencies** : Easily visualize your sources 
<img width="743" alt="Pasted image 20250405161809" src="https://github.com/user-attachments/assets/c5d78836-5568-4488-befe-8d1340385a39" />


- **Best Practices Comparison**: Automatically benchmark reports against industry standards

This tool also incorporates Best Practice Analyzer. What I value in this experience is the concise explanation of why each rule constitutes a best practice.

<img width="1135" alt="Pasted image 20250405163812" src="https://github.com/user-attachments/assets/e315c0f8-b315-4493-a82c-cde7160df149" />



- **Comprehensive Overview**:
	- Page-level insights
	- Most frequently used visuals
	- Action tracking
	- Custom visual identification

<img width="1160" alt="Pasted image 20250405164911" src="https://github.com/user-attachments/assets/d259a41d-12ac-4dd4-9cc0-33beda8f98cb" />



<img width="1157" alt="Pasted image 20250405164255" src="https://github.com/user-attachments/assets/a9825187-ff74-4485-8d61-0f0afab0bda9" />


<br><br>
These views offer **a wealth of information in a user-friendly format.** 

- [x]  **Detailed Analysis**: Allows you to inspect each page—including hidden visuals—to understand layout, utilized fields, applied filters, active measures, synced slicers, and more.
- [x]  **Thorough Documentation**: Captures and integrates a wide range of details into your Power BI report documentation, serving as an excellent resource for verifying every component.
- [x]  **Optimized Element Management**: Helps you check that all components are properly renamed and only the essential ones are kept.
- [x]  **Dashboard-Like Transparency**: Provides a clear, dashboard-style overview of your report's underlying components, enhancing client transparency and demonstrating your meticulous, organized, and detail-oriented approach.
<br><br>
- **Bookmarks**: 
PowerOps accomplishes what most tools cannot, **it helps document bookmarks!**

Let's briefly discuss Power BI bookmarks for context before exploring how PowerOps assists with bookmark documentation.

#### Bookmark documentation
>[!WARNING]
>Bookmarks are the weakest point of Power BI reports. While they offer great flexibility for report building, they present significant documentation challenges. **When problems occur, even minor ones, bookmarks typically require complete reconstruction** rather than simple fixes. This makes knowledge transfer and handover processes particularly difficult.
<br><br>
##### Why bookmarks are difficult to document?

###### 1. Not enough metadata
Bookmarks capture the visual state (i.e., filters, slicers, and selected visuals) at a particular moment, but they don't store detailed metadata about why certain settings were chosen, the underlying data relationships, or the business logic behind them. Also, there's no built-in way to search through bookmarks to find which ones contain specific visuals or settings.

###### 2. Maintenance Challenges:  
Since bookmarks are manually created, any change in the report (like renaming visuals, modifying filters, or updating data models) might break the bookmark’s intended context. This makes ongoing maintenance time-consuming and error-prone especially if testing is manual.

###### 3. Static Nature vs. Dynamic Data:  
Bookmarks only capture fixed snapshots. When working with changing data, you may need more dynamic controls. In these situations, you can quickly encounter bookmark limitations.
<br><br>
>[!IMPORTANT]
>**Microsoft’s Direction**:  
>Microsoft has been moving toward reducing reliance on bookmarks by introducing enhanced visual interactions and native features (such as field parameters and better filtering options) that provide more dynamic and context-aware ways to manage visuals. This evolution indicates a preference for more robust, self-documenting features over bookmarks.

<br><br>

**What are the best practices to document Bookmarks today?**

1. **Create a dedicated hidden page inside your Power BI report**
	- **Inventory**: List each bookmark with its name, purpose, and the specific page/visuals it affects.
	- **Visual representation**: Include screenshots or thumbnails of the report state that each bookmark represents. This visual cue helps users quickly understand the context of each bookmark.
2. **Manual descriptions**
	Since Power BI doesn’t provide a native description field for bookmarks, create a table on your documentation page where you can detail:
	- **Purpose**: What the bookmark is intended to highlight or achieve.
	- **Components Affected**: Which visuals, filters, or slicers are included.
	- **Usage Scenarios**: When and why a user should select that bookmark (e.g., "Used for end-of-month summary" or "Focus on product category breakdown").
<br><br>
>[!IMPORTANT]
>Including bookmarks in your documentation is crucial as it serves as a **training resource for new team members and handover materials.** This reduces dependence on original creators and maintains consistency over time.
>
<br><br>

>[!TIP]
>- **Don't use too many bookmarks** 
>Keep it simple with just a max of 5-10 essential bookmarks per report. Too many bookmarks make your report hard to maintain.
>- **Choose bookmarks carefully** 
>Use bookmarks only for important navigation and storytelling. Group and name them logically by how they're used (like "Overview" or "Detailed Analysis"). Also, rename and group visual elements on your page - this makes selection easier when creating bookmarks. For example, grouping 10 related visuals into one named group lets you select them all at once instead of individually.
>- **Clean up regularly** 
>Check your bookmarks often. Delete ones you don't use much or that could be created differently as new features are introduced. This makes your report simpler and easier to test.


<br><br>

Let's come back to PowerOps now and see how it helps us document bookmarks:
I created three bookmarks in the demo file.

**1st Bookmark** is a straightforward one, it impacts all visuals on the page and their underlying data.

<img width="320" alt="Bookmark1" src="https://github.com/user-attachments/assets/32a5103a-ee92-4079-8463-4d010667ff06" />



<br><br>
**2nd Bookmark** is a bit more complex. Only 1 visual slicer is impacted by the selected visual
*UI limits today: what is the selected visual used for the second bookmark?*

<img width="323" alt="Bookmark2" src="https://github.com/user-attachments/assets/6011614c-5530-41e5-8798-5667c30cdc61" />


<br><br>
**3rd Bookmark** is what I call "the documentation nightmare". Multiple visuals are impacted by the bookmark, data is not ticked, selection items not renamed or grouped in an intuitive way.

<img width="319" alt="Bookmark3" src="https://github.com/user-attachments/assets/fe92d7c4-ffc1-4514-9bab-b34eea1b0a7a" />


<br><br>
 PowerOps provides a very useful view where we can see the settings chosen. It's the same information we can obtain if we check the individual bookmarks on Power BI, but in a format we can snip or export easily.



export excel
![Pasted image 20250406154020](https://github.com/user-attachments/assets/8476d8c2-6a69-4644-ad91-fc7d049ea9c9)



What we cannot find is information about which visuals were selected in bookmarks. External tools like PowerOps can help document some bookmark aspects, but they still can't fully compensate for Power BI's lack of searchable bookmark metadata, particularly regarding which visuals were selected in each bookmark. This limitation reinforces why proper documentation is essential.

<br><br>
>[!NOTE]
>PowerOps' greatest strength, in my view, lies in its clean interface and visually engaging insight summaries that integrate perfectly into documentation. Combining meaningful images with contextual text follows the 'Show and Tell' best practice employed in Power BI reports (data storytelling). This substantially enhances overall documentation value.
>
<br><br>


### 3. TMDL Explorer 

This is an innovative app, the first I discovered to harness TMDL.
As the potential of TMDL continues to be uncovered and the community shares new, practical use cases, we can expect a growing array of tools designed to help us visualize data relationships and/or create scripts that accelerate Power BI development. We're still in the early stages, so the scope for innovative new tools is vast.

**TMDL Explorer allows one to:**
- Visualize the connections between measures in your semantic model
- Easily identify both upstream and downstream dependencies

**How to use it**  
1. Go to your TMDL view  
2. Copy table TMDL to clipboard  
3. Paste into the app  
4. Explore your measures

[Source post on LinkedIn](https://www.linkedin.com/posts/maxanatsko_powerbi-tmdl-datamodeling-activity-7305923704616611841-BOvZ/?utm_source=share&utm_medium=member_android&rcm=ACoAAAd2rAYBtqG-2bVNWh14j0hOzgmbFYqs3hE)

<img width="938" alt="Pasted image 20250313135846" src="https://github.com/user-attachments/assets/27e95ea9-5340-4da1-aae8-1a5fa4928eaf" />




<br><br>
### 4. Visualize Model Refresh - SQL Server Profiler

Ever wondered why a Power BI dataset refresh takes so long? Phil Seamark presents a method for capturing events during a Power BI refresh and transforming this data into visual reports that illustrate these events.

In his article [Visualise your Power BI Refresh](https://dax.tips/2021/02/15/visualise-your-power-bi-refresh/), Phil provides comprehensive details. Below is a condensed overview highlighting key steps and the documentation value of this output. For deeper insight into graph interpretation, I recommend reading Phil's complete blog post.

#### Process overview:

##### 1. Launch the Traces 
Begin by initiating the traces to capture events.

![Pasted image 20250325140444](https://github.com/user-attachments/assets/37dd5fa5-bea9-4227-9ec1-91c39a528af2)



![Pasted image 20250325140452](https://github.com/user-attachments/assets/cf5e6fcf-4d48-42f3-870a-6f1b8adb9611)



##### 2. Trigger the Semantic Model Dataset Refresh and Save XML file 
Start the refresh process and save the resulting traces. 

Save the trace file
![Pasted image 20250325140529](https://github.com/user-attachments/assets/e9eea18c-5dc6-407c-840c-2e786221b68a)


##### 3. Update Parameters
Use the provided Power BI PBIX (developed by Phil Seamark) and update parameters.

![Pasted image 20250325140547](https://github.com/user-attachments/assets/54d0d286-c087-4be1-9838-034a9600414b)



##### 4. The results
Visualize and Document Model Refresh

![Pasted image 20250324181506](https://github.com/user-attachments/assets/5aa82ff2-47c5-4ce7-a0a1-4ab6419a8c28)



#### Why Visualize and Document Model Refresh?

- **Transparency and Clarity:**  
    When you can see the refresh process, it's easier to understand how different data sources work together. Adding this to your documentation helps all parties involved understand how data moves and depends on other data.
    
- **Troubleshooting and Optimization:**  
    Visuals make it easier to spot where things might be slowing down or breaking. When something goes wrong, having these diagrams helps you quickly find the problem area, which saves a lot of time fixing it.
    
- **Knowledge Transfer and Onboarding:**  
    Good refresh process documents are really helpful when new people join the team or when handing over projects to someone else.
    
- **Performance Monitoring:**  
    Having documents about your refresh process lets you track how well it's performing over time.
    
- **Stakeholder Communication:**  
    It helps non-technical people understand how data updates work, which makes them trust your reports more.
    
- **Audit and Compliance:**  
    Detailed visual maps of your refresh process help meet compliance requirements and create audit trails. They make each step transparent for any needed reviews.
    

#### Integration with Power BI Documentation:

Incorporating visual model refresh diagrams into your overall project documentation aligns with best practices by providing a comprehensive view of your Power BI solution. This complements documentation on data sources, transformations, and visualizations, creating a complete picture of end-to-end data flow. It also enhances maintainability and scalability while establishing a foundation for continuous improvement.

### Quick Recap

In Issue #10, we explored various tools that not only enhance your work but also ensure the quality of your output. We discussed their advantages, what they bring to the table, and how best to leverage them. However, I want to stress again that these tools are not a replacement for proper documentation, they act as accelerators and aides. In a broader sense, they are part of a process driven by a genuine need.

💬 Let’s discuss:

What’s your go-to tool for Power BI documentation?
What’s the biggest challenge you’ve faced in keeping reports well-documented?
Drop your thoughts in the LinkedIn post: We’d love to keep the discussion going! LinkedIn post: [#Issue 10 - External Tools - Their Role in Documentation - Part 2](https://www.linkedin.com/posts/alexandru-badiu_powerbi-documentation-dataanalytis-activity-7315308684941688833-7Dn3?utm_source=share&utm_medium=member_desktop&rcm=ACoAAAd2rAYBtqG-2bVNWh14j0hOzgmbFYqs3hE)
