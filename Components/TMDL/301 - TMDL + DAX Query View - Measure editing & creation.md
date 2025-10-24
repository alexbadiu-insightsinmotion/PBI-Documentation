

<img width="1950" height="1068" alt="Issue 301" src="https://github.com/user-attachments/assets/113c32f0-bce1-4f80-9140-134a6c555e0d" />


In our [previous article](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/TMDL/300%20-%20Foundation%20%26%20Setup%20-%20Introduction%20to%20TMDL.md), we explored how TMDL transforms Power BI from an isolated development experience into a professional, collaborative platform.

We saw how version control, code reviews, and reusable components become possible with TMDL's text-based format.

But TMDL isn't the only game-changer in modern Power BI development. Just before TMDL was launched, Microsoft introduced another powerful tool: **DAX Query View**.

This raises a practical question that many developers face:

- **How do these two features work together?**  
- **When should you use each one?**  
- **Are they competing tools, or complementary ones?**
<br>

The short answer: **they're complementary.** When used together, they create a development workflow that's greater than the sum of its parts.
<br>

Let's explore how.
<br>

### **A quick refresher** 
<br>

Before diving into how they work together, let's clarify what each tool does:

**TMDL View**  
Bulk editing and structural modification tool

- Script multiple objects at once
- Use find/replace and multi-cursor editing
- Access properties not available in the UI
- Create reusable templates

<br>

**DAX Query View**  
Testing and prototyping environment

- Write and test DAX without impacting your model without specific validation
- Validate calculations before adding them
- Simplifies debugging
- Create reusable query templates

<br>


Think of it this way: **TMDL View is for changing things. DAX Query View is for validating things.**
<br>

> [!TIP]  
> TMDL View became generally available (GA) in September 2025. It now appears by default in Power BI Desktop (no preview feature toggle needed).

<br>
<img width="829" height="443" alt="Pasted image 20251020222733" src="https://github.com/user-attachments/assets/e8c134bc-f87e-4c76-863d-a48a9eb7dd22" />




### **When to use what** 

The real power emerges when you combine both views. 
Here's a decision framework proposal:

| Task                   | Primary Tool   | Supporting Tool | Why                           |
| ---------------------- | -------------- | --------------- | ----------------------------- |
| Creating new measures  | DAX Query View | TMDL View       | Test first, format later      |
| Bulk property changes  | TMDL View      | DAX Query View  | Change many, validate all     |
| Testing calculations   | DAX Query View | -               | Sandbox environment           |
| Formatting measures    | TMDL View      | -               | Edit multiple formats at once |
| Refactoring model-wide | TMDL View      | DAX Query View  | Edit globally, verify locally |
| Prototyping logic      | DAX Query View | -               | Iterate quickly               |

<br>
Most tasks use both tools. Here's a pattern you could use:

1. **Prototype** in DAX Query View
2. **Test** with real data
3. **Add** to model (one click)
4. **Polish** properties in TMDL View
5. **Validate** back in DAX Query View
   
<br>

This pattern applies to nearly every task. Once you internalize it, you'll move between views naturally.

<br>

Don't worry about memorizing this table. After creating a few measures using both tools, the workflow becomes instinctive.

<br>

> [!IMPORTANT]  
> Most Power BI developers will use both tools multiple times in a single session. This isn't about choosing one over the other, it's about knowing which tool fits each step of your workflow.
<br>

<img width="500" height="400" alt="Pasted image 20251019144844" src="https://github.com/user-attachments/assets/ab7ec096-5d2a-491d-9e89-d1fe94ac1866" />



### **Core techniques you need to know** 

Before we build complete scenarios, let's focus on the essential techniques.

These are the building blocks. Every article in this series will use these skills.

#### **Technique 1: Drag-and-Drop code generation**

The easiest way to learn TMDL syntax: **let Power BI write it for you.**

**How it works:**

1. Open TMDL View
2. Select any object in the Data pane (measure, table, column)
3. Drag it onto the TMDL canvas
4. Power BI generates the complete TMDL code

