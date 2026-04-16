# Level 3 Submission — Shubham Kumar
**Track A: Agent Builders**

## Agent: Digital Twin ROI Scoper

**Repo:** https://github.com/kshubham090/lpi-roi-scoper
**Code:** `submissions/shubham-kumar/level3/agent.py`
**A2A Card:** `submissions/shubham-kumar/level3/agent.json`

## What It Does

So basically I built this agent that acts like a consultant. You tell it your industry, what you want to do, and how much time or people you have — and it goes and fetches real data from the LPI tools, thinks about it, and tells you what's actually doable. Not just what sounds cool, but what fits your situation. It also tells you what to not do yet, which I think is actually the more useful part.

Takes three inputs from the user:
- Industry (e.g. healthcare, manufacturing, smart buildings)
- Use case (e.g. predictive maintenance, energy optimization)
- Constraints (e.g. small team, 3 months, limited budget)

Queries three LPI tools in sequence, synthesizes via local Ollama LLM, and outputs a structured ROI scope report:

1. **Realistic scope** — what can actually be done given constraints
2. **Expected outcomes** — grounded in real case studies from the LPI
3. **SMILE phases to prioritize** — based on scenario-specific advice
4. **What to skip/defer** — so the team doesn't overcommit early
5. **First 3 actions** — concrete steps to start this week

Every claim cites its source tool. Provenance is printed separately at the end.

## LPI Tools Used

| Tool | Arguments | Purpose |
|------|-----------|---------|
| `get_insights` | `scenario: "{usecase} in {industry}"` | Scenario-specific SMILE implementation advice |
| `get_case_studies` | `query: "{industry}"` | Real-world analogues in the same industry |
| `query_knowledge` | `query: "{usecase} digital twin implementation"` | Technical implementation knowledge |

## Tech Stack

- Python 3.10+
- Ollama (local LLM — no API key required)
- LPI MCP server via subprocess (JSON-RPC stdio)
- Standard library only (+ `requests`)

## Run It

```bash
# Interactive
python submissions/shubham-kumar/level3/agent.py

# CLI
python submissions/shubham-kumar/level3/agent.py \
  --industry healthcare \
  --usecase "patient flow optimization" \
  --constraints "2 developers, 2 months, no cloud"
```
