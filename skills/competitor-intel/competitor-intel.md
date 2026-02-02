---
name: competitor-intel
description: Map competitive landscape with positioning, pricing, features, weaknesses, and generate battlecards for sales conversations.
triggers: analyze competitors, competitive landscape, competitor analysis, battlecard, who competes with
requires_mcp: exa
context: fork
---

# Competitor Intel Skill

Generate comprehensive competitive intelligence including landscape mapping, feature comparison, positioning analysis, and sales battlecards.

## What This Skill Produces

1. **Competitive Landscape** - Map of all competitors by category
2. **Feature Comparison Matrix** - Side-by-side capabilities
3. **Positioning Analysis** - How each competitor positions themselves
4. **Pricing Intelligence** - Pricing models and ranges
5. **Win/Loss Insights** - Why customers choose each competitor
6. **Battlecards** - Objection handling for each competitor
7. **Landmine Questions** - Questions that expose competitor weaknesses

## Tool Restriction (Critical)

ONLY use `mcp__exa__web_search_advanced_exa`. Load it via ToolSearch first.

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents with model "haiku".

## Workflow

### Step 1: Define the Target

Get from user:

1. **Your company/product** - What are you selling?
2. **Known competitors** - Any competitors you already know about?
3. **Your key differentiators** - What makes you unique?
4. **Target market** - Who are you selling to?
5. **Focus area** - Full landscape or specific competitors?

### Step 2: Discover Competitors

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- query: "[Your product] competitors alternatives"
- numResults: 20

Also search:
- "[Your product] vs"
- "best [product category] software"
- "[Your product] alternative"
- "companies like [Your product]"
- G2/Capterra category searches

Compile complete list of competitors, categorize:
- Direct competitors (same solution, same market)
- Indirect competitors (different solution, same problem)
- Potential competitors (adjacent, could enter)
```

### Step 3: Research Each Competitor

For each key competitor (top 5-7), spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- category: "company"
- query: "[Competitor Name]"
- numResults: 10
- enableSummary: true

Extract:
- Company description
- Founded year
- Funding raised
- Employee count
- Headquarters
- Key customers (logos)
- Target market
```

### Step 4: Feature Analysis

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- query: "[Competitor] features capabilities product"
- numResults: 10

Also search:
- "[Competitor] vs [Your Product]"
- "[Competitor] review"
- "[Competitor] site:g2.com"

Extract for each competitor:
- Core features
- Unique capabilities
- Integrations
- Platform/technical specs
- What's missing (from reviews)
```

### Step 5: Pricing Research

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- query: "[Competitor] pricing cost"
- numResults: 10

Extract:
- Pricing model (per seat, usage, flat fee)
- Price points / tiers
- Enterprise pricing (if available)
- Free tier or trial
- Contract requirements
```

### Step 6: Positioning Analysis

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- query: "[Competitor] about us mission"
- numResults: 5

Also analyze:
- Their homepage headline
- How they describe themselves
- Key messaging themes
- Target persona language
- Tagline

Categorize positioning:
- Feature leader ("most powerful")
- Price leader ("most affordable")
- Ease of use ("simplest")
- Vertical specialist ("built for [industry]")
- Innovation leader ("most advanced")
- Service leader ("best support")
```

### Step 7: Gather Win/Loss Intel

Spawn Task agent:

```
Use mcp__exa__web_search_advanced_exa with:
- query: "[Competitor] review pros cons"
- numResults: 15

Search:
- G2 reviews
- Capterra reviews
- Reddit discussions
- Twitter complaints
- Trustpilot

Extract:
- Common praise (why people choose them)
- Common complaints (weaknesses)
- Who loves them (persona/use case)
- Who struggles (bad fit scenarios)
```

### Step 8: Find Landmines

Based on research, identify weaknesses to expose:

```
For each competitor, find:
- Features they lack
- Use cases they can't handle
- Scalability issues
- Support complaints
- Integration gaps
- Pricing pain points

