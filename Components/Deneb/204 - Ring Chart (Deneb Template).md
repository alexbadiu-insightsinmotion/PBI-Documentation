<img width="1280" height="710" alt="204 - Image - Title Ring Chart" src="https://github.com/user-attachments/assets/49bcee0f-3c79-4f7b-9989-139b7fa9346f" />

## Ring Chart

*October 1, 2025*

The standard donut chart in Power BI can be used to display a KPI as a percentage. While it can also be used to display multiple measures as concentric donuts when multiple donut charts placed on top of one another, it is incumbent upon the developer to ensure consistent sizing, colouring, and alignment. Deneb/Vega-Lite permits a multi-layer visual and ensures proper sizing, colouring, and alignment. I provide a Deneb template for a ring chart (or 3-donut chart).

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json 
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "7864b3e2-17de-4e99-8114-de8212c99283",
      "generated": "2025-10-01T21:14:51.180Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Ring Chart",
      "description": "A chart of 3 concentric donut charts (rings) depicting percentage measures as a proportion of 100%",
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
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  \"title\": {\r\n    \"font\": \"Segoe UI\",\r\n    \"fontSize\": 24,\r\n    \"fontWeight\": \"bold\",\r\n    \"fontStyle\": \"italic\",\r\n    \"color\": \"#4A4A4A\",\r\n    \"subtitleFont\": \"Segoe UI\",\r\n    \"subtitleFontSize\": 16,\r\n    \"subtitleFontWeight\": \"normal\",\r\n    \"subtitleFontStyle\": \"italic\",\r\n    \"subtitleColor\": \"#969696\"\r\n  },\r\n  \"legend\": {\r\n    \"orient\": \"top\",\r\n    \"direction\": \"horizontal\",\r\n    \"title\": null,\r\n    \"symbolType\": \"circle\",\r\n    \"symbolSize\": 400,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 14,\r\n    \"labelFontStyle\": \"italic\"\r\n  },\r\n  \"style\": {\r\n    \"_divider_rule_style\": {\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_ring_background_style\": {\r\n      \"theta\": 0,\r\n      \"theta2\": {\r\n        \"expr\": \"2 * PI\"\r\n      },\r\n      \"color\": \"#969696\",\r\n      \"opacity\": 0.3\r\n    },\r\n    \"_ring_value_style\": {\r\n      // must be at least half the [_ring_width] parameter\r\n      \"cornerRadius\": 10,\r\n      \"opacity\": 1.0\r\n    },\r\n    \"_ring_label_style\": {\r\n      \"theta\": 0,\r\n      \"fontSize\": 12,\r\n      \"color\": \"#FFFFFF\"\r\n    },\r\n    \"_total_label_style\": {\r\n      \"align\": \"center\",\r\n      // adjust font size to fit chosen visual size\r\n      \"fontSize\": 16,\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_total_value_style\": {\r\n      \"align\": \"center\",\r\n      // adjust font size to fit the chosen visual size\r\n      \"fontSize\": 28,\r\n      \"color\": \"#000000\"\r\n    }\r\n  }\r\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Channel",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__1__",
        "name": "Total Sales",
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
    "offset": 10,
    "text": "Ring Chart"
  },
  // dataset (from Power BI)
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "joinaggregate": [
        {
          "op": "sum",
          "field": "__1__",
          "as": "_sum_total_sales"
        }
      ]
    },
    // rank the channels by sales
    {
      "window": [
        {
          "op": "rank",
          "as": "_channel_rank"
        }
      ],
      "sort": [
        {
          "field": "__1__",
          "order": "descending"
        }
      ]
    },
    // calculate the percent for each ring
    {
      "calculate": "datum['__1__'] / datum['_sum_total_sales']",
      "as": "_ring_percent"
    },
    // calculate the ending radians for each ring
    {
      "calculate": "2 * PI * datum['_ring_percent']",
      "as": "_ring_theta2"
    },
    // calculate the ring outer and inner sizes
    {
      "calculate": "_ring_max - ( _ring_width + _ring_gap ) * ( datum['_channel_rank'] - 1 )",
      "as": "_ring_outer_radius"
    },
    {
      "calculate": "datum['_ring_outer_radius'] - _ring_width",
      "as": "_ring_inner_radius"
    }
  ],
  "params": [
    // set ring sizes
    {
      "name": "_ring_max",
      "value": 200
    },
    {
      "name": "_ring_width",
      "value": 20
    },
    {
      "name": "_ring_gap",
      "value": 5
    }
  ],
  "layer": [
    {
      "name": "RING_BACKGROUND",
      "mark": {
        "type": "arc",
        "style": "_ring_background_style"
      },
      "encoding": {
        "radius": {
          "field": "_ring_outer_radius",
          "type": "quantitative"
        },
        "radius2": {
          "field": "_ring_inner_radius"
        }
      }
    },
    {
      "name": "RING",
      "mark": {
        "type": "arc",
        "style": "_ring_value_style",
        "theta": 0,
        "tooltip": true
      },
      "encoding": {
        "radius": {
          "field": "_ring_outer_radius",
          "type": "quantitative"
        },
        "radius2": {
          "field": "_ring_inner_radius"
        },
        "theta2": {
          "field": "_ring_theta2",
          "type": "quantitative"
        },
        "color": {
          "field": "__0__",
          "type": "nominal",
          "scale": {
            "domain": [
              "Wholesale",
              "Distributor",
              "Export"
            ],
            // use current Power BI theme colours
            "range": [
              {
                "expr": "pbiColor(0)"
              },
              {
                "expr": "pbiColor(4)"
              },
              {
                "expr": "pbiColor(7)"
              }
            ]
          },
          "sort": {
            "field": "_channel_rank",
            "order": "ascending"
          }
        },
        "tooltip": [
          {
            "field": "__0__",
            "type": "nominal"
          },
          {
            "field": "__1__",
            "type": "quantitative",
            "title": "Channel Sales",
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#,0"
          },
          {
            "field": "_ring_percent",
            "type": "quantitative",
            "title": "% of Total Sales",
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#0%"
          }
        ]
      }
    },
    {
      "name": "RING_LABEL",
      "mark": {
        "type": "text",
        "xOffset": 16,
        // adjust Y offset to fit the chosen visual size
        "yOffset": 10,
        "style": "_ring_label_style"
      },
      "encoding": {
        "text": {
          "field": "_ring_percent",
          "type": "quantitative",
          "formatType": "pbiFormat",
          // adjust Power BI format string as desired to suit dataset
          "format": "0%"
        },
        "radius": {
          "field": "_ring_outer_radius",
          "type": "quantitative"
        },
        "radius2": {
          "field": "_ring_inner_radius"
        }
      }
    },
    {
      "name": "TOTAL_LABEL",
      "mark": {
        "type": "text",
        "yOffset": -16,
        "style": "_total_label_style"
      },
      "encoding": {
        "text": {
          "value": "__1__"
        }
      }
    },
    {
      "name": "TOTAL",
      "mark": {
        "type": "text",
        "yOffset": 10,
        "style": "_total_value_style"
      },
      "encoding": {
        "text": {
          "field": "_sum_total_sales",
          "type": "quantitative",
          "formatType": "pbiFormat",
          // adjust Power BI format string as desired to suit dataset
          "format": "#,0"
        }
      }
    }
  ]
}
```
</details>

<hr>

This template displays a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block
- a ***transform*** block with:
	- a ***joinaggregate/sum*** transform to extend the Power BI dataset with the total sales
	- a ***window/rank*** transform to rank the channels by sales
	- 4x ***calculate*** transforms to determine the ring percent, ending radians, outer and inner radii
- a ***params*** block with:
	- 3x parameters for the ring maximum, width, and gap
- a ***layer*** block with five marks (background, ring, label, total label, and total)
	
1 - Ring Background:
- an ***arc*** mark with:
	- a named style
	- starting radius and ending radius

2 - Ring:
- an ***arc*** mark with:
	- a named style
	- starting radius and ending radius
	- starting radians (0) and ending radians
	- conditional colour using Power BI theme colours (1, 5, 8)
	- legend (top, horizontal, no title, circle, label font family, label font size, label font style)
	- a custom tooltip (channel, sales, percent of total sales)

3 - Ring Label:
- a ***text*** mark with:
	- a named style
	- percentage using Power BI formatting as provided by Deneb
	
4 - Total Label:
- a ***text*** mark with:
	- a named style
	- a hard-coded value

5 - Total:
- a ***text*** mark with:
	- a named style
	- value using Power BI formatting as provided by Deneb
	
6 - Config:
- configuration values set for:
	- border (colour set to null)
 	- title style
    - legend style
	- named styles:
  		- divider (colour)
		- ring background (starting radians = 0, ending radians = 2 * PI, colour, opacity)
		- ring value (rounded corners, opacity)
		- ring label (position, colour, opacity)
		- total label (alignment, font size, colour)
		- total value (alignment, font size, colour)		


### Links:

Here's the template:

[904.1 - JSON - Deneb Template - Ring Chart ](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/904.1%20-%20deneb_template.ring_chart.v1.8.1.json)

<br>

Here's an example Power BI file using the template:

[904.2 - PBIX - Deneb Example - Ring Chart ](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/904.2%20-%20Deneb%20Reusable%20Components%20-%20Ring%20Chart%20-%20V1.8.1.pbix)

*- eof*
