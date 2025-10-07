<img width="1280" height="640" alt="106 - Image - Title - Organizational Themes" src="https://github.com/user-attachments/assets/7b8e2b4d-2b5d-4278-a014-49f6f7109a2e" />

## Organizational Themes

Microsoft recently (July 2025) added support for ***Organizational Themes*** to Power BI to, in their words, *" ... to ensure consistent branding and styling across all reports ..."* and to *"... ensure that each report accurately reflects the organization's visual identity."*

<br>

### How to make a Theme available for use in your Organization

Once a Power BI JSON theme has been developed, there is now an easy way to make this theme available to all Power BI developers in your organization. This step, however, must be performed by a Power BI administrator.

First, access the ***Admin Portal***:

<img width="467" height="589" alt="01 - Image - Organizational Themes - Admin Portal" src="https://github.com/user-attachments/assets/ccc4a660-2587-4f39-9f99-99df38834f97" />

<br><br>

Then, browse to the ***Organizational themes (preview)*** section and click on the ***Add theme*** button:

<img width="665" height="597" alt="02 - Image - Organizational Themes - Add Theme" src="https://github.com/user-attachments/assets/296f1069-5395-4dd5-8475-1d9f0f8626e9" />

The theme will be ***disabled*** when added.

<br>

Finally, ***enable*** the theme by clicking the vertical ellipsis and selecting ***Enable for theme gallery***:

<img width="975" height="587" alt="03 - Image - Organizational Themes - Enable Theme For Gallery" src="https://github.com/user-attachments/assets/48b55604-7bc0-4a46-a03f-90d675a33227" />

<br>

### How to use an Organizational Theme 

The familiar process of applying a standard theme to a Power BI file is used for organizational themes as well. Browse to the ***View*** item of the Power BI Desktop toolbar and click on the ***down arrow*** in the ***Themes*** section. There will now be a new area available entitled ***Organizational themes***; click on the desired theme to apply it to your Power BI file.

<img width="462" height="734" alt="04 - Image - Organizational Themes - Theme Gallery" src="https://github.com/user-attachments/assets/f9b6c42e-c766-4e81-bd5e-529901060791" />

<br>

### How the Thumbnail looks in the Theme Gallery

Organizational themes are displayed in the ***Theme Gallery***. The *theme name* is not visible (but is in the tooltip), but the *background colour* can be used to differentiate themes. Dark, light, green, and red example backgrounds are included in the image above.

To change the background colour of your theme, add a ***background*** line to your JSON theme file and set the HEX code of the desired colour.

``` json
{
  "name": "Test Green Background",
  "dataColors": ["#3257A8", "#37A794", "#8B3D88", "#DD6B7F", "#6B91C9", "#F5C869", "#77C4A8", "#DEA6CF"],
  "background": "#013220"
}
```

<br>

## Resources

*LinkedIn Posts*

The LinkedIn posts covering specific areas of the Power BI theme file are listed below: <br>
[101 - How do you specify Global Attributes in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7368600915009830912-wb3Z) <br>
[102 - How do you specify Bar, Column, Line, and Area Charts in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7371153792802897920-ZqnK) <br>
[103 - How do you specify Circular Charts and Cards in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7373669687638859777-KZTg) <br>
[104 - How do you specify Slicers, Tables and Matrices in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7376225981377957889-8ayy) <br>
[105 - How do you specify Other Native Visuals and Custom Visuals in a Power BI JSON Theme file?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7378735827834650624-WX5F) <br>
[106 - How do you enable and use Organizational Themes in Power BI?](https://www.linkedin.com/posts/gregphilps_powerbi-documentationmatters-dataanalytics-activity-7381300506129825793-qOkk) <br>

*Samples*

Sample theme fragments covering specific areas of the Power BI theme file are available in the GitHub repo: <br>

[901 - Power BI Theme Fragment - Base 1 - Name.json](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/901%20-%20Power%20BI%20Theme%20Fragment%20-%20Base%201%20-%20Name.json) <br>
[902 - Power BI Theme Fragment - Base 2 - Global Colours.json](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/902%20-%20Power%20BI%20Theme%20Fragment%20-%20Base%202%20-%20Global%20Colours.json) <br>
[903 - Power BI Theme Fragment - Base 3 - Global Page Attributes.json](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/903%20-%20Power%20BI%20Theme%20Fragment%20-%20Base%203%20-%20Global%20Page%20Attributes.json) <br>
[904 - Power BI Theme Fragment - Base 4 - Global Visual Attributes.json](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/904%20-%20Power%20BI%20Theme%20Fragment%20-%20Base%204%20-%20Global%20Visual%20Attributes.json) <br>
[905 - Power BI Theme Fragment - Bar and Column Charts](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/905%20-%20Power%20BI%20Theme%20Fragment%20-%20Bar%20and%20Column%20Charts.json) <br>
[906 - Power BI Theme Fragment - Line and Area Charts](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/906%20-%20Power%20BI%20Theme%20Fragment%20-%20Line%20and%20Area%20Charts.json) <br>
[907 - Power BI Theme Fragment - Circular Charts](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/907%20-%20Power%20BI%20Theme%20Fragment%20-%20Circular%20Charts.json) <br>
[908 - Power BI Theme Fragment - Cards](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/908%20-%20Power%20BI%20Theme%20Fragment%20-%20Cards.json) <br>
[909 - Power BI Theme Fragment - Slicers](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/909%20-%20Power%20BI%20Theme%20Fragment%20-%20Slicers.json) <br>
[910 - Power BI Theme Fragment - Tables and Matrices](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/910%20-%20Power%20BI%20Theme%20Fragment%20-%20Tables%20and%20Matrices.json) <br>
[911 - Power BI Theme Fragment - Other Native Visuals](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/911%20-%20Power%20BI%20Theme%20Fragment%20-%20Other.json) <br>
[912 - Power BI Theme Fragment - Custom Visuals](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Theme/912%20-%20Power%20BI%20Theme%20Fragment%20-%20Custom%20Visuals.json) <br>

*-- eof*
