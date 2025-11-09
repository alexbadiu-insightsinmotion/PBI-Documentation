
<img width="1950" height="1068" alt="Issue #302" src="https://github.com/user-attachments/assets/c9804b65-6c40-477f-b9f8-e010ed0c2d4a" />


In the [previous article](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/TMDL/301%20-%20TMDL%20%2B%20DAX%20Query%20View%20-%20Measure%20editing%20%26%20creation.md), we explored how TMDL and DAX Query View work together. We learned the core techniques: drag-and-drop code generation, multi-cursor editing, and the basic workflow pattern. <br> 

Now let's put those techniques into action. 
<br> 

This blog post focuses on the most common task in Power BI development: **creating measures**. Not just writing DAX formulas, but the complete workflow, from initial idea to production tested & validated measures.

**The purpose of this article is to present a repeatable process for measure development that's faster, safer, and more professional than clicking through the UI.**

- How to prototype complex calculations safely
- When to use each tool in the development cycle
- How to create reusable measure templates
- Best practices that prevent common mistakes

Let's dive in.
<br> 

### Today's challenge
<br> 

Before TMDL and DAX Query View, "traditional" measure development looked like this:
<br> 

1. Create new measure through UI dialog
2. Write DAX directly in the formula bar
3. Click OK and wait couple of seconds
4. Add measure to a visual
5. Wait for it to calculate
6. Realize there's an error
7. Edit the measure again
8. Repeat until it works

<br> 

And hopefully you remember to:
1. Format the measure properly
2. Remember to add a description
3. Add the measure in the right folder/table
4. Remember to use clear and user-friendly naming
5. Delete the previous version if you added in comments // 
<br>

This workflow has real problems.

**Problem 1: Every test affects your model**

You're saving changes with each attempt. And if you are working in a shared semantic model? Others see your broken or work-in-progress measures. They might even use them in reports.

**Problem 2: Debugging is painful**

You can't see intermediate values easily. You can't test parts of the logic independently. Without external tools you're guessing what's wrong. 

What if you are building complex formulas with multiple VARs leveraging virtual tables? Good luck figuring out the issue.

**Problem 3: No experimentation space**

Want to try two different approaches and use the simplest and optimized solution? You have to:

- Create both measures in the model
- Test them both
- Delete the one that doesn't work or is less optimized (and hope you deleted the right one)

<br> 

>[!Warning]
>Without room for experimentation, **most report developers settle for the first version of the "code that works"** instead of optimizing for readability, performance, and simplicity.

<br> 

**Problem 4: Formatting is an afterthought**

Once the formula works, you still need to:

- Set the format string (open dialog)
- Set the display folder (open dialog)
- Add a description (open dialog)
- Add any annotations (open dialog)

Each requires additional clicks. Most developers skip this step and **Documentation suffers**.
<br> 
<br>

> [!WARNING]  
> This traditional workflow leads naturally to model bloat. Developers create test measures like "Sales Test 2", "Sales Final", "Sales ACTUAL Final". **Then forget to delete them**. The model accumulates unused calculations that can create ambiguity and lead to wrong measure use.


<br> 

**Example**: A developer wants to create a more complex cumulative YTD comparison measure.

Traditional approach: 30 minutes (just a gut estimation - including all the trial and error, fixing errors, and formatting).

Modern approach with a better organization and some useful scripts for DAX Query View + TMDL View can reduce the workflow to less than 10 minutes.

**That's 3x faster.** Scale that to 50 measures, and you've saved 2 days of development time. 

**So yes, there's a better way !**
<br> 
<br> 

---
### **The Modern Workflow** 

With DAX Query View and TMDL View, measure development becomes more professional.

Here's the proposed pattern also discussed in the previous [blog article](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/TMDL/301%20-%20TMDL%20%2B%20DAX%20Query%20View%20-%20Measure%20editing%20%26%20creation.md):
<br> 
<br>

**Phase 1: Prototype in DAX Query View**
<br> 

Write and test your DAX without affecting the model. See results immediately. Try different approaches safely. Build complex logic incrementally.

**Phase 2: Validate with real data**
<br> 

Test the measure with actual filters and contexts. Verify it behaves correctly across different dimensions. Check edge cases.

**Phase 3: Add to model**
<br> 

Once the logic works, add the measure with one click. No copying. No pasting. No typos.

