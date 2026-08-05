# DuckDive rebase platform baseline

Established: 2026-08-05 (Australia/Perth)

## Decision

Use commit `08a9bd6` as the code baseline for a different approach to the multi-dataset challenge. The local branch is `codex/rebase-platform-baseline`.

This is a design and development baseline, not a production rollback or deployment candidate. `main` remains at `bab28df`, and the Phase 2C-D D1 candidate remains preserved on `codex/phase-2cd-d1-review` at `76e23d6`.

## Why this cut

`08a9bd6` is the narrowest point that retains the useful product and governance kernel:

- the released VIC Housing estate and analytics contract
- authenticated, owner-scoped workspaces and Dives
- question-led starter selection with explicit manual Apply
- editor version, reset, revert, embed, and unlisted-share controls
- browser-local semantic-model inspection and private reviewed evidence
- deterministic activation preview
- owner-scoped operational dataset registration with runtime bindings kept separate

Moving forward from this point does not inherit the later WHO-specific runtime design. Compared with `bab28df`, the baseline excludes 772 added lines across 24 changed files, including runtime routes, migrations 017 and 018, MotherDuck operational adapters, the WHO query policy, runtime lifecycle scripts, and their tests. It also excludes the D1 recipe and agent-context candidate.

The operational registry is retained because it is neutral: it records that an owner accepted reviewed evidence without choosing how that dataset must be queried, rendered, provisioned, or exposed.

## Product truth at the baseline

The baseline supports a governed single-dataset product and a safe review-to-registration path. It does not provide a visible second dataset.

| Capability | Baseline state |
|---|---|
| VIC Housing question, starter, editor, embed, and share lifecycle | Retained |
| Semantic-model evidence review and private draft persistence | Retained |
| Deterministic activation preview and operational registration | Retained |
| Runtime resource binding or dataset-routed query execution | Not present |
| WHO-specific contracts, identities, routes, or policies | Not present |
| Trusted WHO recipe, deterministic WHO source, or WHO Dive | Not present |
| Multi-dataset selector or owner-visible second dataset | Not present |

## Hard constraints retained

- Browser traffic stays behind authenticated and owner-scoped Next.js routes.
- Reviewed evidence remains separate from executable connectivity and runtime authority.
- Raw semantic archives, source addresses, credentials, unrestricted SQL, and exact security filters do not enter persisted contracts.
- Workspace and Dive ownership fail closed.
- VIC remains isolated from unrelated datasets and workloads.
- Questions do not start an agent run without explicit owner action.
- Production, database, MotherDuck, sharing, token, and deployment mutations require explicit approval and fresh evidence.

Everything else is open to redesign. The new direction does not need to preserve the WHO adapter, the Phase 2C-C route shape, the D1 recipe contract, or the earlier phase sequence.

## How to approach the challenge differently

The next design starts with one owner-visible outcome, not another infrastructure layer:

> An owner selects one reviewed dataset, asks one supported question, and receives one governed result or Dive that can be inspected, retried, and removed without reaching VIC or exposing connectivity.

Before implementation, define that journey in a short product brief containing:

1. the intended owner and dataset
2. the exact first question and expected visible result
3. the minimum runtime and rendering capability needed for that result
4. the ownership, isolation, refusal, and cleanup behavior
5. the single browser walkthrough that proves the slice is useful

Choose platform abstractions only after the journey proves they are required. Prefer an existing provider or configuration seam, then a small local adapter, before introducing new schema or orchestration.

## Delivery shape from this baseline

Use vertical, owner-reviewable slices:

1. **Product brief**: agree on the first visible outcome and its evaluation walkthrough. No code or external mutation.
2. **Local proof**: render the expected result from deterministic fixtures through the smallest interface. No production wiring.
3. **Governed integration**: add only the runtime boundary needed by that proof, with denial and cleanup tests.
4. **Owner evaluation**: expose the result behind an explicit action and verify it in the browser.
5. **Release decision**: only then decide whether to retain, generalize, or remove the approach.

Each slice must end with something the owner can evaluate. A slice that only creates another internal contract is incomplete unless it directly unlocks the next visible proof.

## Operational cautions

- Production has already received additive migrations 016 through 018. Do not attempt to roll back or delete those schema objects merely because this code baseline predates migrations 017 and 018; unused additive schema may remain dormant.
- A read-only walkthrough on 2026-08-05 found `/datasets/new` and `/admin` rendering but the production homepage failing with Server Components digest `4116751761`. This baseline does not diagnose or repair that drift and must not be deployed as an assumed fix.
- Historical production evidence for later commits remains valid evidence about what was tested then, but it does not change the selected code baseline or prove current health.
- Do not merge, push, deploy, migrate, provision, issue tokens, or create Dives from this branch until a new direction and release gate are approved.

## Baseline acceptance

The cut is acceptable when:

- `codex/rebase-platform-baseline` descends from `08a9bd6`
- `main` remains at `bab28df`
- `codex/phase-2cd-d1-review` remains at `76e23d6`
- tests, lint, TypeScript, and the production build pass on the baseline branch
- WHO runtime routes, policies, migrations 017 and 018, and D1 recipe/context files are absent
- the worktree is clean and the branch is local-only

The next authorized activity is design of the first owner-visible vertical slice. No implementation direction has yet been selected.
