<img width="1280" height="724" alt="219 - Image - Title - Sentiment Analysis" src="https://github.com/user-attachments/assets/7fed35b3-e5d8-42e7-88de-e8790f624fc8" />

## Sentiment Analysis

*October 5, 2026*

Deneb/Vega-Lite can be used to present survey data in a ***Sentiment Analysis*** visual. While such a visual was released publicly almost 3 years ago on the *Deneb Showcase* section of the *Enterprise DNA Support Forum* (now retired), the updated version presented here has additional features, including:
- a single Y axis moved outside visual extents
- class totals aligned with the category/class bars and beside the visuals (negative - left; positive - right; neutral - right)
- uses Power BI theme sentiment colours complete with variable shading (top ranked category in full colour; lower ranked categories shaded 25% lighter in colour)
- 2 tooltips: a ***custom tooltip*** card with multiple fonts, sizes, and styles (negative, positive), and a Deneb/Vega-Lite/Power BI ***standard tooltip*** (neutral)

<br>

https://github.com/user-attachments/assets/beee6450-7cbd-42c6-ad81-93c2bde4a04d

<br>

> [!NOTE]
> *I'd like to give special mention and thanks to my co-contributor [Alex Badiu](linkedin.com/in/alexandru-badiu) for both the idea for and the creation of the code for the custom tooltip for the non-neutral stacked bars; his implementation gives full-control to the developer to present any tooltip s/he likes, and I'm sure will be widely utilized ... thank Alex!*

<details closed>
<summary>Here's the description of the fictitious survey data:</summary>

The fictitious survey data is modelled linking question groups to questions, which in turn is linked to both choices and responses:

<img width="863" height="708" alt="6-Data Model" src="https://github.com/user-attachments/assets/75f8b759-d8e0-4692-8c92-ef0532e9e430" />

<img width="642" height="333" alt="7-Manage Relationships" src="https://github.com/user-attachments/assets/b16785b9-c5a4-4039-8901-34cb3748ac54" />

The fictitious survey data is contained in a single 5-tab spreadsheeted; the tabs, along with all or a portion of their sample data, are presented below:

<img width="729" height="176" alt="1-Question Groups" src="https://github.com/user-attachments/assets/3f5b6933-5136-425c-a960-61eb1fc90f5a" />

<img width="504" height="552" alt="2-Questions" src="https://github.com/user-attachments/assets/2621045d-6368-44d9-babe-08c6d75017be" />

<img width="513" height="616" alt="3-Coice Groups" src="https://github.com/user-attachments/assets/3669ffa5-5007-4710-875a-8943ce1d684f" />

<img width="506" height="811" alt="4-Choices" src="https://github.com/user-attachments/assets/4e9d9be1-2cc5-4b40-a878-a3c774f57009" />

<img width="1704" height="811" alt="5-Responses" src="https://github.com/user-attachments/assets/576d8f38-754e-43af-b2bc-5daaec310b9b" />

The [Responses] was prepared in a format that was deemed (by the author) to be a possible format an organization might use; the data was further re-shaped (unpivoted) in the Power Query Editor in Power BI to a format more consumable for visualization:

<img width="1682" height="574" alt="8-Modelled Responses" src="https://github.com/user-attachments/assets/5fd39e99-afd1-41cb-ade7-9a6e6bcd6fc3" />

</details>

This template uses the latest Deneb version (2.0.0; September 2026) and illustrates a number of Deneb/Vega-Lite features, including:

<br>

0 - General:
- a ***title*** block with:
    - a static title
    - a 2-line dynamic subtitle (via an array) and using ***direct data access*** to determine the sample size
