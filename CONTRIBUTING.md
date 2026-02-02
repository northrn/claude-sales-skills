# Contributing to Claude Sales Skills

We welcome contributions! Here's how to add your own skills.

## Skill File Format

All skills are markdown files with YAML frontmatter:

```markdown
---
name: skill-name
description: Brief description of what the skill does
triggers: comma, separated, trigger, phrases
requires_mcp: exa, github (optional - list required MCP servers)
context: fork
---

# Skill Name

## What This Skill Does

Describe the output and value.

## Workflow

Step-by-step instructions Claude will follow.

## Templates/Frameworks

Any templates, prompts, or frameworks the skill uses.
```

## Best Practices

### 1. Token Isolation

For skills that make many API calls or process large amounts of data, use Task agents:

```markdown
Spawn Task agent with model "haiku" to:
- Run searches internally
- Process and deduplicate results
- Return only distilled output
- Keep main context clean
```

### 2. Clear Outputs

Define exactly what files/artifacts the skill creates:

```markdown
## Output Files

| File | Description |
|------|-------------|
| `output.csv` | Main data file |
| `summary.md` | Human-readable summary |
```

### 3. Sensible Defaults

Provide defaults but allow customization:

```markdown
- User says "quick" → minimal output
- User says "comprehensive" → full output
- Ambiguous → ask or use reasonable default
```

### 4. Error Handling

Include fallback instructions:

```markdown
If Exa returns insufficient results:
- Try alternative query variations
- Expand geography
- Notify user of limitations
```

## Directory Structure

```
skills/
├── skill-name/
│   ├── skill-name.md    # Main skill file
│   └── README.md        # Documentation
```

## Submitting a Skill

1. Fork this repository
2. Create your skill in `skills/your-skill-name/`
3. Test thoroughly with Claude Code
4. Submit a pull request with:
   - Description of what the skill does
   - Example usage
   - Any MCP requirements

## Skill Ideas

Looking for ideas? Here are some we'd love to see:

### Sales & BD
- **Account Research** - Deep dive on a single company
- **Competitor Analysis** - Map competitive landscape
- **Meeting Prep** - Research before sales calls
- **Objection Handling** - Generate responses to common objections

### Marketing
- **Content Research** - Find trending topics and angles
- **SEO Analysis** - Keyword and competitor analysis
- **Social Listening** - Monitor brand mentions

### Operations
- **Vendor Research** - Compare potential vendors
- **Market Sizing** - TAM/SAM/SOM calculations
- **Pricing Research** - Competitive pricing analysis

## Questions?

Open an issue or reach out!
