<img width="1920" alt="13 - Image - Title - Deployment" src="https://github.com/user-attachments/assets/b3042ccf-942c-4c28-94d4-a93cc7187c1f" />

**What Deployment characteristics should be described in a Design Document?**

So far the design document has concentrated on the characteristics of the report development process. Once development and validation are complete (for an iteration), the report is deployed online such that it can be shared. Whether the ultimate sharing means is direct access from a Power BI workspace or indirectly through a Power BI app, the report must be published to a Power BI workspace. Two classical methods to deploy a Power BI report to a Power BI workspace will be described here: manual deployment and using deployment pipelines.

> [!NOTE]  
> There are preview features in Power BI Desktop (*as of the March 2025 release; not sure of when they were first released)* that allow and enable ***no-publish publishing*** through integration with OneDrive and SharePoint, but this publishing method is beyond the scope of this discussion and there is no further elaboration here. For more information, there are many online resources available, including a video from *Guy in a Cube*: <https://www.youtube.com/watch?v=FtsYYZpH6S4>

<img width="748" alt="13 - Image - OneDrive and SharePoint" src="https://github.com/user-attachments/assets/525b7ac9-ce89-422d-bfe1-5127403cf2b5" />

## Parameters

Regardless of deployment method, to ease the deployment process, Power BI files should be configured with parameters for data sources (e.g., file: folder name, file name; database: server name, database name; etc.). The same Power BI file can then be deployed to each environment, and, in each, the parameters can be modified as desired in the Power BI Service.

Assign an ID and (short) name to each parameter used along with notes for each environment.

*The following example uses three environments (development, testing, and production [or DEV, TEST, and PROD]) and SharePoint (SP) as data access locations.*

| ***ID*** | ***Name*** | ***DEV*** | ***TEST*** | ***PROD*** |
| --- | --- | --- | --- | --- |
| *P-1* | *Invoices SP Folder name* | *Invoicing\_DEV* | *Invoicing\_TEST* | *Invoicing* |
| *P-2* | *Invoices SP File name* | *Invoices.xlsx* | *Invoices.xlsx* | *Invoices.xlsx* |
| *P-3* | *Customers SP Folder name* | *Customers\_DEV* | *Customers\_TEST* | *Customers* |
| *P-4* | *Customers SP File name* | *Customers.xlsx* | *Customers.xlsx* | *Customers.xlsx* |

## Manual Deployment

Power BI artifacts (PBIX files) can easily be published to the Power BI Service using Power BI Desktop. The publisher has full control over artifact selection.

> [!WARNING]  
> *It is possible (though not recommended) to create custom versions for each environment (e.g., credentials, data sources, filters, etc.). In a 3-tier environment, this would be 3 separate versions each tailored for the specific target environment. If such a method is used, it is then incumbent upon the publisher (often the developer) to ensure that the correct PBIX file is used in each publishing instance.*

> [!NOTE]  
> *It is a much better idea to use the same PBIX file for all environments, and then make any necessary data source and credential changes in the Power BI Service after publishing.*

There are many resources available for the use of Power BI Desktop to publish artifacts to the Power BI Service, but a simple example of a 3-tier deployment is:

- Create the DEV artifacts in Power BI Desktop using the DEV data sources and credentials
- Create the DEV, TEST, and PROD workspaces
- Publish the artifacts to the DEV workspace
- Publish the artifacts to the TEST workspace
- Manually set data sources and credentials in the TEST workspace
- Manually set parameters in the TEST workspace
- Manually refresh data in the TEST workspace
- Complete validation in the TEST workspace
- Publish the artifacts to the PROD workspace
- Manually set data sources and credentials in the PROD workspace
- Manually set parameters in the PROD workspace
- Manually refresh data in the PROD workspace
- Manually set the data refresh frequency in the PROD workspace
- Ensure the correct ownership of the semantic models in the PROD workspace
- Ensure the correct workspace access to protect the PROD assets

These steps are necessary whether the deployment is conducted by the developers or others. In many organizations, developers can only publish to the DEV environment and other authorized personnel are responsible for all publishing to the TEST and PROD environments.

## Deployment Pipelines

Using a deployment pipeline in Power BI restricts the manual publishing of artifacts using Power BI Desktop to only a single instance, namely the initial publishing to the DEV environment; additional deployments to downstream environments do not require Power BI Desktop but instead are achieved via the pipeline in the Power BI Service.

To take full advantage of deployment pipelines, the parameters used (as described above) can be incorporated into the deployment pipeline itself and the correct setting of these values during deployment can easily be confirmed after in the Power BI Service.

