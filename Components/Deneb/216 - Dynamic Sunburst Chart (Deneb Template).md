<img width="1280" height="659" alt="216 - Image - Title - Dynamic Sunburst Chart - V3" src="https://github.com/user-attachments/assets/b76f5cdf-e7f1-4a59-9344-ec18a6c12631" />

## Dynamic Sunburst Chart

*March 16, 2026*

Deneb/Vega-Lite can be used to create a ***Dynamic Sunburst Chart*** to graphically show market decomposition with concentric donut charts for categories and subcategories. Further, D/VL can be used to create an integrated "slicer" to both highlight the selected category and to display only the subcategories for the selected category. Finally, D/VL transformations can be used in the chart to produce a ***Top 3 and Others*** design, both at the category and subcategory levels.

The example presented herein is a composite visual with an inner donut for categories, an outer donut for subcategories (complete with dual labels and leader lines), and a slicer; as noted above, the visual uses a ***Top 3 and Others*** design.

A simple synthetic dataset representing a selection of rounded values for product categories and subcategories was used in the development of this template.

I provide a Deneb template for just this scenario. 

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "90aeaa76-46c8-46e7-9f39-e4ed334758cc",
      "generated": "2026-03-16T20:10:36.954Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Dynamic Sunburst Chart",
      "description": "Useful for market decomposition analysis, this \"Top 3 and Others\" chart has an inner donut for categories, an outer donut for subcategories, and an integrated Vega-Lite slicer. Subcategories are displayed only for the selected category and have multi-line data labels and leader lines. ",
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
      "highlight": true,
      "dataPointLimit": 50
    },
    "config": "{\r\n  \"view\": {\r\n    \"stroke\": null\r\n  },\r\n  \"title\": {\r\n    \"font\": \"Segoe UI\",\r\n    \"fontSize\": 24,\r\n    \"fontWeight\": \"bold\",\r\n    \"fontStyle\": \"italic\",\r\n    \"color\": \"#4A4A4A\",\r\n    \"subtitleFont\": \"Segoe UI\",\r\n    \"subtitleFontSize\": 16,\r\n    \"subtitleFontWeight\": \"normal\",\r\n    \"subtitleFontStyle\": \"italic\",\r\n    \"subtitleColor\": \"#969696\"\r\n  },\r\n  \"style\": {\r\n    \"subcategory_leader_line_mask_arc_style\": {\r\n      \"color\": \"white\"\r\n    },\r\n    \"_slice_arc_style\": {\r\n      \"stroke\": \"white\",\r\n      \"strokeWidth\": 4\r\n    },\r\n    \"_subcategory_name_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 14,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"normal\",\r\n      \"color\": \"#4A4A4A\"\r\n    },\r\n    \"_subcategory_amount_percent_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 12,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"normal\",\r\n      \"color\": \"#707070\"\r\n    },\r\n    \"_subcategory_leader_line_rule_style\": {\r\n      \"color\": \"#969696\"\r\n    },\r\n    \"_category_label_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 14,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#707070\"\r\n    },\r\n    \"_category_name_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 24,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"normal\",\r\n      \"color\": \"#4A4A4A\"\r\n    },\r\n    \"_category_amount_percent_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 16,\r\n      \"fontWeight\": \"bold\",\r\n      \"fontStyle\": \"normal\",\r\n      \"color\": \"#4A4A4A\"\r\n    },\r\n    \"_total_label_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 14,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"italic\",\r\n      \"color\": \"#707070\"\r\n    },\r\n    \"_slicer_category_name_text_style\": {\r\n      \"font\": \"Segoe UI\"\r\n    },\r\n    \"_slicer_category_amount_text_style\": {\r\n      \"font\": \"Segoe UI\",\r\n      \"fontSize\": 10,\r\n      \"fontWeight\": \"normal\",\r\n      \"fontStyle\": \"normal\"\r\n    }\r\n  }\r\n}",
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
        "name": "Subcategory ID",
        "description": "",
        "kind": "column",
        "type": "numeric"
      },
      {
        "key": "__3__",
        "name": "Subcategory",
        "description": "",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__4__",
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
    // "offset": 20,
    "text": "Dynamic Sunburst Chart",
    "subtitle": [
      "Market Segment Decomposition | Category and subcategory | Top 3 and Others",
      "Absolute amounts in € | Category percentages of total | Subcategory percentages of category"
    ]
  },
  // Power BI dataset
  "data": {
    "name": "dataset"
  },
  "transform": [
    // use an internal development ID for easy dataset identification
    {
      "calculate": "1",
      "as": "_DEV_ID"
    },
    // assign internal names to dataset fields
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
      "as": "_subcategory_id"
    },
    {
      "calculate": "datum['__3__']",
      "as": "_subcategory"
    },
    {
      "calculate": "datum['__4__']",
      "as": "_amount"
    },
    // get amount and rank for subcategories
    {
      "aggregate": [
        {
          "op": "sum",
          "field": "_amount",
          "as": "_subcategory_amount"
        }
      ],
      // include additional fields in grouping so they can be accessed after the aggregation
      "groupby": [
        "_subcategory",
        "_subcategory_id",
        "_category",
        "_category_id"
      ]
    },
    {
      "window": [
        {
          "op": "dense_rank",
          "as": "_subcategory_rank"
        }
      ],
      "groupby": [
        "_category"
      ],
      "sort": [
        {
          "field": "_subcategory_amount",
          "order": "descending"
        }
      ]
    },
    // get amount and rank for categories    
    {
      "joinaggregate": [
        {
          "op": "sum",
          "field": "_subcategory_amount",
          "as": "_category_amount"
        }
      ],
      "groupby": [
        "_category"
      ]
    },
    {
      "window": [
        {
          "op": "dense_rank",
          "as": "_category_rank"
        }
      ],
      "sort": [
        {
          "field": "_category_amount",
          "order": "descending"
        }
      ]
    },
    // get total amount
    {
      "joinaggregate": [
        {
          "op": "sum",
          "field": "_subcategory_amount",
          "as": "_total_amount"
        }
      ]
    },
    // count categories
    {
      "joinaggregate": [
        {
          "op": "distinct",
          "field": "_category_id",
          "as": "_number_of_categories"
        }
      ]
    },
    // if more than 3 categories, then for those ranked 4+, set category = Other
    {
      "calculate": "if( datum['_number_of_categories'] > 3, datum['_category_rank'] > 3 ? 'Other' : datum['_category'], datum['_category'] )",
      "as": "_category"
    },
    // if more than 3 categories, then for those ranked 4+, set category id = 9
    {
      "calculate": "if( datum['_number_of_categories'] > 3, datum['_category_rank'] > 3 ? 9 : datum['_category_id'], datum['_category_id'] )",
      "as": "_category_id"
    },
    // redo amount and rank for categories
    {
      "joinaggregate": [
        {
          "op": "sum",
          "field": "_subcategory_amount",
          "as": "_category_amount"
        }
      ],
      "groupby": [
        "_category"
      ]
    },
    {
      "window": [
        {
          "op": "dense_rank",
          "as": "_category_rank"
        }
      ],
      "sort": [
        {
          "field": "_category_amount",
          "order": "descending"
        }
      ]
    },
    // if category = [Other] then category_rank = 9
    {
      "calculate": "datum['_category'] == 'Other' ? 9 : datum['_category_rank']",
      "as": "_category_rank"
    },
    // count subcategories
    {
      "joinaggregate": [
        {
          "op": "distinct",
          "field": "_subcategory_id",
          "as": "_number_of_subcategories"
        }
      ],
      "groupby": [
        "_category_id"
      ]
    },
    // redo subcategory ranking
    {
      "window": [
        {
          "op": "dense_rank",
          "as": "_subcategory_rank"
        }
      ],
      "groupby": [
        "_category"
      ],
      "sort": [
        {
          "field": "_subcategory_amount",
          "order": "descending"
        }
      ]
    },
    // if more than 3 subcategories, then 4+ subcategory = Other
    {
      "calculate": "if( datum['_number_of_subcategories'] > 3, datum['_subcategory_rank'] > 3 ? 'Other' : datum['_subcategory'], datum['_subcategory'] )",
      "as": "_subcategory"
    },
    // if more than 3 subcategories, then 4+ subcategory id = 99
    {
      "calculate": "if( datum['_number_of_subcategories'] > 3, datum['_subcategory_rank'] > 3 ? 99 : datum['_subcategory_rank'], datum['_subcategory_rank'] )",
      "as": "_subcategory_rank"
    },
    // redo amount and rank for subcategories
    {
      "aggregate": [
        {
          "op": "sum",
          "field": "_subcategory_amount",
          "as": "_subcategory_amount"
        }
      ],
      "groupby": [
        "_subcategory",
        "_category",
        "_category_id",
        "_category_amount",
        "_category_rank",
        "_total_amount"
      ]
    },
    {
      "window": [
        {
          "op": "dense_rank",
          "as": "_subcategory_rank"
        }
      ],
      "groupby": [
        "_category"
      ],
      "sort": [
        {
          "field": "_subcategory_amount",
          "order": "descending"
        }
      ]
    },
    // if subcategory = [Other] then subcategory_rank = 99
    {
      "calculate": "datum['_subcategory'] == 'Other' ? 99 : datum['_subcategory_rank']",
      "as": "_subcategory_rank"
    },
    // create composite rank for ordering
    {
      "calculate": "( datum['_category_rank'] * 100 ) + datum['_subcategory_rank']",
      "as": "_composite_rank"
    }
  ],
  "params": [
    {
      "name": "_subcategory_label_radius",
      "value": 84
    },
    {
      "name": "_subcategory_leader_line_radius",
      "value": 85
    },
    {
      "name": "_category_colour_1",
      "expr": "pbiColor(0)"
    },
    {
      "name": "_category_colour_2",
      "expr": "pbiColor(1)"
    },
    {
      "name": "_category_colour_3",
      "expr": "pbiColor(2)"
    },
    {
      "name": "_category_colour_other",
      "value": "#C9C9C9"
    }
  ],
  "vconcat": [
    {
      "name": "DYNAMIC_SUNBURST",
      "width": 800,
      "height": 800,
      "layer": [
        {
          "name": "SUBCATEGORY",
          "transform": [
            {
              "calculate": "2",
              "as": "_DEV_ID"
            },
            // redo category ranking
            {
              "window": [
                {
                  "op": "dense_rank",
                  "as": "_category_rank2"
                }
              ],
              "sort": [
                {
                  "field": "_category_rank",
                  "order": "ascending"
                }
              ]
            }
          ],
          "encoding": {
            "theta": {
              "field": "_subcategory_amount",
              "type": "quantitative"
            },
            "order": {
              "field": "_composite_rank",
              "type": "quantitative",
              "sort": "ascending"
            }
          },
          "layer": [
            {
              "name": "SUBCATEGORY_DONUT_LABELS",
              "transform": [
                {
                  "calculate": "3",
                  "as": "_DEV_ID"
                },
                {
                  "calculate": "datum['_category_amount'] / datum['_total_amount']",
                  "as": "_category_percent"
                },
                {
                  "calculate": "datum['_subcategory_amount'] / datum['_category_amount']",
                  "as": "_subcategory_percent"
                },
                {
                  "window": [
                    {
                      "op": "sum",
                      "field": "_subcategory_amount",
                      "as": "_end_amount"
                    }
                  ],
                  "sort": [
                    {
                      "field": "_composite_rank",
                      "order": "ascending"
                    }
                  ],
                  "ignorePeers": false,
                  "frame": [
                    null,
                    0
                  ]
                },
                {
                  "calculate": "datum['_end_amount'] - datum['_subcategory_amount']",
                  "as": "_start_amount"
                },
                {
                  "calculate": "toNumber( format( datum['_start_amount'] / datum['_category_amount'], '.2f' ) )",
                  "as": "_start_percent"
                },
                {
                  "calculate": "toNumber( format( datum['_end_amount'] / datum['_category_amount'], '.2f' ) )",
                  "as": "_end_percent"
                },
                // *** DEV ONLY - EASIER TO CHECK DEGREES - 
                // round/truncate degree values to 2 decimal places
                {
                  "calculate": "toNumber( format( 360 * datum['_category_percent'] * datum['_start_percent'], '.2f' ) )",
                  "as": "_start_degrees"
                },
                {
                  "calculate": "toNumber( format( 360 * datum['_category_percent'] * datum['_end_percent'], '.2f' ) )",
                  "as": "_end_degrees"
                },
                {
                  "calculate": "toNumber( format( ( datum['_start_degrees'] + datum['_end_degrees'] ) / 2, '.2f' ) )",
                  "as": "_mid_degrees"
                },
                // round/truncate radian values to 2 decimal places            
                {
                  "calculate": "toNumber( format( 2 * PI * datum['_category_percent'] * datum['_start_percent'], '.2f' ) )",
                  "as": "_start_radians"
                },
                {
                  "calculate": "toNumber( format( 2 * PI * datum['_category_percent'] * datum['_end_percent'], '.2f' ) )",
                  "as": "_end_radians"
                },
                {
                  "calculate": "toNumber( format( ( datum['_start_radians'] + datum['_end_radians'] ) / 2, '.2f' ) )",
                  "as": "_mid_radians"
                },
                {
                  "calculate": "sin( datum['_mid_radians'] ) * _subcategory_label_radius",
                  "as": "_x"
                },
                {
                  "calculate": "cos( datum['_mid_radians'] ) * _subcategory_label_radius",
                  "as": "_y"
                },
                // adjust Power BI format string to suit dataset        
                {
                  "calculate": "pbiFormat( datum['_subcategory_amount'], '#,0,. K' ) + ' / ' + pbiFormat( datum['_subcategory_percent'], '#%' )",
                  "as": "_subcategory_amount_percent_label"
                },
                {
                  "calculate": "_slicer_clicked_category_id._category_id",
                  "as": "_slicer_selected_category_id"
                }
              ],
              "encoding": {
                "x": {
                  "field": "_x",
                  "type": "quantitative",
                  "scale": {
                    "domain": [
                      -100,
                      100
                    ]
                  },
                  "axis": null
                },
                "y": {
                  "field": "_y",
                  "type": "quantitative",
                  "scale": {
                    "domain": [
                      -100,
                      100
                    ]
                  },
                  "axis": null
                }
              },
              "layer": [
                {
                  "name": "SUBCATEGORY_NAME_SLICE_LABELS",
                  "transform": [
                    {
                      "calculate": "4",
                      "as": "_DEV_ID"
                    }
                  ],
                  "mark": {
                    "type": "text",
                    "xOffset": {
                      "expr": "if( datum['_mid_radians'] <= PI, 10, -10 )"
                    },
                    "yOffset": 0,
                    "align": {
                      "expr": "if( datum['_mid_radians'] <= PI, 'left', 'right' )"
                    },
                    "opacity": {
                      "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 1 : 0"
                    },
                    "style": "_subcategory_name_text_style"
                  },
                  "encoding": {
                    "text": {
                      "field": "_subcategory",
                      "type": "nominal"
                    }
                  }
                },
                {
                  "name": "SUBCATEGORY_AMOUNT_PERCENT_SLICE_LABELS",
                  "transform": [
                    {
                      "calculate": "5",
                      "as": "_DEV_ID"
                    }
                  ],
                  "mark": {
                    "type": "text",
                    "xOffset": {
                      "expr": "if( datum['_mid_radians'] <= PI, 10, -10 )"
                    },
                    "yOffset": 14,
                    "align": {
                      "expr": "if( datum['_mid_radians'] <= PI, 'left', 'right' )"
                    },
                    "opacity": {
                      "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 1 : 0"
                    },
                    "style": "_subcategory_amount_percent_text_style"
                  },
                  "encoding": {
                    "text": {
                      "field": "_subcategory_amount_percent_label",
                      "type": "nominal"
                    }
                  }
                },
                {
                  "name": "SUBCATEGORY_LEADER_LINE",
                  "transform": [
                    {
                      "calculate": "6",
                      "as": "_DEV_ID"
                    }
                  ],
                  "mark": {
                    "type": "rule",
                    "opacity": {
                      "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 1 : 0"
                    },
                    "style": "_subcategory_leader_line_rule_style"
                  },
                  "encoding": {
                    "x": {
                      "datum": 0
                    },
                    "y": {
                      "datum": 0
                    },
                    "x2": {
                      "field": "_x"
                    },
                    "y2": {
                      "field": "_y"
                    }
                  }
                },
                {
                  "name": "SUBCATEGORY_LEADER_LINE_MASK",
                  "transform": [
                    {
                      "calculate": "7",
                      "as": "_DEV_ID"
                    }
                  ],
                  "mark": {
                    "type": "arc",
                    "innerRadius": 0,
                    "outerRadius": 305,
                    "style": "subcategory_leader_line_mask_arc_style"
                  },
                  "encoding": {
                    "x": {
                      "datum": 0
                    },
                    "y": {
                      "datum": 0
                    },
                    "x2": {
                      "field": "_x"
                    },
                    "y2": {
                      "field": "_y"
                    }
                  }
                }
              ]
            },
            {
              "name": "SUBCATEGORY_DONUT_SLICES",
              "transform": [
                {
                  "calculate": "8",
                  "as": "_DEV_ID"
                },
                {
                  "calculate": "_slicer_clicked_category_id._category_id",
                  "as": "_slicer_selected_category_id"
                }
              ],
              "mark": {
                "type": "arc",
                "innerRadius": 200,
                "outerRadius": 300,
                "color": {
                  "expr": "datum['_subcategory'] == 'Other' ? _category_colour_other : datum['_category_rank2'] == 1 ? _category_colour_1 : datum['_category_rank2'] == 2 ? _category_colour_2 : datum['_category_rank2'] == 3 ? _category_colour_3 : datum['_category_rank2'] == 4 ? _category_colour_other :'blue'"
                },
                "style": "_slice_arc_style"
              },
              "encoding": {
                "opacity": {
                  "condition": [
                    {
                      "test": "datum['_category_id'] != datum['_slicer_selected_category_id']",
                      "value": 0
                    },
                    {
                      "test": "datum['_subcategory'] == 'Other'",
                      "value": 1
                    }
                  ],
                  // each subcategory rank is 10% lighter (e.g., opacity is [1=90%, 2=80%, 3=70%)
                  "value": {
                    "expr": "1 - ( datum['_subcategory_rank'] / 10 )"
                  }
                }
              }
            }
          ]
        },
        {
          "name": "CATEGORY",
          "transform": [
            {
              "calculate": "9",
              "as": "_DEV_ID"
            },
            {
              "aggregate": [
                {
                  "op": "sum",
                  "field": "_subcategory_amount",
                  "as": "_category_amount"
                }
              ],
              "groupby": [
                "_category",
                "_category_id",
                "_category_rank",
                "_total_amount"
              ]
            },
            // redo category ranking to put [Other] last
            {
              "window": [
                {
                  "op": "rank",
                  "as": "_category_rank"
                }
              ],
              "sort": [
                {
                  "field": "_category_rank",
                  "order": "ascending"
                }
              ]
            }
          ],
          "encoding": {
            "theta": {
              "field": "_category_amount",
              "type": "quantitative"
            },
            "order": {
              "field": "_category_rank",
              "type": "quantitative",
              "sort": "ascending"
            }
          },
          "layer": [
            {
              "name": "CATEGORY_DONUT_SLICES",
              "transform": [
                {
                  "calculate": "10",
                  "as": "_DEV_ID"
                },
                {
                  "calculate": "_slicer_clicked_category_id._category_id",
                  "as": "_slicer_selected_category_id"
                }
              ],
              "mark": {
                "type": "arc",
                "outerRadius": 150,
                "innerRadius": 100,
                "color": {
                  "expr": "datum['_category'] == 'Other' ? _category_colour_other : datum['_category_rank'] == 1 ? _category_colour_1 : datum['_category_rank'] == 2 ? _category_colour_2 : datum['_category_rank'] == 3 ? _category_colour_3 : 'blue'"
                },
                "style": "_slice_arc_style"
              },
              "encoding": {
                "opacity": {
                  "condition": [
                    {
                      "test": "datum['_slicer_selected_category_id'] == null",
                      "value": 1
                    },
                    {
                      "test": "datum['_category_id'] == datum['_slicer_selected_category_id']",
                      "value": 1
                    }
                  ],
                  "value": 0.5
                }
              }
            }
          ]
        },
        {
          "name": "CENTER_INFO",
          "transform": [
            {
              "calculate": "11",
              "as": "_DEV_ID"
            },
            {
              "aggregate": [
                {
                  "op": "sum",
                  "field": "_subcategory_amount",
                  "as": "_category_amount2"
                }
              ],
              "groupby": [
                "_category",
                "_category_id",
                "_DEV_ID"
              ]
            },
            {
              "joinaggregate": [
                {
                  "op": "sum",
                  "field": "_category_amount2",
                  "as": "_total_amount2"
                }
              ]
            },
            {
              "calculate": "datum['_category_amount2'] / datum['_total_amount2']",
              "as": "_category_percent2"
            },
            // adjust Power BI format string to suit dataset        
            {
              "calculate": "pbiFormat( datum['_category_amount2'], '#,0,. K' ) + ' / ' + pbiFormat( datum['_category_percent2'], '#%' )",
              "as": "_category_amount_percent_label"
            },
            // adjust Power BI format string to suit dataset        
            {
              "calculate": "'of ' + pbiFormat( datum['_total_amount2'], '#,0,. K' ) + ' Total'",
              "as": "_total_label"
            }
          ],
          "layer": [
            {
              "name": "VIEWING_CATEGORY_LABEL",
              "transform": [
                {
                  "calculate": "_slicer_clicked_category_id._category_id",
                  "as": "_slicer_selected_category_id"
                },
                // only keep a single record
                {
                  "filter": "datum['_category_id'] == datum['_slicer_selected_category_id']"
                }
              ],
              "mark": {
                "type": "text",
                "baseline": "bottom",
                "yOffset": -26,
                "style": "_category_label_text_style"
              },
              "encoding": {
                "x": {
                  "datum": 0
                },
                "y": {
                  "datum": 0
                },
                "theta": {
                  "value": 0
                },
                "text": {
                  "value": "Viewing Category"
                }
              }
            },
            {
              "name": "SELECTED_CATEGORY_NAME",
              "transform": [
                {
                  "calculate": "_slicer_clicked_category_id._category_id",
                  "as": "_slicer_selected_category_id"
                },
                // only keep a single record
                {
                  "filter": "datum['_category_id'] == datum['_slicer_selected_category_id']"
                }
              ],
              "mark": {
                "type": "text",
                "baseline": "bottom",
                "yOffset": 0,
                "style": "_category_name_text_style"
              },
              "encoding": {
                "theta": {
                  "value": 0
                },
                "text": {
                  "field": "_category",
                  "type": "nominal"
                }
              }
            },
            {
              "name": "SELECTED_CATEGORY_AMOUNT_PERCENT",
              "transform": [
                {
                  "calculate": "_slicer_clicked_category_id._category_id",
                  "as": "_slicer_selected_category_id"
                },
                // only keep a single record
                {
                  "filter": "datum['_category_id'] == datum['_slicer_selected_category_id']"
                }
              ],
              "mark": {
                "type": "text",
                "align": "center",
                "baseline": "top",
                "yOffset": 0,
                "style": "_category_amount_percent_text_style"
              },
              "encoding": {
                "theta": {
                  "value": 0
                },
                "text": {
                  "field": "_category_amount_percent_label",
                  "type": "nominal"
                }
              }
            },
            {
              "name": "TOTAL_AMOUNT_LABEL",
              "transform": [
                {
                  "calculate": "_slicer_clicked_category_id._category_id",
                  "as": "_slicer_selected_category_id"
                },
                // only keep a single record
                {
                  "filter": "datum['_category_id'] == datum['_slicer_selected_category_id']"
                }
              ],
              "mark": {
                "type": "text",
                "align": "center",
                "baseline": "top",
                "yOffset": 20,
                "style": "_total_label_text_style"
              },
              "encoding": {
                "theta": {
                  "value": 0
                },
                "text": {
                  "field": "_total_label",
                  "type": "nominal"
                }
              }
            }
          ]
        }
      ]
    },
    {
      "name": "SLICER",
      "width": 800,
      "height": 40,
      "layer": [
        {
          "name": "BARS",
          "transform": [
            {
              "calculate": "12",
              "as": "_DEV_ID"
            },
            // aggregate the categories
            {
              "aggregate": [
                {
                  "op": "sum",
                  "field": "_subcategory_amount",
                  "as": "_category_amount"
                }
              ],
              "groupby": [
                "_category",
                "_category_id",
                "_category_rank",
                "_total_amount"
              ]
            },
            // redo category ranking
            {
              "window": [
                {
                  "op": "dense_rank",
                  "as": "_category_rank"
                }
              ],
              "sort": [
                {
                  "field": "_category_amount",
                  "order": "descending"
                }
              ]
            },
            // if category = [Other] then category_rank = 9
            {
              "calculate": "datum['_category'] == 'Other' ? 9 : datum['_category_rank']",
              "as": "_category_rank"
            },
            // redo category ranking to put [Other] last
            {
              "window": [
                {
                  "op": "dense_rank",
                  "as": "_category_rank"
                }
              ],
              "sort": [
                {
                  "field": "_category_rank",
                  "order": "ascending"
                }
              ]
            },
            /* 
              full width = 1000
              indent = 95 (each side, so 1000-190 = 810 left for "pills"
              pill = 720 (4x180)
              space = 90 (3x30)
              X coordinate should be:
              - pill 1: 95 to 275
              - pill 2: 305 to 485
              - pill 3: 515 to 695
              - pill 4: 725 to 905
            */
            {
              "calculate": "( ( datum['_category_rank'] - 1 ) * 180 ) + ( ( datum['_category_rank'] - 1 ) * 30 ) + 95",
              "as": "_slicer_bar_start_x"
            },
            {
              "calculate": "datum['_slicer_bar_start_x'] + 180",
              "as": "_slicer_bar_end_x"
            },
            {
              "calculate": "_slicer_clicked_category_id._category_id",
              "as": "_slicer_selected_category_id"
            }
          ],
          "encoding": {
            "order": {
              "field": "_category_rank",
              "type": "quantitative",
              "sort": "ascending"
            },
            "x": {
              "field": "_slicer_bar_start_x",
              "type": "quantitative",
              "scale": {
                "domain": [
                  0,
                  1000
                ]
              },
              "axis": {
                "title": null,
                "labels": false,
                "domain": false,
                "ticks": false,
                "grid": false
              }
            },
            "x2": {
              "field": "_slicer_bar_end_x"
            }
          },
          "layer": [
            {
              "name": "SLICER_BARS",
              "params": [
                {
                  "name": "_slicer_clicked_category_id",
                  "select": {
                    "type": "point",
                    "fields": [
                      "_category_id"
                    ],
                    "on": "click", // mouse click event
                    // "on": "pointerover", // mouse hover event
                    "resolve": "global"
                  }
                }
              ],
              "mark": {
                "type": "bar",
                "cornerRadius": 100,
                "y": 10,
                "y2": 30,
                "color": {
                  "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? '#303030' : '#E3E3E3'"
                }
              }
            },
            {
              "name": "SLICER_CIRCLES",
              "mark": {
                "type": "point",
                "shape": "circle",
                "filled": true,
                "size": {
                  "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 100 : 80"
                },
                "xOffset": {
                  "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 20 : 10"
                },
                "color": {
                  "expr": "datum['_category'] == 'Other' ? _category_colour_other : datum['_category_rank'] == 1 ? _category_colour_1 : datum['_category_rank'] == 2 ? _category_colour_2 : datum['_category_rank'] == 3 ? _category_colour_3 : 'blue'"
                }
              },
              "encoding": {
                "y": {
                  "value": 10
                },
                "text": {
                  "field": "_category",
                  "type": "nominal"
                }
              }
            },
            {
              "name": "SLICER_LABELS",
              "mark": {
                "type": "text",
                "align": "left",
                "baseline": "middle",
                "xOffset": {
                  "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 30 : 20"
                },
                "fontSize": {
                  "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 14 : 12"
                },
                "fontWeight": {
                  "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 'bold' : 'normal'"
                },
                "color": {
                  "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 'white' : 'black'"
                },
                "style": "_slicer_category_name_text_style"
              },
              "encoding": {
                "y": {
                  "value": 10
                },
                "text": {
                  "field": "_category",
                  "type": "nominal"
                }
              }
            },
            {
              "name": "SLICER_AMOUNTS",
              "mark": {
                "type": "text",
                "align": "right",
                "baseline": "middle",
                "xOffset": -10,
                "yOffset": 0,
                "color": {
                  "expr": "datum['_category_id'] == datum['_slicer_selected_category_id'] ? 'white' : 'black'"
                },
                "style": "_slicer_category_amount_text_style"
              },
              "encoding": {
                "x": {
                  "field": "_slicer_bar_end_x",
                  "type": "quantitative"
                },
                "y": {
                  "value": 10
                },
                "text": {
                  "field": "_category_amount",
                  "type": "quantitative",
                  "formatType": "pbiFormat",
                  // adjust format string to suit dataset
                  "format": "#0,. K"
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

<br>
<br>

0 - General:
- a ***title*** block with multi-line ***subtitle*** (using an array)
- a standard Power BI dataset
- a shared ***transform*** block with:
    - 5x ***calculate*** transforms to assign internal names to the Power BI dataset fields
    - 1x ***aggregate*** and ***window/dense_rank*** transforms to determine and rank the subcategory amounts
    - 1x ***joinaggregate*** and ***window/dense_rank*** transforms to determine and rank the category amounts
    - 2x ***joinaggregate*** transforms to determine the total amount and the number of categories
    - 2x ***calculate*** transforms to assign "Other" to categories ranked 4 and over
    - 1x ***joinaggregate*** and ***window/dense_rank*** and ***calculate*** transforms to redo the category amounts and ranks (now that "Other" applied)
    - 1x ***joinaggregate*** transform to determine the number of subcategories per category
    - 1x ***window/dense_rank*** transform to redo the subcategory ranks (now that "Other" applied)
    - 2x ***calculate*** transforms to assign "Other" to subcategories ranked 4 and over
    - 1x ***aggregate*** and ***window/dense_rank*** and ***calculate*** transforms to redo the subcategory amounts and ranks (now that "Other" applied)
    - 1x ***calculate*** transform to determine the composite rank (category and subcategory)
- a shared ***params*** block with:
    - 2x ***value*** parameters for the subcategory label and leader line radii
    - 3x ***expr*** parameters to internalize the top 3 ***Power BI theme colours***
    - 1x ***value*** parameter for the "Other" colour
- a ***vconcat*** block for the dynamic sunburst visual and the slicer

<br>
    
1 - Dynamic Sunburst Chart:
- a ***layer*** block for the subcategory, category, and center info

1a - Subcategory:
- a nested ***transform*** block with:
    - 1x ***window/dense_rank*** transforms to redo the category ranking
- a ***shared encoding*** block to ensure the same angular size/position and order are used for all layered marks
- a ***layer*** block for the donut slices and labels

1a1 - Subcategory Donut Slice Labels:
- a nested ***transform*** block with:
    - 2x ***calculate*** transforms to determine the category and subcategory percentages
    - 1x ***window/sum*** transform to determine the cumulative angular size (end amount) of the donut slices ordered by the composite rank (as calculated above)
    - 1x ***calculate*** transform to determine the start amount of the donut slices
    - 2x ***calculate*** transforms to determine the starting and ending percent of the donut slices
    - 3x ***calculate*** transforms to determine the starting, ending, and mid radians of the donut slices
    - 2x ***calculate*** transforms using the mid radians and sin and cos trigonometry functions to determine the X and Y positions of the mid-points of the donut slices
    - 1x *** calculate*** transform to determine the composite 2nd line of the data label (amount / percent [formatting via ***Power BI format strings*** as enabled by Deneb])
    - 1x ***calculate*** transform to extract the category ID from the clicked global parameter object
- a ***shared encoding*** block with fixed scales (-100 to +100) for the X and Y axes
- a ***layer*** block for the subcategory name label, amount/percent label, leader lines, and leader line mask

> [!NOTE]
> *X and Y positions are used for the subcategory labels; it is expected that this will become unnecessary once the correct syntax is found to reuse the existing "theta" encoding, but this solution works, and while it is verbose and calculation-heavy, more concise syntax is left for further development*

1a1a - Subcategory Donut Slice Labels (line 1):
- a ***text*** mark with:
    - ***conditional X position*** based on mid radians (<=PI=+10; >PI=-10)
    - Y position = 0
    - ***conditional alignment*** based on mid radians (<=PI=left; >PI=right)
    - ***conditional opacity*** based on selected category ID (selected=1; unselected=0)
    - value of the ***subcategory name***
    - a *named style*

1a1b - Subcategory Donut Slice Labels (line 2):
- a ***text*** mark with:
    - ***conditional X position*** based on mid radians (<=PI=+10; >PI=-10)
    - Y position = 14 (simulate a line break)
    - ***conditional alignment*** based on mid radians (<=PI=left; >PI=right)
    - ***conditional opacity*** based on selected category ID (selected=1; unselected=0)
    - value of the ***subcategory amount and percent of category*** (as calculated in the nested transform block above)
    - a *named style*

1a1c - Subcategory Donut Slice Label Leader Lines:
- a ***rule*** mark with:
    - ***fixed starting X and Y coordinates*** at the origin (0,0)
    - ***conditional X and Y coordinates*** at the sin and cos of the mid theta radian value
    - ***conditional opacity*** based on selected category ID (selected=1; unselected=0)
    - a *named style*
 
1a1d - Subcategory Donut Slice Label Leader Line Mask:
- an ***arc*** mark with:
    - ***fixed starting X and Y coordinates*** at the origin (0,0)
    - ***conditional X and Y coordinates*** at the sin and cos of the mid theta radian value
    - a *named style*
  
1a2 - Subcategory Donut Slices:
- an ***arc*** mark with:
    - a fixed ***stroke*** (white, 4px) to slightly separate the "slices"
    - ***conditional colour*** (other=light grey; top 3 set to ***Power BI theme colours***)
    - ***conditional opacity*** based on selected category ID (selected=1; unselected=0; each successive subcategory rank 10% lighter [1=90%, 2=80%, 3=70%])
    - a *named style*

1b - Category:
- a nested ***transform*** block with:
    - an ***aggregate*** and ***window/rank*** transforms to reduce the dataset to 4 records (top 3 and others)
- a ***shared encoding*** block to order the categories
- an ***arc*** mark with:
    - a fixed ***stroke*** (white, 4px) to slightly separate the "slices"
    - ***conditional colour*** (other=light grey; top 3 set to ***Power BI theme colours***)
    - ***conditional opacity*** based on selected category ID (selected=1; unselected=0.5))

1c - Center Info:
 - a nested ***transform*** block with:
    - 1x ***aggregate*** and ***joinaggregate*** transform to redo the category and total amounts
    - 3x ***calculate*** transforms to determine the category percent of total, category amount/percent label, and total label

1c1 - Viewing Category Label:
- a nested ***transform*** block with:
    - 1x ***calculate*** transform to extract the category ID from the clicked global parameter object
    - 1x ***filter*** transform to keep only the single record for the selected category
- a ***text*** mark with:
    - alignment = center
    - baseline = bottom
    - a *named style*
    - a fixed value

1c2 - Selected Category Name Label:
- a nested ***transform*** block with:
    - 1x ***calculate*** transform to extract the category ID from the clicked global parameter object
    - 1x ***filter*** transform to keep only the single record for the selected category
- a ***text*** mark with:
    - alignment = center
    - baseline = bottom
    - a *named style*
    - the selected category name

1c3 - Selected Category Amount/Percent Label:
- a nested ***transform*** block with:
    - 1x ***calculate*** transform to extract the category ID from the clicked global parameter object
    - 1x ***filter*** transform to keep only the single record for the selected category
- a ***text*** mark with:
    - alignment = center
    - baseline = top
    - a *named style*
    - the category amount/percent label

1c4 - Total Label:
- a nested ***transform*** block with:
    - 1x ***calculate*** transform to extract the category ID from the clicked global parameter object
    - 1x ***filter*** transform to keep only the single record for the selected category
- a ***text*** mark with:
    - alignment = center
    - baseline = top
    - a *named style*
    - the total label

<br>

2 - Slicer:
- a nested ***transform*** block with:
    - 1x ***aggregate*** and ***window/dense_rank*** transforms to reduce the dataset to 4 records (top 3 and others)
    - 1x ***calculate*** transforms to set the "Other" category to a high rank (9)
    - 1x ***window/dense_rank*** transform to redo the category ranks (now that "Other" applied)
    - 2x ***calculate*** transforms to determine the start and end X coordinates of the slicer bars (pills)
    - 1x ***calculate*** transform to extract the category ID from the clicked global parameter object
    - a ***shared encoding*** block to order the categories and ensure all layered mark use the same X coordinates
- a ***layer*** block for the slicer bars, circles, labels, and amounts

2a - Bars:
- a ***params*** block with:
    - a ***point selection*** to respond to the ***click*** event and a ***resolve/global*** key:value pair to make the clicked category parameter available globally so it can be instantiated and used as needed by other marks
- a ***bar*** mark with:
    - ***rounded corners*** (over 1/2 the Y size to cause a ***pill*** display)
    - ***conditional colour*** (selected=black; unselected=light grey)

2b - Circles:
- a ***point/circle*** mark with:
    - ***conditional size*** (selected=100; unselected=80)
    - ***conditional X offset*** (selected=20; unselected=10)
    - ***conditional colour*** (other=light grey; top 3 set to ***Power BI theme colours***)

2c - Labels:
- a ***text*** mark with:
    - ***conditional X offset*** (selected=30; unselected=20)
    - ***conditional font size*** (selected=14; unselected=12)
    - ***conditional font weight*** (selected=bold; unselected=normal)
    - ***conditional font colour*** (selected=white; unselected=black)
    - a ***named style***

2d - Amounts:
- a ***text*** mark with:
    - ***conditional font colour*** (selected=white; unselected=black)
    - value formatting via a ***Power BI format string*** as enabled by Deneb
    - a ***named style***

<br>
  
3 - Config:
- configuration values set for:
    - border (colour [stroke] set to null)
    - title font attributes (family, size, weight, style, colour)
    - subtitle font attributes (family, size, weight, style, colour)
- named styles:
    - donut slice (stroke colour, width)
    - subcategory name font attributes (family, size, weight, style, colour)
    - subcategory amount/percent font attributes (family, size, weight, style, colour)
    - subcategory leader line (colour)
    - subcategory leader line mask (colour)
    - category name font attributes (family, size, weight, style, colour)
    - category amount/percent font attributes (family, size, weight, style, colour)
    - total label font attributes (family, size, weight, style, colour)
    - slicer category name font family
    - slicer category amount font attributes (family, size, weight, style)
 
<hr>

### Links:

Here's the template:

[916.1 - JSON - Deneb Template - Dynamic Sunburst Chart](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/915.1%20-%20deneb_template.financial_waterfall_chart.v1.8.2.json) *** FIX *** <br>

<br>

Here's an example Power BI file using the template:

[916.2 - PBIX - Deneb Example - Dynamic Sunburst Chart](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/915.2%20-%20Deneb%20Reusable%20Components%20-%20Financial%20Waterfall%20Chart%20-%20V1.8.2.pbix) *** FIX *** <br>

*- eof*
