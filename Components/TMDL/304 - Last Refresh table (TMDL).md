<img width="1280" height="700" alt="304 - Image - Title - TMDL Last Refresh table" src="https://github.com/user-attachments/assets/e37bcc8e-8e05-4543-851b-f4dd116ffa53" />

## Last Refresh Table

One item that should be displayed in every Power BI report is the date (and time) the data was last refreshed. Only with this information can one properly interpret the data behind the report and take actions upon its' insights. To that end, reports often have a supporting table for *Last Refresh* complete with some measures to expose this information. *(Each time the Power BI Service refreshes a report, all tables are recalculated, including the *Last Refresh* table, and it will always reflect the last date and time a refresh instance was started.)*

Adding a *Last Refresh* table to a Power BI report involves several steps. The example TMDL script below performs several tasks, including:

- create the *Last Refresh* table from source ***Power Query/M*** code
  - *includes [Last Refresh] (datetime), [Date] (date only), and [Time] (time only) columns*
- hides the table and all columns from report viewers
- sets the *format* for the [Last Refresh] column to ***yyyy-mm-dd h:nn:ss AM/PM***
- sets the *format* for the [Date] column to ***yyyy-mm-dd***
- sets the *format* for the [Time] column to ***hh:nn:ss AM/PM***

<details closed>
<summary>Here's the code:</summary>

```
createOrReplace

	table 'Last Refresh'
		isHidden: true

		column 'Last Refresh'
			dataType: dateTime
			isHidden: true
			formatString: yyyy-mm-dd h:nn:ss AM/PM
			summarizeBy: none
			sourceColumn: Last Refresh

			annotation SummarizationSetBy = Automatic

			annotation PBI_FormatHint = {"isDateTimeCustom":true}

		column Date
			dataType: dateTime
			isHidden: true
			formatString: yyyy-mm-dd
			summarizeBy: none
			sourceColumn: Date

			annotation SummarizationSetBy = Automatic

			annotation UnderlyingDateTimeDataType = Date

			annotation PBI_FormatHint = {"isDateTimeCustom":true}

		column Time
			dataType: dateTime
			isHidden: true
			formatString: hh:nn:ss AM/PM
			summarizeBy: none
			sourceColumn: Time

			annotation SummarizationSetBy = Automatic

			annotation UnderlyingDateTimeDataType = Time

			annotation PBI_FormatHint = {"isCustom":true}

		partition 'Last Refresh' = m
			mode: import
			source =
					let
					  Source = DateTime.FixedLocalNow(),
					  ConvertToTable = #table( 1, {{Source}} ),
					  RenameColumn = Table.RenameColumns( ConvertToTable, {{"Column1", "Last Refresh"}} ),
					  ChangeType = Table.TransformColumnTypes( RenameColumn, {{"Last Refresh", type datetime}} ),
					
					  AddDate = Table.AddColumn( ChangeType, "Date", each DateTime.Date( [Last Refresh] ), type date ),
					  AddTime = Table.AddColumn( AddDate, "Time", each DateTime.Time( [Last Refresh] ), type time ),
					
					  FINAL_QUERY = AddTime
					in
					  FINAL_QUERY

		changedProperty = IsHidden

		annotation PBI_NavigationStepName = Navigation

		annotation PBI_ResultType = Table
```
</details>

<br>

*-- eof*