Turn into questions:
"How important is [feature they lack] to your workflow?"
"Have you thought about what happens when you [scenario they can't handle]?"
```

### Step 9: Generate Battlecards

For each key competitor, create battlecard:

```
## [Competitor] Battlecard

**When you hear:** "We're also looking at [Competitor]"

**Quick response:** [2-sentence positioning]

**Their strengths:** [Be honest - builds credibility]
- [Strength 1]
- [Strength 2]

**Their weaknesses:** [Where we win]
- [Weakness 1]
- [Weakness 2]

**Landmine questions:**
1. "[Question that exposes weakness]"
2. "[Question that exposes weakness]"

**If they say [Competitor] is cheaper:**
[Response]

**If they say [Competitor] has feature X:**
[Response]

**Proof points:**
- [Customer who switched from Competitor]
- [Head-to-head win story]
```

### Step 10: Generate Output

Create markdown file: `competitive-intel-[date].md`

## Output Format

```markdown
# Competitive Intelligence Report

**Generated:** [Date]
**Your Product:** [Product Name]
**Market:** [Target Market]

---

## Executive Summary

[2-3 paragraphs summarizing competitive landscape, your position, key opportunities]

---

## Competitive Landscape Map

### Direct Competitors
| Competitor | Positioning | Target Market | Funding | Employees |
|------------|-------------|---------------|---------|-----------|
| | | | | |

### Indirect Competitors
| Competitor | What They Do | Overlap |
|------------|--------------|---------|
| | | |

### Emerging Threats
| Company | Why to Watch |
|---------|--------------|
| | |

---

## Feature Comparison Matrix

| Feature | You | Competitor A | Competitor B | Competitor C |
|---------|-----|--------------|--------------|--------------|
| [Feature 1] | ✅ | ✅ | ❌ | ⚠️ |
| [Feature 2] | ✅ | ⚠️ | ✅ | ❌ |

Legend: ✅ = Strong | ⚠️ = Partial | ❌ = Missing

---

## Pricing Comparison

| Competitor | Model | Entry Price | Mid-Tier | Enterprise |
|------------|-------|-------------|----------|------------|
| | | | | |

---

## Positioning Map

[Describe how each competitor positions - what quadrant they occupy]

---

## Battlecard: [Competitor A]

**Quick positioning:** [One line on how we beat them]

### Their Strengths (acknowledge)
- [Strength 1]
- [Strength 2]

### Their Weaknesses (exploit)
- [Weakness 1] — *Our advantage: [how we're better]*
- [Weakness 2] — *Our advantage: [how we're better]*

### Landmine Questions
1. "[Question]"
2. "[Question]"
3. "[Question]"

### Common Objections

**"[Competitor] is cheaper"**
> [Response]

**"[Competitor] has [feature]"**
> [Response]

**"We're already using [Competitor]"**
> [Response]

### Proof Points
- [Customer who switched]
- [Head-to-head win]

---

## Battlecard: [Competitor B]
[Repeat format]

---

## Win Themes (Why Customers Choose Us)

1. [Theme 1]
2. [Theme 2]
3. [Theme 3]

## Loss Themes (Why We Lose)

1. [Theme 1] — *Mitigation: [how to address]*
2. [Theme 2] — *Mitigation: [how to address]*

---

## Competitive Playbook

### Discovery Questions to Ask
[Questions that uncover competitor weaknesses]

### Objections to Preempt
[Common competitor claims to address proactively]

### Traps to Avoid
[Scenarios where competitors win - disqualify or reframe]

---

*Intel compiled by Claude — refresh recommended every 90 days*
```

## Dynamic Tuning

- User names specific competitor → Deep dive on that one
- User says "quick overview" → Landscape + summary only
- User says "battlecards only" → Skip landscape, generate cards
- User provides win/loss data → Incorporate their intelligence

## Refresh Cadence

Competitive intel gets stale. Recommend:
- Full refresh: Quarterly
- News monitoring: Weekly
- Pricing check: Monthly
- After losses: Immediate

## Models

- **haiku**: All research and data extraction
- **sonnet/opus**: Battlecard writing, positioning analysis, strategic synthesis
