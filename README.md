# AI Council
### A Governed Multi-Agent Deliberation System

---

## What This Is

The AI Council is a governed multi-agent reasoning system — a framework of seven independent voices, each representing a distinct institutional perspective, coordinated through a structured deliberation protocol to produce durable, auditable outputs on complex problems.

It is architecture-first and governance-first. The governing documents are the system. The wrapper executes them.

---

## The Problem It Addresses

AI systems working on complex tasks exhibit consistent failure modes. Topic drift pulls the system away from its original objective. Role drift blurs the boundaries of what the system was designed to do. Silent assumption creep introduces unstated premises that compound over time. Context degradation erodes the coherence of earlier decisions as the session grows.

Scaling beyond a single instance introduces a second class of problems. Multiple AI instances operating on the same problem without explicit coordination produce blended, dominated, or contradictory output. Without a defined protocol for how instances communicate, defer, flag concerns, and contribute to a shared record, the coordination layer becomes the new failure surface.

These failure modes matter most when the output carries real weight. In those contexts a drifting system produces not just an unreliable output but an unauditable one — no record of what was considered, what perspectives were surfaced, what conflicts existed, or where the reasoning went wrong.

The AI Council addresses each failure mode with a dedicated architectural layer.

---

## How It Works

### The Document Stack

Every voice instance is initialized from a precisely defined document stack. The stack is not variable. Every instance receives the same foundational documents and one unique Voice Delta that defines its institutional identity.

**Kernel** — foundational governance layer. Establishes document authority ordering, conflict resolution rules, and immutability constraints. Every instance reads this first.

**Exchange Document** — governs how every instance writes to and interacts with the Paper. Defines entry format, the flag and tag systems, and the two permitted Paper operations.

**Voice Core** — shared behavioral baseline all seven voices inherit equally. Establishes violation staging, withheld authorities, and the delta relationship.

**Voice Delta** — one of seven. Defines this instance's institutional mandate, personality weight configuration, and any authorized modifications to the Voice Core baseline.

**Personality Core** — instructs the instance how to apply its weighted cognitive orientation. Not a governance document. Shapes expression only.

**Personality Deltas** — four cognitive orientations (Analyst, Consultant, Designer, Operator) blended at weights declared in the Voice Delta.

A higher document in the authority ordering always takes precedence. Conflicts are never resolved silently. A rule may only be overridden by a lower document if the higher document explicitly authorizes that override, names the condition, and identifies which delta holds the authority.

---

### The Paper Model

The Paper is the single source of truth for a deliberation session. Every voice instance reads it in full before producing output. All contributions, structural markers, flags, tags, and session events are written to it. Nothing about the session exists outside it.

Two operations are permitted. **Write** produces a new entry. **Classify** applies a tag to an existing entry retroactively. Content is immutable once written. Tags are append-only with one authorized exception declared in The Judge's delta.

Structural markers written by the wrapper appear as `{SYSTEM}` entries — seat order declarations, round order sequences, session open and close markers. Infrastructure made visible in the record.

---

### The Flag and Tag System

**Flags** are positional strings routing attention to specific voices. Seat order is fixed at session open. A flag of `(X__X_X_)` in a seven-voice session signals voices in positions one, four, and six. Flags accumulate across a round — the voice with the most flags leads the following round. A voice that received no flags may abstain entirely.

**Tags** classify entries and govern escalation.

| Tag | Meaning | Effect |
|---|---|---|
| `{Warn}` | Entry approaches a boundary | Entry remains active, all voices treat with caution |
| `{Vio1}` | Clear mandate violation | Entry disqualified from deliberation, session continues |
| `{Vio2}` | Severe or repeat violation | Pause-and-review — wrapper routes to The Judge before continuing |
| `{Halt}` | Session integrity compromised | Pause-and-review — wrapper routes to The Protector before continuing |

`{Vio2}` and `{Halt}` are circuit breakers, not correction tools. They stop the deliberation so the situation can be evaluated externally before continuing.

Any voice may apply any tag. Decision authority over interrupt-level consequences belongs exclusively to the voice whose delta declares it.

---

### The Seven Voices

