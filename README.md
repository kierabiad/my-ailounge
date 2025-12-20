# Mind You AI Council and AI Factory

This repository functions as the **Mind You AI Council and AI Factory**, an advanced, AI-powered internal ecosystem engineered to elevate organizational productivity by a factor of 100x. It achieves this by serving as a central hub for strategic AI-driven management and operational execution, systematically reducing manual engineering overhead and fostering unparalleled efficiency across all technical domains.

The agents within this repository are instrumental in:
- Communication triage
- Delivery and Jira management
- Infrastructure and cost hygiene
- Knowledge management
- Structured technical debate

---

## Tooling & Model Usage

This repository is actively used with **Gemini CLI** and **opencode CLI**. The guidance below reflects current team practice and constraints.

### Gemini CLI

- Gemini CLI is used primarily for **management, planning, summaries, and coordination tasks**.
- Each Gemini account has **independent rate limits and capacity**.
- To fully utilize Gemini at scale, developers are expected to:
  - Coordinate with teammates
  - Leverage **partner accounts** when appropriate
  - Be aware of per‑account limits during heavy usage periods
- Gemini’s **auto model selection** is sufficient in most cases and is the preferred mode.
  - The system can decide when to switch models without manual intervention.

### opencode CLI

- opencode is used for **structured agent execution and coding workflows**.
- Model switching in opencode must be **manual and deliberate**.
- Developers are expected to:
  - Choose models explicitly based on the task
  - Understand the **capacity, strengths, and limits** of each model
  - Acknowledge model selection when working on **essential goals or objectives**

### Model Strategy by Role

- **Management & Coordination** → Gemini
- **Coding, Refactoring, Reviews** → Other specialized models (e.g., Anthropic, OpenAI)

This separation is intentional and helps optimize for:
- Cost
- Reliability
- Cognitive clarity


## API Pricing

For pricing information on all models referenced in this document (e.g., OpenAI, Gemini, Anthropic), please consult their respective official API pricing pages.