- a standard Power BI dataset
- a shared ***transform*** block with:
    - 9x ***calculate*** transforms to assign internal names to the Power BI dataset fields
    - a ***filter*** transform to ensure there are no nulls in the dataset (likely not necessary, but included to deal with possible dataset model incompleteness)
    - a ***window/dense_rank*** transform to rank the questions within a question group
    - 2x ***window/rank*** transforms to rank the choices within each question (ascending; descending) (used subsequently to determine the bar colour shading)
    - a ***calculate*** transform to determine the choice bar colour shade percent 
    - a ***calculate*** transform to round the choice bar shade percent to 2 decimal places (not necessary, but included to enhance the display of shade percent values in the ***data pane***)
    - a ***calculate*** transform to determine the choice bar colour using the Power BI theme sentiment colours and shade percentages (calculated above) as enabled by ***Deneb***
    - a ***calculate*** transform to determine the choice bar data label colour (top ranked - white; others - #5A4A38)
    - a ***calculate*** transform to compose a composite label for the X-axis for the question ID and category
    - a ***joinaggregate/sum*** transform to determine the category totals
    - 2x ***calculate*** transforms to determine the choice percent of the category total, both as a whole number and as a decimal percent
    - a ***calculate*** transform to determine the negative class percent
    - 2x ***joinaggregate/sum*** transforms to determine the category/class responses, both as a whole number and as a decimal percent
   - a ***calculate*** transform to round the category/class responses percent to 2 decimal places
    - a ***stack*** transform to stack the choice bars within a class/category and determine the stacked starting and ending X data values
    - a ***joinaggregate/sum*** transform to determine the offset required to display both negative and positive values on the same visual
    - a ***calculate*** transform to determine the neutral class percent
    - ***joinaggregate/sum*** and ***calculate*** transforms to determine the adjustment of neutral choice bars
    - 3x ***calculate*** transforms to determine the adjusted start, end, and mid X data values for each choice bar
    - a ***calculate*** transform to update the question with the current category
    <br>--- custom tooltip positioning support ---
    - a ***window/dense_rank*** transform to determine the row index as the tooltip y band scale orders it (nominal, ascending on _category_label)
    - a ***joinaggregate/sum*** transform to determine the number of rows in the tooltip y band scale, so the card can be clamped vertically
    - 3x ***calculate*** transforms to convert the segment midpoint / end / start values from from percent space to pixels
    - 3x ***calculate*** transforms to determine the side, horizontal offset, and vertical offset for the tooltip center 
- a shared ***params*** block with:
    - 3x ***value*** parameters to set the shade percent reduction (between choices within a class), the left gutter size (for the question Y labels), and the header/legend width
    <br>--- custom tooltip geometry support ---
    - 13x ***value*** parameters and 1x ***expr*** parameter to set the custom tooltip card size and contents placement Y values
- a ***vconcat*** block for the header and the stacked bar visuals

1 - Header:
- a nested ***transform*** block with:
    - a ***calculate*** transform to determine the X value for each legend entry
    - a ***filter*** transform to restrict the dataset to only a single question record within a question group
- a ***layer*** block for the horizontal divider (rule), the legend shapes, and the legend labels

1a - Divider (Header Horizontal Rule):
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to only a single question record within a question group
- a ***rule*** mark with standard height and hard-coded width

1b - Legend Shapes:
- a ***circle*** mark with:
    - a ***scale/domain*** block using the header/legend width parameters to set the width
    - both ***zero*** and ***nice*** properties (both set to ***false***) to prevent Vega-Lite from forcing 0 into the domain and rounding it, which silently discards the shifted origin

1c - Legend Labels:
- a ***text*** mark with a maximum width limit (in pixels) (an ellipsis is added to truncated text)

2 - Stacked Bars:
- a defined ***spacing*** property to make room for the positive class/question totals
- a ***hconcat*** block for the non-neutral and neutral bar chart visuals

2a - Non-Neutral:
- a ***layer*** block for the non-neutral (negative; positive) bars, the non-neutral label, the non-neutral class label, the non-neutral single marks (zero vertical rule, negative and positive class title dividers, negative and positive class titles), custom tooltip hovered outline, card [with shadow], category and choice text marks, divider, labels, and values

2a1 - Non-Neutral Bar:
- a hard-coded ***width*** (2x the neutral width)
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to non-neutral records
- a nested ***params*** block with:
    - a ***point*** selection parameter to return the hovered question and choice with:
        - a ***resolve/global*** key:value pair to make the local parameter visible to all other marks
- a ***bar*** mark with:
    - dynamic ***corner rounding*** (only round the first and last bars)
    - a set size ***scale/domain*** block (-100 to +100) to enhance comparisons between different surveys and survey questions
    - an ***X axis*** with dynamic font size and weight (zero larger and bold)
    - a ***Y axis*** with padding to offset the labels to the left

2a2 - Non-Neutral Label:
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to non-neutral records with choice percents equal to or above 5%
- a ***text*** mark with:
    - the value formatted with a ***Power BI format string*** as enabled by Deneb
    - dynamic label colour (white if first or last value, else #5A4A38)

2a3 - Non-Neutral Class Label:
- a hard-coded ***height*** (step size = 60)
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to non-neutral records with choice rank = 1 (both ascending and descending)
- a ***text*** mark with:
    - ***dynamic alignment*** (negative = right; positive = left)
    - ***dynamic X position*** (negative = 0; positive = 800)
    - ***dynamic X offset*** (negative = -4 px; positive = +4 px)
    - a ***named style***
    - the value formatted with a ***Power BI format string*** as enabled by Deneb

2a4 - Non-Neutral Single Marks:
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to a single row only
- a ***layer*** block for the zero vertical rule, negative and positive class title dividers, negative and positive class titles 

2a4a - Non-Neutral Zero Vertical Rule:
- a ***rule*** mark with:
    - a fixed X position (0)
    - a ***named style***

2a4b - Non-Neutral Negative Sentiment Class Divider:
- a ***rule*** mark with:
    - a fixed X width (-100 to -1, to leave a small gap between adjacent the rule marks)
    - a fixed Y position (-10) 
    - a ***named style***

2a4c - Non-Neutral Positive Sentiment Class Divider:
- a ***rule*** mark with:
    - a fixed X width (1 to 100, to leave a small gap between adjacent the rule marks)
    - a fixed Y position (-10) 
    - a ***named style***

2a4d - Negative Sentiment Class Title:
- a ***text*** mark with:
    - a fixed X position (-50)
    - a fixed Y position (-24) 
    - a ***named style***

2a4e - Positive Sentiment Class Title:
- a ***text*** mark with:
    - a fixed X position (+50)
    - a fixed Y position (-24)
    - a ***named style***

2a5 - Custom Tooltip - Hover Outline:
- a nested ***transform*** block with:
    -  a ***filter*** transform to restrict the dataset to non-neutral records
    -  a ***filter*** transform to restrict the dataset to the hovered bar (question and choice, as enabled by the global ***point*** selection parameter)
- a ***bar*** mark with disabled fill (null) and dark stroke (#3D3A36)
    - *(the syntax for a named style in layered stacked bars could not be found, so inline formatting was used instead)*

2a6 - Custom Tooltip - Container:
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to non-neutral records
    - a ***calculate*** transform to determine if the current record is the one being hovered-over
    - a ***filter*** transform to restrict the dataset to only the hovered-over record
- a nested ***shared encoding*** block to ensure all layered marks use the same axes
- a ***layer*** block for the custom tooltip shadow, card, category and choice text marks, divider, labels, and values

2a6a - Custom Tooltip - Shadow:
- a ***rect*** mark with:
    - hard-coded ***fill colour*** (#3D3A36) and ***fill opacity*** (0.06)
    - no ***stroke*** (null)
    - ***rounded corners*** (8 px)
    - ***width*** and ***height*** as per the shared parameters (each increased by 4 px)
    - dynamic X and Y positions (as calculated in the ***shared transforms*** in section [0] above; Y offset by 2 px)

2a6b - Custom Tooltip - Card:
- a ***rect*** mark with:
    - ***width*** and ***height*** as per the ****shared parameters***
    - ***dynamic X and Y positions*** (as calculated in the ***shared transforms*** in section [0] above)
    - a ***named style***

2a6c - Custom Tooltip - Category:
- a ***text*** mark with:
    - ***dynamic length*** (limit set to card width - padding)
    - ***dynamic position*** (as calculated in the ***shared transforms*** in section [0] above and offset by 1/2 the card ***width*** and ***height*** parameters)
    - a ***named style***

2a6d - Custom Tooltip - Choice:
- a ***text*** mark with:
    - ***dynamic length*** (limit set to card width - padding)
    - ***dynamic position*** (as calculated in the ***shared transforms*** in section [0] above and offset by 1/2 the card ***width*** and ***height*** parameters)
    - a ***named style***

2a6e - Custom Tooltip - Divider:
- a ***rect*** mark with:
    - ***width*** as per the ***shared parameter***
    - hard-coded ***height*** (1)
    - ***dynamic position*** (as calculated in the ***shared transforms*** in section [0] above and offset by 1/2 the card ***height*** parameter)
    - a ***named style***

2a6f - Custom Tooltip - Labels:
- a ***text*** mark with:
    - ***line height*** (as calculated in the ***shared transforms*** in section [0] above)
    - ***dynamic position*** (as calculated in the ***shared transforms*** in section [0] above and offset by 1/2 the card ***width*** and ***height*** parameters)
    - a ***named style***
    - an ***array*** of 4 elements (array renders one line per element)

2a6f - Custom Tooltip - Values:
- a ***text*** mark with:
    - ***line height*** (as calculated in the ***shared transforms*** in section [0] above)
    - ***dynamic length*** (limit set to card width - padding) (to keep a long question short from running into the labels column)
    - ***dynamic position*** (as calculated in the ***shared transforms*** in section [0] above and offset by 1/2 the card ***width*** and ***height*** parameters)
    - a ***named style***
    - an ***array*** of 4 elements (array renders one line per element) (values formatted with ***Power BI format strings*** as enabled by Deneb)

2b - Neutral:
- a ***layer*** block for the neutral bars, the neutral label, the neutral class label, the neutral single marks (neutral class title divider, neutral class title)

2b1 - Neutral Bar:
- a hard-coded ***width*** (1/2x the non-neutral width)
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to neutral records
- a ***bar*** mark with:
    - a set size ***scale/domain*** block (0 to 100) to enhance comparisons between different surveys and survey questions
    - an ***X axis*** with dynamic font size and weight (zero larger and bold)
    - a ***standard Deneb tooltip*** (group, question, choice, % responses, # of responses)

2b2 - Neutral Label:
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to neutral records with choice percents equal to or above 5%
- a ***text*** mark with:
    - the value formatted with a ***Power BI format string*** as enabled by Deneb
    - static label colour (white)

2b3 - Neutral Class Label:
- a hard-coded ***height*** (step size = 60)
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to neutral records
    - a ***joinaggregate/sum*** transform to determine the neutral class percent
- a ***text*** mark with:
    - ***static alignment*** (left)
    - ***static X position*** (400)
    - ***static X offset*** (4 px)
    - a ***named style***
    - the value formatted with a ***Power BI format string*** as enabled by Deneb

2b4 - Neutral Single Marks:
- a nested ***transform*** block with:
    - a ***filter*** transform to restrict the dataset to a single row only
- a ***layer*** block for the neutral class title divider and the neutral class title

2b4a - Neutral Negative Sentiment Class Divider:
- a ***rule*** mark with:
    - a fixed X width (1 to 100)
    - a fixed Y position (-10) 
    - a ***named style***

2b4b - Neutral Sentiment Class Title:
- a ***text*** mark with:
    - a fixed X position (+50)
    - a fixed Y position (-24) 
    - a ***named style***

3 - Config:
- configuration values set for:
    - border colour ([stroke] set to transparent [null])
    - global font family (Segoe UI)
    - global bar attributes (height, stroke colour, stroke width)
    - title font attributes (family, size, weight, style, colour)
    - subtitle font attributes (family, size, weight, style, colour)
    - X axis attributes (ticks [off], domain [on; #A3A3A3], grid [on; #E3E3E3], and labels (font style, colour)
    - Y axis attributes (ticks [off], domain [off], grid [off], and labels (font size, weight, style, colour)
- named styles:
    - header divider rule (colour, stroke width)
    - legend text font (size, weight, style, colour)
    - sentiment title text font (family, size, weight, style, colour)
    - sentiment divider rule (colour, stroke width)
    - non-neutral vertical zero rule (colour)
    - question class percent text font (family, size, weight, style, colour)
    - tooltip card rectangle (colour, opacity, stroke colour, stroke width, corner radius)
    - tooltip category text font (family, size, weight, style, colour)
    - tooltip choice text font (family, size, weight, style, colour)
    - tooltip divider recctangle (colour, opacity)
    - tooltip labels text font (family, size, weight, style, colour)
    - tooltip values text font (family, size, weight, style, colour)

<hr>
 
<details closed>
<summary>Here's the template JSON code:</summary>

``` json
{
... MORE TO COME ...
}
```

</details>

<hr>

### Links:

Here's the template:

[919.1 - JSON - Deneb Template - Sentiment Analysis](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/919.1%20-%20deneb_template.sentiment_analysis.v2.0.0.json) <br> 

<br>

Here's an example Power BI file using the template:

[919.2 - PBIX - Deneb Example - Sentiment Analysis](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/919.2%20-%20Deneb%20Reuseable%20Components%20-%20Sentiment%20Analysis%20-%20v2.0.0.pbix) <br>

<br>

Hers's the fictitious sample survey data used:

[919.3 - XLSX - Sample Vehicle Survey Data - Sentiment Analysis](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/Components/Deneb/919.3%20-%20Sample%20Vehicle%20Survey%20Data.xlsx) <br>

*- eof*