**Phase 4: Polish with TMDL View**
<br> 

Set display folders, format strings, and descriptions for multiple measures at once. No clicking through dialogs. Just one standardization logic applied to all measures.

**Phase 5: Final Validation**
<br> 

Return to DAX Query View to verify everything works as expected in the actual model.



<img width="1200" height="1063" alt="image" src="https://github.com/user-attachments/assets/5ac51036-8b1c-41ac-bceb-0e964863e97a" />



This workflow separates tasks in different phases:
<br> 

- **Logic development** happens in DAX Query View
- **Metadata management** happens in TMDL View
- **Validation** happens in both

<br> 

**The gains are the following:**
<br> 

**1. Faster iteration**  
Test immediately and without saving. Try many different variations in the time it used to take to test one.
<br> 

**2. Cleaner models**  
No test measures cluttering your model. No "Sales Test 3 FINAL v2". Everything added is tested and validated by the developer.
<br> 

**3. Better documentation**  
Bulk metadata updates are fast. You can do them without losing time. Models stay documented.
<br> 

**4. Lower risk**  
The measures change when you explicitly add them. 
<br> 

**5. Easier collaboration**  
Team members never see broken test measures. They only see finished, tested, documented measures. And if they have an inquiry? You can break down the logic and show the correctness of your intermediary steps using Dax Query View.
<br> 

> [!TIP]  
> The pattern scales to any complexity level.

<br> 


---

### **Phase 1 - Prototyping in DAX Query View**
<br> 

Let's walk through a real example. We'll create a sales measure that calculates revenue correctly.

#### **1. Open DAX Query View and start simple**
<br> 

Click the "DAX Query View" button in Power BI Desktop. You'll see a blank code editor.

Don't try to write perfect code immediately. Start with the simplest version:

```dax
DEFINE
    MEASURE '_Measures'[Sales Test] = SUM(Sales[Amount])

EVALUATE
{ [Sales Test] }
```

You can also start from an existing simple measure (Define and Evaluate)

<img width="565" height="420" alt="Pasted image 20251106101303" src="https://github.com/user-attachments/assets/e3c3d709-bfbf-4c9e-bb8e-3878052e3592" />
<br> 

 
 and simply change the name
 <br>
 
<img width="472" height="400" alt="Pasted image 20251106101649" src="https://github.com/user-attachments/assets/6182a21e-1b25-4e51-b49b-e8171729a515" />


<br>
<br>


>[!NOTE] 
>In DAX Query View, all queries return tables. To display a scalar value such as a measure, you need to wrap it in a table expression, either by using **`SUMMARIZECOLUMNS`** (or **`ROW`**) to create a table with a column name, or by enclosing the measure in curly brackets `{[MeasureName]}`

<br> 


Click "Run" or `CTRL + SHIFT + E`. You see the result immediately.

Does the number look reasonable? If yes, continue. If no, check your column reference.
<br> 

> [!TIP]  
> Always start with the simplest version. Get something running. Then make it more complex. This incremental approach catches errors early when they're easy to fix.

<br> 


#### **2. Add complexity incrementally**
<br> 

Now make the calculation more realistic. Maybe you need quantity times net price:
<br> 

```dax
DEFINE
    MEASURE '_Measures'[Sales Test] = 
        SUMX(
            Sales,
            Sales[Quantity] * Sales[Net Price]
        )

EVALUATE
{ [Sales Test] }
```

Run it again. Check the result. Does it differ from the simple SUM? It should as you are multiplying Quantity * Net Price.

<img width="400" height="400" alt="Pasted image 20251106103405" src="https://github.com/user-attachments/assets/d2bc1b7b-bd9e-4abb-8819-87ee9b2ad242" />
<br> 


What if the result looks way off compared to what you expect? Here's how to debug:
<br> 

Add intermediate checks:

```dax
DEFINE
    MEASURE '_Measures'[Sales Test] = 
        SUMX(
            Sales,
            Sales[Quantity] * Sales[Net Price]
        )

EVALUATE
{
    ("Total Sales", [Sales Test]),
    ("Row Count", COUNTROWS(Sales)),
    ("Avg Quantity", AVERAGE(Sales[Quantity])),
    ("Avg Net Price", AVERAGE(Sales[Net Price]))
}
```

