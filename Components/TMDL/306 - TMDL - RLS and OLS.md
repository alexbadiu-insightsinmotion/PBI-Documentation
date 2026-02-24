

<img width="1950" height="1068" alt="Issue 306" src="https://github.com/user-attachments/assets/9f913d98-b126-442b-94d5-8a984e88bc4d" />



# The Power BI feature that was never accessible (until now)

_How TMDL unlocked column-level security that was impossible in Power BI Desktop_
<br>




**Here's something many Power BI developers don't know:** Until recently, you literally couldn't **securely hide** individual columns from specific users in Power BI Desktop. No button. No checkbox. No way.

Sure, you can "hide" columns in Power BI Desktop. But that's just visual hiding, **everyone can still see them**. Right-click, unhide. Or just reference them in a measure. The data is completely accessible.

Want to show managers their team's performance but **truly lock down** salary data column so they can't access it at all? **Impossible in the UI.**

The only option was using external tools like Tabular Editor, an incredibly powerful professional tool.

TMDL just changed everything.
<br>
<br>


## What you couldn't do before

Let's say you have an employee table with **performance ratings** **AND** **compensation data**. You need:

- **Managers** → See their team's performance, but **NOT salaries**
- **HR Managers** → See their team's performance **AND salaries**
- **HR Admins** → See everything, everyone

  

In Power BI Desktop's UI, you can set up Row-Level Security (RLS) to filter which employees someone sees. But **securely** hiding specific columns? **That feature literally doesn't exist in the interface.**
<br>
<br>



### Why "Hide Column" isn't security

Yes, Power BI Desktop has a "Hide" button for columns. But here's the problem:

- **Anyone can unhide it:** Right-click → Show hidden fields
- **Measures can still reference it:** `Total Salary = SUM(Employees[Salary])` works fine, even if Salary is "hidden"
- **Data is fully accessible:** The column data lives in the model, available to anyone who can query it


**What you need is Object-Level Security (OLS):** The column doesn't just disappear from view, it's **completely inaccessible**. Measures that reference it return errors. DAX queries can't touch it. The data is truly locked down.

Because OLS wasn't accessible in Power BI Desktop, some companies ended up building **three separate .pbix files** with **three separate semantic models**, one for each role. Same visuals, same calculations, but triple the maintenance and triple the compute costs.
<br>
<br>


## The professional path

Advanced developers have long used **Object-Level Security (OLS)** through Tabular Editor

But Tabular Editor is a **professional developer tool**. It requires:

1. Downloading and installing an external application 
2. Potentially pay a license - Tabular 3 (you can also use the free edition Tabular Editor 2)
3. Navigating a different interface designed for advanced scenarios
4. Configuring security in one tool with impact on another

**The accessibility gap:** Once you configure OLS in Tabular Editor and save your .pbix file, there's **limited visibility of column-level security in Power BI Desktop**. While roles appear in the Manage Roles dialog, you can't easily see which specific columns are secured without reopening Tabular Editor.

Team members who don't use Tabular Editor have no clear way to audit which columns are protected by OLS.
<br>
<br>

### The business cost of inaccessibility

Because OLS wasn't directly accessible in Power BI Desktop, **many organizations simply never used it**.

Instead, they built what made sense with the tools they knew:

- **Three separate datasets:** One for Managers (without salary columns), one for HR (with salary), one for Executives (full access)
- **Three separate reports:** Same visuals, same logic, different data sources
- **Triple the maintenance:** Every change to business logic gets implemented three times
- **Triple the compute cost:** Three semantic models refreshing instead of one
- **Triple the storage:** Same data loaded three times in different workspaces

**Inevitably, 1 of the reports will be out-of-sync with the others, and people will be using different data/calculations so results are unlikely to be the same**

Why three datasets instead of one with RLS? Because when sensitive columns like salary exist in the model, **everyone with access can see them**, even if hidden. A common solution to prevent access was to create separate datasets with those columns physically removed.

The irony? The capability to avoid all this existed the whole time in Tabular Editor. But because it required specialized knowledge that many Power BI developers didn't have, organizations chose the simpler (but far more expensive) path.

**OLS was powerful, it just wasn't accessible to the average Power BI developer.**
<br>
<br>

## Enter TMDL

TMDL (Tabular Model Definition Language) turns your entire Power BI model (including security) into **readable text files** that live right inside your Power BI project.

**Here's the best part:** RLS (row-level) and OLS (object-level) security can work **together** in the same role. You can filter which rows someone sees AND remove specific columns, all in one security definition.

Here's the complete security setup for our three roles. 

<details closed>
<summary>Here's the code:</summary>
	
