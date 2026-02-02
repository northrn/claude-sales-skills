---
name: discovery-questions
description: Generate tailored discovery questions based on prospect's role, industry, company stage, and likely pain points. Includes follow-up questions and what to listen for.
triggers: discovery questions, what should I ask, questions for, discovery call, sales questions
requires_mcp: exa
context: fork
---

# Discovery Questions Skill

Generate tailored discovery questions that uncover real pain, establish urgency, and qualify opportunities. Questions are customized by role, industry, company stage, and deal context.

## What This Skill Produces

1. **Opening Questions** - Build rapport and set the agenda
2. **Situation Questions** - Understand current state
3. **Problem Questions** - Uncover pain points
4. **Implication Questions** - Quantify impact and create urgency
5. **Need-Payoff Questions** - Get them to articulate value
6. **Qualification Questions** - Assess fit and buying process
7. **Follow-Up Prompts** - What to ask based on their answers
8. **Red Flags to Listen For** - Signals this might not close

## Workflow

### Step 1: Gather Context

Get from user:

1. **Prospect's role/title** - Who are you talking to?
2. **Company name** - Optional, for research
3. **Industry** - What space are they in?
4. **What you sell** - Brief description
5. **Call type** - First call? Follow-up? Demo?
6. **Anything you already know** - Prior conversations, triggers

### Step 2: Research Context (if company provided)

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- type: "deep"
- category: "company"
- query: "[Company Name]"
- numResults: 5
- enableSummary: true
- subpages: 2
- subpageTarget: ["about", "careers", "news"]

Also search category "news" for recent triggers.

Extract:
- Company size and stage
- Recent news or changes
- Tech stack (if relevant)
- Public challenges or initiatives
```

### Step 3: Identify Question Framework

Use **SPIN Selling** framework adapted for context:

```
S - Situation: Understand their current state
P - Problem: Uncover pain and challenges
I - Implication: Quantify the impact
N - Need-Payoff: Get them to articulate the value
```

Plus:
- **Qualification**: Assess fit, timeline, budget, authority
- **Competition**: Understand alternatives they're considering

### Step 4: Generate Role-Based Questions

**For Executives (C-Suite, VP):**

Focus on: Strategy, metrics, business impact, risk

```
Situation:
- "What are your top 3 priorities for this year?"
- "How does [area] fit into your overall strategy?"
- "What metrics are you personally measured on?"

Problem:
- "What's the biggest obstacle to hitting those goals?"
- "Where are you losing sleep right now?"
- "What would need to change for next year to be better than this year?"

Implication:
- "If you don't solve [problem], what happens to [goal]?"
- "What's this costing you—in time, money, or opportunity?"
- "How is this affecting other parts of the business?"

Need-Payoff:
- "If you could solve [problem], what would that mean for [goal]?"
- "What would success look like 12 months from now?"
```

**For Directors/Managers:**

Focus on: Team performance, process, tools, proving ROI

```
Situation:
- "Walk me through how your team currently handles [process]."
- "What tools are you using today?"
- "How many people are involved in [process]?"

Problem:
- "What's not working well with the current approach?"
- "Where do things break down or slow down?"
- "What do you wish your team could do that they can't today?"

Implication:
- "How much time does your team spend on [problem]?"
- "What happens when [problem] occurs?"
- "How does this affect your ability to hit your numbers?"

Need-Payoff:
- "If your team could [solve problem], what would that free them up to do?"
- "How would your leadership view you if you fixed this?"
```

**For Individual Contributors/End Users:**

Focus on: Day-to-day workflow, frustrations, wishes

```
Situation:
- "Walk me through a typical day/week for you."
- "What tools do you spend the most time in?"
- "What does your workflow look like for [process]?"

Problem:
- "What's the most frustrating part of your job?"
- "Where do you feel like you're wasting time?"
- "What do you wish was easier?"

Implication:
- "How often does [problem] come up?"
- "What do you have to do when that happens?"
- "How does that affect your ability to [goal]?"

Need-Payoff:
- "If [problem] went away, what would you do with that time?"
- "What would make your job significantly better?"
```

### Step 5: Generate Industry-Specific Questions

Spawn Task agent if needed:

```
Use mcp__exa__web_search_advanced_exa with:
- query: "[Industry] challenges trends 2025"
- numResults: 10
- enableSummary: true

