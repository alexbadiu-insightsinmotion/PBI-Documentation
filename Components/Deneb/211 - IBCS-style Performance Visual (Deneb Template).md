<img width="1280" height="638" alt="211 - Image - Title - IBCS-style Performance Visual" src="https://github.com/user-attachments/assets/286d1080-b502-40c0-925c-019ef0ffb74e" />

## IBCS-style Performance Visual

*November 19, 2025*

Deneb/Vega-Lite can be used to create a composite visual in the IBCS style consisting of separate sections for the variance percent, variance amount, and amount.

The example presented here has ***bar charts*** for the variance percent, variance amount, and overlapping PY and CY amount, along with a top legend; the variance values and percents and the legend use the Power BI theme sentiment colours.

This example uses only the simplest of DAX measures to calculate the current year and previous year sales:
``` dax
Sales CY =
SUMX(
    Sales,
    Sales[Order Quantity] * Sales[Unit Price]
)

Sales PY =
CALCULATE(
    [Sales CY],
    DATEADD( Dates[Date], -1, YEAR )
)
```

I provide a Deneb template for just this scanario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "debb1aee-2c6a-4e91-a8c3-968f51546d2b",
      "generated": "2025-11-19T11:06:48.946Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "IBCS-style Performance Visual",
      "description": "An IBCS-style Performance Visual, with vertically-concatenated sections for a legend, a variance percent column chart, a variance amount column chart, and overlapping column charts for current year amount over previous year amount; the variances and legend use the Power BI theme sentiment colours",
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
      "selection": true,
      "selectionMode": "simple",
      "highlight": true,
      "dataPointLimit": 50
    },
    "config": "{\n  \"view\": {\n    \"stroke\": null\n  },\n  \"lineBreak\": \"[::]\",\n  \"title\": {\n    \"font\": \"Segoe UI\",\n    \"fontSize\": 24,\n    \"fontWeight\": \"bold\",\n    \"fontStyle\": \"italic\",\n    \"color\": \"#4A4A4A\",\n    \"subtitleFont\": \"Segoe UI\",\n    \"subtitleFontSize\": 16,\n    \"subtitleFontWeight\": \"normal\",\n    \"subtitleFontStyle\": \"italic\",\n    \"subtitleColor\": \"#969696\"\n  },\n  \"legend\": {\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 12,\n    \"labelFontStyle\": \"italic\",\n    \"labelColor\": \"#4A4A4A\",\n    \"symbolSize\": 200,\n    \"symbolType\": \"circle\"\n  },\n  \"axis\": {\n    \"ticks\": false,\n    \"grid\": false,\n    \"domain\": false,\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 12,\n    \"labelFontWeight\": \"normal\",\n    \"labelColor\": \"#605E5C\",\n    \"titleFont\": \"Segoe UI\",\n    \"titleFontSize\": 16,\n    \"titleFontWeight\": \"bold\",\n    \"titleColor\": \"#252423\"\n  },\n  \"axisQuantitative\": {\n    \"grid\": true,\n    \"labelFlush\": true\n  },\n  \"axisNominal\": {\n    \"grid\": false,\n    \"labelFlush\": true\n  },\n  \"axisX\": {\n    \"labelPadding\": 5\n  },\n  \"axisY\": {\n    \"labelPadding\": 10\n  },\n  \"style\": {\n    \"_divider_rule_style\": {\n      \"color\": \"#B0B0B0\"\n    },\n    \"_percent_end_symbol_style\": {\n      \"shape\": \"circle\",\n      \"size\": 100,\n      \"filled\": true,\n      \"color\": \"#000000\",\n      \"opacity\": 1\n    },\n    \"_data_label_text_style\": {\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 12,\n      \"color\": \"#1A1A1A\"\n    }\n  }\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Period",
        "description": "(e.g., Year)",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__1__",
        "name": "Category",
        "description": "(e.g., Product)",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__2__",
        "name": "Sales CY",
        "description": "Current Period Amount (e.g., current year sales)",
        "kind": "measure",
        "type": "numeric"
      },
      {
        "key": "__3__",
        "name": "Sales PY",
        "description": "Previous Period Amount (e.g., previous year sales)",
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
    "text": "IBCS-style Performance Visual",
    "subtitle": {
      "expr": "'Sales Revenue in € | Variance to PY | ' + data('data_0')[0]['_number_of_products'] + ' Products ' + '[::]' + 'For period = ' + format( data('dataset')[0]['Year'], '.0f' )"
    }
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "joinaggregate": [
        {
          "op": "count",
          "field": "__1__",
          "as": "_number_of_products"
        }
      ]
    },
    {
      "calculate": "datum['__2__'] - datum['__3__']",
      "as": "_variance_amount"
    },
    {
      "calculate": "datum['_variance_amount'] / datum['__3__']",
      "as": "_variance_percent"
    },
    {
      "calculate": "datum['_variance_amount'] > 100000 ? 100000 : datum['_variance_amount'] < -100000 ? -100000 : datum['_variance_amount']",
      "as": "_threshold_variance_amount"
    },
    {
      "calculate": "datum['_variance_percent'] > 1 ? 1 : datum['_variance_percent'] < -1 ? -1 : datum['_variance_percent']",
      "as": "_threshold_variance_percent"
    }
  ],
  "params": [
    {
      "name": "_py_colour",
      "value": "#C9C9C9"
    },
    {
      "name": "_cy_colour",
      "value": "#969696"
    },
    {
      "name": "_gridline_zero_colour",
      "value": "#000000"
    },
    {
      "name": "_gridline_colour",
      "value": "#E3E3E3"
    },
    {
      "name": "_gridline_zero_width",
      "value": 1.5
    },
    {
      "name": "_gridline_width",
      "value": 1
    }
  ],
  "spacing": 4,
  "vconcat": [
    {
      "name": "DIVIDER",
      // adjust width as desired to suit visual
      "width": 610,
      "height": 20,
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
        "xOffset": -90,
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
      "width": 600,
      "height": 1,
      "data": {
        "values": [
          {
            "legend_id": 1,
            "legend_size": 1,
            "legend_label": "Previous Year"
          },
          {
            "legend_id": 2,
            "legend_size": 1,
            "legend_label": "Current Year"
          },
          {
            "legend_id": 3,
            "legend_size": 1,
            "legend_label": "Positive Variance"
          },
          {
            "legend_id": 4,
            "legend_size": 1,
            "legend_label": "Negative Variance"
          }
        ]
      },
      "mark": {
        "type": "arc",
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
              "Current Year",
              "Previous Year",
              "Positive Variance",
              "Negative Variance"
            ],
            "range": [
              {
                "expr": "_cy_colour"
              },
              {
                "expr": "_py_colour"
              },
              {
                "expr": "pbiColor('positive')"
              },
              {
                "expr": "pbiColor('negative')"
              }
            ]
          },
          "legend": {
            "direction": "horizontal",
            "title": null,
            "offset": 0,
            "orient": "none",
            // position the legend to start at the Y axis titles rather than the X axis zero
            "legendX": -70
          }
        }
      }
    },
    {
      "name": "VARIANCE_PERCENT",
      "width": 600,
      "height": 200,
      "layer": [
        {
          "name": "PERCENT_END_SYMBOL",
          "mark": {
            "type": "point",
            "style": "_percent_end_symbol_style"
          },
          "encoding": {
            "x": {
              "field": "__1__",
              "type": "nominal",
              "axis": null
            },
            "y": {
              "field": "_threshold_variance_percent",
              "type": "quantitative"
            }
          }
        },
        {
          "name": "PERCENT",
          "mark": {
            "type": "bar",
            "tooltip": true,
            "width": {
              "band": 0.05
            },
            "style": "_variance_percent_bar_style"
          },
          "encoding": {
            "x": {
              "field": "__1__",
              "type": "nominal"
            },
            "y": {
              "field": "_threshold_variance_percent",
              "type": "quantitative",
              "scale": {
                "domain": [
                  -1,
                  1
                ]
              },
              "axis": {
                "gridColor": {
                  "expr": "datum.value == 0 ? _gridline_zero_colour : _gridline_colour"
                },
                "gridWidth": {
                  "expr": "datum.value == 0 ? _gridline_zero_width : _gridline_width"
                },
                "title": "Variance Percent",
                // adjust as necessary to align Y axes
                "titlePadding": 10,
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#%"
              }
            },
            "color": {
              "condition": [
                {
                  "test": "datum['_variance_percent'] < 0",
                  "value": {
                    "expr": "pbiColor('negative')"
                  }
                }
              ],
              "value": {
                "expr": "pbiColor('positive')"
              }
            },
            "tooltip": [
              {
                "field": "__1__",
                "type": "nominal"
              },
              {
                "field": "__2__",
                "type": "quantitative",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#,0"
              },
              {
                "field": "__3__",
                "type": "quantitative",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#,0"
              },
              {
                "field": "_variance_amount",
                "type": "quantitative",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#,0",
                "title": "Variance"
              },
              {
                "field": "_variance_percent",
                "type": "quantitative",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#%",
                "title": "Variance %"
              }
            ]
          }
        },
        {
          "name": "PERCENT_LABEL",
          "mark": {
            "type": "text",
            "align": "center",
            "yOffset": {
              "expr": "datum['_variance_percent'] < 0 ? 7 : -5"
            },
            "baseline": {
              "expr": "datum['_variance_percent'] < 0 ? 'top' : 'bottom'"
            },
            "style": "_data_label_text_style"
          },
          "encoding": {
            "text": {
              "field": "_variance_percent",
              "type": "quantitative",
              // // use D3/Vega/Vega-Lite formatting: refer to https://d3js.org/d3-format#d3-format for a list of available format strings
              // "format": "+#.0%"
              "formatType": "pbiFormat",
              // adjust Power BI format string as desired to suit dataset
              "format": "+#%; -#%; #"
            },
            "x": {
              "field": "__1__",
              "type": "nominal"
            },
            "y": {
              "field": "_threshold_variance_percent",
              "type": "quantitative"
            }
          }
        },
        {
          "name": "PERCENT_INDICATOR",
          "mark": {
            "type": "point",
            "shape": {
              "expr": "datum['_variance_percent'] < 0 ? 'triangle-down' : 'triangle-up'"
            },
            "size": 150,
            "yOffset": {
              "expr": "datum['_variance_percent'] < 0 ? 24 : -24"
            }
          },
          "encoding": {
            "x": {
              "field": "__1__",
              "type": "nominal"
            },
            "y": {
              "field": "_threshold_variance_percent",
              "type": "quantitative"
            },
            "color": {
              "condition": [
                {
                  "test": "datum['_variance_percent'] < -1",
                  "value": {
                    "expr": "pbiColor('negative')"
                  }
                },
                {
                  "test": "datum['_variance_percent'] > 1",
                  "value": {
                    "expr": "pbiColor('positive')"
                  }
                }
              ],
              "value": "transparent"
            }
          }
        }
      ]
    },
    {
      "name": "VARIANCE_AMOUNT",
      "width": 600,
      "height": 200,
      "layer": [
        {
          "name": "AMOUNT",
          "mark": {
            "type": "bar",
            "tooltip": true,
            "xOffset": 0,
            "width": {
              "band": 0.2
            }
          },
          "encoding": {
            "x": {
              "field": "__1__",
              "type": "nominal",
              "axis": null
            },
            "y": {
              "field": "_threshold_variance_amount",
              "type": "quantitative",
              "scale": {
                "domain": [
                  -100000,
                  100000
                ]
              },
              "axis": {
                "gridColor": {
                  "expr": "datum.value == 0 ? _gridline_zero_colour : _gridline_colour"
                },
                "gridWidth": {
                  "expr": "datum.value == 0 ? _gridline_zero_width : _gridline_width"
                },
                "title": "Variance Amount",
                // adjust as necessary to align Y axes
                "titlePadding": 10,
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#0,.# K"
              }
            },
            "color": {
              "condition": [
                {
                  "test": "datum['_threshold_variance_amount'] < 0",
                  "value": {
                    "expr": "pbiColor('negative')"
                  }
                }
              ],
              "value": {
                "expr": "pbiColor('positive')"
              }
            },
            "tooltip": [
              {
                "field": "__1__",
                "type": "nominal"
              },
              {
                "field": "__2__",
                "type": "quantitative",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#,0"
              },
              {
                "field": "__3__",
                "type": "quantitative",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#,0"
              },
              {
                "field": "_variance_amount",
                "type": "quantitative",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#,0",
                "title": "Variance"
              },
              {
                "field": "_variance_percent",
                "type": "quantitative",
                "formatType": "pbiFormat",
                // adjust Power BI format string as desired to suit dataset
                "format": "#%",
                "title": "Variance %"
              }
            ]
          }
        },
        {
          "name": "AMOUNT_LABEL",
          "mark": {
            "type": "text",
            "align": "center",
            "yOffset": {
              "expr": "datum['_threshold_variance_amount'] < 0 ? 5 : -3"
            },
            "baseline": {
              "expr": "datum['_threshold_variance_amount'] < 0 ? 'top' : 'bottom'"
            },
            "style": "_data_label_text_style"
          },
          "encoding": {
            "text": {
              "field": "_variance_amount",
              "type": "quantitative",
              // to use signed formtting, use the format string "+,.0f"; for a ful listing of available D3/Vega/Vega-Lite  format strings, refer to https://d3js.org/d3-format#d3-format
              "formatType": "pbiFormat",
              "format": "+#,. K€; -#,. K€; 0"
            },
            "x": {
              "field": "__1__",
              "type": "nominal"
            },
            "y": {
              "field": "_threshold_variance_amount",
              "type": "quantitative"
            }
          }
        },
        {
          "name": "AMOUNT_INDICATOR",
          "mark": {
            "type": "point",
            "filled": true,
            "opacity": 1,
            "shape": {
              "expr": "datum['_threshold_variance_amount'] < 0 ? 'triangle-down' : 'triangle-up'"
            },
            "size": 150,
            "yOffset": {
              "expr": "datum['_threshold_variance_amount'] < 0 ? 24 : -24"
            }
          },
          "encoding": {
            "x": {
              "field": "__1__",
              "type": "nominal"
            },
            "y": {
              "field": "_threshold_variance_amount",
              "type": "quantitative"
            },
            "color": {
              "condition": [
                {
                  "test": "datum['_variance_amount'] < -100000",
                  "value": {
                    "expr": "pbiColor('negative')"
                  }
                },
                {
                  "test": "datum['_variance_amount'] > 100000",
                  "value": {
                    "expr": "pbiColor('positive')"
                  }
                }
              ],
              "value": "transparent"
            }
          }
        }
      ]
    },
    {
      "name": "OVERLAPPING_COLUMN_CHART",
      "width": 600,
      "height": 280,
      "encoding": {
        "x": {
          "field": "__1__",
          "type": "nominal",
          "axis": {
            "labelAngle": 0,
            "labelPadding": 10,
            // use the "linebreak" character from the "config\lineBreak" to split the words onto different lines
            "labelExpr": "replace( datum.value, ' ', '[::]')",
            "titlePadding": 4
          }
        },
        "y": {
          "type": "quantitative",
          "axis": {
            "gridColor": {
              "expr": "datum.value == 0 ? _gridline_zero_colour : _gridline_colour"
            },
            "gridWidth": {
              "expr": "datum.value == 0 ? _gridline_zero_width : _gridline_width"
            },
            "tickCount": 4,
            "title": "Amount",
            // adjust as necessary to align Y axes
            "titlePadding": 16,
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#0,,.# M"
          }
        },
        "tooltip": [
          {
            "field": "__1__",
            "type": "nominal"
          },
          {
            "field": "__2__",
            "type": "quantitative",
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#,0"
          },
          {
            "field": "__3__",
            "type": "quantitative",
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#,0"
          },
          {
            "field": "_variance_amount",
            "type": "quantitative",
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#,0",
            "title": "Variance"
          },
          {
            "field": "_variance_percent",
            "type": "quantitative",
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#%",
            "title": "Variance %"
          }
        ]
      },
      "layer": [
        {
          "name": "PREVIOUS_YEAR",
          "mark": {
            "type": "bar",
            "tooltip": true,
            "xOffset": 0,
            "width": {
              "band": 0.5
            },
            "color": {
              "expr": "_py_colour"
            }
          },
          "encoding": {
            "y": {
              "field": "__3__"
            }
          }
        },
        {
          "name": "CURRENT_YEAR",
          "mark": {
            "type": "bar",
            "tooltip": true,
            "xOffset": 20,
            "width": {
              "band": 0.5
            },
            "color": {
              "expr": "_cy_colour"
            }
          },
          "encoding": {
            "y": {
              "field": "__2__"
            }
          }
        },
        {
          "name": "CY_LABEL",
          "mark": {
            "type": "text",
            "align": "left",
            "yOffset": -10,
            "style": "_data_label_text_style"
          },
          "encoding": {
            "text": {
              "field": "__2__",
              "type": "quantitative",
              "formatType": "pbiFormat",
              // adjust Power BI format string as desired to suit dataset
              "format": "#0,,.0 M€"
              // "format": "#,0"
            },
            "x": {
              "field": "__1__",
              "type": "nominal"
            },
            "y": {
              "field": "__2__",
              "type": "quantitative",
              "aggregate": "sum"
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

This example illustrates a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block with:
  - an *expression* for the subtitle with:
    - *direct data access* to retrieve the number of categories (products) and current year provided in the Power BI dataset
    - *multi-line* presentation using a custom linebreak character string ([::])
- a standard Power BI dataset
- a ***transform*** block with:
    - a ***joinaggregate/count*** transform to determine the number of products
    - 2x ***calculate*** transforms to determine the variance amount and variance percent
    - 2x ***calculate*** transforms to determine the threshold variance amount and threshold variance percent
- a ***params*** block with:
    - 2x ***value*** parameters for the current year and previous year colours
    - 2x ***value*** parameters for the gridline and gridline zero colours
    - 2x ***value*** parameters for the gridline and gridline zero widths
- a ***vconcat*** block for the divider, legend, variance percent, variance amount, and overlapping amount sections 

1 - Divider:
- a ***rule*** mark with:
    - a single-record hard-coded dataset
    - ranged X values to set the starting point and width
    - a *named style*

2 - Legend:
- an ***arc*** mark with:
    - a four-record hard-coded dataset
    - a ***radius*** or zero to hide the visual and show only the legend
    - a ****scale/domain/range*** block in the ***color*** block to apply the CY and PY parameter colours to the amounts and Power BI theme sentiment colours to the positive and negative variance amounts and variance percents

3 - Variance Percent
- a ***layer*** block for the end symbol, (up to threshold) variance percent column, variance percent label, and variance percent (above threshold) indicator

3a - Variance Percent End Symbol:
- a ***point*** mark with:
    - a ***named style*** with:
        - shape=circle
        - size=100
        - colour=black

3b - Variance Percent Column:
- a ***bar*** mark with:
    - 5% band width
    - uses the threshold variance percent (if > +100% then +100%, if <-100% then -100%, else variance percent)
    - ***Y axis*** with:
        - a ***scale/domain*** block to set the scale to -100% to +100%
		- ***label formatting*** via a Power BI format string as enabled by Deneb
        - ***conditional gridline colour*** (zero=black, others=#E3E3E3)
        - ***conditional gridline width*** (zero=1.5, others=1)
        - ***padding*** to adjust the title alignment to match the other sections in this composite visual
	- ***conditional colour*** using the Power BI theme sentiment colours (positive=positive, negative=negative)
    - a custom ***tooltip*** including the product and all 4 data values (CY amount, PY amount, variance amount, variance percent); data values formatted using Power BI format strings as enabled by Deneb

3c - Variance Percent Label:
- a ***text*** mark with:
    - ***conditional Y offset*** (positive=-5 px, negative=+7 px)
    - ***conditional baseline*** (positive=bottom, negative=top)
    - a common ***named style*** (font family, size, and colour) so the data labels in all sections in this composite visual look the same
    - signed formatted using 3-part Power BI format strings as enabled by Deneb ("+#%; -#%; #")

3d - Variance Percent Indicator:
- a ***point*** mark with:
    - ***conditional shape*** (positive=triangle-up, negative=triangle-down)
    - ***conditional Y offset*** (positive=-24 px, negative=+24px)
	- ***conditional colour*** using the Power BI theme sentiment colours (>100%=positive, <-100%=negative, else transparent)

4 - Variance Amount
- a ***layer*** block for the (up to threshold) variance amount column, variance amount label, and variance amount (above threshold) indicator

4a - Variance Amount Column:
- a ***bar*** mark with:
    - 20% band width
    - uses the threshold variance amount (if > +100000 then +100000, if <-100000 then -100000, else variance amount)
    - ***Y axis*** with:
        - a ***scale/domain*** block to set the scale to -100000 to +100000
		- ***label formatting*** via a Power BI format string as enabled by Deneb
        - ***conditional gridline colour*** (zero=black, others=#E3E3E3)
        - ***conditional gridline width*** (zero=1.5, others=1)
        - ***padding*** to adjust the title alignment to match the other sections in this composite visual
	- ***conditional colour*** using the Power BI theme sentiment colours (positive=positive, negative=negative)
    - a custom ***tooltip*** including the product and all 4 data values (CY amount, PY amount, variance amount, variance percent); data values formatted using Power BI format strings as enabled by Deneb

4b - Variance Amount Label:
- a ***text*** mark with:
    - ***conditional Y offset*** (positive=-3 px, negative=+5 px)
    - ***conditional baseline*** (positive=bottom, negative=top)
    - a common ***named style*** (font family, size, and colour) so the data labels in all sections in this composite visual look the same
    - signed formatted using 3-part Power BI format strings as enabled by Deneb ("+#,. K€; -#,. K€; 0")

4c - Variance Amount Indicator:
- a ***point*** mark with:
    - ***conditional shape*** (positive=triangle-up, negative=triangle-down)
    - ***conditional Y offset*** (positive=-24 px, negative=+24px)
	- ***conditional colour*** using the Power BI theme sentiment colours (>100000=positive, <-100000=negative, else transparent)

5 - Column Chart:
- a ***shared encoding*** block (to ensure the same X and Y scales are used by all layered objects) with:
    - ***X-axis*** with:
        - *multi-line* presentation using a custom linebreak character string ([::])
    - ***Y-axis*** with:
        - ***label formatting*** via a Power BI format string as enabled by Deneb 
        - ***conditional gridline colour*** (zero=black, others=#E3E3E3)
        - ***conditional gridline width*** (zero=1.5, others=1)
        - ***padding*** to adjust the title alignment to match the other sections in this composite visual
        - a custom ***tooltip*** including the product and all 4 data values (CY amount, PY amount, variance amount, variance percent); data values formatted using Power BI format strings as enabled by Deneb

5a - Previous Year Column:
- a ***bar*** mark with:
    - zero ***offset***
    - 50% ***band width***
    - the PY colour set in the parameters section above

5b - Current Year Column:
- a ***bar*** mark with:
    - 20 px ***offset***
    - 50% ***band width***
    - the CY colour set in the parameters section above

5c - Current Year Label:
- a ***text*** mark with:
    - ***label formatting*** via a Power BI format string as enabled by Deneb 
	- a ***named style***

6 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
    - line break character string ([::])
    - title font attributes (family, size, weight, style, colour [for each of title and subtitle])
    - legend font attributes (family, size, colour)
    - legend symbol attributes (type, size)
    - general ***axis*** label font attributes (family, size, weight, colour)
    - general ***axis*** title font attributes (family, size, weight, colour)
    - ***X*** axis (nominal) attributes (grid [disabled], flush end labels [enabled], label padding)
    - ***Y*** axis (quantitative) attributes (grid [enabled], flush end labels [enabled], label padding)
    - named styles:
		- divider (colour)
        - percent end symbol (shape, size, filled, colour, opacity)
        - data label text (font family, size, colour)

<hr>

### Links:

Here's the template:

[911.1 - JSON - Deneb Template - IBCS-style Performance Visual](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/911.1%20-%20deneb_template.ibcs-style_performance_visual.v1.8.2.json) <br>

<br>

Here's an example Power BI file using the template:

[911.2 - PBIX - Deneb Example - IBCS-style Performance Visual](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/911.2%20-%20Deneb%20Reusable%20Components%20-%20IBCS-style%20Performance%20Visual%20-%20V1.8.2.pbix) <br>

*- eof*