```tmdl
createOrReplace

	/// 1. MANAGER: Only their team + NO Salary/Phone
	role 'Manager_Restricted'
			modelPermission: read

			tablePermission 'Employees' = [ManagerEmail] = USERPRINCIPALNAME()
				columnPermission 'PersonalPhone (OLS)' = none
				columnPermission 'HomeAddress (OLS)' = none

			tablePermission 'Compensation'
				metadataPermission: none


	/// 2. HR MANAGER: Only their team + YES Salary/Phone
	role 'HR_Manager_Reports'
    	modelPermission: read

    	tablePermission 'Employees' = [ManagerEmail] = USERPRINCIPALNAME()



	/// 3. HR GLOBAL ADMIN: The "Everything" Role
	role 'HR_Global_Admin'
    	modelPermission: read
```
</details>

<hr>

**That's it.** This TMDL script replaces potentially three separate Power BI files and three semantic models.

If you would like to follow along and run your own tests, use the TMDL script below to create the tables, sample data and relationships required for this use case.

<details closed>
<summary>Here's the code:</summary>

```
createOrReplace

	model Model
		culture: en-US
		defaultPowerBIDataSourceVersion: powerBI_V3
		sourceQueryCulture: en-US
		dataAccessOptions
			legacyRedirects
			returnErrorValuesAsNull

		/// Mixed Dimension
		table Employees
			lineageTag: 5b0ba414-d7ba-4ddf-85d1-758b4f46d60d

			column EmpID
				dataType: string
				lineageTag: 211d5de8-a81b-408c-904d-79d076d0a4e3
				summarizeBy: none
				sourceColumn: EmpID

				annotation SummarizationSetBy = Automatic

			column Name
				dataType: string
				lineageTag: db14ca69-88f0-4447-9358-6bd316b0150d
				summarizeBy: none
				sourceColumn: Name

				annotation SummarizationSetBy = Automatic

			column ManagerEmail
				dataType: string
				lineageTag: 8d9b59fd-af25-4abd-b315-b013efb20fa2
				summarizeBy: none
				sourceColumn: ManagerEmail

				annotation SummarizationSetBy = Automatic

			column Department
				dataType: string
				lineageTag: 971557ec-446c-46a6-8754-46550bdb18bf
				summarizeBy: none
				sourceColumn: Department

				annotation SummarizationSetBy = Automatic

			column 'PersonalPhone (OLS)'
				dataType: string
				lineageTag: 96c15aa8-f592-4684-ae83-40ec3dab7f95
				summarizeBy: none
				sourceColumn: PersonalPhone (OLS)

				annotation SummarizationSetBy = Automatic

			column 'HomeAddress (OLS)'
				dataType: string
				lineageTag: 35943e5c-6c42-44b4-bbc3-12d8381f1c0e
				summarizeBy: none
				sourceColumn: HomeAddress (OLS)

				annotation SummarizationSetBy = Automatic

			partition Employees = m
				mode: import
				source =
						let
						    Source = Table.FromRows(Json.Document(Binary.Decompress(Binary.FromText("jY/NDoIwEIRfZdMzGv6KehOUxINGA0fCoZQmNJZiEIm+vVvUYDhx6TSzs9/uZhmJbdshFgmV5AKVGd3ypr4x/Vqiohc/BX90sjd1SunCdoYWx/XgxKSGtCO5NZBctKOmwLdoigklZUrcR4KJ+jSAM7tCiOgvwUN7V7FWSTONf34T0iEZMSa/Wm/gIrWApPxhfLT3rJflnFVM2HMdiFX9dws1l/fztjDZgPoQyZZXcNQkz98=", BinaryEncoding.Base64), Compression.Deflate)), let _t = ((type nullable text) meta [Serialized.Text = true]) in type table [EmpID = _t, Name = _t, ManagerEmail = _t, Department = _t, #"PersonalPhone (OLS)" = _t, #"HomeAddress (OLS)" = _t]),
						    #"Changed Type" = Table.TransformColumnTypes(Source,{{"EmpID", type text}, {"Name", type text}, {"ManagerEmail", type text}, {"Department", type text}, {"PersonalPhone (OLS)", type text}, {"HomeAddress (OLS)", type text}})
						in
						    #"Changed Type"

			annotation PBI_NavigationStepName = Navigation

			annotation PBI_ResultType = Table

		/// Safe Fact
		table Performance
			lineageTag: 29f14b6a-ea94-4d1f-8471-393c9de9520a

			column EmpID
				dataType: string
				lineageTag: 0cc1fa6e-c6fe-4125-a2da-e2556162da80
				summarizeBy: none
				sourceColumn: EmpID

				annotation SummarizationSetBy = Automatic

			column ReviewDate
				dataType: dateTime
				formatString: Long Date
				lineageTag: 47137855-25fa-488d-ab9c-cab92e8d5d0c
				summarizeBy: none
				sourceColumn: ReviewDate

				annotation SummarizationSetBy = Automatic

				annotation UnderlyingDateTimeDataType = Date

			column Rating
				dataType: int64
				formatString: 0
				lineageTag: 4cc56bad-191c-471c-9d64-7864e3d3b20a
				summarizeBy: none
				sourceColumn: Rating

				annotation SummarizationSetBy = Automatic

			column TrainingHours
				dataType: int64
				formatString: 0
				lineageTag: e1cac331-f053-430b-9443-ca26b4342e2c
				summarizeBy: none
				sourceColumn: TrainingHours

				annotation SummarizationSetBy = Automatic

			partition Performance = m
				mode: import
				source =
						let
						    Source = Table.FromRows(Json.Document(Binary.Decompress(Binary.FromText("i45WcjUwMFHSUTIyMDLWNTTSNTAEckxB2EApVgcsbYouDVJvCJSOBQA=", BinaryEncoding.Base64), Compression.Deflate)), let _t = ((type nullable text) meta [Serialized.Text = true]) in type table [EmpID = _t, ReviewDate = _t, Rating = _t, TrainingHours = _t]),
						    #"Changed Type" = Table.TransformColumnTypes(Source,{{"EmpID", type text}, {"ReviewDate", type date}, {"Rating", Int64.Type}, {"TrainingHours", Int64.Type}})
						in
						    #"Changed Type"

			annotation PBI_NavigationStepName = Navigation

			annotation PBI_ResultType = Table

		/// Secret Fact
		table Compensation
			lineageTag: 2336151e-0d64-4620-bdd7-9ed928cdbb7f

			column EmpID
				dataType: string
				lineageTag: d7800ca2-4b7b-4be7-adbc-a48d9de8f7ca
				summarizeBy: none
				sourceColumn: EmpID

				annotation SummarizationSetBy = Automatic

			column Salary
				dataType: int64
				formatString: 0
				lineageTag: cbc9b094-5e3f-49ba-8ba2-3cb2b9803650
				summarizeBy: sum
				sourceColumn: Salary

				annotation SummarizationSetBy = Automatic

			column Bonus
				dataType: int64
				formatString: 0
				lineageTag: 23a4f863-b56f-4667-9187-0a682414be7e
				summarizeBy: sum
				sourceColumn: Bonus

				annotation SummarizationSetBy = Automatic

			partition Compensation = m
				mode: import
				source =
						let
						    Source = Table.FromRows(Json.Document(Binary.Decompress(Binary.FromText("i45WcjUwMFHSUTI3NTAwANIWICpWByxuCuSbQcVNwOKxAA==", BinaryEncoding.Base64), Compression.Deflate)), let _t = ((type nullable text) meta [Serialized.Text = true]) in type table [EmpID = _t, Salary = _t, Bonus = _t]),
						    #"Changed Type" = Table.TransformColumnTypes(Source,{{"EmpID", type text}, {"Salary", Int64.Type}, {"Bonus", Int64.Type}})
						in
						    #"Changed Type"

			annotation PBI_NavigationStepName = Navigation

			annotation PBI_ResultType = Table

		relationship 1aded688-ce28-ab8f-3f8b-7446208dedb2
			fromColumn: Employees.EmpID
			toColumn: Performance.EmpID

		relationship 21030618-6f60-9e71-1437-7e1724ff576d
			fromColumn: Compensation.EmpID
			toColumn: Employees.EmpID

		cultureInfo en-US

			linguisticMetadata = {"Version":"1.0.0","Language":"en-US"}
				contentType: json

		annotation __PBI_TimeIntelligenceEnabled = 0

		annotation PBI_QueryOrder = ["Employees","Performance","Compensation"]

		annotation PBI_ProTooling = ["TMDLView_Desktop"]

```
</details>

