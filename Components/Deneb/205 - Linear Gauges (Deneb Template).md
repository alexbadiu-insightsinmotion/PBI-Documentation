<img width="1280" height="710" alt="205 - Image - Title - Linear Gauges" src="https://github.com/user-attachments/assets/25cc9a90-2af2-4fc7-9f6c-73cf0ae6a4c8" />

## Linear Gauges

*October 9, 2025*

The native Power BI native gauge visual takes-up significant screen real estate and has a lot of whitespace. Deneb/Vega-Lite enables many possibilities for alternative ***linear gauges*** that have less whitespace and have more sizing options. I provide 3 Deneb templates for options for a linear gauge using columnar bar marks. 

<br>

<details closed>
<summary>Here's the template JSON code for option 1:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "b850749f-94c8-49fb-923f-4d1d29b2796f",
      "generated": "2025-10-06T17:33:00.775Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Linear Gauge - Option 1 - Units (with performance zones and pointer)",
      "description": "[No Description Provided]",
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
    "config": "{\n  \"autosize\": {\n    \"type\": \"fit\",\n    \"resize\": true,\n    \"contains\": \"padding\"\n  },\n  \"view\": {\n    \"stroke\": null\n  },\n  \"axisX\": {\n    \"ticks\": false,\n    \"grid\": false,\n    \"domain\": true,\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 16,\n    \"tickOffset\": -4\n  },\n  \"title\": {\n    \"font\": \"Segoe UI\",\n    \"fontSize\": 14,\n    \"fontWeight\": \"bold\",\n    \"fontStyle\": \"italic\",\n    \"color\": \"#4A4A4A\",\n    \"subtitleFont\": \"Segoe UI\",\n    \"subtitleFontSize\": 14,\n    \"subtitleFontWeight\": \"normal\",\n    \"subtitleFontStyle\": \"italic\",\n    \"subtitleColor\": \"#969696\"\n  },\n  \"style\": {\n    \"_divider_rule_style\": {\n      \"color\": \"#969696\"\n    },\n    \"_column_chart_style\": {\n      \"cornerRadius\": 10,\n      \"stroke\": \"white\"\n    },\n    \"_rule_style\": {\n      \"color\": \"#969696\"\n    },\n    \"_symbol_style\": {\n      \"color\": {\n        \"expr\": \"pbiColor(0)\"\n      },\n      \"filled\": true\n    },\n    \"_symbol_label_style\": {\n      \"fontSize\": 12,\n      \"color\": \"black\",\n      \"baseline\": \"top\"\n    },\n    \"_segment_label_style\": {\n      \"fontSize\": 16,\n      \"color\": \"#969696\"\n    }\n  }\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Percentage",
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
    "text": "Option 1 - Units (with performance zones and pointer)"
  },
  // multiple datasets
  "data": {
    // dataset (for X-axis - hard-coded - 100 records)
    "sequence": {
      "start": 1,
      "stop": 101,
      "step": 1,
      "as": "_x2"
    },
    // dataset (for Percentage - from Power BI - 1 record)
    "name": "dataset"
  },
  "params": [
    {
      "name": "_segment_0",
      "value": 0
    },
    {
      "name": "_segment_1",
      "value": 33
    },
    {
      "name": "_segment_2",
      "value": 66
    },
    {
      "name": "_segment_3",
      "value": 100
    },
    {
      "name": "_segment_1_mid",
      "expr": "_segment_0 + floor( ( _segment_1 - _segment_0 ) / 2 )"
    },
    {
      "name": "_segment_2_mid",
      "expr": "_segment_1 + floor( ( _segment_2 - _segment_1 ) / 2 )"
    },
    {
      "name": "_segment_3_mid",
      "expr": "_segment_2 + floor( ( _segment_3 - _segment_2 ) / 2 )"
    }
  ],
  "transform": [
    {
      // compose composite dataset
      "lookup": "_threshold",
      "from": {
        "data": {
          "name": "dataset"
        },
        "key": "_x2",
        "fields": [
          "__0__"
        ]
      }
    },
    {
      "calculate": "datum['_x2'] - 1",
      "as": "_x1"
    },
    {
      "calculate": "datum['_x1'] <= _segment_1 ? 'Low' : datum['_x1'] <= _segment_2 ? 'Medium' : datum['_x1'] <= _segment_3 ? 'High' : ''",
      "as": "_segment_label"
    }
  ],
  // set to zero to eliminate vertical whitespace between concatenated visuals
  "spacing": 0,
  "vconcat": [
    {
      "name": "DIVIDER",
      "width": 540,
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
      "name": "LINEAR_GAUGE",
      "width": 540,
      "height": 80,
      "encoding": {
        "y": {
          "axis": null
        }
      },
      "layer": [
        {
          "name": "GAUGE",
          "mark": {
            "type": "bar",
            "style": "_column_chart_style"
          },
          "encoding": {
            "x": {
              "field": "_x1",
              "type": "quantitative",
              "axis": {
                "title": null,
                "domain": false,
                "labels": false
              }
            },
            "x2": {
              "field": "_x2"
            },
            "y": {
              "datum": 0
            },
            "y2": {
              "datum": 10
            },
            "fill": {
              "condition": [
                {
                  "test": "datum['_x2'] <= 33",
                  "value": {
                    "expr": "pbiColor(7)"
                  }
                },
                {
                  "test": "datum['_x2'] <= 66",
                  "value": {
                    "expr": "pbiColor(5)"
                  }
                },
                {
                  "test": "datum['_x2'] <= 100",
                  "value": {
                    "expr": "pbiColor(3)"
                  }
                }
              ],
              "value": "transparent"
            }
          }
        },
        // {
        //   "name": "RULE",
        //   "mark": {
        //     "type": "rule",
        //     "style": "_rule_style"
        //   },
        //   "encoding": {
        //     "y": {
        //       "datum": 11.5
        //     }
        //   }
        // },
        {
          "name": "SEGMENT_LABELS",
          "transform": [
            {
              "filter": "( datum['_x1'] == _segment_1_mid ) || ( datum['_x1'] == _segment_2_mid ) || ( datum['_x1'] == _segment_3_mid )"
            }
          ],
          "mark": {
            "type": "text",
            "baseline": "bottom",
            "style": "_segment_label_style"
          },
          "encoding": {
            "text": {
              "field": "_segment_label",
              "type": "nominal"
            },
            "x": {
              "field": "_x1",
              "type": "quantitative",
              "axis": {
                "title": null,
                "domain": false,
                "labels": false
              }
            },
            "y": {
              "datum": 10.5
            }
          }
        },
        {
          "name": "PERCENT_SYMBOL",
          "mark": {
            "type": "point",
            "shape": "triangle-down",
            "size": 600,
            "xOffset": -6,
            "yOffset": -10,
            "style": "_symbol_style"
          },
          "encoding": {
            "x": {
              "field": "__0__",
              "type": "quantitative",
              "axis": null
            },
            "y": {
              "datum": 8
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

<details closed>
<summary>Here's the template JSON code for option 2:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "5b98ac59-f131-493f-a5be-3daf0a44cfcf",
      "generated": "2025-10-06T17:33:01.331Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Linear Gauge - Option 2 - Units (with performance zones)",
      "description": "[No Description Provided]",
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
    "config": "{\n  \"autosize\": {\n    \"type\": \"fit\",\n    \"resize\": true,\n    \"contains\": \"padding\"\n  },\n  \"view\": {\n    \"stroke\": null\n  },\n  \"axisX\": {\n    \"ticks\": false,\n    \"grid\": false,\n    \"domain\": true,\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 16,\n    \"tickOffset\": -4\n  },\n  \"title\": {\n    \"font\": \"Segoe UI\",\n    \"fontSize\": 14,\n    \"fontWeight\": \"bold\",\n    \"fontStyle\": \"italic\",\n    \"color\": \"#4A4A4A\",\n    \"subtitleFont\": \"Segoe UI\",\n    \"subtitleFontSize\": 14,\n    \"subtitleFontWeight\": \"normal\",\n    \"subtitleFontStyle\": \"italic\",\n    \"subtitleColor\": \"#969696\"\n  },\n  \"style\": {\n    \"_divider_rule_style\": {\n      \"color\": \"#969696\"\n    },\n    \"_column_chart_style\": {\n      \"cornerRadius\": 10,\n      \"stroke\": \"white\"\n    }\n  }\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Percentage",
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
    "text": "Option 2 - Units (with performance zones)"
  },
  // multiple datasets
  "data": {
    // dataset (for X-axis - hard-coded - 100 records)
    "sequence": {
      "start": 1,
      "stop": 101,
      "step": 1,
      "as": "_x2"
    },
    // dataset (for Percentage - from Power BI - 1 record)
    "name": "dataset"
  },
  "transform": [
    {
      // compose composite dataset
      "lookup": "_threshold",
      "from": {
        "data": {
          "name": "dataset"
        },
        "key": "_x2",
        "fields": [
          "__0__"
        ]
      }
    },
    {
      "calculate": "datum['_x2'] - 1",
      "as": "_x1"
    }
  ],
  // set to zero to eliminate vertical whitespace between concatenated visuals
  "spacing": 0,
  "vconcat": [
    {
      "name": "DIVIDER",
      "width": 540,
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
      "name": "BARS_AND_PERFORMANCE_ZONES",
      "width": 540,
      "height": 70,
      "encoding": {
        "x": {
          "field": "_x1",
          "type": "quantitative",
          "axis": {
            "title": null,
            "values": [
              20,
              40,
              60,
              80
            ]
          }
        },
        "x2": {
          "field": "_x2"
        },
        "y": {
          "axis": null
        }
      },
      "layer": [
        {
          "name": "PERFORMANCE_ZONES",
          "mark": {
            "type": "bar",
            "style": "_column_chart_style"
          },
          "encoding": {
            "y": {
              "datum": 1.4
            },
            "y2": {
              "datum": 2
            },
            "fill": {
              "condition": [
                {
                  "test": "datum['_x2'] <= 33",
                  "value": "#F1948A"
                },
                {
                  "test": "datum['_x2'] <= 66",
                  "value": "#F7DC6F"
                },
                {
                  "test": "datum['_x2'] <= 100",
                  "value": "#82E0AA"
                }
              ],
              "value": "transparent"
            }
          }
        },
        {
          "name": "GAUGE_BARS",
          "mark": {
            "type": "bar",
            "style": "_column_chart_style"
          },
          "encoding": {
            "y": {
              "datum": 0
            },
            "y2": {
              "datum": 1.5
            },
            "fill": {
              "condition": [
                // if <= Percentage --> Power BI theme colour 3
                {
                  "test": "datum['_x2'] <= datum['__0__']",
                  "value": {
                    "expr": "pbiColor(2)"
                  }
                },
                // if evenly divisible by 20 --> dark grey
                {
                  "test": "datum['_x2'] % 20 == 0",
                  "value": "#C9C9C9"
                }
              ],
              // otherwise --> light grey
              "value": "#E3E3E3"
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
<details closed>
<summary>Here's the template JSON code for option 3:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "c68ed757-1e9f-4be6-8c48-3ba7579d4768",
      "generated": "2025-10-06T17:33:01.765Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Linear Gauge - Option 3 - Units (basic)",
      "description": "[No Description Provided]",
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
    "config": "{\n  \"autosize\": {\n    \"type\": \"fit\",\n    \"resize\": true,\n    \"contains\": \"padding\"\n  },\n  \"view\": {\n    \"stroke\": null\n  },\n  \"axisX\": {\n    \"ticks\": false,\n    \"grid\": false,\n    \"domain\": true,\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 16,\n    \"tickOffset\": -4\n  },\n  \"title\": {\n    \"font\": \"Segoe UI\",\n    \"fontSize\": 14,\n    \"fontWeight\": \"bold\",\n    \"fontStyle\": \"italic\",\n    \"color\": \"#4A4A4A\",\n    \"subtitleFont\": \"Segoe UI\",\n    \"subtitleFontSize\": 14,\n    \"subtitleFontWeight\": \"normal\",\n    \"subtitleFontStyle\": \"italic\",\n    \"subtitleColor\": \"#969696\"\n  },\n  \"style\": {\n    \"_divider_rule_style\": {\n      \"color\": \"#969696\"\n    },\n    \"_column_chart_style\": {\n      \"cornerRadius\": 10,\n      \"stroke\": \"white\"\n    }\n  }\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Percentage",
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
    "text": "Option 3 - Units (basic)"
  },
  // multiple datasets
  "data": {
    // dataset (for X-axis - hard-coded - 100 records)
    "sequence": {
      "start": 1,
      "stop": 101,
      "step": 1,
      "as": "_x2"
    },
    // dataset (for Percentage - from Power BI - 1 record)
    "name": "dataset"
  },
  "transform": [
    {
      // compose composite dataset
      "lookup": "_threshold",
      "from": {
        "data": {
          "name": "dataset"
        },
        "key": "_x2",
        "fields": [
          "__0__"
        ]
      }
    },
    {
      "calculate": "datum['_x2'] - 1",
      "as": "_x1"
    }
  ],
  // set to zero to eliminate vertical whitespace between concatenated visuals
  "spacing": 0,
  "vconcat": [
    {
      "name": "DIVIDER",
      "width": 540,
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
      "name": "LINEAR_GAUGE",
      "width": 540,
      "height": 70,
      "mark": {
        "type": "bar",
        "style": "_column_chart_style"
      },
      "encoding": {
        "x": {
          "field": "_x1",
          "type": "quantitative",
          "axis": {
            "title": null,
            "values": [
              20,
              40,
              60,
              80
            ]
          }
        },
        "x2": {
          "field": "_x2"
        },
        "fill": {
          "condition": [
            // if <= Percentage --> Power BI theme colour 3
            {
              "test": "datum['_x2'] <= datum['__0__']",
              "value": {
                "expr": "pbiColor(2)"
              }
            },
            // if evenly divisible by 20 --> dark grey
            {
              "test": "datum['_x2'] % 20 == 0",
              "value": "#C9C9C9"
            }
          ],
          // otherwise --> light grey
          "value": "#E3E3E3"
        }
      }
    }
  ]
}
```

</details>

<br>

The first option template displays a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block
- uses multiple datasets:
	- a 100-row ***sequence*** dataset internally-generated in Vega-Lite with integer values from 1 to 101
	- a standard Power BI dataset (in this case, with only a single record consisting of the slicer percentage selection)
 - a ***params*** block with:
	- 3x ***value*** parameters for the performance zone endpoints
    - 3x ***expr*** parameters to determine the performance zone midpoints
- a ***transform*** block with:
	- a ***lookup*** transform to extend the *sequence* dataset with the percentage from the Power BI dataset
	- a ***calculate*** transform to extend the *sequence* dataset with a "-1" value (to enable the use of ranged bar marks)
    - a ***calculate*** transform to extend the *sequence* dataset with segment labels

1 - Divider:
- a ***rule*** mark with:
  - a single-record hard-coded dataset
  - ranged X values to set the starting point and width
  - a named style

2 - Linear Gauge:
- a ***layer*** block for the linear gauge
	- *(the *layer* is not needed for rendering purposes, but is included to allow easy block naming)*
	- a ***bar*** mark with:
		- a named style
		- reversed X and Y axes to render as a column chart
		- ranged X and Y axes using X/X2/Y/Y2 encoding
		- hard-coded values for the X axis labels (20, 40, 60, 80)
		- *conditional* fill colour set by segment (performance zone) using Power Bi theme colours (7, 5, 1)

2 - Segment Labels:
- a ***transform*** block with:
	- a ***filter*** transform to reduce the dataset by including only segment midpoints (i.e., 3 records)
	- a ***bar*** mark with:
		- a named style
        -  a hard-coded Y value to position the segment labels above the columns

3 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
	- X axis (no domain, no ticks, no grid, label font family, label font size)
    - title style
    - named styles:
		- divider (colour)
		- column chart (rounded corners, stroke colour)
        - segment label (colour, font size)
        - symbol (Power BI theme colour 1, filled = true)

<hr>

### Links:

Here's the templates:

[905.1 - JSON - Deneb Template - Option 1 - Units (withperformance zones and pointer)](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/905.1%20-%20deneb_template.linear_gauge_1_units_with_performance_zones_and_pointer.v1.8.1.json) <br>
[905.2 - JSON - Deneb Template - Option 2 - Units (with performance zones)](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/905.2%20-%20deneb_template.linear_gauge_2_units_with_performance_zones.v1.8.1.json) <br>
[905.3 - JSON - Deneb Template - Option 3 - Units (basic) ](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/905.3%20-%20deneb_template.linear_gauge_3_units_basic.v1.8.1.json) <br>

<br>

Here's an example Power BI file using the templates:

[905.4 - PBIX - Deneb Example - Linear Gauges ](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/905.4%20-%20Deneb%20Reusable%20Components%20-%20Linear%20Gauges%20-%20V1.8.1.pbix) <br>

*- eof*
