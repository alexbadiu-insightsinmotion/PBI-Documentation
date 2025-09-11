<img width="1280" height="710" alt="201 - Image - Title - Space-Saving Bar Chart with Top N and Others (d)" src="https://github.com/user-attachments/assets/6adce39d-d142-48e8-b5b0-9eb3850b465b" />

## Space-Saving Bar Chart with Top N and Others

*September 9, 2025*

One characteristic common to the standard horizontal bar charts used in Power BI is that they have a portion of the width used by the Y-axis values, thus reducing the width available for the bars. 

Another characteristic common to the standard horizontal bar charts used in Power BI is that they display all categories (Y values); the visual often only displays a subset of the categories and must be scrolled, so the "big picture" can be lost. What's often of interest, however, is how the top performers are faring against each other and all others.

Deneb can be used to address both of these issues, recovering the lost width by placing the Y-axis values above the bars (instead of beside them) and showing only the top N categories alongside an aggregate of the "others".

I provide a Deneb template for just this situation, a *space-saving bar chart with top N and others*.

https://github.com/user-attachments/assets/c9e34f7e-fe56-44f2-83e0-640aba57776e

<br>

<details closed>
<summary>Here's the template JSON code:</summary>

``` json 
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "information": {
      "uuid": "0ef0b7e8-014b-48d8-a39d-6c71a8c28318",
      "generated": "2025-09-09T16:19:25.425Z",
      "previewImageBase64PNG": "data:image/png;base64,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",
      "name": "Space-Saving Bar Chart with Top N and Others",
      "description": "Full-width bar chart with category above bar displaying bars for the top N categories and another aggregated bar for all remaining categories. A ranged screen widget allows selection of the top N value.",
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
    "config": "{\n  \"view\": {\n    \"stroke\": \"transparent\"\n  },\n  \"axisY\": {\n    \"ticks\": false,\n    \"grid\": false,\n    \"domain\": false\n  },\n  \"axisX\": {\n    \"ticks\": false,\n    \"grid\": true,\n    \"domain\": false,\n    // \"gridColor\": \"#969696\",\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 12\n  },\n  \"style\": {\n    \"_bar_style\": {\n      // any value of above 50% of the bar height will be treated as\n      // 50% of the bar height: set to a large number to always get 50%\n      \"cornerRadiusEnd\": 6\n    },\n    \"_category_text_style\": {\n      \"align\": \"left\",\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 16\n    },\n    \"_data_label_text_style\": {\n      \"align\": \"left\",\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 14\n    }\n  }\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Category",
        "description": "The category to be displayed on the Y axis",
        "kind": "column",
        "type": "text"
      },
      {
        "key": "__1__",
        "name": "Value",
        "description": "The quantitative value to be displayed on the X axis",
        "kind": "measure",
        "type": "numeric"
      }
    ]
  },
  // set the desired width and height to fit the available space on the report page
  "width": 560,
  "height": 530,
  // set the desired padding (0 used to minimize white space)
  "padding": {
    "top": 0,
    "bottom": 0,
    "left": 0,
    "right": 0
  },
  // dataset (from Power BI)
  "data": {
    "name": "dataset"
  },
  // extend dataset with rank (will be used to determine bar height, category text Y offset, and opacity)
  "transform": [
    {
      "window": [
        {
          "op": "dense_rank",
          "as": "_category_rank"
        }
      ],
      "sort": [
        {
          "field": "__1__",
          "order": "descending"
        }
      ]
    },
    {
      "calculate": "if( datum['_category_rank'] > _top_n, 'Other', datum['__0__'] )",
      "as": "_category"
    },
    {
      "calculate": "if( datum['_category'] == 'Other', 99, datum['_category_rank'] )",
      "as": "_category_rank2"
    },
    // compose a composite label (rank-category)
    {
      "calculate": "pad( datum['_category_rank2'], 2, '0', 'left' ) + '-' + datum['_category']",
      "as": "_category_rank_and_label"
    },
    // re-aggregate the dataset using the composite label (shouldn't make a difference, but is worthwhile confirming nonetheless)
    {
      "aggregate": [
        {
          "op": "sum",
          "field": "__1__",
          "as": "_sum_value_by_category"
        }
      ],
      "groupby": [
        "_category_rank_and_label"
      ]
    },
    // extract just the rank from the composite label
    {
      "calculate": "toNumber( slice( datum['_category_rank_and_label'], 0, 2 ) )",
      "as": "_category_rank3"
    },
    // extract just the category from the composite label
    {
      "calculate": "slice( datum['_category_rank_and_label'], 3, 100 )",
      "as": "_category_label3"
    }
  ],
  "params": [
    {
      "name": "_top_n",
      "value": 5,
      "bind": {
        "input": "range",
        "min": 1,
        "max": 10,
        "step": 1,
        "name": "Top N: "
      }
    },
    // adjust the bar height as desired
    {
      "name": "_bar_height",
      "expr": "( 11 - _top_n ) * 6"
    },
    // adjust the Y offset for the category label to suit the bar height parameter calculation
    {
      "name": "_category_text_y_offset",
      "expr": "-1 * ( _bar_height / 2 ) - 10"
    }
  ],
  // locate shared (common) Y encoding outside layer block
  "encoding": {
    "y": {
      "field": "_category_rank_and_label",
      "type": "nominal",
      "axis": null,
      "sort": {
        "op": "sum",
        "field": "_sum_value_by_category",
        "order": "descending"
      }
    }
  },
  // layer block for bar, category (i.e., axis label), and data label
  "layer": [
    {
      "name": "BAR",
      "mark": {
        "type": "bar",
        "height": {
          "expr": "_bar_height"
        },
        "color": {
          "expr": "datum['_category_label3'] != 'Other' ? pbiColor(0) : '#C9C9C9'"
        },
        "opacity": {
          "expr": "datum['_category_label3'] != 'Other' ? 1 - ( datum['_category_rank3']  / 10 ) : 1"
        },
        "style": "_bar_style"
      },
      "encoding": {
        "x": {
          "field": "_sum_value_by_category",
          "type": "quantitative",
          "axis": {
            "title": null,
            "tickCount": 4,
            // don't show the X axis = 0 label (make it transparent)
            "labelColor": {
              "expr": "datum.value == 0 ? 'transparent' : '#C9C9C9'"
            },
            // don't show the X axis = 0 grid line (make it transparent)
            "gridColor": {
              "expr": "datum.value == 0 ? 'transparent' : '#EEEEEE'"
            },
            "formatType": "pbiFormat",
            // adjust Power BI format string as desired to suit dataset
            "format": "#0,,,. B"
          }
        }
      }
    },
    {
      "name": "CATEGORY",
      "mark": {
        "type": "text",
        "color": "black",
        "yOffset": {
          "expr": "_category_text_y_offset"
        },
        "style": "_category_text_style"
      },
      "encoding": {
        // hard-code the X value to 0
        "x": {
          "datum": 0
        },
        "text": {
          "field": "_category_label3",
          "type": "nominal"
        }
      }
    },
    {
      "name": "DATA_LABEL",
      "mark": {
        "type": "text",
        "color": "black",
        "baseline": "middle",
        "xOffset": 5,
        "style": "_data_label_text_style"
      },
      "encoding": {
        "x": {
          "field": "_sum_value_by_category",
          "type": "quantitative"
        },
        "text": {
          "field": "_sum_value_by_category",
          "formatType": "pbiFormat",
          // adjust Power BI format string as desired to suit dataset          
          "format": "#0,,,.0 B"
        }
      }
    }
  ]
}
```

