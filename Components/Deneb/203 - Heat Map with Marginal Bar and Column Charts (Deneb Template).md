<img width="1280" height="710" alt="203 - Image - Title Heat Map with Marginal Bar and Column Charts" src="https://github.com/user-attachments/assets/d629f418-b499-4b2c-827b-0c39c5f84f43" />

## Heat Map with Marginal Bar and Column Charts

*September 24, 2025*

Heat maps are often extended in Power BI with additional native visuals for bar and column charts with different aggregations. It is incumbent upon the developer to ensure consistent behaviour, sizes, colours, and alignment.

One of the features built-in to the Vega-Lite language is the ability to combine a number of visuals into a single ***composite*** visual that may both reduce developer effort and expose additional insights. Deneb/Vega-Lite ensures alignment automatically and produces only a single visual. I provide a Deneb template for a heat map with marginal bar and column charts.

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "98afa1d4-a749-40c7-a501-a451fdb52c1d",
      "generated": "2025-09-24T14:45:57.221Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Heat Map with Marginal Bar and Column Charts",
      "description": "Matrix (heat map) of total sales by day of the week by hour of the day with both marginal Bar Chart of aggregated total sales by hour of the day and marginal Column Chart of aggregated total sales by day of the week",
      "author": "Greg Philps"
    },
    "deneb": {
      "build": "1.8.1.0",
      "metaVersion": 1,
      "provider": "vegaLite",
      "providerVersion": "6.1.0"
    },
    "interactivity": {
      "tooltip": true,
      "contextMenu": true,
      "selection": false,
      "selectionMode": "simple",
      "highlight": false,
      "dataPointLimit": 50
    },
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  // add padding to each mark\r\n  \"scale\": {\r\n    \"bandPaddingInner\": 0.15\r\n  },\r\n  \"axis\": {\r\n    \"title\": null,\r\n    \"ticks\": null,\r\n    \"domain\": false,\r\n    // add padding to axis labels\r\n    \"labelPadding\": 14,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 14\r\n  },\r\n  \"axisX\": {\r\n    // show X-axis labels horizontally\r\n    \"labelAngle\": 0,\r\n    // show X-axis labels at top\r\n    \"orient\": \"top\"\r\n  },\r\n  \"axisQuantitative\": {\r\n    \"labels\": false,\r\n    \"grid\": false\r\n  },\r\n  \"title\": {\r\n    \"font\": \"Segoe UI\",\r\n    \"fontSize\": 20,\r\n    \"fontWeight\": \"bold\",\r\n    \"fontStyle\": \"italic\",\r\n    \"color\": \"#4A4A4A\",\r\n    \"subtitleFont\": \"Segoe UI\",\r\n    \"subtitleFontSize\": 16,\r\n    \"subtitleFontWeight\": \"normal\",\r\n    \"subtitleFontStyle\": \"italic\",\r\n    \"subtitleColor\": \"#969696\"\r\n  },\r\n  \"style\": {\r\n    \"_divider_rule_style\": {\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_heat_map_style\": {\r\n      // *** FIX ***\r\n\r\n\r\n      \"cornerRadius\": 4\r\n    },\r\n    \"_bar_chart_style\": {\r\n      \"cornerRadiusEnd\": 4\r\n    },\r\n    \"_column_chart_style\": {\r\n      \"cornerRadiusBottomLeft\": 4,\r\n      \"cornerRadiusBottomRight\": 4\r\n    }\r\n  }\r\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Transaction ID",
        "description": "",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__1__",
        "name": "DateTime",
        "description": "",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__2__",
        "name": "Sales",
        "description": "",
        "kind": "column",
        "type": "numeric"
      }
    ]
  },
  // text and position only; formatting done in "config\title"
  "title": {
    "anchor": "start",
    "align": "left",
    "offset": 10,
    "text": "Heat Map with Marginal Bar and Column Charts",
    "subtitle": "(darker=higher; lighter=lower)"
  },
  // set the desired padding (0 used to minimize white space)
  "padding": {
    "top": 0,
    "bottom": 0,
    "left": 0,
    "right": 0
  },
  // dataset (from Power BI)
  "data": {
    "name": "dataset"
  },
  // calculate the colours for each visual independently
  "resolve": {
    "scale": {
      "color": "independent"
    }
  },
  "transform": [
    // extend the dataset with date values
    {
      "calculate": "day( datum['__1__'] )",
      "as": "_day_of_week"
    },
    {
      "calculate": "dayFormat( datum['_day_of_week'] )",
      "as": "_day_of_week_name"
    },
    {
      "calculate": "dayAbbrevFormat( datum['_day_of_week'] )",
      "as": "_day_of_week_short_name"
    },
    {
      "calculate": "pad( datum['_day_of_week'], 2, '0', 'left' ) + '-' + datum['_day_of_week_short_name']",
      "as": "_day_of_week_number_label"
    },
    // extend the dataset with time values
    {
      "calculate": "hours( datum['__1__'] )",
      "as": "_hour24"
    },
    {
      "calculate": "datum['_hour24'] < 13 ? datum['_hour24'] : datum['_hour24'] - 12",
      "as": "_hour12"
    },
    {
      "calculate": "datum['_hour24'] < 12 ? datum['_hour12'] + ' AM': datum['_hour12'] + ' PM'",
      "as": "_hour_ampm"
    },
    {
      "calculate": "pad( datum['_hour24'], 2, '0', 'left' ) + '-' + datum['_hour_ampm']",
      "as": "_hour_number_label"
    }
  ],
  "spacing": 10,
  "vconcat": [
    {
      "name": "DIVIDER",
      "width": 390,
      "height": 10,
      // hard-code a single-record dataset
      "data": {
        "values": [
          {
            "id": 1
          }
        ]
      },
      "mark": {
        "type": "rule",
        "xOffset": -50,
        "style": "_divider_rule_style"
      },
      "encoding": {
        "y": {
          "datum": 2,
          "scale": {
            "domain": [
              0,
              1
            ]
          },
          "axis": null
        },
        "x": {
          "datum": -100,
          "axis": null
        },
        "x2": {
          "datum": 100
        }
      }
    },
    {
      "name": "TOP_SECTION",
      "spacing": 10,
      "hconcat": [
        {
          "name": "HEAT_MAP",
          // // alternative: use fixed width and height
          // "width": 400,
          // "height": 500,
          // alternative: use width and height step sizes for "rect" marks (use same size for "square")
          "width": {
            "step": 40
          },
          "height": {
            "step": 40
          },
          "mark": {
            "type": "rect",
            "tooltip": true,
            "style": "_heat_map_style"
          },
          "encoding": {
            "y": {
              "field": "_hour_number_label",
              "type": "nominal",
              "axis": {
                // extract the hour name from the composite label
                "labelExpr": "slice( datum.value, 3, 100 )",
                "title": null
              }
            },
            "x": {
              "field": "_day_of_week_number_label",
              "type": "nominal",
              "axis": {
                // extract the day name from the composite label              
                "labelExpr": "slice( datum.value, 3, 100 )",
                "title": null
              }
            },
            // alternative: use Power BI theme colours 
            "fill": {
              "field": "__2__",
              "type": "quantitative",
              "legend": null,
              "scale": {
                "range": [
                  {
                    "expr": "pbiColor(0)"
                  },
                  {
                    "expr": "pbiColor(4)"
                  }
                ]
              }
            },
            // // alternative: use named colours 
            // "fill": {
            //   "field": "Sales",
            //   "type": "quantitative",
            //   "legend": null,
            //   "scale": {
            //     "range": [
            //       "#FAF9F5",
            //       "#D4C4B0"
            //     ]
            //   }
            // },
            // // alternative: use Vega-Lite built-in color scheme
            // "fill": {
            //   "bin": true,
            //   "field": "Sales",
            //   "type": "quantitative",
            //   "aggregate": "sum",
            //   "legend": null,
            //   "scale": {
            //     "scheme": "browns"
            //     // for more Vega-Lite Sequential Colour Schemes see: https://vega.github.io/vega/docs/schemes/
            //   }
            // },
            "tooltip": [
              {
                "field": "_day_of_week_name",
                "type": "nominal",
                "title": "Day of Week"
              },
              {
                "field": "_hour_ampm",
                "type": "nominal",
                "title": "Hour"
              },
              {
                "field": "__2__",
                "type": "quantitative",
                "title": "__2__"
              }
            ]
          }
        },
        {
          "name": "BAR_CHART",
          "width": 100,
          "height": 520,
          "mark": {
            "type": "bar",
            "height": {
              "band": 0.9
            },
            "tooltip": true,
            "style": "_bar_chart_style"
          },
          "encoding": {
            "y": {
              "field": "_hour_number_label",
              "type": "nominal",
              "axis": null
            },
            "x": {
              "field": "__2__",
              "type": "quantitative",
              "aggregate": "sum"
            },
            "color": {
              "field": "__2__",
              "type": "quantitative",
              "aggregate": "sum",
              "legend": null,
              // use a gradient of the current Power BI theme colours from 1 to 8
              "scale": {
                "range": [
                  {
                    "expr": "pbiColor(3)"
                  },
                  {
                    "expr": "pbiColor(7)"
                  }
                ]
              }
            },
            "tooltip": [
              {
                "field": "_hour_ampm",
                "type": "nominal",
                "title": "Hour"
              },
              {
                "field": "__2__",
                "type": "quantitative",
                "aggregate": "sum",
                "title": "__2__",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#,##0."
              }
            ]
          }
        }
      ]
    },
    {
      "name": "COLUMN_CHART",
      "width": 280,
      "height": 100,
      "mark": {
        "type": "bar",
        "width": {
          "band": 0.9
        },
        "tooltip": true,
        "style": "_column_chart_style"
      },
      "encoding": {
        "y": {
          "field": "__2__",
          "type": "quantitative",
          "aggregate": "sum",
          "scale": {
            "reverse": true
          }
        },
        "x": {
          "field": "_day_of_week",
          "type": "nominal",
          "axis": null
        },
        "color": {
          "field": "__2__",
          "type": "quantitative",
          "aggregate": "sum",
          "legend": null,
          // use a gradient of the current Power BI theme colours from 1 to 8
          "scale": {
            "range": [
              {
                "expr": "pbiColor(3)"
              },
              {
                "expr": "pbiColor(7)"
              }
            ]
          }
        },
        "tooltip": [
          {
            "field": "_day_of_week_name",
            "type": "nominal",
            "title": "Day of Week"
          },
          {
            "field": "__2__",
            "type": "quantitative",
            "aggregate": "sum",
            "title": "__2__",
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#,##0."
          }
        ]
      }
    }
  ]
}
```

</details>

<br>

This template displays a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block with ***subtitle***
- a ***padding*** block (all margins set to zero) to minimize whitespace
- a ***resolve*** block to configure Vega-Lite to apply colours independently to each visual
- a ***transform*** block with:
	- 3x ***calculate*** transforms to determine the day-of-the-week
	- a ***calculate*** transform to determine the composite day-of-the-week label
	- 3x ***calculate*** transforms to determine the hour-of-the-day
	- a ***calculate*** transform to determine the composite hour-of-the-day label
- a ***vconcat*** block for the divider, the heat map and bar chart (horizontally-concatenated), and the column chart

1 - Divider:
- a ***rule*** mark with:
  - a single-record hard-coded dataset
  - ranged X values to set the starting point and width
  - a named style
 
2 - Heat Map:
- a ***hconcat*** block for:
	- a ***rect*** mark for the matrix with:
        - fixed step size for both width and height (40) to produce squares
		- Y axis:
			- uses the hour name extracted from the composite hour-of-the-day label
		- X axis:
			- uses the day name extracted from the composite day-of-the-week label
			- sets the axis location to the top
		- gradient colour boundries set to the *Power BI theme colours* (1 to 5)
		- a custom tooltip
 
3 - Bar Chart:
- a ***bar*** mark with:
	- 90% band height
	- a named style
	- a custom tooltip
	- aggregated by hour-of-the-day
	- a gradient colour scale from the Power BI theme colours (4 to 8)
	- a custom tooltip
	
4 - Column Chart:
- a ***bar*** mark with:
	- inverted X and Y axes to render as a column chart
		- Y axis has scale reversed to render downwards
	- 90% band height
	- a named style
	- a custom tooltip
	- aggregated by day-of-the-week
	- a gradient colour scale from the Power BI theme colours (4 to 8)
	- a custom tooltip	

5 - Config:
- configuration values set for:
	- border (colour set to null)
	- inner padding (15%, to show a gap between ***rect*** marks in the matrix)
	- general axis characteristics (no title, no domain, no ticks, label padding, label font family, label font size)
	- X axis (horizontal values, positioned at visual top)
	- quantitative axes (no labels, no grid)
	- named styles:
		- divider (colour)
        - heat map (rounded corners = 4 px)
		- bar chart (rounded corners [right end] = 4 px)
		- column chart (rounded corners [bottom] = 4 px)	

<hr>

### Links:

Here's the template:

[903.1 - JSON - Deneb Template - Heat Map with Marginal Bar and Column Charts ](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/903.1%20-%20deneb_template.heat_map_with_marginal_bar_and_column_charts.v1.8.1.json)

<br>

Here's an example Power BI file using the template:

[903.2 - PBIX - Deneb Example - Heat Map with Marginal Bar and Column Charts ](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/903.2%20-%20Deneb%20Reusable%20Components%20-%20Heat%20Map%20with%20Marginal%20Bar%20and%20Column%20Charts%20-%20V1.8.1.pbix)

*- eof*
