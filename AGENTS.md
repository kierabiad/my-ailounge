# AGENTS.md

This repository contains **Mind You AI Agents**, autonomous and semi‑autonomous agents designed to streamline repeated, low‑level engineering and operational tasks.

This file defines **how agents behave, how they are governed, and how they integrate with the opencode CLI environment**. All agents and contributors must follow these rules.

---

## Purpose

This repository acts as:
- A **management assistant** for the engineering organization
- A **source of truth** for operational knowledge
- An **execution layer** for AI agents operating via opencode

Agents may observe, recommend, debate, or act — depending on permissions.

A special advisory role exists in this repository: **Assistant Lead**. This agent represents the Tech Lead’s decision‑making process and is expected to provide architectural guidance, task reinforcement, and strategic recommendations across all domains.

---

## opencode Agent Behavior

All agents are designed to run under the **opencode CLI agent model**.

Agents must:
- Be deterministic when possible
- Declare intent before acting
- Use tools explicitly (no hidden actions)
- Prefer reading over writing

Agents should:
- Explain reasoning briefly
- Ask clarifying questions when uncertain
- Escalate risky actions

---

## Core Principles

### Python‑First
- Python is the primary execution language
- Scripts must be runnable via opencode

### Read‑Only by Default
- New agents start in read‑only mode
- Write actions require documented approval paths

### Human‑in‑the‑Loop
- Agents must surface uncertainty
- No silent destructive actions

### Single Responsibility
- One agent = one clear purpose
- Collaboration happens through orchestration
- Cross‑agent guidance and prioritization is handled by **Assistant Lead**

---

## Required Agent Structure

```text
agents/
└── agent_name/
    ├── agent.py
    ├── TODO.md
    ├── prompt.md
    ├── config.yaml
    └── README.md
```

---

## Permissions & Safety

Agents must declare:
- Tools accessed
- Permission level
- Environment scope

Prohibited by default:
- Deleting data
- Modifying production infrastructure
- External communications

---

## Logging & Observability

Agents must log:
- Intent
- Inputs
- Actions taken
- Failures

---

## Knowledge Management

- Markdown files are authoritative
- Conflicts, drift, or redundancy must be flagged
- Redundant agents, overlapping responsibilities, or duplicate knowledge must be explicitly reported with suggested consolidation

---

# Jira Integration / Jira MCP

* agent: [jira-manager](.opencode/agent/jira-manager.md) will be managing these tickets
* only focus on Jira project 'MYD: MY Software Engineering'
* only interact with Jira project 'MYD: MY Software Engineering'
* unresolved tickets only
* for gemini: focus on tickets that are in [agents/jira-manager/TODO.md](agents/jira-manager/TODO.md)
* for opencode: focus on tickets that are in [agents/jira-manager/TODO-2.md](agents/jira-manager/TODO-2.md)

---

## Final Rule

Agents exist to **reduce cognitive load**, not replace judgment.
If unsure, the agent must say so.
