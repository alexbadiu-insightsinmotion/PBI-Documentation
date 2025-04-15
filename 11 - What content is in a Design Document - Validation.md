<img width="1920" alt="11 - Image - Title - Validation" src="https://github.com/user-attachments/assets/f3e173c7-ea82-461b-bb10-206ec33d1878" />

**What Validation characteristics should be described in a Design Document?**

Validation must be successfully completed before any report is rolled-out. Ideally one would use automated validation, but many organizations (especially smaller ones) implement and rely on manual validation to decide if a report is ready for production use.

A discussion of automated validation was presented earlier by Alex in [issue #6](<https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/06%20-%20Automated%20Testing%20in%20Power%20BI.md>) of this series. Manual testing is the subject of this issue.

Also presented here is a general discussion of some components of the three main areas of manual validation: development testing, acceptance testing, and production testing.

## Validation Spreadsheet

One way to itemize and clarify manual validation is to prepare a table of the required tests. Such a table might have columns for:

* Test group (ID and name)
* Test (ID, name, notes, priority, expected results, and tolerance/allowed variance)
* Procedure (setup [steps], procedure [steps], actual results, and teardown [steps])
* Date (date and time performed and by whom)
* Status (pass, fail, deferred)

This is one area where it may actually be beneficial to NOT include all specifics in the design document, but to use a separate spreadsheet instead.

An example spreadsheet with a few possible tests for an invoicing system is shown below:

<img width="1687" alt="11 - Image - Validation Spreadsheet - 2" src="https://github.com/user-attachments/assets/0d6f5434-671a-4878-8b89-416607a36c86" />

### General

A test name should follow a consistent naming scheme and be short but fully described. As well, tests should be categorized into groups and have a priority level (e.g., P1, P2, P3, critical, major, minor, etc.).

> [!TIP]
> Assign a unique ID to every test and test group to avoid misunderstandings

### Setup and Teardown

Effective testing needs a consistent starting system state. Also known as an ***initial state***, it is the system loaded with a known set of data from the source systems.

Setup is the preparation of the test system for an upcoming test, or, said another way, is the changes necessary ***to change the test system from its initial state to being prepared for conduction of the test***. The setup steps should be clearly stated (easily repeatable) as they may be performed many times.

Teardown is the restoration of the test system to the initial state, or, alternatively, the changes necessary ***to return the test system to its initial state after the execution of the test***. Again, the steps should be clearly stated (easily repeatable) as they may be performed many times.

### Results

The expected results are those determined from the source systems (i.e., those providing the data for the report) before the test.

The actual results are those determined from executing the test in the test system (i.e., the report itself).

The variance is the difference between the expected results and the actual results. When expressed as a percentage, this can easily be compared to a tolerance (or allowed variance) to determine the success or failure of the test.

### Status

The date the test was conducted, the name of the person who conducted the test, and the status of the test must be recorded. All tests that were completed must have these 3 items, while there should be explanatory notes describing the cause/situation for any tests that were deferred.

This information, when viewed along with the test priorities, will allow fact-based evaluation of whether a system (report) passed the validation and is ready for deployment to the production environment.

## Development Testing

Development testing is an inherent part of the development process and will be performed by the developers on a continuous basis during the development period.

### Design Criteria

Test cases should be provided to the developers during the development period to ensure that the criteria that will be used during acceptance testing are used to develop the solution.

Each test case should describe a scenario and expected behaviour, including normal, alternate, and exception paths where appropriate.

> [!TIP]
> *One of the best ways to increase project velocity is to write the test cases as early as possible in the development cycle; the developers can then take the test criteria into account when designing and iterating the solution. (If the test cases are not developed until acceptance testing, it decreases the likelihood that the solution will perform as desired and meet expectations.)*

### Unit Testing

Unit testing will be conducted on individual system components by the developers throughout the development period.

### Integration Testing

Integration testing will be conducted on the system as a whole by the developers throughout the development period and will verify the connections between modules (reports) and data sources.

For reports that serve multiple audiences, integration testing should be conducted for each audience (e.g., IT, administrators, users, external, etc.).

## Acceptance Testing

Acceptance testing should be conducted by persons different than the developers who will ideally be those responsible (i.e., the business users) for ensuring the reports meet business acceptance criteria. This is also commonly referred to as UAT, or User Acceptance Testing.

If acceptance testing is not conducted and one instead relies on developer testing, then the impacts and risks must be accepted, such as:

- The DEV environment may not be reflective of the PROD environment (e.g., workstation specifications, network [geographical] performance, etc.)
- Developers will test their understanding of how the system (report) works, which is not necessarily how the system (report) should work
  - To mitigate this impact, it is imperative that the report specifications are exhaustive and handle all normal, alternate, and exception flows
- Developers often have elevated permissions in the DEV environment and, as a result, system (report) security may not be adequately verified
- The DEV environment often has reduced data volume, variety, and freshness compared to the PROD environment

Acceptance testing should be conducted in a dedicated testing environment that:

- Is configured in the same fashion as the production environment
- Has representative data variety, freshness, volume, and access:
  - To give confidence that testing will reflect use in the production environment
  - To leverage the business knowledge of the testers (business users) as to whether values are correct or within tolerance ranges

In addition, appropriate accounts need to be available for testers to utilize during testing to confirm solution security.

### Feature Testing

At the most basic level, if the system (report) doesn’t exhibit the features scoped, then the system (report) has not met its’ purpose. All features should therefore be covered during acceptance testing to verify that the system (report) meets its’ requirements.

### Standards Testing

Standards testing will be dependent upon the organization and will reflect the norms that are expected by any existing report in the organization (e.g., page transitions in less than 1 second, matrix refreshes after slicer selections in less than 2 seconds, etc.). Further, an organization may have standard theming and visual layout that should be used (e.g., fonts, colours, shadings, sidebar navigation, etc.), and this too should be verified.

Standards testing should also always be conducted with a fixed configuration/environment (e.g., Windows 11 Home 64-bit, Intel I5 processor, 8 GB RAM, browser used = Microsoft Edge version 1.35.0, network normal usage level [e.g., not Between 9-11 am ET, not overnight (11pm-7am)], etc.).

### Performance Testing

Even though a system (report) may exhibit all required features and meet all relevant standards, it may not be used by end users (and hence not solve its’ intended purpose) if it is too slow. Performance must be at an acceptable level before a deployment decision is made, and this must be verified.

For performance testing to be relevant, then, as said above, the testing environment needs to be representative of the production environment in data variety, freshness, volume, and access, and should have load and network performance similar to production.

### Security Testing

For reports that serve multiple audiences, acceptance testing should be conducted using appropriate accounts for each target audience (e.g., IT, administrators, users, external, etc.). This testing should ensure that only appropriate records are displayed to any group (e.g., executives see all records, sales managers see only records for their territories, salespeople see only their own sales records, etc.).

### Signoff

Each individual acceptance test should be signed-off and dated by the person who conducted the test and assigned a status.

Once all tests have a signoff, an overall ***go/no-go*** decision can be made by the business owner on whether the system is ready for deployment to the production environment.

## Production Use

### Smoke Testing

Smoke testing should be performed after deployment to the production environment to confirm the access to the report, that it works as intended, and that it is ready for use.

Smoke testing refers to light or ad-hoc testing of the major features and is often used to identify red flags or hot spots for resolution before widespread use.

> [!NOTE]
> *Smoke testing is a reference to the old adage, **“where there’s smoke there’s fire”***

### Monitoring

Testing is not ***“done”*** when a report is deployed to the production environment; rather, ongoing monitoring should regularly be conducted to confirm that the report is functioning as intended, and may include such areas as:

- Data Refresh (is the scheduled refresh happening as intended?)
- Functionality (are the inherent features functioning as intended?)
- Access (is the security properly applied for internal audience(s) and external users [if appropriate]?)

A superset or subset of these areas will apply to different situations and will be subject to organizational monitoring criteria.

Of note in all cases, though, is the credentials used for the monitoring: if the monitor is an Administrator and uses her/his account (or a service account) to monitor the workspace/semantic model/report/app, then elevated permissions may not be reflective of audience use. An account with appropriate credentials and permissions should especially be used if there are access or security restrictions for external users.

### Issue Recreation

Often manual testing will not be exhaustive, and it is also not unheard of that users will encounter issues and file bug reports. The user often is more focussed on identifying that an issue exists, rather than including a complete set of steps to recreate the issue. Also, just because an issue exists does not necessarily mean that it needs to be fixed immediately.

Having a user or team accurately and completely and document an issue is very helpful in being able to recreate the issue (e.g., account, workstation setup, browser used, etc.) will contribute to the severity, priority, and level-of-effort estimation being properly evaluated and prioritized. Addressing the issue can then be either scheduled or added to any known issues.

## Resources

*LinkedIn Posts*

The LinkedIn posts covering the design document are listed below: <br>
[1. General and Scope](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7295051537129615362-px8i) <br>
[2. Workflow, Issues, and Business Rules](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7300125349743316992-tG1U) <br>
[3. Data](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7305187426413563904-6yVG) <br>
[4. Reports](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7310232246613934082-w7iW) <br>
[5. Validation](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7310232246613934082-w7iW) *** FIX ***

*Samples*

Sample document fragments covering specific sections are available in the GitHub repo: <br>

[1, Design Document - Sample Fragment 01 - General and Scope](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2001%20-%20General%20and%20Scope%20-%20V0.1.docx) <br>
[2. Design Document - Sample Fragment 02 - Workflow, Issues, and Business Rules](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2002%20-%20Workflow%20Issues%20and%20Business%20Rules%20-%20V0.2.docx) <br>
[3. Design Document - Sample Fragment 03 - Data](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2003%20-%20Data%20-%20V0.3.docx) <br>
[4. Design Document - Sample Fragment 04 - Reports](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2004%20-%20Reports%20-%20V0.4.docx) <br>
[5a. Design Document - Sample Fragment 05 - Validation](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Fragment%2005%20-%20Validation%20-%20V0.5.docx) <br>
[5b. Design Document - Sample Validation Spresdsheet](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Design%20Document%20-%20Sample%20Validation%20Spreadsheet%20-%20V0.5.xlsx)
