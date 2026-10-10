# Domain Docs

How the engineering skills should consume this repo's domain documentation when exploring the codebase.

This repo is **single-context**: one `GLOSSARY.md` and one `docs/adr/` at the root. No monorepo
signals were found (no workspace file, no `packages/`), so there is no `GLOSSARY-MAP.md` and no
per-context layout.

## Before exploring, read these

- **`GLOSSARY.md`** at the repo root, or
- **`GLOSSARY-MAP.md`** at the repo root if it exists: it points at one `GLOSSARY.md` per context. Read each one relevant to the topic.
- **`docs/adr/`**: read ADRs that touch the area you're about to work in.

If any of these files don't exist, **proceed silently**. Don't flag their absence; don't suggest creating them upfront. The `/domain-modeling` skill (reached via `/grill-with-docs` and `/improve-codebase-architecture`) creates them lazily when terms or decisions actually get resolved.

Neither exists in this repo today. That is the expected state, not a gap to report.

## File structure

```
/
├── GLOSSARY.md          ← created lazily
├── docs/adr/            ← created lazily
└── src/
```

## Use the glossary's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal, a hypothesis, a test name), use the term as defined in `GLOSSARY.md`. Don't drift to synonyms the glossary explicitly avoids.

If the concept you need isn't in the glossary yet, that's a signal: either you're inventing language the project doesn't use (reconsider) or there's a real gap (note it for `/domain-modeling`).

Until a `GLOSSARY.md` exists, use the vocabulary the codebase and `docs/*.md` already establish —
repository, snapshot, backup plan, schedule, browse cache, indexed snapshot, master key, task event
bus, retention, prune, mirror.

## Flag ADR conflicts

If your output contradicts an existing ADR, surface it explicitly rather than silently overriding:

> _Contradicts ADR-0007 (event-sourced orders), but worth reopening because…_

Note that `docs/decisions.md` is **not** an ADR directory, but it plays a similar role: it records
settled decisions that prior audits raised and rejected, and `CLAUDE.md` requires reading the
relevant entry before re-proposing a change. Treat a conflict with it the same way as an ADR
conflict — surface it, don't override it silently.
