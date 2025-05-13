
<img width="1920" alt="Issue 14 (User Adoption)" src="https://github.com/user-attachments/assets/188fa5bf-360a-45dd-bb79-e20d6d88ea94" />

##### Table of Contents  
[Enhancing User Adoption]() <br>
	&nbsp;&nbsp;[1. Problem Diagnosis]() <br>
  	&nbsp;&nbsp;[2. How to build a Power BI report promotion strategy]() <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.1 Define what success looks like]() <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.2 Identify what end users need to know to feel confident using the report]() <br>
 	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.3 Recap]() <br>
  	&nbsp;&nbsp;[3. Experience & Onboarding options today]() <br>
   	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3.1 Intuitive Design and standardized resources]() <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3.2 Info Buttons : Help at the right time]() <br>
 	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3.3 "What’s New" notification : Improve awareness]() <br>
   	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3.4 Release Page : Share the roadmap]() <br>
   	 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3.5 Collect feedback directly in Power BI using Apps]() <br>
   	 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3.6 Teams Digest to keep users engaged]() <br>

 
# Enhancing User Adoption
<br><br>
> **“Vision without action is merely a dream. Action without vision just passes the time. Vision with action can change the world.”** — Joel A. Barker   <br><br>

You poured your heart and soul into building a Power BI report. Every visual, every metric, every color is in its place. It's beautiful. Functional. Accessible. Slick. You added the "crème de la crème" of features: dynamic menu, field parameters, highlights, dynamic titles, dynamic navigation, etc.
You spent so much time to make it pixel perfect... You step back and admire your work. You expect people to love it, to compliment you and your work, to ask for more. But what do you hear?

Silence.
No feedback. No questions. No one’s even using it.

**How is that even possible?**

## 1. Problem Diagnosis  

Let’s be honest: **a powerful report is worthless if no one opens it.**

We’ve already mentioned  in previous posts the importance of :

- Uncovering the real need
- Understanding and articulating the problem
- Mapping personas
- Involving and testing with end users
- Building with goals in mind and using a clear definition of done
- Documenting the process, the value, the expected actions

But here's the missing piece: **adoption doesn’t come automatically** after development.

It’s easy to think of the project in phases like: **planning, building, testing, deploying**. But if you’re treating documentation and onboarding as a simple “**deliverable**,” that’s where things start to fall apart. 

Documentation is not just a deliverable. It’s part of the journey. It's iterative, dynamic, alive. It evolves as the report does and acts as a true north star.

And yet, the final step, **deploying a report** isn’t just about moving it to PROD, setting up refresh schedules, or pushing through CI/CD pipelines. That’s the technical deployment.

What I’m talking about is the **real deployment**:

> The moment your report meets the users.  
> The moment adoption starts or doesn’t.  
> The moment you see if it makes the impact you expected or ends up collecting dust.
> <br>

>[!Important]
>Building a great report **is the first step**. Getting people to use it? That’s where the real success begins. That starts with smart, intentional promotion.
<br>

So how do we promote a report to end users you might ask

- **Static release notes?** Most users won’t even open them.
- **PDF guides?** Developers _might_ read them. End users? Unlikely.
- **Dev training sessions?** Valuable, but doesn't solve for user onboarding.
- **Emails?** Informative, sure. But are they effective for long-term adoption?
- **Kickoff webinars?** Great. But what about new users who join next month? Or the month after that?
- **Lunch and learn sessions?**  Ideal, but costly to organize frequently and sustain over time.

  <br>

| **Assessment Method**      | **Pros**                                               | **Cons**                                                             |
| -------------------------- | ------------------------------------------------------ | -------------------------------------------------------------------- |
| Release notes & PDF guides | Low effort to produce and distribute.                  | Very low readership and retention among end users.                   |
| Dev training sessions      | Deep technical understanding for power users.          | Doesn’t cover new arrivals; overly technical for general users.      |
| Emails                     | Reach users’ inboxes directly.                         | Quickly buried under other mail; limited impact on lasting adoption. |
| Kickoff webinars           | High initial engagement, real-time interaction.        | One-time event. requires replay or follow-up for later joiners.      |
| Lunch-and-learns           | Casual, interactive setting that encourages questions. | High organizational overhead; hard to maintain regular cadence.      |
<br><br>

