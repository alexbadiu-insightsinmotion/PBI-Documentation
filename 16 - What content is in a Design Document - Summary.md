![16 - Image - Title - Summary](https://github.com/user-attachments/assets/07269e54-ca4d-4647-99b0-fa8d9e30f425)

**What is a Summary of the main content points in a Design Document?**

Throughout this series numerous points have been discussed under each of the major sections of the Power BI design document, and with this issue I’d like to list my personal top points from each section. So, here goes:

## General

The design document is a “**_living_**” document (will be updated throughout the design, testing, and production use periods), so increment the version with each iteration. Use a format and storage location that is common in your organization, that is accessible to all stakeholders (so they can easily \[and constantly\] find and reference it), and that has version control.

## Scope

Be specific with all scope items, and list in three sections: those that will be included, those that will be excluded, and those that will be deferred to a later iteration.

> [!NOTE]  
> *Design note: You can help reduce scope creep by being brutal with both priority and scope (exclude whatever you can, defer whatever you can). Include only high priority and essential items.*<br><br>
> *“If everything is a priority, then nothing is a priority”*

## Workflow

Include a simple workflow flowchart (with swim lanes) for source data (i.e., from operational systems), interim data access location (e.g., SharePoint, etc.), and the Power BI Service (with lanes for staging tables, transformed tables, and model and reports in the Power BI workspace).

## Issues

List each issue encountered during development, including the full decision history for each status level (e.g., NEW, CRITICAL, NOTE, IN PROGRESS, RESOLVED, DEFERRED, etc.). Append, don’t edit.

## Business Rules

Document business rules so developers, testers, and users are measuring the same thing; doing so will prevent “unforced errors”. Use a status to record all activity along with the relevant approval status level (e.g., NEW, DRAFT, DISCUSSION, REVISED, APPROVED (by whom), etc.)

## Data

Fully describe all the environments that will be used in the project (e.g., DEV, TEST, PROD, etc.).

> [!NOTE]  
> *“Everybody has a TEST environment; some are lucky enough to also have a PROD environment”*

List each data source, describe its’ access credentials, and note its’ status (e.g., EXISTING, NEW, IN DEVELOPMENT, APPROVED (by whom), VERIFIED (by whom), etc.) and date.

> [!NOTE]  
> *Design note: Use system accounts/service principals, not personal accounts.*

Reduce the data volume (rows X columns) as much as possible for each report.

> [!NOTE]  
> *“Reduce data volume as much as possible by aggregating as far upstream as possible”*<br><br>
> *“There is no benefit in transferring data you're not going to use”*

## Reports

Include a header (with title and last data refresh) and a footer (with report ID and version [updated with each iteration]) on every page.

> [!NOTE]  
> *Design Note: Use a standard theme, consistent filters, and familiar navigation (your first option should be the built-in navigation provided by Power BI Apps).*

## Validation

Record manual acceptance tests in a table (ID, group, name, notes, priority, expected results, tolerance/allowed variance, setup steps, procedure steps, actual results, teardown steps, date, performed by, and status).

> [!NOTE]  
> *Design Note: Provide acceptance tests to the developers as early as possible in the development period, with each case describing a scenario and expected behaviour, including normal, alternate, and exception paths where appropriate.*
<br><br>
> *Acceptance testing should be conducted by persons different than the developers.*
<br><br>
> *Testing is not “**_done_**” when a report is deployed to the production environment; rather, conduct regular and ongoing monitoring to confirm that the report is functioning as intended (e.g., data refresh, functionality, access, etc.).*

## Deployment

Follow a written procedure for each deployment, have it signed-off after each completion, and incorporate any “**_lessons learned_**” to make future deployments smoother and easier.

> [!NOTE]  
> *Design Note: Use data source parameters and deploy the same PBIX file to each environment; adjust parameters in the deployment pipelines or Power BI Service as necessary.*
<br><br>
> *Use deployment pipelines as a first choice (if licensing permits) for iterative, repeatable deployments. Use manual deployment only if necessary.*
<br><br>
> *A deployment is not “**_done_**” just because it completed without errors. Use smoke testing to confirm basic access and functionality.*

## Model

Extract data as-is into clearly-named staging tables. Reference, merge, or append staging tables before applying any required transformations to create model tables.

Use DAX INFO VIEW functions to extract the model (tables, columns, relationships, measures) as implemented and collate into documentation tables.

> [!NOTE]  
> *Design Note: Use a single, standard, and best practice \[Dates\] dimension table (and mark as such). Here’s an excellent Power Query/M example by Enterprise DNA Expert Melissa de Korte:*
<br><br>
> <https://forum.enterprisedna.co/t/extended-date-table-power-query-m-function/6390>

> [!NOTE]  
> *Design Note: Use a \[Last Refresh\] supporting table. Here’s an excellent Power Query/M example by Enterprise DNA Expert Melissa de Korte:*
<br><br>
> <https://forum.enterprisedna.co/t/adding-a-last-refresh-date-to-your-report/6485>

## Resources

*LinkedIn Posts*

The LinkedIn posts covering the design document are listed below: <br>
[1. General and Scope](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7295051537129615362-px8i) <br>
[2. Workflow, Issues, and Business Rules](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7300125349743316992-tG1U) <br>
[3. Data](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7305187426413563904-6yVG) <br>
[4. Reports](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7310232246613934082-w7iW) <br>
[5. Validation](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7317852256215662593-MvcI) <br>
[6. Deployment](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7322931000085295104-BIIF) <br>
[7. Model](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7330534859825639427-JRdN) <br>
[8. Summary](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7310232246613934082-w7iW) *** FIX *** <br>

*Samples*

Sample document fragments covering specific sections are available in the GitHub repo: <br>

[1, Design Document - Sample Fragment 01 - General and Scope](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2001%20-%20General%20and%20Scope%20-%20V0.1.docx) <br>
[2. Design Document - Sample Fragment 02 - Workflow, Issues, and Business Rules](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2002%20-%20Workflow%20Issues%20and%20Business%20Rules%20-%20V0.2.docx) <br>
[3. Design Document - Sample Fragment 03 - Data](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2003%20-%20Data%20-%20V0.3.docx) <br>
[4. Design Document - Sample Fragment 04 - Reports](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2004%20-%20Reports%20-%20V0.4.docx) <br>
[5a. Design Document - Sample Fragment 05 - Validation](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2005%20-%20Validation%20-%20V0.5.docx) <br>
[5b. Design Document - Sample Validation Spreadsheet](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Validation%20Spreadsheet%20-%20V0.5.xlsx) <br>
[6. Design Document - Sample Fragment 06 - Deployment](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2006%20-%20Deployment%20-%20V0.6.docx) <br>
[7a. Design Document - Sample Fragment 07 - Model](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2007%20-%20Model%20-%20V0.7.docx) <br>
[7b. Design Document - Sample Power BI File](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Power%20BI%20File.pbix) <br>
