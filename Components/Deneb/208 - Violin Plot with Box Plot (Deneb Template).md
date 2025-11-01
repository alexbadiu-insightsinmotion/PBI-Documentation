<img width="1280" height="710" alt="208 - Image - Title - Violin Plot with Box Plot" src="https://github.com/user-attachments/assets/6bfbcdcd-b384-499e-a585-8fa26d62e9f7" />

## Violin Plot with Box Plot

*October 27, 2025*

Deneb/Vega-Lite can be used to display statistical analyses of Power BI datasets via ***Violin Plots*** and ***Box Plots***. 
- a *Violin Plot* displays the probability density of a value smoothed by Kernal Density Estimation (KDE; higher densities are shown as wider, and lower densities are shown as narrower)
- a *Box Plot* displays various probability statistics (in this case, the minimum, the first quartile [25th percentile], the second quartile [50th percentile, or median], the third quartile [75th percentile], and the maximum).

The example presented here is a statistical distribution of value by group (e.g., sales by country), with a *Violin Plot* overlaid by a *Box Plot*.

I provide a Deneb template for just this senario. 


<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "84b3a290-16a6-46ad-b91d-5846ac6b6e34",
      "generated": "2025-10-27T10:26:21.005Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Violin Plot with Box Plot",
      "description": "A composite visual to display statistical distribution of value by group:\n- Violin Plot: Kernel Density Estimation (KDE)-smoothed probability density by value\n- Box Plot: population statistics (median, 1st & 3rd quartiles, min & max)",
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
    "config": "{\n  \"autosize\": {\n    \"type\": \"fit\",\n    \"resize\": true,\n    \"contains\": \"padding\"\n  },\n  \"view\": {\n    \"stroke\": null\n  },\n  \"title\": {\n    \"font\": \"Segoe UI\",\n    \"fontSize\": 24,\n    \"fontWeight\": \"bold\",\n    \"fontStyle\": \"italic\",\n    \"color\": \"#4A4A4A\",\n    \"subtitleFont\": \"Segoe UI\",\n    \"subtitleFontSize\": 16,\n    \"subtitleFontWeight\": \"normal\",\n    \"subtitleFontStyle\": \"italic\",\n    \"subtitleColor\": \"#969696\"\n  },\n  // the settings for the facet \"header\" (i.e., the category)\n  \"header\": {\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 18,\n    \"labelColor\": \"#1A1A1A\"\n  },\n  \"axisX\": {\n    // don't want labels as facet headers suffice\n    \"labels\": false,\n    \"grid\": false,\n    \"ticks\": false\n  },\n  \"axisY\": {\n    \"ticks\": true,\n    \"grid\": true,\n    \"domain\": true,\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 14,\n    \"labelColor\": \"#1A1A1A\"\n  },\n  \"style\": {\n    \"_divider_rule_style\": {\n      \"color\": \"#969696\"\n    }\n  }\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Category",
        "description": "The category of the transaction value",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__1__",
        "name": "Transaction Date",
        "description": "Not used, but included in the dataset to prevent aggregation by Power BI",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__2__",
        "name": "Transaction Number",
        "description": "Not used, but included in the dataset to prevent aggregation by Power BI",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__3__",
        "name": "Category Value",
        "description": "The value of the transaction for the category",
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
    "text": "Violin Plot with Box Plot",
    "subtitle": [
      "Statistical Distribution of Value by Group (e.g., Sales by Country)",
      "Violin Plot - displays smoothed probability density (higher=wider, lower=narrower)",
      "Box Plot - displays probability statistics (median, 1st & 3rd quartiles, min & max)"
    ]
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "spacing": 10,
  "vconcat": [
    {
      "name": "DIVIDER",
      "width": 510,
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
        "xOffset": -60,
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
          "datum": 50
        }
      }
    },
    {
      "name": "VIOLIN",
      "facet": {
        "column": {
          "field": "_category",
          // facet header - orientation and position only (attributes set in config\header)
          "header": {
            "orient": "bottom",
            "title": null
          }
        }
      },
      "spec": {
        "width": 105,
        "height": 600,
        "transform": [
          // assign internal names to dataset fields
          {
            "calculate": "datum['__0__']",
            "as": "_category"
          },
          {
            "calculate": "datum['__3__']",
            "as": "_value"
          }
        ],
        "encoding": {
          "y": {
            "type": "quantitative",
            "title": null,
            "axis": {
              "tickCount": 10
            }
          },
          "x": {
            "type": "quantitative",
            "axis": {
              "title": null
            }
          },
          "color": {
            "field": "_category",
            "type": "nominal",
            "legend": null,
            "scale": {
              "range": [
                {
                  "expr": "pbiColor(0)"
                },
                {
                  "expr": "pbiColor(1)"
                },
                {
                  "expr": "pbiColor(2)"
                },
                {
                  "expr": "pbiColor(3)"
                },
                {
                  "expr": "pbiColor(4)"
                },
                {
                  "expr": "pbiColor(5)"
                },
                {
                  "expr": "pbiColor(6)"
                },
                {
                  "expr": "pbiColor(7)"
                }
              ]
            }
          }
        },
        "layer": [
          {
            "name": "KDE_PLOT",
            "transform": [
              {
                "density": "_value",
                "groupby": [
                  "_category"
                ],
                "extent": [
                  0,
                  100000
                ],
                "as": [
                  "_kde_value",
                  "_kde_density"
                ]
              },
              {
                "calculate": "datum['_kde_density'] * -1",
                "as": "_negative_kde_density"
              }
            ],
            "layer": [
              {
                "name": "KDE_POSITIVE",
                "mark": {
                  "type": "area",
                  "orient": "vertical",
                  "opacity": 0.5
                },
                "encoding": {
                  "y": {
                    "field": "_kde_value"
                  },
                  "x": {
                    "field": "_kde_density"
                  }
                }
              },
              {
                "name": "KDE_NEGATIVE",
                "mark": {
                  "type": "area",
                  "orient": "vertical",
                  "opacity": 0.5
                },
                "encoding": {
                  "y": {
                    "field": "_kde_value"
                  },
                  "x": {
                    "field": "_negative_kde_density"
                  }
                }
              }
            ],
            "encoding": {
              "x2": {
                "datum": 0
              }
            }
          },
          {
            "name": "BOX_PLOT",
            // for boxplot mark properties, refer to the Vega-Lite documentation:
            // https://vega.github.io/vega-lite/docs/boxplot.html#properties
            "mark": {
              "type": "boxplot",
              "extent": "min-max", // [min-max] or number representing interquartile range (default = 1.5)
              "median": {
                "color": "black",
                "strokeWidth": 2
              },
              "size": 20
            },
            "encoding": {
              "y": {
                "field": "_value"
              },
              "fill": {
                "value": "#969696"
              },
              "stroke": {
                "value": "black"
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

<br>

<br>

The template displays a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block with multi-line ***subtitle*** array
- a standard Power BI dataset
- a ***vconcat*** block for the divider and violin plot

1 - Divider:
- a ***rule*** mark with:
    - a single-record hard-coded dataset
    - ranged X values to set the starting point and width
    - a named style

2 - Violin Plot with Box Plot:
- a ***facet*** block (by Country) with bottom headers
- 1 ***spec*** block with:
    - a ***transform*** block with:
	  - 2x ***calculate*** transforms to assign internal names to the dataset fields
- a ***shared encoding*** block with:
    - ***X axis*** and ***Y axis*** blocks to ensure the same axis scales and properties are used for all layered marks
    - a ***color\scale\range*** block with 8 values from the Power BI theme colours
- a ***layer*** block for the violin plot and the box plot

2a - Violin Plot:
- a ***transform*** block with:
    - a ***Kernal Density Estimation*** transform to calculate the KDE value and density
    - a ***calculate*** transform to determine the negative KDE density
- a nested ***layer*** block with 2x ***area*** marks for the positive and negative KDE plots

2b - Box Plot:
- a ***boxplot*** mark with:
    - "min-max" ***extent***
    - dark grey ***fill*** colour
    - black ***median*** and ***stroke*** colour
    - *(tooltip showing all boxplot statistics [max, Q3, median, Q1, min] automatically-generated by Vega-Lite)*

3 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
    - title (title attributes [family, size, weight, style, colour], subtitle attributes [family, size, weight, style, colour])
    - facet header (label attributes [family, size, colour])
	- X axis (labels [disabled], grid [disabled], ticks [disabled])
    - Y axis (label attributes [family, size, colour], grid [enabled], domain [enabled], ticks [enabled])
    - named styles:
		- divider (colour)

<hr>

### Links:

Here's the templates:

[908.1 - JSON - Deneb Template - Violin Plot with Box Plot](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/908.1%20-%20deneb_template.violin_plot_with_box_plot.v1.8.2.json) <br>

<br>

Here's an example Power BI file using the templates:

[908.2 - PBIX - Deneb Example - Violin Plot with Box Plot](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/908.2%20-%20Deneb%20Reusable%20Components%20-%20Violin%20Plot%20with%20Box%20Plot%20-%20V1.8.2.pbix) <br>

*- eof*