>[!Important]
>Users **need support the moment they need it**, not just at project launch.
>

Without a **thoughtful onboarding experience**, here’s what you’ll likely see:

- Low adoption
- Features go unnoticed
- Support tickets pile up over "issues" that aren't even issues in the first place
- Stakeholders lose confidence
- New users are lost from day one

Ask yourself this:  
👉 _What’s your onboarding strategy for Power BI reports today?_  
👉 _Is it really working?_

If the answer to the second question is **YES** - amazing. **Share your approach in the comments**. I am sure it will be very valuable for everyone. If not, here’s a hard truth: launching a Power BI report without promoting and onboarding users will simply not have the impact you hope for.

## 2. How to build a Power BI report promotion strategy

A well-defined approach centered on **purpose, communication, and user engagement** is essential for effectively promoting your report and driving its adoption.

#### 1. Define what success looks like:

Start by identifying **how you’ll measure adoption, engagement, and business value**. 
Ask yourself:

- **💎 _How will you measure adoption and usage?_**
    - Are **active users** growing weekly, monthly, daily?
	- What **percentage of licensed users** are actively engaging with the report?
	- **How often is the report accessed per user?**
	- Are people using it on **mobile or desktop**? What does that tell you?
	- Are new users returning? Or dropping off?

>[!Note]
>Counting and only considering “active users” can be misleading (e.g., someone opening the report doesn’t mean they’re acting on insights, etc.)
>


- **❤️ _What qualitative signals can you track?_**
	- Are **users satisfied?** (Consider a quarterly or annual feedback survey)
	- How many **feature requests** or comments are you receiving?
	- Are you getting **fewer ad hoc questions**? That’s a sign of self-service success.
	- Is the report being referenced in meetings or strategic conversations?
	- Are teams asking to **build on top of your model**? That shows real self service traction.
	- Are users achieving the same analytical goals, but faster and with less support?
    
