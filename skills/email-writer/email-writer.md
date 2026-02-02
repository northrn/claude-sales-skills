---
name: email-writer
description: Generate personalized cold emails using prospect research. Creates multiple variants for A/B testing with subject lines and follow-up sequences.
triggers: write cold email, personalize email, email to, write outreach, cold email for
requires_mcp: exa
context: fork
---

# Email Writer Skill

Generate highly personalized cold emails that reference specific details about the prospect, their company, and timely triggers.

## What This Skill Produces

1. **3 Email Variants** - Different angles for A/B testing
2. **Subject Lines** - 3-5 options per variant with predicted open rates
3. **Follow-Up Sequence** - Emails 2 and 3 for non-responders
4. **LinkedIn Touchpoints** - Connection request and follow-up messages
5. **Personalization Notes** - Why each personalization was chosen

## Tool Restriction (Critical)

ONLY use `mcp__exa__web_search_advanced_exa`. Load it via ToolSearch first.

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents with model "haiku".

## Workflow

### Step 1: Gather Context

Get from user (ask if not provided):

1. **Prospect name** - Who are you emailing?
2. **Company name** - Where do they work?
3. **What you sell** - Brief description of your product/service
4. **Your social proof** - Key customers, results, credibility
5. **CTA preference** - Call, reply, link click?
6. **Tone** - Professional, casual, provocative?

### Step 2: Research the Prospect

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- category: "people"
- query: "[Prospect Name] [Company Name]"
- numResults: 10

Find:
- Current title and tenure
- LinkedIn URL
- Previous companies/roles
- Content they've created (posts, articles, podcasts)
- Recent social activity
- Education
- Any personal interests visible
```

### Step 3: Research the Company

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- category: "company"
- query: "[Company Name]"
- numResults: 5

Find:
- What they do
- Company size
- Recent funding
- Growth signals
```

### Step 4: Find Triggers

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- category: "news"
- query: "[Company Name]"
- numResults: 10
- startPublishedDate: 60 days ago

Look for:
- Funding announcements
- Product launches
- Executive hires
- Expansion news
- Partnerships
- Press coverage

Also search:
- "[Prospect Name]" recent activity
- "[Company Name] hiring [prospect's dept]"
```

### Step 5: Identify Personalization Hooks

Rank personalization options by strength:

**Tier 1 - Strongest (use if available):**
- Something they personally wrote/said (LinkedIn post, podcast, article)
- Mutual connection
- Specific trigger event affecting their role

**Tier 2 - Strong:**
- Recent company news
- Job posting in their department
- Tech stack match
- Competitor relationship

**Tier 3 - Good:**
- Company growth/funding
- Role-based pain points
- Industry trends

**Tier 4 - Generic (avoid if possible):**
- Company description
- Their job title only

Select top 3 hooks for 3 email variants.

### Step 6: Generate Email Variants

Create 3 different emails, each using a different hook:

**Variant A: Trigger-Based**
- Lead with recent news or event
- Connect to pain point
- Bridge to solution

**Variant B: Content/Personal**
- Reference something they said/wrote
- Show you did research
- Connect to your value

**Variant C: Problem-First**
- Lead with pain point common to their role
- Agitate briefly
- Offer solution

### Step 7: Apply Email Best Practices

**Structure (PAS Framework):**
```
[Personalized hook - 1 sentence]

[Problem/Pain - 1-2 sentences]

[Solution + Proof - 1-2 sentences]

[CTA - 1 sentence]

[Signature]
```

**Rules:**
- Under 100 words (75 ideal)
- 3-4 short paragraphs max
- One clear CTA
- No attachments
- No "I hope this email finds you well"
- No "I'd love to pick your brain"
- Mobile-friendly (short lines)

**Subject Line Rules:**
- Under 50 characters
- Lowercase often outperforms
- Question or statement, not clickbait
- Personalization when natural
- No spam words (free, urgent, act now)

### Step 8: Generate Follow-Up Sequence

**Email 2 (3-4 days after Email 1):**
```
Purpose: Add value, not just "bumping this up"
- Reference Email 1 briefly
- Add NEW information (case study, stat, insight)
- Restate CTA differently
```

**Email 3 (5-7 days after Email 2):**
```
Purpose: Breakup / permission to close
- Acknowledge they're busy
- Give them an out
- One final soft CTA
- P.S. with referral ask
```

### Step 9: Generate LinkedIn Touches

**Connection Request (300 char limit):**
```
Short, specific reason for connecting
- Reference shared interest or connection
- No pitch
- Just connect
```

**LinkedIn Message (after connecting):**
```
- Thank for connecting
- One sentence of value
- Soft CTA or question
- NOT a copy of your email
```

### Step 10: Generate Output

Create markdown file: `[prospect-name]-outreach.md`

## Output Format

```markdown
# Cold Outreach: [Prospect Name] at [Company]

**Generated:** [Date]
**Prospect:** [Name], [Title]
**Company:** [Company Name]

---

## Research Summary

**About [Prospect]:**
- [Key finding 1]
- [Key finding 2]
- [Personal detail for rapport]

**About [Company]:**
- [What they do]
- [Recent news/trigger]

**Personalization hooks used:**
1. [Hook 1 - which email]
2. [Hook 2 - which email]
3. [Hook 3 - which email]

---

## Email Variant A: Trigger-Based

### Subject Lines
1. `[subject line 1]` — *Predicted open: 45%*
2. `[subject line 2]` — *Predicted open: 42%*
3. `[subject line 3]` — *Predicted open: 40%*

### Email Body

```
[Email text here]
```

**Why this works:** [Explanation of personalization strategy]

---

## Email Variant B: Content/Personal

### Subject Lines
1. `[subject line 1]`
2. `[subject line 2]`

### Email Body

```
[Email text here]
```

**Why this works:** [Explanation]

---

## Email Variant C: Problem-First

### Subject Lines
1. `[subject line 1]`
2. `[subject line 2]`

### Email Body

```
[Email text here]
```

**Why this works:** [Explanation]

---

## Follow-Up Sequence

### Email 2 (Send Day 4 if no reply)

**Subject:** `re: [original subject]`

```
[Email text]
```

---

### Email 3 (Send Day 10 if no reply)

**Subject:** `should I close your file?`

```
[Email text]
```

---

## LinkedIn Sequence

### Connection Request

```
[Request text - under 300 chars]
```

### Follow-Up Message (after they accept)

```
[Message text]
```

---

## A/B Test Recommendation

**Test first:** Variant [A/B/C] because [reason]

**If no response after full sequence:**
Wait 30 days, then try different angle with new trigger

---

*Emails generated by Claude — personalization level: high*
```

## Email Quality Checklist

Before outputting, verify each email:

- [ ] Under 100 words
- [ ] Personalization in first sentence
- [ ] Clear single CTA
- [ ] No generic opener ("Hope you're well")
- [ ] No jargon or buzzwords
- [ ] Sounds human, not templated
- [ ] Mobile-friendly (short paragraphs)
- [ ] Subject line under 50 chars

## Dynamic Tuning

- User provides trigger → Use it as primary hook
- User says "casual" → More conversational tone
- User says "executive" → Shorter, more direct
- User provides their email → Match their voice/style
- No good personalization found → Note limitation, use best available

## Models

- **haiku**: All research and data extraction
- **sonnet/opus**: Email writing, subject lines, personalization strategy
