<img width="1280" height="659" alt="214 - Image - Title - Correlation Chart" src="https://github.com/user-attachments/assets/41047191-0f2e-466f-a5a8-f7943b9eb279" />

## Correlation Chart

*January 14, 2026*

Deneb/Vega-Lite can be used to create a correlation chart showing how well team members work together over time.

Dataset Description:
- This dataset tracks the correlation of time spent working together on projects between six team members across two years, analyzed by semester.

Correlation Chart Description:
- Each cell represents the percentage of time two team members collaborated on shared projects during specific months, with correlations above 70% coloured to highlight significant collaborative relationships.

Correlation Chart Benefits:
- Monitor Cross-Pollination: tracks whether team members are rotating through different project partnerships across semesters, preventing siloed expertise and ensuring knowledge sharing throughout the organization
- Monitor Team Cohesion: identifies which team members work well together
- Identify Collaboration Gaps: identifies team members who consistently show low correlation with others, indicating potential isolation that may require intervention through deliberate project assignments or team activities
- Leadership - Health: serves as a team health dashboard and transforms collaboration data into actionable intelligence for building a truly cohesive team where everyone works with everyone over time
- Leadership - Cultural Evolution: shows if intentional efforts to improve cross-functional collaboration are actually working over time
- Balance Team Dynamics: ensures no permanent "cliques" form by observing if the same pairs frequently work together and show resultant high correlation over time, and promotes healthy rotation of working relationships
- Proactive Team Building: provides insights to deliberately design future project teams that break up overly-correlated pairs and create new collaborative opportunities, fostering a more resilient and interconnected team culture

This example presents a facet (or small multiple) for each team member with 2 parts: a header with their name and role, and a correlation matrix displaying their correlation score with each team member for a six-month period. Only correlations over 70% are shown, and the correlation ***squares*** are coloured in bands, with the peak score in the matrix being both highlighted and labelled. Further, Power BI theme colours are used, all calculations are done in Deneb/Vega-Lite (no Power BI calculations [i.e., no DAX] are used), and a native Power BI slicer is used to filter the [Dates] table into semesters (halves).