</details>

<br>

This template displays a number of Deneb/Vega-Lite features, including:

0 - General:
- a ***title*** block
- a ***transform*** block with:
	- a ***window/rank*** transform to sort the categories
	- 2x ***calculate*** transforms to set the category of those records outside the top N to *Other* and rank to a high value
	- a ***calculate*** transform to determine the composite Y axis label (rank:category)
	- an ***aggregate/sum*** transform to determine the category value
	- 2x ***calculate*** transforms to extract the rank and category from the composite label
- a ***params*** block with:
	- a range parameter to enable user interaction in the selection of the *Top N* value
- a shared ***encoding*** block to ensure the same Y is used for all layered marks
- a ***layer*** block for the category, bar, and data label

1 - Category:
- a ***text*** mark using a named style with:
	- an X position of zero

2 - Bar:
- a ***bar*** mark using a named style with:
	- ***conditional colour*** (for top N, Power BI theme colour 1; grey for *Other*)
	- ***conditional opacity*** (for top N, 1 - rank/12; 1 for *Other*)
	- X-axis with 
		- ***conditional label and grid colour*** (transparent) to *hide* the zero entry
		- ***Power BI formatting*** for the axis labels

3 - Data Label:
- a ***text*** mark using a named style with:
	- an X position of the category aggregate value
	- ***Power BI formatting*** for the aggregate value

In addition, many configuration values were set in the ***Config*** section, including both axis formats and named styles.

<hr>

### Links:

Here's the template:

[901.1 - JSON - Deneb Template - Space-Saving Bar Chart with Top N and Others](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/901.1%20-%20deneb_template.space_saving_bar_chart_with_top_n_and_others.v1.8.1.json)

<br>

Here's an example Power BI file using the template with two different datasets:
- movie sales by genre
  - after using the template to generate the Deneb visual, the following were adjusted:
    - width changed to 1100 (line 2)
    - height change to 600 (line 3)
- product sales by country
  - after using the template to generate the Deneb visual, the following were adjusted:
    - width changed to 1100 (line 2)
    - height change to 600 (line 3)
    - X-axis format changed to "#0,,. M" (millions) (line 138)
    - data label format changed to "#0,,.0 M" (millions) (line 182)

[901.2 - PBIX - Deneb Example - Space-Saving Bar Chart with Top N and Others](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/901.2%20-%20Deneb%20Reusable%20Components%20-%20Space-Saving%20Bar%20Chart%20with%20Top%20N%20and%20Others%20-%20V1.8.1.pbix)
