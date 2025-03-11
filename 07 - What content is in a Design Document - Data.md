<img width="1920" alt="07 - Image - Title - Data" src="https://github.com/user-attachments/assets/a0ac9319-73ea-4506-b5ba-e507d080ca47" />

**What Data characteristics should be described in a Design Document?**

The Power BI data connection mode (import or direct) will determine the format and impact of the data section in the design document. As data movement is not a component of **direct query** models, **import** mode data access will be described herein.

The data available to (and presented in) a Power BI report will be subject to several criteria, including the source environment, access credentials, data volume, data refresh frequency, transformations, and modelling (relationships).

This issue deals with the Data major section, and the remaining sections will be covered in subsequent issues.

## Environments

Describe the different separate environments to be used in the project. (For example, in a 3-tier layout, separate instances of the source application(s), databases, and target report sharing platform will be available and used [e.g., DEV, TEST, PROD]. In a 4-tier layout, the environments may be named DEV, TEST, STAGE, and PROD.)

Evaluate the (paraphrased) statement,

> *“Everybody has a TEST environment; some are lucky enough to also have a PROD environment.”*

If you choose to test in production, then you accept the impacts and risks (e.g., degraded performance, responsiveness, reliability/downtime, etc.).

Note whether dedicated source applications are available in each environment, or if it is necessary, for example, to use the PROD environment for development and acceptance testing.

If separate instances of source applications are available, note the data characteristics and whether they are representative of the PROD environment (e.g., network performance, data security, data volume, data variability, data refresh, etc.).

## Data Sources

Describe the characteristics of accessing the data for the report(s) including the source systems, access credentials, volume of data (and available level of detail [or granularity]), and the frequency of update.

Operational systems will ideally not be used as data sources for direct reporting purposes; rather dedicated data warehouses or replicas will hopefully be the sources from which to do reporting.

If operational systems are in fact the reporting data source, then the performance impact of the data transfer processes must be acceptable. One possible approach to minimize the impact is to do all reporting on **yesterday's** data (i.e., only refresh once per day, after hours, when performance impacts are acceptable).

### Sources

Assign an [ID] to each data source, describe it, and use the [Status] column to note if it is new or existing (e.g., EXISTING, NEW, IN DEVELOPMENT, APPROVED (by whom), VERIFIED (by whom), etc.) and date (use a consistent and unambiguous date format [e.g., yyyy-mm-dd, dd-mmm-yyyy, etc.]).

Include all data sources that will be used in the data flows and semantic models serving the reports that are existing and those included in this document.

Here's an example:

| **ID** | **Name** | **Description** | **Status** |
| --- | --- | --- | --- |
| *S-1* | *Customer Data Source* | *Microsoft Dynamics (on-premises)* | *NEW (2025-02-14):*<br>1. *A request was submitted to [Specific Person Name] in the IT department for implementation of a new Power BI Gateway and service account to access all customer data*<br><br>*IN DEVELOPMENT (2025-02-28):*<br>1. *The [Specific Name] gateway is currently being implemented with the [Specific Name] service account to access all customer data in the DEV environment*<br>2. *The gateways have not been implemented yet nor service accounts created for the TEST and PROD environments* |
| *S-2* | *Invoice Data Source* | *SAP Financials (on-premises)* | *EXISTING (2025-02-27):*<br>1. *The [Specific Gateway Name] Power BI Gateway can be used to access to all financial data using the [Specific Service Account] account credentials in the PROD environment*<br>2. *There are currently no instances of SAP Financials in the DEV or TEST environments, nor are there any plans to implement them* |

### Credentials

Assign an [ID] to each credential set that will be used to access each data source in each environment and the IP address/URL, account name, and password that will be used to connect to it, ideally service accounts created and used exclusively for data access by other services.

> [!NOTE] 
> *these credentials should refer to* ***system*** *accounts and not personal accounts, as personal accounts can be subject to changes by others outside of the reporting system without notice (e.g., reassignment, promotion/demotion, retirement, leaving, etc.).*

Here's an example:

| **ID** | **Name** | **Environment** | **Credentials** |
| --- | --- | --- | --- |
| *C-11* | *Customer Data Source Credentials* | *DEV* | *IP/URL: 192.1.1.1*<br>*Account name: serviceDYN-DEV@abc.ca*<br>*Password=(retrieve from Keepass)*<br>*- Entry=serviceDYN-DEV*<br>*- Vault=[Insert Key Vault Name]*<br>*- Secret=[Insert Secret Name]* |
| *C-12* | *Customer Data Source Credentials* | *TEST* | *IP/URL: dynamics-TEST.abc.com*<br>*Account name: serviceDYN-TEST@abc.ca*<br>*Password=(retrieve from Keepass)*<br>*- Entry=serviceDYN-TEST*<br>*- Vault=[Insert Key Vault Name]*<br>*- Secret=[Insert Secret Name]* |
| *C-13* | *Customer Data Source Credentials* | *PROD* | *IP/URL: dynamics.abc.com*<br>*Account name: serviceDYN@abc.ca*<br>*Password=(retrieve from Keepass)*<br>*- Entry=serviceDYN*<br>*- Vault=[Insert Key Vault Name]*<br>*- Secret=[Insert Secret Name]* |
| *C-21* | *Invoice Data Source Credentials* | *DEV* | *IP/URL: 192.2.2.2*<br>*Account name: serviceSAP-DEV@abc.ca*<br>*Password=(retrieve from Keepass)*<br>*- Entry=serviceSAP-DEV*<br>*- Vault=[Insert Key Vault Name]*<br>*- Secret=[Insert Secret Name]* |
| *C-22* | *Invoice Data Source Credentials* | *TEST* | *IP/URL: sap-TEST.abc.com*<br>*Account name: serviceSAP-TEST@abc.ca*<br>*Password=(retrieve from Keepass)*<br>*- Entry=serviceSAP-TEST*<br>*- Vault=[Insert Key Vault Name]*<br>*- Secret=[Insert Secret Name]* |
| *C-23* | *Invoice Data Source Credentials* | *PROD* | *IP/URL: sap.abc.com*<br>*Account name: serviceSAP@abc.ca*<br>*Password=(retrieve from Keepass)*<br>*- Entry=serviceSAP*<br>*- Vault=[Insert Key Vault Name]*<br>*- Secret=[Insert Secret Name]* |

### Volume

Reduce the data volume (rows X columns) as much as possible for each report.

Don't load high-cardinality columns (e.g., Sales Key, Alternate Sales Key, etc.) unless they are absolutely necessary for your report(s).