I provide a Deneb template for just this scenario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "36349513-b60b-4ad3-be79-f49783fd74f0",
      "generated": "2026-01-13T16:17:25.332Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Correlation Chart",
      "description": "A team correlation chart, with a facet for each team member with 2 parts: a header and a correlation matrix. Only correlations over 70% are shown, and the correlation squares are coloured in bands, with the peak score in the matrix both highlighted and labelled.",
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
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  \"title\": {\r\n    \"font\": \"Segoe UI Semibold\",\r\n    \"fontSize\": 18,\r\n    \"fontWeight\": \"normal\",\r\n    \"fontStyle\": \"italic\",\r\n    \"color\": \"#5C5347\",\r\n    \"subtitleFont\": \"Segoe UI\",\r\n    \"subtitleFontSize\": 14,\r\n    \"subtitleFontWeight\": \"normal\",\r\n    \"subtitleFontStyle\": \"italic\",\r\n    \"subtitleColor\": \"#8C8377\"\r\n  },\r\n  \"axis\": {\r\n    \"domain\": false,\r\n    \"ticks\": false,\r\n    \"labelFont\": \"Segoe UI\",\r\n    \"labelFontSize\": 12,\r\n    \"labelColor\": \"#605E5C\"\r\n  },\r\n  \"axisDiscrete\": {\r\n    \"grid\": false,\r\n    \"labelPadding\": 4\r\n  },\r\n  \"axisQuantitative\": {\r\n    \"grid\": false,\r\n    \"labelAlign\": \"center\",\r\n    \"labelPadding\": 4\r\n  },\r\n  \"style\": {\r\n    \"_divider_rule_style\": {\r\n      \"color\": \"#E3E3E3\"\r\n    },\r\n    \"_facet_card_background_bar_style\": {\r\n      \"cornerRadius\": 4,\r\n      \"color\": \"transparent\"      \r\n      // // use the parameter to have the same background colour\r\n      // \"color\": {\r\n      //   \"expr\": \"_background_colour\"\r\n      // }\r\n    },\r\n    \"_facet_point_style\": {\r\n      \"shape\": \"circle\",\r\n      \"filled\": true,\r\n      \"size\": 2000,\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_facet_initial_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 20,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"normal\",\r\n      \"color\": \"white\"\r\n    },\r\n    \"_facet_title_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 18,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#4A4A4A\"\r\n    },\r\n    \"_facet_subtitle_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_correlation_rectangle_style\": {\r\n      \"stroke\": {\r\n        \"expr\": \"_background_colour\"\r\n      },\r\n      \"strokeWidth\": 2,\r\n      \"cornerRadius\": 4\r\n    },\r\n    \"_correlation_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"italic\"\r\n    },\r\n    \"_custom_legend_bar_style\": {\r\n      \"cornerRadius\": 4\r\n    },\r\n    \"_custom_legend_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#969696\"\r\n    }\r\n  }\r\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Date",
        "description": "",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__1__",
        "name": "Person_ID",
        "description": "",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__2__",
        "name": "Person_Name",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__3__",
        "name": "Person_Initials",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__4__",
        "name": "Person_Role",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__5__",
        "name": "Correlated_Person_ID",
        "description": "",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__6__",
        "name": "Correlated_Person_Name",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__7__",
        "name": "Correlated_Person_Initials",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__8__",
        "name": "Correlated_Person_Role",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__9__",
        "name": "Correlation_Score",
        "description": "",
        "kind": "column",
        "type": "numeric"
      }
    ]
  }, // START
  // text and position only; formatting done in "config\title"
  "title": {
    "anchor": "start",
    "align": "left",
    "text": "Correlation Chart",
    "subtitle": "Correlations over 70%",
    "subtitlePadding": 2
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "transform": [
    // assign internal names to dataset fields
    {
      "calculate": "toDate( datum['__0__'] )",
      "as": "_date"
    },
    {
      "calculate": "toNumber( datum['__9__'] )",
      "as": "_value"
    },
    {
      "calculate": "datum['__1__']",
      "as": "_person_id"
    },
    {
      "calculate": "datum['__3__']",
      "as": "_person_initials"
    },
    {
      "calculate": "datum['__2__']",
      "as": "_person_name"
    },
    {
      "calculate": "datum['__4__']",
      "as": "_person_role"
    },
    {
      "calculate": "datum['__5__']",
      "as": "_correlated_person_id"
    },
    {
      "calculate": "datum['__6__']",
      "as": "_correlated_person_name"
    },
    {
      "calculate": "datum['__7__']",
      "as": "_correlated_person_initials"
    },
    {
      "calculate": "datum['__8__']",
      "as": "_correlated_person_role"
    },
    {
      "calculate": "toNumber( datum['__9__'] )",
      "as": "_correlation_score"
    },
    {
      "calculate": "datum['_correlation_score'] / 100",
      "as": "_correlation_score_percent"
    },
    // get date components
    {
      "calculate": "month( datum['_date'] )",
      "as": "_month"
    }
  ],
  "params": [
    {
      "name": "_background_colour",
      "value": "#FAF9F6"
    },
    // choose the [value] parameters for hard-coded colours or the [expr] parameters for Power BI theme colours
    {
      "name": "_square_colour_1",
      // "value": "#F0EAD6"
      "expr": "pbiColor(2)"
    },
    {
      "name": "_square_colour_2",
      // "value": "#E6D2B5"
      "expr": "pbiColor(1)"
    },
    {
      "name": "_square_colour_3",
      // "value": "#C69C6D"
      "expr": "pbiColor(0)"
    },
    {
      "name": "_square_colour_peak",
      "value": "#1E1E1E"
    }
  ],
  // adjust to achieve the desired vertical spacing between the divider and the chart
  "spacing": 0,
  "vconcat": [
    {
      "name": "DIVIDER_1",
      // adjust width as desired to suit visual
      "width": 940,
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
        "xOffset": -10,
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
      "name": "PERFORMANCE_CHART",
      "columns": 3,
      "spacing": 20,
      "facet": {
        "field": "_person_name",
        "type": "nominal",
        "header": {
          "title": null,
          "labelExpr": "null"
        }
      },
      "spec": {
        "spacing": 4,
        "vconcat": [
          {
            "name": "TITLE_BLOCK",
            // ensure only 1 record per person
            "transform": [
              {
                "aggregate": [
                  {
                    "op": "sum",
                    "field": "_correlation_score",
                    "as": "_sum_correlation_score"
                  }
                ],
                "groupby": [
                  "_person_id",
                  "_person_name", // add field for pass-through to aggregation
                  "_person_initials", // add field for pass-through to aggregation
                  "_person_role" // add field for pass-through to aggregation
                ]
              }
            ],
            "height": 60,
            "width": 280,
            // shared encoding
            "encoding": {
              "x": {
                "type": "quantitative",
                "axis": null,
                "scale": {
                  "domain": [
                    0,
                    100
                  ]
                }
              },
              "y": {
                "type": "quantitative",
                "axis": null
              }
            },
            "layer": [
              {
                "name": "BACKGROUND_BAR",
                "mark": {
                  "type": "bar",
                  "style": "_facet_card_background_bar_style"
                },
                "encoding": {
                  "x": {
                    "datum": 0
                  },
                  "x2": {
                    "datum": 100
                  },
                  "y": {
                    "datum": 0
                  },
                  "y2": {
                    "datum": 100
                  }
                }
              },
              {
                "name": "CIRCLE",
                "mark": {
                  "type": "point",
                  "style": "_facet_point_style"
                },
                "encoding": {
                  "x": {
                    "datum": 10
                  },
                  "y": {
                    "datum": 50
                  }
                }
              },
              {
                "name": "INITIALS",
                "mark": {
                  "type": "text",
                  "align": "center",
                  "style": "_facet_initial_text_style"
                },
                "encoding": {
                  "text": {
                    "field": "_person_initials",
                    "type": "nominal"
                  },
                  "x": {
                    "datum": 10
                  },
                  "y": {
                    "datum": 50
                  }
                }
              },
              {
                "name": "TITLE",
                "mark": {
                  "type": "text",
                  "align": "left",
                  "baseline": "bottom",
                  "style": "_facet_title_text_style"
                },
                "encoding": {
                  "text": {
                    "field": "_person_name",
                    "type": "nominal"
                  },
                  "x": {
                    "datum": 20
                  },
                  "y": {
                    "datum": 45
                  }
                }
              },
              {
                "name": "SUBTITLE",
                "transform": [
                  {
                    "calculate": "upper( datum['_person_role'] )",
                    "as": "_uppercase_person_role"
                  }
                ],
                "mark": {
                  "type": "text",
                  "align": "left",
                  "baseline": "top",
                  "style": "_facet_subtitle_text_style"
                },
                "encoding": {
                  "text": {
                    "field": "_uppercase_person_role",
                    "type": "nominal"
                  },
                  "x": {
                    "datum": 20
                  },
                  "y": {
                    "datum": 40
                  }
                }
              },
              {
                // add space between title text and correlation chart
                "name": "SPACER",
                "mark": {
                  "type": "text",
                  "color": "transparent"
                },
                "encoding": {
                  "text": {
                    "value": "junk"
                  },
                  "x": {
                    "datum": 1
                  },
                  "y": {
                    // adjust value as desired
                    "datum": -8
                  }
                }
              }
            ]
          },
          {
            "name": "CORRELATION_CHART",
            "height": 240,
            "width": 280,
            // set the colour of the view background
            "view": {
              "fill": {
                "expr": "_background_colour"
              }
            },
            "transform": [
              // determine the peak correlation score (per person)
              {
                "joinaggregate": [
                  {
                    "op": "max",
                    "field": "_correlation_score",
                    "as": "_max_correlation_score"
                  }
                ],
                "groupby": [
                  "_person_id"
                ]
              },
              {
                "calculate": "monthFormat( datum['_month'] )",
                "as": "_month_name"
              },
              {
                "calculate": "monthAbbrevFormat( datum['_month'] )",
                "as": "_month_abbrev"
              }
            ],
            "encoding": {
              "x": {
                "field": "_month_abbrev",
                "type": "nominal",
                "axis": {
                  "orient": "top",
                  "labelAngle": 0,
                  "title": null
                },
                "sort": [
                  "Jan",
                  "Feb",
                  "Mar",
                  "Apr",
                  "May",
                  "Jun",
                  "Jul",
                  "Aug",
                  "Sep",
                  "Oct",
                  "Nov",
                  "Dec"
                ]
              },
              "y": {
                "field": "_correlated_person_initials",
                "type": "nominal",
                "axis": {
                  "title": null
                }
              },
              "tooltip": [
                {
                  "field": "_month_name",
                  "type": "nominal",
                  "title": "Month"
                },
                {
                  "field": "_person_name",
                  "type": "nominal",
                  "title": "Person"
                },
                {
                  "field": "_correlated_person_name",
                  "type": "nominal",
                  "title": "Correlated Person"
                },
                {
                  "field": "_correlation_score_percent",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  "format": "#%",
                  "title": "Correlation Score"
                }
              ]
            },
            "layer": [
              {
                "name": "RECTANGLE",
                "mark": {
                  "type": "rect",
                  "tooltip": true,
                  "style": "_correlation_rectangle_style"
                },
                "encoding": {
                  "x": {
                    "field": "_month_abbrev"
                  },
                  "color": {
                    "condition": [
                      {
                        "test": "datum['_correlation_score'] == datum['_max_correlation_score']",
                        "value": {
                          "expr": "_square_colour_peak"
                        }
                      },
                      {
                        "test": "datum['_correlation_score_percent'] >= 0.9",
                        "value": {
                          "expr": "_square_colour_3"
                        }
                      },
                      {
                        "test": "datum['_correlation_score_percent'] >= 0.8",
                        "value": {
                          "expr": "_square_colour_2"
                        }
                      },
                      {
                        "test": "datum['_correlation_score_percent'] >= 0.7",
                        "value": {
                          "expr": "_square_colour_1"
                        }
                      }
                    ],
                    "value": "transparent"
                  }
                }
              },
              {
                "name": "LABEL",
                "mark": {
                  "type": "text",
                  "style": "_correlation_text_style"
                },
                "encoding": {
                  "text": {
                    "field": "_correlation_score_percent",
                    "formatType": "pbiFormat",
                    "format": "#%"
                  },
                  "x": {
                    "field": "_month_abbrev"
                  },
                  "color": {
                    "condition": [
                      {
                        "test": "datum['_correlation_score'] == datum['_max_correlation_score']",
                        "value": "#FFFFFF"
                      }
                    ],
                    "value": "transparent"
                  }
                }
              }
            ] // end layer
          } // end block
        ] // end vconcat
      } // end spec
    }, // end block
    {
      "name": "LEGEND",
      "width": 200,
      "height": 10,
      "data": {
        "values": [
          {
            "_legend_id": 1,
            "_legend_x1": 0,
            "_legend_x2": 10,
            "_legend_label": "70-|79%"
          },
          {
            "_legend_id": 2,
            "_legend_x1": 20,
            "_legend_x2": 30,
            "_legend_label": "80-|89%"
          },
          {
            "_legend_id": 3,
            "_legend_x1": 40,
            "_legend_x2": 50,
            "_legend_label": "90-|99%"
          },
          {
            "_legend_id": 4,
            "_legend_x1": 60,
            "_legend_x2": 70,
            "_legend_label": "Peak"
          }
        ]
      },
      "encoding": {
        "x": {
          "type": "quantitative",
          "axis": {
            "title": null,
            "labels": false,
            "domain": false,
            "grid": false
          },
          "scale": {
            "domain": [
              0,
              100
            ]
          }
        },
        "y": {
          "type": "quantitative",
          "axis": {
            "title": null,
            "labels": false,
            "domain": false,
            "grid": false
          },
          "scale": {
            "domain": [
              0,
              1
            ]
          }
        }
      },
      "layer": [
        {
          "name": "SQUARES",
          "mark": {
            "type": "bar",
            "height": 20,
            "baseline": "top",
            "style": "_custom_legend_bar_style"
          },
          "encoding": {
            "x": {
              "field": "_legend_x1"
            },
            "x2": {
              "field": "_legend_x2"
            },
            "color": {
              "field": "_legend_label",
              "type": "nominal",
              "scale": {
                "domain": [
                  "70-|79%",
                  "80-|89%",
                  "90-|99%",
                  "Peak"
                ],
                "range": [
                  {
                    "expr": "_square_colour_1"
                  },
                  {
                    "expr": "_square_colour_2"
                  },
                  {
                    "expr": "_square_colour_3"
                  },
                  {
                    "expr": "_square_colour_peak"
                  }
                ]
              },
              // set to null to turn off the legend automatically generated by Vega-Lite
              "legend": null
            }
          }
        },
        {
          "name": "LABELS",
          "transform": [
            {
              "calculate": "( datum['_legend_x1'] + datum['_legend_x2'] ) / 2",
              "as": "_legend_x_mid"
            }
          ],
          "mark": {
            "type": "text",
            "baseline": "top",
            "align": "center",
            "lineBreak": "|",
            "style": "_custom_legend_text_style"
          },
          "encoding": {
            "text": {
              "field": "_legend_label",
              "type": "nominal"
            },
            "x": {
              "field": "_legend_x_mid"
            },
            "y": {
              "datum": -2
            }
          }
        }
      ]
    }
  ] // end vconcat
} // END
```
</details>

<br>

This example illustrates a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block with ***subtitle***
- a standard Power BI dataset
- a ***transform*** block with:
    - 11x ***calculate*** transforms to assign internal names to the Power BI dataset fields
    - a ***calculate*** transform to determine the correlation score as a percentage
    - a ***calculate*** transform to determine the month
- a ***params*** block with:
    - 2x ***value*** parameters to set the background and peak square colours
    - 3x ***expr*** parameters to set the correlation score band colours to the ***Power BI theme colours***
- a ***vconcat*** block for the divider, the correlation chart, and the custom legend

1 - Divider:
- a ***rule*** mark with:
    - a single-record hard-coded dataset
    - ***ranged X values*** to set the starting point and width
    - a *named style*

2 - Correlation Chart:
- a ***facet*** block to create small multiples by team member with header titles and labels disabled
- a ***spec*** block with a ***vconcat*** block for the facet title section and facet correlation matrix

>[!NOTE]
>*facets are configured to use 3 columns by adding a ***columns: 3*** key:value pair and NOT using ***row*** or ***column*** in the facet definition*

2a - Header:
- a nested ***transform*** block with:
    - an ***aggregate*** transform to restrict the dataset to 1 record per person
        - *additional fields (name, initials, role) added to the aggregation to have them "pass-through" the aggregation and thus be available afterwards*
- a ***shared encoding*** block to ensure all layered marks use the same axis configurations
 	- the ***X-axis*** uses a ***scale/domain*** array to set a 0-100 scale for ease of positioning the component elements
- a ***layer*** block for the background bar, the circle, the initials, the name, the role, and a vertical spacer

2a (1) - Background Bar:
- a ***bar*** mark with:
    - ranged X and Y values to set the full-size height and width
    - a *named style*

2a (2) - Circle:
- a ***point/circle*** mark with:
    - fixed X and Y values for absolute positioning
    - a *named style*

2a (3) - Initials:
- a ***text*** mark with:
    - fixed X and Y values for absolute positioning
    - a *named style*

2a (4) - Name:
- a ***text*** mark with:
    - baseline=bottom
    - fixed X and Y values for absolute positioning
    - a *named style*
 
2a (3) - Role:
- a nested ***transform*** block with:
    - a ***calculate*** transform to convert the role to uppercase
- a ***text*** mark with:
    - baseline=top
    - fixed X and Y values for absolute positioning
    - a *named style*

 2a (6) - Spacer:
- a ***text*** mark with:
    - colour=transparent (as intent is not to show data, but only to provide vertical space between the header and the correlation matrix)
    - fixed X and Y values for absolute positioning

2b - Matrix:
- a ***view/fill*** block to set the background colour of the matrix
- a nested ***transform*** block with:
    - a ***joinaggregate/max*** transform to determine the highest correlation score for each person
    - 2x ***calculate*** transforms to determine the full name and abbreviation for the numerical month
- a ***shared encoding*** block to ensure all layered marks use the same axis configurations
 	- the ***X-axis*** block with:
      - an ***orient/top*** key:value pair to position the labels at the top of the matrix
      - a ***sort*** block to display the (text) month abbreviations in calendar order
      - a ***tooltip*** block with:
        - full month name, person name, and correlated person name
        - correlation score as a percentage using a ***Power BI format string*** as enabled by Deneb
- a ***layer*** block for the correlation rectangle (actually a square) and the correlation label

2b (1) - Correlation Rectangle (Square):
- a ***rect*** mark with:
    - ***conditional colour*** (uses the band colours defined in the ***params*** block)
    - tooltip enabled (uses the custom tooltip as defined in the ***shared encoding*** block)
    - a *named style*

2b (2) - Correlation Label:
- a ***text*** mark with:
    - correlation score as a percentage using a ***Power BI format string*** as enabled by Deneb
    - ***conditional colour*** (if score=max then white, else transparent [so, not displayed])
    - tooltip enabled (uses the custom tooltip as defined in the shared encoding block)
    - a *named style*

3 - Legend:
- a 4-record ***hard-coded dataset*** (labels include a linebreak character to enable multi-line display)
- a ***shared encoding*** block to ensure all layered marks use the same axis configurations
 	- the ***X-axis*** uses a ***scale/domain*** array to set a 0-100 scale for ease of positioning the component elements
   	- the ***Y-axis*** uses a ***scale/domain*** array to set a 0-1 scale for ease of positioning the component elements
- a ***layer*** block for the squares and the labels

3a - Legend Squares:
- a ***bar*** mark with:
    - ***ranged X values*** to set the starting and ending positions
    - ***conditional colour*** via a *scale/domain/range* block (using the ***Power BI theme colours*** as defined in the ***params*** block above)
    - a *named style*

3b - Legend Labels:
- a nested ***transform*** block with:
    - a ***calculate*** transform to determine the mid X coordinate of each "square"
- a ***text*** mark with:
    - a custom linebreak character (matching that used in the dataset labels)
    - a *named style*

4 - Config:
- configuration values set for:
	- border (colour [stroke] set to null)
    - title font attributes (family, size, weight, style, colour)
    - subtitle font attributes (family, size, weight, style, colour)
    - general ***axis*** attributes (domain [disabled], ticks [disabled], label font attributes [family, size, colour])
    - ***X*** axis (quantitative) attributes (grid [disabled], label padding)
    - ***Y*** axis (discrete) attributes (grid [disabled], label padding)
    - named styles:
        - divider colour
        - facet card background bar attributes (corner rounding, colour [enable parameter to use the same background colour as the matrix])
        - facet card point attributes (shape=circle, filled=true, size, colour)
        - facet card initials text attributes (family, size, weight, style, colour)
        - facet card name text attributes (family, size, weight, style, colour)
        - facet card role text attributes (family, size, weight, style, colour)
        - correlation score square (rectangle) attributes (corner rounding, stroke colour, stroke width)     
        - correlation score label font attributes (family, size, weight, style)
        - custom legend bar (square) corner rounding
        - custom legend label font attributes (family, size, weight, style, colour)

<hr>

### Links:

Here's the template:

[914.1 - JSON - Deneb Template - Correlation Chart](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/914.1%20-%20deneb_correlation_chart.v1.8.2.json) <br>

<br>

Here's an example Power BI file using the template:

[914.2 - PBIX - Deneb Example - Correlation Chart](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/914.2%20-%20Deneb%20Reusable%20Components%20-%20Correlation%20Chart%20-%20V1.8.2.pbix) <br>

*- eof*
