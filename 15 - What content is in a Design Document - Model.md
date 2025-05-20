<img width="1920" alt="15 - Image - Title - Model" src="https://github.com/user-attachments/assets/9806fa6b-945c-4e83-84e6-57e2e5009b59" />

**What Model characteristics should be described in a Design Document?**

The data model is the heart of any Power BI report. This “back-end” is often not given the attention it deserves, as it may seem like spending time on portions of the solution that are not visible to consumers is wasted effort: this could not be farther from the truth. You will be rewarded in many ways if care is taken preparing your data model, including:

- Better performance
- Simpler calculations
- Easier upgrades (via increased comprehension of existing model and more realistic evaluation of the impact and effort required for changes)

The intent of the semantic model design was explored in earlier issues (#7 & #9).

<https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/07%20-%20What%20content%20is%20in%20a%20Design%20Document%20-%20Data.md#semantic-model>

<https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/09%20-%20What%20content%20is%20in%20a%20Design%20Document%20-%20Reports.md#semantic-model-specific>

This issue instead deals with the actual design as implemented in the Power BI file.

> [!NOTE]
> *While the sections of the design document to date reflect the design intent, the implemented (actual) model is often presented in appendicies.*

## General

### Staging

Before delving into the specifics of the model, it is worth describing the data extract and transformation logic.

Data should be extracted as-is (i.e., without transformations) into staging tables. Staging tables should further be clearly named as such, for example, by adding a “RAW” prefix. Where necessary, staging tables can be merged to produce a model table (e.g., RAW Customers + RAW Addresses 🡪 Customers, etc.).
<br><br>
Staging Table: RAW Customers

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Customer ID | Integer | 1 | Primary Key |
| 2 | Customer | Text | Dave |  |
| 3 | Address ID | Integer | 1 | Foreign Key |

<br>

Staging Table: RAW Addresses

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Address ID | Integer | 1 | Primary Key |
| 3 | City | Text | Ottawa |  |
| 4 | Country | Text | Canada |  |

<br>

Transformation Operation: Merge RAW Customers and RAW Addresses tables using Address ID (left outer join)

<br>

Model Table: Customers

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Customer ID | Integer | 1 | Primary Key |
| 2 | Customer | Text | Dave |  |
| 3 | City | Text | Ottawa |  |
| 4 | Country | Text | Canada |  |

<br>

### INFO VIEW Functions

The INFO VIEW functions can be easily leveraged to extract the implemented design. Once this information is consolidated in one place (yes, I know Power BI Desktop is one place, but the information is somewhat distributed and a “big picture” can be challenging to see), a “10,000 foot” view can expose discrepancies more easily.

To that end, the tables and columns, relationships, and measures as implemented should be collated in documentation tables.

*NOTE: The procedure used to export the following table data from Power BI Desktop was to:*

1. *Open DAX Query View and enter the desired query*
2. *Click the “Run” button*
3. *Click the “Copy” button and select “Entire table”*
4. *Select more than the needed number of rows in the desired design document table and use CTRL-V to paste the exported data*
5. *Remove the header row and any blank or duplicate rows*
6. *Edit the “ID” and “Notes” columns as necessary*
7. *Add the data for the “Sample” column as desired*

<br>

## Tables and Columns

*List all tables in the model; the following can be used in DAX Query View from within Power BI Desktop to retrieve the table data:*

```dax
EVALUATE
VAR _Result =
  SELECTCOLUMNS(
    INFO.VIEW.TABLES(),
    "ID", [ID],
    "Name", [Name],
    "Category", [DataCategory],
    "Type", IF( ISBLANK([Expression]), "Normal", "Calculated" ),
    "Expression", [Expression],
    "Is Hidden", [IsHidden]
  )

RETURN
_Result
```

| **ID** | **Name** | **Category** | **Type** | **Expression** | **Is Hidden** |
| --- | --- | --- | --- | --- | --- |
| 1 | Key Measures | Regular | Normal |  | false |
| 2 | Dates | Time | Normal |  | false |
| 3 | Invoices | Regular | Normal |  | false |
| 4 | Customers | Regular | Normal |  | false |
| 5 | Last Refresh | Regular | Normal |  | true |
| 6 | Orders | Regular | Normal |  | false |
| 7 | Products | Regular | Normal |  | false |
| 8 | Regions | Regular | Normal |  | false |
| 9 | Aging | Regular | Calculated | SELECTCOLUMNS ( <br>GENERATESERIES ( 1, 6, 1 ), <br>"Aging ID", <br>[Value]<br> ) | true |

*List all columns in each table; the following can be used in DAX Query View from within Power BI Desktop to retrieve the column data (adjust the [_Table] variable to suit):*

```dax
EVALUATE
VAR _Table = "Dates"
VAR _Result =
  SELECTCOLUMNS(
    FILTER( INFO.VIEW.COLUMNS(), [Table] = _Table && [Type] IN {"Data", "Calculated"} ),
    "ID", [ID],
    "Name", [Name],
    "Type", IF( [DataType] = "True/False" , "Boolean", [DataType] ),
    // "Nulls", IF( [IsNullable] = TRUE(), "Yes", "No" ),
    "Sample", BLANK(),
    "Notes", COMBINEVALUES( " | ", IF( [IsKey] = TRUE(), "Primary Key", BLANK() ),
      IF( OR( [FormatString] = "0", [DataType] = "True/False" ), BLANK(), [FormatString] ), [Expression] )
  )

RETURN
_Result
```

### Fact

#### Invoices

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Invoice ID | Integer | 2401 | Primary Key |
| 2 | Invoice Date | Date | January 31, 2024 | Long Date |
| 3 | Amount | Number | 371900 |  |
| 4 | Customer ID | Integer | 1 | Foreign Key |
| 5 | Region ID | Integer | 1 | Foreign Key |

#### Orders

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Order ID | Integer | 2407 | Primary Key |
| 2 | Order Date | Date | July 17, 2024 | Long Date |
| 3 | Product ID | Integer | 5 | Foreign Key |
| 4 | Quantity | Integer | 16 |  |
| 5 | Customer ID | Integer | 4 | Foreign Key |
| 6 | Region ID | Integer | 6 | Foreign Key |

### Dimension

#### Customers

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Customer ID | Integer | 1 | Primary Key |
| 2 | Customer | Text | Dave |  |
| 3 | City | Text | Ottawa |  |
| 4 | Country | Text | Canada |  |

#### Products

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Product ID | Integer | 4 | Primary Key |
| 2 | Product | Text | Shoes |  |
| 3 | Unit Price | Integer | 120 |  |
| 4 | Unit Cost | Integer | 110 |  |

#### Regions

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Region ID | Integer | 1 | Primary Key |
| 2 | Region | Text | Canada |  |

#### Dates

*A date table will be created using M-code directly in Power BI. The date table should cover the entire time span of interest and with full calendar years and will be initially created for a three-year period (i.e., 2023-01-01 to 2025-12-31).*

The [Dates] table was generated using Power Query/M code from the Extended Date Table by Enterprise DNA Expert Melissa de Korte, one of the (if not the) best date tables available for Power BI.<br>
https://forum.enterprisedna.co/t/extended-date-table-power-query-m-function/6390.

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Date | Date | 05-Feb-2025 | Primary Key  dd-mmm-yyyy |
| 2 | Year | Integer | 2025 |  |
| 3 | Quarter Number | Integer | 1 |  |
| 4 | Quarter | Text | Q1 |  |
| 5 | Month | Integer | 2 |  |
| 6 | Month & Year | Text | Feb 2025 |  |
| 7 | MonthnYear | Integer | 202502 |  |
| 8 | Month Name | Text | February |  |
| 9 | Month Short | Text | Feb |  |
| 10 | Month Initial | Text | F |  |
| 11 | Day of Month | Integer | 5 |  |
| 12 | Day of Week Number | Integer | 2 |  |
| 13 | Day of Week Name | Text | Wednesday |  |
| 14 | Day of Week Initial | Text | W |  |
| 15 | DateInt | Integer | 20250205 |  |
| 16 | IsAfterToday | Boolean | True |  |
| 17 | IsWeekDay | Boolean | True |  |
| 18 | Day Type | Text | Weekday |  |
| 19 | Fiscal Year | Text | FY2025 |  |
| 20 | Fiscal Quarter | Text | FQ4 2025 |  |
| 21 | FQuarternYear | Integer | 20254 |  |
| 22 | Fiscal Period | Text | FP11 2025 |  |
| 23 | FPeriodnYear | Integer | 202511 |  |
| 24 | IsCurrentFY | Boolean | True |  |
| 25 | IsCurrentFQ | Boolean | True |  |
| 26 | IsCurrentFP | Boolean | False |  |
| 27 | IsPYTD | Boolean | False |  |
| 28 | IsPFYTD | Boolean | False |  |

### Supporting

#### Aging

This is a calculated table and reflects the invoice aging groups used by the organization.

```dax
Aging = SELECTCOLUMNS ( GENERATESERIES ( 1, 6, 1 ), "Aging ID", [Value] )
```

| **ID** | **Name** | **Type** | **DAX Expression** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Aging ID | Integer | (see table creation expression above) | Primary Key |
| 2 | Aging | Text | SWITCH(TRUE(),<br>  [Aging ID] = 1, "0-30 days",<br>  [Aging ID] = 2, "31-60 days",<br>  [Aging ID] = 3, "61-90 days",<br>  [Aging ID] = 4, "91-120 days",<br>  [Aging ID] = 5, "121-180 days",<br>  [Aging ID] = 6, "over 180 days",<br>  "ERROR") |  |
| 3 | Min | Integer | SWITCH(TRUE(),<br>  [Aging ID] = 1, 0,<br>  [Aging ID] = 2, 31,<br>  [Aging ID] = 3, 61,<br>  [Aging ID] = 4, 91,<br>  [Aging ID] = 5, 121,<br>  [Aging ID] = 6, 181,<br>  -1) |  |
| 4 | Max | Integer | SWITCH(TRUE(),<br>  [Aging ID] = 1, 30,<br>  [Aging ID] = 2, 60,<br>  [Aging ID] = 3, 90,<br>  [Aging ID] = 4, 120,<br>  [Aging ID] = 5, 180,<br>  [Aging ID] = 6, 9999,<br>  -1) |  |

#### Tiers

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Tier ID | Integer | 1 | Primary Key |
| 2 | Tier | Text | Gold |  |
| 3 | Lower Bound | Integer | 10,000,000 |  |
| 4 | Upper Bound | Integer | 9,999,999,999 |  |

#### Last Refresh

There is no data source for this table, rather, it was generated using Power Query/M code by Enterprise DNA Expert Melissa de Korte:
https://forum.enterprisedna.co/t/adding-a-last-refresh-date-to-your-report/6485

This table is a supporting table used by the [Last Refresh] measure.

```m
let
  Source = DateTime.FixedLocalNow(),
  #"Converted to Table" = #table(1, {{Source}}),
  #"Renamed Columns" = Table.RenameColumns(#"Converted to Table", {{"Column1", "Last Refresh"}}),
  #"Changed Type" = Table.TransformColumnTypes(#"Renamed Columns", {{"Last Refresh", type datetime}}),
  #"Inserted Date" = Table.AddColumn(#"Changed Type", "Date", each DateTime.Date([Last Refresh]), type date),
  #"Insert Time" = Table.AddColumn(#"Inserted Date", "Time", each DateTime.Time([Last Refresh]), type time)

in
  #"Insert Time"
```

| **ID** | **Name** | **Type** | **Sample** | **Notes** |
| --- | --- | --- | --- | --- |
| 1 | Last Refresh | Date | 2024-12-05 1:19.22 | General Date |
| 2 | Date | Date | December 5, 2024 | Long Date |
| 3 | Time | Date | 1:19.22 PM | Long Time |

<br>

## Relationships

*List all relationships in the model; the following can be used in DAX Query View from within Power BI to retrieve the relationship details:*

```dax
EVALUATE
VAR _Result =
  SELECTCOLUMNS(
    INFO.VIEW.RELATIONSHIPS(),
    "ID", [ID],
    // "Relationship", [Relationship],
    "From", [FromTable] & "[" & [FromColumn] & "]",
    "To", [ToTable] & "[" & [ToColumn] & "]",
    "Cardinality", [FromCardinality] & "-to-" & [ToCardinality],
    "Cross-filter Direction", SWITCH( TRUE(),
        [CrossFilteringBehavior] = "OneDirection", "Single",
        [CrossFilteringBehavior] = "BothDirections", "Both",
        [CrossFilteringBehavior] ),
    "Status", IF( [IsActive] = TRUE(), "Active", "Inactive" )
  )

RETURN
_Result
```

| **ID** | **From** | **To** | **Cardinality** | **Cross-Filter Direction** | **Status** |
| --- | --- | --- | --- | --- | --- |
| 1 | Invoices[Customer ID] | Customers[Customer ID] | Many-to-One | Single | Active |
| 2 | Invoices[Invoice Date] | Dates[Date] | Many-to-One | Single | Active |
| 3 | Orders[Order Date] | Dates[Date] | Many-to-One | Single | Active |
| 4 | Orders[Product ID] | Products[Product ID] | Many-to-One | Single | Active |
| 5 | Orders[Region ID] | Regions[Region ID] | Many-to-One | Single | Active |
| 6 | Orders[Customer ID] | Customers[Customer ID] | Many-to-One | Single | Active |

<br>

## Measures

A manually-entered **Key Measures** table was added and various measures.

*To format all measures in a Power BI model:*

1. *Open [Power BI Desktop] and the PBIX file of interest*
2. *Open the [Tabular Editor V2] (Version 2.13 or higher) external tool*
3. *Select the [C# Script] tab*
4. *Enter the below in the C# Script window, then click the [Run] button*

```
bool shortFormat = false;
bool skipSpaceAfterFunctionName = true;
FormatDax(Model.AllMeasures, shortFormat, skipSpaceAfterFunctionName);
```

*Method:*

*List all measures in the model; the following can be used in DAX Query View from within Power BI to retrieve the measure names and expressions:*

```dax
EVALUATE
VAR _Result =
  SELECTCOLUMNS(
    INFO.VIEW.MEASURES(),
    "Documentation", [Name] & " = " & [Expression]
  )

RETURN
_Result
```

*Alternate Method 1 (DAX Studio): To list all the measures in a Power BI model:*

1. *Open [Power BI Desktop] and the PBIX file of interest*
2. *Open the [DAX Studio] external tool*
3. *Right-click on any table in the [Metadata] tab of the [Query] pane and select [Define All Measures (All Tables)*

*Alternate Method 2 (TMDL): To list all the measures in a Power BI model (including format strings):*

1. *Open [Power BI Desktop] and the PBIX file of interest*
2. *In the left sidebar, select [TMDL View]*
3. *Drag the desired table (containing the measures) into the TMDL window*
4. *Remove unwanted lines (createOrReplace, table, lineageTag, partition, annotation)*

```dax
Total Sales = SUMX( Orders, Orders[Quantity] * RELATED( Products[Unit Price] ) )

Total Costs = SUMX( Orders, Orders[Quantity] * RELATED( Products[Unit Cost] ) )

Total Profit = [Total Sales] - [Total Costs]

Profit % = DIVIDE( [Total Profit], [Total Sales], 0 )
```

## Resources

*LinkedIn Posts*

The LinkedIn posts covering the design document are listed below: <br>
[1. General and Scope](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7295051537129615362-px8i) <br>
[2. Workflow, Issues, and Business Rules](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7300125349743316992-tG1U) <br>
[3. Data](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7305187426413563904-6yVG) <br>
[4. Reports](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7310232246613934082-w7iW) <br>
[5. Validation](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7317852256215662593-MvcI) <br>
[6. Deployment](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7322931000085295104-BIIF) <br>
[7. Model](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7310232246613934082-w7iW) *** FIX *** <br>

*Samples*

Sample document fragments covering specific sections are available in the GitHub repo: <br>

[1. Design Document - Sample Fragment 01 - General and Scope](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2001%20-%20General%20and%20Scope%20-%20V0.1.docx) <br>
[2. Design Document - Sample Fragment 02 - Workflow, Issues, and Business Rules](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2002%20-%20Workflow%20Issues%20and%20Business%20Rules%20-%20V0.2.docx) <br>
[3. Design Document - Sample Fragment 03 - Data](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2003%20-%20Data%20-%20V0.3.docx) <br>
[4. Design Document - Sample Fragment 04 - Reports](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2004%20-%20Reports%20-%20V0.4.docx) <br>
[5a. Design Document - Sample Fragment 05 - Validation](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2005%20-%20Validation%20-%20V0.5.docx) <br>
[5b. Design Document - Sample Validation Spreadsheet](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Validation%20Spreadsheet%20-%20V0.5.xlsx) <br>
[6. Design Document - Sample Fragment 06 - Deployment](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2006%20-%20Deployment%20-%20V0.6.docx) <br>
[7a. Design Document - Sample Fragment 07 - Model](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2006%20-%20Model%20-%20V0.7.docx) *** CHECK *** <br>
[7b. Design Document - Sample Power BI File](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Power%20BI%20File.pbix) *** CHECK *** <br>
