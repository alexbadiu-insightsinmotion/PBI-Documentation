<img width="1920" alt="05 - Image - Title - Workflow Issues Business Rules" src="https://github.com/user-attachments/assets/cd70cfda-307e-4009-8403-2fc749f53cf7" />

**How can you record Workflow, Issues, and Business Rules in a Design Document?**

Provide high-level descriptions of the data provision and preparation *workflow*, including all steps from the moment the data is initially accessed from the operational sources until the consumption of the report(s) by the end users. This includes methods, processes (manual, automated), accounts (permissions), and schedules. 

Identify *issues* and resolve them during a project. Having their resolution clearly stated is essential for the design and acceptance of the solution. Documenting their evolution not only traces the decision process but also can be a useful reference for retrospectives and future projects.

Document the corporate *business rules*, as filters and calculations are often organization-specific. This increases solution acceptance as all stakeholders (e.g., analyst, developer, and tester are using the same algorithms.

This issue deals with the Workflow, Issues, and Business Rules major sections, and the remaining sections will be covered in subsequent issues.

## Workflow

Assign an order to each step using a numbered list. Prevent misunderstandings by creating a simple flowchart to illustrate the workflow.

Here's an example:

1. Invoice data will be extracted from the corporate financial system manually by employees using personal accounts on a scheduled basis (daily at 11:00 pm) and will be stored as a series of CSV files in dedicated SharePoint folder.
2. Customer data will be extracted from the corporate customer relationship management system automatically by PowerShell scripts on a scheduled basis (daily at 11:00 pm) using a service account with full access to all records and will be stored as a series of CSV files in a dedicated SharePoint folder.
3. The data will then be imported into raw (untransformed) staging tables in the Power BI Service on a scheduled basis (daily at 1:00 am) automatically by a series of Power BI dataflows.
4. The data in the staging tables will then be transformed into reporting tables in the Power BI Service on a scheduled basis (daily at 2:00 am) automatically by a series of Power BI dataflows.
5. The data in the reporting tables will then be automatically loaded into a common semantic model (dataset) in the Power BI Service on a scheduled basis.
6. The end user will then use a browser to access on-demand the [Invoicing] Power BI App in the [Invoicing] Power BI workspace and select the desired page in the desired Power BI report (which uses the data from the common semantic model).

A flowchart of the data workflow is:<br>
![05 - Image - Workflow Flowchart](https://github.com/user-attachments/assets/ed2b9adc-a5f1-4d93-8018-f6710b22cfe1)

## Issues

Issues (i.e., the **what**) will be identified and resolved during a project. Recording the status history allows one to follow the decision-making process as **why** and **who** are two commonly asked questions when an item (e.g.,  feature, behaviour, procedure, etc.) is included or excluded.

Assign an ID and (short) name to each issue, describe it, and use a status to record all activity along with the relevant status level (e.g., NEW, CRITICAL, NOTE, IN PROGRESS, RESOLVED, DEFERRED, etc.) and date (use a consistent and unambiguous date format [e.g., yyyy-mm-dd, dd-mmm-yyyy, etc.]).

Here's an example:

| <div style="width:20px">*ID*</div> | <div style="width:100px">*Name*</div> | *Description* | *Status* |
| --- | --- | --- | --- |
| *I-1* | *Data Access* | *Access the CRM system using a dedicated service account with full permissions to access all records* | *NEW (2024-10-01):* <br>1. *[Specific Person Name] in IT department to pursue creation of service account for source system data access* |
| *I-2* | *ETL Process - Part 1: Extract* | *Scheduled PowerShell scripts to automatically extract raw data from the operational CRM system and load them into CSV files in a dedicated folder in the SharePoint environment* | *NEW (2025-02-03):*   <br>1. *[Specific Person Name] in DEV department to be responsible for the development of an ETL process to get the raw (untransformed) data into the reporting environment*   <br><br>*IN PROGRESS (2025-02-10):* <br>2. *[John Doe] has created a series of PowerShell scripts to read the raw data from the operational CRM database, store it in CSV files, and load it into the SharePoint environment* |
| *I-3* | *ETL Process - Part 2: Transform* | *Scheduled Power BI dataflows to automatically load the raw data from the CSV files in the SharePoint environment, transform the data into staging tables, and combine tables in the Power BI Service to support the data model* | *NEW (2025-02-10):* <br>1. *[Specific Person Name] in DEV department to be responsible for the development of a series of Power BI dataflows to transform the raw data into usable reporting data in the reporting environment* <br><br>*IN PROGRESS (2025-02-17):* <br>2. *[Sue Smith] has created prototype dataflows to read the SharePoint data and transform it into Power BI staging tables* |
| *I-4* | *Data Filtering* | *Operational data from the current and previous fiscal years only will be loaded (i.e., no historical or archive data)* | *NEW (2025-02-03):* <br>1. *A request was submitted to [Specific Person Name] (the business owner for the reports) to state the data quantity that would be extracted* <br><br>*RESOLVED (2025-02-10):* <br>2. *[Nancy Jones] confirmed that operational data from the beginning of the previous fiscal year would effectively answer the reports' intended questions* |

## Business Rules

Business rules and calculations are not universal. Different organizations, and even different groups within an organization, often have unique understandings for a **rule**, be it a definition, algorithm, or filter. To ensure that all team members (not to mention those others who will be interacting with the solution) use the same rule, it is a good idea to document the rule, even if it seems like you're *"restating the obvious"*. The cost to a project or organization in decreased reputation, decreased goodwill, increased resources (time and cost), and opportunity costs of having the business, developers, or testers using different rules is an unnecessary expense. To paraphrase a common sports reference, the use of different rules by different groups is an **unforced error**. With a small amount of effort, such errors can easily be avoided.

Assign an ID to each business rule, describe it, and use a status to record all activity along with the relevant approval status level (e.g., NEW, DRAFT, DISCUSSION, REVISED, APPROVED (by whom), etc.) and date (use a consistent and unambiguous date format [e.g., yyyy-mm-dd, dd-mmm-yyyy, etc.]). Include all business rules that will be used in the data transformation, calculation, acceptance testing, and deployment, and end use processes.

Here's an example:

| <div style="width:30px">*ID*</div> | *Name* | *Description* | *Status* |
| --- | --- | --- | --- |
| *BR-1* | *Active Customer* | *A customer with over 1,000 employees who has paid an invoice for a product or service delivered within the last 12 months.* | *DRAFT (2025-02-03):* <br> 1. *“Any customer who has made a purchase”.* <br> 2. *A request was submitted to [Specific Person Name] in the sales department for confirmation* <br><br> *APPROVED (2025-02-10):* <br> 1. *[Derek James] confirmed that the customer size must be over 1,000 employees and the customer must have made a purchase within the preceding year.* <br> 2. *The rule description was updated accordingly* |
| *BR-2* | *Loyal Customer* | *A customer of any size who has made 3 or more purchases within the last 24 months.*  *A customer may be classified as “loyal” but will be “inactive” if they do not satisfy the “active” customer rule.* | *NEW (2025-02-03):* <br> 1. *A request was submitted to [Specific Person Name] in the sales department for the definition of a loyal customer*   *DRAFT (2025-02-04):*   1. *“Any customer who has made at least 2 purchases”.* <br><br> *APPROVED (2025-02-10):* <br> 1. *[Derek James] confirmed that the customer can be of any size but must have made at least 3 purchases in the preceding 2 years; an “inactive” customer can be a “loyal” customer* <br> 2. *The rule description was updated accordingly* |
| *BR-3* | *Open Invoice* | *An open invoice is one that has been sent to a customer, but one which has not been paid.*  *An open invoice is classified as "overdue" when the due date is past.* | *DRAFT (2025-02-03):* <br> 1. *“An invoice that has not been cancelled and that has passed the draft, approved, and sent status levels”* <br> 2. *A request was submitted to [Specific Person Name] in the accounting department for confirmation* <br><br> *APPROVED (2025-02-10):* <br> 1. *[Sally McMillan] confirmed that the draft rule is correct.* |
| *BR-4* | *Invoice Amount* | *The stated amount (converted to Euros if the stated currency is not Euros) and is exclusive of any late payment fees.* | *DRAFT (2025-02-03):* <br> 1. *“The stated amount on the invoice”.* <br><br> *DISCUSSION (2025-02-04):* <br>  1. *[Thomas Delaney] of accounting noted that the invoice amount must be in the corporate reporting currency of Euros.* <br><br> *REVISED (2025-02-05):* <br> 1. *“The stated amount on the invoice converted into Euros”.* <br> 2. *The rule description was updated accordingly* <br> 3. *A request was submitted to [Specific Person Name] in the accounting department for confirmation* <br><br>  *APPROVED (2025-02-06):* <br> 1. *[Mary Wallace] confirmed that the revised rule is correct.* |

## Resources

*LinkedIn Posts*

The LinkedIn posts covering the the design document are listed below: <br>
[1. General and Scope](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7295051537129615362-px8i) <br>
[2. Workflow, Issues, and Business Rules](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7295051537129615362-px8i) <br> *** FIX ***


*Samples*

Sample document fragments covering specific sections are available in the GitHub repo: <br>

[1, Design Document - Sample Fragment 01 - General and Scope](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Power%20BI%20Documentation%20-%20Design%20Document%20-%20Sample%20Fragment%2001%20-%20General%20and%20Scope%20-%20V0.1.docx) <br>
[2. Design Document - Sample Fragment 02 - Workflow, Issues, and Business Rules](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Power%20BI%20Documentation%20%E2%80%93%20Design%20Document%20-%20Sample%20Fragment%2002%20-%20Workflow%20Issues%20and%20Business%20Rules%20-%20V0.2.docx) <br>