<hr>

and for the measures use this TMDL script:

<details closed>
<summary>Here's the code:</summary>

```
createOrReplace

	ref table Employees
		/// 1. Measures for the Employees tabl
		measure Headcount = COUNTROWS('Employees')
			formatString: #,0
			displayFolder: "Operational Metrics"

	ref table Performance
		/// 2. Measures for the Performance table
		measure 'Avg Rating' = AVERAGE('Performance'[Rating])
			formatString: 0.0
			displayFolder: "Operational Metrics"

		measure 'Total Training Hours' = SUM('Performance'[TrainingHours])
			formatString: #,0
			displayFolder: "Operational Metrics"

	ref table Compensation
		/// 3. Measures for the Compensation table (SENSITIVE)
		measure 'Total Payroll' = SUM('Compensation'[Salary]) + SUM('Compensation'[Bonus])
			formatString: "\$#,0;(\$#,0);\$#,0"
			displayFolder: "Financial Metrics"

		measure 'Avg Salary' = AVERAGE('Compensation'[Salary])
			formatString: "\$#,0;(\$#,0);\$#,0"
			displayFolder: "Financial Metrics"

		measure 'Efficiency Ratio' = [Total Payroll] / SUM('Performance'[Rating])
			formatString: "0.00"
			displayFolder: "Financial Metrics"
```
</details>

