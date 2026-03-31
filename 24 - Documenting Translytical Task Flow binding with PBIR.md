
**Translytical Task Flows are GA, but documenting how they're wired is not that simple.**

Fabcon Atlanta 2026 made it official. Translytical Task Flows, action buttons that invoke Fabric User-Defined Functions from Power BI,are now generally available. That means we need to anticipate real use, in production reports, and maintenance operations.

Here is a realistic scenario. You inherit one of these reports, created by another colleague. The UDF logic has changed. You need to add a new DAX-based dynamic parameter. You open the report, find the action button, and realize: there is no clear view of what is bound to what. The UI does not expose it. One wrong click on the **fx** button and every binding is gone.

The binding map is not lost. It is distributed across the PBIR report definition and the semantic model TMDL files. This article shows you how to reconstruct it in full, and six practices that make every future report self-documenting. Let's dive in.



### Why the UI won't help you

<img width="1623" height="1161" alt="Pasted image 20260330170920" src="https://github.com/user-attachments/assets/056ee44f-4e2a-4105-960e-b2238008721f" />


The report looks clean. Action buttons on the page. A Format pane on the right. You navigate to the Action section and find the Data Function **fx** button.

<img width="176" height="595" alt="Pasted image 20260330171207" src="https://github.com/user-attachments/assets/9ec06b11-cb95-435f-a3ac-3a141b0bc00f" />


You can click it and select the User Data Function, assuming you already know which one to choose.

<img width="1088" height="426" alt="Pasted image 20260330171257" src="https://github.com/user-attachments/assets/3318b108-ab32-4080-b0fe-d1b6fbe86a02" />


<img width="164" height="937" alt="Pasted image 20260330171937" src="https://github.com/user-attachments/assets/ba9cbb27-4795-4a78-adc6-f495b3883134" />


**The risk is immediate.** Clicking that button resets the binding. Every parameter configuration you did not document is gone. You are starting from scratch.

> [!IMPORTANT]
> You can't control what you don't understand, and you can't understand what you don't observe.

The natural instinct is to look inside the PBIR JSON. The bindings must be stored somewhere in `visual.json`.

<img width="551" height="669" alt="Pasted image 20260330174246" src="https://github.com/user-attachments/assets/9e09781c-dae4-4612-89c3-e0a3cb3bed75" />


They are not directly there.

Searching `visual.json` for the button GUID (`59f8b15373dbadd47ff9`, the `actionButton` named `btn_ReviewNextSegment`) confirms it: `"parameters": []` is always empty. **PBIR does not persist UDF parameter bindings.** This is not a misconfiguration, nor a bug. The binding data is not stored in that field.



### The Resolution: Reconstruct the full binding map

The binding map exists. It is just distributed. The write-back table schema reveals the expected UDF parameters. The page visuals reveal the binding sources. The TMDL measures reveal the logic. You only need to know where to look.

Here is the exact prompt I use. Drop it into any new AI session. Replace the two placeholders. The AI does the rest.

```
I have a Power BI PBIP project. I need you to fully document the UDF (Data Function) parameter bindings for one action button, discovering everything from the PBIR JSON and semantic model files. Assume we know nothing about the parameters upfront.

Working directory: <PBIP_ROOT> ← replace with the actual path
Button visual GUID: <VISUAL_GUID> ← replace with the visual ID (e.g. 59f8b15373dbadd47ff9)

Please follow these steps exactly, using ONLY the local PBIR/TMDL files:

STEP 1: Locate the button
Search all visual.json files under <PBIP_ROOT>/**.Report/definition/pages/_/visuals/_/visual.json for the file whose "name" field equals <VISUAL_GUID>. Confirm it is a DataFunction-type action button (visualLink.type = 'DataFunction'). Note: "parameters": [] being empty is expected. PBIR does not persist UDF bindings.

STEP 2: Identify the write-back table
Look for tables in <PBIP_ROOT>/**.SemanticModel/definition/tables/ that are likely write-back buffers. Signals to look for:
• Table names containing "Buffer", "Submission", "WriteBk", or "Staging"
• Measures using USERPRINCIPALNAME() (signals the UPN is written back)
• Columns like CountryID, Status, SavedDateTime, SubmittedBy
Read the best candidate table's .tmdl file and list ALL its columns with data types. These columns are the candidate UDF parameters (the fields written by the UDF).

STEP 3: Identify the page and all its visuals
From the button's visual.json path, extract the page GUID. Read all visual.json files on the same page. For each visual, extract:
• visual name (GUID)
• visualType
• title (from visualContainerObjects.title)
• all query field projections (queryRef, nativeQueryRef, Entity, Property)

STEP 4: Map write-back columns to page visuals and measures
For each column of the write-back table, find the most likely source on the page:
a) Slicer visuals (advancedSlicerVisual, slicer, textSlicer) → match by field Entity/Property
b) fx measures in KeyMeasures.tmdl → match by:
   • USERPRINCIPALNAME() → userUpn-type param
   • SELECTEDVALUE(DimX[Key]) → ID/key-type params
   • SUM / CALCULATE aggregates → amount/volume params
c) Numeric parameter slicers (tables generating 0–N series) → percentage/rate params

STEP 5: Produce the final parameter table
Output a markdown table with columns:
| UDF Parameter Name | Binding Type | Power BI Object Name | Visual GUID | Measure / Column / Field | Source File |

Include one row per write-back column. For any column that cannot be matched, mark binding as "UNKNOWN (requires UDF notebook inspection)".

STEP 6: PBIR limitation note
Confirm that "parameters": [] is present in the button's visual.json and note that this is a known PBIR serialization limitation (not a misconfiguration).
```



