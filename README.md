# Spec Team Toolkit

Two skills for the spec team's document workflow, bundled into one plugin.

## Skills

### `hld-builder`
Builds the High Level Design — the customer-facing scoping document that goes to product customers for approval.

- Built incrementally across sessions from two durable artifacts — `scope-list.md` (entities, personas, journeys, adjacent systems) and `hld-draft.md` (the working document, with per-section status tags and a change-tracking table) — that the user re-uploads to resume where they left off.
- Runs discovery from a fixed question script (`references/discovery_questions.md`), not improvised questions, so every analyst gets the same process; conditional sections are only asked about when the signal for them appears.
- Drafts into the team's real HLD template (`references/hld_template_structure.md`, exact Hebrew headers) following the status-tag and change-log conventions in `references/draft_conventions.md`.
- On finalize (only when asked), renders the draft as a Word document and self-reviews it against the full 10-part QA checklist (bundled in `references/hld_qa_review.md`), fixing Critical/High issues before handing it over.

### `lld-figma-spec`
Builds the Low Level Design — the developer/QA-facing component spec derived from a Figma design.

- Pulls real data from Figma via connected Figma MCP tools (design context, screenshots, variable definitions) rather than asking the user to describe the design by hand.
- Produces the team's existing two-part format: a content-entry table (Umbraco 13 editor types, API-sourced fields excluded) and a display/behavior table (logic, edge cases, responsiveness, accessibility), following the exact rules in `references/lld_instructions.md`.

## Notes

- `scope-list.md` and `hld-draft.md` produced by `hld-builder` are meant to be downloaded and re-uploaded at the start of the next session, since the HLD is built across conversations rather than in one sitting.
- Neither skill has been run through formal test evaluations yet — try each on a real project before rolling out broadly.
