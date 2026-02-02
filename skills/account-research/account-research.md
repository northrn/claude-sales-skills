---
name: account-research
description: Deep dive research on a single company - org chart, tech stack, recent news, financials, decision makers, pain points, and outreach angles.
triggers: research company, tell me about company, account research, deep dive on, what do you know about
requires_mcp: exa
context: fork
---

# Account Research Skill

Generate a comprehensive research dossier on a single company to prepare for outreach or sales conversations.

## What This Skill Produces

1. **Company Overview** - What they do, size, funding, locations
2. **Key People** - Decision makers with LinkedIn, role context, tenure
3. **Tech Stack** - Tools and technologies they use
4. **Recent News** - Funding, hiring, product launches, exec changes
5. **Pain Points** - Likely challenges based on company stage, industry, news
6. **Outreach Angles** - Personalized hooks for cold outreach
7. **Competitive Context** - Who they compete with, how they position

## Tool Restriction (Critical)

ONLY use `mcp__exa__web_search_advanced_exa`. Load it via ToolSearch first.

## Deep Research Mode

Use Exa's advanced parameters for comprehensive research:

```
Key parameters for deep research:
- type: "deep"           # Comprehensive search (vs "fast" or "auto")
- subpages: 3-5          # Crawl subpages from main results
- subpageTarget: [...]   # Target specific pages like "about", "team", "careers"
- livecrawl: "preferred" # Get fresh data, fall back to cache
- enableSummary: true    # AI-generated summaries
- enableHighlights: true # Extract key passages
- numResults: 15-30      # More results for better coverage
```

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents with model "haiku":

- Agent runs Exa searches internally
- Agent processes results
- Agent returns only distilled insights
- Main context stays clean

## Workflow

### Step 1: Identify the Company

Extract company name from user input. If ambiguous, ask for clarification:
- "Research Stripe" → Clear
- "Research Mercury" → Ask: "Mercury the fintech or Mercury the band?"

### Step 2: Company Overview

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- type: "deep"
- category: "company"
- query: "[Company Name]"
- numResults: 10
- enableSummary: true
- enableHighlights: true
- livecrawl: "preferred"
- subpages: 3
- subpageTarget: ["about", "company", "team", "investors"]

Extract:
- Official company description
- Headquarters location
- Employee count
- Year founded
- Funding raised (if startup)
- Revenue (if available)
- Stock ticker (if public)
- Parent company (if subsidiary)
- Key investors/board members
- Mission/vision statement
```

### Step 3: Key People

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- type: "deep"
- category: "people"
- query: "[Company Name] CEO founder VP director executive"
- numResults: 25
- enableSummary: true
- livecrawl: "preferred"

Run additional queries in parallel:
- "[Company Name] leadership team"
- "[Company Name] head of marketing sales"

Find and return for each person:
- First Name
- Last Name
- Title
- LinkedIn URL
- Tenure (if visible)
- Previous company (if notable)
- Recent content they've published (for personalization)

Prioritize:
1. C-Suite (CEO, CTO, CFO, CMO, CRO)
2. VP/SVP level
3. Directors in target functions (Sales, Marketing, Ops, IT)
4. Your likely buyer personas
```

### Step 4: Tech Stack

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- type: "deep"
- query: "[Company Name] tech stack tools software"
- numResults: 15
- enableSummary: true
- enableHighlights: true
- livecrawl: "preferred"
- includeDomains: ["stackshare.io", "builtwith.com", "wappalyzer.com"]

Also run parallel searches:
- "[Company Name] careers engineering stack requirements"
- "[Company Name] integrations partners"

Extract technologies in categories:
- CRM (Salesforce, HubSpot, etc.)
- Marketing (Marketo, Mailchimp, etc.)
- Analytics (Mixpanel, Amplitude, etc.)
- Data/BI (Snowflake, Looker, etc.)
- Infrastructure (AWS, GCP, Azure)
- Communication (Slack, Teams)
- Dev tools (GitHub, Jira, etc.)
- Other relevant tools
```

### Step 5: Recent News & Triggers

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- type: "deep"
- category: "news"
- query: "[Company Name]"
- numResults: 20
- startPublishedDate: 6 months ago (YYYY-MM-DD format)
- enableSummary: true
- enableHighlights: true
- highlightsQuery: "announcement funding launch hire"
- livecrawl: "always"

Run parallel search for financial news:
- category: "financial report"
- query: "[Company Name] earnings revenue"

Categorize news by type:
- Funding rounds
- Product launches
- Executive hires/departures
- Partnerships announced
- Acquisitions
- Layoffs or restructuring
- Awards or recognition
- Expansion (new offices, markets)
- Earnings/financial updates

Return:
- Headline
- Date
- Category
- Key takeaway (why this matters for outreach)
- Source URL
```

