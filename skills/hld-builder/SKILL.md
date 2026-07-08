---
name: hld-builder
description: Use this skill to write, continue, update, or review a High Level Design (HLD) document that goes to customers for approval — phrases like "write an HLD", "let's scope this project", "continue the HLD for X", "review this HLD", or any conversation about entities, personas, journeys, or adjacent systems for a new project, even without the word "HLD". The HLD is built incrementally across sessions, not in one sitting — trigger this whenever an existing scope-list.md or hld-draft.md is uploaded to resume work. Also trigger for auditing an existing HLD against the team's quality checklist. Uses a fixed, non-improvised question script so the process is identical across analysts.
---

# HLD Builder

## What this skill does

Guides production of a High Level Design (HLD) — the customer-facing scoping document that gets approved before development starts — across as many sessions as it takes. It is built from three durable artifacts that carry state between sessions:

- **`scope-list.md`** — the running inventory of entities, personas, processes, and adjacent systems
- **`hld-draft.md`** — the working document itself, with a per-section status tag and a change-tracking table (same convention this team already uses in real HLDs)
- **`references/hld_qa_review.md`** — the team's formal QA checklist, applied as a self-review pass only when the draft is asked to be finalized for delivery

Two things matter most in how this skill behaves, because they were explicit requirements from the team:

1. **The discovery questions are fixed, not improvised.** Every analyst should get the same process. Use `references/discovery_questions.md` verbatim — ask the questions as written, don't invent new ones or skip ones that apply.
2. **The document is written incrementally.** Not all information exists on day one, and things change later. The workflow below is built around resuming, updating, and tracking change over time — not a single one-shot generation.

## Session start protocol (run this every time, first)

1. Check whether the user has provided/uploaded an existing `scope-list.md` and/or `hld-draft.md`.
2. **If they exist:** load them. Read `references/draft_conventions.md` for how to interpret the status tags and change log. Summarize for the user in one short message: which sections are done, which are partial or waiting on information, and which contain unvalidated assumptions. Then ask what they want to do this session (finish an open section, update something that changed, add a newly-discovered scope item) — don't just restart discovery from the top.
3. **If they don't exist:** this is a new project. Create both files fresh as the conversation develops. Start discovery from `references/discovery_questions.md`, section 1.
4. **Never re-ask a question that's already answered** in the existing files unless the user indicates something changed.

## Phase 1 — Discovery (scope list + fixed questions)

Maintain `scope-list.md` with four sections: Entities, Personas/user types, Processes, Adjacent systems. Update it immediately whenever something new surfaces or something is dropped from scope — don't batch updates to the end.

Ask discovery questions strictly from `references/discovery_questions.md`. Its signal table (built into `references/hld_template_structure.md`) determines which conditional sections apply — whether there are human end-users, whether the system owns its own data entities, whether there's a backoffice/reporting need, whether it's mostly a service-to-service integration. Only ask the conditional-section questions once the signal for that section is actually present.

If the user doesn't have an answer yet: don't push. Mark it per `references/draft_conventions.md` (`[סטטוס: ממתין למידע]` or a `❓ פתוח:` note inline) and move on. This is expected, not an error state.

## Phase 2 — Write into the working draft as you go

Read `references/hld_template_structure.md` for the real section structure and exact Hebrew headers this team uses (not a generic Business/Functional/Information-Model template). As each section gets enough information, write or update it directly in `hld-draft.md`, following `references/draft_conventions.md`:

- Tag the section's current status
- Add a row to the change-tracking table for every update, however small
- If an update to one section could affect an already-drafted one (e.g. a new adjacent system changes a process that references it), flag the affected section back to `[סטטוס: טיוטה חלקית]` with a `❓ פתוח:` note explaining what needs re-checking

The "תהליכים עסקיים במבט על" section should be narrative prose per process (one subheading per process, describing rules and edge cases), not a table — that's how this team actually writes it.

At the end of each session, make sure `hld-draft.md` and `scope-list.md` reflect everything discussed, and remind the user to keep both for next time (they can re-upload them to resume).

## Phase 3 — Self-review before delivery (only when asked to finalize)

This is not run automatically at the end of every session — only when the user says the document (or a specific section) is ready to move toward customer delivery. Running a full QA pass on a deliberately partial draft isn't useful and will just produce noise.

When triggered: render `hld-draft.md` into a Word document via the docx skill, using only sections marked `הושלם`. If sections aren't complete, say so explicitly and confirm whether to proceed anyway (e.g. for an internal interim review) before generating.

Then apply the full checklist in `references/hld_qa_review.md` — all 10 parts — to that Word draft, as an internal step. Part 2's categories are a coverage lens, not literal headers to match onto the Hebrew structure. Fix Critical/High issues yourself; flag Medium/Low items and genuine judgment calls (e.g. "should this stay in the HLD or move to the LLD?") to the user instead of silently deciding. The deliverable is the improved Word document — don't dump the raw 10-part review on the user unless they ask for it or explicitly requested a review rather than a draft.

## Output

- `hld-draft.md` — the persistent working file, offered as a download at the end of every session so the user can resume next time
- `scope-list.md` — the persistent scope inventory, same reason
- The customer-facing Word document — generated on request when the draft (or a session's worth of it) is ready to move toward delivery
