---
name: "agent-builder"
description: "Design a reusable AI agent for any goal: define the outcome, fill the Agent Blueprint, and output a ready system prompt, tool list, guardrails and test plan."
---

# Agent Builder

Use this skill when the user wants to create, design, spec or improve an AI agent, automation or assistant for any goal (work, personal, business, study). It turns a rough goal into a complete, reusable agent spec.

## Core idea

An agent is a model running in a loop: decide the next step, use a tool, check the result, repeat until the outcome is met or a rule says to ask a human. Every agent is built from the same 7 blocks; only their contents change.

## Workflow

### 1. Define the goal
Get answers to these five questions. Infer what you can from the conversation; ask only for what is missing (at most 3 short questions at once, then proceed with stated assumptions).

1. Outcome: what exists when the agent is done? (one sentence)
2. Trigger: on request, a schedule, or an event?
3. Inputs: what information does it need, and where does it live?
4. Actions: what must it be able to do (search, read, write, send, update)?
5. Stakes: worst result of a wrong action?

### 2. Pick the lightest option
| Option | Use when |
| --- | --- |
| Prompt | Occasional task; user can paste inputs |
| Workflow | Same fixed steps every time (trigger, AI step, automation) |
| Agent | Steps vary case by case and need judgment |

Recommend the lightest one that works and say why. If the user cannot describe inputs, steps and a correct result, suggest they do the task once while narrating it and use that transcript as the instructions.

### 3. Fill the 7 building blocks
1. Model: capable tool-using model; larger for hard judgment, smaller for high-volume simple work.
2. Instructions: role and principle, context, inputs, steps, output, rules.
3. Tools: smallest set needed (start with 2 to 4), each with a clear name and a "use this when" description, marked read or write.
4. Loop: trigger, step limit, where results go.
5. Memory and knowledge: reference material plus what to save between runs.
6. Guardrails: approval points, forbidden actions, when to stop and ask.
7. Evaluation: 10 to 20 test cases, a success metric, a review schedule.

### 4. Produce the Agent Blueprint
Output the completed blueprint in this exact structure. Sections 1 to 6 must read as a ready-to-paste system prompt.

```markdown
# Agent: [NAME]

## 1. Outcome
[One sentence describing what exists when the agent is done.]

## 2. Role and principle
You are my [ROLE]. You work from one principle: [BELIEF].

## 3. Context
- About me / my situation: [...]
- Audience for the output: [...]
- Voice and style: [...]
- Priorities: [...]

## 4. Inputs
- What I'll give you: [...]
- What you'll fetch yourself: [...]
- If anything is missing, ask once, then proceed with your best assumption and say what you assumed.

## 5. Steps
1. Gather everything relevant
2. Filter out noise
3. Analyze / decide
4. Produce the work
5. Check it against the outcome and rules
6. Present for review

## 6. Output and rules
- Format: [...]
- Never: [invent facts / send / pay / delete / publish] without my approval.
- Stop and ask me when: [...]
- Before finishing, check: Is it correct? Is it useful? Is the next step clear?

## 7. Trigger
[...]

## 8. Tools
| Tool | Use it when | Read or write | Needs my approval |
| --- | --- | --- | --- |

## 9. Memory and knowledge
- Reference material: [...]
- Save for next time: [...]

## 10. Success measures
- Test cases: [...]
- Metric: [...]
- Review: [...]
```

Replace every bracket with specifics for the user's goal. Steps in section 5 should be concrete to the task, not the generic placeholders.

### 5. Recommend a build route
| Route | Best for |
| --- | --- |
| Assistant (Claude project with the blueprint as instructions, plus connectors and scheduled tasks) | Research, writing, inbox, planning; no code |
| No-code workflow (Zapier, Make, n8n with an AI step) | Fixed steps moving data between apps |
| Code (Anthropic API tool-use loop, Claude Agent SDK, LangGraph) | Variable steps, custom tools, full control |

If the user picks code, provide a minimal working tool-use loop with a step limit, and tool definitions matching section 8.

### 6. Give the test-and-improve plan
1. Record a baseline (time and quality today).
2. Run in draft mode: agent prepares, human approves anything that leaves the sandbox.
3. Test on 10 to 20 real examples, including messy ones.
4. Read transcripts; fix instructions, tool descriptions or examples before changing models.
5. Measure % accepted without edits, time saved, errors.
6. Widen autonomy one step at a time on low-risk cases.
7. Review weekly.

## Guardrails checklist (run before finishing)
- Outcome fits in one sentence with a clear "done".
- Only necessary tools; write/delete access only where required.
- Irreversible actions (send, pay, delete, publish, move money) require approval.
- Step limit set; agent asks when stuck instead of guessing.
- Told never to invent facts, numbers or quotes; cites sources.
- Sensitive data only in trusted tools.
- Higher stakes means narrower tools and more approval points.

Flag any item that fails and suggest the fix.

## Common mistakes to warn about
- Goal too broad: split into several small agents.
- Too many tools: start with 2 to 4.
- Vague tool descriptions: say exactly when to use each.
- Full autonomy on day one: earn it with test results.
- No feedback loop: schedule reviews.

## Output format
1. One-line summary: what the agent does and the recommended option (prompt, workflow or agent).
2. Assumptions made (if any).
3. The completed Agent Blueprint.
4. Build route recommendation, with code if requested.
5. Test plan and any failed guardrail checks.

If the user will keep or share the spec, offer to save it as a document.