### Step 6: Social Presence & Content

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- type: "deep"
- category: "tweet"
- query: "[Company Name] OR @[company handle]"
- numResults: 15
- livecrawl: "preferred"

Run parallel searches:
- category: "personal site"
- query: "[CEO/Founder Name] blog podcast interview"

Also search for:
- Company LinkedIn page activity
- CEO/founder thought leadership
- Recent podcast appearances
- Conference talks
- Blog posts by executives

Extract:
- Key themes they talk about
- Tone and positioning
- Recent announcements via social
- Content that can be referenced in outreach
- Personal interests of key executives
```

### Step 7: Competitive Context

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- type: "deep"
- query: "[Company Name] vs competitors alternatives comparison"
- numResults: 15
- enableSummary: true
- enableHighlights: true
- highlightsQuery: "compared to versus alternative better than"

Run parallel searches:
- "[Company Name] competitor analysis"
- "companies like [Company Name]"
- "[Company Name] alternative review"

Extract:
- Main competitors (direct and indirect)
- How they differentiate (their claimed positioning)
- Market position (leader, challenger, niche)
- Where they win vs. lose
- Pricing comparison (if available)
```

### Step 8: Synthesize Pain Points

Based on all research, infer likely pain points:

**By Company Stage:**
- Startup (< 50 employees): Scaling, process, hiring, runway
- Growth (50-500): Systems breaking, middle management, specialization
- Enterprise (500+): Coordination, innovation speed, technical debt

**By Recent News:**
- Just raised funding → Growth pressure, hiring fast, new initiatives
- Layoffs → Cost cutting, efficiency focus, doing more with less
- New executive → Change in direction, proving themselves, new initiatives
- Product launch → Go-to-market focus, competitive pressure

**By Industry:**
- Apply relevant industry-specific challenges

### Step 9: Generate Outreach Angles

Create 3-5 personalized outreach angles based on research:

```
For each angle, provide:
- Hook (the opening line referencing something specific)
- Connection to pain point
- Bridge to your solution
- Example email subject line
```

Angle types:
1. **Trigger-based** - Reference recent news/event
2. **Tech stack** - Reference tool they use that you integrate with
3. **Competitor** - Reference competitor they're likely losing to
4. **Growth stage** - Reference challenges typical at their stage
5. **Content-based** - Reference something their CEO said/wrote

### Step 10: Generate Output

Create single markdown file: `[company-name]-research.md`

## Output Format

```markdown
# [Company Name] - Account Research

**Generated:** [Date]
**Research depth:** Comprehensive

---

## Company Snapshot

| Attribute | Value |
|-----------|-------|
| Website | |
| Headquarters | |
| Employees | |
| Founded | |
| Funding | |
| Revenue | |
| Industry | |

**What they do:** [2-3 sentence description]

---

## Key People

### Executive Team

| Name | Title | LinkedIn | Notes |
|------|-------|----------|-------|
| | | | |

### Target Contacts (Your Likely Buyers)

| Name | Title | LinkedIn | Notes |
|------|-------|----------|-------|
| | | | |

---

## Tech Stack

| Category | Tools |
|----------|-------|
| CRM | |
| Marketing | |
| Analytics | |
| Infrastructure | |
| Communication | |

---

## Recent News & Triggers

### [Category]
- **[Date]:** [Headline] - [Key takeaway]
  - Source: [URL]

---

## Competitive Landscape

**Main Competitors:** [List]

**Positioning:** [How they differentiate]

**Market Position:** [Leader/Challenger/Niche]

---

## Likely Pain Points

Based on research, [Company] is likely dealing with:

1. **[Pain Point]** - [Evidence from research]
2. **[Pain Point]** - [Evidence from research]
3. **[Pain Point]** - [Evidence from research]

---

## Outreach Angles

### Angle 1: [Name]
- **Hook:** "[Opening line]"
- **Pain point:** [What this addresses]
- **Subject line:** "[Example subject]"

### Angle 2: [Name]
...

---

## Conversation Starters

Questions to ask in discovery:
1. [Question based on research]
2. [Question based on research]
3. [Question based on research]

---

## Red Flags / Considerations

- [Any concerns or things to be aware of]

---

*Research compiled by Claude*
```

## Dynamic Tuning

- User says "quick research" → Overview + key people only
- User says "deep dive" → Full research with all sections
- User says "focus on [topic]" → Emphasize that section
- Default → Comprehensive research

## Models

- **haiku**: All Exa searches, data extraction
- **sonnet/opus**: Pain point synthesis, outreach angle generation
