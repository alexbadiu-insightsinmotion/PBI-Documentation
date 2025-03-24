<img width="1920" alt="09 - Image - Title - Reports" src="https://github.com/user-attachments/assets/124ffa1b-0dd0-4ba9-a9d6-2c6e95a39302" />

**What Report characteristics should be described in a Design Document?**

Many Power BI reporting efforts consist of multiple files, and, as such, the design will likely be spread-out, and it can thus be difficult to get an overall picture (especially if multiple developers are involved). The design document provides a **one-stop-shop** and can improve both the clarity and the consistency of the design (not to mention, at the same time reducing rework).

The reports in the project will ideally not only share a theme and a common data model, but there are likely other common items as well (e.g., theme, navigation, etc.). The items that are specific to an individual report (e.g., filters, visuals, etc.) are described separately below.

## Common

Describe the design features that will be common to all reports in the project.

### Theme

Describe the theme file used in the reports, including page size, colours, fonts, font sizes, etc.

| **ID** | **Item** | **Description** | **Notes** |
| --- | --- | --- | --- |
| *T-1* | *Page* | *Desktop:*<br>*Canvas size - 1600 by 900*<br>*Canvas background - light grey (#F0F0F0)*<br>*Wallpaper - none*<br>*Filter cards - default colours*<br><br>*Mobile:*<br>*n/a* | *pixels, width by height* |
| *T-2* | *Colours, Main* | *Shades of blue*<br>*#8BC7F7*<br>*#46B3F3*<br>*#009FEF*<br>*#008CEE*<br>*#0078ED*<br>*#0050EB*<br>*#0641C8*<br>*#0B31A5* | *Based on “Storm” theme*<br>*included with Power BI Desktop* |
| *T-3* | *Colours, Sentiment* | *Green-yellow-red (i.e., “stoplight”)*<br>*Negative - red (#E81123)*<br>*Positive - green (#3BB44A)*<br>*Neutral - yellow (#F2C811)* |  |
| *T-4* | *Fonts* | *Visual titles - Segoe UI Semibold, 12 pt, black (#000000)*<br>*Visual subtitles - Segoe UI, 10 pt, dark grey (#969696)*<br>*Axis labels - Segoe UI, 8pt, black*<br>*Axis titles - none (disabled; rather, include in visual title)*<br>*Data labels - Segoe UI, 8pt, black*<br>*Callout values - Segoe UI Semibold, 18 pt, black* |  |
| *T-5* | *Visuals* | *Padding (pixels) - 4/4/4/4*<br>*Rounded corners (visuals) - 8 pixels*<br>*Rounded corners (cards, buttons) - 4 pixels*<br>*Background Colour - white (#FFFFFF)*<br>*Shadow - none*<br>*Glow - none* |  |
| *T-6* | *Miscellaneous* | *Visual Titles - off*<br>*Icons - off*<br>*Grid lines - light grey (#E3E3E3)*<br>*Tooltips - Modern*<br>*Pages - Only 1 visible, all others hidden* |  |

### Filters

Describe the filters that will be applied to every report:

- Only include active customers (i.e., those with active invoices)
- Only include active invoices (i.e., those with non-deleted invoices)
- Only include invoices from the current and past two calendar years

Here's an example:

<img width="160" alt="09 - Image - Filter Pane" src="https://github.com/user-attachments/assets/3ae730cc-9061-4ed0-a746-ba40e986e865" />

Filters specific to each report should be listed in their respective sections below.

### Navigation

Navigation should be self-evident (and self-explanatory) and should require no audience instructions.

An information overlay can also be added to provide additional identification and illustration of the use of the navigation items. Many design tools can be used for such an effort.

Here's a quick procedure:

- Ensure the Power BI report is finished
- Grab a screenshot of final Power BI report page
- Edit the screenshot image in a design tool
- Overlay a full-screen rectangle (no border, partially transparent)
	- *The Power BI report screenshot image is now in the background*
- Add callouts for the navigation features as desired
- Hide or remove the background image
- Save the image (as picture)
- Add the image to the Power BI Desktop file (expand to full-screen)
- Add 2 bookmarks (panel open, panel closed)
- Add info button to activate the panel open bookmark
- Edit the image action to activate the panel closed bookmark

*Guy in a Cube* posted a video back in 2021 illustrating such a process:

https://www.youtube.com/watch?v=yYr_SlG8bpw

The existing audience experience with the navigation currently employed in operational Power BI reports in your organization should be the default navigation method and only changed if specifically requested by the audience(s) for the report(s).

A Power BI App should be the first option for multi-report navigation; individual reports can then be designed without a navigation system (i.e., pages only), with the App providing the default hierarchical navigation with no code.

If standalone navigation will be used in each report, arrange items as a top bar or sidebar (or both) and design with "bounce" (subtle changes during mouseover and selection [e.g., font size, font colour, background colour, underline, etc.]) so users intuitively know where they are and how to navigate. Describe all items, including [ID], name (category and subcategory), and design (normal, hover, selected).

Here's an example:

| **ID** | **Name (Category / Subcategory)** | **Design / Selected / Unselected / Hover** |
| --- | --- | --- |
| *N-1* | *Invoices* | *DESIGN:*<br>* *Type=button*<br>* *Shape=any, with border=off*<br>* *Action=page navigation (subcategory 1)*<br><br>*DEFAULT (selected):*<br>* *Font=Segoe UI, white, 10 pt*<br>* *Background=dark blue*<br>* *Navigation=page, Invoices-All*<br><br>*DEFAULT (unselected):*<br>* *Font=Segoe UI, medium grey, 10 pt*<br>* *Background=medium blue*<br>* *Navigation=page, Invoices-All*<br><br>*HOVER:*<br>* *Font=Segoe UI, dark grey,* ***11 pt***<br>* *Background=medium grey*<br>* *Navigation=page, Invoices-All* |
| *N-2* | *Invoices / All* | *(same as N-1 above)* |
| *N-3* | *Invoices / Current* | *(same as N-1 above, but with adjusted page navigation and<br>selected and unselected defaults reversed)* |
| *N-4* | *Invoices / Upcoming* | *(same as N-1 above, but with adjusted page navigation and<br>selected and unselected defaults reversed)* |
| *N-5* | *Invoices / Historical* | *(same as N-1 above, but with adjusted page navigation and<br>selected and unselected defaults reversed)* |

*NOTE: Drill-through is not navigation and should rather be described in each specific report.*

### Page Header

Describe all elements that will be present in the header of each page.

Here’s an example:

Each page of the report will include the following header elements:

- Report title
- Horizontal 2-level navigation menu (level 1 = category [above], level 2 = subcategory, or page [below])
  + Invoices
    - All
    - Current
    - Upcoming
    - Historical
  + Customers
    - Level
    - Tier
    - Country
  + Other
    - Addresses
    - Known Issues
- Language slicer
  + EN/FR
- Last data refresh date (from the common dataset used by the report)
  + *Note: this will reflect the last date/time the dataset was refreshed by the Power BI Service, and is not indicative of the date/time that the data was last extracted from the source systems*

### Page Footer

*Describe all elements that will be present in the footer of each page.*

*Here’s an example:*

*Each page of the report will include the following footer elements:*

- *Line – Separator (grey)*
- *Image – Logo (at left)*
- *Textbox - Filter Selections (in middle)*
- *Textbox (or Card) – Report ID / Version / Version Date (at right)*
- *Textbox (or Card) – Dataset ID / Version / Version Date (at right)*

### Slicers

Slicers should use the same design features and should require no audience instructions.

*Describe the slicers that will be included on all report pages.*

*Here’s an example:*

| **ID** | **Slicer** | **Design Features / Data / Notes** |
| --- | --- | --- |
| *n/a* | *General* | *Title=Segoe UI Semibold, 10 pt*<br>*Values=Segoe UI, 8 pt*<br>*Style=dropdown*<br>*Selection=multi-select; CTRL off; Select All off*<br>*Header icons=off*<br>*Search box=enabled* |
| *S-1* | *Fiscal year* | *Data=Dates[Fiscal Year]*<br>*Notes=search box unavailable as numeric data* |
| *S-2* | *Fiscal quarter* | *Data=Dates[Fiscal Quarter]*<br>*Notes=search box unavailable as numeric data* |
| *S-3* | *Date range* | *Type=between*<br>*Slider=on, responsive off*<br>*Data=Dates[Date]* |
| *S-4* | *Province* | *Type=text*<br>*Data=Countries[Province]* |
| *S-5* | *City* | *Type=text*<br>*Data=Countries[City]* |

## Specific

Describe the design features that will be used in each specific report in the project (e.g., filters [in addition to those already applied to the common data], pages, slicers, visuals, etc.).

Here are some descriptions:

## Semantic Model (specific)

Describe the design of each specific semantic model in each specific report, including all fact tables, dimension (lookup) tables, and supporting tables.

Assign an [ID] to each relationship and fully describe it, including the fields/columns that will be used to link tables, the cardinality, and the directionality of each relationship.

*(Note: This is the design intent, not the implementation; the DAX INFO functions will be used in the appendices [a subsequent issue] to extract the actual relationships from the developed model.)*

Here's an example:

| **ID** | **From (table[column])** | **To (table[column])** | **Cardinality / Directionality** |
| --- | --- | --- | --- |
| *CR-1* | *Dates[Date]* | *Invoices[Date]* | *C=one-to-many*<br>*D=single* |
| *CR-2* | *Customers[Customer ID]* | *Invoices[Customer ID]* | *C=one-to-many*<br>*D=single* |

Include an image of each specific data model in each specific report and arrange tables for clarity (e.g., waterfall design, with dimension (lookup) tables at the top, fact tables in the middle, supporting tables in the bottom-left, and measure tables in the top-right, etc.)

<img width="1272" alt="09 - Image - Data Model - Light Mode" src="https://github.com/user-attachments/assets/b1da368c-84bf-47c0-8472-ba117593c45b" />

### AR01 – All Invoices

This report shows summary and KPI information about all invoices, and includes the following:


Filters:

-	none

Slicers:

- Fiscal year and fiscal quarter hierarchy
- Province and city hierarchy
- Customers

KPIs:

- Count of customers
- Count of invoices
- Total invoice amount
- Total invoice outstanding amo9unt
- Earliest invoice date
- Latest invoice date

Gauges:

- Paid invoice amount vs. total invoice amounts
- Outstanding invoice amount vs. total invoice amounts

Horizontal bar charts:

- Total invoice amounts by province
- Total invoice amounts by payment method

### AR02 – Current Invoices

This report shows detailed information about unpaid invoices (with aging), and includes the following:

Filters:

-	Invoices[Status] != PAID
-	Invoices[Status] IN { ISSUED, OVERDUE }

Slicers:

- Fiscal year
- Fiscal quarter
- Province
- City
- Customers
- Payment method, Funds centre, Cost centre, Material type

KPIs:

- Total invoice amount
- Total invoice paid amount
- Total invoice outstanding amount

Matrix:

- Customers on rows
- Invoice aging groups on columns

Table:

- Columns for invoice aging group, outstanding invoice amount per group, outstanding invoice amount percentage of total per group (percentage with data bars)
- Horizontal bar chart:
  + Outstanding invoices by customer

### AR03 – Upcoming Invoices

This report shows detailed information about in-process and future invoices, and includes the following:

Filters:

-	Invoices[Status] IN { SCHEDULED, DRAFT, IN PROGRESS, APPROVED }

Slicers:

- Fiscal year
- Fiscal quarter
- Province
- City
- Customers

KPIs:

- Total invoice amount
- Total invoice paid amount
- Total invoice outstanding amount

Table:

- Invoice detail, with columns for customer, order/project ID, (temporary placeholder) invoice number, (anticipated) amount, (scheduled) invoice date

### AR04 – Historical Invoices

This report shows detailed information about paid invoices, and includes the following:

Filters:

-	Invoices[Status] = PAID

Slicers:

- Fiscal year
- Fiscal quarter
- Province
- City
- Customers

Maps:

- Invoice amount by city
- Outstanding invoice amount by city

## Resources

*LinkedIn Posts*

The LinkedIn posts covering the design document are listed below: <br>
[1. General and Scope](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7295051537129615362-px8i) <br>
[2. Workflow, Issues, and Business Rules](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7300125349743316992-tG1U)) <br>
[3. Data](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7305187426413563904-6yVG) <br>
[4. Reports](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7305187426413563904-6yVG) *** FIX *** <br>

*Samples*

Sample document fragments covering specific sections are available in the GitHub repo: <br>

[1, Design Document - Sample Fragment 01 - General and Scope](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2001%20-%20General%20and%20Scope%20-%20V0.1.docx) <br>
[2. Design Document - Sample Fragment 02 - Workflow, Issues, and Business Rules](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2002%20-%20Workflow%20Issues%20and%20Business%20Rules%20-%20V0.2.docx) <br>
[3. Design Document - Sample Fragment 03 - Data](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2003%20-%20Data%20-%20V0.3.docx) <br>
[4. Design Document - Sample Fragment 04 - Reports](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2003%20-%20Reports%20-%20V0.4.docx) *** CHECK *** <br>