Identify:
- Top 3-5 industry challenges
- Regulatory or compliance concerns
- Technology trends
- Competitive pressures
```

**Industry Question Templates:**

Healthcare:
- "How are you handling [regulatory requirement]?"
- "What's your approach to [industry trend - e.g., value-based care]?"
- "How do staffing challenges affect [area]?"

SaaS/Tech:
- "How are you thinking about [PLG/expansion revenue/churn]?"
- "What's your tech stack look like for [area]?"
- "How do you measure [key SaaS metric]?"

Financial Services:
- "How are you balancing [compliance] with [customer experience]?"
- "What's your approach to [industry trend]?"
- "How are you thinking about [regulatory change]?"

Manufacturing:
- "How are supply chain challenges affecting you?"
- "What's your approach to [automation/efficiency]?"
- "How do you handle [quality/compliance]?"

### Step 6: Generate Qualification Questions

**BANT+ Framework:**

```
Budget:
- "Do you have budget allocated for solving this?"
- "What's the investment range you're considering?"
- "How do projects like this typically get funded?"

Authority:
- "Who else would be involved in this decision?"
- "Walk me through your typical evaluation process."
- "Who would need to sign off on this?"

Need:
- "On a scale of 1-10, how urgent is solving this?"
- "What happens if you don't solve this in the next [timeframe]?"
- "Is this a 'nice to have' or a 'must have'?"

Timeline:
- "When are you hoping to have a solution in place?"
- "What's driving that timeline?"
- "What would need to happen to move faster/slower?"

Competition:
- "What else are you evaluating?"
- "What would make you choose [competitor] over us?"
- "Have you tried solving this internally?"
```

### Step 7: Generate Follow-Up Prompts

For each question category, provide follow-up guidance:

```
When they say [common answer], ask:
- "[Follow-up question]"
- "[Dig deeper question]"

Listen for:
- [Signal of strong pain]
- [Red flag]
```

**Example Follow-Ups:**

If they mention a problem:
- "Tell me more about that."
- "How long has that been going on?"
- "What have you tried so far?"
- "What happened?"

If they're vague:
- "Can you give me a specific example?"
- "Walk me through the last time that happened."
- "What did that look like in practice?"

If they mention a competitor:
- "What do you like about them?"
- "What concerns do you have?"
- "How are you thinking about the decision?"

### Step 8: Identify Red Flags

Generate deal red flags to listen for:

```
Timeline Red Flags:
- "No rush" / "Sometime next year" → Low urgency
- "Just researching" → Not ready to buy

Authority Red Flags:
- "I'll have to check with..." → Not the decision maker
- "My boss asked me to look into this" → Champion, not buyer

Budget Red Flags:
- "We don't have budget" → May be real or smokescreen
- "Can you send pricing first?" → Price shopping

Need Red Flags:
- "Everything is working fine" → No pain
- "We're just curious" → No real need

Competition Red Flags:
- "We're already pretty far along with [competitor]" → Late to the deal
- "We have an internal solution" → Build vs. buy
```

### Step 9: Create Call Structure

Provide recommended call flow:

```
## Suggested Call Flow (30 minutes)

### Opening (3 min)
- Thank them for time
- Confirm time available
- Set agenda and ask permission

### Situation (5 min)
- 2-3 situation questions
- Understand current state

### Problem Discovery (10 min)
- 3-4 problem questions
- Dig into pain with follow-ups

### Implication (5 min)
- Quantify the impact
- Create urgency

### Qualification (5 min)
- Timeline, process, stakeholders

### Next Steps (2 min)
- Summarize what you heard
- Propose clear next step
- Confirm calendar
```

### Step 10: Generate Output

Create markdown file: `discovery-questions-[context].md`

## Output Format

```markdown
# Discovery Questions: [Role] at [Industry/Company]

**Call Type:** [First call/Follow-up/etc.]
**Your Solution:** [What you sell]
**Generated:** [Date]

---

## Pre-Call Context

**What we know:**
- [Any known info about company/prospect]

**Likely pain points:**
- [Inferred pain 1]
- [Inferred pain 2]

