# Proposal Writer Skill

Generate professional sales proposals from call notes or deal context.

## Quick Start

```bash
cp proposal-writer.md ~/.claude/skills/
```

## Trigger Phrases

- "write proposal for [company]"
- "create proposal for [deal]"
- "generate proposal"
- "draft proposal for [company]"

## Output

Generates `proposal-[company]-[date].md` with:
- Executive summary
- Understanding of needs (from their perspective)
- Proposed solution mapped to requirements
- Scope of work with inclusions/exclusions
- Pricing with 3 options
- Timeline with milestones
- Relevant case studies
- Terms and next steps

## Example

```
> write proposal for Acme Corp, they need our analytics platform,
> budget is $50k, main pain point is manual reporting taking 20 hours/week

Generating proposal...

✓ Researched Acme Corp
✓ Found relevant case studies
✓ Created 3 pricing options
✓ Built implementation timeline

File created: ~/Documents/proposal-acme-corp-2025-02-02.md
```

## Best Practices

Provide as much context as possible:
- Call notes or meeting summary
- Specific pain points discussed
- Their requirements and must-haves
- Budget range
- Timeline expectations
- Who else is involved in decision
