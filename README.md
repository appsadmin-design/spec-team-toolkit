# Spec Team Toolkit

Two skills for the spec team's document workflow, bundled into one plugin.

## Skills

### `hld-builder`
Builds the High Level Design — the customer-facing scoping document that goes to product customers for approval.

- Maintains a living `scope-list.md` (entities, personas, journeys, adjacent systems) that evolves through discovery instead of being fixed upfront.
- Interviews around the same categories a formal HLD review checks for (Business, Functional Design, Information Model, Interfaces, Non-Functional, Operational), so the draft doesn't fail its own review later.
- Drafts the HLD as a Word document, then self-reviews the draft against the full 10-part QA checklist (bundled in `references/hld_qa_review.md`) and fixes Critical/High issues before handing it over.

### `lld-figma-spec`
Builds the Low Level Design — the developer/QA-facing component spec derived from a Figma design.

- Pulls real data from Figma via connected Figma MCP tools (design context, screenshots, variable definitions) rather than asking the user to describe the design by hand.
- Produces the team's existing two-part format: a content-entry table (Umbraco 13 editor types, API-sourced fields excluded) and a display/behavior table (logic, edge cases, responsiveness, accessibility), following the exact rules in `references/lld_instructions.md`.

## Notes

- `scope-list.md` produced by `hld-builder` is meant to be downloaded and re-uploaded at the start of the next discovery session, since scope discovery is meant to carry across conversations.
- Neither skill has been run through formal test evaluations yet — try each on a real project before rolling out broadly.
