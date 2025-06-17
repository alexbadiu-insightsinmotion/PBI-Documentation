
![[Issue 17 1.png]]


## Enhancing User Adoption – Part 2: AI-powered solutions for rapid onboarding

### Intro

AI-powered content creation is changing the way we onboard and engage business users with analytics. Deliverables that once took days or weeks with a significant budget can now be delivered in a few hours and at a fraction of the cost. This speed lowers barriers to adoption, gives non-technical users confidence and makes global rollouts truly possible.

**These new technologies** bring important trade-offs: 
- auto-generated videos can feel impersonal, 
- governance frameworks may struggle to keep pace
- questions around ethics, cost control, ownership and long-term sustainability demand our attention.  

Even if you are not ready to automate every step today, experimenting with these capabilities is critical. The potential impact on adoption rates and user satisfaction is already immense today when using AI and early exploration gives us the experience to identify and manage risks before the next wave of AI driven experiences arrives.

In this blog post I will share my thoughts on practical, hands-on ways to leverage AI for rapid Power BI onboarding. I will walk through AI-generated onboarding videos, slide decks and a look ahead at what I think will come next. 

And, of course, I'll keep the topic as much as possible aligned with our ongoing documentation series. 😉

### 1. AI-generated Onboarding Videos

#### Why bother?

When it comes to attention spans, we all know nothing beats video content. It is the most effective medium with a positive impact on change management and onboarding, and also helps setting expectations and making a great and professional first impression. 
All too often, new users receive only an email and a link (so not really a guidance on where to start). Micro-tutorials in short, focused format can bridge that gap and drive adoption.

Why not produce these micro-tutorials already you might ask? The obstacle is always cost, time and responsibility. I built the Power BI report but should I also be the one to film, edit, add subtitles and translate training videos?  Plus, traditional training video projects can take weeks or cost a small fortune. With AI tools at least, you can go from a blank canvas and have tangible results within the hour.


---

#### How it works

Using **HeyGen** **AI** and **ChatGPT**, I created a two-minute onboarding video for an existing Power BI report in under a half an hour. With zero extra software installed, no licenses or retakes. Don't get me wrong, it is far from being perfect, but it’s more than enough to get users started.

Here’s my process:

1. **Extract**
    I wrote down the report’s essence in bullet points: key metrics, context, navigation tips. I then provided ChatGPT with that outline plus a screenshot of the report. Within seconds, I had a first version of a two-minute script.
    
2. **Generate  
    **HeyGen AI** turned the script into a natural-sounding voiceover and let me pick a customizable on-screen avatar.
    
3. **Integrate**  
    I layered the report screenshot behind the avatar. This process took about 15 minutes. More time and I could have added highlights, zoom ins and other, but the result was good enough for my purpose.
    
4. **Localize**
    In a real rollout, I’d run an iterative feedback cycle to fine-tune tone and accuracy of the message. I’d also use HeyGen to create multilingual versions for broader reach. That would surely bring some extra points for adoption!

*onboarding video created with AI*
![[Pasted image 20250616222529.png]]

---

#### Pros & Cons
**Speed and scale**  
AI delivers a complete onboarding video in under an hour instead of days or weeks.

**Cost efficiency**  
No actors, equipment, or studio time means dramatically lower expenses.

**Community and global reach**  
Easily share videos within the BI community and, with a language-selector button that can be easily added in a Power BI report, link directly to localized versions in the language of choice.

**Engagement and accessibility**  
Short and straight to the point videos hold attention better than flat docs. Auto-generated captions will broaden access for all users.

---

#### Watch out for

**Authenticity gap**  
AI voices and avatars can feel impersonal. Mixing in live footage for key moments can restore a human touch.

**Content drift**  
Automated scripts may miss nuances. Always get a subject-matter expert to review and validate.

**Data privacy**  
Uploading sensitive report assets to external AI platforms is risky. Strict governance and validation from your organization is needed to ensure you are doing things the right way.

**Impact on roles**  
Content creators must adapt as AI automates routine tasks and reshapes roles. We should all be ready to evolve our skills and responsibilities accordingly.

##### Responsible AI Checklist  
- Data privacy sign-off ✔  
- SME script review ✔  
- Version-control prompts ✔  
- Accessibility & caption QA ✔  
- Cost & license guardrails ✔  

#### Why it matters

By embracing AI video generation today, we lay the foundation for a more interactive, personalized and scalable adoption journey. The speed, scale, multilingual support and lower costs compared with traditional content creation methods add new arrows to our quiver, enabling initiatives we once thought impossible. 
At the same time, this shift will reshape real roles. Content teams must establish structured processes, rigorous quality checks and thorough impact analysis. Documentation is critical and acts as a safety net: capturing your prompting techniques, following best practices, testing, validating and logging each step keeps you in control and prevents an AI “jungle.” Collaboration and transparency are non-negotiable, and well-maintained documentation will form the bridge between the "old ways" and new "AI ways". Remember, it isn’t the strongest or the most intelligent who survive, but those most responsive to change. Fortunately, in this transformation, humans, not technology, remain firmly in the driver’s seat.


---

### 2. AI-generated Slide Decks

#### Why slides?

Some people prefer consuming information content looking at videos. These videos can be human or produced by AI (Ethics nod: Always disclose to end users that they’re viewing an AI avatar or content).  Others may prefer having access to documents or prefer the human contact during presentations. Slide generation AI solves two problems: it address an audience preferring qualitative and esthetical presentations and providing content to human presenters that will focus more on the quality of the content, and not on making "beautiful slides". AI can therefore improve human to human interaction.

#### How it works

