---
name: lead-generation
description: Build targeted outreach lists with contacts, LinkedIn profiles, and trigger events. Creates ready-to-use CSV tracker and email templates.
triggers: find leads, build outreach list, lead generation, prospect list, find contacts, sales leads, outreach campaign
requires_mcp: exa
context: fork
---

# Lead Generation Skill

Build targeted B2B outreach lists with enriched contacts, trigger events, and ready-to-send email templates.

## What This Skill Produces

1. **Enriched CSV Tracker** - Companies, contacts, LinkedIn URLs, trigger events, priority scores
2. **Hot Leads Summary** - Top 10 priority contacts with custom email drafts
3. **Email Templates** - Cold email sequence using proven frameworks (PAS, BAB)
4. **README** - Quick start guide with 90-day outreach calendar

## Tool Restriction (Critical)

ONLY use `mcp__exa__web_search_advanced_exa`. Load it via ToolSearch first.

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents with model "haiku":

- Agent runs Exa searches internally
- Agent processes and deduplicates results
- Agent returns only distilled markdown tables
- Main context stays clean regardless of search volume

## Workflow

### Step 1: Gather Requirements

Ask user for:

1. **Target industry** - e.g., "healthcare", "manufacturing", "SaaS"
2. **Geography** - e.g., "Northern Ontario", "Texas", "DACH region"
3. **Company size** - e.g., "50-500 employees", "enterprise", "SMB"
4. **Target roles** - Default: Marketing, HR, Communications, Procurement
5. **Output location** - Default: `~/Documents/{industry}-outreach/`

If user provides partial info, infer sensibly and confirm.

### Step 2: Find Companies

Spawn Task agent to search for companies:

```
Use mcp__exa__web_search_advanced_exa with:
- category: "company"
- numResults: 30-50
- enableSummary: true

Run 2-3 query variations in parallel:
1. "{industry} companies {geography}"
2. "{specific subsector} {geography} organizations"
3. "{industry} {major cities in geography}"

Merge, deduplicate by domain. Return markdown table:
- Company Name
- Location (city)
- Website
- Type/Subsector
- Employee count (if available)
- Brief description
```

### Step 3: Find Contacts

Spawn Task agent for each company tier (parallelize):

```
Use mcp__exa__web_search_advanced_exa with:
- category: "people"
- numResults: 8-10 per company

Search patterns:
- "[Company Name] {target role} director manager"
- "[Company Name] marketing communications HR"

Extract and return:
- First Name (given name only)
- Last Name (family name, including suffixes like Jr., PhD, CHRP)
- Title/Role
- LinkedIn URL
- Organization
```

Target roles by priority:
1. Marketing Director/Manager
2. Communications Director/Manager
3. HR Director/Manager (for staff programs)
4. Procurement/Purchasing Manager
5. Executive Director/CEO (for smaller orgs)

### Step 4: Find Trigger Events

Spawn Task agent to search for news:

```
Use mcp__exa__web_search_advanced_exa with:
- category: "news"
- numResults: 15-20
- startPublishedDate: 6 months ago

Search for:
- "[Company names] expansion hiring funding news"
- "{industry} {geography} new facility announcement"
- "{industry} {geography} recruitment hiring 2025"

Look for trigger types:
- Expansion / new facilities
- Major funding / donations
- Executive hires
- Recruitment campaigns
- Anniversary celebrations
- Awards / recognition
- Community events

Return:
- Company name
- Trigger type
- Description
- Date
- Source URL
```

### Step 5: Score and Prioritize

Assign priority scores:

| Criteria | Score |
|----------|-------|
| Has active trigger event | +3 |
| Decision-maker title (Director+) | +2 |
| Larger organization (200+ employees) | +1 |
| Foundation/events-focused org | +2 |
| Multiple contacts found | +1 |

Priority levels:
- HOT: Score 5+
- HIGH: Score 3-4
- MEDIUM: Score 1-2
- LOW: Score 0

### Step 6: Generate Outputs

Create output folder: `~/Documents/{industry}-{geography}-outreach/`

#### File 1: outreach-tracker-enriched.csv

Columns:
```
Organization, City, Website, First Name, Last Name, Contact Title, Contact Email,
Contact LinkedIn, Tier, Status, Trigger Event, Priority Score,
Email 1 Sent, Email 1 Opened, Email 2 Sent, Reply Date, Reply Type,
Meeting Booked, Notes, Next Action
```

**Name Splitting Rules:**
- Split "John Smith" → First Name: "John", Last Name: "Smith"
- Split "Mary Jane Watson" → First Name: "Mary Jane", Last Name: "Watson" (last word is last name)
- Split "Dr. John Smith" → First Name: "John", Last Name: "Smith" (drop prefix)
- If only one name found → First Name: "[Name]", Last Name: ""
- Suffixes like "Jr.", "III", "PhD", "CHRP" → keep with last name

#### File 2: HOT-LEADS-SUMMARY.md

Include:
- Top 10 priority contacts table (with First Name, Last Name as separate columns)
- Trigger event details for each hot lead
- **Custom email draft for each hot lead** (reference specific trigger, use First Name for greeting)
- Week 1 outreach schedule

#### File 3: email-templates.md

Include:
- 3-email cold sequence (PAS framework)
- Alternative openers for A/B testing
- LinkedIn connection request templates
- Subject line options with expected open rates
- Follow-up timing guide

#### File 4: README.md

Include:
- File overview
- Quick start checklist
- Weekly/monthly outreach goals
- Tracking benchmarks (40% open, 8% reply, 3% meeting)

### Step 7: Present Summary

After creating files, present to user:

1. Stats: Total companies, contacts, hot leads found
2. Top 3 hottest opportunities with why
3. File locations
4. Recommended first actions

## Email Frameworks

### PAS (Problem-Agitate-Solution) - Email 1

```
Subject: quick question about [Company]

Hi [First Name],

[Problem - 1 sentence about common pain point]

[Agitate - What happens if unsolved]

[Solution - How you help, with social proof]

Worth a 15-minute call?

[Your Name]
```

### Follow-up - Email 2 (3-4 days later)

```
Subject: re: quick question about [Company]

Hi [First Name],

Following up on my note from earlier this week.

[Add one new piece of value or social proof]

If [product/service] ever lands on your desk, happy to be a resource.

[Your Name]
```

### Breakup - Email 3 (5-7 days later)

```
Subject: should I close your file?

Hi [First Name],

I've reached out a couple times and haven't heard back—totally get it, you're busy.

I'll assume the timing isn't right and won't follow up again. But if [need] comes up down the road, my door's open.

All the best,
[Your Name]

P.S. — If there's someone else at [Company] I should talk to, I'd appreciate a point in the right direction.
```

## Trigger-Based Email Customization

When a company has a trigger event, customize Email 1:

```
Subject: [company] [trigger - e.g., "expansion", "hiring push"]

Hi [First Name],

Saw the news about [specific trigger - e.g., "the new facility in Thunder Bay"].

When [companies like yours] go through [trigger type], they usually need help with [relevant products/services].

We've worked with [social proof] for [X] years on exactly this.

Would a quick call be useful?

[Your Name]
```

## Dynamic Tuning

- User says "quick list" → 10-15 companies, top contacts only
- User says "comprehensive" → 30-50 companies, full enrichment
- User specifies number → match it
- Ambiguous → default to 20-30 companies

## Models

- **haiku**: All Exa searches, contact extraction, list building
- **sonnet/opus**: Email customization, trigger analysis, final summary