<hr>

<br>

## Why this is brilliant

Look at what's happening in that `Manager_Restricted` role:

**The tablePermission with DAX filter:** `tablePermission 'Employees' = [ManagerEmail] = USERPRINCIPALNAME()`  

→ This is **dynamic RLS**: ONE role works for all managers. 

The DAX expression `USERPRINCIPALNAME()` automatically filters to show each manager only their own team. No creating "Manager_Alice," "Manager_Bob," "Manager_Charlie". One dynamic role scales to hundreds of managers.

**The columnPermission settings:** `columnPermission 'PersonalPhone (OLS)' = none`  

→ This is **OLS working WITH RLS**: Even for the rows they CAN see (their team), these columns are **completely inaccessible**, not just hidden, but locked. Try to reference them in a measure? Error. Try to unhide them? They don't exist for this role.


**The Compensation table permission:** `tablePermission 'Compensation'` with `metadataPermission: none`  

→ The entire Compensation table vanishes for this role, **table-level OLS**. Not "hidden in the field list" - the table literally doesn't exist in their report.


**HR_Global_Admin view**
<img width="2467" height="1131" alt="Pasted image 20260215090756" src="https://github.com/user-attachments/assets/7ec28f00-262a-47b5-b61e-f8cc74d2ba6e" />



**Testing Manager_Restricted role**
Expectations:
	- no access to Compensation table
	- no access to measures referencing that table
	- no access to columns "PersonalPhone (OLS)" and "HomeAddress (OLS)"


Do you see how easy it is to read and audit this role?

<img width="800" height="300" alt="Pasted image 20260215100504" src="https://github.com/user-attachments/assets/48f00ec1-6979-4332-a8fa-2e599c6d4a38" />

<br>


<img width="369" height="372" alt="Pasted image 20260215090451" src="https://github.com/user-attachments/assets/689027cd-136b-4129-bd47-484e961f5d20" />

<br>

Let’s verify the behavior works as expected.
<img width="2509" height="1150" alt="Pasted image 20260215090522" src="https://github.com/user-attachments/assets/fa322ffc-8b0e-44de-bdcf-ef4c645809c6" />





**This is a killer combination:** Dynamic RLS + Column OLS + Table OLS, all in one role definition. That's what makes this powerful.
<br>
<br>

## The accessibility difference is everything

**Before TMDL (using Tabular Editor):**

- Download and learn to use an external tool with a different UI
- Configure security in one tool, develop in another
- **Limited visibility in Power BI Desktop**: column-level restrictions aren't clearly visible in the UI
- Security settings are invisible to team members who don't have Tabular Editor
- Collaboration: Difficult (not everyone has or knows Tabular Editor)

<br>
<br>

**With TMDL:**

- Security lives in **text files inside your Power BI project**
- Open in any text editor (VS Code, Notepad, whatever)
- **Completely visible and readable**
- Version controlled in Git
- Peer reviewable (pull requests)
- Time: 2-5 minutes for 3 roles (copy-paste and edit)
- Collaboration: Anyone can read and edit text files

Need 10 department-specific roles? Copy-paste the block 10 times, change one line each. Done in 5 minutes.

Business rules change and now managers should also filter by another attribute? Add one line to the DAX filter across all manager roles with find-and-replace. In Tabular Editor's UI, you'd click through each role individually.


>[!TIP]
>This is a genuine TMDL win : when your business rules evolve and you need to update security filters across multiple roles, TMDL's text format makes it trivial while UI-based tools require repetitive clicking.

<br>

**The impact:** Your security configuration is **accessible to everyone on your team**.

<br>
<br>

## The real positive impact: security you can actually see and share

This is the part that fundamentally changes how teams work with Power BI security:

**In TMDL:**

- Your entire security architecture is **visible text files** in your project folder
- An auditor can verify your security model in 30 seconds by reading the `.tmdl` file
- Junior developers can learn by reading the code, it's self-documenting
- Security lives in Git with your other code

Security configuration is no longer hidden in binary .pbix files or external tools. It's **plain text that anyone can read, review, and understand**.

<br>
<br>


## Conclusion

**One Power BI file. Three security roles. Zero maintenance nightmares. One semantic model instead of three.**

TMDL didn't just make OLS "easier", it made it **visible, auditable, and accessible to every Power BI developer**.

The capability existed before through Tabular Editor, but because it required specialized knowledge, many organizations never used it. They built multiple datasets instead, paying the price in maintenance burden and compute costs.

TMDL changes the equation: we can move from external tools requiring specialized knowledge to **text files anyone can edit**. 

