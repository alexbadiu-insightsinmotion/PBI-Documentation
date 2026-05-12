<img width="1277" height="712" alt="217 - Image - Title - Performance Analyzer" src="https://github.com/user-attachments/assets/d9b4840a-ae35-4a59-9af8-6220b9c70f75" />

## Performance Analysis

*May 11, 2026*

Deneb/Vega-Lite can be used to present ***Power BI Performance Analyzer*** data linked to ***Power BI PBIR*** data and compare multiple visuals within a report.

This exploration was first envisaged by ***Alexandru Badiu*** after viewing ***Chris Webb***’s blog post late last year:
https://blog.crossjoin.co.uk/2025/12/21/visualising-power-bi-performance-analyzer-data-with-a-vibe-coded-custom-visual/

To use this solution on your report of interest, follow these steps:
1.	Create an ***Analysis*** PBIX file, either by downloading the complete file linked below or by creating a new, empty PBIX, running the TMDL script linked below to create the M code and measures, using the Deneb templates linked below to create 2 new visuals, and creating native Power BI slicers and tables (see below for more details)
2.	Save the report of interest as a ***Power BI Project*** and note the folder
3.	Ensure all visuals have a title (must be unique within the page)
4.	Run ***Performance Analyzer*** against each page in the PBIP report, export the JSON results to a folder, and note the folder
5.	Using the ***Analysis*** PBIX, select ***Home \ Queries \ Transform data \ Edit Parameters*** from the Power BI Desktop toolbar to update the first 4 parameters in the [Analysis] PBIX to reflect the paths to the PBIP and PA data
    - Update the value for the ***folder_PBIR_Data*** parameter (e.g., C:\Temp\Performance\Sales.Report\definition\
    - Update the value for the ***folder_PBIR_Sample_Page*** parameter (e.g., C:\Temp\Performance\Sales.Report\definition\pages\1fdd4311559dac8e97a3)
    - Update the value for the ***folder_Performance_Data*** parameter (e.g., C:\Temp\Performance\Sales.Performance)
    - Update the value for the ***file_Visual_Types*** parameter (e.g., C:\Temp\Performance\Power BI Visual Internal and Display Names.json)

<br>

<img width="400" height="255" alt="217 - Performance Analyzer - Edit Parameters" src="https://github.com/user-attachments/assets/a4e83dad-993a-476e-930f-43e2aa241a30" />

<br>

> [!NOTE]
> *There was a tenant issue during development when using the Azure Maps visual, so testing against map visuals could not be performed*

> [!NOTE]
> *Although I’m the one releasing this solution, it is truly a collaborative effort and would not have been possible without the generous assistance of two of my fellow Enterprise DNA Power BI Expert Panel members, ***Alexandru Badiu*** and ***Melissa de Korte***. (I’m certain the Power Query code could be vastly improved, but as this is an initial effort, and my M skills are minimal at best by comparison, please excuse the verbose and non-optimized M code.)*

The example presented herein imports and links 2 types of Power BI data:
- the actual report design (in JSON format as created/maintained when the file is saved as a ***Power BI Project***, so ***PBIR*** format), and
- the ***Performance Analyzer***, or ***PA*** output, exported as a JSON file for each page in the report

The modelled data is combined with a number of measures and used to support visuals on 4 pages:
- a Deneb visual to compare multiple visuals on a page
- another Deneb visual to provide a deeper-dive into a single visual
- native Power BI tables to present the PBIR data (pages and visuals), and
- a native Power BI table to present the PA data (events).

The development of these Deneb templates used 5 reports for testing: a synthetic ***Sales*** dataset and visuals, a synthetic ***AI-generated*** dataset and visuals, and 3 of my Enterprise DNA challenge entries (8 [Service Desk Issues], 14 [Emergency Services Analytics], and 15 [Formula 1 Analysis]).

> [!NOTE]
> *The pages and visuals in my C8, C14, and C15 reports were re-created as "old" Power BI files don't have the latest syntax when saved as Power BI Project files; it is recommended that only newer files be used*

I provide 2 Deneb templates for this scenario. The legend and timeline code is common to both the ***Multiple Visuals*** and ***Single Visual*** pages, and the more extensive ***Single Visual*** code example illustrates a number of Deneb/Vega-Lite features, including:

<br>

0 - General:
- a ***title*** block with multi-line ***subtitle*** using an array and ***direct data access*** to get the visual name
- a standard Power BI dataset
- a shared ***transform*** block with:
    - a ***filter*** transform to remove the [User Action] event
    - 11x ***calculate*** transforms to assign internal names to the Power BI dataset fields
    - a ***calculate*** transform to set the event order
      - *(a "quick-and-dirty" "hard-coded" sorting method was used and will not sort properly if different event names are present in the dataset)*
    - a ***calculate*** transform to set the event colour using parameter-based ***Power BI theme colours*** 
    - a ***joinaggregate*** transform to determine the minimum start time
    - 2x ***calculate*** transforms to determine the zero-based event start and end times
    - an ***extent*** transform to store a 2-dimensional array of the minimum and maximum zero-based event end time into a parameter
- a shared ***params*** block with:
    - an ***expr*** parameter to extract the 2nd element from the zero-based event end time parameter created by the ***extent*** transform
    - a ***value*** parameter for the [Visual Container Lifecycle] event colour
    - 3x ***expr*** parameters for the query & render, execution, and 0ms events using ***Power BI theme colours***
- a ***vconcat*** block for the legend, timeline, KPI cards, and category table

1 - Legend:
- a hard-coded 4-record dataset
- a ***hconcat*** block for the left (aligned) and right (aligned) legend
- a ***resolve/scale/color*** block set to ***independent*** to disable (override) Vega-Lite's default behaviour of merging legends

1a - Left Legend:
- a nested ***transform*** block with a ***filter*** transform to restrict the dataset to the first 3 records
- an ***arc*** mark with zero radius to show the legend only
- ***conditional colour*** (lifecycle=light grey; parent/execution set to ***Power BI theme colours***)
- legend with square symbols and fixed X position (-200)

1b - Right Legend:
- a nested ***transform*** block with a ***filter*** transform to restrict the dataset to the last (4th) record
- an ***arc*** mark with zero radius to show the legend only
- ***conditional colour*** (0ms events set to ***Power BI theme colour***)
- legend with diamond symbols and fixed X position (340)

2 - Timeline:
- a nested ***transform*** block with:
    - a ***calculate*** transform to determine the composite event label (level / name)
    - a ***calculate*** transform to copy the maximum event end time from the parameter to a data column
- a shared ***encoding*** block with:
    - ***Y*** axis:
        - uses the composite event level/name field to ensure all layered marks use the same ***Y*** axis
        - a ***sort*** block to use the event order (calculated above)
        - ***conditional padding*** to indent by level
        - ***conditional font weight*** (lifecycle/query/render=bold, others=normal)
        - extracts the name from the event ***composite label***
    - ***X*** axis:
        - a custom ***label expression*** to append a "ms" suffix to the axis value
        - ***top*** orientation
        - a custom ***scale/domainMax*** expression to set the scale to 10% above the maximum event end time parameter value
- a ***layer*** block for the non-zero duration events, zero duration events, maximum duration, and duration labels

2a - Non-Zero Duration Events:
- a nested ***transform*** block with a ***filter*** transform to restrict the dataset to events with durations greater than zero
- a ***bar** mark with:
    - ***ranged*** X coordinates
    - ***conditional colour*** using the event colour calculated above
    - a ***named style***

2b - Zero Duration Events:
- a nested ***transform*** block with a ***filter*** transform to restrict the dataset to events with zero duration
- a ***point/diamond** mark with:
    - ***conditional colour*** using the event colour calculated above
    - a ***named style***
    - a shared ***encoding*** block with:
        - ***X*** axis:
            - a custom ***label expression*** to append a "ms" suffix to the axis value
            - ***bottom*** orientation (to show a 2nd ***X*** axis)
            - a custom ***scale/domainMax*** expression to set the scale to 10% above the maximum event end time parameter value

2c - Maximum Duration:
- a ***rule*** mark with:
    - ***Y*** axis set to null to turn off the axis specified in Timeline ***shared encoding*** block
    - a ***named style***

2d - Duration Labels:
- a nested ***transform*** block with:
    - a ***calculate*** transform to determine the ***X*** coordinate of the data label (lifecycle=end, query/render=start, if duration <50 then end else start)
- a ***text*** mark with:
    - ***conditional colour*** (query/render=white, others=dark grey)
    - ***conditional font weight*** (lifecycle/query/render=bold, others=normal)
    - value formatting via a ***Power BI format string*** as enabled by Deneb
    - ***X axis*** labels turned off
    - a ***named style***

3 - KPI Cards:
- a nested ***transform*** block with:
    - 4x ***calculate*** and ***joinaggeregate*** transforms to get the lifecycle, model, DAX, and render durations
    - a ***window/rank*** transform to generate sequential numbers that can be used by subsequent filter
    - 8x ***calculate*** transforms to set X and Y values for the card rectangles, titles, and values
    - a ***joinaggregate/count*** transform to get the total number of events
    - 2x ***calculate*** transforms to determine the card values and formulae
    - a ***filer*** transform to restrict the dataset to 5 records
- a ***shared encoding*** block with fixed X and Y ***scale/range*** blocks
- a ***layer*** block for the rectangles, titles, values, info text background bars, and info text

3a - Rectangles:
- a ***bar*** mark with:
    - ***ranged X and Y*** coordinates
    - a ***named style***

3b - Titles:
- a ***text*** mark
    - ***baseline*** set to bottom
    - a ***named style***

3c - Values:
- a ***text*** mark
    - ***baseline*** set to top
    - a ***named style***

3d - Info Background Rectangles:
- a nested ***transform*** block with 4x ***calculate*** transforms to set the X and Y coordinates (left, right, top, bottom)
- a ***bar*** mark with a ***named style***

3e - Info Text:
- a nested ***transform*** block with 2x ***calculate*** transforms to set the X and Y coordinates of the info icon
- a ***text*** mark with:
    - hard-coded unicode value (question mark in a diamond)
    - a ***tooltip*** displaying the formula used to calculate the card value
    - a ***named style***

4 - Table:
- a nested ***transform*** block with:
    - a ***calculate*** transform to add a 2-dimensional array (0, 1) to the dataset
    - a ***flatten*** transform to duplicate the records (using the 2-dimensional array)
    - a ***filter*** transform to restrict the dataset to the original number of records plus 1 for the total
    - a ***calculate*** transform to set the event name of the total row
    - 5x ***calculate*** transforms to determine the model, DAX, query, render, and total duration
    - a ***calculate*** transform to assign events to categories
    - an ***aggregate*** transform to determine the category event count and duration
        - *(additional fields were added to "pass-through" the aggregation [thus becoming accessible in the aggregated dataset])*
    - a ***calculate*** transform to set the category names
    - a ***calculate*** transform to recalculate the category durations
    - a ***calculate*** transform to append a unicode suffix (question mark in a diamond) to indicate the presence of a tooltip
    - a ***calculate*** transform to compose a tooltip string of all category events
    - 5x ***joinaggregate/max*** transforms to determine the maximum values for the model, DAX, query, render, and total duration
    - 2x ***calculate*** transforms to determine the category average values
    - 2x ***calculate*** transforms to determine the category weight (with value formatting via a ***Power BI format string*** as enabled by Deneb)
- a ***shared encoding*** block to ensure all layered mark use the same axes, ordering, and scales
- a ***layer*** block for the background bar, category, count, average, and weight

4a - Background Bars:
- a ***bar*** mark with:
    - ***conditional colour*** (title=dark grey, total=light grey, others=transparent)
    - ***conditional corner rounding*** (title top left and right=8, total bottom left and right=8, others 0)
    - hard-coded full-width ***ranged X*** values

4b - Category:
- a ***text*** mark with:
    - ***conditional colour*** (title=white, others=dark grey)
    - ***conditional font size*** (category=16, others=14)
    - ***conditional font weight*** (title/total=bold, others=normal)
    - a custom ***tooltip*** displaying the category events

4c - Count:
- a ***text*** mark with:
    - ***conditional colour*** (title=white, others=dark grey)
    - ***conditional font size*** (category=16, others=14)
    - ***conditional font weight*** (title/total=bold, others=normal)

4d - Average:
- a ***text*** mark with:
    - ***conditional colour*** (title=white, others=dark grey)
    - ***conditional font size*** (category=16, others=14)
    - ***conditional font weight*** (title/total=bold, others=normal)
    - value formatting via a ***Power BI format string*** as enabled by Deneb

4e - Weight:
- a ***text*** mark with:
    - ***conditional colour*** (title=white, others=dark grey)
    - ***conditional font size*** (category=16, others=14)
    - ***conditional font weight*** (title/total=bold, others=normal)
    - value formatting via a ***Power BI format string*** as enabled by Deneb

5 - Config:
- configuration values set for:
    - border (colour [stroke] set to null)
    - title font attributes (family, size, weight, style, colour)
    - subtitle font attributes (family, size, weight, style, colour)
    - legend font attributes (family, size, weight, style, colour)
    - facet header font attributes (family, size, weight, style, colour) [used by ***multiple visuals*** Deneb code, but repeated here to ensure the same configuration settings are used for both visuals]
    - X axis settings for title (off), ticks, grid, domain, and labels (tick count, domain width and colour, label font family, size, and colour)
    - Y axis settings for title (off), ticks, grid, domain, and labels (domain width and colour, label font family, size, and colour)
- named styles:
    - non-zero duration bar (corner rounding)
    - zero duration point (filled, size)
    - maximum duration rule (stroke dash pattern, colour)
    - KPI card bar (corner rounding, fill colour, stroke colour [slightly lighter to simulate shadow])
    - KPI card title font attributes (family, size, weight, style, colour)
    - KPI card value font attributes (family, size, weight, style, colour)
    - KPI card info background bar (corner rounding, colour)
    - KPI card info font attributes (family, size, colour)

<details closed>
<summary>Here's the steps to manually create an Analysis PBIX file:</summary>

- Download the ***917.5 - Data - Power BI Visual Internal and Display Names - Performance Analysis*** JSON data file linked below
- Create a new, empty PBIX file
- Open the ***TMDL View***, paste the text from the ***917.4 - TMDL - Performance Analysis - All*** TMDL script file linked below, adjust the file paths as necessary, and click ***Apply***  then ***Refresh***
- Create 4 new pages, one each for:
  - Multiple Visuals
  - Single Visual
  - PBIR Data
  - PA Data
- On the ***Multiple Visuals*** page, create
  - ***Pages*** slicer: 
    - Pages \ pageName
    - Single select
    - Filter out (Blank) (basic or advanced)
  - ***Visuals*** slicer:
    - Visuals \ visualName
    - ***Multi-select***
    - Filter out (Blank) (advanced filtering --> "is not blank")
  - ***Deneb*** visual:
    - Create a new, empty ***Deneb*** visual
    - Add data fields for:
      - Pages \ pageId
      - Visuals \ visualId
      - Visuals \ visualName
      - Visuals \ visualType
      - Performance \ events.id
      - Performance \ events.name
      - Performance \ events.start
      - Performance \ events.end
      - Performance \ events.parentId
      - Key Measures \ Duration
      - Key Measures \ Hierarchy Level
    - Edit the Deneb visual and select the ***917.1 - JSON - Deneb Template - Performance Analysis - Multiple Visuals*** template linked below
- On the ***Single Visual*** page, create
  - ***Pages*** slicer: 
    - Pages \ pageName
    - Single select
    - Filter out (Blank) (basic or advanced)
  - ***Visuals*** slicer:
    - Visuals \ visualName
    - ***Single-select***
    - Filter out (Blank) (advanced filtering --> "is not blank")
  - ***Deneb*** visual:
    - Create a new, empty ***Deneb*** visual
    - Add data fields for:
      - Pages \ pageId
      - Visuals \ visualId
      - Visuals \ visualName
      - Visuals \ visualType
      - Performance \ events.id
      - Performance \ events.name
      - Performance \ events.start
      - Performance \ events.end
      - Performance \ events.parentId
      - Key Measures \ Duration
      - Key Measures \ Hierarchy Level
    - Edit the Deneb visual and select the ***917.2 - JSON - Deneb Template - Performance Analysis - Single Visual*** template linked below
- On the ***PBIR Data*** page, create
  - ***Pages*** table, with columns for: 
    - Pages \ pageId
    - Pages \ pageName
    - Pages \ pageOrder
  - ***Visuals*** table, with columns for:
    - Visuals \ visualId
    - Visuals \ displayName
    - Visuals \ visualName
    - Key Measures \ Visual Lifecycle Duration 
    - Key Measures \ Visual Performance Icon 
    - Key Measures \ Visual Performance Explanation
  - Disable Totals
- On the ***PA Data*** page, create
  - ***Pages*** slicer: 
    - Pages \ pageName
    - Single select
    - Filter out (Blank) (basic or advanced)
  - ***Events*** table, with columns for:
    - Pages \ pageName
    - Visuals \ visualName
    - Performance \ events.id
    - Performance \ events.name
    - Performance \ events.start
    - Performance \ events.end
    - Performance \ events.parentId
    - Key Measures \ Duration
    - Key Measures \ Hierarchy Path
    - Key Measures \ Hierarchy Level
  - Disable Totals

</details>

<details closed>
<summary>Here's the Multiple Visuals template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v6.json",
  "usermeta": {
    "information": {
      "uuid": "77c2cbe4-2d73-49ee-b8e5-e3d31ee27e0f",
      "generated": "2026-05-08T18:30:21.173Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Performance Analyzer Export Analysis - Multiple Visuals",
      "description": "Analyzing multiple Power BI visuals at-a-time, this visual presents Performance Analyzer data exported from Power BI report pages linked to Power BI Project data (PBIR format)",
      "author": "Greg Philps"
    },
    "deneb": {
      "build": "1.9.0",
      "metaVersion": 1,
      "provider": "vegaLite",
      "providerVersion": "6.4.1"
    },
    "interactivity": {
      "tooltip": true,
      "contextMenu": true,
      "selection": false,
      "selectionMode": "simple",
      "highlight": false,
      "dataPointLimit": 50
    },
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  // visual title\r\n  \"title\": {\r\n    \"font\": \"Segoe UI\",\r\n    \"fontSize\": 24,\r\n    \"fontWeight\": \"bold\",\r\n    \"fontStyle\": \"italic\",\r\n    \"color\": \"#4A4A4A\",\r\n    \"subtitleFont\": \"Segoe UI\",\r\n    \"subtitleFontSize\": 16,\r\n    \"subtitleFontWeight\": \"normal\",\r\n    \"subtitleFontStyle\": \"italic\",\r\n    \"subtitleColor\": \"#969696\"\r\n  },\r\n  // legend\r\n  \"legend\": {\r\n    \"title\": null,\r\n    \"font\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelFontWeight\": \"normal\",\r\n    \"labelFontStyle\": \"italic\",\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  // facet header\r\n  \"header\": {\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 18,\r\n    \"labelFontWeight\": \"bold\",\r\n    \"labelFontStyle\": \"italic\",\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  \"axisX\": {\r\n    \"title\": false,\r\n    \"ticks\": true,\r\n    \"tickCount\": 10,\r\n    \"domain\": true,\r\n    \"domainWidth\": 2,\r\n    \"domainColor\": \"#A3A3A3\",\r\n    \"offset\": 4,\r\n    \"grid\": true,\r\n    \"gridColor\": \"#EEEEEE\",\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 10,\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  \"axisY\": {\r\n    \"title\": false,\r\n    \"ticks\": false,\r\n    \"domain\": true,\r\n    \"domainWidth\": 2,\r\n    \"domainColor\": \"#A3A3A3\",\r\n    \"offset\": 4,\r\n    // \"grid\": false,\r\n    // \"labels\": false,\r\n    \"labelPadding\": 4,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  \"style\": {\r\n    \"_non_zero_duration_bar_style\": {\r\n      \"cornerRadiusEnd\": 4\r\n    },\r\n    \"_zero_duration_point_style\": {\r\n      \"filled\": true,\r\n      \"size\": 200\r\n    },\r\n    \"_max_duration_rule_style\": {\r\n      \"strokeDash\": [\r\n        3,\r\n        3\r\n      ],\r\n      \"color\": \"#7D7D7D\"\r\n    },\r\n    \"_card_bar_style\": {\r\n      \"cornerRadius\": 8,\r\n      \"color\": \"#DDDDDD\",\r\n      \"stroke\": \"#EEEEEE\"\r\n    },\r\n    \"_card_title_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 14,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"normal\",\r\n      \"color\": \"#4A4A4A\"\r\n    },\r\n    \"_card_value_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 24,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"normal\",\r\n      \"color\": \"#707070\"\r\n    },\r\n    \"_info_bar_style\": {\r\n      \"cornerRadius\": 10,\r\n      \"color\": \"transparent\"\r\n    },\r\n    \"_info_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 16,\r\n      \"color\": \"#AAAAAA\"\r\n    }\r\n  }\r\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "pageId",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__1__",
        "name": "visualId",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__2__",
        "name": "visualName",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__3__",
        "name": "visualType",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__4__",
        "name": "events_id",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__5__",
        "name": "events_name",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__6__",
        "name": "events_start",
        "description": "",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__7__",
        "name": "events_end",
        "description": "",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__8__",
        "name": "events_parentId",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__9__",
        "name": "Duration",
        "description": "",
        "kind": "measure",
        "type": "numeric"
      },
      {
        "key": "__10__",
        "name": "Hierarchy Level",
        "description": "",
        "kind": "measure",
        "type": "numeric"
      }
    ]
  },
  // text and position only; formatting done in "config\title"
  "title": {
    "anchor": "start",
    "align": "left",
    "offset": 20,
    "text": "Performance Analyzer Export Analysis",
    "subtitle": "Analysis of event duration and decomposition | Multiple Visuals"
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "transform": [
    // remove [User Action] events
    {
      "filter": "datum['__5__'] != 'User Action'"
    },
    // use an internal development ID for easy dataset identification
    {
      "calculate": "1",
      "as": "_DEV_ID"
    },
    // assign internal names to dataset fields
    {
      "calculate": "datum['__0__']",
      "as": "_page_id"
    },
    {
      "calculate": "datum['__1__']",
      "as": "_visual_id"
    },
    {
      "calculate": "datum['__2__']",
      "as": "_visual_title"
    },
    {
      "calculate": "datum['__3__']",
      "as": "_visual_type"
    },
    {
      "calculate": "datum['__4__']",
      "as": "_event_id"
    },
    {
      "calculate": "datum['__5__']",
      "as": "_event_name"
    },
    {
      "calculate": "datum['__6__']",
      "as": "_event_start"
    },
    {
      "calculate": "datum['__7__']",
      "as": "_event_end"
    },
    {
      "calculate": "round( datum['__9__'] )",
      "as": "_event_duration"
    },
    {
      "calculate": "datum['__8__']",
      "as": "_event_parent_id"
    },
    {
      "calculate": "datum['__10__']",
      "as": "_hierarchy_level"
    },
    // further development needed: this is a "quick-and-dirty" "hard-coded" sorting method and will not sort properly if additional event names are present in the dataset 
    {
      "calculate": "indexof( ['Visual Container Lifecycle', 'Resolve Parameters', 'Query', 'Query Generation', 'Query Pending', 'Execute Semantic Query', 'Execute DAX Query', 'Execute Query', 'Serialize Rowset', 'Parse Query Result', 'Render', 'Data View Transform', 'Visual Update', 'Visual Update Async'], datum['_event_name'] )",
      "as": "_event_order"
    },
    // adjust Power BI theme colours as desired
    {
      "calculate": "datum['_event_name'] == 'Visual Container Lifecycle' ? _event_colour_1 : datum['_event_name'] == 'Query' ? _event_colour_2 : datum['_event_name'] == 'Render' ? _event_colour_2 : datum['_event_name'] == 'Execute Semantic Query' ? _event_colour_3 : pbiColor(7)",
      "as": "_event_colour"
    },
    {
      "joinaggregate": [
        {
          "op": "min",
          "field": "_event_start",
          "as": "_min_event_start"
        }
      ],
      "groupby": [
        "_visual_id"
      ]
    },
    {
      "calculate": "round( datum['_event_start'] - datum['_min_event_start'] )",
      "as": "_event_start_zero"
    },
    {
      "calculate": "round( datum['_event_end'] - datum['_min_event_start'] )",
      "as": "_event_end_zero"
    },
    {
      "extent": "_event_end_zero",
      "param": "_event_end_zero_extent_array"
    }
  ],
  "params": [
    {
      "name": "_max_event_duration",
      "expr": "_event_end_zero_extent_array[1]"
    },
    {
      // visual container lifecycle
      "name": "_event_colour_1",
      "value": "#E3E3E3"
    },
    // query, render
    {
      "name": "_event_colour_2",
      "expr": "pbiColor(3)"
    },
    {
      // execution task
      "name": "_event_colour_3",
      "expr": "pbiColor(5)"
    },
    {
      // 0ms event
      "name": "_event_colour_4",
      "expr": "pbiColor(7)"
    }
  ],
  "vconcat": [
    {
      "name": "LEGEND",
      "data": {
        "values": [
          {
            "_legend_id": 1,
            "_legend_size": 1,
            "_legend_label": "Parent Phase"
          },
          {
            "_legend_id": 2,
            "_legend_size": 1,
            "_legend_label": "Execution Task"
          },
          {
            "_legend_id": 3,
            "_legend_size": 1,
            "_legend_label": "Container Lifecycle"
          },
          {
            "_legend_id": 4,
            "_legend_size": 1,
            "_legend_label": "0ms Event"
          }
        ]
      },
      "hconcat": [
        {
          "name": "LEGEND_LEFT",
          "width": 370,
          "height": 20,
          "transform": [
            {
              "filter": "datum['_legend_id'] <= 3"
            }
          ],
          "mark": {
            "type": "arc",
            "radius": 0
          },
          "encoding": {
            "theta": {
              "field": "_legend_size",
              "type": "quantitative"
            },
            "color": {
              "field": "_legend_label",
              "type": "nominal",
              "scale": {
                "domain": [
                  "Parent Phase",
                  "Execution Task",
                  "Container Lifecycle"
                ],
                "range": [
                  {
                    "expr": "_event_colour_2"
                  },
                  {
                    "expr": "_event_colour_3"
                  },
                  {
                    "expr": "_event_colour_1"
                  }
                ]
              },
              "legend": {
                "orient": "none", // none, top-left, top-right
                "direction": "horizontal",
                "legendX": -200,
                "offset": 0,
                "symbolType": "square"
              }
            }
          }
        },
        {
          "name": "LEGEND_RIGHT",
          "width": 370,
          "height": 20,
          "transform": [
            {
              "filter": "datum['_legend_id'] > 3"
            }
          ],
          "mark": {
            "type": "arc",
            "radius": 0
          },
          "encoding": {
            "theta": {
              "field": "_legend_size",
              "type": "quantitative"
            },
            "color": {
              "field": "_legend_label",
              "type": "nominal",
              "scale": {
                "domain": [
                  "0ms Event"
                ],
                "range": [
                  {
                    "expr": "_event_colour_4"
                  }
                ]
              },
              "legend": {
                "orient": "none", // none, top-left, top-right
                "direction": "horizontal",
                "legendX": 340,
                "offset": 0,
                "symbolType": "diamond"
              }
            }
          }
        }
      ],
      "resolve": {
        "scale": {
          "color": "independent"
        }
      }
    },
    {
      "facet": {
        "row": {
          "field": "_visual_title",
          "type": "nominal",
          "header": {
            "title": null
          }
        }
      },
      "spec": {
        "name": "TIMELINE",
        "transform": [
          // use an internal development ID for easy dataset identification
          {
            "calculate": "4",
            "as": "_DEV_ID"
          },
          {
            "calculate": "pad( datum['_hierarchy_level'], 2, '0', 'left' ) + '-' + datum['_event_name']",
            "as": "_event_level_event_name_label"
          },
          {
            "joinaggregate": [
              {
                "op": "max",
                "field": "_event_end_zero",
                "as": "_max_event_duration_x"
              }
            ],
            "groupby": [
              "_visual_id"
            ]
          }
        ],
        "encoding": {
          "y": {
            "field": "_event_level_event_name_label",
            "type": "nominal",
            "axis": {
              "title": null,
              "labelAlign": "left",
              "labelPadding": {
                "expr": "200 - 10 * ( toNumber( slice( datum.value, 0, 2 ) ) - 1 )"
              },
              "labelExpr": "slice( datum.value, 3, 100 ) == 'Visual Container Lifecycle' ? upper( slice( datum.value, 3, 100 ) ) : slice( datum.value, 3, 100 )",
              "labelFontWeight": {
                "expr": "indexof( ['Visual Container Lifecycle', 'Query', 'Render'], slice( datum.value, 3, 100 ) ) > -1 ? 'bold' : 'normal'"
              }
            },
            "sort": {
              "field": "_event_order",
              "order": "ascending"
            }
          },
          "x": {
            "type": "quantitative",
            "axis": {
              "title": null,
              "orient": "top",
              "labelExpr": "datum.value + 'ms'"
            },
            "scale": {
              "domainMax": {
                // set X axis scale to 10% above maximum
                "expr": "_max_event_duration + ( _max_event_duration / 10 )"
              }
            }
          }
        },
        "layer": [
          {
            "name": "NON_ZER0_DURATION_EVENTS_BAR",
            "width": 780,
            "height": 300,
            "transform": [
              {
                "filter": "datum['_event_duration'] > 0"
              }
            ],
            "mark": {
              "type": "bar",
              "style": "_non_zero_duration_bar_style"
            },
            "encoding": {
              "x": {
                "field": "_event_start_zero",
                "axis": {
                  "labels": false
                }
              },
              "x2": {
                "field": "_event_end_zero"
              },
              "color": {
                "field": "_event_colour",
                "type": "nominal",
                "scale": null
              }
            }
          },
          {
            "name": "ZER0_DURATION_EVENTS_DIAMOND",
            "width": 780,
            "height": 300,
            "transform": [
              {
                "filter": "datum['_event_duration'] == 0"
              }
            ],
            "mark": {
              "type": "point",
              "shape": "diamond",
              "style": "_zero_duration_point_style"
            },
            "encoding": {
              "x": {
                "field": "_event_start_zero",
                "type": "quantitative",
                "axis": {
                  "title": null,
                  "orient": "bottom",
                  "labelExpr": "datum.value + 'ms'"
                },
                "scale": {
                  "domainMax": {
                    // set X axis scale to 10% above maximum
                    "expr": "_max_event_duration + ( _max_event_duration / 10 )"
                  }
                }
              },
              "color": {
                "field": "_event_colour",
                "type": "nominal",
                "scale": null
              }
            }
          },
          {
            "name": "MAX_DURATION",
            "mark": {
              "type": "rule",
              "style": "_max_duration_rule_style"
            },
            "encoding": {
              "x": {
                "field": "_max_event_duration_x",
                "type": "quantitative"
              },
              // turn off the Y axis
              "y": null
            }
          },
          {
            "name": "DURATION_LABELS",
            "transform": [
              {
                "calculate": "datum['_event_duration'] == 0 ? datum['_event_end_zero'] + if( datum['_event_end_zero'] <= 40, 1, 2) : datum['_event_name'] == 'Visual Container Lifecycle' ? datum['_event_end_zero'] : datum['_event_name'] == 'Query' ? datum['_event_start_zero'] : datum['_event_name'] == 'Render' ? datum['_event_start_zero'] : datum['_event_duration'] < 50 ? datum['_event_end_zero'] : datum['_event_start_zero']",
                "as": "_event_duration_label_x"
              },
              {
                "calculate": "datum['_event_end_zero'] - datum['_event_start_zero']",
                "as": "_event_duration"
              }
            ],
            "mark": {
              "type": "text",
              "align": "left",
              // adjust offsets as desired
              "xOffset": 4,
              "yOffset": 1,
              "fontWeight": {
                "expr": "indexof( ['Visual Container Lifecycle', 'Query', 'Render'], datum['_event_name'] ) > -1 ? 'bold' : 'normal'"
              },
              "color": {
                "expr": "indexof( ['Query', 'Render'], datum['_event_name'] ) > -1 ? 'white' : '#4A4A4A'"
              },
              "style": "_duration_text_style"
            },
            "encoding": {
              "text": {
                "field": "_event_duration",
                "type": "quantitative",
                "formatType": "pbiFormat",
                "format": "#,0ms"
              },
              "x": {
                "field": "_event_duration_label_x",
                "type": "quantitative",
                "axis": {
                  "labels": false
                }
              }
            }
          }
        ]
      }
    }
  ]
}
```

</details>

<details closed>
<summary>Here's the Single Visual template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v6.json",
  "usermeta": {
    "information": {
      "uuid": "e2ae22bb-a050-44a9-945c-cecb364d4d69",
      "generated": "2026-05-08T15:03:45.227Z",
      "previewImageBase64PNG": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAKwAAAB5CAYAAACkwspEAAAQAElEQVR4AeydB3yURfPH99IJRZDeiyhFqiBI751AaIIiRUF6EUR8BUQUEBVUelV6DyWUEIKoSAn4KgjoiwqKiJTQAwFCyuX+33nM3T8JueTucne5wPHJj92d3dnZnZ3bnd19njsP5f7n1kAW0oBmsG3bth0Ngtu1a1fX2PaAgIB8pBd36NChiJFmbUidhcD69u3bF03K27JlywLU/QE0HUj1LzAwMDe8m8G0bt26eaZaCCL1VKLMM0QV4UAwWuJJAW0CMosbac2bN3+iTZs2XY1pd5h1NOCBMWSjuZV0Ol1UQkLCBAxgGQgiPgb4xMfHT2HAl4BN4AuwEWxiwBcTLgBrwAawpHXr1p/AOwcEkS5End3ANb1e34P0BiOPt7f3BwaDITu0N6CNp/xqwo9J7yK+k3BEXFxcMdqVC/5L9+7d20r+R9A3kT+f+HLiswjX0Mbh1FWMdEnKVyeel/gSym0A84lvgFbUy8urH/EJYImPj08/Dw+P6sSljvzwuf+yiAY87ty5k5u2XsMwx2Ic1xjcr8AJDOEnBvUX4nHQE8BacAmcgbYPnngggx0N7SA0g6en5zn4fKBvhpYHWkUg/OVJHwQyowtPJPQboBW4Rfn7yLpGeAL8lj179iWEZYAPPDIzEuj8SN+jvLRFQj/kfQrtPvgbvAT+pmBZwut8SC7QFmkDVXv4wEeWLoG8X4k8Qx5RlYvQSyJuZA0NeISFhV3etWvX24lhH+JrwRSaf4eRXh4aGjowJCREsIVwIhgPbS4YQrmuoD+0OaQHEM4nlLLrif9K3mAwGrxOeg5hf9A1IiLiXeqXv4W7d++eT57wziDvHeJjgoKCogm3k260c+fOsVeuXOmMwd3GCEdBGwaGihzyjhGOAn9C+whMA93BO9T7JvSXQDcEfU5fnmRmn0/eZ9Q9CPp44q9Kv8l3/2URDciMp+bPn19m9uzZvtJmCUEuBjQU3/P+pEmTTDPQnDlzKm/cuFFmUClqAuWNvDJ7mujTp0/PvmjRIn8TITFy9OjROIxlWpcuXfZjiLovvvjiycSsVAMpj0/7cZMmTfRJ6yNeeO7cuXnBcyCvkZn25AK+INeCBQsK4DpcxkiHBwcHR0oZoQOtzZJ2wxU0YFkbPMRYKdqB2acvg96fsCNLbcuFCxf2xo9sUbBgwa7QS86bN68v9NzXr19/CSPoAd8b4BUwFP+wAWWakS9hf2hCH+Dn59cCV6MTvD2h9QFViL8OhoBXqb8ktC6ELyNvJPEa0PtS/zDi/YmPAf1Ad2bXdjly5GhFKOnelBG+nCzveUAlZLeljt6U7U17uoifCp7hA/E8YSXKi9yuifkNhg8fHku/3X9ZTAMeGNRF/Lj9LLtfEm7EeLbRh+9jY2NDSe8ePHjwel9f3wcYxZ8YxcmrV6+uGTRo0IYhQ4bMhDeMcB7YS/4N+H6FZxXp1WAxRhE8dOjQNQLK7oJ2kvgSMH/YsGFLBw8e/BPxTYRzqXMW+UdJL5c05VdhnItJfwlEXhA8Gykzh/RKymxGVgRl/klMr6INmzDQX8hbTn3zwY+UDxkwYMB30ETuJikrNMoaaK/7L4tpwMPf3z87hvhs/vz5X5aZCQxm0KsSCvozM3XCiAsywP4YR4DMuNBkNmwEn8yaMptWgccXnrygm8xilBnMLPkqGER6DLOcVcdjI0aMiAF30tKn5IMYY5mBAwfex6iP0Va3MRqV8oiFHv3797/J7LMqceZZxuwzk0HfSbiXvq7FRfiO+EnKyGy6mnA96ZngO3hmYLSHiZ+E53sM5iDx1dBlBlxAXOpbSHoGs52cAFCl+8+tAds1oG26zLFjcLfEoM3lCx0j/VNCN9wacIYG0jRYZzTALePR14A9e6gZ7MfDhhWZOnJwFVsqXr9wYdXNixYVtoX30qVL/ufOnat+7dq1nLbwu3mcqwH2KWav0p3VEs1gEzwMw3QG3QHOXYtynfk9CAULubpcC+T6tT/pA8QlLfiE+ARppKfOcNCgEoZK2liGUK5wF1LfDM5Ad5O3FVo7wjAg/GtJd+YkoCI+8DGMtglpU/3wfUq5HYm8O0jLlfFwaHJ9+zVpuSreGRAQsAzaVtLJnlWQdrlhXw2cDA//7Ocjh0MYp87oXMbwPPH56L4n4Skg1/FCXwDNYeOhGaxBr5YblK4zN0cXOWCvDdqAQRzuvwzktuoL0g2IS1owlrjchikPnaGTMuhWSNpYhlButAZR3xguIFqT1wlaCGErIPwvk97CFexpPrWtCxcufIi0qX743qRcQCJvAOkp5MtN2dvQm5F+nbD9jh07XiXsRPqifYfHXVtKDVSpW3e0itf3ZBy2oHMZwxLEh6D7NYQVQbdE+mBoDhsPzWDHzZt3evzseV+nbKQl6S4DhuztOmjQGUvKpiyTN2/eOyVKlAgrVqyYnOGmzHanXUwDVRo0kOc+MrVVmsFmagvcwt0asEIDmWaw7du3LwHq4PvUxRfNZ0mbO3TokJPy4gt3JF5Onmu1hE/KUD5nQEBAm1atWjVv3bp1feqRp8EkK10IL+VbgQ7A4vZKxfTxaXha4fd1JLSKF55q8HSgDqv0JHLpZ1V4xd+0SlfdunXzYe9QHV4L9CySnItMM9jevXtH4OscxvcJxxe9bkm3t2/fHkX5kL59+4YS/33v3r23LeGTMpSPQk5ov3799u/evfsg9ZwVuiUQXsqH9enTZzehxe2VuunjGXjCpM2EVvHiEx6HZzu6OkpoFW9YWNgJeLaIXNpvsa6CgoJi2Tv8BK9NepY+OxKZZrB3796tvnr16jdswb179963hU94kDtJQluQEblZkTcyMtJSXb3sSCNNWreHLHcsH2U7duxYl6XnOZaDp0g/J6+UEM8P6pFXmyWiDGhAXi3KVe3UqVMF0nVZXutQtnRgYGApltxnqa8JPNWJNyK/BmWfg78ytGSPHpYsWbJIo0aNWjRu3Hg64eepoD60VIErUM5cXnr0Fi1alE+vjLn8jMh1Yd7UdD+1YcOGjc6fP1/ilVdemWkB1iY1KkfGtRnW09OzG2eiNRISEup7eHjIQzCB3t7eLXU6XQXySsXFxdWmEWNABS8vr5qU7R4TE9Of8n0p34iy9SjTFNQj7wVodQjlOdgGsbGxRaA3pa488Jv+cuXK9TSJthxrmZ63JZ30rwsJc+iURp45HiPdzauUURcSosqH/vwZr0B/f/88TDrNmXzaMPG8hU89Gewk7rBz1odakoLggX8Tha80DZ9FzjlnE04G8mbBl9D344OtIRT6EOiLwXx8wHHQ5In+AYQfQVsNlkJfTFrqkjcPQqHN3LNnz05os8DpFLLdSRfXAAZ7hzHcK74/djCdMXwXtCfusHPW9FSizbBSiKW+LMt5QYnXqFHDm91iNomzZPvxiaoqNEkbQb68yWrzVd3tmzcv3rp88T0U0vLUqVMvMFs/ayn49De3tGzKcqwGzVLSLE37+Pi0srRsynKsVG1S0ixNs2K1sLRsKuVapkJLV9fCw2pq8cbUaBeODk0Gi1JK6PX6Lkz/LxcqVKgXm4Rm+J3D+JRVhV6X26gXMdxhLAntwavR0dGvs1y8if/aHp7S1jbUx9OzqE6vlxuSf2bNmlVx4MCB3YYOHVoY3/ZUeqBNZ9IrYy4fg7WZ19fX9w9z9aZH51bPZt6M9JcPmc39jYqKKmHtuDq6vMlgOcr4htluPtP/WsKlTP07oc0l/J5wAcvAGiBpWeKXEV9IuRmy5MPzl60Nhfc3ZCzDnXifOm26bbNVtpsvbQ2wT/FOu4Tzc00G62zRUTExp+KVfs7U4UN6W4sN8+Z0sZbHWD6DvJ2M9VgaOluvj7o8k8Gy/BdjaS/vzA7vXrO+mE6nVliLW9eufGYtj7F85PWrnxvj1oY3rlyeYS3PlJGDzO3EnanqR0aWyWB1Ol0ljph64p8OxFedRDgKI27q6J7WatxUDRj3rhr2/hTVc/gbauikKeqloSMcLdZdfxbVgMlg8SN3x8bGypdRLMaXnITxBrHZ+t6R/Yrx8gn7ft/X4xZ9+MG4Oe+NH7d6zufj5k4aP27tvFnjDMpgFtmfeOKTtPLTyvPPlevjtPLTysuZJ8+MtPJTy4tP8P7KkTq0vu6szWEyWOnGjRs3YplZK3FklY2N1gU2VPeg68RV4Mgr2VsBlPHkhCA7+Tb/TZo5M3L87AXTDpz+a90P5y8vkLgl6DXqrXmWlEutTAZ5LW6jUfakOXPSfPPXZuU5gZGTjX+cIMYqEckMtmjRon4cbxW4f//+S1y5iksQiAFXZbbNw83Vq7gKgxLp9TjWepNzuna4DfLEeQOrpKYojMyqzO59qOsNZNRJke1OZpIGONp0uW/HSWawcuuFO/AN534rOGb6nHPHfRjvb9AO4zLMJpTvwvqc2fcQ8U+gbSQuT5wfyIhOqWcbmEVdM6n3cEbqcvPaVQMF7FqbHSpLZrBym8WMWol6te/PCg4OjuTwWM+sV1VuvKArXIEcxHNIPKvh5/Dwfrg5+XBvrPpSj6zWz0e5vckMNjWXIF++fJW5piueLVu21zHc7g8ePOiaI0cOeRj5FdyDcllFOSfDw19OUIbA+Pv3m8TFxckTZVP4cPblAyhXzFmlG499O5MZbGouAbcdp1iu5dZrDsv1hh07diwnlC8S3ufn53clq2iwSt26az10Hp+2DQwMwvVYAybQr+VBQUH6rNKH9Nr5OOQnM1iWer9WrVo9ZRxEo0sgimA2KslSajopYMAvcC9/X3gSXYnKzFbaAzNS3hVRuU6dfYfDQgODFi2IAZfMwBC0eOHb6KFsQEDA89I3V+zL49qmZAbLJsufnX9Fduuvsdz3adeuXecCBQq8iLH2h/4EJwX9ifcFr0pedHR0T3ia4UqUYaefA3chAN434O1E6PBLB5sGzWCQD5346PLlH6lBKYPhSR8fnzy4QtULFy7cl/5MwHidegtoU9/szyTHmvavNQM1JjPYsLCwmyEhIduZPeXZ1hXEtxCX52G/wF04yRL6OVgOlkkersEyeELI+534EVyEzZSfieGGYsjHMtAuh7F66HT3/61cF6lUaoCq1B1cnx/oo1yiLOHEZArp39Rj9o/jzAhX63IygzU2jhk02fIPXcdy7ynLPxuvqrJcMoPmFzDTVpB8YDC6Evv27XsQzAkDNJf7e6p8xRvlKlfdV65ylePlKj87YcnmLeW+3Brc8qPFSwp0GzgoT7eBg3VdBw6e6nINz4QGcV1fKBPEpikyVYPlkyU/ptESwx2KUUrYgUPk0cyglcmTTjShVnkVJh/LZnHKvAzewHjbsXy69MlBvF5fnDW/sUCn8yjHSlASd6fWY770M5yp/mXoJjPVGjNITNVgWdZDWQI3s/TPI76HUA72p7M0yjKJFxC2BPoOlsxfOeL6mvhaMNPb2/sQ7oD8oksGm+UcdkOCUvTzB9yZecCFl37n6CMrSEnVYKXhsvzL0i9xI4w7Qj/ITQAAEABJREFUZuiFmU21L6JIdAMMUkbcgH24AxJ3VRQqU2ZVQoKhB77sCp0u4VtWEXF/Crpqe93tSq4BswbLUilvTtbDOOWSYAgD2yLJiUERvV5fFdpADPc1/NoAfFyXPtJK2m0PT89KCQZDH6XzaOLp6ZmN049AcWnoh/s5hqSKcsG4WYNl3b+JC7CCcBtLv/y+1Vcs+9qJAemj165dk1dlFslzBxjvEWbaaBfsX7pNwiWQV3QW0Tf3cwzpaivzC5g12PSadvTo0Tgpg6HqGWz5FUNJZgnEent/oJS+sWecflqWaHDmNfJq5olOXXK6BsuyLz5eTpZ8OdbKERgYmFvi4s+yhJoeikmsXjv+Soy7bFCzZs242Hh1Os7La+Lu7ZufSzzZ0Llsg90NM2kgXYPV6XT58PFGRkVFNWD5H8CxVl1uuDpwDNQvLi6uXLZs2V7E/xvGTdDL+LOj7969+7ypdleO6PVxOoMh7tz5877c0sk3DMq3mryV9PrZGc13cRmu/XhhasoTf5VjrSn4s/sIP9u2bduunTt3bgUL8W/lediVuARz8QXl9fBPiR9JrR5Xo9Vs0uR6rK/vm4OGjZJnfXfST3kYZjq3dlG2tvVkeHjlkwcPtjHC1nrcfOY1kGyGlaOs9u3bJ/uWF04JTEdYxmqYhQpCL2tMN2/e/AlxE4zprBKKa2DfthpmKg/dLiNOHDo0gtWnWMuWLYtHRESY+w4x+zbhEa8tmcFmz549G0t+yYIFC8qrKm0x3mEslyU5BSiNL9sF5Y8DbSjzLMdBDfD9+uAKvMgNWFMuDOTL3R5xdVnfPfRXlQuVNpMnTx6Ovgair8fxIRrrFWeGI5nBsizeAttZ+qez5MvSP1eWeI6w9kOTB1s+5Brzh0uXLh0gLd/WsgJXYCNltxI+dg+HPKxT3QalU58Z4enl9d0LpUufAl/16dIlqF7ZsntqlSwZM3nYsNLW4EBoaHFryict+/3evTbzPty/zKeYDJZPfzlZuoxNSho/mniEJXkY5vWkaaG58a8GqtStu7hKnXpvGrF97YrXPD0Szgp++ParbyW0Bb8cOXjAFj7hOfXD4f0S2oIEvd7l3BiTwbJ01WHpep0lfzq7/XeZSScSH4shl/p3ONz/W6eBf0t3fu111WPIcPXa2HdU71Fj1PAPPlRtX+r5b6aL/++h17vuOSxL/HLcgYm4AG8RTib9OvFPOB045+J6ddnm4ev/vHXZkv+tnz9HLf1kmlo1c0bI3PfGhYSuXxOi0ymL4ePr+4015ZOWtYY3iSITiO82eHvKw+5EXefPNMNKk4ynBBUrVvSRXb+kOQ14klB7S5YZ15fZt4aEUr5GjRrebCIs+gUYKf+4YfzsBV+8M2t+pXGz5+u6DB1ZIfzsP2M2Hfy+E7T21qDfuImvWVM+admeo8f2S5pOKy7tTIQnYRudztPb1cYsmcFyCSCvjuQpVarUoHv37vXOkSOHPPNaW04BMNJxNL4lJwbC04YThEGcJnTi8kB+Xqcb+b1BI3xfl3uGknZn+t+FCxf80V05Llwe51duMjwOYnymSnAB7rDjlwuC2bgE8h2w+6CF4hbIazMfEt9B/AfCYMotpMxG0l/jQsibqCuhf7dnzx6Xew/I1MFMjHDmewd9bUNv7uduMzAOyQyWpV/emjW5ALLkM2vm6tSpU16J4yZkM7oLGZD52LL+HB5eVy5dgPuLPGy0gmQGmz9/fh2nBbVxBVpjqN2LFi3anwuCslwK1CpSpEhP3ITAsmXLvnj//v2XuEjoSxmX++4lG/VgFZsthS/9cfqVBGV4p0m9es1xo9xf5GGLEuFJZrBBQUHRLOuhLFubCDdwry5fFX/s6tWre/FjN7CkrYO2GhdgNfHllImhDvefBRrIX7L0emVQy0e9/bZ8iYdAnl1Yjs5d9os88uTJ47rHWqJzcy5BiRIlcp09ezY+pUvALFtIXAXhdSNtDXDGHc/sUGrfrpDf9m7fZghevz7spwMHgk6Gh29MD5dOn56XXhlz+df//ttK3kOGn8MPRZ0IP7hZHxcXn3avnJ+LDv9fqDUuAcdbAxISEpoUKlRI3qoVF0GeNaj3/7W5Yyk1YNCpBpciIsqdu3BBxTyIbrnv0KGuP5443i0mNqabUgaz0Ovj26WVn1aeIUHfNq38h/OgKJVDp3Sd9QaD9t5eyn5kZjqZwbI8WewShISELN69e/c6f3//3RyQ78VFkGcNDmVmZ7KC7Erly6ta1aqpCs88o5o1bKBqVq2qfH18XLLpMQ8euPY5rDmtybMDYsyp5UO36RUZX1/f28uXL29pC8LDwxvawic8Bw8ebCShLYC3gS18wiO8p/46t/L8lasDrcWt6AfvWMtjLH/zfvQ4Y9zasFLlymuk7elh3bp11VOzDUfQks2wjhBgrs5ff/01kouKOFtw5coVL1v4hOfatWueEqaObGm2JyIiwtsWPuG5fPmyp87L69a92Ngz1uL3P/+8ai2Psfzps2evGOPWhujKIj3rdLo4c+Nsb3qmGWxYWNjtVatWPVi5cmXM6tWrf+7evfu36WHNmjU/Ut5/8+bNt4hfWrJkybH0eIz5lP8ROX6sCBeXLVsWRz1/G/PSC4WX8j5bt269Smhxe6Ve+ngBHp8tW7ZcI7SKd8WKFbfgycnJzK+EVvEuXbr0Jjx5goODb9B+i3W1adOmQ8yokfD609/blvD26NHjF3sbprn6Ms1gOTo7Dw7jC4fLI4vmGpiUzsBFUT4Ef3kb8d/37t17O2l+WnHKRyEnlA/KXnzvg9Rj8e+oCi/lw8B2YHF7pT308Qw8YdJmQqt44TkOz3bqsEpPIpd+noB3C3VYpSs+0LEcV/4Er016FtmORDKDvXPnTt5//vnnSUfi0qVL/sYOsVnz4DKisCPlRUZGljlz5oxvEpnet27dKulImdevXy9K30zf7E3cz5HypO6oqKj8xj5KiPuSXeiOBHrMLbKcCZPB0sECN2/ePBAfH3+Dm5gL9kRsbOwF6r5Enf/ExMSMNBoQPlIVLiXCHSUThd4AP3Dp0RWj0QyID0xbaP91hEz6doEPyA0++EcwlLoykMj1vnDhwuvIO0f/7apXqc8okw/JoRs3bhRPlJkN+nhkRkgZe4MPx8W7d+/euH379mr6mldkOgsmg6VT9fR6fYWEBC4QDQZ5t8tuwFizMWi+dFS+/qgtBqTJ5Yq3OfJKAcXA2k2e1CUyMRqFQp+k/paiUOg6+tiCsAA0u8vkw5dNZGIsxai/hcj8448/PDCcNqRzIteufZT6jDK5Pn+a1aqZyGQi8EReIPCWMvYE+pOx9Lt8+bKi/naMaTmR6SxohuNoYVzxqTJlyqgcObTHak3iPD09daaEnSNJZaJkT2P1DJ7DXvvg4kWVLl1a+fx7rqrN6CKXXbQEDkEKmQ6RkbRSDw8PVbJkSVWsWLGkZKfFHzJYPqmKT42STxBugpIZg6VGS7MMKD69iplRsbRqIcuCunjxomKZVcyiik+8lidpqQdjUTJgiYP4UMckn1lQMSMqkSf1SyhgplLSHqmLJU+TI+Uk/ddffylp10MVJhLSkyntl/YxK2n9kFDqFfnSHwk5PtPalJacRHFaIINprp+sYOr8+fNaH6QvIkv6KBC9ST9Fl6ILSUsZ3AtNp5JmNtNkpPwvLZmiP6lTxkv6KmMpaYHIERkyzpInMs6dO6dYDVKKeCjt5eWlmGweojuD8JDBSicE0iEZNGmcDJgYQHR0tGaMogAZAClnHNyzZ89qhimdx2fVDBBfNV0FiIJEkaIwI598MGQgxTilHX///bcmV+IiR+TmzZtXSdtsUZLIlPb/+eefmkGKbGm3yJH+SH/lAyHtyZUrl81ykrZNZEq7BfJBEEMx9lMMUwxW9I0LoX3opR0CWZWkn2KYSeuzJC71nj59Wpt0pD/CI+NolCP9lLZInsjgMscufRU5jsJDBitTvSxr5cqVU5UrV1aFCxdWz3CNWKhQISXLT1WuEvPly6ctCyVKlFAVK1ZU1bhqrFGjhipatKh66qmnVKlSpbTwueeeU6KEtBov+c8++6yqUqWKkvpEbtmyZbU6RXaBAgW0uORXqFBB1axZUz399NNKDOmJJ55Iq2qzeSJTljVpt7TX2D9JC0RWrVq1VPHixRVXz8pWOUkbwOWBEn2I/qS/ojdjPytVqqRy586tJC1lBMZyQhfdJ63L0njBggXV888/r0Sn0ifpj+jNKEfoxv6KDNG3pXVnVjmPlIJlZuMMTh07dkxxJqe4kVKSluUsZVl7pWUm/u677xTXl+p///uf+uWXX8Sht1f1qdZz8uRJtWfPHnXo0CGnyZQV48CBA4qzUbV//34Nol/pf6qNtANRdCkryfHjx9Xhw4fVt99+q42pI2Xaodlmq3jIYLNnz64VlqWDDYq2PMmn77ffflMcKKtt27Ypbm20jsuyqhXOwH9ShyxbsiTLLCRLpfhrsoRmoNp0WWWpFTky4zhDpvjqYiSytIteRb/SBnFHpLGSL6E9IS6B7CnElxVXSnScM2dOzS8WOY6QKfU6Eg8ZrGwGZOMgPs2TTz6pOdcyoDKwsjwLxKjFjxUfKKONEznij0o9IkPiUq8oWmjpw/oS8iGR9ovBypLrDJniD4uBit8qro+kRba4WWK0onfre5I2h3zoOULUNq5yaiJp0bEjZabdooznPmSwoswWLVpo/mvz5s1V/fr1Vfv27dULL7ygxE+tU6eOatWqlWrXrp2SmTejTZCZRuoWGeKbVq9eXTVp0sShxybe3t5K/Ma2bdtqfqozZMrqIb6r6E72Bs2aNdOO+sSHlP7KviCjukzJL3XWrVtX851FhvRX/HVHykzZBnunTQbLUuWUVzUwUPmSBq0fzHBOecqHIxiTHPrplNd6kJlUjqnPWscd9B+6Nb0hQNzgIDGZWq3JYPFtDrE8b2BA74NTjgIylnMSoSmWQd2EnAPAYfKo+wSDtw4tJxAacHfWI/codIfJpP7DnCxsQKbs/OORtQrar4QOkUm/Ylk1tuJihIlMlvw4ZH2BzD8IHSXzNnUv5RTllMh0FkwGi29zA3dgAP5pQVDbUWAjsAYFazMehnuBpbKro2RJvfiNbY8cOfI1MrUZBx/8CPQA4LA+shR3Qp+/yyAiV89x0mYGtpajZNLHvMjrx6Sj/dYEMmOQOR+Z1R0osxj1j8Q3jpR+Ogsmg23dunXbNm3a1O/du3fD3g7Em2++2VxkGdG3b9+ajpTXq1evakuXLm1llEcf20Cr7kiZXbt2rWGUJyEyWzpSntTdo0ePOiLLCGQ2E7qjgRztOQ2nGixCpzC9h7ga3O3xcPkxYTYPw37ecKrBIrS8swS65Tx6GsB+nPbt6yaXIKUaBwwYoDp37qxmzJihxo8fr1i61YIFC9SECRPUK6+8ouTqUMLZs2erqVOnqpEjRyojj8QnT56s0T7++GM1ceJEFRgYqCGlnKySNpkac64AAAdiSURBVPYXl0brl/Rv2rRpSvov/RXYqy+iT8H06dM1fUvdffv21cZAdCk6lbHoC03aZS+5Urf0R8a4adOmSvr4/vvva214++231bvvvpvpY2jWYBcvXqzdaI0ZM0YzyOXLl6vBgwerKVOmqNWrV6sTJ05o4YgRIzSDnjVrljLySFw6J6F09IMPPlDBwcEa7KVcZ9dj7O+nn36qpF/Sv3feeUdJ/yUtsFebZIIQvPXWW5q+pW7Rv0B0KTqVsZC0tMtecqVu6Y+M8TfffKMZ6Hvvvae1QT4kYsDBjKO95NlST6oGyxS/wg2dWwc68zqwxdjswaMZ7K5du7oCnREhISF93XDrIC0bMNpKYjjUHsZoSR2awaZWkGu8Qh07diyOX+ot36klIbvBXMRzBAQElE+Nx3Lao1dy0qRJ5fH/TC87OrKH+LbZWb5rg8qOlCP9QUbtzz777Elcg/oSp5+5HCkzvbrNGiw3J5W4Om1z5cqV12JiYrpEREQM5JaoJfG+Op1uYYcOHZz6Lk96HcnsfHRS/e7duzmc0Y579+7pGZvCBoOhqSPlSX+QUzs6OroUR4w1kCVj3pUw0/7MGuy2bdv27tixYzHhou3bt68Gc4lv8vX1XcyV34uktZucTGu5iwlmBlo3bty4G85oFrPcAxCMzFmOlCf9Qc5sNoDHRBanCCtJL3WkzPTqNmuw5hiDgoJit27d6nLfG2quvW76o6UBqw320eq+uzdZTQNug81qI/aYt9eswXLLVaZTp05VQYF27drlady4sZ+cGkg6LZ09rnn4dk47JRAdy0kBMmux8XLYdzsYTwkIc3FCUAPURqZrnhLExsbmRhmlUU4jdogd8+bNK1+DM51d41SOt5xyfIPsLPPnzFMCUQonBfLK8AsfffRRbkk7Ajdv3tQx3oWjoqLKYgsvgGeQ45qnBDt37jzGNVwwG6wgTguWb968+QzHWnK0NSo0NDTp0/T0wf3HLtpppwSibWa6S2A218O3JO0IUL92GpF4SjCPPq6ClnVOCTghuA3uOkI57jrdGrBEA2Z9WEuY3WXcGnC2BswaLJuuwqBMygYJTWCkc1WbDYg/pZGI+7A5kytDh20GNEEu9B+bEl+Wy/osl/7OaJZsuNgANQK18SsdpucPP/yw/JQpU+rTP9ffdOFsF4yPj6/EFWw3MCkwMLAxhtgcWjE2YYWgjQ0ICHiRzVk3aI2Jd4TWOS4uLpANyJecJjw2P4HE5sQXnRTGx8/mDINlw6XHUJ9hjMo5atNFvU8wtq31ev3TWWLTxYbrONewIVzBbgKTIiMjj2CIPxLfv2nTpnDCT9iMbeS6diUbs21+fn57uLL9BT55E7YjtEPOGDxXkMHMeocZNkiuMp3RHuQ9QN4SwpWO2nT95z//uU39M5GzLMtsuthgyXcVaG+b7tu37wHGGGluQCgbjZGeJj9hy5Ytlwk1PkL3n1sDdtOAWR/WbhLcFbk1YEcNuA3Wjsp0V+V4DZg1WDkJEBibwO4/mzzELWk2WPnYgBUnNO2KJb9Xr17ZoT9WJwSiD3bRvrJjl1DSjoacEkydOrUZMuuw+XLoKcH777/fROThzz4HaoHMv5pNTcHs/EuyC+0QGBjYC8PsKA9uX7lyZSxG3BAl+ZNXhp1xICcDPTkR6PzgwYNe7CbbsTF7rE4IjLpDH3nlgWdj2pEhpwS+7N4LIrM0BuWQkwk5JeDER8bzaS8vr1yM9QuMrVzPu+bVLKcA37LJmglWcRogP062gBOBqWyo9nNtex7ad6TXUm4Nm60tpBdTNoiOPVYnBGKYI0aMiGHm2eXEU4KbEydOXItMwX1pg70hpwScEHyKnMWjRo26TDif9GZkZp2rWQuUYsCgL1POfUKAEtx/9teAWR/W/qLcNbo1kHENmDVYfNXC3bt3fwYftWBKMWysiuO3FkhJf5zTLJWP7POwWeKtWRz6Ijj38rZkUzZdL7H5Ggy6gGoYpvu5WJSQ9I8NidPemhW5jI1c6hRx1KZLZLCJzo0dPM0GvAR7E2e8NSti04TZGZYN1FE2V3sI17GhWke4AGwGx7kzdz8Xm0KtbEic/Tys9qwqM7tDNl3SPa5kr1D/6rFjxx6nf7PYeK0knfU2XVzDup+LlRF1w+ka0GbY8+fPT3DDrYOM2ICzLFczWPyvamCyGzq3DnTW6wD/trBTDdZZwtxy3BrIqAa0GTa1SiIiIrSf7zx+/LiSX/ATcLyhjh49qriG1VjkR43lFxIlwbWtBFpZ+VlK4Ttw4IBav369Rn9U/4uMjFTyK9g//fSTU7ooskTXMh6Olvnf//5XiYwff/zR1EdJ29RROzEZDTYiZX3yo3HyI73VqlXTfoxYfvRt9OjR2o/L+fn5acWLFy+uypcvr8Xlh3glIuUaNmyoqsHXoEED1aNHDyE/ssidO7cqVaqUkh+nU074J7JE16JnR8uUH4gWGfKD1CJX4oKU3TQYDNqv16SkOyKtGSyGN4zztlFuJLh1kGCdDjDWodjPJEcYZ2p1/h8AAAD///d6DuYAAAAGSURBVAMAG3xW5VAQxuEAAAAASUVORK5CYII=",
      "name": "Performance Analyzer Export Analysis - Single Visual",
      "description": "Analyzing a single Power BI visual at-a-time, this visual presents Performance Analyzer data exported from Power BI report pages linked to Power BI Project data (PBIR format)",
      "author": "Greg Philps"
    },
    "deneb": {
      "build": "1.9.0",
      "metaVersion": 1,
      "provider": "vegaLite",
      "providerVersion": "6.4.1"
    },
    "interactivity": {
      "tooltip": true,
      "contextMenu": true,
      "selection": false,
      "selectionMode": "simple",
      "highlight": false,
      "dataPointLimit": 50
    },
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  // visual title\r\n  \"title\": {\r\n    \"font\": \"Segoe UI\",\r\n    \"fontSize\": 24,\r\n    \"fontWeight\": \"bold\",\r\n    \"fontStyle\": \"italic\",\r\n    \"color\": \"#4A4A4A\",\r\n    \"subtitleFont\": \"Segoe UI\",\r\n    \"subtitleFontSize\": 16,\r\n    \"subtitleFontWeight\": \"normal\",\r\n    \"subtitleFontStyle\": \"italic\",\r\n    \"subtitleColor\": \"#969696\"\r\n  },\r\n  // legend\r\n  \"legend\": {\r\n    \"title\": null,\r\n    \"font\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelFontWeight\": \"normal\",\r\n    \"labelFontStyle\": \"italic\",\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  // facet header\r\n  \"header\": {\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 18,\r\n    \"labelFontWeight\": \"bold\",\r\n    \"labelFontStyle\": \"italic\",\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  \"axisX\": {\r\n    \"title\": false,\r\n    \"ticks\": true,\r\n    \"tickCount\": 10,\r\n    \"domain\": true,\r\n    \"domainWidth\": 2,\r\n    \"domainColor\": \"#A3A3A3\",\r\n    \"offset\": 4,\r\n    \"grid\": true,\r\n    \"gridColor\": \"#EEEEEE\",\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 10,\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  \"axisY\": {\r\n    \"title\": false,\r\n    \"ticks\": false,\r\n    \"domain\": true,\r\n    \"domainWidth\": 2,\r\n    \"domainColor\": \"#A3A3A3\",\r\n    \"offset\": 4,\r\n    // \"grid\": false,\r\n    // \"labels\": false,\r\n    \"labelPadding\": 4,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  \"style\": {\r\n    \"_non_zero_duration_bar_style\": {\r\n      \"cornerRadiusEnd\": 4\r\n    },\r\n    \"_zero_duration_point_style\": {\r\n      \"filled\": true,\r\n      \"size\": 200\r\n    },\r\n    \"_max_duration_rule_style\": {\r\n      \"strokeDash\": [\r\n        3,\r\n        3\r\n      ],\r\n      \"color\": \"#7D7D7D\"\r\n    },\r\n    \"_card_bar_style\": {\r\n      \"cornerRadius\": 8,\r\n      \"color\": \"#DDDDDD\",\r\n      \"stroke\": \"#EEEEEE\"\r\n    },\r\n    \"_card_title_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 14,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"normal\",\r\n      \"color\": \"#4A4A4A\"\r\n    },\r\n    \"_card_value_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 24,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"normal\",\r\n      \"color\": \"#707070\"\r\n    },\r\n    \"_info_bar_style\": {\r\n      \"cornerRadius\": 10,\r\n      \"color\": \"transparent\"\r\n    },\r\n    \"_info_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 16,\r\n      \"color\": \"#AAAAAA\"\r\n    }\r\n  }\r\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "pageId",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__1__",
        "name": "visualId",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__2__",
        "name": "visualName",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__3__",
        "name": "visualType",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__4__",
        "name": "events_id",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__5__",
        "name": "events_name",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__6__",
        "name": "events_start",
        "description": "",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__7__",
        "name": "events_end",
        "description": "",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__8__",
        "name": "events_parentId",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__9__",
        "name": "Duration",
        "description": "",
        "kind": "measure",
        "type": "numeric"
      },
      {
        "key": "__10__",
        "name": "Hierarchy Level",
        "description": "",
        "kind": "measure",
        "type": "numeric"
      }
    ]
  },
  // text and position only; formatting done in "config\title"
  "title": {
    "anchor": "start",
    "align": "left",
    "offset": 20,
    "text": "Performance Analyzer Export Analysis",
    "subtitle": {
      "expr": "['Analysis of event duration and decomposition | Single Visual', data('data_0')[0]['_visual_title']]"
    }
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "transform": [
    // remove [User Action] events
    {
      "filter": "datum['__5__'] != 'User Action'"
    },
    // use an internal development ID for easy dataset identification
    {
      "calculate": "1",
      "as": "_DEV_ID"
    },
    // assign internal names to dataset fields
    {
      "calculate": "datum['__0__']",
      "as": "_page_id"
    },
    {
      "calculate": "datum['__1__']",
      "as": "_visual_id"
    },
    {
      "calculate": "datum['__2__']",
      "as": "_visual_title"
    },
    {
      "calculate": "datum['__3__']",
      "as": "_visual_type"
    },
    {
      "calculate": "datum['__4__']",
      "as": "_event_id"
    },
    {
      "calculate": "datum['__5__']",
      "as": "_event_name"
    },
    {
      "calculate": "datum['__6__']",
      "as": "_event_start"
    },
    {
      "calculate": "datum['__7__']",
      "as": "_event_end"
    },
    {
      "calculate": "datum['__8__']",
      "as": "_event_parent_id"
    },
    {
      "calculate": "round( datum['__9__'] )",
      "as": "_event_duration"
    },
    {
      "calculate": "datum['__10__']",
      "as": "_hierarchy_level"
    },
    // further development needed: this is a "quick-and-dirty" "hard-coded" sorting method and will not sort properly if additional event names are present in the dataset 
    {
      "calculate": "indexof( ['Visual Container Lifecycle', 'Resolve Parameters', 'Query', 'Query Generation', 'Query Pending', 'Execute Semantic Query', 'Execute DAX Query', 'Execute Query', 'Serialize Rowset', 'Parse Query Result', 'Render', 'Data View Transform', 'Visual Update', 'Visual Update Async'], datum['_event_name'] )",
      "as": "_event_order"
    },
    // adjust Power BI theme colours as desired
    {
      "calculate": "datum['_event_name'] == 'Visual Container Lifecycle' ? _event_colour_1 : datum['_event_name'] == 'Query' ? _event_colour_2 : datum['_event_name'] == 'Render' ? _event_colour_2 : datum['_event_name'] == 'Execute Semantic Query' ? _event_colour_3 : pbiColor(7)",
      "as": "_event_colour"
    },
    {
      "joinaggregate": [
        {
          "op": "min",
          "field": "_event_start",
          "as": "_min_event_start"
        }
      ],
      "groupby": [
        "_visual_id"
      ]
    },
    {
      "calculate": "round( datum['_event_start'] - datum['_min_event_start'] )",
      "as": "_event_start_zero"
    },
    {
      "calculate": "round( datum['_event_end'] - datum['_min_event_start'] )",
      "as": "_event_end_zero"
    },
    {
      "extent": "_event_end_zero",
      "param": "_event_end_zero_extent_array"
    }
  ],
  "params": [
    {
      "name": "_max_event_duration",
      "expr": "_event_end_zero_extent_array[1]"
    },
    {
      // visual container lifecycle
      "name": "_event_colour_1",
      "value": "#E3E3E3"
    },
    // query, render
    {
      "name": "_event_colour_2",
      "expr": "pbiColor(3)"
    },
    {
      // execution task
      "name": "_event_colour_3",
      "expr": "pbiColor(5)"
    },
    {
      // 0ms event
      "name": "_event_colour_4",
      "expr": "pbiColor(7)"
    }
  ],
  "spacing": 10,
  "vconcat": [
    {
      "name": "LEGEND",
      "data": {
        "values": [
          {
            "_legend_id": 1,
            "_legend_size": 1,
            "_legend_label": "Parent Phase"
          },
          {
            "_legend_id": 2,
            "_legend_size": 1,
            "_legend_label": "Execution Task"
          },
          {
            "_legend_id": 3,
            "_legend_size": 1,
            "_legend_label": "Container Lifecycle"
          },
          {
            "_legend_id": 4,
            "_legend_size": 1,
            "_legend_label": "0ms Event"
          }
        ]
      },
      "hconcat": [
        {
          "name": "LEGEND_LEFT",
          "width": 370,
          "height": 20,
          "transform": [
            {
              "filter": "datum['_legend_id'] <= 3"
            }
          ],
          "mark": {
            "type": "arc",
            "radius": 0
          },
          "encoding": {
            "theta": {
              "field": "_legend_size",
              "type": "quantitative"
            },
            "color": {
              "field": "_legend_label",
              "type": "nominal",
              "scale": {
                "domain": [
                  "Parent Phase",
                  "Execution Task",
                  "Container Lifecycle"
                ],
                "range": [
                  {
                    "expr": "_event_colour_2"
                  },
                  {
                    "expr": "_event_colour_3"
                  },
                  {
                    "expr": "_event_colour_1"
                  }
                ]
              },
              "legend": {
                "orient": "none", // none, top-left, top-right
                "direction": "horizontal",
                "legendX": -200,
                "offset": 0,
                "symbolType": "square"
              }
            }
          }
        },
        {
          "name": "LEGEND_RIGHT",
          "width": 370,
          "height": 20,
          "transform": [
            {
              "filter": "datum['_legend_id'] > 3"
            }
          ],
          "mark": {
            "type": "arc",
            "radius": 0
          },
          "encoding": {
            "theta": {
              "field": "_legend_size",
              "type": "quantitative"
            },
            "color": {
              "field": "_legend_label",
              "type": "nominal",
              "scale": {
                "domain": [
                  "0ms Event"
                ],
                "range": [
                  {
                    "expr": "_event_colour_4"
                  }
                ]
              },
              "legend": {
                "orient": "none", // none, top-left, top-right
                "direction": "horizontal",
                "legendX": 340,
                "offset": 0,
                "symbolType": "diamond"
              }
            }
          }
        }
      ],
      "resolve": {
        "scale": {
          "color": "independent"
        }
      }
    },
    {
      "name": "TIMELINE",
      "transform": [
        // use an internal development ID for easy dataset identification
        {
          "calculate": "2",
          "as": "_DEV_ID"
        },
        {
          "calculate": "pad( datum['_hierarchy_level'], 2, '0', 'left' ) + '-' + datum['_event_name']",
          "as": "_event_level_event_name_label"
        },
        {
          "calculate": "_max_event_duration",
          "as": "_max_event_duration_x"
        }
      ],
      "encoding": {
        "y": {
          "field": "_event_level_event_name_label",
          "type": "nominal",
          "axis": {
            "title": null,
            "labelAlign": "left",
            "labelPadding": {
              "expr": "200 - 10 * ( toNumber( slice( datum.value, 0, 2 ) ) - 1 )"
            },
            "labelExpr": "slice( datum.value, 3, 100 ) == 'Visual Container Lifecycle' ? upper( slice( datum.value, 3, 100 ) ) : slice( datum.value, 3, 100 )",
            "labelFontWeight": {
              "expr": "indexof( ['Visual Container Lifecycle', 'Query', 'Render'], slice( datum.value, 3, 100 ) ) > -1 ? 'bold' : 'normal'"
            }
          },
          "sort": {
            "field": "_event_order",
            "order": "ascending"
          }
        },
        "x": {
          "type": "quantitative",
          "axis": {
            "title": null,
            "orient": "top",
            "labelExpr": "datum.value + 'ms'"
          },
          "scale": {
            "domainMax": {
              // set X axis scale to 10% above maximum
              "expr": "_max_event_duration + ( _max_event_duration / 10 )"
            }
          }
        }
      },
      "layer": [
        {
          "name": "NON_ZER0_DURATION_EVENTS_BAR",
          "width": 780,
          "height": 300,
          "transform": [
            // use an internal development ID for easy dataset identification
            {
              "calculate": "3",
              "as": "_DEV_ID"
            },
            {
              "filter": "datum['_event_duration'] > 0"
            }
          ],
          "mark": {
            "type": "bar",
            "style": "_non_zero_duration_bar_style"
          },
          "encoding": {
            "x": {
              "field": "_event_start_zero",
              "axis": {
                "labels": false
              }
            },
            "x2": {
              "field": "_event_end_zero"
            },
            "color": {
              "field": "_event_colour",
              "type": "nominal",
              "scale": null
            }
          }
        },
        {
          "name": "ZER0_DURATION_EVENTS_DIAMOND",
          "width": 780,
          "height": 300,
          "transform": [
            // use an internal development ID for easy dataset identification
            {
              "calculate": "4",
              "as": "_DEV_ID"
            },
            {
              "filter": "datum['_event_duration'] == 0"
            }
          ],
          "mark": {
            "type": "point",
            "shape": "diamond",
            "style": "_zero_duration_point_style"
          },
          "encoding": {
            "x": {
              "field": "_event_start_zero",
              "type": "quantitative",
              "axis": {
                "title": null,
                "orient": "bottom",
                "labelExpr": "datum.value + 'ms'"
              },
              "scale": {
                "domainMax": {
                  // set X axis scale to 10% above maximum
                  "expr": "_max_event_duration + ( _max_event_duration / 10 )"
                }
              }
            },
            "color": {
              "field": "_event_colour",
              "type": "nominal",
              "scale": null
            }
          }
        },
        {
          "name": "MAX_DURATION",
          "mark": {
            "type": "rule",
            "style": "_max_duration_rule_style"
          },
          "encoding": {
            "x": {
              "field": "_max_event_duration_x",
              "type": "quantitative"
            },
            // turn off the Y axis
            "y": null
          }
        },
        {
          "name": "DURATION_LABELS",
          "transform": [
            // use an internal development ID for easy dataset identification
            {
              "calculate": "5",
              "as": "_DEV_ID"
            },
            {
              "calculate": "datum['_event_duration'] == 0 ? datum['_event_end_zero'] + if( datum['_event_end_zero'] <= 40, 1, 2) : datum['_event_name'] == 'Visual Container Lifecycle' ? datum['_event_end_zero'] : datum['_event_name'] == 'Query' ? datum['_event_start_zero'] : datum['_event_name'] == 'Render' ? datum['_event_start_zero'] : datum['_event_duration'] < 50 ? datum['_event_end_zero'] : datum['_event_start_zero']",
              "as": "_event_duration_label_x"
            },
            {
              "calculate": "datum['_event_end_zero'] - datum['_event_start_zero']",
              "as": "_event_duration"
            }
          ],
          "mark": {
            "type": "text",
            "align": "left",
            // adjust offsets as desired
            "xOffset": 4,
            "yOffset": 1,
            "fontWeight": {
              "expr": "indexof( ['Visual Container Lifecycle', 'Query', 'Render'], datum['_event_name'] ) > -1 ? 'bold' : 'normal'"
            },
            "color": {
              "expr": "indexof( ['Query', 'Render'], datum['_event_name'] ) > -1 ? 'white' : '#4A4A4A'"
            },
            "style": "_duration_text_style"
          },
          "encoding": {
            "text": {
              "field": "_event_duration",
              "type": "quantitative",
              "formatType": "pbiFormat",
              "format": "#,0ms"
            },
            "x": {
              "field": "_event_duration_label_x",
              "type": "quantitative",
              "axis": {
                "labels": false
              }
            }
          }
        }
      ]
    },
    {
      "name": "KPI_CARDS",
      "width": 860,
      "height": 80,
      "transform": [
        // use an internal development ID for easy dataset identification
        {
          "calculate": "6",
          "as": "_DEV_ID"
        },
        // calculate KPI values
        {
          "calculate": "datum['_event_name'] == 'Visual Container Lifecycle' ? ( datum['_event_end_zero'] - datum['_event_start_zero'] ): null",
          "as": "_lifecycle_duration"
        },
        {
          "calculate": "datum['_event_name'] == 'Execute Semantic Query' ? datum['_event_duration'] : null",
          "as": "_semantic_duration"
        },
        {
          "calculate": "datum['_event_name'] == 'Execute DAX Query' ? datum['_event_duration'] : null",
          "as": "_dax_duration"
        },
        {
          "calculate": "datum['_event_name'] == 'Render' ? datum['_event_duration'] : null",
          "as": "_render_duration"
        },
        {
          "joinaggregate": [
            {
              "op": "max",
              "field": "_lifecycle_duration",
              "as": "_lifecycle_duration"
            },
            {
              "op": "max",
              "field": "_semantic_duration",
              "as": "_semantic_duration"
            },
            {
              "op": "max",
              "field": "_dax_duration",
              "as": "_dax_duration"
            },
            {
              "op": "max",
              "field": "_render_duration",
              "as": "_render_duration"
            }
          ]
        },
        // rank to generate sequential numbers that can be used by subsequent filter
        {
          "window": [
            {
              "op": "rank",
              "field": "_event_duration",
              "as": "_rank"
            }
          ]
        },
        {
          "calculate": "datum['_rank'] - 1",
          "as": "_rank"
        },
        {
          "calculate": "['Lifecycle Duration', 'Model Impact', 'DAX Impact', 'Render Impact', 'Wait Impact'][datum['_rank']]",
          "as": "_card_title"
        },
        {
          "calculate": "upper( datum['_card_title'] )",
          "as": "_upper_card_title"
        },
        {
          "calculate": "[10, 210, 410, 610, 810][datum['_rank']]",
          "as": "_card_left_x"
        },
        {
          "calculate": "datum['_card_left_x'] + 10",
          "as": "_card_label_x"
        },
        {
          "calculate": "50",
          "as": "_card_label_y"
        },
        {
          "calculate": "datum['_card_left_x'] + 180",
          "as": "_card_right_x"
        },
        {
          "calculate": "0",
          "as": "_card_bottom_y"
        },
        {
          "calculate": "100",
          "as": "_card_top_y"
        },
        {
          "joinaggregate": [
            {
              "op": "count",
              "field": "_DEV_ID",
              "as": "_total_events"
            }
          ]
        },
        {
          "calculate": "datum['_card_title'] == 'Lifecycle Duration' ? datum['_lifecycle_duration'] + 'ms' : datum['_card_title'] == 'Model Impact' ? if( ( datum['_semantic_duration'] - datum['_dax_duration'] ) / datum['_lifecycle_duration'] < 0.01, '<1%', pbiFormat( ( datum['_semantic_duration'] - datum['_dax_duration'] ) / datum['_lifecycle_duration'], '#.%' ) ) : datum['_card_title'] == 'DAX Impact' ? if( datum['_dax_duration'] / datum['_lifecycle_duration'] < 0.01, '<1%', pbiFormat( datum['_dax_duration'] / datum['_lifecycle_duration'], '#.%' ) ) : datum['_card_title'] == 'Render Impact' ? pbiFormat( datum['_render_duration'] / datum['_lifecycle_duration'], '#.%' ) : datum['_card_title'] == 'Wait Impact' ? pbiFormat( (  datum['_lifecycle_duration'] - datum['_semantic_duration'] - datum['_render_duration'] ) / datum['_lifecycle_duration'], '#.%' ) : 99",
          "as": "_card_value"
        },
        {
          "calculate": "datum['_card_title'] == 'Lifecycle Duration' ? '[Visual Container Lifecycle]' : datum['_card_title'] == 'Model Impact' ? '( [Execute Semantic Query] − [Execute DAX Query] ) / Lifecycle Duration' : datum['_card_title'] == 'DAX Impact' ? '[Execute DAX Query] / Lifecycle Duration' : datum['_card_title'] == 'Render Impact' ? '[Render] / Lifecycle Duration' : datum['_card_title'] == 'Wait Impact' ? '(Lifecycle Duration – Model Impact Duration – DAX Impact Duration – Render Impact Duration) / Lifecycle Duration' : 99",
          "as": "_card_formula"
        },
        {
          "filter": "datum['_rank'] <= 4"
        }
      ],
      "encoding": {
        "x": {
          "type": "quantitative",
          "axis": null,
          "scale": {
            "range": [
              -200,
              780
            ]
          }
        },
        "y": {
          "type": "quantitative",
          "axis": null,
          "scale": {
            "domain": [
              0,
              100
            ]
          }
        }
      },
      "layer": [
        {
          "name": "RECTANGLES",
          "mark": {
            "type": "bar",
            "style": "_card_bar_style"
          },
          "encoding": {
            "x": {
              "field": "_card_left_x"
            },
            "x2": {
              "field": "_card_right_x"
            },
            "y": {
              "field": "_card_bottom_y"
            },
            "y2": {
              "field": "_card_top_y"
            }
          }
        },
        {
          "name": "TITLES",
          "mark": {
            "type": "text",
            "align": "left",
            "baseline": "bottom",
            "yOffset": -2,
            "style": "_card_title_text_style"
          },
          "encoding": {
            "text": {
              "field": "_upper_card_title",
              "type": "nominal"
            },
            "x": {
              "field": "_card_label_x"
            },
            "y": {
              "field": "_card_label_y"
            }
          }
        },
        {
          "name": "VALUES",
          "mark": {
            "type": "text",
            "align": "left",
            "baseline": "top",
            "yOffset": 2,
            "style": "_card_value_text_style"
          },
          "encoding": {
            "text": {
              "field": "_card_value",
              "type": "nominal"
            },
            "x": {
              "field": "_card_label_x"
            },
            "y": {
              "field": "_card_label_y"
            }
          }
        },
        {
          "name": "INFO_BACKGROUND_RECTANGLES",
          "transform": [
            {
              "calculate": "datum['_card_right_x'] - 24",
              "as": "_info_left_x"
            },
            {
              "calculate": "datum['_card_right_x'] - 4",
              "as": "_info_right_x"
            },
            {
              "calculate": "datum['_card_top_y'] - 24",
              "as": "_info_bottom_y"
            },
            {
              "calculate": "datum['_card_top_y'] - 4",
              "as": "_info_top_y"
            }
          ],
          "mark": {
            "type": "bar",
            "style": "_info_bar_style"
          },
          "encoding": {
            "x": {
              "field": "_info_left_x"
            },
            "x2": {
              "field": "_info_right_x"
            },
            "y": {
              "field": "_info_bottom_y"
            },
            "y2": {
              "field": "_info_top_y"
            }
          }
        },
        {
          "name": "INFO_TEXT",
          "transform": [
            // use an internal development ID for easy dataset identification
            {
              "calculate": "7",
              "as": "_DEV_ID"
            },
            {
              "calculate": "datum['_card_right_x'] - 14",
              "as": "_info_x"
            },
            {
              "calculate": "datum['_card_top_y'] - 14",
              "as": "_info_y"
            }
          ],
          "mark": {
            "type": "text",
            "align": "center",
            "baseline": "middle",
            "tooltip": true,
            "style": "_info_text_style"
          },
          "encoding": {
            "text": {
              // unicode symbol for question mark in a diamond
              // future development - find unicode symbol for information mark in a circle
              "value": "\uD83D"
            },
            "x": {
              "field": "_info_x"
            },
            "y": {
              "field": "_info_y"
            },
            "tooltip": [
              {
                "field": "_card_formula",
                "title": "Formula: "
              }
            ]
          }
        }
      ]
    },
    {
      "name": "TABLE",
      "width": 960,
      "height": 260,
      "transform": [
        // *** DEV: dataset = data_14
        // use an internal development ID for easy dataset identification
        {
          "calculate": "8",
          "as": "_DEV_ID"
        },
        {
          "calculate": "'01'",
          "as": "_extra"
        },
        {
          "flatten": [
            "_extra"
          ]
        },
        {
          "joinaggregate": [
            {
              "op": "max",
              "field": "__row__",
              "as": "_max_row"
            }
          ]
        },
        // to add only 1 row, select all for "_extra" = 0 and only a single row for "_extra" = 1
        {
          "filter": "datum['_extra'] == 0 || datum['__row__'] == datum['_max_row'] && datum['_extra'] == 1"
        },
        {
          "calculate": "datum['_extra'] == 1 ? datum['_max_row'] + 1 : datum['__row__']",
          "as": "__row__"
        },
        {
          "calculate": "datum['_extra'] == 1 ? 'TOTAL SESSION' : datum['_event_name']",
          "as": "_event_name"
        },
        {
          "calculate": "datum['_event_name'] == 'Visual Container Lifecycle' ? ( datum['_event_end_zero'] - datum['_event_start_zero'] ) : null",
          "as": "_lifecycle_duration"
        },
        {
          "calculate": "datum['_event_name'] == 'Execute Semantic Query' ? datum['_event_duration'] : null",
          "as": "_model_duration"
        },
        {
          "calculate": "datum['_event_name'] == 'Execute DAX Query' ? datum['_event_duration'] : null",
          "as": "_dax_duration"
        },
        {
          "calculate": "datum['_event_name'] == 'Query' ? datum['_event_duration'] : null",
          "as": "_query_duration"
        },
        {
          "calculate": "datum['_event_name'] == 'Render' ? datum['_event_duration'] : null",
          "as": "_render_duration"
        },
        {
          "calculate": "indexof( ['Visual Container Lifecycle'], datum['_event_name'] ) > -1 ? 0 : indexof( ['Execute Semantic Query'], datum['_event_name'] ) > -1 ? 1 : indexof( ['Execute DAX Query'], datum['_event_name'] ) > -1 ? 2 : indexof( ['Query Generation', 'Query Pending', 'Execute Query', 'Serialize Rowset', 'Parse Query Result'], datum['_event_name'] ) > -1 ? 3 : indexof( ['Data View Transform', 'Visual Update Async', 'Visual Update'], datum['_event_name'] ) > -1 ? 4 : indexof( ['Resolve Parameters', 'Geocoding'], datum['_event_name'] ) > -1 ? 5 : indexof( ['TOTAL SESSION'], datum['_event_name'] ) > -1 ? 6 : 99",
          "as": "_event_category_id"
        },
        {
          "aggregate": [
            {
              "op": "count",
              "field": "_event_id",
              "as": "_category_events"
            },
            {
              "op": "sum",
              "field": "_event_duration",
              "as": "_category_duration"
            }
          ],
          "groupby": [
            "_event_category_id",
            "_DEV_ID", // include additional fields to pass-through aggregation
            "_lifecycle_duration",
            "_model_duration",
            "_dax_duration",
            "_query_duration",
            "_render_duration"
          ]
        },
        {
          "calculate": "['EVENT CATEGORY', 'Model', 'DAX', 'Query Pending', 'Render Visual', 'Others', 'TOTAL SESSION'][datum['_event_category_id']]",
          "as": "_event_category"
        },
        {
          "calculate": "datum['_event_category'] == 'Query Pending' ? datum['_query_duration'] : datum['_event_category'] == 'Render Visual' ? datum['_render_duration'] : datum['_category_duration']",
          "as": "_category_duration"
        },
        {
          "calculate": "indexof( ['Model', 'DAX', 'Query Pending', 'Render Visual', 'Others'], datum['_event_category'] ) > -1 ? datum['_event_category'] + ' \uD83D' : datum['_event_category']",
          "as": "_event_category_display_name"
        },
        // *** FUTURE DEVELOPMENT - USE "CRLF" INSTEAD OF ";" TO JOIN ARRAY ELEMENTS ***
        {
          "calculate": "datum['_event_category'] == 'Model' ? join( ['Execute Semantic Query'], '; ' ) : datum['_event_category'] == 'DAX' ? join( ['Execute DAX Query'], '; ' ) : datum['_event_category'] == 'Query Pending' ? join( ['Query', 'Query Generation', 'Query Pending', 'Execute Query', 'Serialize Rowset', 'Parse Query Result'], '; ' ) : datum['_event_category'] == 'Render Visual' ? join( ['Render', 'Data View Transform', 'Visual Update Async', 'Visual Update'], '; ' ) : datum['_event_category'] == 'Others' ? join( ['Resolve Parameters', 'Geocoding'], '; ' ) : 'n/a'",
          "as": "_category_events_for_tooltip"
        },
        {
          "calculate": "datum['_event_category_id'] == 0 ? 'COUNT' : datum['_category_events']",
          "as": "_category_events2"
        },
        {
          "joinaggregate": [
            {
              "op": "sum",
              "field": "_category_events",
              "as": "_total_events"
            },
            {
              "op": "max",
              "field": "_lifecycle_duration",
              "as": "_max_duration"
            },
            {
              "op": "max",
              "field": "_model_duration",
              "as": "_model_duration"
            },
            {
              "op": "max",
              "field": "_dax_duration",
              "as": "_dax_duration"
            },
            {
              "op": "max",
              "field": "_query_duration",
              "as": "_query_duration"
            },
            {
              "op": "max",
              "field": "_render_duration",
              "as": "_render_duration"
            }
          ]
        },
        {
          "filter": "datum['_event_category_id'] != 99"
        },
        {
          // subtract title, total, query, and render rows
          "calculate": "datum['_total_events'] - 4",
          "as": "_total_events"
        },
        // set the total events
        {
          "calculate": "datum['_event_category_id'] == 6 ? datum['_total_events'] : datum['_category_events2']",
          "as": "_category_events2"
        },
        // recalculate the category durations
        {
          "calculate": "datum['_event_category_id'] == 3 ? ( datum['_query_duration'] - datum['_model_duration'] - datum['_dax_duration'] ) : datum['_event_category_id'] == 4 ? datum['_render_duration'] : datum['_category_duration']",
          "as": "_category_duration2"
        },
        {
          "calculate": "datum['_event_category_id'] == 0 ? 'AVG (ms)' : datum['_event_category_id'] == 6 ? datum['_max_duration'] : datum['_category_duration2'] / datum['_category_events']",
          "as": "_category_average_duration2"
        },
        {
          "calculate": "datum['_event_category_id'] == 0 ? 'WEIGHT' : datum['_event_category_id'] == 6 ? 1 : datum['_category_duration2'] / datum['_max_duration']",
          "as": "_category_weight"
        },
        // adjust format string to suit dataset
        {
          "calculate": " datum['_event_category_id'] == 0 ? 'WEIGHT' : pbiFormat(datum['_category_weight'], '0.#%')",
          "as": "_category_weight2"
        }
      ],
      "encoding": {
        "y": {
          "field": "_event_category_id",
          "type": "nominal",
          "axis": null
        },
        "x": {
          "axis": null,
          "scale": {
            "range": [
              -200,
              780
            ]
          }
        }
      },
      "layer": [
        {
          // conditional conerRadius and colour
          // event_category_id = 0 --> title
          // event_category_id = 6 --> total
          "name": "BACKGROUND_BAR",
          "mark": {
            "type": "bar",
            "cornerRadiusTopLeft": {
              "expr": "datum['_event_category_id'] == 0 ? 8 : 0"
            },
            "cornerRadiusTopRight": {
              "expr": "datum['_event_category_id'] == 0 ? 8 : 0"
            },
            "cornerRadiusBottomLeft": {
              "expr": "datum['_event_category_id'] == 6 ? 8 : 0"
            },
            "cornerRadiusBottomRight": {
              "expr": "datum['_event_category_id'] == 6 ? 8 : 0"
            },
            "color": {
              "expr": "datum['_event_category_id'] == 0 ? '#4A4A4A' : datum['_event_category_id'] == 6 ? '#E3E3E3' : 'transparent'"
            }
          },
          "encoding": {
            "x": {
              "datum": -200
            },
            "x2": {
              "datum": 100
            }
          }
        },
        {
          "name": "CATEGORY",
          "mark": {
            "type": "text",
            "align": "left",
            "fontSize": {
              "expr": "datum['_event_category_id'] == 0 || datum['_event_category_id'] == 6 ? 16 : 14"
            },
            "fontWeight": {
              "expr": "datum['_event_category_id'] == 0 || datum['_event_category_id'] == 6 ? 'bold' : 'normal'"
            },
            "color": {
              "expr": "datum['_event_category_id'] == 0 ? 'white' : '#4F4F4F'"
            },
            "tooltip": true
          },
          "encoding": {
            "text": {
              "field": "_event_category_display_name",
              "type": "nominal"
            },
            "x": {
              "datum": -190
            },
            "tooltip": [
              {
                "field": "_category_events_for_tooltip",
                "type": "nominal",
                "title": "Events:"
              }
            ]
          }
        },
        {
          "name": "COUNT",
          "mark": {
            "type": "text",
            "align": "right",
            "fontSize": {
              "expr": "datum['_event_category_id'] == 0 || datum['_event_category_id'] == 6 ? 16 : 14"
            },
            "fontWeight": {
              "expr": "datum['_event_category_id'] == 0 || datum['_event_category_id'] == 6 ? 'bold' : 'normal'"
            },
            "color": {
              "expr": "datum['_event_category_id'] == 0 ? 'white' : datum['_event_category_id'] == 6 ? '#4A4A4A' : '#808080'"
            }
          },
          "encoding": {
            "text": {
              "field": "_category_events2",
              "type": "nominal"
            },
            "x": {
              "datum": -30
            }
          }
        },
        {
          "name": "AVERAGE",
          "mark": {
            "type": "text",
            "align": "right",
            "fontSize": {
              "expr": "datum['_event_category_id'] == 0 || datum['_event_category_id'] == 6 ? 16 : 14"
            },
            "fontWeight": {
              "expr": "datum['_event_category_id'] == 0 || datum['_event_category_id'] == 6 ? 'bold' : 'normal'"
            },
            "color": {
              "expr": "datum['_event_category_id'] == 0 ? 'white' : datum['_event_category_id'] == 6 ? '#4A4A4A' : '#808080'"
            }
          },
          "encoding": {
            "text": {
              "field": "_category_average_duration2",
              "type": "nominal",
              // adjust format string to suit dataset
              "formatType": "pbiFormat",
              "format": "#,#."
            },
            "x": {
              "datum": 30
            }
          }
        },
        {
          "name": "WEIGHT",
          "mark": {
            "type": "text",
            "align": "right",
            "fontSize": {
              "expr": "datum['_event_category_id'] == 0 || datum['_event_category_id'] == 6 ? 16 : 14"
            },
            "fontWeight": {
              "expr": "datum['_event_category_id'] == 0 || datum['_event_category_id'] == 6 ? 'bold' : 'normal'"
            },
            "color": {
              "expr": "datum['_event_category_id'] == 0 ? 'white' : datum['_event_category_id'] == 6 ? '#4A4A4A' : '#808080'"
            }
          },
          "encoding": {
            "text": {
              "field": "_category_weight2",
              "type": "nominal"
            },
            "x": {
              "datum": 90
            }
          }
        }
      ]
    }
  ]
}
```

</details>

### Links:

Here's the template:

[917.1 - JSON - Deneb Template - Performance Analysis - Multiple Visuals](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/916.1%20-%20deneb_template.dynamic_sunburst_chart.v1.8.2.json) *** FIX *** <br>
[917.2 - JSON - Deneb Template - Performance Analysis - Single Visual](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/916.1%20-%20deneb_template.dynamic_sunburst_chart.v1.8.2.json) *** FIX *** <br>

<br>

Here's an example Power BI file using the template:

[917.3 - PBIX - Deneb Example - Performance Analysis](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/916.2%20-%20Deneb%20Reusable%20Components%20-%20Dynamic%20Sunburst%20Chart%20-%20V1.8.2.pbix) *** FIX *** <br>

<br>

Here's the TMDL code:

[917.4 - TMDL - Performance Analysis - All](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/916.1%20-%20deneb_template.dynamic_sunburst_chart.v1.8.2.json) *** FIX *** <br>

<br>

Here's the support data file for Power BI visual types:

[917.5 - Data - Power BI Visual Internal and Display Names - Performance Analysis](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/916.1%20-%20deneb_template.dynamic_sunburst_chart.v1.8.2.json) *** FIX *** <br>

*- eof*
