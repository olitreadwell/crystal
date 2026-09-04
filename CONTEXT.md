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
- `2026-09-04` self-found duplicated-word/typo pack (6 files) — outcome: pr-opened https://github.com/olitreadwell/crystal/pull/1 — lesson: `typos` CI does NOT flag duplicated words, so fixing the man pages "a a", changelog/comment `methods methods` / `when when`, and the fast-glob generator's `are are` + stale `.cr`→`.sh` ref was safe and CI-neutral.
- `2026-09-04` #13466 (open, kind:docs) — API docs render `Dir.mkdir`/`mkdir_p` default mode as decimal `511` instead of `0o777`. Root cause: lexer normalizes non-decimal literals to decimal (`src/compiler/crystal/syntax/lexer.cr`), so the docs generator (`src/compiler/crystal/tools/doc/method.cr`) prints `511`. Maintainer straight-shoota suggested using `File::Permissions::All`. Fix: default `mode : Int32 = File::Permissions::All.to_i32` in `Dir.mkdir`/`mkdir_p` + `FileUtils.mkdir`/`mkdir_p` (4 overloads), docs now render `File::Permissions::All.to_i32`. Verified: `crystal tool format --check` clean, stdlib type-checks via `crystal build --no-codegen`, `crystal docs` renders `File::Permissions::All.to_i32` (no `511`). Could not run `make std_spec` (no cc/linker in env). — outcome: pr-opened

## Mined gaps (discovered, not yet attempted)
- `2026-09-04` docs-generator root cause: lexer converts octal/hex/binary literals to decimal, so ANY stdlib default arg written as `0o777`/`0xFF` renders as decimal in API docs (not just Dir.mkdir). A compiler-level fix (preserve original literal for docs) would fix all such cases, but needs a full compiler build to verify (no cc in env). — status: proposed
- duplicated-word typos in hand-written docs/comments (not caught by the `typos` spell-checker, which does not flag repeated valid words):
  - `doc/man/crystal.adoc` + `doc/man/crystal-init.adoc`: "Create a a new Crystal project"
  - `doc/changelogs/v1.16.md`: "`#wait_writable` methods methods"
  - `src/io/file_descriptor.cr` doc comment: "even when when it feels redundant"
  - `scripts/generate_glob_specs.sh` + generated `spec/std/file/match-fast-glob_spec.cr`: "They are are  collection" + stale header ref `scripts/generate_glob_specs.cr` (actual file is `.sh`)
