# Proposal Generator
> Automated sales proposal engine — from client brief to signed PDF in minutes.

---

## What It Does

- **Client fills a multi-step intake form** → a complete commercial proposal is generated automatically, without any manual writing or formatting.
- **AI reads the project brief**, identifies scope and requirements, selects the relevant service packages, and calculates a tailored estimate.
- **Outputs a complete deck and invoice** — cloned from a master template, populated with custom content, and sent directly to the client via email.
- **CRM updated at every step** — deal records, contact info, document links, and status fields are synced automatically throughout the pipeline.

---

## Architecture Overview

```
[Client fills multi-step intake form]
              │
              ▼
     [Analysis Layer]
  AI reads brief — identifies
  project type, scope, constraints
              │
              ▼
    [Pricing Engine]
  Matches scope to service grid,
    calculates tailored estimate
              │
              ▼
    [Generation Layer]
  AI writes all slide content
    and proposal narrative
              │
              ▼
   [Document Builder]
  Clones master template,
  replaces all placeholders
              │
              ▼
    [Delivery Layer]
  Exports PDF → sends via email
       → updates CRM
```

---

## Stack

| Layer | Approach |
|---|---|
| Intake | Multi-step web form (stateless, zero JS framework) |
| Analysis | AI pipeline (project classification + scope parsing) |
| Pricing | Rule-based service matching with AI validation |
| Generation | AI writing pipeline (proposal narrative + slide copy) |
| Document Builder | Template clone + placeholder replacement engine |
| Delivery | Email dispatch + CRM sync |
| Orchestration | Event-driven async workflow runner |

---

## Key Decisions

- **State-based processing.** Each stage of the pipeline reads the previous stage's output from a shared state layer. This makes every step independently testable, debuggable, and resumable without rerunning the full pipeline from scratch.
- **Dynamic generation over templates.** Rather than filling slots in a static proposal template, the AI drafts all content from the project brief and profile data. Output is tailored to each client — not a dressed-up placeholder.
- **Decoupled delivery.** The email dispatch, CRM update, and document export are independent steps triggered by a status change — not chained inline. Any step can fail and retry without affecting the others.

---

## Metrics

| Metric | Value |
|---|---|
| Full proposal generated | Under 10 minutes |
| Manual writing or formatting | Zero |
| CRM update | Automatic at every stage |
| Output consistency | Identical quality across every client |

---

## Status

**Production** — Active on every inbound client brief.
