
![Issue #21](https://github.com/user-attachments/assets/d39b541e-ef45-48cd-88ca-15466fd1cd82)


# Documenting Power BI bookmarks: From PBIR JSON to clear documentation

Power BI bookmarks are powerful tools for creating interactive reports, but documenting them properly can be challenging. In this post, I'll show you how to extract meaningful documentation from bookmark PBIR JSON files using AI assistance, plus share some important discoveries about how bookmarks actually work.


_You must first enable PBIR in Power BI Desktop preview features: go to **File** > **Options and settings** > **Options** > **Preview features** and check the box next to **“Store reports using enhanced metadata format (PBIR)**”._

PBIR is associated with **Power BI Project files (.pbip)**, which store reports and semantic models in a source-control-friendly folder structure
## The Challenge: Understanding bookmark behavior

When creating bookmarks in Power BI, the UI can be misleading. I discovered this firsthand when analyzing a "**Reset Filters**" bookmark that appeared to apply to "**All Visuals**" in the UI but behaved differently in the JSON.


<img width="516" height="353" alt="Pasted image 20250729162114" src="https://github.com/user-attachments/assets/a127debe-a809-477f-a8a8-4c164b84e07f" />


How I created the bookmark: **I selected all items in the page to make sure it applies to all visuals and pressed Update** with the above settings. 
I then saved the Power BI report under the PBIP Format in a Folder called DemoDataset.

### Key Discovery: "All Visuals" vs "Selected Visuals"

**Here's what I learned about bookmarks that I did not expect:**

- **True "All Visuals"**: No `targetVisualNames` property in JSON - **affects all current AND future visuals**
- **"Selected Visuals"**: `targetVisualNames` property present - **only affects listed visuals**, even if you selected all current visuals when creating it

Let's open this report in Visual Studio Code and have a look at the PBIR bookmark JSON

<img width="375" height="348" alt="Pasted image 20250901131852" src="https://github.com/user-attachments/assets/35b0542f-93cb-44de-8331-8a4b7c679bd2" />


*Open Folder > Chose the folder > DemoDataset*

<img width="695" height="509" alt="Pasted image 20250901132221" src="https://github.com/user-attachments/assets/f35ecebc-18bd-47b2-8552-a484455b9fbe" />



The report definition is stored inside the `definition\` folder with the following structure: (bookmark first, pages and visuals second)
```
├── bookmarks\
│   ├── [bookmarkName].bookmark.json
|   └── bookmarks.json
├── pages\
│   ├── [pageName]\
│   |   ├── \visuals
|   │   |   ├── [visualName]\
|   |   │   │   |── mobile.json
|   |   |   └   └── visual.json
|   |   └── page.json
|   └── pages.json
├── version.json
├── reportExtensions.json
└── report.json
```

<br>

<details closed>
<summary>Here's the full JSON code:</summary>
  
``` json
{
  "$schema": "https://developer.microsoft.com/json-schemas/fabric/item/report/definition/bookmark/1.4.0/schema.json",
  "displayName": "Reset Filters",
  "name": "77f6391b96f7c17022ed",
  "options": {
    "targetVisualNames": [
      "5e6acabae3ac49fd5c3b",
      "bf11a6fb91dc9f853419",
      "ed774ceec96dd040ac19",
      "34f97140074284eaa8de"
    ]
  },
  "explorationState": {
    "version": "1.3",
    "activeSection": "4cb813ea0b6a5c8296b0",
    "filters": {
      "byExpr": [
        {
          "name": "5bf850d4ae79b6122847",
          "type": "Categorical",
          "filter": {
            "Version": 2,
            "From": [
              {
                "Name": "d",
                "Entity": "Date",
                "Type": 0
              }
            ],
            "Where": [
              {
                "Condition": {
                  "In": {
                    "Expressions": [
                      {
                        "Column": {
                          "Expression": {
                            "SourceRef": {
                              "Source": "d"
                            }
                          },
                          "Property": "Year"
                        }
                      }
                    ],
                    "Values": [
                      [
                        {
                          "Literal": {
                            "Value": "2019L"
                          }
                        }
                      ]
                    ]
                  }
                }
              }
            ]
          },
          "expression": {
            "Column": {
              "Expression": {
                "SourceRef": {
                  "Entity": "Date"
                }
              },
              "Property": "Year"
            }
          },
          "howCreated": 1
        }
      ]
    },
    "sections": {
      "4cb813ea0b6a5c8296b0": {
        "visualContainers": {
          "34f97140074284eaa8de": {
            "filters": {
              "byExpr": [
                {
                  "name": "70e95568ae04fa1d4cd0",
                  "type": "Categorical",
                  "expression": {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Continent"
                    }
                  },
                  "howCreated": 0
                },
                {
                  "name": "2a38a5d841d9322e52c4",
                  "type": "Categorical",
                  "expression": {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Country"
                    }
                  },
                  "howCreated": 0
                },
                {
                  "name": "eebd83c6a4a3378e0706",
                  "type": "Advanced",
                  "expression": {
                    "Measure": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Sales"
                        }
                      },
                      "Property": "Sales"
                    }
                  },
                  "howCreated": 0
                },
                {
                  "name": "5f0bc86dfc9a074e9486",
                  "type": "Advanced",
                  "expression": {
                    "Measure": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Sales"
                        }
                      },
                      "Property": "Sales PY"
                    }
                  },
                  "howCreated": 0
                }
              ]
            },
            "singleVisual": {
              "visualType": "clusteredBarChart",
              "objects": {},
              "orderBy": [
                {
                  "Direction": 2,
                  "Expression": {
                    "Measure": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Sales"
                        }
                      },
                      "Property": "Sales"
                    }
                  }
                }
              ],
              "activeProjections": {
                "Category": [
                  {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Continent"
                    }
                  }
                ]
              }
            }
          },
          "ed774ceec96dd040ac19": {
            "filters": {
              "byExpr": [
                {
                  "name": "5edc333a7dbbaa98ba74",
                  "type": "Categorical",
                  "expression": {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Continent"
                    }
                  },
                  "howCreated": 0
                },
                {
                  "name": "ca874f1b83beed1bfc93",
                  "type": "Categorical",
                  "expression": {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Country"
                    }
                  },
                  "howCreated": 0
                },
                {
                  "name": "bf5689a2fa810580a03a",
                  "type": "Advanced",
                  "expression": {
                    "Measure": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Sales"
                        }
                      },
                      "Property": "Sales"
                    }
                  },
                  "howCreated": 0
                },
                {
                  "name": "e7febea5ccadf56781bb",
                  "type": "Advanced",
                  "expression": {
                    "Measure": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Sales"
                        }
                      },
                      "Property": "Sales PY"
                    }
                  },
                  "howCreated": 0
                }
              ]
            },
            "singleVisual": {
              "visualType": "ribbonChart",
              "objects": {},
              "orderBy": [
                {
                  "Direction": 1,
                  "Expression": {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Continent"
                    }
                  }
                },
                {
                  "Direction": 1,
                  "Expression": {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Country"
                    }
                  }
                }
              ],
              "activeProjections": {
                "Category": [
                  {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Continent"
                    }
                  }
                ]
              },
              "display": {
                "mode": "hidden"
              }
            }
          },
          "bf11a6fb91dc9f853419": {
            "filters": {
              "byExpr": [
                {
                  "name": "23c698b6efa81dc92f5c",
                  "type": "Categorical",
                  "expression": {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Gender"
                    }
                  },
                  "howCreated": 0
                }
              ]
            },
            "singleVisual": {
              "visualType": "slicer",
              "objects": {
                "merge": {
                  "general": [
                    {
                      "properties": {
                        "filter": {
                          "filter": {
                            "Version": 2,
                            "From": [
                              {
                                "Name": "c",
                                "Entity": "Customer",
                                "Type": 0
                              }
                            ],
                            "Where": [
                              {
                                "Condition": {
                                  "Contains": {
                                    "Left": {
                                      "Column": {
                                        "Expression": {
                                          "SourceRef": {
                                            "Source": "c"
                                          }
                                        },
                                        "Property": "Gender"
                                      }
                                    },
                                    "Right": {
                                      "Literal": {
                                        "Value": "'Ma'"
                                      }
                                    }
                                  }
                                }
                              }
                            ]
                          }
                        }
                      }
                    }
                  ],
                  "data": [
                    {
                      "properties": {
                        "mode": {
                          "expr": {
                            "Literal": {
                              "Value": "'Basic'"
                            }
                          }
                        }
                      }
                    }
                  ]
                }
              },
              "activeProjections": {
                "Values": [
                  {
                    "Column": {
                      "Expression": {
                        "SourceRef": {
                          "Entity": "Customer"
                        }
                      },
                      "Property": "Gender"
                    }
                  }
                ]
              }
            }
          }
        }
      }
    },
    "objects": {}
  }
}
```
</details>

<br>

This is interesting. Even though the Power BI UI shows a checkmark indicating the bookmark impacts "All visuals," it actually affects only the visuals that were on the page when the bookmark was created.

```json
// This bookmark only affects the listed visuals
"options": {
  "targetVisualNames": [
    "5e6acabae3ac49fd5c3b",
    "bf11a6fb91dc9f853419",
    "ed774ceec96dd040ac19",
    "34f97140074284eaa8de"
  ]
}
```

>[!NOTE]
**Important Note**: Filter states (Data) are always applied to all visuals on the page, regardless of the `targetVisualNames` setting. The `targetVisualNames` property only limits which visuals receive Display/Selection changes.

Now that we learned this, let's move forward and see how we can leverage PBIR and Github Copilot (or other LLM models) to document better our bookmarks.
## My documentation workflow

### Step 1: Identify the Bookmark JSON to document

Using Visual Studio Code, I can easily access the bookmark's JSON structure.

### Step 2: Add the bookmark and the page to the AI context chat in Visual Studio Code


<img width="608" height="599" alt="Pasted image 20250729160823" src="https://github.com/user-attachments/assets/a8731b20-0579-4545-a7ec-687202bab855" />



### Step 3: Choose your LLM of choice
<img width="257" height="142" alt="Pasted image 20250901134123" src="https://github.com/user-attachments/assets/d649c9c3-5ef5-4ce2-bde4-af6638373483" />



### Step 4: Add the following prompt

I developed this prompt to systematically analyze bookmark JSON files:

```
What can you tell me about this bookmark to help me document it?