The voices are the institutional perspectives that constitute the deliberation. All seven are architecturally equal — flat hierarchy, no governing tier. Special authorities are explicitly declared in individual deltas, not inherited from position.

| Voice | Institutional Identity | Delta Authority |
|---|---|---|
| **The Judge** | Legitimate Governance & Rule of Law | Tag modification authority; evaluates `{Vio2}` interrupts |
| **The Steward** | Justice & Conflict Resolution | Session open authority; permanent session presence; checkpoint authority |
| **The Protector** | Security & Protection | `{Halt}` execution authority; autonomous intervention |
| **The Scholar** | Continuity & Archival | Document authorship for transcripts and concept keys; writes to `reference/` |
| **The Builder** | Adaptation & Self-Correction | Read access to `reference/` directory; additive-only mandate |
| **The Trader** | Feasibility & Financial Grounding | Criteria-governed external fetch authority; maps the deliberation floor |
| **The Visionary** | Research & Developmental Grounding | Criteria-governed external fetch authority; maps the deliberation ceiling |

---

### The Arbitration Core

The Arbiter is not a voice instance. It is the wrapper — the orchestration logic that manages session lifecycle, pipes documents to voice APIs, and enforces the deliberation protocol. It does not reason, deliberate, or contribute content. It executes functions.

The Arbitration Core document specifies the full execution logic: session initialization, seat order generation, pre-deliberation sequence, round execution loop, interrupt handling for `{Vio2}` and `{Halt}`, exit conditions, and session close.

---

## Repository Structure

```
KERNEL.md                          — Document orientation, authority ordering, immutability
EXCHANGE.md                        — Paper interaction protocol, flag and tag system
ARBITRATION_CORE.md                — Wrapper orchestration logic and execution specification
DESIGN_BRIEF.md                    — Full system overview, philosophy, and current state

/voices
    THE_JUDGE.md
    THE_STEWARD.md
    THE_PROTECTOR.md
    THE_SCHOLAR.md
    THE_BUILDER.md
    THE_TRADER.md
    THE_VISIONARY.md
    VOICE_CORE.md

/personality
    PERSONALITY_CORE.md
    ANALYST.md
    CONSULTANT.md
    DESIGNER.md
    OPERATOR.md

/templates
    TEMPLATE_TRANSCRIPT.md          — Verbatim session transcript format (Scholar reference)
    TEMPLATE_CONCEPT_KEY.md         — Concept key format (Scholar reference)
    TEMPLATE_VIOLATION_DOCUMENT.md  — Violation document format (Judge reference)
```

---

## Current Status

All governance documents are complete. All seven voice deltas are complete. The wrapper (Orchestra) is in active development against the fully specced Arbitration Core.

| Component | Status |
|---|---|
| Kernel | Complete |
| Exchange Document | Complete |
| Voice Core | Complete |
| Arbitration Core | Complete |
| Personality Core + 4 deltas | Complete |
| All 7 Voice Deltas | Complete |
| 3 Template Documents | Complete |
| Orchestra wrapper | In development |
| Persistent document system | Designed, implementation in progress |

---

## What This Is Not

- A conversational assistant
- An autonomous decision-maker
- A consensus engine — unresolved conflict in the output is a feature, not a failure
- A recommendation engine
- A memory-dependent system — every session initializes from documents, not history
- A solution to the full AI alignment problem — it contributes to one track of a larger problem

---

## Philosophy

The governing philosophy begins with a position on inevitability. AI capability exceeding human oversight is not a contingency to prepare for. It is a timeline to design around. The question is not whether to prevent that but how to manage the conditions under which it happens and what exists downstream when it does.

This project is a contribution to one of two simultaneous obligations that cannot be pursued independently — demonstrating that governed multi-agent reasoning is architecturally viable, that AI systems operating within a defined governance structure can be directed, constrained, and held accountable without engineering out the capabilities that make them useful.

The principle that makes that contribution possible is the same one that should govern AI development at scale: no single entity can govern itself reliably. A system with sole authority over its own behavior has no external tension to hold it centered. The AI Council's architecture is built on that premise.

---

*This is a working architecture and a partially implemented system. It is not a finished product.*