### 6 Practices to make UDF bindings Self-Documenting

The prompt above solves the immediate problem. The following six best practices eliminate it going forward. Apply them to every new Translytical report and any AI or human can reconstruct the full binding map from the TMDL files alone.

#### 1. Name your visuals after their UDF parameter

Set the visual **title** (the `visualContainerObjects.title` field in PBIR) to match the UDF parameter name exactly. PBIR serializes titles. An AI can read them directly.

| Instead of... | Use... |
|---|---|
| `slicer_Country` | `udf_countryName` |
| `Select Primary Driver` | `udf_primaryDriver` |
| `Justify Your Assumptions` | `udf_justification` |
| `Select Confidence Rating` | `udf_confidenceRating` |

A prompt like "find all visuals whose title starts with `udf_`" immediately maps parameters to visuals. No inference needed.

#### 2. Add a `displayFolder` to UDF-bound measures in the semantic model

Group all measures that feed UDF parameters under a dedicated folder in `KeyMeasures.tmdl`:

```
measure UPN = USERPRINCIPALNAME()
    displayFolder: "UDF Parameters"

measure 'Selected Country Key' = SELECTEDVALUE(DimCountry[CountryKey])
    displayFolder: "UDF Parameters"

measure 'Total Volume NY' = CALCULATE(SUM(FactSales[Volume]), Dates[Year] = 2026)
    displayFolder: "UDF Parameters"
```

Scanning for `displayFolder: "UDF Parameters"` retrieves all fx parameter candidates instantly.

#### 3. Add measure `description` annotations to document the UDF param name

TMDL supports `description` on measures. Use it to state the UDF parameter name explicitly:

```
measure UPN = USERPRINCIPALNAME()
    description: "UDF parameter: userUpn | the current user's identity"
    displayFolder: "UDF Parameters"

measure 'Selected Country Key' = SELECTEDVALUE(DimCountry[CountryKey])
    description: "UDF parameter: countryId | integer key of the selected country"
    displayFolder: "UDF Parameters"
```

Grep for `description: "UDF parameter:` and the full map is reconstructed.

#### 4. Create a single registry measure as a comment block

Add one documentation measure to `KeyMeasures`. This measure will never be used in visuals but will be fully readable by any AI or human from the TMDL file:

```
measure __UDF_Registry_ReviewNextSegment = """
// UDF: btn_ReviewNextSegment (SAVE / SUBMIT)
// Fabric item: navigationSection = '3a1da8dd68291a0a2879'
// Write-back table: BudgetConsolidationBuffer
//
// Parameter bindings:
// userUpn          → fx measure: [UPN]
// countryName      → slicer title: udf_countryName (DimCountry.CountryName)
// countryId        → fx measure: [Selected Country Key]
// baselineAmount   → fx measure: [Total Volume NY]
// inputPct         → slicer title: udf_inputPct (Parameter.Parameter)
// primaryDriver    → slicer title: udf_primaryDriver (Drivers.Drivers)
// confidenceRating → slicer title: udf_confidenceRating (Confidence Rating)
// justification    → slicer title: udf_justification (AssumptionNotes)
// riskAssessment   → slicer title: udf_riskAssessment (AssumptionNotes)
BLANK()"""
    description: "UDF parameter registry | do not use in visuals"
    displayFolder: "UDF Parameters/_Registry"
```

#### 5. Design the write-back table with self-documenting column names

Match write-back table column names to UDF parameter names exactly. If the UDF parameter is `inputPct`, the column is `InputPct`, not `SubmittedPct`. A direct 1:1 mapping that any AI resolves without inference.

#### 6. Keep button titles consistent and context-specific

When the same UDF button exists on multiple pages, vague titles like `btn_ReviewNextSegment` make them impossible to distinguish. Include the segment or context in the title:

• `btn_Save_Enterprise`  
• `btn_Save_MidMarket`  
• `btn_Save_SMB`

---

### How to verify in Power BI Desktop

Use this to confirm or reconfigure bindings after running the prompt above:

1. Open the report and navigate to the page that contains the action button
2. Select the button → Format pane → Action → Type = "Data Function"
3. Under "Data Function parameters", confirm each parameter matches the reconstructed table from the AI output
4. If the report has multiple UDF buttons (SAVE, SUBMIT, or per-segment variants), repeat for each one
5. Save the file. Bindings will again serialize as `"parameters": []` in the PBIR JSON. This is expected, not a bug.

> [!TIP]
> Run this verification after every UDF logic change. The bindings reset silently if you click the wrong button. Your registry measure is the source of truth.


### Conclusion

**PBIR does not persist UDF parameter bindings.** `"parameters": []` is always empty, by design.

**The binding map exists. It is just distributed.** Write-back table schema, page visuals, and TMDL measures give you everything you need.

**The reusable prompt does the work.** One AI session, two placeholders, six steps. Full binding documentation without opening Power BI Desktop.

**Six practices eliminate the problem going forward.** Visual titles, display folders, measure descriptions, a registry measure, consistent column names, and consistent button titles make every future report self-documenting.

**What's next:** How to automate UDF parameter validation as part of a PBIP CI pipeline, catching broken bindings before they reach production.



💬 Drop your thoughts in the LinkedIn post.  
✅ Scripts available in the GitHub repo.

### I'll be back! ⌛
