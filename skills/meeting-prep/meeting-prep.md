---
name: meeting-prep
description: Generate a pre-call research brief with company context, attendee backgrounds, suggested questions, likely objections, and talking points.
triggers: prep me for call, meeting prep, prepare for meeting, call prep, before my call with
requires_mcp: exa
context: fork
---

# Meeting Prep Skill

Generate a one-page pre-call brief to walk into any sales conversation prepared and confident.

## What This Skill Produces

1. **Company Context** - Quick snapshot relevant to the call
2. **Attendee Profiles** - Who you're meeting, their background, what they care about
3. **Recent Triggers** - News or events to reference
4. **Discovery Questions** - Tailored questions based on research
5. **Likely Objections** - What they might push back on
6. **Talking Points** - Key points to hit based on their situation
7. **Conversation Starters** - Ice breakers and rapport builders

## Tool Restriction (Critical)

ONLY use `mcp__exa__web_search_advanced_exa`. Load it via ToolSearch first.

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents with model "haiku".

## Workflow

### Step 1: Gather Meeting Context

Ask user (if not provided):

1. **Company name** - Who is the meeting with?
2. **Attendee names** - Who specifically will be on the call?
3. **Meeting type** - Discovery, demo, negotiation, check-in?
4. **Your goal** - What outcome do you want?
5. **What you sell** - Brief context on your product/service (if not obvious)

If user provides partial info (e.g., just "prep me for call with Acme"), research company first, then ask about attendees.

### Step 2: Company Quick Context

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- category: "company"
- query: "[Company Name]"
- numResults: 3
- enableSummary: true

Extract only:
- What they do (1 sentence)
- Size (employees)
- Recent funding or stage
- HQ location
```

### Step 3: Attendee Research

For each attendee, spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- category: "people"
- query: "[Attendee Name] [Company Name]"
- numResults: 5

Extract:
- First Name, Last Name
- Current title
- LinkedIn URL
- Time in role (if visible)
- Previous companies
- Education (if notable - same school = rapport)
- Content they've created (posts, podcasts, talks)
- Anything personal/hobby-related (for rapport)
```

### Step 4: Recent News Check

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- category: "news"
- query: "[Company Name]"
- numResults: 5
- startPublishedDate: 30 days ago

Find:
- Anything announced in last 30 days
- Press mentions
- Product updates
- Hiring announcements

Return only items worth mentioning in conversation.
```

### Step 5: Generate Discovery Questions

Based on research, generate tailored questions:

**By Role:**
- Executive → Strategic questions about vision, priorities, metrics
- VP/Director → Operational questions about team, process, challenges
- Manager → Tactical questions about day-to-day, tools, pain points
- IC → User questions about workflow, frustrations, wishes

**By Company Stage:**
- Startup → Growth plans, runway, priorities, speed of decision
- Growth → Scaling challenges, what's breaking, team structure
- Enterprise → Politics, procurement process, other stakeholders

**By Recent News:**
- Funding → "How are you thinking about deploying the new capital?"
- New hire in their dept → "How has [new person] changed priorities?"
- Product launch → "How has the launch gone? What's the focus now?"

Generate 5-7 questions, ranked by importance.

### Step 6: Anticipate Objections

Based on company profile, predict likely objections:

**By Company Stage:**
- Startup → "We don't have budget" / "Not a priority right now"
- Growth → "We're building this internally" / "Too busy to implement"
- Enterprise → "Need to involve procurement" / "Long evaluation process"

**By Role:**
- Executive → "Prove the ROI" / "Why now?"
- Technical → "Security concerns" / "Integration complexity"
- End user → "Change management" / "Learning curve"

For each objection, provide:
- The objection
- Why they might say it
- How to respond
- Proof point or question to ask

### Step 7: Create Talking Points

Based on their situation, identify 3-4 key talking points:

```
Each talking point should:
- Connect to something from research
- Address a likely pain point
- Lead to your value proposition
- Include a customer proof point if possible
```

### Step 8: Rapport Builders

Find personal connection opportunities:

- Shared connections (LinkedIn)
- Same school or previous company
- Common interests (from social)
- Something they posted about recently
- Conference they spoke at
- Podcast they were on

### Step 9: Generate Output

Create single markdown file: `[company-name]-meeting-prep.md`

**Design for scanning** - Sales reps look at this 5 minutes before the call.

## Output Format

```markdown
# Meeting Prep: [Company Name]

**Call Date:** [If provided]
**Call Type:** [Discovery/Demo/etc.]
**Your Goal:** [Outcome you want]

---

## 30-Second Company Context

**[Company Name]** is a [what they do] with [X employees] based in [location].
[One sentence on recent news or current situation].

---

## Who You're Meeting

### [Attendee 1 Name]
**[Title]** | [Tenure] | [LinkedIn URL]

**Background:**
- Previous: [Previous company/role]
- [Notable education or credential]

**What they care about:** [Based on role]

**Rapport hook:** [Something personal to mention]

---

### [Attendee 2 Name]
...

---

## Recent News to Reference

- **[Date]:** [News item] — [How to reference it]

---

## Discovery Questions

*Start with these, adapt based on conversation flow*

1. **[Question]**
   - *Why ask:* [What you're trying to learn]

2. **[Question]**
   - *Why ask:* [What you're trying to learn]

3. **[Question]**
   ...

---

## Likely Objections

### "[Objection]"
**Why they'll say it:** [Context]
**Response:** [How to handle]
**Follow-up question:** [Question to ask]

---

## Key Talking Points

1. **[Talking Point]**
   - Connect to: [Their situation]
   - Proof point: [Customer example]

2. **[Talking Point]**
   ...

---

## Conversation Starters

- [Ice breaker based on research]
- [Personal connection if found]
- [Reference to recent news]

---

## Red Flags to Watch For

- [Warning sign that deal may not close]
- [Political concern]

---

## After the Call

- [ ] Send follow-up email within 2 hours
- [ ] Update CRM with notes
- [ ] Schedule next step

---

*Prep generated by Claude — [Timestamp]*
```

## Dynamic Tuning

- User says "quick prep" → Company context + attendee profiles only
- User says "deep prep" → Full research with objections and talking points
- User provides call type → Tailor questions and talking points to that stage
- No attendee names → Research company, suggest likely attendees by title

## Edge Cases

**Can't find attendee:**
- Try variations of name
- Search company + title
- Note: "Limited public info on [Name] - research their LinkedIn before the call"

**No recent news:**
- Note: "No major news in last 30 days"
- Fall back to older triggers if significant

**Multiple attendees (4+):**
- Prioritize by seniority
- Note decision maker vs. influencers vs. evaluators

## Models

- **haiku**: All Exa searches, profile extraction
- **sonnet/opus**: Question generation, objection handling, synthesis
