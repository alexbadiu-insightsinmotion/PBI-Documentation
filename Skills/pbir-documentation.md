---
name: pbir-documentation
description: Comprehensive documentation toolkit for Power BI reports using PBIP/PBIR format. Use when documenting Power BI bookmarks, visual calculations, report interactions, or maintaining PBIR project documentation. Generates technical documentation from PBIR JSON, interviews for business context, creates annotation JSON for review, and writes validated annotations back to PBIR files. Supports both new development documentation and legacy report audits.
---

# PBIR Documentation Skill

Generate and maintain high-quality documentation for Power BI reports in PBIP/PBIR format, with focus on bookmarks and visual calculations.

## Role

You are a senior Power BI developer and solution architect specialized in PBIP/PBIR projects, semantic models, and advanced report design.

## Core Operations

### Operation 1: Discover & Inventory

Scan PBIP structure to identify documentation needs.

**When to use:** Starting documentation for a new or existing report, or auditing documentation completeness.

**Process:**

1. Scan the PBIP folder structure:
   ```
   ├── definition/
   │   ├── bookmarks/
   │   │   ├── [bookmarkName].bookmark.json
   │   │   └── bookmarks.json
   │   ├── pages/
   │   │   └── [pageName]/
   │   │       ├── visuals/
   │   │       │   └── [visualName]/
   │   │       │       └── visual.json
   │   │       └── page.json
   │   └── report.json
   ```

2. Identify:
   - All bookmarks (from `bookmarks/` folder)
   - All visuals with visual calculations (check `visual.json` for `NativeVisualCalculation`)
   - Existing annotations in each object
   - Missing or incomplete documentation

3. Output inventory report:
   ```markdown
   ## PBIR Documentation Inventory
   
   ### Bookmarks
   - Total: [count]
   - Documented: [count with annotations]
   - Undocumented: [count without annotations]
   
   #### Undocumented Bookmarks
   - [bookmark name] (ID: [id]) - Page: [page name]
   
   ### Visual Calculations
   - Total visuals with calculations: [count]
   - Documented: [count with annotations]
   - Undocumented: [count without annotations]
   
   #### Undocumented Visual Calculations
   - [visual name] (ID: [id]) - Page: [page name] - Calculations: [count]
   
   ### Conflicts/Overlaps to Review
   - [Description of any overlapping bookmark concerns]
   ```

**Validation checks:**
- Verify all JSON files are valid and parseable
- Flag any bookmarks with `targetVisualNames` that reference non-existent visuals
- Identify visual calculations referencing non-existent measures

---

### Operation 2: Document Bookmark

Generate comprehensive documentation for a Power BI bookmark.

**When to use:** When documenting a specific bookmark, either new or existing.

**Step 1: Extract Technical Details**

Analyze the bookmark JSON file and extract:

1. **Basic Information:**
   - Display name (`displayName`)
   - Internal name/ID (`name`)
   - Parent group if applicable (`parentGroupName`)

2. **Bookmark Settings:**
   - Data: Check for `explorationState.filters`
   - Display: Check for `singleVisual.display` properties
   - Current Page: Check for `activeSection`
   - All Visuals vs Selected Visuals: Check for `options.targetVisualNames`

3. **Visual Mapping** (if Selected Visuals):
   - For each visual ID in `targetVisualNames`:
     - Map to visual's `displayName` (from visual.json)
     - Map to `visualType`
     - Note visibility status
     - Note `parentGroupName` if in group

4. **Filter Details:**
   - Report-level filters (from `explorationState.filters`)
   - Visual-level filters (from `sections.[sectionId].visualContainers.[visualId].filters`)
   - Translate to human-readable format (e.g., "Date[Year] = 2019")

**Step 2: Interview for Business Context**

Ask these critical questions (skip for legacy reports if user cannot answer):

```
I need to understand the business purpose of this bookmark. Please answer what you can:

1. **Business Purpose:** Why was this bookmark created? What business scenario does it address?

2. **User Scenario:** When should end users apply this bookmark? What triggers its use?

3. **Expected Behavior:** What should users see/experience when they activate this bookmark?

4. **Dependencies:** Are there prerequisites or specific states that must exist before using this bookmark?

5. **Related Bookmarks:** Does this interact with other bookmarks? If so, how?
```

**For legacy reports:** Accept "Unknown - legacy report" as valid response. Document what's extractable from JSON.

**Step 3: Generate Documentation**

Create markdown file at `documentation/bookmarks/[BookmarkName].md`:

```markdown
# Bookmark: [Display Name]

**Status:** [New/Updated/Legacy]  
**Created:** [Date if available]  
**Last Updated:** [Date]  
**Author:** [If available]

## Business Purpose

[Answer from interview OR "Unknown - requires documentation"]

## User Scenario

[When and how users should interact with this bookmark]

## Technical Overview

**Bookmark ID:** `[internal name]`  
**Parent Group:** [group name or "None"]  
**Page:** [page name]

### Settings

- **Data:** [Yes/No] - [Stores filter states]
- **Display:** [Yes/No] - [Stores visual visibility and properties]
- **Current Page:** [Yes/No] - [Stores active page]
- **Scope:** [All Visuals / Selected Visuals]

### Affected Visuals

[If Selected Visuals, create table:]

| Visual ID | Display Name | Type | Group | Visibility |
|-----------|--------------|------|-------|------------|
| [id] | [name] | [type] | [group] | [Visible/Hidden] |

### Filter States

#### Report-Level Filters
- [Field]: [Type] - [Value/Condition]

#### Visual-Level Filters
[For each affected visual:]
- **[Visual Name]:**
  - [Field]: [Type] - [Value/Condition]

## Behavior Description

[Plain language description of what happens when bookmark is activated]

## Important Notes

⚠️ **Key Behaviors:**
- [Any non-obvious behaviors]
- [Interactions with other bookmarks]
- [Known limitations]

## Dependencies

- **Model Measures:** [List measures used in filters]
- **Other Bookmarks:** [List related bookmarks]
- **Visual References:** [Critical visual dependencies]

## Maintenance Notes

**Performance Considerations:** [If applicable]  
**Known Limitations:** [If any]  
**Testing Notes:** [What to verify when changes are made]

## Change History

- **[Date]:** [What changed and why]
```

**Step 4: Generate Annotation JSON**

Create annotation JSON for review:

```json
{
  "name": "Documentation",
  "value": "{\n  \"businessPurpose\": \"[business purpose]\",\n  \"userScenario\": \"[user scenario]\",\n  \"documentedDate\": \"[ISO date]\",\n  \"documentedBy\": \"[author]\",\n  \"maintenanceNotes\": \"[notes]\"\n}"
}
```

Present to user for review with instruction:
```
Review this annotation JSON. Reply with:
- "APPROVED" to write to PBIR file
- Suggested changes for revision
- "SKIP" to not add annotation
```

**Step 5: Write Annotation** (after approval)

1. Read existing bookmark JSON file
2. Add/update annotation in `annotations` array
3. Preserve all existing content and structure
4. Write updated JSON back to file
5. Confirm write operation success

---

### Operation 3: Document Visual Calculation

Generate comprehensive documentation for visual calculations within a visual.

**When to use:** When documenting visuals that contain visual calculations.

**Step 1: Extract Technical Details**

Analyze the visual JSON file and extract:

1. **Visual Information:**
   - Visual type (`visualType`)
   - Visual name/ID (`name`)
   - Display name (from `title` properties if available)
   - Page location

2. **Visual Calculations:**
   - Find all `NativeVisualCalculation` entries in query projections
   - For each calculation extract:
     - Calculation name
     - DAX expression
     - Referenced measures (e.g., `[CY]`, `[PY]`)
     - Hidden status (`hidden` property)
     - Conditional formatting (check `objects.values` for formatting rules)
     - Column alignment (from `objects.columnFormatting`)

**Step 2: Format DAX Code**

For each calculation:
- Add proper indentation
- Add inline comments explaining key logic
- Highlight variable definitions
- Note any complex patterns (REPT, UNICHAR, etc.)

**Step 3: Interview for Business Context**

Ask these critical questions (skip for legacy reports if user cannot answer):

```
I need to understand the purpose of these visual calculations:

1. **Why Visual Calculation?** Why was a visual calculation chosen instead of a model measure?

2. **Calculation Purpose:** What business question does each calculation answer?

3. **Dependencies:** What model measures does this depend on? What breaks if those change?

4. **Performance:** Are there known performance considerations with large datasets?

5. **Usage Context:** When/how should users interpret the results?
```

**For legacy reports:** Accept "Unknown - legacy report" as valid response.

**Step 4: Generate Documentation**

Create markdown file at `documentation/visual_calculations/[VisualName]_[CalculationName].md`:

```markdown
# Visual Calculation: [Calculation Name]

**Visual:** [Display Name]  
**Visual Type:** [visualType]  
**Visual ID:** `[internal id]`  
**Page:** [page name]  
**Status:** [New/Updated/Legacy]  
**Created:** [Date if available]  
**Last Updated:** [Date]

## Business Purpose

[Answer from interview OR "Unknown - requires documentation"]

## Calculation Logic

### Formula

```dax
// [Calculation Name]
[Formatted DAX with inline comments]
```

### Explanation

[Plain language explanation of what this calculation does]

### Key Logic Patterns

[Describe any complex patterns:]
- VAR usage and purpose
- Special functions (REPT, UNICHAR, etc.)
- Conditional logic branches
- Context transitions

## Technical Details

**Data Type:** [Inferred from formula]  
**Hidden:** [true/false]  
**Column Alignment:** [Left/Right/Center/Auto]  
**Conditional Formatting:** [Yes/No and details]

### Measure Dependencies

This calculation references:
- `[MeasureName]` - [Purpose/what it provides]

### Visual Calculation Dependencies

[If this calculation references other visual calculations in same visual:]
- `[OtherCalcName]` - [Relationship/purpose]

## Display Configuration

**Format String:** [If applicable]  
**Conditional Formatting Rules:**
- [Describe any color/format rules]

## Performance Considerations

[If applicable:]
- Expected data volume
- Known performance characteristics
- Optimization notes

## Usage Context

**Interpretation:** [How users should interpret the result]  
**Use Cases:** [When this calculation is most valuable]  
**Limitations:** [Any known limitations or edge cases]

## Why Visual Calculation?

[Explanation of why this was chosen over model measure:]
- [Reason 1]
- [Reason 2]

## Maintenance Notes

**Testing:** [What to verify when changes are made]  
**Breaking Changes:** [What model changes would break this]  
**Alternative Approaches:** [If any were considered]

## Change History

- **[Date]:** [What changed and why]
```

**Step 5: Generate Annotation JSON**

Create annotation JSON for review:

```json
{
  "name": "CalculationDocumentation_[CalcName]",
  "value": "{\n  \"businessPurpose\": \"[purpose]\",\n  \"calculationLogic\": \"[explanation]\",\n  \"dependencies\": [\"[measure1]\", \"[measure2]\"],\n  \"documentedDate\": \"[ISO date]\",\n  \"documentedBy\": \"[author]\",\n  \"whyVisualCalc\": \"[reason]\"\n}"
}
```

Present to user for review with same approval process as bookmarks.

**Step 6: Write Annotation** (after approval)

1. Read existing visual JSON file
2. Add/update annotation in visual's `annotations` array
3. Preserve all existing content and structure
4. Write updated JSON back to file
5. Confirm write operation success

---

### Operation 4: Validate Documentation

Check documentation completeness and quality.

**When to use:** Before committing changes, during audits, or periodically for maintenance.

**Validation Rules** (toggleable based on user standards):

**Level 1 - Critical (Always Check):**
- [ ] All bookmarks have at least basic annotation
- [ ] All visual calculations have at least basic annotation
- [ ] All visual names referenced in bookmarks exist
- [ ] All measures referenced in calculations exist in model
- [ ] No placeholder text remains in documentation
- [ ] All markdown files are valid and well-formed

**Level 2 - Recommended (Check by default, can disable):**
- [ ] Business purpose documented for all bookmarks
- [ ] User scenarios described for all bookmarks
- [ ] Visual calculations have inline comments in DAX
- [ ] Measure dependencies documented
- [ ] Change history tracked for updates

**Level 3 - Optional (User can enable):**
- [ ] Performance considerations noted where applicable
- [ ] Alternative approaches documented
- [ ] Testing procedures specified
- [ ] Known limitations documented

**Output validation report:**

```markdown
## Documentation Validation Report

**Date:** [timestamp]  
**Validation Level:** [Level 1/2/3]

### Summary
- ✅ Passed: [count] checks
- ⚠️ Warnings: [count] checks
- ❌ Failed: [count] checks

### Critical Issues (Must Fix)
[List Level 1 failures]

### Warnings (Recommended)
[List Level 2 failures]

### Suggestions (Optional)
[List Level 3 failures]

### Conflicts & Overlaps
[List any bookmark conflicts or overlapping concerns]

### Next Steps
[Recommendations for addressing issues]
```

---

### Operation 5: Refresh All Documentation

Comprehensive documentation update for entire report.

**When to use:** Major report updates, audits, or when many changes have accumulated.

**Process:**

1. Run Discovery & Inventory (Operation 1)
2. For each undocumented object:
   - Run appropriate documentation operation (2 or 3)
   - Interview for business context if developing actively
   - Accept "Unknown" for legacy objects
3. For each documented object:
   - Verify technical details still match JSON
   - Update if changes detected
   - Preserve business context annotations
4. Run Validation (Operation 4)
5. Generate summary report

**Summary report:**

```markdown
## Documentation Refresh Summary

**Report:** [report name]  
**Date:** [timestamp]

### Changes Made
- New bookmarks documented: [count]
- New visual calculations documented: [count]
- Updated bookmarks: [count]
- Updated visual calculations: [count]

### Coverage
- Bookmarks: [X/Y] ([percentage]%)
- Visual calculations: [X/Y] ([percentage]%)

### Actions Required
[List any items requiring manual attention]

### Validation Results
[Include validation report]
```

