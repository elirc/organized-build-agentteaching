# Extension Projects

Use these as future engineering exercises.

> **Status (2026-10-06):** This repository is a snapshot of [elirc/3buildagentteaching](https://github.com/elirc/3buildagentteaching) taken right after its onboarding docs were added and before its 20-story backlog was merged. This wishlist is older than the code in this
> snapshot: several items already exist here. Each item below is marked
> **[exists: ...]**, **partly** or **still open**, checked against this
> snapshot, so you extend what exists instead of rebuilding it. Paths are
> relative to the repo root; the schema is `packages/db/prisma/schema.prisma`.

## Agent Extensions

- Lesson plan review agent - still open
- Curriculum gap analysis agent - still open
- Guardian communication draft workflow - **[exists: `packages/agents/src/guardian-communication-agent.ts`]**
- Grading consistency analyzer - **[exists: `packages/agents/src/grading-consistency-agent.ts`]**
- Student success coach dashboard - partly: `packages/agents/src/student-success-review-agent.ts` exists, with no dedicated dashboard
- Privacy/security review agent - still open
- Agent orchestration dashboard - **[exists: `/agent-ops` lists manifests, recommendations and evaluations (`apps/web/app/agent-ops/page.tsx`, `packages/application/src/queries/agent-ops-query.ts`)]**
- Recursive system audit agent - still open
- Automatic test gap analyzer - still open
- Academic term postmortem agent - still open

## Workflow Extensions

- Intervention approval workflow - **[exists: `InterventionApproval` model, `canTransitionApproval` in `packages/domain/src/approvals.ts`, `/approvals` page]**
- Human approval queue for agent recommendations - **[exists: `AgentRecommendation` with `Proposed`/`Approved`/`Rejected`/`Completed` statuses and `approvedByUserId`, `/agent-recommendations` page]**
- Real-time attendance alerts - still open (`attendance-anomaly-agent.ts` exists, but nothing pushes alerts in real time)
- Notification system - partly: a `Notification` model with type, channel and status, and a `/notifications` page
- Guardian digest scheduling - still open (`GuardianDigest` is a `JobType` value only)
- Report generation jobs - still open (`ReportGeneration` is a `JobType` value; the worker only special-cases its timeouts)
- Teacher workload rebalance queue - still open (`teacher-workload-agent.ts` exists)

## Architecture Extensions

- Multi-tenant school/district support - still open (no school or district model)
- Stronger RBAC policies - partly: application services call `assertCan` (`packages/application/src/context.ts:6`)
- Route-level permission middleware - still open (there is no `middleware.ts`)
- Background worker process - partly: `packages/application/src/services/worker-service.ts` processes jobs with `WorkerLock` leases, but it runs inside the web app; `apps/` holds only `web`
- Feature flags - still open
- Import/export jobs - still open
- Data-quality dashboard - still open

## Testing Extensions

- Playwright smoke tests - still open
- Prisma integration tests with a test database - still open (the 28 Vitest cases in `packages/*/src/*.test.ts` need no database)
- Agent golden-output regression tests - still open (an `AgentEvaluation` model exists, but there are no fixture files)
- Accessibility checks - still open
- Load-test seed generation - still open

## Suggested First Extension

The old suggestion here (a Guardian Communication Draft Agent) already
exists in `packages/agents/src/guardian-communication-agent.ts`. The best
first extension in this snapshot is a **Lesson Plan Review Agent**. Copy the
shape of `grading-consistency-agent.ts` for deterministic rubric matching,
register it in `packages/agents/src/registry.ts`, and add tests next to
`packages/agents/src/agents.test.ts`.

**Check**: the agent runs from the app, running it twice on the same input
produces identical output, and `npm test` passes.
