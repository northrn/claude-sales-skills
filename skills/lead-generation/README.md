# Lead Generation Skill

Build targeted B2B outreach lists with enriched contacts, trigger events, and ready-to-send email templates.

## Quick Start

1. Copy to your skills folder:
   ```bash
   cp lead-generation.md ~/.claude/skills/
   ```

2. Use in Claude Code:
   ```
   find leads for healthcare companies in Texas
   ```

## Requirements

- [Exa MCP Server](https://exa.ai) for company/contact search

## Trigger Phrases

- "find leads for..."
- "build outreach list for..."
- "lead generation for..."
- "prospect list for..."
- "find contacts at..."

## Output

Creates a folder with:

| File | Contents |
|------|----------|
| `outreach-tracker-enriched.csv` | Full contact list with LinkedIn URLs, trigger events, priority scores |
| `HOT-LEADS-SUMMARY.md` | Top 10 contacts with custom email drafts |
| `email-templates.md` | Cold email sequences (PAS framework) |
| `README.md` | Quick start guide |

## Example

```
> build outreach list for fintech startups in Toronto

Creating outreach list for fintech startups in Toronto...

✓ Found 28 companies
✓ Found 45 contacts with LinkedIn profiles
✓ Identified 6 trigger events (funding, hiring, expansion)
✓ Scored and prioritized leads

Top opportunities:
1. Wealthsimple - Series F funding ($750M) - Contact: Head of Marketing
2. Koho - Expansion announcement - Contact: Communications Director
3. Neo Financial - Active hiring (50+ roles) - Contact: HR Director

Files created: ~/Documents/fintech-toronto-outreach/
```

## Customization

Edit the skill file to:

- Change default target roles
- Modify email templates
- Adjust priority scoring
- Add industry-specific search queries
