# Arcleo scopes and stages

Generated tables, kept beside the skill as human-readable data: the engine routes from the compiled scope grid and stage graph, never from these.

## Scope-to-Stage Mapping

The orchestration engine resolves scope-level stage routing internally (it reads the compiled scope grid the table below summarises). The summary table is kept here as human-readable data - not dispatch logic - and is regenerated, never hand-edited. (One carve-out: `scope save` adds a plan the human chose to keep to the runtime scope registry (the durable `arcleo/scopes/<name>.md` record, projected into `.claude/scopes/arcleo-<name>.md` and a `scope-grid.json` entry) - that is the sanctioned write path for saved scopes, not a hand-edit; this summary table itself stays generated.)

Source of truth: one file per scope under `.claude/scopes/arcleo-<name>.md` (identity + keywords + description + skeleton default) plus each stage's `scopes:` frontmatter (membership), transposed into the compiled grid at `arcleo engine graph compile`. Adding a scope is the same muscle memory as authoring a sensor or agent — drop `.claude/scopes/arcleo-<name>.md`, tag the member stages' `scopes:` lists, recompile, then `arcleo engine gen scope-table` to regenerate the table below + commit. No prose edit required. CI runs `scope-table --check` to prevent drift.

<!-- BEGIN: compiled scope grid via `arcleo engine gen scope-table` - do NOT hand-edit -->

| Scope          | Depth         | TestStrategy | EXECUTE / Total |
|----------------|---------------|--------------|-----------------|
| bugfix         | Minimal       | (default)    | 9 / 33          |
| classic        | Standard      | (default)    | 18 / 33         |
| enterprise     | Comprehensive | (default)    | 33 / 33         |
| express        | Minimal       | (default)    | 10 / 33         |
| feature        | Standard      | (default)    | 33 / 33         |
| infra          | Standard      | (default)    | 13 / 33         |
| mvp            | Standard      | (default)    | 23 / 33         |
| poc            | Minimal       | (default)    | 8 / 33          |
| refactor       | Minimal       | (default)    | 10 / 33         |
| security-patch | Minimal       | (default)    | 10 / 33         |
| workshop       | Standard      | Minimal      | 26 / 33         |

<!-- END: compiled scope grid -->

---

## Stage Graph

The engine reads the compiled `data/stage-graph.json` directly for all routing; this table is the human-readable mirror of that graph (each compiled stage, its phase, execution mode, lead/support agents, and run mode) — data, not dispatch logic.

<!-- BEGIN: compiled stage graph via `arcleo engine gen stage-table` - do NOT hand-edit -->

