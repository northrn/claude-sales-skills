---
name: proposal-writer
description: Generate professional sales proposals from call notes, meeting summaries, or deal context. Creates scope, pricing, timeline, and case studies.
triggers: write proposal, create proposal, proposal for, generate proposal, draft proposal
requires_mcp: exa
context: fork
---

# Proposal Writer Skill

Generate professional, customized sales proposals that win deals. Takes call notes, deal context, or meeting summaries and produces a complete proposal document.

## What This Skill Produces

1. **Executive Summary** - Personalized overview connecting their pain to your solution
2. **Understanding of Needs** - Demonstrates you listened and understand their situation
3. **Proposed Solution** - What you're offering, mapped to their requirements
4. **Scope of Work** - Detailed deliverables and what's included/excluded
5. **Investment & Pricing** - Clear pricing with options if applicable
6. **Timeline & Milestones** - Implementation roadmap
7. **Case Studies** - Relevant customer proof points
8. **Terms & Next Steps** - How to move forward

## Workflow

### Step 1: Gather Context

Get from user (ask if not provided):

**Required:**
1. **Company name** - Who is this proposal for?
2. **What you're proposing** - Product/service and scope
3. **Pricing** - How much and pricing model
4. **Key contact** - Who receives this?

**Helpful (ask for or research):**
5. **Call notes or meeting summary** - What did you discuss?
6. **Their pain points** - What problems are they trying to solve?
7. **Their requirements** - Specific needs or must-haves
8. **Timeline** - When do they need this?
9. **Competition** - Who else are they evaluating?
10. **Decision process** - Who else is involved?

### Step 2: Research the Company (if needed)

If user didn't provide context, spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- type: "deep"
- category: "company"
- query: "[Company Name]"
- numResults: 5
- enableSummary: true

Extract:
- What they do
- Company size
- Industry
- Recent news
- Any public info about their challenges
```

### Step 3: Find Relevant Case Studies

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- query: "[Your Company] case study [prospect's industry]"
- numResults: 10
- enableSummary: true

Find:
- Case studies in same industry
- Case studies with similar company size
- Case studies solving similar problems
- Specific results/metrics achieved

If no direct matches, find adjacent case studies and note how to position them.
```

### Step 4: Structure the Proposal

**Standard Proposal Sections:**

```
1. Cover Page
2. Executive Summary (1 page max)
3. Understanding Your Needs
4. Proposed Solution
5. Scope of Work
6. Investment
7. Timeline
8. Why [Your Company]
9. Relevant Case Studies
10. Terms & Conditions
11. Next Steps
```

**Adapt based on deal stage:**
- Early stage → More education, lighter on specifics
- Late stage → More detail, specific pricing, clear terms
- Competitive → More differentiation, more proof points

### Step 5: Write Executive Summary

The most important page. Structure:

```
Paragraph 1: Their situation and challenge
- Reference specific pain points from calls
- Show you understand their business

Paragraph 2: The impact of not solving this
- Quantify if possible (time, money, risk)
- Create urgency without being pushy

Paragraph 3: Your solution and why it fits
- High-level what you're proposing
- Why you're uniquely suited

Paragraph 4: Expected outcomes
- Specific results they can expect
- Reference similar customer results

Paragraph 5: Investment and next steps
- High-level investment range
- Clear call to action
```

### Step 6: Write Understanding Section

Demonstrate you listened. Structure:

```
"Based on our conversations, we understand that [Company] is facing:"

1. [Challenge 1 - in their words]
   - Impact: [What this costs them]

2. [Challenge 2 - in their words]
   - Impact: [What this costs them]

3. [Challenge 3 - in their words]
   - Impact: [What this costs them]

"Your key requirements include:"
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

"Success for this project looks like:"
- [Outcome 1]
- [Outcome 2]
```

### Step 7: Write Solution Section

Map your offering to their needs:

```
For each pain point/requirement:
- Their need: [What they said]
- Our solution: [How we address it]
- The benefit: [Outcome they'll get]
```

Include:
- Product/service overview
- Key features relevant to THEM (not everything)
- How it works at high level
- Integration/implementation approach

### Step 8: Write Scope of Work

Be specific to prevent scope creep:

```
## What's Included

### Phase 1: [Name]
- Deliverable 1
- Deliverable 2
- Deliverable 3

### Phase 2: [Name]
- Deliverable 1
- Deliverable 2

### Ongoing
- What's included in ongoing relationship

## What's Not Included
- [Out of scope item 1]
- [Out of scope item 2]
- Note: These can be added as optional enhancements

## Assumptions
- [Assumption 1 - e.g., client provides X]
- [Assumption 2 - e.g., timeline assumes Y]
```

### Step 9: Write Investment Section

Clear, confident pricing:

```
## Investment

### Option A: [Name] - $X
[Description]
Includes:
- Item 1
- Item 2
Best for: [Who should choose this]

### Option B: [Name] - $Y (Recommended)
[Description]
Includes:
- Everything in Option A
- Plus: Item 3
- Plus: Item 4
Best for: [Who should choose this]

### Option C: [Name] - $Z
[Description]
Includes:
- Everything in Option B
- Plus: Item 5
Best for: [Who should choose this]

## Payment Terms
- [Payment schedule]
- [Payment methods accepted]

## What's Not Included (Available as Add-Ons)
- [Add-on 1] - $X
- [Add-on 2] - $Y
```

**Pricing Psychology:**
- Always give 3 options (anchor high)
- Mark middle option as "Recommended" or "Most Popular"
- Bundle value, don't itemize commodity items