1. **What is the bookmark’s name?**
    - Use the `displayName` property for the bookmark name.
      
2. **Is the bookmark part of a group?**
    - If so, provide the group name using the `parentGroupName` property.
      
3. **Which settings were selected for the bookmark?**
    - Indicate if the bookmark stores **Data**, **Display**, **Current Page**, and whether it applies to **All Visuals** or **Selected Visuals**.
      
4. **If Selected Visuals:**
    - Create a mapping from each visual ID in `targetVisualNames` to its:
        - `displayName` (from the visual’s JSON)
        - `visualType` (from the visual’s JSON)
        - `parentGroupName` (if available, for context/grouping)
        - **Visibility status** (Visible or Hidden, based on the visual’s display properties)
    - Output this mapping as a Markdown table.
      
5. **Add a summary table:**
    - Use the following format:
    
    |Bookmark Name|Group Name|Data|Display|Current Page|All Visuals|Selected Visuals|Visuals Included (ID: Status)|
    |---|---|---|---|---|---|---|---|
    
1. **Filter Details:**
    - List all filters stored by the bookmark, both at the report and visual level, in plain language.  
        For each filter, specify:
        - The field(s) being filtered (e.g., `Date[Year]`)
        - The filter type (e.g., categorical, advanced)
        - The value(s) or condition(s) being applied (e.g., equals 2019, contains 'Ma')
    - Summarize what activating the bookmark will do to the report’s filters in a human-readable way.
