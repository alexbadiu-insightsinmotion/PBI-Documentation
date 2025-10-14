<img width="1280" height="640" alt="107 - Image - Title - Dark Themes" src="https://github.com/user-attachments/assets/c0501c05-2964-4cc6-b526-0aea959b9b3c" />

## Dark Themes

A new Power BI report will use a *light theme* by default. This issue describes a set of steps that can be used to create a *dark theme* in a Power BI report.

### Page Background

The *page background* colour of a Power BI report can be controlled by the ***background*** block in the ***visualStyles*** object.

```json
{
  "name": "Example Dark Theme - Step 1 - Page Background Colour",
  "dataColors": ["#70B0E0", "#FCB714", "#2878BD", "#0EB194", "#108372", "#AF916D", "#C4B07B", "#F15628"],
  "visualStyles": {
    "*": {
      "*": {
        // DEVELOPMENT NOTE: set the page background colour
        "background": [{ "color": { "solid": { "color": "#080831" } } }]
      }
    }
  }
}
```

<br>

### Table and Matrix Background Colour

The background colour of *tables* and *matrices* in a Power BI report can be controlled by the ***background*** property.

```json
{
  "name": "Example Dark Theme - Step 2 - Table and Matrix Background Colour",
  "dataColors": ["#70B0E0", "#FCB714", "#2878BD", "#0EB194", "#108372", "#AF916D", "#C4B07B", "#F15628"],
  // DEVELOPMENT NOTE: set the background colour for tables and matrices
  "background": "#080831",
  "visualStyles": {
    "*": {
      "*": {
        "background": [{ "color": { "solid": { "color": "#080831" } } }]
      }
    }
  }
}
```
<br>

### Text Colour

The text colours must be set to a light colour to be visible in a dark theme.

The text attributes in *visual titles* can be controlled by the ***largeTitle*** block in the ***textClasses*** object.

```json
{
  "name": "Example Dark Theme - Step 3 - Visual Titles Colour",
  "dataColors": ["#70B0E0", "#FCB714", "#2878BD", "#0EB194", "#108372", "#AF916D", "#C4B07B", "#F15628"],
  "background": "#080831",
  "textClasses": {
    // DEVELOPMENT NOTE: set the text attributes of visual titles
    "largeTitle": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 13,
      "color": "#FFFFFF"
    }
  },  
  "visualStyles": {
    "*": {
      "*": {
        "background": [{ "color": { "solid": { "color": "#080831" } } }]
      }
    }
  }
}
```

<br>

The text attributes in *axis titles* and *slicer headers* can be controlled by the ***title*** block in the ***textClasses*** object.

```json
{
  "name": "Example Dark Theme - Step 4 - Axis Titles and Slicer Headers Colours",
  "dataColors": ["#70B0E0", "#FCB714", "#2878BD", "#0EB194", "#108372", "#AF916D", "#C4B07B", "#F15628"],
  "background": "#080831",
  "textClasses": {
    "largeTitle": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 13,
      "color": "#FFFFFF"
    },
    // DEVELOPMENT NOTE: set the text attributes of axis titles and slicer headers
    "title": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 10,
      "color": "#FFFFFF"
    }
  },
  "visualStyles": {
    "*": {
      "*": {
        "background": [{ "color": { "solid": { "color": "#080831" } } }]
      }
    }
  }
}

```

<br>

The text attributes in *text boxes* (*smart narratives*) and the *table* and *matrix* total lines can be controlled by the ***label*** block in the ***textClasses*** object, while the text attributes of the *callout* values in *Card* visuals can be controlled by the ***callout*** block in the ***textClasses*** object.

```json
{
  "name": "Example Dark Theme - Step 5 - Text Box Text Colour, Table and Matix Totals Colour, and Card Callout Colour",
  "dataColors": ["#70B0E0", "#FCB714", "#2878BD", "#0EB194", "#108372", "#AF916D", "#C4B07B", "#F15628"],
  "background": "#080831",
  "textClasses": {
    "largeTitle": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 13,
      "color": "#FFFFFF"
    },
    "title": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 10,
      "color": "#FFFFFF"
    },
    // DEVELOPMENT NOTE: set the text attributes of text boxes (smart narratives) and total lines in table and matrix visuals
    "label": {
      "fontFace": "Segoe UI",
      "fontSize": 10,
      "color": "#FFFFFF"
    },
    // DEVELOPMENT NOTE: set the text attributes of callout values in card visuals
    "callout": {
      "fontFace": "Segoe UI",
      "fontSize": 18,
      "color": "#FFFFFF"
    }
  },
  "visualStyles": {
    "*": {
      "*": {
        "background": [{ "color": { "solid": { "color": "#080831" } } }]
      }
    }
  }
}

```

<br>

The text colour of the *axis labels*, *legend labels*, and *data labels* in circular chart visuals (pie, donut) can be controlled by the ***firstLevelElements*** and *** secondLevelElements*** properties.

