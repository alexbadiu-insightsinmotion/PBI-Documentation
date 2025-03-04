

### Data Quality and Automated Testing in Power BI

<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Issue%206.png" />


Ever had a report go live after testing, only to have end users report issues that could have been identified earlier?

A common challenge persists across many organizations and that is **the lack of structured testing protocols** before deploying Power BI solutions to production environments. Too often, we rely on superficial checks and subjective approvals ("**X said it looks good**") rather than systematic verification. This article explores three key benefits of automated testing in Power BI: maintaining data quality, improving documentation standards, and building client confidence through professional development practices.

##### Table of Contents  
[Why Automated Testing Matters for PBI](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#why-automated-testing-matters-for-power-bi) <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Beyond Manual Verification](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#beyond-manual-verification) <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Build Client Confidence](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#building-client-confidence) <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Definition of Done in Power BI projects](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#definition-of-done-power-bi-drill-through-functionality) <br>
[Introducing DAX QUERY VIEW](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#introducing-dax-query-view) <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Automated Testing Methodology in PBI via DAX QUERY VIEW](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#automated-testing-methodology-in-power-bi-via-dax-query-view) <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Types of Tests Possible in DAX QUERY VIEW](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#types-of-tests-possible-in-dax-query-view) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1. Data Quality Tests](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#1-data-quality-tests) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2. Referential Integrity Tests](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#2-referential-integrity-tests) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3. Calculation Consistency Tests](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#3-calculation-consistency-tests) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4. Business Rule Tests](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#4-business-rule-tests) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5. Completness Tests](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#5-completeness-tests) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6. Intermediate Calculation Tests](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#6-intermediate-calculation-tests) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[7. Historical Comparison Tests](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#7-historical-comparison-tests) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[8. Aggregation Tests](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#8-aggregation-tests) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[9. Schema Tests](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#9-schema-tests) <br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[10. Consolidation Testing Approach](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#consolidated-testing-approach) <br>
[Summary](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#summary) <br>
[Conclusion](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#conclusion) <br>
[Read More](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/06%20-%20BEFORE%20RELEASE%20-%20Automated%20Testing%20in%20Power%20BI.md#read-more)

### Why Automated Testing Matters for Power BI

#### Beyond Manual Verification

Traditional testing approaches for Power BI reports often consist of visual inspections and basic data sampling **very often limited only to new features** to be delivered. While these methods can catch obvious errors, **they're limited by human fallibility and preconceptions**, inconsistent application, and inability to scale. Humans tend to discount earlier things they may have otherwise noticed, especially during re-testing (I don't need to look at this as I've checked it before...). Automated testing provides a systematic approach that ensures comprehensive **coverage across all new and old (regression testing) features.**

#### Building Client Confidence

Demonstrating **a robust testing framework communicates professionalism and attention to detail** that builds confidence. Rather than stating **"we've checked it works,**" teams can **provide evidence through documented test results** that ensure data accuracy.

#### Definition of Done in Power BI projects

Definition of Done is a shared understanding of **what "complete" means for any deliverable**. It's a checklist of criteria that must be met before work is considered finished.

##### Definition of Done: Power BI Drill-Through Functionality

Implementation of custom drill-through functionality allowing users to navigate from summary visualizations to detailed reports based on selected data points.

> [!NOTE]  
>Example of Definition of Done Criteria
>1. **Functionality Requirements:**
>   - Drill-through action configured on all summary visuals
>   - Target detailed pages created with proper filtering context
>    - Custom tooltip hints indicating drill-through availability
>2. **Performance Requirements**
>   - Drill-through action completes in under 3 seconds
>   - No noticeable performance degradation on source pages
>   - Memory usage remains within allocated thresholds
> 3. **Testing Requirements**
>   - Functionality verified across different browsers
>   - Testing completed with various data volumes (small, medium, large selections)
>   - Edge cases handled (null values, etc.)
>   - Dedicated accuracy tests developed for automated testing
>   - If the testing is conducted in the TEST environment, the results may not be at all reflective of the PROD environment, which likely has different networks performance and security criteria.
> 4. **Documentation and training**
>   - Technical documentation updated with implementation details
>   - User guide created with step-by-step instructions
>   - Training materials prepared for end users
>   - Video demonstration created for knowledge base
> 5. **Security**
>   - Row-level security propagated correctly through drill-through actions
> 6. **Quality Assurance**
>   - Code review completed by senior developer
>   - All test cases passed and documented
>   - No high or critical bugs remaining
>   - Stakeholder sign-off received
> 7. **Deployments**
>   - Feature deployed to development environment
>   - UAT completed with stakeholder approval
>   - Release notes prepared
>   - Rollback plan documented


##### What it serves

- Creates **clarity on quality expectations**
- **Prevents incomplete work** from moving forward
- **Reduces rework and technical debt**
- Builds **consistency across team deliverables**
- Establishes **a common language between technical and business stakeholders**

##### How automated testing relates to DoD (Definition of Done) in Power BI

Automated testing in Power BI directly supports DoD by:
- Providing **objective verification of calculation accuracy**
- **Decomposing complex logic into smaller**, testable DAX 
- **Documenting business rules as executable tests**
- Creating a **repeatable validation process**
- **Preserving test cases** alongside the model in version control


> [!TIP]
> Automated testing methodology will help  **develop a library of reusable tests**. This approach makes it **easier to scale testing** as your "regression" tests are already developed and also **serve as template for other Power BI projects.**

# Introducing DAX QUERY VIEW

As Power BI reports and data models become **more complex and business-critical**, implementing automated testing becomes increasingly important. **Testing helps ensure that calculations are accurate, data is complete, and the business logic is correctly implemented.** However, Power BI lacks built-in testing capabilities found in more traditional software development environments.

This is where **DAX Query View** offers a solution. By leveraging DAX queries, analysts and developers can implement a comprehensive testing methodology directly within their Power BI models. This approach allows for **validation of data quality, calculation accuracy, and business rule compliance** without requiring external tools or processes.

The following methodology outlines how to implement systematic testing in Power BI using DAX Query View, starting with creating a structured approach to document test cases, and then executing those tests through DAX queries. These tests can validate everything from basic data quality to complex business rules, **all while being saved as part of your model and visible in version control systems.**

By implementing this approach, you can significantly **increase confidence** in your Power BI reports, **reduce errors**, and **quickly identify issues** if/when they occur - all through a single, unified testing interface that requires just one click to execute.


### Automated Testing Methodology in Power BI via DAX Query View

#### How to Create Automated Testing

##### 1. Create a Reference Excel File

Document with the PO or business expert matter the automated tests to be performed:

- Test name
- Priority
- Expected values
- Allowed variance percentage
- DAX code to test

For each new KPI created, document the definition and business rules as explained in last week Greg's article [05 - What content is in a Design Document - Workflow Issues Business Rules](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/05%20-%20What%20content%20is%20in%20a%20Design%20Document%20-%20Workflow%20Issues%20Business%20Rules.md#business-rules)  and request an example (e.g., number of employees in France in December 2024). This Excel file will serve as a reference and be part of the "Definition of Done" criteria.

##### 2. Import the Excel File into Power BI

Integrate this file as a disconnected table in your model.

<img width="920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302174444.png" />

##### 3. Create a DAX Query in DAX Query View

Use the following structure for your tests:

<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302174647.png" /> <br>

##### You can access the DAX CODE HERE -> [DAX Query View | Script - DAX Test Pattern](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/DAX%20Test%20Pattern) 

> [!IMPORTANT]  
>**Tests are performed each time you click RUN**. The best part is that they're saved with your model and can be seen in DevOps/GitHub.

### Types of Tests Possible in DAX Query View

#### 1. Data Quality Tests

Access the 'quick queries' menu by right-clicking on any table in the model view, from the DAX Query View, then select 'Show column statistics' to reveal built-in analytical functions that can be used for testing.

- Number of distinct values
- Minimum and maximum values
- Medians and averages
- Number of null or zero values
- Value distribution

example: Number of different countries in the dimension table should be 45

```dax
EVALUATE
ROW(
    "Test Name", "Customer Table - Count of Distinct Countries",
    "Expected Value", 45,
    "Actual Value", DISTINCTCOUNT('Customer'[Country]),
    "Allowed variance %", 0,
    "Test Passed", DISTINCTCOUNT('Customer'[Country]) = 45
)
```
##### You can access the DAX CODE HERE -> [DAX Query View | Script - Data Quality Test 1](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Data%20Quality%20Test%201) 

Another example:

<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302164910.png" />

##### You can access the DAX CODE HERE -> [DAX Query View | Script - Data Quality Test 2](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Data%20Quality%20Test%202) 


#### 2. Referential Integrity Tests

Verify that all foreign keys correspond to existing primary keys:

>[!TIP]
>It’s essential to check referential integrity in Power BI to ensure that relationships between tables are consistent and reliable, preventing orphaned data and ensuring accurate analyses.


```
FILTER(
INFO.STORAGETABLES(),
[RIVIOLATION_COUNT]>0)
```
##### You can access the DAX CODE HERE -> [DAX Query View | Script - Referential Integrity 1](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Referential%20Integrity%201) 

<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302163340.png" />


A more detailed query identifying what Dimensions are in RI violation and the exact number of rows impacted.

<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302163105.png" />

##### You can access the DAX CODE HERE -> [DAX Query View | Script - Referential Integrity 2](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Referential%20Integrity%202) 

Another example for checking orphaned records:

```dax
EVALUATE
ROW(
    "Test Name", "F_Client_Overdraft with Invalid Code MIG",
    "Expected Value", 0,
    "Actual Value", COUNTROWS(FILTER(F_CLIENT_OVERDRAFT, NOT(F_CLIENT_OVERDRAFT[CODE_MIG] IN VALUES(D_STRUCTURES[CODE_MIG])))),
    "Allowed variance %", 0,
    "Test Passed", COUNTROWS(FILTER(F_CLIENT_OVERDRAFT, NOT(F_CLIENT_OVERDRAFT[CODE_MIG] IN VALUES(D_STRUCTURES[CODE_MIG])))) = 0
)
```
##### You can access the DAX CODE HERE -> [DAX Query View | Script - Referential Integrity 3](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Referential%20Integrity%203) 

<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302164128.png" />

#### 3. Calculation Consistency Tests

Validate that different calculation methods produce consistent results.

This test makes sense because it validates that the overall Total Sales measure is exactly the sum of its quarterly components, ensuring the aggregation logic is correct and consistent within an acceptable margin.
```dax
EVALUATE
ROW(
    "Test Name", "Total Sales - Sum equals aggregated quarters",
    "Expected Value", [Total Sales],
    "Actual Value", [Q1 Sales] + [Q2 Sales] + [Q3 Sales] + [Q4 Sales],
    "Allowed variance %", 0.001,
    "Variance %", ABS(1-DIVIDE([Total Sales], [Q1 Sales] + [Q2 Sales] + [Q3 Sales] + [Q4 Sales])),
    "Test Passed", ABS(1-DIVIDE([Total Sales], [Q1 Sales] + [Q2 Sales] + [Q3 Sales] + [Q4 Sales])) <= 0.001
)
```
##### You can access the DAX CODE HERE -> [DAX Query View | Script - Referential Integrity 3](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Referential%20Integrity%203) 

#### 4. Business Rule Tests

Verify that business constraints are met.

This query validates that Sales table has a non-negative Gross Margin, flagging the test if any negative values are found.

```dax
EVALUATE
ROW(
    "Test Name", "Gross Margin always positive",
    "Expected Value", 0,
    "Actual Value", COUNTROWS(FILTER(Sales, [Gross Margin] < 0)),
    "Allowed variance %", 0,
    "Test Passed", COUNTROWS(FILTER(Sales, [Gross Margin] < 0)) = 0
)
```
##### You can access the DAX CODE HERE -> [DAX Query View | Script - Business Rules](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Business%20Rules%20Tests) 

#### 5. Completeness Tests

Ensure all dimensions contain the expected members.

This DAX test validates that the 'Product Categories' table **contains exactly the ten expected categories** by comparing the count of matching categories against an expected value of 10.

```dax
EVALUATE
ROW(
    "Test Name", "Product Categories - All expected categories present",
    "Expected Value", 10,
    "Actual Value", COUNTROWS(FILTER('Product Categories', 
                       [Category] IN {"Category1", "Category2", "Category3", "Category4", "Category5", 
                                     "Category6", "Category7", "Category8", "Category9", "Category10"})),
    "Allowed variance %", 0,
    "Test Passed", COUNTROWS(FILTER('Product Categories', 
                   [Category] IN {"Category1", "Category2", "Category3", "Category4", "Category5", 
                                 "Category6", "Category7", "Category8", "Category9", "Category10"})) = 10
)
```
##### You can access the DAX CODE HERE -> [DAX Query View | Script - Completness test](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Completness%20Tests) 

#### 6. Intermediate Calculation Tests

Break down complex calculations to identify problematic steps.

This test makes sense because it helps catch errors early, clarifies complex logic for maintenance, and provides documented evidence of expected outcomes for easier troubleshooting and future development.

```dax
EVALUATE
ADDCOLUMNS(
    SUMMARIZE(
        Sales,
        Sales[Year]
    ),
    "Base Revenue", [Base Revenue],
    "Discounts", [Total Discounts],
    "Taxes", [Total Taxes],
    "Expected Net Revenue", [Base Revenue] - [Total Discounts] + [Total Taxes],
    "Actual Net Revenue", [Net Revenue],
    "Difference", [Net Revenue] - ([Base Revenue] - [Total Discounts] + [Total Taxes]),
    "Test Passed", ABS([Net Revenue] - ([Base Revenue] - [Total Discounts] + [Total Taxes])) < 0.01
)
```
##### You can access the DAX CODE HERE -> [DAX Query View | Script - Intermediate Calculation](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Intermediate%20Calculation) 

#### 7. Historical Comparison Tests

Check that certain metrics remain consistent with historical data.


```dax
EVALUATE
ROW(
    "Test Name", "Average Order Value - Within historical bounds",
    "Min Historical", 250,
    "Max Historical", 350,
    "Current Value", [Average Order Value],
    "Test Passed", [Average Order Value] >= 250 && [Average Order Value] <= 350
)
```
##### You can access the DAX CODE HERE -> [DAX Query View | Script - Historical Comparison](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Historical%20Comparison) 

#### 8. Aggregation Tests

Validate that different aggregation levels are consistent.

Check that Total Revenue equals sum of regional revenues

```dax
EVALUATE
ROW(
    "Test Name", "Total Revenue equals sum of regional revenues",
    "Total Revenue", [Total Revenue],
    "Sum of Regions", SUMX(VALUES(Region[RegionName]), CALCULATE([Total Revenue])),
    "Difference", [Total Revenue] - SUMX(VALUES(Region[RegionName]), CALCULATE([Total Revenue])),
    "Test Passed", ABS([Total Revenue] - SUMX(VALUES(Region[RegionName]), CALCULATE([Total Revenue]))) < 0.01
)
```
##### You can access the DAX CODE HERE -> [DAX Query View | Script - Aggregation Test](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Aggregation%20Tests) 

#### 9. Schema Tests

Validating schema consistency is crucial because any unexpected changes in your central model can break dependent reports, leading to errors and inaccurate analyses. Ensuring the schema remains consistent safeguards the integrity of all connected reports and minimizes disruptions and costly troubleshooting.

##### You can access the DAX CODE HERE -> [DAX Query View | Script - Schema Test](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/Schema%20Tests) 

<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302164756.png" />

#### Consolidated Testing Approach

All of the tests described above **can be integrated into** the structure shown in section 3, allowing you to have **a single query that runs all tests with one click**. This provides a comprehensive overview of your model's quality and accuracy. Here's how you can consolidate them:

Your excel structure should be similar to this :
<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302170807.png" />

DAX Query structure :
<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302170649.png" />

**DAX Code** based on excel <br>
<img width="520" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302171047.png" />

##### You can access the DAX CODE HERE -> [DAX Query View | Script - DAX Code Script](https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/DAX%20Query%20View%20/DAX%20Test%20Pattern) 

Result of "DAX Code"  in Visual Studio Code -> Copy for each ID test the corresponding DAX formula
<img width="1920" alt="Issue 6" src="https://github.com/alexbadiu-insightsinmotion/Documentation/blob/main/Images/Pasted%20image%2020250302171019.png" />

This way, you can run your entire test suite with a single click in DAX Query View, giving you a comprehensive snapshot of your model's quality and reliability. The results will show you at a glance which tests have passed and which need attention **BEFORE considering publishing** to DEV environment or committing to a dev branch.


### Summary

Implementing a formal Definition of Done with embedded testing improves significantly Power BI development. By documenting expected outcomes in an Excel and validating them with DAX Query queries tests, teams can objectively measure when a report meets business requirements. This structured approach **ensures consistency, builds confidence in reports, and significantly reduces errors in production.**

### Conclusion

While this article focuses on testing within Power BI using DAX Query View, it's crucial to understand **that data quality testing should be included throughout the entire project lifecycle**, from data ingestion to final report distribution. The testing methodology described here addresses the Power BI developer's scope, but represents just one component of a comprehensive data quality strategy.

Effective organizations implement quality gates at multiple stages: during ingestion, ETL (Extract Transform Load), data pipeline development, within the data warehouse / lakehouse, and finally in Power BI reports. For advanced implementations, consider exploring CI/CD Azure pipelines with PR-triggered (Pull Request) automated tests. For guidance on implementing these advanced techniques, see our read more section. Each layer should have appropriate testing mechanisms that verify data integrity, transformation accuracy, and business rule compliance.

By integrating testing across the entire data flow and making it a core part of your Definition of Done at each stage, you create a robust foundation for reliable, trustworthy business intelligence that stakeholders can confidently use for decision-making.

### Read more

- Great detailed presentation on IOWA PBI User Group with James Bartlett and Narayana Windenberger : https://www.youtube.com/live/PL7Xw2dvVrE?si=FJ7j7ZLtLiiWrKTl

- John Kerski blog: [DAX Query View Testing Pattern | John Kerski’s Blog](https://www.kerski.tech/bringing-dataops-to-power-bi-part36/)
