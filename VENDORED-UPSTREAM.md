# VENDORED UPSTREAM — not Asolaria code

**This repository is a mirror of a third-party project.**

| | |
|---|---|
| upstream | https://github.com/chopratejas/headroom |
| licence | Apache-2.0 (retained unchanged) |
| authors | "Headroom Maintainers" |
| this copy | a snapshot, one commit: `chore: release main (#1574)` by `github-actions[bot]` |

## Scope of the operator toolchain rule

The operator standard — **Rust 1.81 with clippy, integer/ternary arithmetic only, never float** —
governs **Asolaria code**: the substrate that runs trits, addresses, and replays. It does **not**
govern vendored upstream code.

Measured 2026-08-06 before that decision was made:

- **No Asolaria code is present here.** Zero files reference asolaria, prism, trit, rime, hbp,
  behcs, or fischer.
- **Nothing in the corpus depends on this repository.** All 181 other repos were swept; every
  occurrence of the word "headroom" in them is the ordinary English usage
  ("emit-budget headroom", "4.3B headroom", "payload with headroom"). There are no imports,
  no path dependencies, no service references.
- Upstream already declares `edition = "2021"`, `resolver = "2"`, `rust-version = "1.80"` — its
  own choices, and not in conflict with the standard.
- 436 `f32`/`f64` sites exist in upstream compression internals. Converting them would create 436
  permanent merge conflicts against a project that is still shipping releases, and would change
  nothing that executes in Asolaria.

**Ruling: out of scope, deliberately, in writing.** Not drift — a declared boundary, in the same
spirit as the `FLOAT-WITNESS-EXEMPT` and `FLOAT-WIRE-BOUNDARY-EXEMPT` markers used in Asolaria
crates: the rule is absolute where it means something, and says so where it does not apply.

If Asolaria ever builds on this project, the integer/ternary layer belongs in a crate the operator
owns that calls into it — leaving upstream pristine and mergeable.

Operator: Jesse Daniel Brown. Declared 2026-08-06.
