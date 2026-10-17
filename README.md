# Agent Builder

A Claude skill. Design a reusable AI agent for any goal: define the outcome, fill the Agent Blueprint, and output a ready system prompt, tool list, guardrails and test plan.

## What's inside

- `agent-builder/SKILL.md`

## Install

### Claude app (claude.ai, desktop, mobile)

1. Download this repo as a ZIP (**Code > Download ZIP**) and unzip it.
2. Zip the `agent-builder` folder on its own, so the ZIP contains `agent-builder/SKILL.md`.
3. In Claude's settings, open the Skills section, upload that ZIP, and turn the skill on.

### Claude Code

```bash
git clone https://github.com/bogsdav/agent-builder.git
mkdir -p ~/.claude/skills
cp -r agent-builder/agent-builder ~/.claude/skills/
```

Restart Claude Code. The skill loads automatically when a request matches its description.

## Try it

- "Design an agent that triages my inbox every morning."
- "Fill the Agent Blueprint for a customer-support assistant."
- "Give me the system prompt, tools and test plan for a research agent."

## License

MIT. See [LICENSE](LICENSE).
