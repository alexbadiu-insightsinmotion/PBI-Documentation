![18 - Image - Title - Requirements Gathering Specification Templates](https://github.com/user-attachments/assets/43f99a32-f757-470f-bee6-42c760d518fa)

***What content is in a Requirements Gathering Specification Template?***

## General

Reporting projects often fail as too much scope is visualized within the available resources (e.g., time, cost, staff availability, staff expertise, etc.). As well, scope creep is often a major contributing cause to project failure. So, be brutal with scope: include only what is essential, exclude all that you can (be specific!), and defer whatever you can, especially those items with an available workaround.

> \[!IMPORTANT\]
> *Plan for iteration*

To try and get a handle on what are the essential scope items to be included in an iteration of a project, it is useful to **gather requirements** directly from business owners and end users before finalizing a scope.

To that end, question-and-answer **specification templates** in a commonly-used format play an important role. Both the report itself and the environment in which it will be developed, tested, and used are important.

## Report

To serve not only as a starting point for the development of and estimation of the time required for each report but also to help define its’ scope, several items should be described for each report, including:

- What is the name and ID of the report?
- What is the purpose of the report?
- What questions is the report intended to answer?
- Who is/are the intended consumers for the report?
  - i.e., who is the audience?
- What is the source of data to be presented in the report?
- Is there an existing source for the data components of the report?
  - If yes, has this source been certified (if so, by whom?)?
  - If no or unknown, are (will there be) personnel available to validate the data, and how long will this take?
- What is the smallest quantity of data that can answer the question(s)?
  - identify ALL filters that can be used to minimize the number of source records
  - identify ALL aggregations that can be applied to minimize the number of reporting records
  - identify ALL columns that can be removed to minimize the amount of data to be processed
- What business rules must be implemented in this report? Are they inherent in the dataset? Are there any exceptions or special cases?
- What are the formulae for any calculations that are necessary in the report? Are there any exceptions or special cases?
- What visuals are desired on the report?
  - (provide a brief description of each)
- What filters (slicers) are required on the report (if any) for interactivity?
- What key performance indicators (or measures) are desired on the report?
- Is there a mock-up of the report and/or wireframe describing the report?
- Are there samples of existing reports that are currently used that present (some) of this information?
  - If yes, why are they being replaced, what are their shortcomings, and what are the desired enhancements?
- And, most importantly, when is this report needed to be in production?

<table><thead><tr><th><p><strong><em>Item</em></strong></p></th><th><p><strong><em>Description</em></strong></p></th></tr><tr><th><p>Report Name</p></th><th><p>&lt;report name&gt;</p></th></tr><tr><th><p>Report ID</p></th><th><p>&lt;report identifier&gt;</p></th></tr></thead><tbody><tr><td><p>Purpose / Questions</p></td><td><p>What question(s) is the report designed to answer?</p><p>Q1:</p><p>Q2:</p><p>Q3:</p><p>Q4:</p><p>Q5:</p><p>What story is the report designed to tell?</p><p>??</p><p>What decisions is this report designed to enable/support?</p><p>??</p></td></tr><tr><td><p>Audience</p></td><td><p>Who are the intended consumers of the report?</p><p>Who?</p><p>Will the report be shared exclusively to internal users in the organization?</p><p>Yes? No? (if yes, describe how (and to whom) the report will be shared)</p><p>Will the report be shared with external users outside of the organization?</p><p>Yes? No? (if yes, describe how (and to whom) the report will be shared)</p><p>Will the report be shared with other departments? If yes, how?</p><p>Yes? No?</p><p>Will the report be shared publicly? If yes, how?</p><p>Yes? No?</p></td></tr><tr><td><p>Data Source</p></td><td><p>What is/are the source(s) of data for this report?</p><p>??</p><p>Is/are these data source(s) validated (endorsed and certified)? (If not, are client resources available and allocated within the report development timeframe?)</p><p>Yes? No?</p></td></tr><tr><td><p>Filters</p></td><td><p>What filters can be applied to minimize dataset size?</p><p>??</p></td></tr><tr><td><p>Aggregations</p></td><td><p>How can the source data be aggregated to match the level of detail (or grain) required from the report to minimize dataset size?</p><p>??</p></td></tr><tr><td><p>Columns</p></td><td><p>What columns are required and what columns can be removed to minimize dataset size?</p><p>??</p></td></tr><tr><td><p>Business Rules</p></td><td><p>What business rules are to be used in this report?</p><p>?? (those not already inherent in the data; those that must be implemented in the report)</p><p>Are there any exemptions or special cases?</p><p>Yes? No? Describe…</p></td></tr><tr><td><p>Calculation Formulae</p></td><td><p>What are the formulae for calculations that are to be used in this report?</p><p>??</p><p>Are there any exemptions or special cases?</p><p>Yes? No? Describe…</p></td></tr><tr><td><p>Visuals</p></td><td><p>What visuals do you want displayed on the report?</p><p>e.g.,</p><ul><li>Column chart – sales by year</li><li>Bar chart – sales by province</li><li>Matrix – sales by year by product category</li><li>…</li></ul></td></tr><tr><td><p>Slicers</p></td><td><p>What interactive slicers should be used on the report?</p><p>e.g.,</p><ul><li>Date c/w slider</li><li>Customer Name (drop-down list)</li><li>Sales Region (tiles)</li><li>…</li></ul></td></tr><tr><td><p>KPI’s / Measures</p></td><td><p>What KPI’s / measures should be displayed on the report?</p><p>??</p></td></tr><tr><td><p>Mock-up / Wireframe</p></td><td><p>Is there a mock-up and/or wireframe available for the report?</p><p>Yes, see attached</p></td></tr><tr><td><p>Existing Samples</p></td><td><p>Are there existing reports that are currently (or have been historically) to preset (some) of this information?</p><p>Yes, see attached</p></td></tr><tr><td><p>Visual Theme</p></td><td><p>Are there client-specific visual elements that must be used for the environment/reports?</p><p>Colours? Fonts? Logos? Other?</p><p>Are there any exemptions or special cases?</p><p>Yes? No? Describe…</p></td></tr><tr><td><p>Other</p></td><td><p>What other features/items should be displayed on the report?</p><ul><li>Report Last Refresh Date (upper-right corner)</li><li>Company logo (lower-left corner)</li><li>Dataset ID / Version / Version Date (lower-right corner)</li><li>Report ID / Version / Version Date (lower-right corner)</li></ul></td></tr><tr><td><p>Timeframe</p></td><td><p>What is the timeframe for development, validation, deployment, and release of the report?</p><ul><li>Development (2 weeks) (first ½ of February 2025)</li><li>Validation (2 days) (3<sup>rd</sup> week of February 2025)</li><li>Deployment (4 weeks) (March 2025)</li><li>Release (June 1, 2025)</li></ul></td></tr></tbody></table>

## Environment

To serve as a starting point for the development of a new Power BI environment (or the enhancement of an existing Power BI environment), several items should be described, including:

- Is there an established Power BI environment that will be modified/enhanced?
  - Regardless, what type of Power BI license will be implemented/used? Premium? Pro? Free (none)? Report Server (on-premises)?
- How many internal report consumers are anticipated at the start and the end of the project?
- Are there any external report consumers? If so, how many, how, and how often will they access the organizations’ reports?
- Are there multiple environments available/anticipated (e.g., DEV, TEST, PROD)?
  - If so, how is code moved between environments? Are deployment pipelines used?
- Are there validated corporate data sources available within the Power BI environment?
  - If yes, are dataflows used?
  - If not, has time been set aside for validation and resources available for validating the data sources?
  - Regardless, if there are on-premises data source(s) that will contribute to the reports, are there available dedicated workstations configured with Power BI gateways for the DEV, TEST, and PROD environments?
- How many reports will be developed, validated, and deployed by the end of the project?
- Is there a designated pilot group of internal resources who will validate the first stage of a phased deployment?
- Are there existing data sources that can be/have been validated along with connection details? (e.g., data warehouse? database? SharePoint? Other?)
  - If not, are there internal resources available within the project timeframe to validate the existing data sources?
- What is the smallest amount of data that can answer the questions inherent in the anticipated reports? Current fiscal year? Last fiscal year? Last 5 fiscal years?
- Can the source data be aggregated before extraction to minimize the Power BI processing time?
- Has time been allocated in the project timeframe to access/transform/validate the data sources?
- Do any (all?) reports have to de delivered simultaneously in multiple languages? English only? If multilingual, is a phased deployment acceptable (e.g., French and Spanish in version 2.0?)
- What are the report refresh requirements? Annual? Monthly? Daily? Real-time? Other?
- Are there internal resources assigned to do the Power BI administration during and after rollout?

| **_Item_** | **_Description_** |
| --- | --- |
| License | What type of Power BI license is available?<br><br>Premium? Pro? Free (none)? Report Server (on-premises) |
| Report Consumers/Authors | How many internal client resources will interact with the reports?<br><br>??<br><br>How will the internal client resources interact with the reports?<br><br>Browser? Mobile? Power BI Desktop? PDF? Other?<br><br>Are there any external resources who will interact with the reports? (if so, how?)<br><br>??<br><br>How many internal report authors currently exist/are anticipated?<br><br>?? |
| Data Source(s) / Gateways | What is/are the data source(s) for the existing and future Power BI reports?<br><br>??<br><br>Are these data source(s) validated (endorsed and certified)? (If not, are client resources available and allocated within the project timeframe?)<br><br>Yes? No?<br><br>If on-premises data source(s) will be used, have multiple gateways been established to connect the DEV, TEST, and PROD environments to the cloud?<br><br>Yes? No? Describe… |
| Data Volume | What are the filters that can be applied to the source/reporting data to minimize the number of records needed for the reports?<br><br>??<br><br>What are the aggregations that can be applied to the source/reporting data to minimize the number of records used in the reports?<br><br>?? |
| Data Refresh Cadence | How frequently does the data need to be refreshed?<br><br>Yearly? Monthly? Weekly? Daily? Hourly? Realtime? Other? Describe… |
| Environments | Are there separate environments available for Power BI (workspaces)?<br><br>(e.g., DEV, TEST, PROD)<br><br>??<br><br>Are there separate environments available for data sources?<br><br>(e.g., DEV, TEST, PROD)<br><br>??<br><br>If there are separate TEST and PROD environments, is the data in the TEST environment consistent with PROD such that validation is effective?<br><br>?? |
| Deployment | How is code deployed? Are deployment pipelines used?<br><br>?? |
| Language | Will the reports be delivered in English only?<br><br>Yes? No?<br><br>If multilingual reports are also required, can the additional languages be delivered later as a separate release/version/iteration?<br><br>Yes? No? |
| Administration | Are there internal resources assigned to do the Power BI administration during and after rollout?<br><br>?? |
| Visual Theme | Are there client-specific visual elements that must be used for the environment/reports?<br><br>Colours? Fonts? Logos? Other?<br><br>Are there any exceptions or special cases?<br><br>Yes? No? Describe… |
| Security | How is security applied?<br><br>Active Directory? No? Describe… |

## Resources

*LinkedIn Posts*

The LinkedIn post covering the covering the requirements gathering specification templates is:
<br>
[Requirements Gathering Specification Templates](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7310232246613934082-w7iW) *** FIX *** <br><br>

*Samples*

Sample requirements gathering specification templates are available in the GitHub repo:
<br>
[1. Requirements Template - Power BI Report](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2006%20-%20Model%20-%20V0.7.docx) *** FIX *** <br>
[2. Requirements Template - Power BI Environment](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Power%20BI%20File.pbix) *** FIX *** <br>