```json
{
  "name": "Example Dark Theme - Step 6 - Axis Labels Colour, Legend Label Colour, and Circular Chart Data Label Colour",
  "dataColors": ["#70B0E0", "#FCB714", "#2878BD", "#0EB194", "#108372", "#AF916D", "#C4B07B", "#F15628"],
  "background": "#080831",
  // DEVELOPMENT NOTE: set the text colour of axis labels, legend labels, and circular chart data labels
  "firstLevelElements": "#FFFFFF",
  "secondLevelElements": "#F0F0F0",
  "textClasses": {
    "largeTitle": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 13,
      "color": "#FFFFFF"
    },
    "title": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 10,
      "color": "#FFFFFF"
    },
    "label": {
      "fontFace": "Segoe UI",
      "fontSize": 10,
      "color": "#FFFFFF"
    },
    "callout": {
      "fontFace": "Segoe UI",
      "fontSize": 18,
      "color": "#FFFFFF"
    }
  },
  "visualStyles": {
    "*": {
      "*": {
        "background": [{ "color": { "solid": { "color": "#080831" } } }]
      }
    }
  }
}

```
### Table and Matrix Divider Colour

The *divider line* colour below the column headers and above the totals in *table* visuals can be controlled by the ***columnHeaders*** and ***total*** blocks in the ***tableEx*** block in the ***visualStyles*** object.

The *divider line* colour below the column headers and to the right of the row headers in *matrix* visuals can be controlled by the ***columnHeaders*** and ***rowHeaders*** blocks in the ***pivotTable*** block in the ***visualStyles*** object.

```json
{
  "name": "Example Dark Theme - Step 7 - Table and Matrix Header and Total Divider Line Colour",
  "dataColors": ["#70B0E0", "#FCB714", "#2878BD", "#0EB194", "#108372", "#AF916D", "#C4B07B", "#F15628"],
  "background": "#080831",
  "firstLevelElements": "#FFFFFF",
  "secondLevelElements": "#F0F0F0",
  "textClasses": {
    "largeTitle": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 13,
      "color": "#FFFFFF"
    },
    "title": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 10,
      "color": "#FFFFFF"
    },
    "label": {
      "fontFace": "Segoe UI",
      "fontSize": 10,
      "color": "#FFFFFF"
    },
    "callout": {
      "fontFace": "Segoe UI",
      "fontSize": 18,
      "color": "#FFFFFF"
    }
  },
  "visualStyles": {
    "*": {
      "*": {
        "background": [{ "color": { "solid": { "color": "#080831" } } }]
      }
    },
    "tableEx": {
      "*": {
        "columnHeaders": [
          {
            // DEVELOPMENT NOTE: set the divider line below the column headers in the table visual
            "outlineColor": {
              "solid": {
                "color": "#F0F0F0"
              }
            },
            "outlineStyle": 4
          }
        ],
        "total": [
          {
            // DEVELOPMENT NOTE: set the divider line above the totals in the table visual
            "outlineColor": {
              "solid": {
                "color": "#F0F0F0"
              }
            },
            "outlineWeight": 1,
            "outlineStyle": 1
          }
        ]
      }
    },
    "pivotTable": {
      "*": {
        "columnHeaders": [
          {
            // DEVELOPMENT NOTE: set the divider line below the column headers in the matrix visual
            "outlineColor": {
              "solid": {
                "color": "#F0F0F0"
              }
            },
            "outlineStyle": 4
          }
        ],
        "rowHeaders": [
          {
            // DEVELOPMENT NOTE: set the divider line to the right of the row headers in the matrix visual
            "outlineColor": {
              "solid": {
                "color": "#F0F0F0"
              }
            },
            "outlineStyle": 2
          }
        ]
      }
    }
  }
}
```

<br>

### Filter Pane

The background and text colours of the *Filter Pane* can be controlled by the ***backgroundColor*** and ***foregroundColor*** blocks in the ***outspacePane*** block in the ***page*** block in the ***visualStyles*** object.


