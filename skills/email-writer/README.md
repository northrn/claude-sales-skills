# Email Writer Skill

Generate highly personalized cold emails using prospect research.

## Quick Start

```bash
cp email-writer.md ~/.claude/skills/
```

## Trigger Phrases

- "write cold email to [person] at [company]"
- "personalize email for [person]"
- "cold email for [company]"
- "write outreach to [person]"

## Output

Generates `[person]-outreach.md` with:
- 3 email variants (different angles for A/B testing)
- 3-5 subject lines per variant with predicted open rates
- Follow-up sequence (emails 2 and 3)
- LinkedIn connection request and follow-up message
- Explanation of personalization strategy

## Example

```
> write cold email to Sarah Chen at Notion

Researching Sarah Chen...

✓ Found LinkedIn profile
✓ Found recent podcast appearance
✓ Company raised Series C recently

Generating emails...

✓ Variant A: Trigger-based (references funding)
✓ Variant B: Content-based (references her podcast)
✓ Variant C: Problem-first (role-based pain point)
✓ Follow-up sequence
✓ LinkedIn messages

File created: ~/Documents/sarah-chen-outreach.md
```

## Email Quality

All emails follow best practices:
- Under 100 words
- Personalization in first sentence
- Single clear CTA
- Mobile-friendly format
- No generic openers
