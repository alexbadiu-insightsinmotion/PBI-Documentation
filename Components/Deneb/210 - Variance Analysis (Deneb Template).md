<img width="1280" height="639" alt="210 - Image - Title - Variance Analysis" src="https://github.com/user-attachments/assets/e3871323-678c-48e1-8d45-5a33af3027a4" />

## Variance Analysis

*November 12, 2025*

Deneb/Vega-Lite can be used to create a composite variance analysis visual consisting of sections for the variance value, category, and variance percents.

The example presented here has an ***arrow chart*** for the variance value and a ***bar chart*** for the variance percent, along with a bottom legend; the variance values and percents and the legend use the Power BI theme sentiment colours.

I provide a Deneb template for just this scanario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "15067f3d-8b64-431f-98d0-a03e78fcdd8c",
      "generated": "2025-11-12T11:32:14.349Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Variance Analysis",
      "description": "A composite visual to present the variance between 2 periods with 5 columns: variance amount, variance amount arrow, category, variance percent bar, and variance percent",
      "author": "Greg Philps"
    },
    "deneb": {
      "build": "1.8.2.0",
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
    "config": "{\r\n  \"autosize\": {\r\n    \"type\": \"fit\",\r\n    \"resize\": true,\r\n    \"contains\": \"padding\"\r\n  },\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  \"lineBreak\": \"|\",\r\n  \"title\": {\r\n    \"font\": \"Segoe UI\",\r\n    \"fontSize\": 14,\r\n    \"color\": \"#4A4A4A\"\r\n  },\r\n  \"legend\": {\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelColor\": \"#4A4A4A\"\r\n  },\r\n  // the settings for the facet \"header\" (i.e., the category)\r\n  \"header\": {\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 16,\r\n    \"labelColor\": \"#1A1A1A\",\r\n    \"titleFont\": \"Segoe UI\",\r\n    \"titleFontSize\": 18,\r\n    \"titleColor\": \"#1A1A1A\"\r\n  },\r\n  \"axisX\": {\r\n    \"labelAngle\": 0,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelColor\": \"#7D7D7D\",\r\n    \"grid\": false,\r\n    \"ticks\": true\r\n  },\r\n  \"axisY\": {\r\n    \"grid\": true,\r\n    \"domain\": true,\r\n    \"ticks\": true,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 14,\r\n    \"labelColor\": \"#7D7D7D\"\r\n  },\r\n  \"style\": {\r\n    \"_divider_rule_style\": {\r\n      \"color\": \"#E3E3E3\"\r\n    },\r\n    \"_arrow_line_style\": {\r\n      \"strokeWidth\": 4,\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_arrowhead_point_style\": {\r\n      \"size\": 100,\r\n      \"filled\": true,\r\n      \"opacity\": 1\r\n    },\r\n    \"_category_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 14,\r\n      \"color\": \"#1A1A1A\"\r\n    },\r\n    \"_variance_value_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"color\": \"#4A4A4A\"\r\n    },\r\n    \"_variance_percent_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"color\": \"#4A4A4A\"\r\n    }\r\n  }\r\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Category ID",
        "description": "",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__1__",
        "name": "Category",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__2__",
        "name": "Period Name",
        "description": "",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__3__",
        "name": "Period Value",
        "description": "",
        "kind": "measure",
        "type": "numeric"
      }
    ]
  },
  // text and position and formatting (formatting done here to avoid conflicts with [hconcat] titles formatted in "config\title")
  "title": {
    "anchor": "start",
    "align": "left",
    "offset": 10,
    "text": {
      "expr": "'Variance Analysis'"
    },
    "subtitle": {
      "expr": "'Period Growth (amount and percent) from ' + format( data('dataset')[0]['Year'], '.0f' ) + ' to ' + format( data('dataset')[1]['Year'], '.0f' )"
    },
    "font": "Segoe UI",
    "fontSize": 24,
    "fontWeight": "bold",
    "fontStyle": "italic",
    "color": "#4A4A4A",
    "subtitleFont": "Segoe UI",
    "subtitleFontSize": 16,
    "subtitleFontWeight": "normal",
    "subtitleFontStyle": "italic",
    "subtitleColor": "#969696"
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "transform": [
    // assign internal names to the dataset fields
    {
      "calculate": "datum['__0__']",
      "as": "_category_id"
    },
    {
      "calculate": "datum['__1__']",
      "as": "_category"
    },
    {
      "calculate": "datum['__2__']",
      "as": "_period"
    },
    {
      "calculate": "datum['__3__']",
      "as": "_value"
    },
    {
      "window": [
        {
          "op": "rank",
          "as": "_period_rank"
        }
      ],
      "sort": [
        {
          "field": "_period",
          "order": "ascending"
        }
      ],
      "groupby": [
        "_category"
      ]
    },
    // determine the period 1 and period 2 values and variance
    {
      "calculate": "datum['_value']",
      "as": "_period1_value"
    },
    {
      "window": [
        {
          "op": "lead",
          "field": "_value",
          "as": "_period2_value"
        }
      ],
      "sort": [
        {
          "field": "_category",
          "order": "ascending"
        },
        {
          "field": "_period",
          "order": "ascending"
        }
      ]
    },
    {
      "calculate": "datum['_period2_value'] - datum['_period1_value']",
      "as": "_variance_value"
    },
    {
      "calculate": "datum['_variance_value'] / datum['_period1_value']",
      "as": "_variance_percent"
    }
  ],
  "spacing": 8,
  "vconcat": [
    {
      "name": "DIVIDER_1",
      // adjust width as desired to suit visual
      "width": 770,
      "height": 4,
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
        "xOffset": -40,
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
          "datum": -10,
          "axis": null
        },
        "x2": {
          "datum": 0
        }
      }
    },
    {
      "name": "VARIANCE_ANALYSIS",
      "hconcat": [
        {
          "name": "VARIANCE_VALUE",
          // text and position only; formatting done in "config\title"
          "title": {
            "anchor": "end",
            "align": "right",
            "dx": -4,
            "text": "Amount Variance"
          },
          "width": 300,
          "height": 400,
          "transform": [
            {
              "filter": "datum['_period_rank'] == 1"
            }
          ],
          "encoding": {
            "x": {
              "field": "_value",
              "type": "quantitative",
              "axis": {
                "title": null,
                "grid": true,
                "gridColor": "#F0F0F0",
                "tickCount": 5,
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "0,,.0 M"
              },
              "scale": {
                // adjust domain as desired to suit dataset
                "domain": [
                  3000000,
                  5000000
                ]
              }
            },
            "y": {
              "field": "_category",
              "type": "nominal",
              "sort": {
                "field": "_category_id",
                "order": "ascending"
              },
              "axis": null
            }
          },
          "layer": [
            {
              "name": "VARIANCE_AMOUNT_LABEL",
              "mark": {
                "type": "text",
                "align": "right",
                "xOffset": -4,
                "fontWeight": {
                  "expr": "datum['_variance_value'] >= 0 ? 'normal' : 'bold'"
                },
                "style": "_variance_value_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_variance_value",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust Power BI format string as desired to suit dataset
                  "format": "0,,.0 M"
                },
                "x": {
                  "datum": 3000000
                }
              }
            },
            {
              "name": "ARROW",
              "mark": {
                "type": "line",
                "color": {
                  "expr": "datum['_variance_percent'] >= 0 ? pbiColor('positive') : pbiColor('negative')"
                },
                "style": "_arrow_line_style"
              },
              "encoding": {
                "x": {
                  "field": "_period1_value",
                  "type": "quantitative"
                },
                "x2": {
                  "field": "_period2_value"
                }
              }
            },
            {
              "name": "ARROWHEAD_POSITIVE",
              "transform": [
                {
                  "filter": "datum['_variance_value'] >= 0"
                }
              ],
              "mark": {
                "type": "point",
                "shape": "triangle-right",
                "color": {
                  "expr": "datum['_variance_value'] >= 0 ? pbiColor('positive') : pbiColor('negative')"
                },
                "style": "_arrowhead_point_style"
              },
              "encoding": {
                "x": {
                  "field": "_period2_value",
                  "type": "quantitative"
                }
              }
            },
            {
              "name": "ARROWHEAD_NEGATIVE",
              "transform": [
                {
                  "filter": "datum['_variance_value'] < 0"
                }
              ],
              "mark": {
                "type": "point",
                "shape": "triangle-left",
                "color": {
                  "expr": "datum['_variance_value'] >= 0 ? pbiColor('positive') : pbiColor('negative')"
                },
                "style": "_arrowhead_point_style"
              },
              "encoding": {
                "x": {
                  "field": "_period2_value",
                  "type": "quantitative"
                }
              }
            }
          ]
        },
        {
          "name": "Y_AXIS",
          // text and position only; formatting done in "config\title"
          "title": {
            "anchor": "middle",
            "align": "center",
            "text": "__1__"
          },
          // adjust width as desired to suit dataset
          "width": 70,
          "height": 400,
          "transform": [
            {
              "filter": "datum['_period_rank'] == 1"
            }
          ],
          "encoding": {
            "y": {
              "field": "_category",
              "type": "nominal",
              "sort": {
                "field": "_category_id",
                "order": "ascending"
              },
              "axis": null
            }
          },
          "layer": [
            {
              "name": "CATEGORY",
              "mark": {
                "type": "text",
                "style": "_category_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_category",
                  "type": "nominal"
                }
              }
            }
          ]
        },
        {
          "name": "VARIANCE_PERCENT",
          // text and position only; formatting done in "config\title"
          "title": {
            "anchor": "start",
            "align": "left",
            "text": "Percent Variance"
          },
          "width": 300,
          "height": 400,
          "transform": [
            {
              "filter": "datum['_period_rank'] == 1"
            }
          ],
          "encoding": {
            "x": {
              "field": "_variance_percent",
              "type": "quantitative",
              "axis": {
                "title": null,
                "grid": true,
                "gridColor": {
                  "expr": "datum.value == 0 ? '#969696' : '#F0F0F0'"
                },
                "tickCount": 5,
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "0%"
              },
              "scale": {
                // adjust domain as desired to suit dataset
                "domain": [
                  -0.3,
                  0.3
                ]
              }
            },
            "y": {
              "field": "_category",
              "type": "nominal",
              "sort": {
                "field": "_category_id",
                "order": "ascending"
              },
              "axis": null
            }
          },
          "layer": [
            // use separate bar marks for +ve and -ve percents as a workaround to [cornerRadius*] not working properly in Vega-Lite with both +ve and -ve values in the same mark
            {
              "name": "NEGATIVE_BAR",
              "transform": [
                {
                  "filter": "datum['_variance_percent'] < 0"
                }
              ],
              "mark": {
                "type": "bar",
                "height": {
                  "band": 0.2
                },
                "color": {
                  "expr": "pbiColor('negative')"
                },
                "cornerRadiusTopLeft": 4,
                "cornerRadiusBottomLeft": 4
              }
            },
            {
              "name": "POSITIVE_BAR",
              "transform": [
                {
                  "filter": "datum['_variance_percent'] >= 0"
                }
              ],
              "mark": {
                "type": "bar",
                "height": {
                  "band": 0.2
                },
                "color": {
                  "expr": "pbiColor('positive')"
                },
                "cornerRadiusTopRight": 4,
                "cornerRadiusBottomRight": 4
              }
            },
            {
              "name": "VARIANCE_PERCENT_LABEL",
              "mark": {
                "type": "text",
                "align": "right",
                "xOffset": 4,
                "fontWeight": {
                  "expr": "datum['_variance_percent'] >= 0 ? 'normal' : 'bold'"
                },
                "style": "_variance_percent_text_style"
              },
              "encoding": {
                "x": {
                  "datum": 0.38
                },
                "text": {
                  "field": "_variance_percent",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust Power BI format string as desired to suit dataset
                  "format": "0.0%"
                }
              }
            }
          ]
        }
      ]
    },
    {
      "name": "DIVIDER_2",
      // adjust width as desired to suit visual
      "width": 770,
      "height": 4,
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
        "xOffset": -40,
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
          "datum": -10,
          "axis": null
        },
        "x2": {
          "datum": 0
        }
      }
    },
    {
      "name": "LEGEND",
      "width": 670,
      "height": 10,
      // hard-code legend values
      "data": {
        "values": [
          {
            "legend_id": 1,
            "legend_size": 1,
            "legend_label": "Positive Variance"
          },
          {
            "legend_id": 2,
            "legend_size": 1,
            "legend_label": "negative Variance"
          }
        ]
      },
      "mark": {
        "type": "arc",
        // set [radius] to zero to hide the visual and keep only the legend
        "radius": 0
      },
      "encoding": {
        "theta": {
          "field": "legend_size",
          "type": "quantitative"
        },
        "color": {
          "field": "legend_label",
          "type": "nominal",
          "scale": {
            "domain": [
              "Positive Variance",
              "Negative Variance"
            ],
            "range": [
              {
                "expr": "pbiColor('positive')"
              },
              {
                "expr": "pbiColor('negative')"
              }
            ]
          },
          "legend": {
            "orient": "none",
            "direction": "horizontal",
            // adjust X and Y offsets as desired to suit visual
            "legendX": 270,
            "legendY": 470,
            "title": null
          }
        }
      }
    }
  ]
}
```
</details>

<br>

This example illustrates a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block with:
  - an *expression* for the title
  - an *expression* for the subtitle with:
    - *direct data access* to retrieve the 1st and 2nd period values from the dataset
- a standard Power BI dataset
- a ***transform*** block with:
    - 4x ***calculate*** transforms to assign internal names to the dataset fields
    - a ***window/rank*** transform to rank the 2 periods
    - a ***calculate*** transform to determine the period 1 value
    - a ***window/lead*** transform to determine the period 2 value
    - 2x ***calculate*** transforms to determine the variance and percent variance
- a ***vconcat*** block for the (title) divider, variance analysis, (legend) divider, and legend

1 - Divider:
- a ***rule*** mark with:
    - a single-record hard-coded dataset
    - ranged X values to set the starting point and width
    - a *named style*

2 - Variance Analysis:
- a nested ***hconcat*** block for the variance value, category, and variance percent

2a - Variance Value:
- a ***title*** block with right-aligned text
- a ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to only the period 1 records
- a ***shared encoding*** block with:
    - an ***X*** block with:
        - the variance value (quantitative)
        - an ***axis*** block to set the grid colour, tick count, and label formatting using Power BI formatting as enabled by Deneb
        - a ***scale/domain*** block set to cover the extents of the dataset
    - a ***Y*** block with:
        - the category (nominal)
        - a ***sort*** block using the category ID in ascending order
    - a nested ***layer*** block for the variance amount label, variance arrow, and positive and negative arrowheads

2a(1) - Variance Value Label:
- a ***text*** mark with:
    - a hard-coded ***X*** value
    - conditional font weight (positive = normal; negative = bold)
    - ***Power BI formatting*** as enabled by Deneb
    - a *named style*

2a(2) - Variance Arrow:
- a ***line*** mark with:
    - ***ranged*** X and Y values
    - conditional colour using the Power BI Theme sentiment colours
    - a *named style*

2a(3) - Variance Positive Arrowhead:
- a ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to only positive variances
- a ***point/triangle-right*** mark with:
    - conditional colour using the Power BI Theme sentiment colours
    - a *named style*

2a(4) - Variance Negative Arrowhead:
- a ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to only negative variances
- a ***point/triangle-left*** mark with:
    - conditional colour using the Power BI Theme sentiment colours
    - a *named style*

2b - Category:
- a ***title*** block with center-aligned text
- a ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to only the period 1 records
- a ***shared encoding*** block with:
    - a ***Y*** block with:
        - the category (nominal)
        - a ***sort*** block using the category ID in ascending order
    - a nested ***layer*** block for the category (not strictly needed, but included to permit naming of all blocks)
- a ***text*** mark with:
    - a *named style*

2c - Variance Percent:
- a ***title*** block with left-aligned text
- a ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to only the period 1 records
- a ***shared encoding*** block with:
    - an ***X*** block with:
        - the variance percent (quantitative)
        - an ***axis*** block with:
          - conditional gridline colour (dark grey for zero gridline; light grey for all others)
          - a hard-coded tick count
          - label formatting using Power BI formatting as enabled by Deneb
        - a ***scale/domain*** block set to cover the extents of the dataset
    - a ***Y*** block with:
        - the category (nominal)
        - a ***sort*** block using the category ID in ascending order
    - a nested ***layer*** block for the positive variance percents, negative variance percents, and variance percent label

>[!NOTE]
> *Separate bar marks were used for the positive and negative percents as a workaround to the ***cornerRadius*** values not being applied properly in Vega-Lite with both positive and negative values in the same bar mark*

2c(1) - Negative Variance Percent:
- a ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to only the negative variance percents
- a ***bar*** mark with:
    - 20% *band height*
	- the *negative* Power BI Theme sentiment colours as enabled by Deneb
    - fixed values for the top-left and bottom-left *corner rounding*
	- a *named style*

2c(2) - Positive Variance Percent:
- a ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to only the positive variance percents
- a ***bar*** mark with:
    - 20% *band height*
	- the *positive* Power BI Theme sentiment colours as enabled by Deneb
    - fixed values for the top-right and bottom-right *corner rounding*
	- a *named style*

2c(3) - Variance Percent Label:
- a ***text*** mark with:
    - a hard-coded ***X*** value
    - conditional font weight (positive = normal; negative = bold)
    - ***Power BI formatting*** as enabled by Deneb
    - a *named style*

3 - Divider:
- a ***rule*** mark with:
    - a single-record hard-coded dataset
    - ranged X values to set the starting point and width
    - a *named style*

4 - Legend:
- an ***arc*** mark with:
    - a 2-record *hard-coded* dataset
    - a *radius* of zero to leverage *Vega-Lite's automatic legend generation*
    - a *scale/domain/range* block to set the colours to the *Power BI theme sentiment colours* (positive, negative)
    - hard-coded ***X*** and ***Y*** positions to place the legend centred below the visual

5 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
    - title font attributes (family, size, colour)
    - legend font attributes (family, size, colour)
	- ***X*** axis attributes (label font attributes [family, size, colour], grid [disabled], ticks [enabled])
    - ***Y*** axis attributes (label font attributes [family, size, colour], grid [enabled], domain [enabled], ticks [enabled])
    - named styles:
		- divider (colour)
        - arrow line (stroke width, colour)
        - arrowhead point (size, filled, opacity)
        - category text (font family, size, colour)
        - variance value text (font family, size, colour)
        - variance percent text (font family, size, colour)
<hr>

### Links:

Here's the template:

[910.1 - JSON - Deneb Template - Variance Analysis](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/909.1%20-%20deneb_template.regression.v1.8.2.json) *** FIX *** <br>

<br>

Here's an example Power BI file using the template:

[910.2 - PBIX - Deneb Example - Variance Analysis](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/909.2%20-%20Deneb%20Reusable%20Components%20-%20Regression%20-%20V1.8.2.pbix) *** FIX *** <br>

*- eof*