### Step 10: Write Timeline

Visual and specific:

```
## Implementation Timeline

### Week 1-2: Kickoff & Discovery
- Kickoff meeting
- Requirements gathering
- Access provisioning

### Week 3-4: [Phase Name]
- [Activities]
- Milestone: [Deliverable]

### Week 5-6: [Phase Name]
- [Activities]
- Milestone: [Deliverable]

### Week 7+: [Ongoing/Launch]
- Go-live
- Training
- Transition to support

*Timeline assumes [start date] kickoff and [assumptions about client responsiveness]*
```

### Step 11: Write Why Us Section

Differentiation without bashing competitors:

```
## Why [Your Company]

### [Differentiator 1]
[Explanation with proof point]

### [Differentiator 2]
[Explanation with proof point]

### Our Track Record
- [Metric 1 - e.g., X customers]
- [Metric 2 - e.g., Y% retention]
- [Metric 3 - e.g., Z awards/recognition]
```

### Step 12: Add Case Studies

Include 2-3 relevant examples:

```
## Customer Success Stories

### [Company Name] - [Industry]
**Challenge:** [What they faced]
**Solution:** [What we did]
**Results:**
- [Metric 1]
- [Metric 2]
- [Metric 3]

"[Quote from customer]" — [Name, Title]
```

### Step 13: Write Terms & Next Steps

Clear path forward:

```
## Terms & Conditions

- Proposal valid for: 30 days
- Contract term: [Length]
- [Key terms - cancellation, SLA, etc.]

## Next Steps

1. Review this proposal
2. [Schedule follow-up call / Send questions]
3. Sign agreement
4. Kickoff within [X days] of signing

To proceed, [contact name] can:
- Reply to this email
- Sign electronically at [link]
- Call me at [number]
```

### Step 14: Generate Output

Create markdown file: `proposal-[company]-[date].md`

## Output Format

```markdown
# Proposal for [Company Name]

**Prepared for:** [Contact Name], [Title]
**Prepared by:** [Your Name], [Your Company]
**Date:** [Date]
**Valid until:** [Date + 30 days]

---

## Executive Summary

[4-5 paragraph executive summary]

---

## Understanding Your Needs

Based on our conversations, we understand that [Company] is facing:

### Challenge 1: [Name]
[Description]
**Impact:** [Quantified if possible]

### Challenge 2: [Name]
...

### Your Requirements
- [Requirement 1]
- [Requirement 2]

### Success Criteria
- [Outcome 1]
- [Outcome 2]

---

## Proposed Solution

### Overview
[High-level description]

### How We Address Your Needs

| Your Need | Our Solution | Your Benefit |
|-----------|--------------|--------------|
| [Need 1] | [Solution] | [Benefit] |
| [Need 2] | [Solution] | [Benefit] |

### Key Capabilities
- [Capability 1]
- [Capability 2]

---

## Scope of Work

### Phase 1: [Name]
**Timeline:** [Weeks X-Y]
**Deliverables:**
- [ ] [Deliverable 1]
- [ ] [Deliverable 2]

### Phase 2: [Name]
...

### What's Included
- [Item 1]
- [Item 2]

### What's Not Included
- [Item 1]
- [Item 2]

---

## Investment

### Option A: [Name]
**$[Amount]** [per month/one-time/etc.]

Includes:
- [Item 1]
- [Item 2]

### Option B: [Name] ⭐ Recommended
**$[Amount]**

Includes:
- Everything in Option A
- [Additional item 1]
- [Additional item 2]

### Option C: [Name]
**$[Amount]**

Includes:
- Everything in Option B
- [Additional item 1]

### Payment Terms
[Terms]

---

## Timeline

| Phase | Timeline | Milestone |
|-------|----------|-----------|
| Kickoff | Week 1 | Project plan approved |
| [Phase] | Week 2-3 | [Milestone] |
| Launch | Week X | Go-live |

---

## Why [Your Company]

### [Differentiator 1]
[Explanation]

### [Differentiator 2]
[Explanation]

### Our Track Record
- [Proof point 1]
- [Proof point 2]

---

## Customer Success Stories

### [Customer 1]
**Industry:** [Industry]
**Challenge:** [Brief challenge]
**Results:** [Key metrics]

### [Customer 2]
...

---

## Terms & Next Steps

### Terms
- Proposal valid for 30 days
- [Other key terms]

### Next Steps
1. Review proposal
2. Schedule follow-up call: [Calendly link or contact]
3. Sign agreement
4. Kick off [timeline]

**Ready to move forward?**
[Clear CTA with contact info]

---

*[Your Company] | [Website] | [Phone]*
```

## Dynamic Tuning

- User provides call notes → Extract pain points and requirements
- User says "quick proposal" → Executive summary + pricing only
- User says "detailed" → Full proposal with all sections
- Competitive deal → Add more differentiation and proof points
- Enterprise deal → More formal tone, add security/compliance section

## Quality Checklist

Before outputting, verify:

- [ ] Executive summary can stand alone
- [ ] Pain points are in THEIR words
- [ ] Solution maps directly to stated needs
- [ ] Pricing is clear with options
- [ ] Timeline is realistic
- [ ] Case studies are relevant
- [ ] Next steps are crystal clear
- [ ] No jargon or buzzwords
- [ ] Proofread for company name consistency

## Models

- **haiku**: Research, case study finding
- **opus**: Proposal writing, executive summary, persuasive copy