- **💥 _What tangible impact do you expect?_**
    - Are key business KPIs improving as a result of insights from the report?
	- Are decision-making cycles shorter?
	- Is there a shift in digital maturity (e.g., a shared understanding of numbers, better data governance, a single version of truth, etc.)
	- Is the report accelerating other analyses or inspiring new self-service projects?
	- Are more cross-functional teams discussing data and sharing with confidence in alignment with the security policies in your organization?
	- Are leaner, more transparent processes emerging thanks to better visibility?
	- **Are you shaping the behaviors your organization wants to encourage?**  
		For example: 
		- **Reduced exports to Excel** in favor of centralized reporting
		- Easier, **more secure sharing across departments**
		- **Breaking down data silos**
		- Better security and **access control**
		- Improved **monitoring, lineage, and trust** in data quality
	- **Is the report cost-effective?**  
	    - What is the compute cost for dataset refreshes per active user?  
	    - Does the impact and value delivered justify the infrastructure consumption?  
	    - Are you measuring the **ROI of the report**, not just its usage?
	- **Can the Power BI solution guide continuous improvement and help sunset outdated content?**  
	    - Can you identify parts of the report that are never used and safely remove them? 
	    - Traditional static reports tend to grow layer by layer (old analyses stay because no one knows if they're still needed. That is why the PowerPoint deck often exceed hundreds of slides)  
	    - Modern BI gives us the **opportunity to track usage and evolve the analysis**.  
	    - Avoid the “onion strategy” (don’t double Power BI analysis on top of the same analysis using legacy Excel reports.)  
		    - **Define a clear switchover point**: validate, keep the analysis work in parallel for a communicated and limited period of the, then retire the old.
	

>[!Important]
>**If you can’t measure it, you can’t objectively monitor it.**
>Objective metrics are essential. If you can’t measure whether criteria are met, evaluating success falls to nothing more than personal opinion.
>

>[!Tip]
>Success is not just usage. It’s **ongoing relevance and influence.**
>

>[!Warning]
>Organizational adoption often fails without formal change-management: sponsorship, training curricula, incentive structures are important topics to consider.
>


#### 2. Identify what end users need to know to feel confident using the report

Before users fully trust and adopt your report, they need clarity. They will need answers to a few fundamental questions. It is important to mention that often these questions are unspoken, but they are critical. Addressing these questions upfront reduces friction, increases confidence and leads to higher adoption

📌 Here are key questions users may ask:

- 🕒 **Is the data up to date?**
    - When was the dataset refreshed?
    - How frequently is it updated? 

>[!Tip]
>Confidence in data freshness ensures timely decisions
>

- ✅ **Is the report trustworthy and ready to use?**
    - Are there data quality checks in place?
    - Has it been tested and validated?
    - Who is responsible or accountable for the data accuracy?

>[!Tip]
>Trust in data quality lowers resistance to use
>

- 🧭 **How does this report help me?**
    - What’s the business purpose?
    - What specific decisions can it support?
    - How does it make my day-to-day work easier or more efficient?

>[!Tip]
>A clear value proposition boosts relevance and usage.
>

- 🔧 **What if I run into issues or have requests?**
	- Where can I report bugs or data issues?
	- How can I request new features or enhancements?
	- Is there a roadmap or plan for future updates?

>[!Tip]
>Knowing there’s a feedback loop builds trust and encourages engagement.
>

- 📚 **Where can I go to learn more or ask for help?**
    - Are there short training videos or tutorials available?
	- Is there a quick-start guide or walkthrough?
	- Who can I contact if I have questions?

>[!Tip]
>Quick access to help reduces frustration and dependency.
>

- 🔍 **Who owns this report and ensure its quality?**
    - Who is responsible for maintaining the report?
	- Is it being monitored regularly for performance and accuracy?

>[!Tip]
>Transparency in ownership creates accountability and user confidence.
>


>[!Tip]
>Build trust by **being transparent and user-centric.** Make this information easily accessible via an info page or integrated help panel in the report.
>


How many of these questions are answered in your current experience workflow?

If users need to hunt for answers or worse, don’t know what to ask, they’ll disengage. **Make confidence part of the experience, not an afterthought.**



---

### Recap: Are You Ready to Move to Onboarding?

Before diving into onboarding techniques, let’s take a moment to review the essentials.

✅ Have you defined what success means for your report?
<br>
✅ Are you confident your users have the clarity they need?

Use the checklists below to validate your foundation:

#### ✅ Power BI Report Success Checklist → [Under development](#power-bi-report-success-checklist)
#### ✅ Power BI User Confidence Checklist → [Under development](#power-bi-user-confidence-checklist)


---

## 2. Experience & Onboarding options today  


Let’s get something clear: onboarding isn't just a welcome email or a kickoff session. It's the **user’s journey** the first time (and every time) they open the report. It's **what they see**, **what they understand**, and **what decisions they feel empowered to make**.

>[!Warning]
>You don’t need a dedicated training platform or a long onboarding program. Start by embedding the guidance smartly into your Power BI report. 
>

Here’s how:

### 1. Intuitive Design and standardized resources

**Consistency** is what makes a report feel “easy to use” before a single number is read or chart is seen. Great experiences are **predictable**, familiar, and low-friction. That doesn’t happen by accident; it’s the result of **intentional design**.

>[!Important]
>**Jakob’s Law**: "Users spend most of their time on other websites (or apps, or tools), so they prefer your product to **work the same way as everything else they already know.**"
>

In Power BI, this means users shouldn’t have to re-learn how to navigate every time they open a new report. **Familiar layouts, intuitive interactions, and reusable design components** reduce friction and create trust.

##### Standardization of resources: Build Once, reuse everywhere

You don’t need to reinvent the wheel for every project. Create a base of design and development resources you can reuse in multiple reports

- **1. Power BI Templates (PBITs)** – structure your base layout, tables (Dates, Key Measures) and pre-load your theme
- **2. Custom Theme Files** – enforce **visual identity** and **saves time**
	 - Define default formatting for **each visual type** (e.g., bar charts, cards, tables, etc.) so you don't waste time clicking through the formatting pane every time
	- Customize font styles, gridlines, label positions, background settings, and more 
	- With **style presets** (Power BI's new feature), you can go even deeper: you can define **multiple visual variants**  within the same theme, giving developers design flexibility _without losing consistency_
- **3. Standard Backgrounds & Icons** – bring visual alignment and structure
- **4. Example Reports** – showcase how navigation, filters, and layout should behave
- **6. Documented Best Practices** 
	- UX/UI rules and semantic model patterns, clearly stated and shared
	- naming conventions: consistent naming for bookmarks, measures, pages, and visuals
	- accessibility guidelines
	- version control & CI/CD processes for clear ownership & backup

>[!Important]
>### 🧭 Vision Drives Consistency
>The secret isn’t just tools, it’s intention. Know what you want your reporting experience to feel like. Define your standards. Document them. Share them. Refine them as you grow.


>[!Important]
>**Bad developers** improvise. No consistency and every report is a one-off.<br>
>**Good developers** follow patterns, but only from memory. <br>
>**Great developers** ***document those patterns***, adapt them to context, and create systems that scale.

---

### 2. Info Buttons: Help at the right time

Don’t wait for users to ask for help. Instead, **build help into the report**.

Embed subtle but visible **info icons** (`?`, ℹ️) near key visuals, filters, or metrics. Clicking them opens a tooltip, panel, or popup with guidance.

>[!Important]
>Conduct a live usability test: have a new user narrate what they see and the questions that arise (“What does this do?” “How do I…?”).
>Wherever they miss essential context, add it in the info section. If parts of the report are already clear, leave them out and avoid explaining the obvious (e.g., “this chart maps sales by state”).

Also consider:

- Adding tooltips to navigation buttons for clear navigation.
- Displaying a summary of active filters on the lower side of the screen. This is especially important within collapsible menus.
- Implementing breadcrumbs to orient users as they navigate between levels.


Examples: <br>
✔- **Aleksandra Godlewska’s** guided walkthrough approach using the play axis visual <br>
✔- **Guy in a Cube’s** info panel trick using bookmarks and selection panes [video](https://youtu.be/yYr_SlG8bpw?si=ylJoUzc3GZmJYdVw)

[Men’s fashion | Financial results – DataVogue](https://data-vogue.com/pbi-core-visuals/mens-fashion-financial-results)

**How**? 
*Each comment is a shape whose background and font colors are driven by DAX-based conditional formatting. You can assign each shape a number to define its sequence on the play axis. When the play axis’s current value matches a shape’s number, its background and font colors appear; otherwise, both remain transparent.*
![Pasted image 20250507174507](https://github.com/user-attachments/assets/209a75f0-03e7-4ea1-8790-c0436d15a9a4)






🔁 **Best practices:**

- Use a consistent icon (e.g., a question mark in a circle, an ℹ️ info symbol, etc.)
- Always place it in the same relative location (top-right of a visual or page section)
- Keep the content short and focused

>[!Tip]
>These icons reduce confusion, lower training needs, and create a more self-service-friendly experience.
>

---

### 3. "What’s New" notification: Improve awareness

Whenever your report gets updated, you should **make it visible**.  
Place a small but noticeable **red badge or “What’s New” button** on the top right corner or navigation pane. Link it to:

- A SharePoint site
- A Power BI page
- Or a short summary of changes

🔁 **Why it works:**

- It grabs attention without interrupting
- Users learn what's changed at their own pace
- It builds a habit of checking for updates, which increases feature adoption

---

### 4. Release Page: Share the roadmap

Create a dedicated page in your Power BI report showing:

- What’s planned
- What’s new
- What’s in progress and when it should be released (next week, next month, next year?)

For inspiration, check out **Miguel Myers’s Core Visuals Vision Board**. Even better, learn how it was built. There are community-created video tutorials and additional resources to help you get started.
[Core Visuals Vision Board - Tutorials & PBIX | LinkedIn](https://www.linkedin.com/pulse/core-visuals-vision-board-tutorials-pbix-pbicorevisuals-jkwkf/)

![Pasted image 20250507180434](https://github.com/user-attachments/assets/a3071b0a-95e8-4424-b675-5ef4bf0b4d1c)


>[!Tip]
>*Bonus*: You build transparency, even before people ask for it. <br>
 _Tip:_ Reuse the same design structure across reports for a "familiarity boost."
>

---

### 5. Collect feedback directly in Power BI using Apps 

One of the most effective ways to share and promote Power BI reports is through **Power BI Apps**. 

- **Centralized access:** Users find all relevant reports in a single place, without managing multiple bookmarks.
- **Built-in feedback:** Embed forms or surveys directly into the app to solicit user input.
- **Consistent branding:** Apply colors, logo of your company to reinforce your organization’s identity.
- **Standardized experience:** Deliver the same navigation and layout to everyone, reducing confusion and speeding adoption.
- **Audience management:** Control who sees what by defining audience

Embedding feedback forms directly into your app encourages **two-way communication** and shows users their input matters. 

You can use these forms to:

- Gather user feedback on **usefulness, clarity, and pain points**
- **Quantify interest** in upcoming **training sessions** or topic deep dives
- **Assess the digital/data maturity** of your audience
- Allow users to **request new features or enhancements**
- Track and **consolidate recurring requests**
- **Review responses regularly** with stakeholders to drive meaningful updates
- **Refine report features, training materials, or onboarding guides** based on feedback

>[!Important]
> Keep your forms **short, focused, and accessible**.  
> Simplicity boosts participation. Visibility builds trust. Regular review shows you're listening.

>[!Important]
> Monitor new feedback items regularly and respond to encourage users’ to provide more feedback items
>(e.g.: “Thanks for your feedback: <item> is in progress and should become available in the 2nd half of 2025”, Thanks for you feedback: <item> has been added to the backlog and will be evaluated for inclusion in an upcoming release. Check <here> to see its’ status”, etc.)


---

### 6. Teams Digest to keep users engaged

Email overload is real and it is getting worse. Instead, use **Microsoft Teams** to notify users of important changes directly in a space where they already work.

Example:
- Announce new KPIs or visuals
- Highlight layout changes or usability improvements
- Explain filter changes or new navigation options

Teams messages offer a non-intrusive, on-demand way to share updates. Users can retrieve information when it suits them, without feeling pressured to respond or read the notification immediately. This respectful, asynchronous approach not only honors their time and focus but also helps build a more engaged user community.

>[!Warning]
> Before implementation, check the organization’s Teams conversation archive policy.

>[!Important]
>🔗 Consolidate users into a dedicated **Teams channel**. Teams messages are more likely to be seen and engaged with than traditional email notifications. A shared channel also:
>
>- Creates a history of updates and announcements
>- Encourages collaboration and discussion among users
>- Becomes a central hub for support, questions, and engagement


These embedded experiences aren’t just onboarding tricks, they’re **living documentation**. They reflect a conscious, deliberate design language. When we repeat visual patterns, reuse navigation flows, and embed **contextual guidance** where it matters, we’re documenting best practices through **experience**, not just static files. <br>

Documentation isn’t a phase or a file, **it’s a mindset**. 

But what if we took it one step further?  
What if **guides themselves evolved** into something more accessible, easy to create, smarter, adaptive and more integrated?  
**That’s where adoption becomes transformation.**

And that's where we will focus in the next article. 
**Stay tuned for part 2.**
