---
name: hld-builder
description: Use this skill whenever the user wants to write, draft, discover, scope, or review a High Level Design (HLD) document for a product or system that will go to customers for approval — including phrases like "write an HLD", "let's scope this project", "help me figure out the scope for X", "create the HLD for customer approval", "review this HLD", "is this HLD ready for development", or any conversation about entities, personas, customer journeys, backoffice processes, or adjacent/integrated systems for a new project. Trigger this even if the user just starts describing a new project's business requirements without ever saying "HLD" — that discovery conversation is exactly what this skill is for. Also trigger for auditing an already-written HLD against a formal quality checklist. Produces a customer-facing Word document that has already been self-reviewed against the team's QA checklist before delivery.
---

# HLD Builder

## What this skill does

Guides a two-phase workflow for producing a High Level Design (HLD) — the customer-facing scoping document that gets approved before development starts:

1. **Discovery & scoping** — maintain a living Scope List and interview the user (the analyst) to fill in the business, functional, information, interface, non-functional, and operational picture.
2. **Draft + self-QA** — write the HLD as a Word document, then actually run it through the QA checklist in `references/hld_qa_review.md` against your own draft, fix what you find, and only then hand it over.

## Why the self-review step matters

An HLD written straight out of a first conversation is almost always missing things the analyst didn't think to mention out loud — out-of-scope boundaries, error flows, non-functional requirements, edge cases in a process. Catching these before the document reaches the customer is far cheaper than catching them after approval. So don't treat the self-review as a formality: work through it properly, the same way a reviewer would, and fix what it surfaces.

## Phase 1 — Scope List (source of truth)

Scope here isn't fixed at kickoff. It's discovered, and sometimes narrowed, as the discovery conversation goes on. Keep a running file called `scope-list.md` with four sections:

1. **Entities** — the data/business objects the system handles
2. **Personas / user types** — who uses the system, in what role
3. **Processes** — customer journeys and backoffice/internal processes
4. **Adjacent systems** — external or integrated systems

At the start of a session:
- Check whether the user has uploaded an existing `scope-list.md`. If so, treat it as the current state and keep extending it rather than starting over.
- If not, create one as the conversation develops.

Whenever the conversation surfaces a new entity, persona, process, or adjacent system — or the user says something is now out of scope — update the file right away rather than waiting until the end. This file is both the thing you draft the HLD from, and something the user should download and bring back next session, since a fresh conversation won't otherwise remember where scoping left off.

Before drafting, walk through the categories from Part 2 of `references/hld_qa_review.md` — Business, Functional Design, Information Model, Interfaces, Non-Functional, Operational — as an interview with the user, using the Scope List as the anchor. This is the fastest way to make sure the eventual document has what it needs before you ever get to the review step.

## Phase 2 — Draft the HLD

Read the docx skill's SKILL.md first, then produce a Word document. Structure it directly around the same categories the QA review checks for, so nothing falls through a structural gap:

- **Business** — objective, scope, out of scope, assumptions, constraints, actors, business rules
- **Functional Design** — capabilities, journeys, processes, state transitions, error/exceptional flows, manual & batch processes
- **Information Model** — entities, relationships, lifecycle, attributes, identifiers
- **Interfaces** — external systems, APIs, events, files, integration assumptions, error handling
- **Non-Functional** — security, performance, availability, logging, monitoring, audit, scalability, configuration, privacy, compliance
- **Operational** — roles, permissions, notifications, reports, administration, support

Write for the customer-facing audience this document is actually for: plain business language, minimal jargon, and a process diagram wherever a flow would be clearer drawn than described.

## Phase 3 — Self-review before delivery

Once a draft exists, apply the full checklist in `references/hld_qa_review.md` — all 10 parts, not only Part 2's structural check — to your own document, as an internal step.

Then:
- Fix anything Critical or High severity yourself before showing the document to the user.
- For Medium/Low items or genuine judgment calls (e.g. "should this stay in the HLD or move to the LLD?"), flag them to the user instead of silently deciding — these usually need the analyst's call.
- The deliverable is the improved Word document, not the raw review output. A short note on what you tightened up is enough — don't dump the full 10-part review on the user unless they ask for it or explicitly asked you to review (rather than write) a document.

## Output

- The HLD: a Word document (.docx)
- The living scope list: `scope-list.md`, offered as a download so the user can carry it into the next session
