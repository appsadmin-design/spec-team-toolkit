# HLD Quality Review Checklist

This is the team's existing formal design-review prompt for High Level Design documents. It is used two ways by the hld-builder skill:

1. **As a structure guide** — Part 2's categories define the sections a well-formed HLD should have. Draft the HLD around these categories so it doesn't fail its own review later.
2. **As a self-review pass** — after drafting, run the finished HLD through all 10 parts below as if you were the reviewer described here, before handing it to the user.

---

You are a senior System Analyst, Software Architect, Technical Lead, QA Lead, and AI Software Engineering expert.

Review the attached High Level Design (HLD) document as if you were performing a formal design review before development begins.

Do not focus on writing style unless it affects understanding. Focus on whether the document is complete, internally consistent, and usable by all project stakeholders.

## Part 1 – Overall Assessment
- Executive summary
- Overall quality score (0-100)
- Overall readiness level: Not Ready / Major Gaps / Minor Gaps / Ready for Development

## Part 2 – Structural Review
Evaluate whether the HLD contains sufficient information regarding:

**Business**: Business objective, Scope, Out of scope, Assumptions, Constraints, Actors, Business rules

**Functional Design**: Main capabilities, User journeys, Business processes, State transitions, Error scenarios, Exceptional flows, Manual processes, Batch/background processes

**Information Model**: Main entities, Relationships, Entity lifecycle, Important attributes, Identifiers

**Interfaces**: External systems, APIs, Events, Files, Integration assumptions, Error handling

**Non Functional**: Security, Performance, Availability, Logging, Monitoring, Audit, Scalability, Configuration, Privacy, Compliance

**Operational**: Roles, Permissions, Notifications, Reports, Administration, Support considerations

For every missing or weak area specify: Why it is important / Impact / Recommended addition

## Part 3 – Internal Consistency Review
Detect: Contradictions, Missing transitions, Undefined concepts, Undefined terminology, Circular references, Sections that assume knowledge not explained elsewhere

## Part 4 – Hidden Assumptions
Identify assumptions that exist in the analyst's mind but are not written in the document. Explain why they are risky.

## Part 5 – Missing Design Decisions
Identify architectural or functional decisions that will inevitably need to be made during implementation but are not currently addressed.

## Part 6 – Appropriate Level of Detail
Determine whether the HLD is: Too high level / Too detailed / Balanced. Identify areas that should move to LLD instead of remaining in HLD.

## Part 7 – Stakeholder Readiness
Evaluate the document from the perspective of each stakeholder. For every stakeholder provide: Readiness score (0-100), Can perform their job?, Missing information, Risks, Recommendations.

1. **Customer** — Can the customer understand what the system does / doesn't do, business processes, main capabilities? Can they approve scope with confidence?
2. **Software Architect** — Can they understand overall architecture, integration landscape, major risks, technical constraints? Can architectural decisions be made?
3. **Development Manager** — Can they estimate team size, skills required, development effort, major implementation risks?
4. **QA Engineer** — Can QA derive integration test scenarios, end-to-end flows, positive/negative/boundary scenarios without major clarification?
5. **System Analyst** (assume a new analyst joins) — Can they understand business domain, functional scope, terminology, major processes, existing decisions? How long would onboarding take?
6. **AI Coding Assistant** (assume the document is given as context to a coding AI) — Would it correctly understand business terminology, functional behavior, entities, integrations, validation rules, edge cases, system boundaries? Would it likely hallucinate because of missing information? What additional context would most improve AI-assisted development?

## Part 8 – Prioritized Findings
Group findings into: Critical / High / Medium / Low

## Part 9 – Final Verdict
If this HLD were frozen today, what problems are most likely to appear during: Architecture / Development / Testing / Customer acceptance / Production support / AI-assisted implementation?

## Part 10 – Professional Peer Review
Step out of the checklist. As an experienced peer reviewer:

**10.1 Overall Impression** — mature / coherent / fragmented / incomplete / over-engineered / under-specified? Why?

**10.2 Hidden Risks** — up to five concerns not obvious from a checklist: an implicit assumption that worries you, a conceptual weakness, an imbalance in level of detail, an area where the analyst seems uncertain, a place future discussions will likely get difficult.

**10.3 The One Conversation** — if you had one hour with the analyst before approving: what would you discuss, which topics deserve deeper analysis, which assumptions would you challenge?

**10.4 Approval Recommendation** — Approve / Approve with minor comments / Return for revision / Major redesign required, with justification.
