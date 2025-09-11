<img width="1280" height="699" alt="200 - Image - Title - Introduction (c)" src="https://github.com/user-attachments/assets/40162ed8-bafe-48d5-98a0-8d0a827c1cad" />

### Introduction

Having access to a cache of *ready-to-use* custom visuals that offer no-formatting experience can only enhance developer productivity and increase standardization of visual appearance and behaviour. It is to that end that several Deneb templates are provided here.

Each Deneb template has been prepared with several common characteristics, including:
- use *Power BI Theme* colours
- use *Segoe UI* font
- use *Config* section for formatting extensively
- use *Named Styles* for formatting extensively
- use *Explanatory Comments* extensively to aid clarity
- use *Alternative Comments* extensively to aid customization

It is anticipated that users will use these Deneb templates as starting points, updating and customizing them to suit their desired purposes.

<br>

### How to Use

Locate the desired Deneb template file (it will have a *.json* extension), then perform the following (simplified) steps (at least, those that I commonly use) to use a Deneb template in Power BI:
1. Ensure the Deneb custom visual is available on the design workstation (if not, install from [here](https://deneb.guide/docs/getting-started#within-power-bi-desktop)) <br>
2. Create a standard (native) Power BI table and add the data as normal
3. Convert the table into a Deneb visual by selecting it and clicking the *Deneb* icon (in either the *Insert* section of the *Home* toolbar or the *Build* pane); the data will become invisible

<img width="714" alt="21 - Image - Deneb Icon in Home-Insert Toolbar" src="https://github.com/user-attachments/assets/34710c56-ad10-4724-909d-3a989d5f5cce" />
<br>
<img width="160" alt="21 - Image - Deneb Icon in Build Pane" src="https://github.com/user-attachments/assets/7c8b55b2-055a-4759-9c9e-3f068c5e2581" />

4. Click the ellipsis (3 dots) above the top-right corner of the Deneb visual and select *Edit*
5. In the *Create or import new specification* dialog under the *Create using...* section, select *Existing template*
6. Click the grey box under *Import your file*, browse to and select the Deneb template file
7. In the right side of the dialog, map you data fields to the template placeholder fields, then click the *Create* button
8. Edit the Vega-Lite JSON code as desired

Refer to the [main Deneb website](https://deneb.guide/docs/templates) for complete documentation on the use of templates.

> [!NOTE]
> *This post was prepared using the Deneb 1.8.0 release and the steps are valid at the time of writing (August 2025); the template facility (and hence, the steps) may change when Deneb v2.x is released (tentatively planned for late 2025 or early 2026).*

Using Deneb templates (especially if they have been developed/configured to use Power BI theme colours) can substantially reduce visual development time and increase consistency.

> [!NOTE]
> *For more information on the incorporation of Power BI colours (theme, divergent, sentiment, and alternative), refer to the [documentation](https://deneb.guide/docs/schemes#expression-based-access-using-pbicolor) on the Deneb website.*