<img width="400" height="580" alt="Pasted image 20251106103633" src="https://github.com/user-attachments/assets/e8a77e27-3f6d-4fa7-a6a1-f316ddad52b5" />


Now you can see if the issue is:
<br> 

- Missing rows (row count is wrong)
- Incorrect quantities (average doesn't make sense)
- Incorrect prices (average doesn't make sense)

This is impossible with traditional measure development. You'd have to create 4 separate measures in your model just to debug one measure.
<br> 

#### **3. Test different contexts**
<br> 

Don't just check the total. Test how the measure behaves with filters:

```dax
DEFINE
    MEASURE '_Measures'[Sales Test] = 
        SUMX(
            Sales,
            Sales[Quantity] * Sales[Net Price]
        )

EVALUATE
SUMMARIZECOLUMNS(
    Product[Category],
    "Total Sales", [Sales Test]
)
ORDER BY [Total Sales] DESC
```

<img width="400" height="600" alt="Pasted image 20251106103751" src="https://github.com/user-attachments/assets/04f94717-0e0e-4325-a131-85655b7c4055" />
<br> 


Does each category look reasonable? Are there any unexpected zeros? Any suspiciously high values?
<br> 

**This is your quality check. Catch errors before the measure goes into the model.**
<br> 

**Real example**: A developer created a sales measure. Tested the total and looked fine. Added the measure to  the model and used in reports.

Two weeks later, someone filtered by a specific product. The measure showed zero. So it raised a ticket saying there is a bug in the measure logic.

If they had tested with filters (like we just did), they would have caught it in 2 minutes.

And if they had documented the measure's intended purpose and use cases, someone else might not have tried forcing it into an unsupported scenario. You don't just avoid confusion, you build trust.
<br> 

#### **4: Build complex logic step by step**
<br> 

For complex calculations, use multiple measures to see each piece:

```dax
DEFINE
    MEASURE '_Measures'[Gross Sales] = 
        SUMX(Sales, Sales[Quantity] * Sales[Net Price])
    
    MEASURE '_Measures'[Discounts] = 
        SUMX(Sales, Sales[Quantity] * 0.15)
    
    MEASURE '_Measures'[Returns] =
        CALCULATE(
            SUMX(Sales, Sales[Quantity] * Sales[Net Price]),
            'Date'[Year] = 2020
        )
    
    MEASURE '_Measures'[Net Sales] = 
        [Gross Sales] - [Discounts] - [Returns]

EVALUATE
{
    ("Gross Sales", [Net Sales]),
    ("Discounts", [Discounts]),
    ("Returns", [Returns]),
    ("Net Sales", [Net Sales])
}
```

<br> 
Each piece of the logic is visible. You can verify every step. Build confidence that the final calculation is correct.
<br> 

>[!NOTE]
>If you have an error in your code, DAX Query View will let you know
> <img width="1396" height="923" alt="Pasted image 20251106104646" src="https://github.com/user-attachments/assets/a94c9851-7fbc-4fbb-b70c-0638c8d3c2bf" />

<br>
<br>


>[!NOTE]
>You can use multiple evaluate statements in one screen

<br>

<img width="520" height="800" alt="Pasted image 20251106104839" src="https://github.com/user-attachments/assets/81f800dc-6c6d-46df-aa95-9901d8f839b2" />


**Why this matters:**

Traditional development: Write the entire formula at once. Hope it works. Debug is nearly impossible if it doesn't.

**DAX Query View:** Build incrementally. Test each component. Combine with confidence. It offers a fluid, professional experience to develop DAX logic directly within Power BI, and serves as an excellent tool for debugging and validation.

<br> 

> [!TIP]  
> **Save your test queries.** They become documentation showing how you validated the measure. Six months later when someone asks "how do you know this measure is correct?", you can show them the query you used to test it.

#### **5: Add to Model**

Once you're satisfied with the logic, add the measure:

1. Select the measure definition you want
2. Click **Add new measure** to add measures one-by-one, or **Update model with changes** to create measures in bulk.
3. Done

<img width="600" height="500" alt="Pasted image 20251106105926" src="https://github.com/user-attachments/assets/2c802ffb-0045-4457-81d3-be3ce5ae48b9" />
<br> 


The measure(s) appears in your model. The formula is exactly what you tested. No transcription errors.

Be aware that after creating a measure in the model, you can’t undo this action to modify it later.

<img width="300" height="150" alt="Pasted image 20251106110202" src="https://github.com/user-attachments/assets/8ce4d9ac-cb06-4be4-977f-5599a6b05e14" />
<br> 


<br> 
<br> 

> [!IMPORTANT]  
> When you add a measure from DAX Query View, it adds ONLY the measure definition. It doesn't include the **formatString**, **displayFolder**, or **description**. **That's intentional**. We'll add those properties next using TMDL View, which is much faster for bulk metadata.

---

### **Phase 2 - Polishing with TMDL View** 
<br> 

We've added several measures to the semantic model. They work correctly. They've been tested and validated.
<br> 

But they're not polished:
<br> 

- No format strings (showing raw numbers)
- No display folders (all in root of table)
- No descriptions (no documentation)

<br> 

Here TMDL View is helpful.
<br> 

#### **Step 1: Script new measures**
<br> 

1. In the Data pane, select all measures you just added (hold Ctrl)
2. Drag them to TMDL View
3. Power BI generates the complete TMDL code

You now see every property for every measure, in one place and ready to edit.

#### **Step 2: Add format strings in bulk**
<br> 

Use [multi-cursor editing](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/TMDL/301%20-%20TMDL%20%2B%20DAX%20Query%20View%20-%20Measure%20editing%20%26%20creation.md):
<br> 

1. Click on the first `lineageTag` line
2. Press `Ctrl + Shift + L` to select all lineageTag lines
3. Press `Enter` to create new line above
4. Type: `formatString:"$#,##0"
5. Preview & Apply

All measures get formatted simultaneously.
<br> 

<img width="800" height="670" alt="Pasted image 20251106111056" src="https://github.com/user-attachments/assets/275f6bd9-4446-404e-b771-f515886f5d03" />
<br> 


What would take 2 minutes per measure (open dialog, set format, close dialog) now takes 20 seconds for all measures.
<br> 

#### **Step 3: Set display folders**
<br> 

Same technique. Same keyboard shortcuts:
<br> 

1. Position cursor after formatString lines
2. Press `Enter`, type: `displayFolder: Sales Metrics`
<br> 

<img width="1010" height="471" alt="Pasted image 20251106111623" src="https://github.com/user-attachments/assets/0bf8d204-9321-48b6-b3bf-19c4ab773e06" />
<br> 


All measures organized into one folder.

Want different folders for different measures? Use `Ctrl + D` to select individually and type different folder names.
<br> 

#### **Step 4: Add descriptions**
<br> 

For descriptions, add comment lines above each measure:
<br> 

```tmdl
/// Calculates total sales revenue by multiplying quantity by net price
measure 'Total Sales' = ...

/// Shows sales amount from previous year for comparison
measure 'Sales LY' = ...
```

The `///` comment becomes the measure description automatically.
<br> 

> [!TIP]  
> **Good descriptions include:**
> 
> - What the measure calculates
> - Key business logic
> - When to use it vs similar measures
> - Owner or last updated by
> 
> Example: `/// Calculates net sales (gross - discounts - returns). Use for revenue reporting. Updated by A.Groemling 10/2024`

<br> 


#### **Step 5: Preview and Apply**
<br> 

Click "Preview" to see what will change. Review carefully:
<br> 

- Green = additions
- Red = deletions
- White = unchanged

<br> 

If it looks good, click "Apply" and add all measure updates simultaneously.
<br> 

**The Result:**
<br> 

What used to require clicking through dialogs for each measure now takes 60 seconds total.
<br> 

- Format strings: ✓
- Display folders: ✓
- Descriptions: ✓

<br> 
<br> 

> [!TIP]  
> **This is why the workflow matters.**
> 
> When metadata updates are this fast, you actually do them. When it requires clicking through 20 dialogs, you skip it.
> 
> TMDL View makes proper documentation much more frictionless.
<br> 
---

### **Phase 3: Creating reusable templates** 
<br> 

After creating a few measures, you'll notice patterns. Same structure. Similar formulas. Different values.
<br> 

Turn these patterns into templates.
<br> 

#### **Example: standard Sales measure template**


```tmdl
createOrReplace

    ref table _Measures

        /// [DESCRIPTION: What this measure calculates and when to use it]
        /// Owner: [YOUR NAME] | Created: [DATE]
        measure '[MEASURE NAME]' = ```
            // [BUSINESS LOGIC COMMENT]
            VAR _Calculation = 
                SUMX(
                    Sales,
                    Sales[Quantity] * Sales[[COLUMN NAME]]
                )
            
            // Final result
            VAR _Result = _Calculation
            
            RETURN
                _Result
            
            // Validation: tested by [NAME] on [DATE]
            // Test cases: [LINK TO DAX QUERY VIEW TEST]
            ```
            formatString: "$"#,##0.00
            displayFolder: [FOLDER NAME]

```

#### **How to Use Templates**
<br> 

1. Copy the template
2. Paste into TMDL View
3. Replace all placeholders:
    - `[DESCRIPTION]` → actual description
    - `[YOUR NAME]` → your name
    - `[DATE]` → today's date
    - `[MEASURE NAME]` → measure name
    - `[COLUMN NAME]` → the column to use
    - `[FOLDER NAME]` → display folder
4. Click Preview & after Apply

One new production-ready measure created in 30 seconds.
<br> 

> [!TIP]  
> **Don't worry about lineageTags.** If you delete the lineageTag line, Power BI generates a new GUID automatically when you apply. Only include lineageTags in templates if you're copying from existing measures.
<br>


> [!TIP]  
> If you want to [remove all *lineageTag* lines](https://www.datazoe.blog/post/dax-date-table-in-tmdl), the following regular expression lineageTag: [0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12} can be used with *Find and Replace*.
<br> 
<br> 
<br>

>[!TIP]  
**DAX User-Defined Functions (UDFs) make templates even more powerful.** With the newly introduced DAX UDF feature, you can encapsulate common calculation patterns with parameters already integrated into the function. This means once you define a UDF, you can reuse it across multiple measures without any code adjustments! You will just need to call the function with your specific parameters. This provides a significant boost to template efficiency, as complex logic lives in one place and updates automatically propagate to all measures using that UDF.
<br> 

#### **Creating templates from existing measures**
<br> 

Don't write templates from scratch. Create them from measures that work:
<br> 

1. Build a measure you're proud of (good formula, well documented)
2. Drag it to TMDL View
3. Replace specific values with placeholders in `[BRACKETS]`
4. Save as a text file: `Sales_Measure_Template.tmdl`

<br> 

#### **Building your template library**
<br> 

Start collecting templates for common patterns <br>
Store them organized <br>
Share this folder with your team via SharePoint or Git. Everyone uses the same templates. Consistency across all projects.
<br> 
<br> 


> [!TIP]  
> **Good templates include:**
> 
> - Clear `[DESCRIPTION]`
> - Comments explaining the logic
> - Validation placeholders for sign-off
> - Standard formatting conventions
> - Usage instructions at the top
> - Examples of clear use cases where they can be used

<br>  

Over time, you build faster. Quality stays high. Documentation stays consistent.
<br> 

---
### Phase 4: Best Practices
<br> 


✓**Practice 1**: Always prototype complex logic <br>
✓**Practice 2:** Test in multiple contexts (read this Documentation article I wrote [DAX Query View and Automated Testing](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/06%20-%20Automated%20Testing%20in%20Power%20BI.md) ) <br>
✓**Practice 3:** Use version control <br> 

> [!IMPORTANT]  
> Version control isn't optional for Power BI professional development.
 

✓**Practice 4:** Document as you go <br>
✓**Practice 5:** Keep test queries <br>
✓**Practice 6:** Build your template library gradually <br>
✓**Practice 7:** Establish team conventions for templates <br>
✓**Practice 8:** Define naming conventions <br>
✓**Practice 9:** Define documentation standards <br>

<br>

> [!WARNING]  
> **Don't skip the validation step.**
> 
> Just because DAX Query View showed correct results doesn't mean the measure works perfectly in all contexts. Always verify in the actual model with real visuals.

---
### **Conclusion** 
<br> 

You now have a complete, professional workflow for measure development:
<br> 

**Prototype** → **Test** → **Add** → **Polish** → **Validate**
<br> 

This workflow is:
<br> 

- **Faster** than traditional development
- **Safer** because you test before committing
- **More maintainable** because documentation is built-in
- **Scalable** through templates and reusable patterns

<br> 

The techniques you learned today prepare you perfectly for that next level.
<br> 

---

💬 **Let's discuss:**  
What measure took you the longest to build the old way? How much time could this workflow save you? Share your thoughts and experience.