```


### Results: Generated Documentation Example

For my "Reset Filters" bookmark, this process generated:

**Bookmark Settings:**

- **Data:** Yes (the `filters` and `explorationState` are present)
- **Display:** Yes (the `singleVisual.display` property is present for at least one visual)
- **Current Page:** Yes (the `activeSection` property is set)
- **All Visuals:** <mark> No </mark> (the `options.targetVisualNames` array is present, so only selected visuals are included)
- **Selected Visuals:** Yes (the bookmark targets specific visuals by ID)

**Visual Mapping:**

| Visual ID            | Display Name        | Visual Type       |
| -------------------- | ------------------- | ----------------- |
| 5e6acabae3ac49fd5c3b | Bookmark            | Group (Bookmark)  |
| bf11a6fb91dc9f853419 | <mark>(not specified)</mark> | slicer            |
| ed774ceec96dd040ac19 | Ribbon Chart        | ribbonChart       |
| 34f97140074284eaa8de | Clustered Bar Chart | clusteredBarChart |

## Best Practices to follow

### 1. Always rename your visuals

**Before:**

```json
"displayName": "(not specified)"
```

**After:**

```json
"displayName": "Gender Filter Slicer"
```

This makes documentation infinitely more useful and helps with future maintenance.

### 2. Use meaningful bookmark names

Instead of "Bookmark1", use descriptive names like:

- `ResetFilters`
- `ShowDetailView`
- `ToggleQuarterlySummary`

### 3. Leverage bookmark groups

Organize related bookmarks into groups. The group names appear in the JSON as `parentGroupName` and help structure your documentation.

### 4. Test bookmark behavior after adding new Visuals

Add a new visual after creating your bookmark and test the behavior. This will reveal whether your bookmark truly applies to "all visuals" or just the selected ones.

**I did this exercise to 'test' what I learned. I added a new visual (scatter chart) and hid it on the page**
<img width="1945" height="598" alt="Pasted image 20250729171021" src="https://github.com/user-attachments/assets/ec781a59-d2f3-409e-9ec1-3800b12bd38a" />



**When I navigate to other bookmarks and back to Reset Filters I see again the visual.**

<img width="969" height="389" alt="Pasted image 20250729171117" src="https://github.com/user-attachments/assets/6ebc3ee2-4c8f-4c8d-b92d-dc43ac4a8a3e" />


**Observation:**
- **Reset Filters** bookmark includes Display settings for specific visuals (those listed in `targetVisualNames`).
- When adding a **new scatter chart**, hiding it, then clicking the bookmark "Reset Filters", the scatter chart **becomes visible** again.


> [!tip]
>**Note:** In Power BI, Data (filter) states in bookmarks are applied to all visuals on the page, regardless of the `targetVisualNames` setting. The `targetVisualNames` property only limits which visuals receive Display/Selection changes.


> [!tip]
>**You cannot create true "All visuals" bookmarks through the Power BI UI.** The only way to achieve this is by manually editing the JSON file



### 5. Build only a limited number of bookmarks

**Rule of thumb:** If you need more than one hand to count your bookmarks on a single page, you probably need to simplify your design.

**Consider alternatives first:**

- **Field parameters:** For switching between different measures or columns, field parameters are often simpler and better than multiple bookmarks
- **Drill-through pages:** For detailed analysis instead of bookmark-driven view changes
- **Page navigation:** Multiple focused pages instead of one complex bookmark-heavy page
- **Translytical Task Flows:** For more complex analytical workflows use Translytical Task Flows (see my Translytical Task Flow challenge entry for advanced techniques [here](https://community.fabric.microsoft.com/t5/Translytical-Task-Flow-Gallery/Dynamic-Power-BI-Experiences/td-p/4808192) )  


### Bonus: Advanced example - complex bookmark analysis

To further demonstrate the power of this documentation approach, I tested it on a more sophisticated bookmark that would have been much trickier to document manually. 


**Details**: There selection on the Gender slicer is set to "Male". The clustered bar chart is filtered to "North America". There is no visibility selection on the ribbon chart. This means that when the user navigates to the "RibbonChart" bookmark and then back to the "FocusSpecific" bookmark, instead of seeing the clustered bar chart, he/she will see the ribbon chart filtered on "North America". A filter applied to all pages for the year 2019 completes this complex bookmark behavior.

<img width="1060" height="398" alt="Pasted image 20250729175157" src="https://github.com/user-attachments/assets/89465279-75ee-457b-b070-7ff6dc77b0fb" />



'FocusSpecific' changes when we navigate to the 'Ribbon Chart' bookmark first and then back to 'FocusSpecific'
<img width="569" height="439" alt="Pasted image 20250902171223" src="https://github.com/user-attachments/assets/6b78cbe6-6750-442c-a1eb-5e724868b380" />





<br>

<details closed>
<summary>AI Analysis: Detailed breakdown of the 'FocusSpecific' bookmark:</summary>

---

### 1. **Bookmark Name**

- **FocusSpecific**

### 2. **Is the bookmark part of a group?**

- **No** (`parentGroupName` property is not present)

### 3. **Bookmark Settings**

- **Data:** Yes (filters and slicer states are stored)
- **Display:** Yes (visual visibility and order are stored)
- **Current Page:** Yes (the active section is set)
- **All Visuals:** No
- **Selected Visuals:** Yes (applies only to visuals listed in `targetVisualNames`)

### 4. **Selected Visuals Mapping**

| Visual ID            | Display Name        | Visual Type       | Parent Group Name    | Visibility |
| -------------------- | ------------------- | ----------------- | -------------------- | ---------- |
| bf11a6fb91dc9f853419 | Slicer Gender       | slicer            | _(none)_             | Visible    |
| 34f97140074284eaa8de | Clustered Bar Chart | clusteredBarChart | 5e6acabae3ac49fd5c3b | Visible    |

- **Display Name**: From the `title` property in each visual’s JSON.
- **Visual Type**: From the `visualType` property.
- **Parent Group Name**: From the `parentGroupName` property if present.
- **Visibility**: Both visuals are visible (no hidden display mode set).

### 5. **Summary Table**

|Bookmark Name|Group Name|Data|Display|Current Page|All Visuals|Selected Visuals|Visuals Included (ID: Status)|
|---|---|---|---|---|---|---|---|
|FocusSpecific|_(none)_|Yes|Yes|Yes|No|Yes|bf11a6fb91dc9f853419: Visible, 34f97140074284eaa8de: Visible|

### 6. **Filter Details**

#### **Report-Level Filter**

- **Field:** `Date[Year]`
- **Type:** Categorical
- **Value:** Equals 2019

#### **Visual-Level Filters**

**Clustered Bar Chart (`34f97140074284eaa8de`):**

- **Continent** (`Customer[Continent]`): Categorical, no value specified (default state)
- **Country** (`Customer[Country]`): Categorical, no value specified (default state)
- **Sales** (`Sales[Sales]`): Advanced, no value specified (default state)
- **Sales PY** (`Sales[Sales PY]`): Advanced, no value specified (default state)
- **Highlight:** North America is selected for `Customer[Continent]` (the chart is highlighted for this value).

**Slicer Gender (`bf11a6fb91dc9f853419`):**

- **Gender** (`Customer[Gender]`): Categorical, filtered to **Male** only.

---

### **Summary of Bookmark Effect**

Activating the **FocusSpecific** bookmark will:

- Set the report to **Page 1**.
- Apply a report-level filter to show only data for **Year = 2019**.
- Limit its effect to two visuals:
    - **Slicer Gender**: Filters the data to only show **Male** customers.
    - **Clustered Bar Chart**: Highlights the **North America** continent, with all other filters at their default state.
- All other visuals remain unaffected by this bookmark.

</details>

<br>


### 5. The Documentation template (manual)

This represents a substantial amount of new information we can leverage using PBIR to enhance our documentation. 
Imagine inheriting a report with these types of bookmarks.
- How would you know which visuals they impact?
- How would you determine if a bookmark behaves as expected?

> [!tip]
>**When using bookmarks, we don't store a description field anywhere**. I believe this presents a phenomenal opportunity to create this type of field when generating bookmarks from the Power BI Desktop UI and store the definition in PBIR. While it would still require manual input, this documentation would be created directly in the source system, which is the best and most accessible kind of documentation. 
**I've submitted a Power BI idea here**: [Add Description field for Bookmarks in Power BI Desktop and PBIR Format](https://community.fabric.microsoft.com/t5/Fabric-Ideas/Add-Description-field-for-Bookmarks-in-Power-BI-Desktop-and-PBIR/idi-p/4818843#M163577). 
If this concept resonates with you, please vote.

In the meantime, let's think about what's missing from the generated documentation - <br> 
**The context, of course.** <br>
For example, when the user navigates to the "RibbonChart" bookmark an back to the "FocusSpecific" bookmark, instead of the Clustered Bar Chart the end user will see the Ribbon Chart instead filtered on "North America". 
We do not see this information written down anywhere. 
- Did we create this boorkmark behavior on purpose?
- Was it part of the Definition of Done?
- Why did we create this bookmark in the first place
- When was it created, what problem was it intended to solve?
- Were other solutions envisaged?
- Was it signed off?
- Where can I find the documentation of the request or the Definition of Done?

What am I missing here is the why. It's beyond the technical part. It's undertanding the problem we need to solve and the approach we decided to take. 

My recommendation is to:
**Create separate documentation for the "why" outside Power BI** (Excel spreadsheet, markdown file, etc.) where you manually add descriptions for each bookmark and list which visuals they affect. The bookmark will become the connecting link between your external documentation and the automatically extracted JSON data (documentation from PBIR).

This hybrid approach gives you both the technical accuracy of the behavior of the bookrmark from the JSON file and the context that only human insight can provide.


## Key takeaways

1. **Don't trust the UI completely** - Always verify bookmark behavior by examining the JSON
2. **Name everything meaningfully** - Your future self (and AI assistants) will thank you
3. **Test with new visuals** - This reveals the true scope of your bookmarks
4. **Use AI to automate analysis** - The JSON structure is complex, but AI can parse it efficiently
5. **Document as you go** - Don't wait until you have dozens of undocumented bookmarks

## Conclusion

**The AI prompt I've shared will automate bookmark documentation to an unprecedented level** : it helps extracting what I consider, the most important information about bookmarks. However, automation alone isn't enough for truly useful documentation.

**The human element remains crucial.** Only you can provide the context that makes documentation valuable: _Why_ was this bookmark created? _When_ should users apply it? _What_ business scenario does it address? _Who_ validated it and in which context?  

**Think of this as a foundation, not the finish line.** The automated extraction gives you the technical skeleton and now you add the business context that makes it meaningful. I hope the approach I've shared here starts you on that journey toward comprehensive, clear and context-rich bookmark documentation.

_Have you discovered any other interesting things about Power BI bookmark behavior? Do you have any ideas for how the prompt I used can be improved? I'd love to hear about your experiences in the comments._

