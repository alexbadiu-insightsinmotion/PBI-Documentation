<img width="1280" height="710" alt="206 - Image - Title - 2-Level Column Chart" src="https://github.com/user-attachments/assets/d5761de9-3890-4c44-bb92-cb741e719407" />

## 2-Level Column Chart

*October 14, 2025*

The native Power BI native stacked column chart (or clustered column chart) can appear cluttered when showing multiple levels. Deneb/Vega-Lite can be used to reduce clutter and produce a ***2-Level Column Chart*** that reduces clutter. 

> [!NOTE]
> Such a chart has been called many names, including *Alternative Stacked Bar Chart*, *Multi-series Column Chart*, *Grouped Column Chart*, *Hierarchical Column Chart*, *Dual-Level Column Chart*, *Bilevel Column Chart*; Alex and I have chosen *2-Level Column Chart* for this type of chart

I provide a Deneb template for just this scanario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "70b0a9f5-5fd4-41b7-b18d-8f8a41573218",
      "generated": "2025-10-14T15:12:40.066Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "2-Level Column Chart",
      "description": "A standard column chart of category with a clustered column chart of subcategory overlaid; data labels are provided for both levels.",
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
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  \"axisY\": {\r\n    \"ticks\": false,\r\n    \"grid\": false,\r\n    \"domain\": false\r\n  },\r\n  \"axisX\": {\r\n    \"ticks\": false,\r\n    \"grid\": false,\r\n    \"domain\": false,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 14,\r\n    // set to desired vertical pixels between axis and labels (default = 2)\r\n    \"labelPadding\": 4\r\n  },\r\n  \"title\": {\r\n    \"font\": \"Segoe UI\",\r\n    \"fontSize\": 24,\r\n    \"fontWeight\": \"bold\",\r\n    \"fontStyle\": \"italic\",\r\n    \"color\": \"#4A4A4A\",\r\n    \"subtitleFont\": \"Segoe UI\",\r\n    \"subtitleFontSize\": 16,\r\n    \"subtitleFontWeight\": \"normal\",\r\n    \"subtitleFontStyle\": \"italic\",\r\n    \"subtitleColor\": \"#969696\"\r\n  },\r\n  \"legend\": {\r\n    \"orient\": \"top\",\r\n    \"direction\": \"horizontal\",\r\n    \"offset\": 0,\r\n    \"title\": null,\r\n    \"symbolType\": \"circle\",\r\n    \"symbolSize\": 400,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 14,\r\n    \"labelFontStyle\": \"italic\"\r\n  },\r\n  \"style\": {\r\n    \"_divider_rule_style\": {\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_category_bar_style\": {\r\n      \"cornerRadiusEnd\": 4,\r\n      \"color\": \"#E3E3E3\"\r\n    },\r\n    \"_subcategory_bar_style\": {\r\n      // \"color\": \"#000000\",\r\n      \"cornerRadiusEnd\": 4,\r\n      \"stroke\": \"#E3E3E3\",\r\n      \"strokeWidth\": 2\r\n    },\r\n    \"_category_label_style\": {\r\n      \"align\": \"center\",\r\n      // adjust font size to fit chosen visual size\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 16,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#000000\"\r\n    },\r\n    \"_subcategory_label_style\": {\r\n      \"align\": \"center\",\r\n      \"baseline\": \"bottom\",\r\n      // adjust font size to fit chosen visual size\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#000000\"\r\n    }\r\n  }\r\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Category",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__1__",
        "name": "Subcategory",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__2__",
        "name": "Value",
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
    "text": "2-Level Column Chart",
    "subtitle": "(also known as Alternative Stacked Bar Chart)",
    "offset": 20
  },
  // dataset (from Power BI)
  "data": {
    "name": "dataset"
  },
  "transform": [
    // assign internal names to dataset fields
    {
      "calculate": "datum['__0__']",
      "as": "_category"
    },
    {
      "calculate": "datum['__1__']",
      "as": "_subcategory"
    },
    {
      "calculate": "datum['__2__']",
      "as": "_subcategory_value"
    },
    // calculate category value
    {
      "joinaggregate": [
        {
          "op": "sum",
          "field": "_subcategory_value",
          "as": "_category_value"
        }
      ],
      "groupby": [
        "_category"
      ]
    },
    // calculate category rank and label
    {
      "window": [
        {
          "op": "rank",
          "as": "_category_rank"
        }
      ],
      "sort": [
        {
          "field": "_category_value",
          "order": "descending"
        }
      ]
    },
    // create a composite label
    {
      "calculate": "pad( datum['_category_rank'], 2, '0', 'left' ) + '-' + datum['_category']",
      "as": "_category_rank_and_label"
    },
    // calculate subcategory rank and percent
    {
      "window": [
        {
          "op": "rank",
          "as": "_subcategory_rank"
        }
      ],
      "groupby": [
        "__0__"
      ],
      "sort": [
        {
          "field": "_subcategory_value",
          "order": "descending"
        }
      ]
    },
    {
      "calculate": "datum['_subcategory_value'] / datum['_category_value']",
      "as": "_subcategory_percent"
    }
  ],
  // set parameters for the Power BI theme colours
  "params": [
    {
      "name": "_theme_colour_1",
      "expr": "pbiColor(0)"
    },
    {
      "name": "_theme_colour_2",
      "expr": "pbiColor(1)"
    },
    {
      "name": "_theme_colour_3",
      "expr": "pbiColor(2)"
    },
    {
      "name": "_theme_colour_4",
      "expr": "pbiColor(3)"
    },
    {
      "name": "_theme_colour_5",
      "expr": "pbiColor(4)"
    },
    {
      "name": "_theme_colour_6",
      "expr": "pbiColor(5)"
    },
    {
      "name": "_theme_colour_7",
      "expr": "pbiColor(6)"
    },
    {
      "name": "_theme_colour_8",
      "expr": "pbiColor(7)"
    },
    {
      "name": "_legend_label_black",
      "value": 1 // 1 = black, any other value = Power BI theme colour
    }
  ],
  "layer": [
    {
      "name": "CATEGORY",
      "transform": [
        {
          "filter": "datum['_subcategory_rank'] == 1"
        }
      ],
      // shared encoding
      "encoding": {
        "x": {
          "field": "_category_rank_and_label",
          "type": "nominal",
          "axis": {
            // extract the category name from the composite label
            "labelExpr": "slice( datum.value, 3, 100 )",
            "labelAngle": 0,
            "title": null
          }
        },
        "y": {
          "field": "_category_value",
          "type": "quantitative",
          "axis": null
        }
      },
      "layer": [
        {
          "name": "CATEGORY_VALUE",
          "mark": {
            "type": "bar",
            "width": {
              "band": 1.05
            },
            "style": "_category_bar_style"
          }
        },
        {
          "name": "CATEGORY_LABEL",
          "mark": {
            "type": "text",
            "baseline": "top",
            "yOffset": 4,
            "style": "_category_label_style"
          },
          "encoding": {
            "text": {
              "field": "_category_value",
              "type": "quantitative",
              "formatType": "pbiFormat",
              // adjust Power BI format string as desired to suit dataset              
              "format": "#0,,.00 M"
            }
          }
        }
      ]
    },
    {
      "name": "SUBCATEGORY",
      // shared encoding
      "encoding": {
        "x": {
          "field": "_category_rank_and_label",
          "type": "nominal"
        },
        "xOffset": {
          "field": "_subcategory",
          "type": "nominal",
          "sort": {
            "field": "_subcategory_value",
            "order": "descending"
          }
        },
        "y": {
          "field": "_subcategory_value",
          "type": "quantitative"
        }
      },
      "layer": [
        {
          "name": "SUBCATEGORY_VALUE",
          "mark": {
            "type": "bar",
            "tooltip": true,
            "style": "_subcategory_bar_style"
          },
          "encoding": {
            "color": {
              "field": "_subcategory",
              "type": "nominal",
              // adjust scale\domain and scale\range to suit dataset
              "scale": {
                "domain": [
                  "Wholesale",
                  "Distributor",
                  "Export"
                ],
                // use current Power BI theme colours
                "range": [
                  {
                    "expr": "pbiColor(1)"
                  },
                  {
                    "expr": "pbiColor(3)"
                  },
                  {
                    "expr": "pbiColor(5)"
                  }
                ]
              },
              "legend": {
                "labelColor": {
                  // use Power BI theme colours via parameters
                  "expr": "_legend_label_black ? 'black' : datum.value == 'Wholesale' ? _theme_colour_2 : datum.value == 'Distributor' ? _theme_colour_4 : datum.value == 'Export' ? _theme_colour_6 :'transparent'"
                }
              }
            },
            "tooltip": [
              {
                "field": "_category",
                "type": "nominal",
                "title": "__0__"
              },
              {
                "field": "_subcategory",
                "type": "nominal",
                "title": "__1__"
              },
              {
                "field": "_subcategory_value",
                "type": "quantitative",
                "formatType": "pbiFormat",
                "format": "#,##0",
                "title": "Sales"
              },
              {
                "field": "_subcategory_percent",
                "type": "quantitative",
                "formatType": "pbiFormat",
                "format": "#%",
                "title": "% of Country Total"
              }
            ]
          }
        },
        {
          "name": "SUBCATEGORY_LABEL",
          "mark": {
            "type": "text",
            "align": "center",
            "style": "_subcategory_label_style"
          },
          "encoding": {
            "text": {
              "field": "_subcategory_value",
              "type": "quantitative",
              "formatType": "pbiFormat",
              // adjust Power BI format string as desired to suit dataset
              "format": "#0,,.0 M"
            }
          }
        }
      ]
    }
  ]
}
```

</details>

<br>

<br>

The template displays a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block with ***subtitle***
- a standard Power BI dataset
- a ***transform*** block with:
	- 3x ***calculate*** transforms to assign internal names to the dataset fields
    - a ***joinaggregate/sum*** transform to calculate the category value
    - a ***window/rank*** transform to rank the categories
    - a ***calculate*** transform to create a composite category label (rank:category)
    - a ***window/rank*** transform to rank the subcategories
 - a ***params*** block with:
    - 8x ***expr*** parameters to internalize the Power BI theme colours (for use in subsequent expressions)
- a ***layer*** block for the category and subcategory

1 - Category:
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to one record per category
- a ***shared encoding*** block to ensure the same X and Y values are used for all layered marks
- a nested ***layer*** block with:
    - a ***bar*** mark with:
        - 105% band width to provide a slightly wider bar than the subsequesnt clustered subcategories
        - a *named style*
    - a ***text*** mark with:
        - *baseline* = top and *yOffset* = 4 to locate the category value data label just inside the bar end
        - a *named style*
        - value formatting using a Power BI format string as enabled by Deneb

2 - Subcategory:
- a ***shared encoding*** block to ensure the same X and Y values and xOffset are used for all layered marks
- a nested ***layer*** block with:
    - a ***bar*** mark with:
        - a custom *tooltip*
        - a *named style*
        - a *scale\domain\range* block using the subcategory names and Power BI Theme colours
    - a ***text*** mark with:
        - a *named style*
        - value formatting using a Power BI format string as enabled by Deneb

3 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
    - Y axis (no domain, no ticks, no grid) 
	- X axis (no domain, no ticks, no grid, label font family, label font size, label padding)
    - title style
    - legend style
    - named styles:
		- divider (colour)
		- category bar (rounded corners, colour)
        - subcategory bar (rounded corners, stroke colour, stroke width)
        - category label (alignment, colour, font family, font size, font weight, font style)
        - subcategory label (alignment, colour, font family, font size, font style)

<hr>

### Links:

Here's the template:

[906.1 - JSON - Deneb Template - 2-Level Column Chart)](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/906.1%20-%20BEFORE%20RELEASE%20-%20deneb_template.2_level_column_chart.v1.8.1.json) <br>

<br>

Here's an example Power BI file using the template:

[906.2 - PBIX - Deneb Example - 2-Level Column Chart](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/906.2%20-%20Deneb%20Reusable%20Components%20-%202-Level%20Column%20Chart%20-%20V1.8.1.pbix) <br>

*- eof*
