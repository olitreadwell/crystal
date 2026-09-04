# crystal-lang/crystal context
> refreshed 2026-09-04 | upstream default: master @ ab61e7031d8747fa3a07b2e8bd16fa8e3b40e0b6

## Identity & policies
- upstream: crystal-lang/crystal, default branch `master`, primary language Crystal (+ compiler shell/C), English-first: yes.
- CLA/DCO: none detected (no CLA workflow, no contributor-signup / CLA ask in CONTRIBUTING).
- AI-assisted PR policy: unstated (no AI ban/disclosure mention in CONTRIBUTING, .github, README).
- signed commits required: no signal of required signatures.
- PR template: `.github/PULL_REQUEST_TEMPLATE/pull_request_template.md` (short guidance list, not checkbox-heavy).
- external tracker: github.

## Conventions (verified from merged PRs)
- branch naming: dominant `fix/<kebab>`, also `refactor/…`, `spec/…`, `infra/…`, `bug/…`, `perf/…`.
- commit style: imperative/Conventional-ish — `Fix: …`, `Fix …`, `Optimize …`, `Update …` (+ CI uses `CI: …`). No emoji prefixes.
- test/lint: `make spec`, `make std_spec`, `ameba` lint, `typos` spell check (whole repo, `crate-ci/typos` v1.50 in linux.yml).
- man pages are generated at build time from hand-maintained `doc/man/*.adoc` (`Makefile` -> `man/%.1`); edit the `.adoc` source.
- how outside PRs land: active core team, steady flow of merged external PRs; CI gates merge.

## Maintainer picture
- multiple active core-team members; steady commit cadence (many commits/day, see git log).
- heavily CI-driven; typos spell-check job means whole-repo spelling is already guarded.

## Issue-area health
- Large, well-organised issue tracker (community:* labels). Not needed for this trivial-fix pass.

## Gap ledger (dedupe — READ FIRST, never re-pick)
(none yet)

## Mined gaps (discovered, not yet attempted)
- duplicated-word typos in hand-written docs/comments (not caught by the `typos` spell-checker, which does not flag repeated valid words):
  - `doc/man/crystal.adoc` + `doc/man/crystal-init.adoc`: "Create a a new Crystal project"
  - `doc/changelogs/v1.16.md`: "`#wait_writable` methods methods"
  - `src/io/file_descriptor.cr` doc comment: "even when when it feels redundant"
  - `scripts/generate_glob_specs.sh` + generated `spec/std/file/match-fast-glob_spec.cr`: "They are are  collection" + stale header ref `scripts/generate_glob_specs.cr` (actual file is `.sh`)
