<img width="1280" height="720" alt="306 - Image - Title - Measures - GP Mockup" src="https://github.com/user-attachments/assets/c287b419-f97a-4d2e-904b-2482fa2a75f3" />

## Key Measures table

A dedicated ***Measures*** table is often created in many Power BI reports. This, along with display folders, can provide a single location for all measures and thus enhance usability. 

The example TMDL script below performs several tasks, including:

- creates an empty *Key Measures* table
- creates an [m1] placeholder measure
- deletes the [Column 1] column

<details closed>
<summary>Here's the code:</summary>
	
``` tmdl
createOrReplace

	table 'Key Measures'

		/// < placeholder measure - delete after other measures created >
		measure 'm1' = 1	

		partition 'Key Measures' = m
			mode: import
			source = 
					let
						Source = Table.FromRows(
							Json.Document(Binary.Decompress(Binary.FromText("i44FAA==", BinaryEncoding.Base64), Compression.Deflate)),
							let
								_t = ((type nullable text) meta [Serialized.Text = true])
							in
								type table [Column1 = _t]
						),
						#"Changed Type" = Table.TransformColumnTypes(Source, {{"Column1", type text}}),
						#"Removed Columns" = Table.RemoveColumns(#"Changed Type", {"Column1"})
					in
						#"Removed Columns"

		annotation PBI_ResultType = Table
```
</details>

<hr>

## Base Measures

TMDL scripts can be used to update an existing object. Many standard measures (or ***base measures***) are often created in a Power BI model. Four example base measures are added to the existing *Key Measures* table, and several tasks are performed, including:

- reference the existing *Key Measures* table
- creates a [Total Sales] measure (= sum of revenue) (format set to #,##0)
- creates a [Total Costs] measure (= sum of costs) (format set to #,##0)
- creates a [Total Profit] measure (= [Total Sales] - [Total Costs]) (format set to #,##0)
- creates a [Margin %] measure (= [Total Profit] / [Total Sales]) (format set to 0%)

The DAX code behind each measure can be added as a *Description* using the 3-slash notation.

## Last Refresh measures

As noted above, TMDL scripts can be used to update an existing object. Three example *Last Refresh* measures measures are added to the existing *Key Measures* table, and several tasks are performed, including:

- reference the existing *Key Measures* table
- creates a [Last Refresh Date] measure (= max 'Last Refresh'[Date]) (format set to dd-mmm-yyyy)
- creates a [last Refresh DateTime Costs] measure (= max 'Last Refresh'[Last Refresh]) (format set to dd-mmm-yyyy h:nn:ss AM/PM)
- creates a [Total Profit] measure (= difference in dates between today and the [Last Refresh Date]) (format set to #,0)

All measures are set to display in the *x_Last_Refresh* folder.

## Report Administration measures

As noted above, TMDL scripts can be used to update an existing object. 

Three example *Report Administration* measures are added to the existing *Key Measures* table, and several tasks are performed, including:

- reference the existing *Key Measures* table
- creates a [Report ID] measure (hard-coded string)
- creates a [Version] measure (hard-coded string)
- creates a [Version Date] measure (hard-coded DAX value) (format set to dd-mmm-yyyy)

All measures are set to display in the *z_Admin* folder.

It is incumbent upon the developer to update the [Report ID] measure once upon report create and to update the [Version] and [Version Date] measures before each deployment.

<hr>

Here's the code to create Base, Last Refresh, and Report Administration measures in the ***Key Measures*** table:

<details closed>
<summary>Here's the code:</summary>

``` tmdl
createOrReplace

	ref table 'Key Measures'

		/// Sales = Sum of Sales
		measure 'Total Sales' = SUM( Sales[Sales] )
			formatString: #,##0			

		/// Costs = Sum of Costs
		measure 'Total Costs' = SUM( Sales[Costs] )
			formatString: #,##0			

		/// Profit = Sales - Costs
		measure 'Total Profit' = [Total Sales] - [Total Costs]
			formatString: #,##0		

		/// Margin % = Profit / Sales
		measure 'Margin %' = DIVIDE( [Total Profit], [Total Sales], 0 )
			formatString: 0%			



		measure 'Last Refresh Date' = MAX( 'Last Refresh'[Date] )
			formatString: dd-mmm-yyyy
			displayFolder: x_Last_Refresh

			annotation PBI_FormatHint = {"isDateTimeCustom":true}

		measure 'Last Refresh DateTime' = MAX( 'Last Refresh'[Last Refresh] )
			formatString: dd-mmm-yyyy h:nn:ss AM/PM
			displayFolder: x_Last_Refresh

			annotation PBI_FormatHint = {"isDateTimeCustom":true}

		measure 'Last Refresh Days Old' = DATEDIFF( TODAY(), [Last Refresh Date], DAY )
			formatString: #,0
			displayFolder: x_Last_Refresh



		measure 'Report ID' = "AR01"
			displayFolder: z_Admin

		measure Version = "0.1"
			displayFolder: z_Admin

		measure 'Version Date' = DATE( 2025, 7, 21 )
			formatString: dd-mmm-yyyy
			displayFolder: z_Admin

		measure 'Report Admin' = [Report ID] & UNICHAR(10) & FORMAT( [Last Refresh Date], "DD-MMM-YYYY" )
			displayFolder: z_Admin


```
</details>

<br>

*-- eof*
