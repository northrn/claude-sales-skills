# Claude Sales Skills

A collection of **Claude Code skills** that turn Claude into a cold-blooded GTM engineer.

These skills extend [Claude Code](https://claude.ai/code) with specialized capabilities for sales, lead generation, competitive intelligence, and business development.

## The GTM Engineer Stack

| Skill | What It Does | Triggers |
|-------|--------------|----------|
| [Lead Generation](skills/lead-generation/) | Build targeted outreach lists with contacts, LinkedIn profiles, trigger events | "find leads for", "build outreach list" |
| [Account Research](skills/account-research/) | Deep dive on a company - org chart, tech stack, news, pain points | "research [company]", "tell me about" |
| [Meeting Prep](skills/meeting-prep/) | Pre-call brief with attendee profiles, questions, objection handling | "prep me for call with", "meeting prep" |
| [Email Writer](skills/email-writer/) | Personalized cold emails with A/B variants and follow-up sequences | "write cold email to", "personalize email" |
| [Competitor Intel](skills/competitor-intel/) | Competitive landscape mapping and sales battlecards | "analyze competitors", "battlecard for" |
| [Discovery Questions](skills/discovery-questions/) | Tailored SPIN questions by role, industry, and context | "discovery questions for", "what should I ask" |
| [Proposal Writer](skills/proposal-writer/) | Generate proposals from call notes with pricing options | "write proposal for", "create proposal" |

## How They Work Together

```
Day 1: "find leads for fintech companies in Toronto"
       → Creates list of 30 companies with 50+ contacts

Day 2: "research Wealthsimple"
       → Deep dossier with org chart, tech stack, pain points

Day 3: "write cold email to Sarah at Wealthsimple"
       → 3 personalized email variants + follow-up sequence

Day 4: "discovery questions for VP Product at fintech"
       → Tailored SPIN questions + follow-up prompts

Day 5: "prep me for call with Wealthsimple"
       → Pre-call brief with attendee research, objection handling

Day 6: "analyze competitors in wealth management space"
       → Battlecards for positioning against alternatives

Day 7: "write proposal for Wealthsimple"
       → Complete proposal with pricing options + case studies
```

## Installation

### Quick Install (One Skill)

```bash
# Create skills directory
mkdir -p ~/.claude/skills

# Download a skill
curl -o ~/.claude/skills/lead-generation.md \
  https://raw.githubusercontent.com/northrn/claude-sales-skills/main/skills/lead-generation/lead-generation.md
```

### Install All Skills

```bash
# Clone repo
git clone https://github.com/northrn/claude-sales-skills.git

# Copy all skills
cp claude-sales-skills/skills/*/*.md ~/.claude/skills/
```

### Verify Installation

```bash
ls ~/.claude/skills/
# Should show: lead-generation.md, account-research.md, etc.
```

## Requirements

These skills use **Exa** for AI-powered web search. You'll need:

1. Get an API key at [exa.ai](https://exa.ai)
2. Add Exa to your Claude Code MCP config (`~/.claude/mcp.json`):

```json
{
  "mcpServers": {
    "exa": {
      "command": "npx",
      "args": ["-y", "@anthropic/exa-mcp-server"],
      "env": {
        "EXA_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

## Skill Details

### Lead Generation
Find companies and contacts in any industry/geography. Outputs:
- Enriched CSV with contacts, LinkedIn URLs, trigger events
- Hot leads summary with custom emails
- Cold email templates

**Example:** `find leads for healthcare companies in Northern Ontario`

---

### Account Research
Deep research on a single company. Outputs:
- Company snapshot (funding, size, tech stack)
- Key people with LinkedIn profiles
- Recent news and triggers
- Pain points and outreach angles

**Example:** `research Stripe`

---

### Meeting Prep
Pre-call brief for any sales conversation. Outputs:
- Attendee profiles with rapport hooks
- Tailored discovery questions
- Likely objections with responses
- Talking points and conversation starters

**Example:** `prep me for call with Notion`

---

### Email Writer
Personalized cold emails using prospect research. Outputs:
- 3 email variants for A/B testing
- Subject lines with predicted open rates
- Follow-up sequence (emails 2-3)
- LinkedIn connection messages

**Example:** `write cold email to Sarah Chen at Notion`

---

### Competitor Intel
Map competitive landscape and create battlecards. Outputs:
- Competitor landscape map
- Feature comparison matrix
- Pricing intelligence
- Battlecards with objection handling

**Example:** `analyze competitors for our CRM product`

---

### Discovery Questions
Generate tailored discovery questions using SPIN methodology. Outputs:
- Situation, Problem, Implication, Need-Payoff questions
- Role-specific and industry-specific questions
- Follow-up prompts for common answers
- Red flags to watch for
- Recommended call structure

**Example:** `discovery questions for VP Marketing at a SaaS company`

---

### Proposal Writer
Generate complete proposals from call notes or deal context. Outputs:
- Executive summary
- Understanding of needs section
- Solution mapped to requirements
- Scope of work
- 3 pricing options (anchored high)
- Timeline with milestones
- Relevant case studies
- Terms and next steps

**Example:** `write proposal for Acme Corp based on our discovery call`

---

## Contributing

We welcome new skills! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Skills We'd Love

**Sales:**
- Discovery Question Generator
- Proposal Writer
- Objection Handler Library
- Win/Loss Analyzer

**Marketing:**
- Content Researcher
- SEO Analyzer
- Social Post Generator
- Event Intel

**Operations:**
- Territory Planner
- Pipeline Analyzer
- Forecast Builder

## License

MIT License - see [LICENSE](LICENSE)

---

Built with [Claude Code](https://claude.ai/code)
