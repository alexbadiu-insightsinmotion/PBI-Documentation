<img width="1920" alt="03 - Image - Title - General and Scope" src="https://github.com/user-attachments/assets/8cc575b1-04a8-4c1d-bf23-3ef29b56847d" />

**What content is in a Design Document?**

Many see documentation as an impediment to agile and iterative development, serving only to slow down the project. This could not be farther from the truth: documentation will actually accelerate development! Not only will documentation help prevent scope creep and reduce expectation gaps, but with a well-defined project and a single source of truth for features, behaviour, performance, audiences, security, design decisions, and validation criteria, everyone benefits.

There are likely others who don't share this opinion, but **Alex Badiu** and I feel the effort spent on Power BI documentation is well worth the effort, and as it's the subject of this series, we'll continue.

Before starting, ensure all stakeholders can easily reference the design document:
- Use a single document
- Use a common format (e.g., Microsoft Word, etc.) to ensure the content can be easily read
- Use a common location (e.g., SharePoint, etc.) to ensure the content can be easily found/accessed

The design document is not just of use during development (i.e., a "one-and-done"), but it is a living, breathing document. Update the content as necesssary to reflect the reports’ state over time as it is used in production. (The design document can also be a valuable resource for those on future projects.)

**Summary**

The content in a design document can itself be grouped into many major sections, including:
- General (identification, version history, acronyms/abbreviations/definitions, table of contents, introduction)
- Scope (included, excluded, deferred)
- Issues (resolved, deferred/known)
- Business rules (calculations, filters, performance, audiences, security)
- Data sources (filters, refresh frequencies, aggregations, credentials, environments [e.g., DEV, TEST, PROD], workflow, gateways, endorsement)
- Common report items (navigation, colours, fonts, images, theme, header, footer, shadow, etc.)
- Specific report items (pages, visuals, slicers, tooltips)
- Validation (design criteria, acceptance testing criteria, test results)
- Deployment (responsible group/persons, procedure, smoke testing)
- Model (tables, relationships, measures)

The first two sections are included below, and the remaining sections will be covered in subsequent issues.

## General

There are several general items, including:

**Identification**

It is important (for any documentation, not just that for Power BI) that users always know exactly what they're looking at. So, although it goes without saying, I'm going to say it anyway:
- Include a title page with document title, author, version, and version date
- Include a page header on every page with document title
- Include a page footer on every page with version, page number, and number of pages

It is not uncommon for users to screenshot or export (to, say, PDF) a page to share with others.  Having identification information on each page permits easy assessment of whether the content is "up-to-date".

**Version History**

Each iteration of the design document should have an incrementing version number and version date. Version numbering allows enhanced communication by ensuring all participants are using the correct reference.

The version number should also be referenced in every feature or testing note to enable an appropriate comparison.

**Terminology**

Another common hindrance to communication on a Power BI project is a difference of opinion on what various terms mean, so it is beneficial to include a table of acronyms, abbreviations, and definitions that all stakeholders can reference during all stages of the project (e.g., requirements gathering, development, acceptance testing, deployment, etc.). Be sure to include all corporate and technical descriptions (even those commonly used in the business environment) so that all levels of stakeholders have the same understanding.

**Table of Contents**

A table of contents can speed navigation within the design document when the pane is turned on.

<img width="1119" alt="03 - Image - Navigation Pane" src="https://github.com/user-attachments/assets/fb20d524-5a03-492f-b151-5cde892a869c" />

**Introduction**

Include a general introduction to the project and include major features, filters, audiences, and performance requirements.

Here's an example:

*The project will produce 4 Power BI reports to monitor the invoicing process. Data will be extracted automatically from the corporate invoicing system and posted automatically to a dedicated document management system folder on a daily basis. The Power BI Service will automatically refresh the report data on a daily basis.*

*The initial release of the reports will be English-only, and French and additional languages will be added in future releases. Only those invoices dated in the current and past fiscal years will be included. The reports will be accessible to internal corporate users only.*

## Scope

The scope of a Power BI project is composed not only of the reports that will be developed and the specific features they will include, but also what items will be excluded and what items will be deferred to future releases.

**Reports**

Assign an ID and (short) name to each report in the project along with high-level description, audience, and security notes for each.

Here's an example:

| *ID* | *Name* | *Description* | *Audience/Security* |
|--|--|--|--|
| *AR01* | *All Invoices* | *A listing of all invoices (historical, current, upcoming)* | *A=Executives, Department Managers / S=Es can see all invoices / S=DMs can see only their own invoices* |
| *AR02* | *Historical Invoices* | *A listing of all historical (paid) invoices* | *A=DMs / S=DMs can see only their own invoices* |
| *AR03* | *Current Invoices* | *A listing of all current (issued & unpaid) invoices including aging* | *A=DMs / S=DMs can see only their own invoices* |
| *AR04* | *Upcoming Invoices* | *A listing of all upcoming (in progress, scheduled) invoices* | *A=DMs / S=DMs can see only their own invoices* |

**Included**

Assign an ID and provide a high-level description and reason for each item that will be included in the project scope.

Here's an example:

| *ID* | *Included Scope Item* | *Description* |
|--|--|--|
| *SI-1* | *Language - English Only* | *Due to a tight time-frame to develop the reports, the initial release will be hard-coded with English labels and data only* |
		
**Excluded**

Assign an ID and provide a high-level description and reason for each item that will be excluded from the project scope.

Here's an example:

| *ID* | *Excluded Scope Item* | *Description* |
|--|--|--|
| *SE-1* | *Language - Add French* | *A future release of the reports will contain translated labels and data and all hard-coded English labels and data will be updated with calculations to present the selected language* |
	

**Deferred**

Assign an ID and provide a high-level description and reason for each item in the project scope that will be deferred until a future release (iteration, version).

Here's an example:

| *ID* | *Deferred Scope Item* | *Description/Reason/Version* |
|--|--|--|
| *SD-1* | *Language - Add multiple languages* | *D=A future release of the reports will contain translated labels and data for multiple languages. In addition to the already-provided English and French data, translations for Spanish, German, Italian, and Portuguese will be added, and all label and data calculations will be adjusted accordingly. R=Corporate translation policies are currently under review and the level of effort cannot be properly scoped and planned at this time. V=2.x* |
	

## Sample

A sample document fragment covering these sections is available at:

<<< INSERT WORD FRAGMENT LINK >>>

#PowerBI, #DocumentationMatters, #DataAnalytics
