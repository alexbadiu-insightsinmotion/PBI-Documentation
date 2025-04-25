
<img width="1920" alt="Issue 12" src="https://github.com/user-attachments/assets/40b03ce5-3221-4291-9c9c-d5e824e74cc1" />



# Documentation: Focusing on PROBLEMS to build better Power BI solutions

Good documentation in Power BI and data analytics is not just about deliverables or end goals, it's a tool that helps teams work together and build better solutions. 
When we focus on **documenting the problem first**, everyone benefits.

## Why problem-focused documentation works

Effective documentation starts by clearly explaining the problem. This should cover:

- Business context
- User needs
- Data details
- Process and people involved
- Reasons behind decisions

For more details read all articles and sample Design Documents: "[What content is in a Design Document](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation)".


<br>
This ensures everyone understands and is aligned on the same goals and can make better decisions together.

### Example: Problem vs. Solution documentation

**Solution-focused documentation (less effective):** "Create a Power BI report with sales by region using a map visual, with drill-through to product details."

By following these instructions precisely, we’ll build a report page featuring a single map that displays sales by region or state, either as varying-sized bubbles or a filled choropleth map. Each bubble or state can be clicked to drill-through to detailed product-level information. 

<img width="925" alt="Solution First" src="https://github.com/user-attachments/assets/5f60ba32-1185-4eb8-8735-3bc8e03f3597" />





**But how helpful is this really?**

In theory, moving from an aggregated view to a detailed view is a good approach. In this specific example, the approach is not very effective as it prioritizes functionality over addressing the actual business needs and problems.

Let me explain: perhaps what users truly need is to understand which products performed better or worse than last year within each specific region. By focusing immediately on "the solution," we overlook and forget to discuss about what's essential - _**the actual user need**_. Instead of discussing, understanding better, brainstorming, proposing, and iterating ideas, we prematurely jump into the technical aspects of development.
Consider the user experience: Is it really pleasant for end users to drill down and then navigate back through EACH region just to identify if specific products are performing well or poorly? A map displaying regional sales through bubble sizes or a filled choropleth map only communicate that some regions generally have more sales than others - **information they likely already know**.

**Problem-focused documentation (more effective):** "Sales managers need to identify underperforming regions or products quickly and understand which products are affecting regional performance. They currently spend 4 hours weekly compiling this information from various sources."

Stating the questions a report is intended to answer rather than how the report will be presented gives freedom to deliver the best solution rather than work in the "tunnel" they've been provided. 
The key questions to ask are:  "What questions is the report intended to answer?" and "What's the minimum amount of data you need to answer those questions?" 

This provides much more useful information and gives us greater flexibility in design and a good basis for discussion and refinement.

For example, we can:

- Mix different granularities and create dynamic interactions directly from the first page
- Display the map alongside product sales & performance compared to KPIs
- Add other general meaningful KPIs and the desired context
- Add field parameters to show different types of analysis on the map dynamically
- Add tooltips for more context
- Include a switch toggle letting users change between the map and a stylized matrix showing product breakdown by region
- Allow end users to set their own highlight criteria and thresholds for what they consider good or bad
<br>
<br>

_An initial iteration based on problem-focused documentation_ 
<img width="925" alt="Problem First" src="https://github.com/user-attachments/assets/0cec8651-11c1-44dd-88c4-5e7d4bb296e1" />


<br>
<br>

This flexibility helps users identify what they need to know quickly, which is the ultimate goal. **Reports are solutions to problems, not showcases of technical or design skills.**

## Following Progressive Disclosure Principles

A better strategy for Power BI report design is to follow the concept of **progressive disclosure**, which serves as the **guiding thread** (“fil conducteur”) for effective storytelling.<br><br>


>[!NOTE]
>
> **Progressive disclosure** in report design is a technique where only the most essential information is shown by default, while additional details are revealed gradually, usually through interactions like clicks, hovers, or drilldowns **guided by strategic highlighting and effective use of colors.**
>
> 👉 It helps keep report clean, reduces cognitive load, and lets users explore data at their own pace **while giving them a clear path to follow.**

For progressive disclosure to work effectively, you **need to highlight information that stands out** and spark the user's curiosity to explore deeper layers of data. This brings us back to understanding the user's needs : **what problems are they trying to solve?** This gives you the guiding path for your story and allows you to use the progressive disclosure technique effectively.
<br>
<br>

## Acceptance Testing: Validating your solution

>[!NOTE]
>
> **Acceptance testing to validate results and visuals** is the process of reviewing a report to ensure that both the data calculations and the visual elements match business expectations and requirements.
>
> 👉 It confirms that KPIs are accurate, filters behave correctly, and visuals reflect the intended insights before final deployment.

<br>
<br>

To perform acceptance testing on a Power BI report and **validate results and visuals**, you should follow a structured process:

### 1. Define Acceptance Criteria

