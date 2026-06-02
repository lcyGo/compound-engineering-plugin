# Concepts

Shared domain vocabulary for this project — entities, named processes, and status concepts with project-specific meaning. Accretes as ce-compound and ce-compound-refresh process learnings; direct edits are fine. Glossary only, not a spec or catch-all.

## Beta skill

A parallel copy of a stable skill, suffixed `-beta`, used to trial a new version alongside the stable one without disrupting users.

A beta skill is invoked manually (model auto-invocation is disabled) and carries a `[BETA]` description prefix; promotion to stable removes the suffix, the prefix, and the manual-only restriction. Promotion is an orchestration change, not just a file rename — every caller that invokes the skill must be updated in the same change so it does not silently inherit stale defaults.

## Confidence anchor

A self-scored confidence value drawn from a fixed five-point scale (`0`, `25`, `50`, `75`, `100`) rather than a continuous float, with each anchor tied to a behavioral criterion the model can honestly self-apply.

Used by the review skills to gate and sort findings; a skill's actionable threshold is itself expressed as an anchor (document review surfaces at `>= 50`, code review at `>= 75`). Corroboration across reviewers promotes a finding one anchor step rather than by a fractional boost.

## Autofix class

The classification of a review finding by how safely its proposed fix can be applied. Four values:

- *safe_auto* — one clearly-correct fix, applied silently.
- *gated_auto* — fix is probably correct but warrants confirmation before applying (e.g. it touches an external reference or crosses surfaces).
- *manual* — resolution needs human judgment; no fix is auto-applied.
- *advisory* — an observation with no required action.