| Slug | # | Stage | Phase | Execution | Lead Agent | Support Agents | Mode |
|------|---|-------|-------|-----------|------------|----------------|------|
| workspace-scaffold | 0.1 | Workspace Scaffold | Initialization | ALWAYS | (orchestrator) | — | inline |
| workspace-detection | 0.2 | Workspace Detection | Initialization | ALWAYS | (orchestrator) | — | inline |
| state-init | 0.3 | State Initialization | Initialization | ALWAYS | (orchestrator) | — | inline |
| intent-capture | 1.1 | Intent Capture & Framing | Ideation | ALWAYS | arcleo-product-agent | arcleo-architect-agent | inline |
| market-research | 1.2 | Market Research | Ideation | CONDITIONAL | arcleo-product-agent | — | inline |
| feasibility | 1.3 | Feasibility & Constraints | Ideation | CONDITIONAL | arcleo-architect-agent | arcleo-aws-platform-agent, arcleo-compliance-agent | inline |
| scope-definition | 1.4 | Scope Definition | Ideation | ALWAYS | arcleo-product-agent | arcleo-delivery-agent | inline |
| team-formation | 1.5 | Team Formation | Ideation | CONDITIONAL | arcleo-delivery-agent | — | inline |
| rough-mockups | 1.6 | Rough Mockups | Ideation | CONDITIONAL | arcleo-design-agent | arcleo-product-agent | inline |
| approval-handoff | 1.7 | Approval & Handoff | Ideation | ALWAYS | arcleo-delivery-agent | arcleo-product-agent | inline |
| reverse-engineering | 2.1 | Reverse Engineering | Inception | CONDITIONAL | arcleo-developer-agent | arcleo-architect-agent | pipeline |
| practices-discovery | 2.2 | Practices Discovery | Inception | CONDITIONAL | arcleo-pipeline-deploy-agent | arcleo-quality-agent, arcleo-developer-agent, arcleo-devsecops-agent | subagent |
| requirements-analysis | 2.3 | Requirements Analysis | Inception | ALWAYS | arcleo-product-agent | — | inline |
| user-stories | 2.4 | User Stories | Inception | CONDITIONAL | arcleo-product-agent | arcleo-design-agent, arcleo-developer-agent, arcleo-quality-agent | mob |
| refined-mockups | 2.5 | Refined Mockups | Inception | CONDITIONAL | arcleo-design-agent | arcleo-product-agent | inline |
| domain-design | 2.6 | Domain Design | Inception | CONDITIONAL | arcleo-architect-agent | arcleo-aws-platform-agent, arcleo-design-agent | inline |
| units-generation | 2.7 | Units Generation | Inception | ALWAYS | arcleo-architect-agent | arcleo-delivery-agent | inline |
| contract-design | 2.8 | Contract Design | Inception | CONDITIONAL | arcleo-architect-agent | arcleo-aws-platform-agent | inline |
| delivery-planning | 2.9 | Delivery Planning | Inception | ALWAYS | arcleo-delivery-agent | arcleo-architect-agent | inline |
| functional-design | 3.1 | Functional Design | Construction | CONDITIONAL | arcleo-architect-agent | arcleo-developer-agent | inline |
| nfr-requirements | 3.2 | NFR Requirements | Construction | CONDITIONAL | arcleo-architect-agent | arcleo-devsecops-agent, arcleo-compliance-agent, arcleo-quality-agent | inline |
| nfr-design | 3.3 | NFR Design | Construction | CONDITIONAL | arcleo-architect-agent | arcleo-aws-platform-agent | inline |
| infrastructure-design | 3.4 | Infrastructure Design | Construction | CONDITIONAL | arcleo-aws-platform-agent | arcleo-devsecops-agent, arcleo-compliance-agent | inline |
| code-generation | 3.5 | Code Generation | Construction | ALWAYS | arcleo-developer-agent | — | subagent |
| build-and-test | 3.6 | Build and Test | Construction | ALWAYS | arcleo-quality-agent | arcleo-devsecops-agent | inline |
| ci-pipeline | 3.7 | CI Pipeline | Construction | CONDITIONAL | arcleo-pipeline-deploy-agent | — | inline |
| deployment-pipeline | 4.1 | Deployment Pipeline | Operation | CONDITIONAL | arcleo-pipeline-deploy-agent | — | inline |
| environment-provisioning | 4.2 | Environment Provisioning | Operation | CONDITIONAL | arcleo-aws-platform-agent | arcleo-devsecops-agent, arcleo-compliance-agent | inline |
| deployment-execution | 4.3 | Deployment Execution | Operation | CONDITIONAL | arcleo-pipeline-deploy-agent | arcleo-developer-agent | inline |
| observability-setup | 4.4 | Observability Setup | Operation | CONDITIONAL | arcleo-operations-agent | — | inline |
| incident-response | 4.5 | Incident Response | Operation | CONDITIONAL | arcleo-operations-agent | — | inline |
| performance-validation | 4.6 | Performance Validation | Operation | CONDITIONAL | arcleo-quality-agent | — | inline |
| feedback-optimization | 4.7 | Feedback & Optimization | Operation | CONDITIONAL | arcleo-operations-agent | arcleo-aws-platform-agent | inline |

<!-- END: compiled stage graph -->