There is nothing inherently wrong with loading too much data, but it will inflict a performance penalty on all report users, be it the IT department (who suffer needlessly with long data refresh times) or the report users (who suffer needlessly with slow reports). One can apply the concepts in [Roche’s Maxim]( https://ssbipolar.com/2021/05/31/roches-maxim/) on transforming Power BI data (*“…as far upstream as possible and as far downstream as necessary…”* to data aggregation (and hence, volume reduction) as well, giving rise to a statement like,

> *“Reduce data volume as much as possible by aggregating as far upstream as possible”*

If you can aggregate data before it is transferred, you can both reduce the time required for data transfer (refresh) and increase Power BI performance (by obviating the need for aggregation within Power BI). Only transfer the volume of data you’re actually going to use, or, said another way,

> *“There is no benefit in transferring data you're not going to use”*

Assign an [ID] to the data source and describe the data volume required to answer the report(s) questions, the grain of the data source and its' use in the report(s), and the available and required aggregation for each.

Here's an example:

| **ID** | **Name** | **Volume** | **Grain/Aggregation** |
| --- | --- | --- | --- |
| *V-1* | *Customer Data Refresh* | *Monthly* | *Source/G=n/a*<br>*Source/A=none*<br><br>*Report/G=n/a*<br>*Report/A=none* |
| *V-2* | *Invoice Data Refresh* | *Daily* | *Source/G=millisecond*<br>*Source/A=none*<br><br>*Report/G=day*<br>*Report/A=rollup to day* |

### Refresh

There's no sense in refreshing data that hasn't changed since the last update. Further, if the report(s) in question will be analysing, say performance up to the end of the previous month, then a daily refresh frequency will consume resources while offering no value. Said another way,

> *“Consider both the source update frequency and the report(s) analysis period before setting the data refresh criteria that will provide the needed value while minimizing the resources required”*

As well, and as noted above, there's no point in making the IT department perform unnecessary data transfer operations, especially as there may be time restrictions (or worse, conflicts) with other daily operation periods (e.g., replications, backups, archives, etc.).

Assign an [ID] to the refresh of the data source and describe the frequency, procedure, target, monitoring, and responsibility for each.

Here's an example:

| **ID** | **Name** | **Frequency** | **Procedure / Target /**  **Monitoring / Responsibility** |
| --- | --- | --- | --- |
| *R-1* | *Customer Data Refresh* | *Monthly* | *P=Manual via Excel file*<br>*T=Dedicated SharePoint folder*<br>*M=Sue Jones (IT department)*<br>*R=Jane Doe (sales department)* |
| *R-2* | *Invoice Data Refresh* | *Daily* | *P=Automatic via scheduled dataflow*<br>*T=Dedicated SharePoint folder*<br>*M=Sue Jones (IT department)*<br>*R=John Smith (accounting department)* |

## Data Connections
Power BI can connect to data in 3 ways:
* Direct
* Gateway
* Cloud connections

Direct connections are ***internal*** sources you ***can*** see from your computer (i.e., those you can connect to directly)
* File sources (e.g., Excel, CSV, Text, JSON, OneDrive, SharePoint, etc.)
* Database sources (e.g., SQL Server, Oracle, MySQL, IBM DB2, IBM Netezza, etc.)

Gateway connections are ***internal*** sources you ***cannot*** see from your computer (i.e., those you cannot connect to without a “bridge”)
* On-premises data sources that are inaccessible to the internet (e.g., behind a firewall on a network drive, etc.)
* Use internally stored and managed credentials

Cloud Connections are ***external*** (Internet, or Web) sources ***hosted*** on cloud platforms
* Cloud sources (e.g., Azure SQL, Snowflake, Databricks, etc.)
* Use externally stored and managed credentials

### Direct

Describe each internal data connection that will be directly accessed, including ID, type, location, folder, responsibility, and filename.

Here's an example:

| **ID** | **Name** | **Description** | **Type / Location / Folder / Responsibility / Filename** |
| --- | --- | --- | --- |
| CD-1 | Aging Buckets | Excel worksheet with five buckets for categorizing invoice data<br>- 0-30 days<br>- 31-60 days<br>- 61-90 days<br>- 91-180 days<br>- 181 days and over<br><br>To be used as the data source for the [Aging] supporting table | T=Excel<br>L=SharePoint<br>Folder=Accounting/Master Data/<br>R=Jennifer Smith/Accounting<br>Filename=Invoice Aging.xlsx

### Gateway

Describe any gateways that will allow indirect connection to on-premises data sources such that they can be accessed by the Power BI Service, including ID, type (new, existing, standby), and status (online, offline, etc.). 
Ideally all gateways will use service accounts with full permission to read all source records (i.e., no security restrictions).
(For all gateways, describe the environment, availability [clustered; standalone] and use [e.g., dedicated to a single gateway; shared by multiple gateways; used by other services, etc.]).
(For any standby gateways, describe the required takeover verification intervals and any characteristics that differ from the primary gateway.)

Here’s an example:

| **ID** | **Name** | **Description** | **Type / Status / Environment / Availability / Use / Responsibility / Verification / Other** |
| --- | --- | --- | --- |
| *CG-1* | *On-premises HR System (Sole)* | *Existing Power BI Gateway already permitting read access by the Power BI Service to Customer data*<br>* *(List of tables exposed and time horizon for each)*<br>* *Customers*<br>* *Contacts*<br>* *Addresses (current)*<br>* *Addresses (historical)*<br>* *Regions* | *T=Existing*<br>*S=Online*<br>*E=PROD (no DEV or TEST gateway)*<br>*A=Power Platform Gateway Cluster GC-1)*<br>*U=Dedicated/single*<br>*R=centrally monitored and managed by corporate tenant administrators*<br>*V=n/a*<br>*O=none* |
| *CG-2* | *On-premises Financial System (Primary)* | *New Power BI Gateway permitting read access by the Power BI Service*<br>* *(List of tables exposed and time horizon for each)*<br>* *Invoices (current fiscal year)*<br>* *Invoices (previous fiscal year)*<br>* *Invoices (historical [that is, before previous fiscal year])*<br>* *Payments (current fiscal year, previous fiscal year)* | *T=New*<br>*S=Offline*<br>*E=PROD (no DEV or TEST gateway)*<br>*A=Standalone*<br>*U=Shared/multiple*<br>*R=locally monitored and managed by accounting department*<br>*V=n/a*<br>*O=none* |
| *CG-3* | *On-premises Financial System (Standby)* | *Standby Power BI Gateway to provide the same access as the primary financial system Power BI Gateway (CG-2)* | *T=Standby*<br>*S=Offline*<br>*E=PROD (no DEV or TEST gateway)*<br>*A=Standalone*<br>*U=Shared/multiple (common standby gateway that provides failover protection for multiple primary gateways)*<br>*R=locally monitored and managed by accounting department*<br>*V=monthly for 24 hours (on first Monday on or after the 15th of the month; full takeover [disable primary, enable standby])*<br>*O=memory (16 GB vs. 256 GB for CG-2)* |

### Cloud

Describe all details necessary to configure the connection, including type, credential type, credentials, authentication method, etc.

Here are a few best practices to consider:
- Use shareable connections
    - Support multiple connection to the same data source
    - Security and permissions can be adjusted to suit:
        - Can assign different tables their own separate connections
        - Can grant User permission to enable others to use the connection to bind to the data source
- Use service principals (preferred) or service accounts (good) rather than personal accounts (poor)
    - Service Principals: No Power BI license needed, centralized security, governance
    - Service Accounts: Power BI license needed, distributed security (credentials must be shared), no-notice password expiry
    - Personal Accounts: Power BI license needed, security managed by others, no-notice credential activation and permission changes (e.g., reassignment, promotion/demotion, retirement, leaving, etc.)

## Dataflows

Describe the design of all dataflows that will be developed for this (series) of reports. Include the type (e.g., staging, fact, dimension, supporting, etc.) and all filters and transformations that will be applied to the dataflow

> [!NOTE]  
> Dataflows should be written for people; the computer will execute working code regardless of clarity. Use whitespace and long and descriptive variable and step names (the computer will internally tokenize them anyway, so ...) and write for those who will be updating the code in the future (which just may be you in 6 months). Don't be the only one who understands your code (don't let your code "fail the bus test").

> [!NOTE]  
> Staging tables are ideally used for connection and data transfer only and contain no transformations.

Here's an example:

| **ID** | **Name (Example)** | **Type** | **Source / Filters / Transformations** |
| --- | --- | --- | --- |
| *D-1* | *RAW Customers* | *Staging* | *S=operational system*<br>*F=none*<br>*T=none* |
| *D-2* | *RAW Invoices* | *Staging* | *S=operational system*<br>*F=only last 2 fiscal years*<br>*T=none* |
| *D-3* | *Customers* | *Dimension* | *S=reference of D-1 (RAW Customers)*<br>*F=none*<br>*T=*<br>* *columns renamed to Proper Case*<br>* *column data types verified* |
| *D-4* | *Invoices* | *Fact* | *S=reference of D-2 (RAW Invoices)*<br>*F=none*<br>*T=*<br>* *columns renamed to Proper Case*<br>* *column data types verified* |
| *D-5* | *Regions* | *Dimension* | *S=reference of D-1 (RAW Customers)*<br>*F=none*<br>*T=*<br>* *columns renamed to Proper Case*<br>* *column data types verified*<br>* *duplicates removed* *<br>*index added* |
| *D-6* | *Aging Buckets<br>(0-30d, 31-60d, 61-90d,<br>91-180d, 181d+)* | *Supporting* | *S=Excel spreadsheet*<br>*F=none*<br>*T=none* |

## Semantic Model

Include an image of the data model and arrange tables for clarity (e.g., waterfall design, with dimension [lookup] tables at the top, fact tables in the middle, supporting tables in the bottom-left, and measure tables in the top-right, etc.)

<img width="1273" alt="07 - Image - Data Model" src="https://github.com/user-attachments/assets/cf7471b0-7cd4-4d87-be85-df1b486bc1ad" />

Describe the design of the semantic model, including all fact tables, dimension (or lookup) tables, and supporting tables.

Assign an [ID] to each relationship and fully describe it, including the fields/columns that will be used to link tables, the cardinality, and the directionality of each relationship.

> [!NOTE]  
> *(This is the design intent, not the implementation; the DAX INFO functions will be used in the appendices [a subsequent issue] to extract the actual relationships from the developed model.)*

Here's an example:

| **ID** | **From (table[column])** | **To (table[column])** | **Cardinality / Directionality** |
| --- | --- | --- | --- |
| *CR-1* | *Dates[Date]* | *Invoices[Date]* | *C=one-to-many*<br>*D=single* |
| *CR-2* | *Customers[Customer ID]* | *Invoices[Customer ID]* | *C=one-to-many*<br>*D=single* |

## Resources

*LinkedIn Posts*

The LinkedIn posts covering the design document are listed below: <br>
[1. General and Scope](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7295051537129615362-px8i) <br>
[2. Workflow, Issues, and Business Rules](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7300125349743316992-tG1U)) <br>
[3. Data](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7295051537129615362-px8i) <br> *** FIX ***

*Samples*

Sample document fragments covering specific sections are available in the GitHub repo: <br>

<<< INSERT SAMPLE 01 WORD FRAGMENT LINK - GENERAL AND SCOPE >>> <br>
<<< INSERT SAMPLE 02 WORD FRAGMENT LINK - WORKFLOW, ISSUES, AND BUSINESS RULES >>> <br>
<<< INSERT SAMPLE 03 WORD FRAGMENT LINK - DATA >>>
