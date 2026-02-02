# Claude Sales Skills

A collection of **Claude Code skills** for sales, lead generation, and business development.

These skills extend [Claude Code](https://claude.ai/code) with specialized capabilities for sales professionals, founders, and business development teams.

## What Are Claude Code Skills?

Skills are markdown files that give Claude Code specialized knowledge and workflows for specific tasks. When you use trigger phrases, Claude automatically loads the skill and follows its instructions.

## Available Skills

| Skill | Description | Triggers |
|-------|-------------|----------|
| [Lead Generation](skills/lead-generation/lead-generation.md) | Build targeted outreach lists with contacts, LinkedIn profiles, trigger events, and ready-to-send email templates | "find leads", "build outreach list", "prospect list" |

## Installation

### Option 1: Copy Individual Skills

1. Create the skills directory (if it doesn't exist):
   ```bash
   mkdir -p ~/.claude/skills
   ```

2. Copy the skill file you want:
   ```bash
   curl -o ~/.claude/skills/lead-generation.md \
     https://raw.githubusercontent.com/northrn/claude-sales-skills/main/skills/lead-generation/lead-generation.md
   ```

3. Use it in Claude Code:
   ```
   find leads for SaaS companies in Austin
   ```

### Option 2: Clone Entire Repo

```bash
git clone https://github.com/northrn/claude-sales-skills.git
cp claude-sales-skills/skills/*/*.md ~/.claude/skills/
```

## Requirements

Some skills require MCP (Model Context Protocol) servers:

| Skill | Required MCP |
|-------|-------------|
| Lead Generation | [Exa](https://exa.ai) - AI-powered web search |

### Setting Up Exa MCP

1. Get an API key at [exa.ai](https://exa.ai)
2. Add to your Claude Code MCP config:
   ```json
   {
     "mcpServers": {
       "exa": {
         "command": "npx",
         "args": ["-y", "@anthropic/exa-mcp-server"],
         "env": {
           "EXA_API_KEY": "your-api-key"
         }
       }
     }
   }
   ```

## Skill Output

The Lead Generation skill creates a complete outreach package:

```
~/Documents/{industry}-{geography}-outreach/
├── outreach-tracker-enriched.csv    # Full contact list with LinkedIn, triggers
├── HOT-LEADS-SUMMARY.md             # Top 10 priority contacts + custom emails
├── email-templates.md               # Cold email sequences
└── README.md                        # Quick start guide
```

## Example Usage

```
> find leads for healthcare companies in the Northeast US

Claude will:
1. Search for healthcare organizations in the region
2. Find key contacts (Marketing, HR, Communications, Procurement)
3. Identify trigger events (funding, expansion, hiring)
4. Score and prioritize leads
5. Generate custom email templates
6. Create ready-to-use CSV tracker
```

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Skill Ideas We'd Love

- **Account Research** - Deep dive on a single company
- **Competitor Analysis** - Map competitive landscape
- **Meeting Prep** - Research before sales calls
- **LinkedIn Outreach** - Optimized connection sequences
- **CRM Enrichment** - Bulk enrich existing contacts

## License

MIT License - see [LICENSE](LICENSE)

---

Built with [Claude Code](https://claude.ai/code)