Define what "**correct**" looks like:
- KPI values match those in source systems (e.g., SAP, SQL, Salesforce, etc.)
- Visuals follow UX guidelines (e.g., no cut-off visuals, accessible colors, etc.)
- All filters behave as expected (e.g., force selection/multiple selection, impact on visuals, etc.)

### 2. Data Validation

Test whether the numbers shown are accurate:
- Cross-check key figures (e.g., Revenue, Margin, Units Sold, etc.) with source queries or Excel exports
- Develop an AutoTesting process to build unitary tests for non-regression testing
- Use DAX Query View to decompose complex metrics in more detail
- Validate totals and subtotals for visuals and check if filters/slicers affect visuals logically

*For more information read the detailed issues: 
[# Issue 6 - Validation Testing](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/06%20-%20Automated%20Testing%20in%20Power%20BI.md) &
[# Issue 11 - Validation](https://github.com/alexbadiu-insightsinmotion/PBI-Documentation/blob/main/11%20-%20What%20content%20is%20in%20a%20Design%20Document%20-%20Validation.md)


### 3. Visuals & Interactions Validation 

Check if charts, slicers, and navigation behave as intended:
- Confirm charts respond to slicers
- Ensure axis labels are visible and formatted with the same attributes (units, font, size, color) 
- Verify X axis starts at 0 unless designed with specific purpose
- Check that hover tooltips are clear, informative and well indicated
- Test that drill-through works and shows the correct context
- Confirm visuals are aligned
- Verify titles and subtitles are present, have consistent font/size, and are meaningful

**Examples:**
- Click on a bar for "Depot B" → Check if the drill-through page shows only data for Depot B
- Hover on a scatter plot point → Tooltip should show Article, Revenue, % Margin, etc.

### 4. Functional Testing 

Validate that buttons, bookmarks, and dynamic elements work properly:
- Test reset filters buttons, navigation buttons, page tooltips
- Test conditional formatting logic

**Examples:**
- Test "Reset filters" → All slicers return to default
- Click "View Detail" → Goes to transaction-level page with correct filters passed

### 5. Edge Case testing

Check extreme, null, or edge cases to ensure stability:
- What happens when you filter to a location that has no sales?
- What visibility issues occur if KPIs have very large numbers?
- What should be displayed when data is null or zero?

### 6. Documentation & Sign-Off

Keep a checklist in Excel or SharePoint List where each test case is tracked:

| Test Case        | Expected      | Actual      | Pass/Fail | Notes                 | Date                |
| ---------------- | ------------- | ----------- | --------- | --------------------- | ------------------- |
| Total Revenue Q1 | €1,234,000    | €1,234,000  | ✅         | Matches SAP           | 22nd of April, 2025 |
| Reset filters    | All default   | All default | ✅         | Working               | 22nd of April, 2025 |
| Depot C no data  | Empty visuals | Display (Blank)       | ❌         | Add "No data" message | 22nd of April, 2025 |

### 7. RACI Matrix

Make sure it is very clear who is responsible for what in terms of testing:
- **Responsible**: Who does the testing and where? (Dev/Test/Prod environment)
- **Accountable**: Who approves the test results?
- **Consulted**: Who provides input on test criteria?
- **Informed**: Who needs to know about test results?

## When clients skip the problem and jump to solutions

Sometimes clients come with ready-made solutions instead of discussing the problem first. This happens because:

- They're repeating what worked before
- They think it will save time
- They don't know what's possible with current tools

> [!IMPORTANT] 
>
> Users frequently try to impose their own solutions, such as requesting a KPI presented as the following _gauge_ indicator. Although this type of visual may lack relevance, can be confusing, and has a debatable aesthetic appeal, **the client remains the final decision-maker.**

<img width="234" alt="Gauge" src="https://github.com/user-attachments/assets/9e040981-81bb-4151-b2e4-b87abaa98a61" />


### Why is this Gauge visualization problematic?

#### 1. Contradictory visual signals

The gauge shows 125% with the needle pointing into the green section, suggesting positive performance. However, the text below clearly states "-41.1% Money Lost." These contradictory signals create confusion for the viewer who must reconcile why something appearing positive is actually representing a significant loss.

#### 2. Unclear relationship between metrics

The visualization presents multiple metrics without explaining their relationship:

- The gauge shows 125% of some measure
- The header states "PRICE COST DELTA"
- Below shows "-41.1% Money Lost"

Without clear context, users cannot understand what 125% represents or how it connects to the 41.1% loss, making the visualization ineffective as a communication tool.

#### 3. Inefficient use of report space

The gauge visual takes substantial real estate while conveying only a single data point. This space could instead show historical trends, comparisons, or additional context that would make the information more actionable and meaningful.

#### 4. Missing reference points and context

The visualization fails to establish:

- What 100% on the gauge represents as a baseline
- Whether 125% is good, acceptable, or concerning for the business
- How current performance compares to targets or previous periods

Without these reference points, the data lacks business context and meaning.

#### 5. Lacks actionable insights

The visualization doesn't guide users toward action. It fails to answer critical questions like:

- Does this performance level require immediate action?
- What factors are driving the negative price cost delta?
- Which areas should be investigated further?
- How does this compare to normal performance ranges?

An effective visualization should not just present numbers but help guide decision-making and next steps.

### Better alternatives

In these situations, it's better to clearly document the initial request by specifying the objectives and reasons for choosing a specific visual. This approach also allows you to inform the client of potential drawbacks:

1. **Risks with non-native visuals**: problems during updates, possible removal, impact on performance, or risks of conversion to paid versions
2. **Increased maintenance**: frequent adjustments required, increasing maintenance effort
3. **Performance impact**: longer loading times, especially with large datasets
4. **Expert recommendation**: Explain specific limitations of the requested visual in addressing business requirements and present a more effective alternative solution based on your expertise. (You're the expert after all)

This is where good documentation becomes valuable. **Written documentation makes people think more carefully**. When you document a client's proposed solution and clearly show its impacts on time, cost, performance, and maintenance, it opens the door to better conversations about alternatives.

**Common Mistakes by Beginner Developers:**
- Agreeing to everything
- Avoiding difficult conversations
- Not documenting risks
- Getting trapped in endless changes

The result? Poor models that are hard to fix later.

> [!TIP]
>
> Always get written approval for requirements. Without it, the line between what was agreed to and "just one more small change" quickly disappears.

> [!TIP]
>
> Revise priorities when scope is added; answer the question, “Yes, I can add this, but which of the current scope items should I defer?” to prevent project delays. 


> [!TIP]
>
> Some may view this as adding unnecessary bureaucracy to development, slowing progress and frustrating clients who want immediate results. However, taking shortcuts by simply implementing whatever is requested is shortsighted. Much like learning to walk before running, establishing clear communication and thoroughly assessing requirements creates alignment that leads to genuinely satisfied clients over the long term.

## Problem Documentation Framework

When documenting a problem, always answer these key questions:

1. **Who** is experiencing the problem? (specific roles/departments)
2. **What** specific task or decision are they struggling with? 
3. **Why** is the current process inadequate?
4. **How** are they currently solving this problem?
5. **When** do they need this information? (daily, monthly, ad-hoc)

Answering these questions provides a solid foundation for your solution design and helps prevent scope creep later in the project.

## Documentation and Design Thinking Work Together

Design thinking (focusing on users and their needs) pairs perfectly with good documentation. Both value:

- Understanding user perspectives
- Working in cycles of improvement
- Getting input from everyone involved

Both approaches ask the essential question: "**Are we solving the right problem**?"

## Documentation in agile environments

In fast-moving agile projects, documentation needs to be:

- **Standardized** - Don't re-invent the wheel. Focus on what is essential 
- **Living** - Updated frequently as new insights emerge
- **Accessible** - Stored where the whole team can easily reference it
- **Visual** - Use diagrams and charts where possible to communicate quickly
- **Valuable** - Not just a "task" to be done, but serving multiple purposes

Even in rapid development cycles, **the problem statement should remain stable** while solutions may evolve.



## Where to store your documentation for Power BI Projects

Several tools integrate well with Power BI development workflows:

- **Azure DevOps Wikis** - For comprehensive project documentation & for tracking requirements and issues
- **JIRA** - For comprehensive project documentation & for tracking requirements and issues
- **Microsoft Teams** - For collaborative documentation and discussions
- **GitHub/AzureDevops/Git** - For version control of documentation alongside code
- **Miro/Figma** - For visual documentation and user journey mapping

Each tool has strengths depending on your team's needs and existing workflows.

> [!TIP]
>The entire series aims to establish a comprehensive, standardized process, helping you prioritize what truly matters. We provide in the GitHub shared in the posts comments documentation procedures, processes, practical tips, recommendations, and code snippets to help all developers enhance their documentation practices and become better professionals.
>
## Conclusion

When documentation focuses on problems first and includes everyone's input, it leads to better solutions. It's not just about writing things down, it's about creating space for critical thinking and shared understanding.

Good documentation prevents costly rework by ensuring everyone agrees on what problem needs solving before jumping to how to solve it. Remember that the most beautiful report is worthless if it doesn't solve the right problem for your users.

By documenting problems clearly, testing solutions thoroughly, and maintaining good communication with stakeholders, you'll build Power BI solutions that truly deliver value to your organization.

> [!IMPORTANT]
>To help you dive deeper, I’ve also put together a focused cheat sheet summarizing the key ideas — feel free to explore it here. [Problem Focused Documentation Cheat-Sheet.pdf](https://github.com/user-attachments/files/19904854/Problem.Focused.Documentation.Cheat-Sheet.pdf)
>



💬 Let’s discuss:

What’s your go-to tool for Power BI documentation?
What’s the biggest challenge you’ve faced in keeping reports well-documented?
Drop your thoughts in the LinkedIn post: We’d love to keep the discussion going! LinkedIn post: [#Issue 12 - When Clients Impose Solutions](https:/linkedin.com)



