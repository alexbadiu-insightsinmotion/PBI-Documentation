<img width="1280" height="710" alt="207 - Image - Title - Performance Quadrants" src="https://github.com/user-attachments/assets/ac38134c-9a37-470c-ade7-0eab0dbed875" />

## Performance Quadrants

*October 19, 2025*

The native Power BI scatter chart doesn't by default categorize the performance of data points. Deneb/Vega-Lite can be used to add ***Performance Quadrant*** backgrounds as well as an internal slider for performance quadrant threshold percentage.

I provide a Deneb template for just this scanario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "93b7159d-5a87-4403-b337-75b692ceb6bb",
      "generated": "2025-10-19T17:44:13.608Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Performance Quadrants",
      "description": "An augmented scatter chart underlaid by four dynamically-selectable performance quadrants",
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
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  \"axisQuantitative\": {\r\n    \"titleFont\": \"Segoe UI\",\r\n    \"titleFontSize\": 14,\r\n    \"titleColor\": \"#171717\",\r\n    \"titleFontWeight\": \"normal\",\r\n    \"titlePadding\": 10,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 10,\r\n    \"labelColor\": \"#4A4A4A\",\r\n    \"grid\": true,\r\n    \"gridColor\": \"#E3E3E3\",\r\n    \"domain\": true,\r\n    \"domainColor\": \"#CCCCCC\",\r\n    \"ticks\": true,\r\n    \"tickColor\": \"#4A4A4A\",\r\n    \"tickSize\": 3\r\n  },\r\n  \"style\": {\r\n    \"_summary_text_style\": {\r\n      \"align\": \"left\",\r\n      \"lineBreak\": \"|\",\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 14,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"italic\"\r\n    },\r\n    \"_quadrant_divider_rule_style\": {\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_quadrant_label_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 14,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"italic\"\r\n    },\r\n    \"_point_style\": {\r\n      \"size\": 400\r\n    }\r\n  }\r\n}",
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
        "name": "Subcategory Value 1",
        "description": "The value to be plotted on the X axis",
        "kind": "measure",
        "type": "numeric"
      },
      {
        "key": "__3__",
        "name": "Subcategory Value 2",
        "description": "The value to be plotted on the Y axis",
        "kind": "measure",
        "type": "numeric"
      }
    ]
  },
  // dataset (from Power BI)
  "data": {
    "name": "dataset"
  },
  "transform": [
    // assign internal names to dataset fields
    {
      "calculate": "datum['__2__']",
      "as": "_x"
    },
    {
      "calculate": "datum['__3__']",
      "as": "_y"
    },
    // compose a composite name (in case there are multiple subcategories with the same name [but in different categories])
    {
      "calculate": "datum['__0__'] + '-' + datum['__1__']",
      "as": "_category_subcategory"
    },
    // assign constant values regardless of filtering
    {
      "window": [
        {
          "op": "rank",
          "as": "_rank"
        }
      ],
      "sort": [
        {
          "field": "_category_subcategory",
          "order": "ascending"
        }
      ]
    },
    // calculate the min and max of X and Y values
    {
      "joinaggregate": [
        {
          "op": "min",
          "field": "_x",
          "as": "_min_x"
        },
        {
          "op": "max",
          "field": "_x",
          "as": "_max_x"
        },
        {
          "op": "min",
          "field": "_y",
          "as": "_min_y"
        },
        {
          "op": "max",
          "field": "_y",
          "as": "_max_y"
        },
        {
          "op": "sum",
          "field": "_x",
          "as": "_sum_x"
        },
        {
          "op": "count",
          "field": "_rank",
          "as": "_total_number_of_subcategories"
        }
      ]
    },
    // calculate the threshold X and Y values
    // (adjust to suit parameters implemented)
    {
      "calculate": "datum['_min_x'] + ( ( datum['_max_x'] - datum['_min_x'] ) * ( _threshold_percent / 100 ) )",
      "as": "_threshold_x"
    },
    {
      "calculate": "datum['_min_y'] + ( ( datum['_max_y'] - datum['_min_y'] ) * ( _threshold_percent / 100 ) )",
      "as": "_threshold_y"
    },
    // Q1 = top right
    // Q2 = top left
    // Q3 = bottom right
    // Q4 = bottom left
    {
      "calculate": "datum['_x'] >= datum['_threshold_x'] && datum['_y'] >= datum['_threshold_y'] ? 1 : datum['_x'] < datum['_threshold_x'] && datum['_y'] >= datum['_threshold_y'] ? 2 : datum['_x'] >= datum['_threshold_x'] && datum['_y'] < datum['_threshold_y'] ? 3 : datum['_x'] < datum['_threshold_x'] && datum['_y'] < datum['_threshold_y'] ? 4 : -99",
      "as": "_quadrant_id"
    },
    {
      "calculate": "datum['_quadrant_id'] == 1 ? 'High/High' : datum['_quadrant_id'] == 2 ? 'High/Low' : datum['_quadrant_id'] == 3 ? 'Low/High' : datum['_quadrant_id'] == 4 ? 'Low/Low' : 'JUNK'",
      "as": "_quadrant_name"
    }
  ],
  "params": [
    // implement a single parameter if a common percentage is desired for both axes
    {
      "name": "_threshold_percent",
      "value": 50,
      "bind": {
        "input": "range",
        "min": 20,
        "max": 80,
        "step": 10,
        "name": "Threshold %: "
      }
    }
    // implment dual paremters if individual percentages are desired for each axis
    // {
    //   "name": "_threshold_percent_x",
    //   "value": 50,
    //   "bind": {
    //     "input": "range",
    //     "min": 0,
    //     "max": 100,
    //     "step": 1,
    //     "name": "X Threshold %: "
    //   }
    // },
    // {
    //   "name": "_threshold_percent_y",
    //   "value": 50,
    //   "bind": {
    //     "input": "range",
    //     "min": 0,
    //     "max": 100,
    //     "step": 1,
    //     "name": "Y Threshold %: "
    //   }
    // }
    ,
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
    }
  ],
  "spacing": 4,
  "vconcat": [
    {
      "name": "SUMMARY_TEXT",
      "width": 540,
      "height": 10,
      "transform": [
        {
          "aggregate": [
            {
              "op": "sum",
              "field": "_x",
              "as": "_quadrant_sum_of_subcategory_value"
            },
            {
              "op": "count",
              "field": "_x",
              "as": "_quadrant_number_of_subcategories"
            }
          ],
          "groupby": [
            "_quadrant_id",
            // include any required extra fields from the source dataset in the [groupby] array
            "_total_number_of_subcategories",
            "_sum_x"
          ]
        },
        // filter dataset to only a single record
        {
          "filter": "datum['_quadrant_id'] == 1"
        },
        {
          "calculate": "datum['_quadrant_number_of_subcategories'] / datum['_total_number_of_subcategories']",
          "as": "_quadrant1_percent_of_subcategories"
        },
        {
          "calculate": "datum['_quadrant_sum_of_subcategory_value'] / datum['_sum_x']",
          "as": "_quadrant1_percent_of_subcategory_value"
        },
        // compose the summary text
        {
          "calculate": "datum['_quadrant_number_of_subcategories'] + ' cities have High Sales and High Quantity, | representing ' + format( datum['_quadrant1_percent_of_subcategories'], '.0%' ) + ' of total cities and ' + format( datum['_quadrant1_percent_of_subcategory_value'], '.0%' ) + ' of total revenue'",
          "as": "_summary_text"
        }
      ],
      "mark": {
        "type": "text",
        "x": -50,
        "y": 0,
        "style": "_summary_text_style"
      },
      "encoding": {
        "text": {
          "field": "_summary_text",
          "type": "nominal"
        }
      }
    },
    {
      "name": "PERFORMANCE_QUADRANTS",
      "width": 540,
      "height": 500,
      "encoding": {
        "x": {
          "type": "quantitative",
          "axis": {
            "tickCount": 7,
            "title": "Sales"
          },
          "scale": {
            "round": true,
            "zero": false
          }
        },
        "y": {
          "type": "quantitative",
          "axis": {
            "tickCount": 8,
            "title": "Quantity"
          },
          "scale": {
            "round": true,
            "zero": false
          }
        }
      },
      "layer": [
        {
          "name": "QUADRANT_RECTANGLES",
          "transform": [
            {
              "calculate": "datum['_quadrant_id'] == 1 ? datum['_threshold_x'] : datum['_quadrant_id'] == 2 ? datum['_min_x'] : datum['_quadrant_id'] == 3 ? datum['_threshold_x'] : datum['_quadrant_id'] == 4 ? datum['_min_x'] : null",
              "as": "_start_x"
            },
            {
              "calculate": "datum['_quadrant_id'] == 1 ? datum['_max_x'] : datum['_quadrant_id'] == 2 ? datum['_threshold_x'] : datum['_quadrant_id'] == 3 ? datum['_max_x'] : datum['_quadrant_id'] == 4 ? datum['_threshold_x'] : null",
              "as": "_end_x"
            },
            {
              "calculate": "datum['_quadrant_id'] == 1 ? datum['_threshold_y'] : datum['_quadrant_id'] == 2 ? datum['_threshold_y'] : datum['_quadrant_id'] == 3 ? datum['_min_y'] : datum['_quadrant_id'] == 4 ? datum['_min_y'] : null",
              "as": "_start_y"
            },
            {
              "calculate": "datum['_quadrant_id'] == 1 ? datum['_max_y'] : datum['_quadrant_id'] == 2 ? datum['_max_y'] : datum['_quadrant_id'] == 3 ? datum['_threshold_y'] : datum['_quadrant_id'] == 4 ? datum['_threshold_y'] : null",
              "as": "_end_y"
            },
            {
              "aggregate": [
                {
                  "op": "sum",
                  "field": "_x",
                  "as": "_quadrant_sum_of_subcategory_value"
                },
                {
                  "op": "count",
                  "field": "_x",
                  "as": "_quadrant_number_of_subcategories"
                }
              ],
              "groupby": [
                "_quadrant_id",
                // include any required extra fields from the source dataset in the [groupby] array
                "_quadrant_name",
                "_min_x",
                "_max_x",
                "_min_y",
                "_max_y",
                "_threshold_x",
                "_threshold_y",
                "_start_x",
                "_end_x",
                "_start_y",
                "_end_y"
              ]
            },
            {
              "calculate": "datum['_quadrant_id'] <= 2 ? datum['_max_y'] : datum['_quadrant_id'] <= 4 ? datum['_min_y'] : 0",
              "as": "_quadrant_name_y"
            },
            {
              "calculate": "datum['_quadrant_id'] <= 2 ? 8 : datum['_quadrant_id'] <= 4 ? -4 : 0",
              "as": "_quadrant_name_yoffset"
            },
            {
              "calculate": "datum['_quadrant_id'] == 1 ? datum['_threshold_x'] + ( datum['_max_x'] - datum['_threshold_x'] ) / 2 : datum['_quadrant_id'] == 2 ? datum['_threshold_x'] - ( datum['_threshold_x'] - datum['_min_x'] ) / 2 : datum['_quadrant_id'] == 3 ? datum['_threshold_x'] + ( datum['_max_x'] - datum['_threshold_x'] ) / 2 : datum['_quadrant_id'] == 4 ? datum['_threshold_x'] - ( datum['_threshold_x'] - datum['_min_x'] ) / 2 : null",
              "as": "_mid_x"
            }
          ],
          "layer": [
            {
              "name": "RECTANGLES",
              "mark": {
                "type": "rect",
                "opacity": 0.3
              },
              "encoding": {
                "x": {
                  "field": "_start_x"
                },
                "x2": {
                  "field": "_end_x"
                },
                "y": {
                  "field": "_start_y"
                },
                "y2": {
                  "field": "_end_y"
                },
                "color": {
                  "field": "_quadrant_id",
                  // turn off the legend automatically generated by Vega-Lite
                  // "legend": null,
                  "scale": {
                    "domain": [
                      1,
                      2,
                      3,
                      4
                    ],
                    "range": [
                      "#737373",
                      "#969696",
                      "#ABABAB",
                      "#BDBDBD"
                    ]
                  },
                  // disable the legend automatically-generated by Vega-Lite
                  "legend": null
                }
              }
            },
            {
              "name": "QUADRANT_DIVIDERS",
              "transform": [
                {
                  "filter": "datum['_quadrant_id'] == 1"
                }
              ],
              "layer": [
                {
                  "name": "VERTICAL_QUADRANT_DIVIDER",
                  "mark": {
                    "type": "rule",
                    "style": "_quadrant_divider_rule_style"
                  },
                  "encoding": {
                    "x": {
                      "field": "_threshold_x"
                    }
                  }
                },
                {
                  "name": "HORIZONTAL_QUADRANT_DIVIDER",
                  "mark": {
                    "type": "rule",
                    "style": "_quadrant_divider_rule_style"
                  },
                  "encoding": {
                    "y": {
                      "field": "_threshold_y"
                    }
                  }
                }
              ]
            },
            {
              "name": "QUADRANT_NAMES",
              "mark": {
                "type": "text",
                "baseline": {
                  "expr": "if( datum['_quadrant_id'] <= 2, 'top', 'bottom' )"
                },
                "yOffset": {
                  "expr": "if( datum['_quadrant_id'] <= 2, 4, -4 )"
                },
                "style": "_quadrant_label_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_quadrant_name",
                  "type": "nominal"
                },
                "x": {
                  "field": "_mid_x",
                  "type": "quantitative"
                },
                "y": {
                  "field": "_quadrant_name_y",
                  "type": "quantitative"
                }
              }
            }
          ]
        },
        {
          "name": "POINTS",
          "transform": [
            {
              // adjust quadrant marker shapes as desired
              /* 
                plotting shapes: "circle", "square", "cross", "diamond", "triangle-up", "triangle-down", "triangle-right", or "triangle-left".
                the line symbol: "stroke"
                centered directional shapes: "arrow", "wedge", or "triangle"
                default value: "circle"
                https://vega.github.io/vega-lite/docs/point.html
              */
              "calculate": "datum['_quadrant_id'] == 1 ? 'diamond' : datum['_quadrant_id'] == 2 ? 'circle' : datum['_quadrant_id'] == 3 ? 'square' : datum['_quadrant_id'] == 4 ? 'triangle-down' : 'wedge'",
              "as": "_point_shape"
            },
            {
              // adjust quadrant marker border colour as desired
              "calculate": "datum['_quadrant_id'] == 1 ? _theme_colour_1 : datum['_quadrant_id'] == 2 ? _theme_colour_2 : datum['_quadrant_id'] == 3 ? _theme_colour_3 : datum['_quadrant_id'] == 4 ? _theme_colour_4 : 'transparent'",
              "as": "_point_stroke_colour"
            },
            {
              // adjust quadrant makder fill colour as desired
              "calculate": "datum['_quadrant_id'] == 1 ? _theme_colour_1 : 'transparent'",
              "as": "_point_fill_colour"
            }
          ],
          "mark": {
            "type": "point",
            "shape": {
              "expr": "datum['_point_shape']"
            },
            "stroke": {
              "expr": "datum['_point_stroke_colour']"
            },
            "fill": {
              "expr": "datum['_point_fill_colour']"
            },
            "tooltip": true,
            "style": "_point_style"
          },
          "encoding": {
            "x": {
              "field": "_x",
              "axis": {
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#,0,,.0 M"
              }
            },
            "y": {
              "field": "_y"
            },
            "tooltip": [
              {
                "field": "__0__",
                "type": "nominal"
              },
              {
                "field": "__1__",
                "type": "nominal"
              },
              {
                "field": "_x",
                "type": "quantitative",
                "title": "Sales",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "$#,0."
              },
              {
                "field": "_y",
                "type": "quantitative",
                "title": "Quantity",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#,0."
              }
            ]
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
- a standard Power BI dataset
- a ***transform*** block with:
	- 2x ***calculate*** transforms to assign internal names to the dataset fields
    - a ***calculate*** transform to create a composite subcategory label (category:subcategory) (in case there are duplicate subcategory names in different categories)
    - a ***window/rank*** transform to rank the composite subcategory labels (for constant access to a specific ranked record in the dataset regardless of any filtering)
    - 6x ***joinaggregate*** transforms to calculate the min and max X and Y values, and the total sum of X values and total number of subcategories
    - 2x ***calculate*** transforms to dynamically calculate the threshold X and Y values (using the selected threshold percentage value)
    - 2x ***calculate*** transforms to assign quadrant IDs and names to each record
 - a ***params*** block with:
    - a ***range*** parameter (screen widget) to enable the user to dynamically select the desired quadrant threshold percentage
    - 8x ***expr*** parameters to internalize the Power BI theme colours (for use in subsequent expressions)
- a ***vconcat*** block for the summary text and performance quadrants

1 - Summary Text:
- a nested ***transform*** block with:
    - 2x ***aggregate*** transforms to aggregate the dataset to 4 records (1 per quadrant)
      - *additional dataset fields were included in the ***groupby*** block to add them to the aggregation*
    - a ***filter*** transform to restrict the dataset to a single record (for performance quadrant 1)
    - 3x ***calculate*** transforms to calculate the percentage and summary text values
      - *percentage formatting using Vega-Lite expressions*
- a ***text*** mark using a named style

2 - Performance Quadrants:
- a ***shared encoding*** block to ensure the same X and Y values are used for all layered marks
- a ***layer*** block for the quadrant rectangles and scatter chart

2a - General:
- a nested ***transform*** block with:
    - 4x ***calculate*** transforms to determine the start and end X and Y values for each quadrant
    - 2x ***aggregate*** transforms to aggregate the dataset to 4 records (1 per quadrant)
      - *additional dataset fields were included in the ***groupby*** block to add them to the aggregation*
    - 3x ***calculate*** transforms to determine the X and Y coordinates and Y offset for the names for each quadrant
- a nested ***layer*** block for the quadrant rectangles, dividers, and names

2b - Quadrant Rectangles:
- a ***rect*** mark with:
    - ranged X and Y values as calculated in the ***transform*** block above
    - a ***color\scale\domain\range*** block to assign darker-to-lighter greyscale values to the quadrants

2c - Vertical Quadrant Divider:
- a ***rule*** mark with:
    - a *named style*
    - only an X value (the X threshold)

2d - Horizontal Quadrant Divider:
- a ***rule*** mark with:
    - a *named style*
    - only a Y value (the Y threshold)

2e - Quadrant Names:
- a ***text*** mark with:
    - conditional baseline and Y offset
    - a *named style*

3 - Scatter Chart:
- a nested ***transform*** block with:
    - 3x ***calculate*** transforms to determine the conditional marker shape, border (stroke) colour, and fill colour for each quadrant
      - *the stroke and fill colours use the Power BI Theme colours as enabled by Deneb (and as internalized in the ***params*** block above)*
- a ***point*** mark with:
    - conditional marker shape, stroke colour, and fill colour as calculated in the ***transform*** block above
    - a custom tooltip
    - a *named style*
    - X axis label formatting using a Power BI format string as enabled by Deneb

4 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
	- quantitative axes (title font attributes [family, size, colour, weight, padding], label attributes [family, size, colour], grid attributes [enabled, colour], domain attributes [enabled, colour], ticks [enabled, colour, size])
    - named styles:
		- summary text (alignment, line break character, font family, font size, font weight, font style)
        - quadrant divider rule (colour)
        - quadrant label text (font family, font size, font weight, font style)
		- marker point (size)

<hr>

### Links:

Here's the template:

[907.1 - JSON - Deneb Template - Performance Quadrants](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/907.1%20-%20deneb_template.performance_quadrants.v1.8.1.json) <br>

<br>

Here's an example Power BI file using the template:

[907.2 - PBIX - Deneb Example - Performance Quadrants](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/907.2%20-%20Deneb%20Reusable%20Components%20-%20Performance%20Quadrants%20-%20V1.8.1.pbix) <br>

*- eof*