![](https://learn.microsoft.com/en-us/power-bi/transform-model/media/desktop-tabular-model-definition-language-view/tmdl-view-02.png)

![](https://learn.microsoft.com/en-us/power-bi/transform-model/media/desktop-tabular-model-definition-language-view/tmdl-view-03.png)

For example, drag a measure called "Total Sales" and you'll see:

```tmdl
measure 'Total Sales' = SUM(Sales[Amount])
    formatString: "$"#,##0
    displayFolder: Core Metrics
    lineageTag: a7f8b234-5c21-4d89-b7e3-9d8f4a7b3e21
```

Every property is visible. No hidden metadata.

> [!TIP]  
> This is the secret to mastering this tool: **drag and drop** & **a bit of curiosity**. Want to know how a relationship looks in TMDL? Drag it in. Curious about table syntax? Drag it in. You do not need to memorize things.

---

#### **Technique 2: Multi-Cursor editing**

The secret to bulk operations: **edit multiple lines simultaneously.**

This single technique will probably save you hours.

**Key shortcuts:**

- `Ctrl + D` - Select next occurrence of current word
- `Ctrl + Shift + L` - Select ALL occurrences

<img width="540" height="1000" alt="Pasted image 20251020223733" src="https://github.com/user-attachments/assets/65feb3ce-5758-4cbf-8e30-90ee42181cc1" />

<br>
<br>

**Real scenario**: You have 10 measures. They all need the same display folder.

**With multi-cursor technique:**

1. Drag all 10 measures to TMDL View
2. Click on the first `displayFolder:` text
3. Press `Ctrl + Shift + L`
4. All 10 occurrences are now selected
5. Type the new folder name once
6. All 10 measures update simultaneously
7. Click Preview
8. Click Apply

**Time: less than 30 seconds.**

**Try it yourself:**

Open any report. Drag 3-4 measures to TMDL View. Find any property that appears multiple times. Use `Ctrl + Shift + L` to select all occurrences. Change one, watch them all change.

---
#### **Technique 3: Find and replace with Regex**

Not always needed, but useful to know we can go beyond basic find-replace. TMDL View supports regex patterns for complex replacements.

Press `Ctrl + F` to open the find-replace panel or press directly `Ctrl + H`.

<img width="440" height="120" alt="Pasted image 20251020224010" src="https://github.com/user-attachments/assets/0d166a5f-8562-4001-8100-762b481dcf76" />




**Common use cases:**

- Replace all format strings: `formatString: 0.00` → `formatString: #,0.00`
- Update column references: `Sales[Old Name]` → `Sales[New Name]`
- Change display folders in bulk
- Remove specific properties across all objects

I recommend starting with the basics. Regex expertise isn't required to create value. Once you understand the potential, regex will naturally become part of your workflow. 

**Example with Regex:**

##### 1. Adding Measure name prefixes based on type

**The Problem:** You want to add `KPI_` prefix to all measures that contain "Target" or "Actual" in their names for better organization.

**Before:**

TMDL

```tmdl
measure 'Sales Target' = 1000000
measure 'Sales Actual' = [Total Sales]
measure 'Profit Target' = 250000
measure 'Profit Actual' = [Total Profit]
measure 'Customer Count' = DISTINCTCOUNT(Customer[ID])
```

**Regex Find:**

regex

```regex
measure '(.*?)(Target|Actual)'
```

**Replace With:**

regex

```regex
measure 'KPI_$1$2'
```

<img width="1000" height="1000" alt="Pasted image 20251020224930" src="https://github.com/user-attachments/assets/ee0ef770-7300-4f5d-aa35-ef94ce55679f" />



**After:**

TMDL

```tmdl
measure 'KPI_Sales Target' = 1000000
measure 'KPI_Sales Actual' = [Total Sales]
measure 'KPI_Profit Target' = 250000
measure 'KPI_Profit Actual' = [Total Profit]
measure 'Customer Count' = DISTINCTCOUNT(Customer[ID])
```
<br>


<img width="500" height="120" alt="Pasted image 20251020225007" src="https://github.com/user-attachments/assets/d34e0ff2-d764-4678-a9c0-6779e9a239b6" />

<br>

<img width="500" height="200" alt="Pasted image 20251020225106" src="https://github.com/user-attachments/assets/647744b1-0e2e-4740-98d0-2b160311a2ef" />





##### 2. Standardizing Variable Naming Conventions

**The Problem:** Your team decided all DAX variables should start with underscore: `Result` → `_Result`, `Total` → `_Total`

**Before:**

TMDL

````tmdl

createOrReplace

	ref table _Measures
		measure 'Total Sales Demo' = 
			VAR GrossSales = SUM(Sales[Gross Amount])
			VAR Discounts = SUM(Sales[Discount Amount])
			VAR Result = GrossSales - Discounts
			RETURN Result
		

		measure 'Profit Margin Demo' = 
			VAR Revenue = [Total Sales]
			VAR Cost = [Total Cost]
			VAR Profit = Revenue - Cost
			VAR Result = DIVIDE(Profit, Revenue)
			RETURN Result
		
````

**Regex Find:**

regex

```regex
VAR ([A-Z][a-zA-Z]+) =
```

**Replace With:**

regex

```regex
VAR _$1 =
```

<img width="1045" height="400" alt="Pasted image 20251020225721" src="https://github.com/user-attachments/assets/46d63941-ac1b-41ff-9d68-b8f6d09bb5a0" />


<img width="250" height="320" alt="Pasted image 20251020225744" src="https://github.com/user-attachments/assets/d71809f9-6e4e-4f7c-9201-80af9a3085be" />




**Important:** Then do second pass to update variable references:

**Find:**

regex

```regex
RETURN ([A-Z][a-zA-Z]+)
```

**Replace:**

regex

```regex
RETURN _$1
```

**After:**

TMDL

```tmdl
measure 'Total Sales' = ```
    VAR _GrossSales = SUM(Sales[Gross Amount])
    VAR _Discounts = SUM(Sales[Discount Amount])
    VAR _Result = _GrossSales - _Discounts
    RETURN _Result
``` 

<img width="460" height="400" alt="Pasted image 20251020225856" src="https://github.com/user-attachments/assets/c80f2fa2-c490-46e7-a372-84b12d21f92e" />




---


##### 3. Adding standard comments to all measures

**The Problem:**
You want to add a validation comment template to all measures that don't have one.

**Before:**
```tmdl
createOrReplace

	ref table _Measures

		/// This measure is the sum of column Test Summarization OFF[Amount]
		measure 'Sum of Amount' =
				
				VAR _Result = SUM('Test Summarization OFF'[Amount])
				RETURN _Result
			formatString: 0.00
			displayFolder: 0 - Core
			lineageTag: ab14f4fe-2fd2-4d44-86bc-1deaa2daaef4

		/// This measure is the sum of column Sales[Net Price]
		measure 'Sum of Net Price' =
				
				VAR _Result = SUM('Sales'[Net Price])
				
				RETURN _Result
			formatString: 0.00
			displayFolder: 0 - Core
			lineageTag: aeba21f2-6895-4424-8735-0134a6e88997
```


**Regex Find:**
```regex
(measure '[^']+' =\s*\n)(\s+)(VAR)
```

**Replace With:**
```regex
$1$2// Validation: rule validated by ______ on __/__/____
$2$3
```

**After:**
```tmdl
createOrReplace

	ref table _Measures

		/// This measure is the sum of column Test Summarization OFF[Amount]
		measure 'Sum of Amount' =
				
				// Validation: rule validated by ______ on __/__/____
				VAR _Result = SUM('Test Summarization OFF'[Amount])
				RETURN _Result
			formatString: 0.00
			displayFolder: 0 - Core
			lineageTag: ab14f4fe-2fd2-4d44-86bc-1deaa2daaef4

		/// This measure is the sum of column Sales[Net Price]
		measure 'Sum of Net Price' =
				
				// Validation: rule validated by ______ on __/__/____
				VAR _Result = SUM('Sales'[Net Price])
				
				RETURN _Result
			formatString: 0.00
			displayFolder: 0 - Core
			lineageTag: aeba21f2-6895-4424-8735-0134a6e88997
```
<br>

<img width="1061" height="271" alt="Pasted image 20251020234336" src="https://github.com/user-attachments/assets/d6e53f76-707e-4405-9690-23552d0666cc" />

<br>
<br>

<img width="600" height="500" alt="Pasted image 20251020234552" src="https://github.com/user-attachments/assets/c7bcb7a2-e378-449f-8f72-5cb7a5cf2c5c" />

<br>


You might observe that some measures in TMDL have backticks. This is important.
<br>
<br>

<img width="800" height="900" alt="Pasted image 20251021110653" src="https://github.com/user-attachments/assets/330cac69-a254-4295-b915-635d75c8ad90" />




When Power BI adds **backticks** automatically, they're protecting your formatting. When writing TMDL manually, you typically don't need them unless you have specific formatting requirements.
<br>

> [!TIP]  
The automatic backtick system is designed to protect your code. You should trust it unless you have a specific, well-understood reason not to.

<br>


> [!TIP]  
> Start with exact text matching. Add regex patterns as you get comfortable. Most tasks don't need regex.

<br>


> [!WARNING]  
> Find-replace is powerful but it's also risky. Always **preview changes before applying**. We'll cover the preview feature next.

<br>
---

#### **Technique 4: Preview before applying**

TMDL View shows you exactly what will change before you commit.

This is a safety net.

<img width="2262" height="1350" alt="Pasted image 20251021111549" src="https://github.com/user-attachments/assets/4db883b6-573f-4988-80da-7f9ae341e1cb" />




**How it works:**

1. Write your TMDL script
2. Click "**Preview**" (don't click "Apply" yet)
3. **Review the diff view carefully**
4. Green = additions. Red = deletions. White = unchanged.
5. If it looks good, click "**Apply**"
6. If something looks wrong, press `Ctrl + Z` to undo


> [!TIP]  
> **Make preview a habit.** Even for simple changes. It takes 5 seconds and prevents mistakes that take 5 minutes to fix.

---

#### **Technique 5: Backup before bulk changes**

Before making bulk changes, create a safety net.

**Option 1: Duplicate the TMDL script page**

1. Duplicate the current page in TMDL View
2. Make your changes on the new page
3. If something breaks, revert to the original page


**Option 2: Use Git (better approach)**

1. Commit your current work
2. Create a new branch: `feature/update-format-strings`
3. Make your changes
4. Test thoroughly
5. Merge when confirmed

We'll explore Git workflows in other future articles.

> [!IMPORTANT]  
> Both TMDL View changes and DAX Query View changes are saved in PBIP. Use version control. It's not optional for professional development.

---
### **First Complete Example**

Let's put these techniques into practice. We'll create a dedicated measure table which is the foundation for organized model development.

**The Challenge:**

Every Power BI model needs a place for storing measures. Creating this manually takes multiple steps through the UI.

With TMDL, it takes less than 30 seconds.

**The Solution:**

```tmdl
createOrReplace
    
    /// This table contains all measures. Created for project organization.
    table _MeasuresAlex
        lineageTag: ac66bbdc-6c66-4a47-a67f-167fe255097a

        measure 0_KPI 
            displayFolder: KPIs
            lineageTag: 2f980b22-990d-4f7e-b024-e45b7d088301

        measure 0_Label
            displayFolder: Titles and Labels
            lineageTag: 2f980b22-990d-4f7e-b024-e45b7d088302

        partition _Measures = m
            mode: import
            source = ```
                    let  
                        _Measures = #table({},{})  
                    in  
                        _Measures
                    ```

        annotation PBI_ResultType = Table
```

<img width="200" height="120" alt="Pasted image 20251021112055" src="https://github.com/user-attachments/assets/d5516c3b-cf95-4e36-b76b-ab711980cbea" />



**How to Use It:**

1. Copy the code above
2. Go to TMDL View in your report
3. Paste the code
4. Click "Preview" to see what will be created
5. Click "Apply"
6. Refresh your model 

**Done**. You now have a measure table with display folders pre-configured.

This TMDL script created:

- An empty table named `_MeasuresAlex`
- Two placeholder measures with organized folders
- All the metadata Power BI needs

The table uses an empty M query: `#table({},{})`. This creates a table with no columns and no rows. Just what we need for storing measures.

> [!TIP]  
> **This is TMDL's real value: reusability.**
> 
> Save this script. Use it in every new project. Customize the display folders for your organization. Share it with your team.
> 
> What took 15 clicks through the UI is now a 10-second copy paste operation.

**Make your own:**

After using this template a few times, customize it:

- Add your standard folders (KPIs, Core Metrics, Time Intelligence)
- Include common placeholder measures
- Add annotations with your team's standards
- Update the description to match your conventions

Then save your customized version as a text inside your team's repo. You now have an accelerator template for every future project.

---

Now that you have a measure table, **let's add measures**. We can use two approaches.

#### **Approach 1: DAX Query View (recommended for new logic)**

Best for: Measures with logic you want to test first.

**Steps:**

1. Open DAX Query View
2. Write your measure with a test:

```dax
DEFINE
    MEASURE '_Measures'[Total Sales] = SUM(Sales[Amount])

EVALUATE
{ [Total Sales] }
```

3. Click "Run" to see the result
4. If the number looks correct, click "Add new measure" or "Overwrite measure"
5. Done


<img width="540" height="300" alt="Pasted image 20251021113747" src="https://github.com/user-attachments/assets/be85fbf5-d4cf-40d5-ad64-1f1df53b0b68" />


The measure is now in your model. No copying. No pasting. No typos.

---
#### **Approach 2: TMDL View (recommended for similar measures)**

Best for: Creating multiple variations of existing measures.

**Steps:**

1. Select 1-2 existing measures (hold Ctrl)
2. Drag them to TMDL View
3. You now see their complete TMDL code
4. Copy, Paste and modify the structure
5. Change names and formulas
6. Remove the lineageTag (it will be created automatically)
7. Click "Apply"

Multiple measures created in one action.

<img width="600" height="440" alt="Pasted image 20251021114450" src="https://github.com/user-attachments/assets/ebc5481d-24f2-4a97-b2f1-78986ec93b2b" />



**Which approach should you use?**

|Situation|Use This|
|---|---|
|New, untested logic|DAX Query View|
|Complex formulas|DAX Query View|
|Copying existing patterns|TMDL View|
|Simple SUM/COUNT measures|Either (your preference)|
|Creating 5+ similar measures|TMDL View|

Most developers use both approaches in the same session. It's not an either/or decision. Use the right tool for each specific task.

> [!TIP]  
> In the next article, we'll dive deep into the complete measure development workflow. You'll see how to prototype complex calculations, add them to your model, then polish their properties. For now, just know that both approaches work.

---
### Practical tips

As you start using these tools daily, here are patterns that make you faster. Let's recap:

**Tip 1: Use both TMDL View and DAX Query View** 

Switch between views using the tabs. Force yourself to do more and more actions using code instead of using UI (even though it takes a bit more time in the beginning)


**Tip 2: Save & rename your DAX queries & TMDL scripts**

Each query tab persists. Use them as:

- Test cases
- Documentation
- Quick validation scripts


**Tip 3: Learn the keyboard shortcuts**

These save massive time:

- `Ctrl + Shift + E` in DAX Query View = Run query
- `Ctrl + D` = Select next occurrence
- `Ctrl + F` = Find/replace
- `Ctrl + Shift + L` = Select all occurrences 
- `Ctrl + Z` = Undo in TMDL View

**Tip 4: Start small**

Don't try to script your entire model immediately. Start with:

- One measure table (we did this today)
- A few measures to practice multi-cursor editing
- One simple find-replace operation

Build confidence. Add complexity gradually.

> [!TIP]  
> **The workflow feels natural after 2-3 practice sessions.** Don't overthink it. Just start using the tools. Muscle memory develops quickly.

---
### **Conclusion** 

You now understand the foundational workflow:

**TMDL View** for structural changes and bulk operations  
**DAX Query View** for testing and validation  
**Both together** for professional development

The five techniques shown today are essential:

1. Drag-and-drop code generation
2. Multi-cursor editing
3. Find-and-replace
4. Preview before applying
5. Backup before bulk changes

These techniques appear in every article that will follow. Everything else builds on this foundation.

**What's next:**

In the next articles, we'll explore other tips related to the development lifecycle. But until then...

**Call to action: Start practicing today**

Open a test/dummy report. Create the measure table using the TMDL script from this article. Add 2-3 measures using both approaches. Try the multi-cursor technique.

Get comfortable moving between views. 

---

💬 **Let's discuss:**  
Drop your thoughts in the LinkedIn post discussion. What bulk operations would save you the most time? Let's learn from each other.

✅ All the TMDL scripts showcased in the series are shared and available in the GitHub Repo

<br>

### **I'll be back!⌛** 