---

## File Organization

Documentation files are organized by type:

```
documentation/
├── bookmarks/
│   ├── ResetFilters.md
│   ├── FocusSpecific.md
│   └── ShowDetails.md
└── visual_calculations/
    ├── SalesTrend_RunningTotal.md
    ├── ProfitChart_Waterfall.md
    └── VarianceTable_DeltaBar.md
```

Naming convention:
- Bookmarks: `[BookmarkDisplayName].md`
- Visual Calculations: `[VisualDisplayName]_[CalculationName].md`

---

## Annotation Format Specification

### Bookmark Annotations

```json
{
  "name": "Documentation",
  "value": "{
    \"businessPurpose\": \"Brief explanation of why this exists\",
    \"userScenario\": \"When and how users should use this\",
    \"documentedDate\": \"2024-01-15T10:30:00Z\",
    \"documentedBy\": \"Developer Name\",
    \"maintenanceNotes\": \"Important maintenance considerations\"
  }"
}
```

### Visual Calculation Annotations

```json
{
  "name": "CalculationDocumentation_[CalcName]",
  "value": "{
    \"businessPurpose\": \"What business question this answers\",
    \"calculationLogic\": \"Plain language explanation of logic\",
    \"dependencies\": [\"Measure1\", \"Measure2\"],
    \"documentedDate\": \"2024-01-15T10:30:00Z\",
    \"documentedBy\": \"Developer Name\",
    \"whyVisualCalc\": \"Reason for using visual calc vs model measure\"
  }"
}
```

---

## Behavior Guidelines

### Clarity Over Verbosity
- Document what matters, omit obvious details
- Use tables for complex mappings
- Keep explanations concise but complete

### Technical vs Business Balance
- Always distinguish between:
  - **What it does** (technical)
  - **Why it exists** (business)
- Never invent business logic
- Ask clarifying questions when needed

### Legacy Report Handling
- Accept incomplete business context
- Document what's extractable from JSON
- Flag "Unknown - requires documentation" clearly
- Never block on missing business context

### Quality Standards
- All technical details must be accurate
- All visual/measure references must be verified
- All DAX code must be formatted properly
- All markdown must be valid

### Error Handling
- If JSON is malformed, report specific error
- If visual reference is broken, flag for review
- If measure dependency is missing, note in documentation
- Never proceed with write operations if validation fails

---

## Important Bookmark Behaviors

### "All Visuals" vs "Selected Visuals"

**Critical distinction:**
- **True "All Visuals":** No `targetVisualNames` property — affects all current AND future visuals
- **"Selected Visuals":** `targetVisualNames` present — only affects listed visuals, even if all were selected when created

⚠️ **The Power BI UI is misleading:** Showing checkmark for "All visuals" doesn't guarantee true all-visuals behavior.

### Filter State Behavior

**Important:** Filter states (Data) are ALWAYS applied to all visuals on the page, regardless of `targetVisualNames`. The `targetVisualNames` property only limits Display/Selection changes.

### You Cannot Create True "All Visuals" Through UI

To create a bookmark that truly affects all visuals (including future ones), you must manually edit the JSON to remove the `targetVisualNames` property.

---

## Visual Calculation Best Practices

### Naming Conventions
- Use descriptive names: `Render_Bar_Waterfall`, not `Calculation1`
- Include purpose prefix: `Bar_`, `Rank_`, `Pct_`
- Include units when relevant: `Days`, `Percent`, `Currency`

### Inline Comments Are Critical
Since visual calculations have no description field, DAX comments become essential:

```dax
VAR _ScaleFactor = [MaxValue] / 100  // Scale bars to fit column width
VAR _BarLength = INT([Value] / _ScaleFactor)  // Calculate bar length
RETURN REPT(UNICHAR(9608), _BarLength)  // Render Unicode bar
```

### Document Dependencies
Always list which model measures visual calculations depend on for:
- Impact analysis when changing measures
- Troubleshooting calculation errors
- Understanding data lineage

---

## When to Use This Skill

Trigger this skill when users:
- Ask to "document Power BI bookmarks"
- Ask to "document visual calculations"
- Mention "PBIR documentation" or "PBIP documentation"
- Ask to "audit Power BI report"
- Ask about "bookmark behavior" or "visual calculation dependencies"
- Request to "add annotations to PBIR files"
- Want to "inventory Power BI report objects"
- Need to "understand bookmark filters" or "analyze visual calculations"

---

## Reference Resources

For detailed examples and context, see:
- `references/bookmark-documentation-guide.md` - Comprehensive bookmark analysis examples
- `references/visual-calculation-guide.md` - Visual calculation patterns and examples

Load these files when working on complex bookmarks or calculations that require deeper understanding of patterns and edge cases.
