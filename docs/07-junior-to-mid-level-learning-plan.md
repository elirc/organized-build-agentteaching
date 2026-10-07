# Junior-To-Mid-Level Learning Plan

> This repository is a snapshot of [elirc/3buildagentteaching](https://github.com/elirc/3buildagentteaching) taken right after its onboarding docs were added and before its 20-story backlog was merged. The 14-day plan below still works as a reading path, but several
> exercises in the later sections describe things that already exist in this
> code. Those now say so and point at the existing version, because reading
> and extending real code teaches more than rebuilding it.

## 14-Day Study Plan

Day 1: Read the README and architecture overview. Run the app and seed data.

Day 2: Read `schema.prisma`. Draw the entity relationship map.

Day 3: Read `seed.ts`. Explain the Maya scenario in your own words.

Day 4: Study `grades.ts`, `attendance.ts`, and `risk.ts`. Run tests.

Day 5: Modify one grade rule and update tests.

Day 6: Trace enrollment from UI to `decideEnrollment`.

Day 7: Add one validation test and one domain edge-case test.

Day 8: Study `agents/src/types.ts` and `registry.ts`.

Day 9: Run every agent from the UI and inspect `/agent-runs/[id]`.

Day 10: Add a small field to an agent trace and test it.

Day 11: Debug a failed job using `/jobs`, `/logs`, and `/audit-events`.

Day 12: Add a new dashboard card using existing domain logic.

Day 13: Review server actions and list where audit events are written.

Day 14: Present the architecture, risks, and extension plan as if in an interview.

## Small Code Modification Tasks

- Add a new enrollment status filter.
- Add a missing-work column to gradebook.
- Add a new structured log seed event.
- Add one more support note visibility rule test.
- Add a teacher workload threshold test.

## Debugging Exercises

- Why did a job dead-letter?
- Why is Maya high risk?
- Why did a section waitlist a student?
- Why did a submission score fail validation?
- Why did agent confidence drop?

## Agent Extension Exercises

- ~~Add a Guardian Communication Draft Agent~~ - already exists
  (`packages/agents/src/guardian-communication-agent.ts`). Instead: read it
  and list every input field it uses.
- Add a Lesson Plan Review Agent with deterministic rubric matching - still
  the best open exercise; `docs/06-extension-projects.md` says what to copy
  and gives the **Check** for done.
- Add agent golden-output tests - still open. `packages/agents/src/agents.test.ts`
  has 8 cases and no fixture files.
- Add an approval flag before creating interventions - read the existing
  `InterventionApproval` model and `packages/domain/src/approvals.ts` first,
  then decide what "before creating" should add.

## Architecture Review Exercises

- Identify logic that should stay out of React.
- Identify where RBAC is too light - start from `assertCan`
  (`packages/application/src/context.ts:6`) and find the paths that skip it.
- Propose a background worker - a lock-based `worker-service.ts` exists in
  `packages/application/src/services/`. Instead: propose how to move it into
  its own process, since `apps/` holds only `web`.
- Propose multi-tenant school support - still open, and still the best
  design exercise here.

## Data Modeling Exercises

- ~~Add terms/academic years~~ - `AcademicTerm` and `GradingPeriod` models
  exist, with a `/terms` page. Instead: trace how a section relates to its term.
- ~~Add rubrics~~ - `Rubric`, `RubricCriterion` and `SubmissionCriterionScore`
  exist. Instead: add one rubric edge-case test (all criteria unscored).
- ~~Add guardian-to-student relationships~~ - `Guardian` and `StudentGuardian`
  exist. Instead: find every query that reads them.
- Add many schools or districts - still open.
- ~~Add notification delivery records~~ - `Notification` has `channel`,
  `status` and `readAt`. Instead: find which code paths create one.

## Interview Talking Points

- Modular monolith boundaries
- Domain logic independent of UI
- Deterministic mock agents as safe learning tools
- Persisted agent traceability
- Audit logs and operational debugging
- Tradeoffs of simulated auth
- How to evolve toward stronger RBAC and background workers