> *The configuration and use of deployment pipelines is dependent upon the available license. My current experience with licenses is quite limited, but my understanding is that a Power BI Premium or Power BI Premium-Per-User (PPU) is required to use deployment pipelines. (During the writing of this post, a Power BI Pro license was used but a Fabric Trial had been recently granted by Microsoft, so I’m not sure if Pro can be used or if a Premium or Fabric license is needed. Regardless, the process is the same, so I’ll end the discussion of licenses here.)*
> *Further, during the research for this post, it was announced in March 2025 that Power BI Premium licensing would be retired and that equivalent Fabric licenses would be available. Microsoft has released details (and, I’m sure, will release many more details) in this post:*
> [*https://powerbi.microsoft.com/en-us/blog/important-update-coming-to-power-bi-premium-licensing/*](https://powerbi.microsoft.com/en-us/blog/important-update-coming-to-power-bi-premium-licensing/)

> [!WARNING]  
> *It is possible (though not recommended) to use a deployment pipeline to move the Power BI artifacts and then to manually update the deployed model in the Power BI Service with any necessary data source changes.*

> [!NOTE]  
> *It is a much better idea to use data source parameters in the PBIX file and set rules directly within the deployment pipeline itself so that manual activity is required only once during the initial setup of the pipeline rather than after each execution iteration.*

There are many resources available for the configuration and use of deployment pipelines, but a simple example of a 3-tier (3-stage) deployment is:

- Create the DEV artifacts in Power BI Desktop using the DEV data sources and credentials
- Create the DEV, TEST, and PROD workspaces
- Publish the artifacts to the DEV workspace using Power BI Desktop
- Create the pipeline with the DEV, TEST, and PROD stages
- Assign the DEV, TEST, and PROD workspaces to stages
- Select artifacts in the DEV stage and deploy to the TEST stage
- Set rules (parameters) in the TEST stage
- Set data sources and credentials in the TEST workspace
- Manually refresh data in the TEST workspace
- Complete validation in the TEST environment
- Select artifacts in the TEST stage and deploy to the PROD stage
- Set rules (parameters) in the PROD stage
- Set data sources and credentials in the PROD workspace
- Manually refresh data in the PROD workspace
- Manually set the data refresh frequency in the PROD workspace
- Ensure the correct ownership of the semantic models in the PROD workspace
- Ensure the correct workspace access to protect the PROD assets

## Procedure

Regardless of deployment method, it is essential to have a repeatable, written, and signed off procedure. Further, the procedure should be updated after each deployment so that any necessary adjustments (lessons learned) are captured, and future deployments will be smoother and easier.

Assign a sequential ID and (short) name to each step in the deployment procedure along with any required notes, the specific final value, and date the step was completed (and by whom).

*NOTE*

*The deployment pipeline method will be used in the following example.*

| ***ID*** | ***Name*** | ***Notes*** | ***Value*** | ***Completion & Signoff*** |
| --- | --- | --- | --- | --- |
| *S-1* | *Environment* | *The target environment* | *PROD* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-2* | *Publish Target Data* | *Target data has been published to the access location* | *SharePoint Folder:*  <br>*\Corporate\Invoicing*  <br>*File names: <br>various* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-3* | *Publish Power BI file* | *Source PBIX has been published to the source Power BI Workspace* | *AR01 - All Invoices* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-4* | *Set Rule/Parameter (Invoices SP Folder name)* | *(as many lines as necessary for 1 per rule/parameter; <br>only 1 shown here for illustrative purposes)* | *Invoicing* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-5* | *Select Artifacts in Source* | *All that will be deployed in this iteration* | *Report:*  <br>*AR01 - All Invoices*  <br>*Semantic Model:*  <br>*AR01 - All Invoices* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-6* | *Deploy* | *From the source environment to the target environment* | *TEST to PROD* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-7* | *Verify Artifacts in Target* | *In Power BI Service*  <br>*All that should have been deployed in this iteration* | *n/a* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-8* | *Verify Data Source Credentials on target* | *In Power BI Service* | *n/a* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-9* | *Verify Security on target* | *In Power BI Service*  <br>*Credentials/access on workspace and/or report and/or app* | *n/a* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-10* | *Verify Parameter (Invoices SP Folder name)* | *(as many lines as necessary for 1 per rule/parameter; <br>only 1 shown here for illustrative purposes)* | *Invoicing* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-11* | *Verify Data Refresh* | *In Power BI Service*  *Manually refresh the data to confirm access* | *n/a* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-12* | *Set Data Refresh Schedule* | *In Power BI Service* | *Daily at <br>2:00 AM UTC* | *Date: 2025-03-29*  <br>*By: Greg Philps* |
| *S-13* | *Verify Deployment* | *In Power BI Service*  *Conduct smoke testing to confirm the <br>basic operation of the report(s)* | *n/a* | *Date: 2025-03-29*  <br>*By: Greg Philps* |

## Resources

*LinkedIn Posts*

The LinkedIn posts covering the design document are listed below: <br>
[1. General and Scope](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7295051537129615362-px8i) <br>
[2. Workflow, Issues, and Business Rules](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7300125349743316992-tG1U) <br>
[3. Data](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7305187426413563904-6yVG) <br>
[4. Reports](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7310232246613934082-w7iW) <br>
[5. Validation](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7317852256215662593-MvcI) <br>
[6. Deployment](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7322931000085295104-BIIF) <br>

*Samples*

Sample document fragments covering specific sections are available in the GitHub repo: <br>

[1, Design Document - Sample Fragment 01 - General and Scope](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2001%20-%20General%20and%20Scope%20-%20V0.1.docx) <br>
[2. Design Document - Sample Fragment 02 - Workflow, Issues, and Business Rules](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2002%20-%20Workflow%20Issues%20and%20Business%20Rules%20-%20V0.2.docx) <br>
[3. Design Document - Sample Fragment 03 - Data](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2003%20-%20Data%20-%20V0.3.docx) <br>
[4. Design Document - Sample Fragment 04 - Reports](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2004%20-%20Reports%20-%20V0.4.docx) <br>
[5a. Design Document - Sample Fragment 05 - Validation](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2005%20-%20Validation%20-%20V0.5.docx) <br>
[5b. Design Document - Sample Validation Spreadsheet](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Validation%20Spreadsheet%20-%20V0.5.xlsx) <br>
[6. Design Document - Sample Fragment 06 - Deployment](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2006%20-%20Deployment%20-%20V0.6.docx)