- OpenAI: [https://openai.com/api/pricing/](https://openai.com/api/pricing/)
- Google Gemini: [https://ai.google.dev/pricing](https://ai.google.dev/pricing)
- Anthropic: [https://www.anthropic.com/api-pricing](https://www.anthropic.com/api-pricing)


## Best Model Per Role

| Role                                 | Recommended Model(s)                                                                                                                                          | Rationale & Strategic Notes                                                                                                                                                                                                                                                                                                                                                                                           |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Code Review**                      | `GPT-5.2` <br> `GPT-5.1` <br> `GPT-4.1` <br> `GPT-4o` <br> `Gemini 3 Pro` <br> `o3`                                                            | *GPT-5.2*: State-of-the-art for deep multi-step review, multi-file context, and agentic orchestration; excelling at automated PR review, traceable reasoning, and tool use across large codebases.<br>*GPT-5.1*: Cost-effective, strong coding/agent performance for continuous review and scrum assistants.<br>*GPT-4.1*: Handles extra-long monorepos, deterministic tool calls.<br>*GPT-4o*: For UX/UI code reviews with multimodal inputs (screenshots, etc).<br>*Gemini 3 Pro* and *o3*: Catch subtle bugs, best for invariants & side-effects.   |
| **Architecture Planning**             | `GPT-5.2` <br> `GPT-5.1` <br> `GPT-4.1` <br> `Gemini 3 Pro` <br> `o3`                                                                         | *GPT-5.2/5.1*: Top for multi-file, long-context system planning, agentic design flows, and knowledge-intensive trade-offs over docs/designs.<br>*GPT-4.1*: Handles massive architecture docs, batch design reviews.<br>*Gemini 3 Pro* and *o3*: Supreme systems thinking and trade-off analysis; leverage for complex scalability and documentation.                                                          |
| **Scrum Master / Standups**           | `GPT-5.2` <br> `GPT-4o` <br> `Gemini 2.5 Flash`                                                                                                       | *GPT-5.2*: Best for orchestrated Jira/standup flows, backlog agents, and tracking sprint status with code context.<br>*GPT-4o*: Low-latency, voice/vision for conversational meetings, triaging, and UI-centric bug tracking.<br>*Gemini 2.5 Flash*: Extremely fast and cheap, excellent for slack/standup summaries and switching project context quickly.                                                       |
| **Tech Lead Planning**                | `GPT-5.2` → `GPT-5.1 Hybrid` <br> `GPT-4.1` → `GPT-4.2 hybrid` <br> `Gemini 3 Pro` → `2.5 Flash Hybrid` <br> `o3`                              | *GPT-5.2/5.1*: Use for project-level planning, risk analysis, and orchestrating coding agents for sprints.<br>*GPT-4.1/4.2*: Combining for structured roadmap generation, changelog synthesis.<br>*Gemini 3 Pro/o3*: Deep strategic analysis (the “brain”).<br>*2.5 Flash/4.2 hybrid*: Generating execution plans, automated ticket writing (the “clipboard”).                                                      |
| **Data Architecture / Schema**        | `GPT-5.2` <br> `GPT-4.1` <br> `Gemini 2.5 Pro` <br> `o3`                                                                                      | *GPT-5.2/4.1*: For schema normalization, lineage tracing, and migration reviews across huge datasets.<br>*Gemini 2.5 Pro*: Balances precision and cost, robust on structural reasoning.<br>*o3*: Remains excellent for pure data modeling and constraint solving.                                                                                                        |
| **Linter / Pre-commit Hook**          | `GPT-4o-mini` <br> `GPT-4.1 (small variant)` <br> `Gemini 2.5 Flash-Lite`                                                                            | Ultra-cheap and fast models (4o-mini, 4.1-small, Flash-Lite) for massive volume pre-commit, formatting, and deterministic static analysis.<br>Excellent for integration in CI pipelines needing instant feedback.                                                                                                                           |
| **Code Generation (Large Features)**  | `GPT-5.2` <br> `GPT-5.1` <br> `Gemini 2.5 Pro`                                                                                                       | *GPT-5.2/5.1*: Top models for agentic assistants writing/refactoring large codebases, handling multi-file context.<br>*Gemini 2.5 Pro*: Strong for big code generation tasks, debugging with logic depth.                                                                                                                                |
| **Real-time Debugging (Voice/Chat)**  | `GPT-4o` <br> `Gemini 2.5 Flash`                                                                                                                     | *GPT-4o*: For multimodal, conversational debugging (text, UI images, voice input/output) with fast feedback.<br>*Gemini 2.5 Flash*: Fast synchronous troubleshooting in chat/voice agents, prioritizing speed over long-form analysis.                                                                |

---

**Forward view:**  
Serious teams run a router:  
* Use the mini-model for volume tasks  
* Use `o3` for judgment calls  
* Use omni (*omni-models*) only when humans are involved  
(*Roles: intern, professor, presenter*)

---

## Philosophy

- Knowledge before automation
- Read‑only before action
- Human‑in‑the‑loop by default
- Python‑first execution

---

## Repository Structure

```text
agents/          # Individual agent definitions
tools/           # Shared Python tool integrations
```

---

## Getting Started

1. Read `AGENTS.md`
2. Explore existing agents in `agents/`
3. Use the new‑agent scaffold to create your own

---

## Non‑Technical Management Documentation

For stakeholders and non‑technical management, additional documentation is available here:

- https://docs.google.com/document/d/16lDOCrXu6rwe9LrreVaaeqMFOpC70GTjccrezGsKt6s/edit?tab=t.0

---

## AI Prompt References

The following spreadsheet contains curated AI prompt references used across agents and workflows:

- https://docs.google.com/spreadsheets/d/1lk6JNKtl3D4bx9b5z_kJ5J8UqMYj0WKFdQ2yE7R87kg/edit?gid=0#gid=0

---

## Non‑Goals

- Replacing human judgment
- Silent or destructive automation
- General application framework

---

# 2026 Targets

## Engineering Targets
- Reduce repetitive Jira/Slack overhead

## Agent & Tooling Targets

- Prompt library with clear categories
- At least 3 reusable Python tools
- Tech Lead assistant
- Scrum master - organizes the jira tickets
- App Tester
- Main Website Tester
- Portal Website Tester
- Analytics Website Tester

## General Improvements
- Faster architectural reviews
- Better consistency in decisions
- Fewer ad‑hoc decisions
- Better documentation
- Less context switching

## Quality Targets
- Improve overall code quality and reliability

## Ownership

This repo is owned by the engineering team and evolves continuously.