``` json
{
  "name": "Example Dark Theme - Step 8 - Filter Pane Text and Background Colours",
  "dataColors": ["#70B0E0", "#FCB714", "#2878BD", "#0EB194", "#108372", "#AF916D", "#C4B07B", "#F15628"],
  "background": "#080831",
  "firstLevelElements": "#FFFFFF",
  "secondLevelElements": "#F0F0F0",
  "textClasses": {
    "largeTitle": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 13,
      "color": "#FFFFFF"
    },
    "title": {
      "fontFace": "Segoe UI Semibold",
      "fontSize": 10,
      "color": "#FFFFFF"
    },
    "label": {
      "fontFace": "Segoe UI",
      "fontSize": 10,
      "color": "#FFFFFF"
    },
    "callout": {
      "fontFace": "Segoe UI",
      "fontSize": 18,
      "color": "#FFFFFF"
    }
  },
  "visualStyles": {
    "*": {
      "*": {
        "background": [
          {
            "show": true,
            "color": { "solid": { "color": "#080831" } },
            "transparency": 25
          }
        ]
      }
    },
    "page": {
      "*": {
        "background": [
          {
            "color": { "solid": { "color": "#080831" } },

            "transparency": 0
          }
        ],
        "outspace": [
          {
            "color": { "solid": { "color": "#080831" } },
            "transparency": 0
          }
        ],
        "outspacePane": [
          {
            // DEVELOPMENT NOTE: set the background and text colours for the filter pane
            "backgroundColor": { "solid": { "color": "#090935" } },
            "foregroundColor": { "solid": { "color": "#FFFFFF" } },
            "fontFamily": "Segoe UI",
            "titleSize": 18,
            "headerSize": 8,
            "transparency": 0,
            "border": true
          }
        ]
      }
    },
    "tableEx": {
      "*": {
        "columnHeaders": [
          {
            "outlineColor": {
              "solid": {
                "color": "#F0F0F0"
              }
            },
            "outlineStyle": 4
          }
        ],
        "total": [
          {
            "outlineColor": {
              "solid": {
                "color": "#F0F0F0"
              }
            },
            "outlineWeight": 1,
            "outlineStyle": 1
          }
        ]
      }
    },
    "pivotTable": {
      "*": {
        "columnHeaders": [
          {
            "outlineColor": {
              "solid": {
                "color": "#F0F0F0"
              }
            },
            "outlineStyle": 4
          }
        ],
        "rowHeaders": [
          {
            "outlineColor": {
              "solid": {
                "color": "#F0F0F0"
              }
            },
            "outlineStyle": 2
          }
        ]
      }
    }
  }
}

```

<br>

## Resources

*LinkedIn Posts*

The LinkedIn posts covering specific areas of the Power BI theme file are listed below: <br>
[101 - How do you specify Global Attributes in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7368600915009830912-wb3Z) <br>
[102 - How do you specify Bar, Column, Line, and Area Charts in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7371153792802897920-ZqnK) <br>
[103 - How do you specify Circular Charts and Cards in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7373669687638859777-KZTg) <br>
[104 - How do you specify Slicers, Tables and Matrices in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7376225981377957889-8ayy) <br>
[105 - How do you specify Other Native Visuals and Custom Visuals in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7378735827834650624-WX5F) <br>
[106 - How do you enable and use Organizational Themes in Power BI?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7381300506129825793-qOkk) <br>
[107 - How do you specify Dark Themes in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7378735827834650624-WX5F) *** FIX *** <br>

*Samples*

Sample theme fragments covering specific areas of the Power BI theme file are available in the GitHub repo: <br>

[901 - Power BI Theme Fragment - Base 1 - Name.json](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/901%20-%20Power%20BI%20Theme%20Fragment%20-%20Base%201%20-%20Name.json) <br>
[902 - Power BI Theme Fragment - Base 2 - Global Colours.json](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/902%20-%20Power%20BI%20Theme%20Fragment%20-%20Base%202%20-%20Global%20Colours.json) <br>
[903 - Power BI Theme Fragment - Base 3 - Global Page Attributes.json](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/903%20-%20Power%20BI%20Theme%20Fragment%20-%20Base%203%20-%20Global%20Page%20Attributes.json) <br>
[904 - Power BI Theme Fragment - Base 4 - Global Visual Attributes.json](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/904%20-%20Power%20BI%20Theme%20Fragment%20-%20Base%204%20-%20Global%20Visual%20Attributes.json) <br>
[905 - Power BI Theme Fragment - Bar and Column Charts](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/905%20-%20Power%20BI%20Theme%20Fragment%20-%20Bar%20and%20Column%20Charts.json) <br>
[906 - Power BI Theme Fragment - Line and Area Charts](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/906%20-%20Power%20BI%20Theme%20Fragment%20-%20Line%20and%20Area%20Charts.json) <br>
[907 - Power BI Theme Fragment - Circular Charts](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/907%20-%20Power%20BI%20Theme%20Fragment%20-%20Circular%20Charts.json) <br>
[908 - Power BI Theme Fragment - Cards](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/908%20-%20Power%20BI%20Theme%20Fragment%20-%20Cards.json) <br>
[909 - Power BI Theme Fragment - Slicers](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/909%20-%20Power%20BI%20Theme%20Fragment%20-%20Slicers.json) <br>
[910 - Power BI Theme Fragment - Tables and Matrices](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/910%20-%20Power%20BI%20Theme%20Fragment%20-%20Tables%20and%20Matrices.json) <br>
[911 - Power BI Theme Fragment - Other Native Visuals](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/911%20-%20Power%20BI%20Theme%20Fragment%20-%20Other.json) <br>
[912 - Power BI Theme Fragment - Custom Visuals](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/912%20-%20Power%20BI%20Theme%20Fragment%20-%20Custom%20Visuals.json) <br>
[913 - Power BI Theme Fragment - Dark Themes](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/912%20-%20Power%20BI%20Theme%20Fragment%20-%20Custom%20Visuals.json) *** FIX *** <br>

*-- eof*