1. **Feed the outline**  
    Drop your detailed prompt into GenSpark.ai (or a similar AI deck generator)
    
2. **AI designs**  
    The tool generates slide decks with layouts, icons, and placeholder charts.
    
3. **Brand polish**  
    Tweak colors, fonts, and refine the details in PowerPoint.
    
4. **Final QA**  
    Review for accuracy and tone before sharing and presenting.
    

**Up-side:** Fast, consistent, well designed.  
**Down-side:** Layouts can feel generic and not yet pixel perfect.

*Slide deck created with AI based on this blog post*
![[Pasted image 20250616223004.png]]

#### Why it matters

PowerPoint creation is notoriously time-intensive. Business teams often spend several hours per deck just on formatting and design. By automating the initial draft:

- **Focus on your story:** You spend less time wrestling with slide masters and more time crafting a compelling narrative.  
- **Boost consistency:** Every presentation should follow a corporate style, reducing endless design back-and-forth.  
- **Accelerate collaboration:** Shared AI-prompts or slide deck templates can cut review cycles so your team can iterate faster.  

For rapid Power BI onboarding, AI-generated decks mean trainers can create tailored presentations much faster and allow you to devote your energy to the insights that really matters.

### 3. What’s Next?

- **Internal AI Tooling**  
    Companies like Enterprise DNA have already started building in-house solutions powered by AI (e.g. Power Vibes) where, based on the metadata extracted, it creates a standardized documentation, and serves like an internal documentation catalog for Power BI reports. This tool is a perfect example of custom applications that can be built to solve specific problems, without needing prior coding expertise. [See LinkedIn post ](https://www.linkedin.com/posts/sammckayenterprisedna_power-vibes-is-now-ready-for-you-to-try-activity-7326772899560804352-_jS_/?rcm=ACoAAAd2rAYBtqG-2bVNWh14j0hOzgmbFYqs3hE&utm_medium=member_android&utm_source=share "Power Vibes is now ready for you to try. This is our new Power BI AI… | Sam McKay, CFA | 25 comments")).
    
- **LLM ↔️ Enterprise Data Integration**  
    By pairing an LLM (such as Anthropic’s Claude) with SharePoint or a lake house via MCP, users can ask natural-language questions against report docs, data dictionaries, or project plans and have summaries logged directly into a personal knowledge base like Obsidian. This speeds developer onboarding and increases ad-hoc analysis flexibility. [See Brian Julius & Goodly](https://youtu.be/BDU21pkZrM0?si=8McIBo5c6IanHyg3)
    
- **Interactive Walkthroughs**  
    Imagine an AI agent embedded inside a Power BI that guides each user, step by step, through your reports, adapting in real time to their clicks, filters, and selections.

- **AI Voice**
	Voice interfaces could let in the future first-time users narrate their data journey, like speaking aloud what they see and feeding recommendations later back to developers. The system might prompt end users to describe the order of on-screen elements they see, test how they perceive and understand certain KPIs (“What does this metric represent?”), or state their goal before any clicks (“How do I filter by region?”). This live, conversational feedback loop delivers an incredible experience: an always-on AI coach that feels like an expert sitting beside you, in the language of your choice.

- **Automated Review**  
    Next-gen AI may analyze your data model and auto-generate daily "summarized news" podcast with topics you care about, propose tutorial scripts and examples, propose user journeys for better UX/UI experience, propose improvements, spot on weaknesses and risks, perform tests & accuracy, send notifications to Teams with proposed solutions and perform them after validation, etc.
    
- **Translytical Feature in Fabric**
    With Fabric’s translytical new feature, Power BI can not only visualize but also trigger Python UDFs directly from the tool. The simulations built for analysis in Power BI can now be stored and shared after validation. Any data-driven actions that you can think about is now possible. AI assistants will help generate and refine Python code, making advanced analytics accessible to every data analyst.

- **Templates & Component re use**
	Future copilots will recommend and even auto-insert your organization’s proven patterns: bilingual layouts, accessibility alerts, Deneb visuals, and best-practice UDF snippets drawn from your own company's collective intelligence.

- **Governance, Documentation & Collaboration** 
	As AI capabilities multiply, a robust governance framework, clear documentation of prompts and processes, and iterative review cycles will be essential to maintain control, ensure quality, and drive sustainable adoption.


---

### The Bottom Line

## Actionable Takeaways

- **Pick a pilot**  
  Start small: choose one report or team and generate an AI-powered onboarding video or slide deck to validate value.

- **Document your process**  
  Capture prompts, tool settings, and review checklists in your governance playbook.

- **Establish guardrails**  
  Define data-privacy rules, approval workflows, and quality standards before scaling.

- **Measure adoption**  
  Track views and user satisfaction before and AI-driven content generation and use.

- **Iterate rapidly**  
  Use feedback loops both from end users and Subject Matter Experts to refine scripts, designs, and walkthroughs.

- **Scale globally**  
  Leverage AI’s multilingual capabilities to roll out consistent, on-brand experiences across regions.

---

## Conclusion

AI isn’t magic but it’s a powerful force multiplier. By embedding AI-generated videos, slide decks, and interactive agents into your Power BI onboarding, you’ll accelerate adoption, boost engagement, and break down language and geographic barriers. 
Yet, new risks and governance requirements emerge, but those are simply part of the experimentation cycle: iterate, document, and measure to keep control. 

The true payoff? You’ll not only build a more engaged audience today but also lay the groundwork for tomorrow’s fully interactive, AI-powered BI experiences where insights could be conversational, personalized, and available in any language, at any time. AI is here to stay, and when guided by clear processes and human oversight, it will redefine how we explore data and tell stories with analytics.