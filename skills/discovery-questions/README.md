# Discovery Questions Skill

Generate tailored discovery questions based on role, industry, and context.

## Quick Start

```bash
cp discovery-questions.md ~/.claude/skills/
```

## Trigger Phrases

- "discovery questions for [role] at [industry]"
- "what should I ask [prospect]"
- "questions for discovery call"
- "sales questions for [context]"

## Output

Generates `discovery-questions-[context].md` with:
- Opening questions (rapport and agenda)
- Situation questions (current state)
- Problem questions (uncover pain)
- Implication questions (quantify impact)
- Need-payoff questions (articulate value)
- Qualification questions (BANT+)
- Follow-up prompts for common answers
- Red flags to watch for
- Recommended call structure

## Example

```
> discovery questions for VP Marketing at a SaaS company

Generating questions...

✓ Role-specific questions for VP Marketing
✓ SaaS industry context added
✓ Follow-up prompts included
✓ Red flags identified

File created: ~/Documents/discovery-questions-vp-marketing-saas.md
```

## Question Framework

Uses **SPIN Selling** methodology:
- **S**ituation - Understand current state
- **P**roblem - Uncover pain points
- **I**mplication - Quantify the impact
- **N**eed-Payoff - Get them to articulate value

Plus qualification (BANT) and competition questions.