**Recent triggers:**
- [News or events to reference]

---

## Opening (Set the Stage)

> "Thanks for taking the time today. I've set aside [X] minutes—does that still work for you?"

> "Before we dive in, I'd love to understand what prompted you to take this call / what you're hoping to get out of our conversation?"

> "Would it be helpful if I shared a bit about what we do, or would you prefer I just ask questions and learn about your situation first?"

---

## Situation Questions (Understand Current State)

1. **"[Question]"**
   - *Why ask:* [What you're trying to learn]
   - *Listen for:* [Key signals]

2. **"[Question]"**
   - *Why ask:* [What you're trying to learn]
   - *Listen for:* [Key signals]

3. **"[Question]"**
   - *Why ask:* [What you're trying to learn]

---

## Problem Questions (Uncover Pain)

1. **"[Question]"**
   - *Why ask:* [What you're trying to learn]
   - *Follow-up if they say yes:* "[Follow-up]"
   - *Follow-up if they're vague:* "[Follow-up]"

2. **"[Question]"**
   - *Why ask:* [What you're trying to learn]
   - *Follow-up:* "[Follow-up]"

3. **"[Question]"**
   - *Why ask:* [What you're trying to learn]

---

## Implication Questions (Quantify Impact)

1. **"[Question]"**
   - *Goal:* Get them to quantify the cost
   - *Listen for:* Numbers, time, risk

2. **"[Question]"**
   - *Goal:* Connect to business impact
   - *Listen for:* Strategic implications

3. **"[Question]"**
   - *Goal:* Create urgency
   - *Listen for:* Timeline pressure

---

## Need-Payoff Questions (Articulate Value)

1. **"[Question]"**
   - *Goal:* Get them to describe the ideal state

2. **"[Question]"**
   - *Goal:* Connect solution to their goals

---

## Qualification Questions

### Budget
- "[Question]"
- *Listen for:* [Signals]

### Authority
- "[Question]"
- *Listen for:* [Signals]

### Timeline
- "[Question]"
- *Listen for:* [Signals]

### Competition
- "[Question]"
- *Listen for:* [Signals]

---

## Industry-Specific Questions

Based on [industry], also consider:

1. **"[Industry question]"**
2. **"[Industry question]"**

---

## Follow-Up Prompts

**When they mention a problem:**
- "Tell me more about that."
- "How long has that been going on?"
- "What have you tried so far?"

**When they're vague:**
- "Can you give me a specific example?"
- "Walk me through the last time that happened."

**When they mention competition:**
- "What do you like about them?"
- "What concerns do you have?"

**To dig deeper on anything:**
- "Why is that?"
- "What do you mean by that?"
- "Help me understand..."

---

## Red Flags to Watch For

| Red Flag | What They Say | What It Means | How to Respond |
|----------|---------------|---------------|----------------|
| Low urgency | "No rush" | Not a priority | Probe for trigger event |
| Not decision maker | "I'll check with..." | Need to find power | Ask to involve them |
| No budget | "We don't have budget" | May be real | Understand their process |
| No pain | "Things are fine" | No compelling reason | Dig for latent pain |

---

## Recommended Call Structure

| Phase | Time | Focus |
|-------|------|-------|
| Opening | 3 min | Rapport, agenda, permission |
| Situation | 5 min | Current state |
| Problem | 10 min | Pain discovery |
| Implication | 5 min | Quantify impact |
| Qualification | 5 min | Process, stakeholders |
| Next Steps | 2 min | Clear action |

---

## Closing Strong

> "Based on what you've shared, it sounds like [summarize pain]. Is that accurate?"

> "What would be most helpful as a next step?"

> "If I could show you how we've helped [similar company] solve [similar problem], would that be valuable?"

---

*Questions generated by Claude — customize based on conversation flow*
```

## Dynamic Tuning

- User provides company name → Research and customize questions
- User says "first call" → More situation/problem questions
- User says "follow-up" → More implication/qualification questions
- User says "executive" → Strategic questions, less tactical
- User says "technical" → Feature/integration questions

## Models

- **haiku**: Research, industry trends
- **sonnet/opus**: Question generation, follow-up prompts
