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
      "uuid": "8cb8bc51-a19d-4a63-b7a3-883b84a78b71",
      "generated": "2025-06-23T13:47:50.411Z",
      "previewImageBase64PNG": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR42mNkYAAAAAYAAjCB0C8AAAAASUVORK5CYII=",
      "name": "Space-Saving Bar Chart with Top N and Others",
      "description": "Full-width bar chart with category above bar displaying bars for the top N categories and another aggregated bar for all remaining categories. A ranged screen widget allows selection of the top N value.",
      "author": "Greg Philps"
    },
    "deneb": {
      "build": "1.7.2.1",
      "metaVersion": 1,
      "provider": "vegaLite",
      "providerVersion": "5.20.1"
    },
    "interactivity": {
      "tooltip": true,
      "contextMenu": true,
      "selection": false,
      "selectionMode": "simple",
      "highlight": false,
      "dataPointLimit": 50
    },
    "config": "{\n  \"view\": {\n    \"stroke\": \"transparent\"\n  },\n  \"axisY\": {\n    \"ticks\": false,\n    \"grid\": false,\n    \"domain\": false\n  },\n  \"axisX\": {\n    \"ticks\": false,\n    \"grid\": true,\n    \"domain\": false,\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 12\n  },\n  \"style\": {\n    \"_bar_style\": {\n      \"cornerRadius\": 50\n    },\n    \"_category_text_style\": {\n      \"align\": \"left\",\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 16\n    },\n    \"_data_label_text_style\": {\n      \"align\": \"left\",\n      \"font\": \"Segoe UI\",\n      \"fontSize\": 14\n    }\n  }\n}",
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
  "title": {
    "anchor": "start",
    "align": "left",
    "text": "Space-Saving Bar Chart with Top N and Others",
    "font": "Segoe UI",
    "fontSize": 24,
    "fontStyle": "italic"
  },
  // dataset (from Power BI)
  "data": {
    "name": "dataset"
  },
  "width": 1150,
  "height": 560,
  // extend dataset with rank (to determine opacity)
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
    {
      "calculate": "pad( datum['_category_rank2'], 2, '0', 'left' ) + '-' + datum['_category']",
      "as": "_category_rank_and_label"
    },
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
    {
      "calculate": "toNumber( slice( datum['_category_rank_and_label'], 0, 2 ) )",
      "as": "_category_rank3"
    },
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
    }
  ],
  // common Y encoding outside layer block
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
  // layer block for category (i.e., axis label), bar, and data label
  "layer": [
    {
      "name": "CATEGORY",
      "mark": {
        "type": "text",
        "color": "black",
        "style": "_category_text_style"
      },
      "encoding": {
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
      "name": "BAR",
      "mark": {
        "type": "bar",
        "height": 15,
        "yOffset": 20,
	// use Power BI theme colour #1 for all categories, except for "Other" which uses grey
        "color": {
          "expr": "datum['_category_label3'] != 'Other' ? pbiColor(0) : '#C9C9C9'"
        },
        // use decreasing opacity by rank (higher rank = high opacity, lower rank = low opacity) or full opacity for "Other"		
        "opacity": {
          "expr": "datum['_category_label3'] != 'Other' ? 1 - ( datum['_category_rank3']  / 12 ) : 1"
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
            "labelColor": {
              "expr": "datum.value == 0 ? 'transparent' : '#7D7D7D'"
            },
            "gridColor": {
              "expr": "datum.value == 0 ? 'transparent' : '#C9C9C9'"
            },
            "formatType": "pbiFormat",
            // adjust Power BI format string as necessary to suit data
            "format": "#0,,,. B"
          }
        }
      }
    },
    {
      "name": "DATA_LABEL",
      "mark": {
        "type": "text",
        "color": "black",
        "xOffset": 5,
        "yOffset": 18,
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
          // adjust Power BI format string as necessary to suit data
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
	- conditional colour (for top N, Power BI theme colour 1; grey for *Other*)
	- conditional opacity (for top N, 1 - rank/12; 1 for *Other*)
	- X-axis with 
		- conditional label and grid colour (transparent) to *hide* the zero entry
		- Power BI formatting for the axis labels

3 - Data Label:
- a ***text*** mark using a named style with:
	- an X position of the category aggregate value
	- Power BI formatting for the aggregate value

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

