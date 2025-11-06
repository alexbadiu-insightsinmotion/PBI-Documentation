<img width="1280" height="710" alt="209 - Image - Title - Regression" src="https://github.com/user-attachments/assets/f4f15a95-a662-4634-9eae-b297e0e4dc73" />

## Regression

*October 31, 2025*

Deneb/Vega-Lite can be used to create regression analyses in Power BI. Vega-Lite has 6 regression algorithms built-in: linear, logarithmic, exponential, power, quadratic, and polynomial.

The example presented here is a scatter chart of movie ratings with a overlaid with a linear regression line and regression statistics (r-squared, y coefficient, x coefficient).

I provide a Deneb template for just this scanario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "6e492565-9afb-44de-b7bc-fd8a85738d5d",
      "generated": "2025-10-31T11:30:15.977Z",
      "previewImageBase64PNG": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR42mNkYAAAAAYAAjCB0C8AAAAASUVORK5CYII=",
      "name": "Regression",
      "description": "Linear regression applied to and overlaying a scatter plot of 2 quantitative values. (Vega-Lite has 6 regression algorithms built-in: linear, logarithmic, exponential, power, quadratic, and polynomial.)",
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
    "config": "{\n  \"view\": {\n    \"stroke\": null\n  },\n  \"lineBreak\": \"|\",\n  \"title\": {\n    \"font\": \"Segoe UI\",\n    \"fontSize\": 24,\n    \"fontWeight\": \"bold\",\n    \"fontStyle\": \"italic\",\n    \"color\": \"#4A4A4A\",\n    \"subtitleFont\": \"Segoe UI\",\n    \"subtitleFontSize\": 16,\n    \"subtitleFontWeight\": \"normal\",\n    \"subtitleFontStyle\": \"italic\",\n    \"subtitleColor\": \"#969696\"\n  },\n  \"axisQuantitative\": {\n    \"ticks\": true,\n    \"grid\": true,\n    \"gridColor\": \"#E3E3E3\",\n    \"domain\": true,\n    \"domainColor\": \"#969696\",\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 12,\n    \"labelColor\": \"#707070\",\n    \"titleFont\": \"Segoe UI\",\n    \"titleFontSize\": 16,\n    \"titleColor\": \"#303030\"\n  },\n  \"style\": {\n    \"_divider_rule_style\": {\n      \"color\": \"#969696\"\n    },\n    \"_data_point_style\": {\n      \"shape\": \"diamond\",\n      \"size\": 100,\n      \"filled\": true,\n      \"color\": {\n        \"expr\": \"pbiColor(3)\"\n      }\n    },\n    \"_regression_line_style\": {\n      \"strokeWidth\": 4,\n      \"color\": \"#D64550\"\n    },\n    \"_regression_rsquared_text_style\": {\n      \"align\": \"right\",\n      \"baseline\": \"top\",\n      \"fontSize\": 20,\n      \"fontWeight\": \"bold\",\n      \"fontStyle\": \"italic\",\n      \"color\": \"#D64550\"\n    },\n    \"_regression_coefficient_text_style\": {\n      \"align\": \"right\",\n      // \"baseline\": \"top\",\n      \"fontSize\": 16,\n      \"fontWeight\": \"normal\",\n      \"fontStyle\": \"italic\",\n      \"color\": \"#D64550\"\n    }\n  }\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Item Name",
        "description": "Not necessary for regression analysis; only used for tooltip; included in the dataset to prevent aggregation by Power BI",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__1__",
        "name": "Item Date",
        "description": "Not necessary for regression analysis; only used for tooltip; included in the dataset to prevent aggregation by Power BI",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__2__",
        "name": "Item Quantitative Value 1",
        "description": "To be shown on Y axis",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__3__",
        "name": "Item Quantitative Value 2",
        "description": "To be shown on X axis",
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
    "text": {
      "expr": "'Regression'"
    },
    "subtitle": {
      "expr": "'Movies rated higher by critics also tend to be rated higher by audiences|though the correlation is moderate (R² ~ ' + format( data('data_3')[0]['rSquared'], '.1f' ) + ')'"
    }
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "vconcat": [
    {
      "name": "DIVIDER",
      "width": 530,
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
      "name": "DATA_AND_REGRESSION",
      "width": 520,
      "height": 600,
      // shared encoding outside of [layer] block
      // both axes are same type, so formatting done once in "config\axisQuantitative"
      "encoding": {
        "x": {
          "type": "quantitative",
          "axis": {
            "tickCount": 10,
            // adjust title to suit dataset
            "title": "Rotten Tomatoes Rating (%)"
          }
        },
        "y": {
          "type": "quantitative",
          "axis": {
            "tickCount": 10,
            // adjust title to suit dataset
            "title": "IMDB Rating (0-10)"
          }
        }
      },
      "layer": [
        {
          "name": "SCATTER_CHART_OF_RAW_DATA",
          "mark": {
            "type": "point",
            "tooltip": true,
            "style": "_data_point_style"
          },
          "encoding": {
            "x": {
              "field": "__3__"
            },
            "y": {
              "field": "__2__"
            },
            "tooltip": [
              {
                "field": "__0__",
                "type": "nominal"
              },
              {
                "field": "__1__",
                "type": "temporal",
                // refer to [https://d3js.org/d3-time-format#locale_format]
                // for a full listing of available format specifiers
                "format": "%Y",
                "title": "Release Year"
              },
              {
                "field": "__1__",
                "type": "temporal",
                // refer to [https://d3js.org/d3-time-format#locale_format]
                // for a full listing of available format specifiers
                // (use a minus sign to disable padding)
                "format": "%B %-d"
              },
              {
                "field": "__2__",
                "type": "quantitative"
              },
              {
                "field": "__3__",
                "type": "quantitative"
              }
            ]
          }
        },
        {
          "name": "REGRESSION_LINE",
          "transform": [
            {
              "regression": "__2__",
              "on": "__3__",
              // refer to [https://vega.github.io/vega-lite/docs/regression.html]
              // for a complete listing of the available regression methods:
              // linear, logarithmic, exponential, power, quadratic, polynomial
              "method": "linear"
            }
          ],
          "mark": {
            "type": "line",
            "style": "_regression_line_style"
          },
          "encoding": {
            "x": {
              "field": "__3__",
              "type": "quantitative"
            },
            "y": {
              "field": "__2__",
              "type": "quantitative"
            }
          }
        },
        {
          "name": "REGRESSION_STATISTIC",
          "transform": [
            {
              "regression": "__2__",
              "on": "__3__",
              // refer to [https://vega.github.io/vega-lite/docs/regression.html]
              // for a complete listing of the available regression methods:
              // linear, logarithmic, exponential, power, quadratic, polynomial        
              "method": "linear",
              "params": true
            },
            {
              "calculate": "'Y coefficient: ' + format( datum['coef'][0], '.2f' )",
              "as": "_y_coefficient"
            },
            {
              "calculate": "'X coefficient: ' + format( datum['coef'][1], '.2f' )",
              "as": "_x_coefficient"
            },
            {
              "calculate": "'R²: ' + format( datum['rSquared'], '.2f' )",
              "as": "_r2"
            }
          ],
          "layer": [
            // position of the regression statistics: hard-coded data coordinates:
            // use the "datum" keyword to access the scales alreadt used by Vega-Lite
            {
              "name": "R_SQUARED",
              "mark": {
                "type": "text",
                "xOffset": -4,
                "yOffset": 4,
                "style": "_regression_rsquared_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_r2",
                  "type": "nominal"
                },
                "x": {
                  "datum": 100
                },
                "y": {
                  "datum": 10 // 10 for top-right; 1 for bottom right
                }
              }
            },
            {
              "name": "Y_COEFFICIENT",
              "mark": {
                "type": "text",
                "xOffset": -4,
                "yOffset": 4,
                "style": "_regression_coefficient_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_y_coefficient",
                  "type": "nominal"
                },
                "x": {
                  "datum": 100
                },
                "y": {
                  "datum": 9.5 // 9.5 for top-right; 0.5 for bottom right
                }
              }
            },
            {
              "name": "X_COEFFICIENT",
              "mark": {
                "type": "text",
                "xOffset": -4,
                "yOffset": 4,
                "style": "_regression_coefficient_text_style"
              },
              "encoding": {
                "text": {
                  "field": "_x_coefficient",
                  "type": "nominal"
                },
                "x": {
                  "datum": 100
                },
                "y": {
                  "datum": 9.2 // 9.2 for top-right; 0.2 for bottom right
                }
              }
            }
          ]
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
  - an *expression* for the title
  - an *expression* for the subtitle with:
    - *direct data access* to retrieve the r-squared statistic from the regression analysis
    - a built-in Vega-Lite *format* function to round the r-squared statistic to 1 decimal place
    - a *linebreak* character (|) to render the subtitle text on 2 lines
- a standard Power BI dataset
- a ***vconcat*** block for the divider and data/regression

1 - Divider:
- a ***rule*** mark with:
    - a single-record hard-coded dataset
    - ranged X values to set the starting point and width
    - a *named style*

2 - Data and Regression:
- a ***shared encoding*** block with:
    - ***X axis*** and ***Y axis*** blocks to set the axis type, tick count, and titles for all layered marks
    - a ***color\scale\range*** block with 8 values from the Power BI theme colours
    - a nested ***layer*** block for the scatter chart (raw data), regression line, and regression statistics
 
2a - Scatter Chart:
- a ***point*** mark with:
  - a custom ***tooltip*** with:
    - *title*
    - *release year* (retrieved from the Power BI dataset date field and formatted as year only)
    - *release month and day* (retrieved from the Power BI dataset date field and formatted as month and day [with zero-padding removed])
    - IMDB Rating
    - Rotten Tomatoes rating
  - a *named style*

2b - Regression Line:
- a ***transform*** block with:
    - a ***regression\linear*** transform to calculate the regression line and statistics
- a ***line*** mark
- a *named style*

2c - Regression Statistics:
- a ***transform*** block with:
    - a ***regression\linear*** transform to calculate the regression line and statistics
    - 3x ***calculate*** transforms to format the regression statistics to 2 decimal places
- a nested ***layer*** block for the regression statistics
- 3x ***text*** marks, each with:
  - hard-coded coordinates
  - a *named style*

3 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
    - line break character
    - title (title attributes [family, size, weight, style, colour], subtitle attributes [family, size, weight, style, colour])
	- quantitative axis attributes (title attributes [family, size, colour], label attributes [family, size, colour], grid [enabled, colour], domain [enabled, colour], ticks [enabled])
    - named styles:
		- divider (colour)
        - data point (shape, size, Power BI Theme colour [as enabled by Deneb])
        - regression line (width, colour)
        - regression r-squared statistic (alignment, baseline, font family, size, weight, style, and colour)
        - regression coefficient statistic (alignment, baseline, font family, size, weight, style, and colour)

<hr>

### Links:

Here's the templates:

[909.1 - JSON - Deneb Template - Regression](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/907.1%20-%20deneb_template.performance_quadrants.v1.8.1.json) *** FIX *** <br>

<br>

Here's an example Power BI file using the templates:

[909.2 - PBIX - Deneb Example - Regression](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/907.2%20-%20Deneb%20Reusable%20Components%20-%20Performance%20Quadrants%20-%20V1.8.1.pbix) *** FIX *** <br>

*- eof*
