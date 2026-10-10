# Issue tracker: GitHub Issues

Issues and specs for this repo live as **GitHub issues on the fork**,
[`johncclayton/resty-desktop`](https://github.com/johncclayton/resty-desktop/issues), reached with
the `gh` CLI.

This repo is a fork with an active upstream (`nraboy/resty-desktop`). Work items live on the fork's
own issue tracker, never as files in the git tree, so they stay out of upstream PR diffs and off
every rebase — the same constraint the previous local-markdown tracker was built to satisfy, now met
without giving up durability or a shared URL.

> Issues are disabled by default on a GitHub fork; they were enabled on this one with
> `gh repo edit --enable-issues`. If `gh issue list` reports them disabled, that setting was reverted.

`.scratch/` is still gitignored and still useful for local throwaway tooling — the Explore
verification harness lives at `.scratch/explorer/verification/` — but it is **not** the issue
tracker. Don't create ticket or spec markdown there.

## Conventions

- One feature is one **spec issue**: the specification in the body, labelled `spec`, acting as the
  tracking issue.
- Implementation slices are **sub-issues** of that spec issue, attached natively so GitHub renders
  the progress tracker. The spec issue's body also carries a readable index table of its slices.
- Each slice body opens with `Part of #<spec>` and, when it has prerequisites, `Blocked by #N, #N`.
  A slice is unblocked when every issue it names is closed.
- Triage state is a **GitHub label** (see `triage-labels.md`). Exactly one triage label at a time.
- Completion is the issue's own **closed-as-completed** state, not a label.
- Conversation history is **GitHub comments**. Don't append a `## Comments` section to a body.

## Commands

```bash
gh issue list                                  # open issues
gh issue list --label ready-for-agent          # the AFK-ready frontier
gh issue view <N> --comments                   # a ticket plus its history
gh issue create --title "…" --body-file <f> --label <triage-label>
gh issue comment <N> --body-file <f>
gh issue edit <N> --add-label X --remove-label Y
gh issue close <N> --reason completed

# attach an existing issue as a sub-issue of a spec issue (note -F, not -f: the API wants an integer)
gh api -X POST repos/johncclayton/resty-desktop/issues/<spec>/sub_issues \
  -F sub_issue_id="$(gh api repos/johncclayton/resty-desktop/issues/<N> --jq .id)"

gh api repos/johncclayton/resty-desktop/issues/<spec>/sub_issues \
  --jq '.[] | "#\(.number) \(.state) \(.title)"'
```

Write any body longer than a line to a file and pass `--body-file`. Shell quoting mangles the long
prose and em dashes these issues are full of.

## When a skill says "publish to the issue tracker"

Create a GitHub issue. If the work is a feature spec, label it `spec` and keep its slices as
sub-issues of it. Apply the triage label the skill names.

## When a skill says "fetch the relevant ticket"

`gh issue view <N> --comments`. The user will normally pass the issue number or URL directly.

## Wayfinding operations

Used by `/wayfinder`. The **map** is a `spec`-labelled issue; each **child ticket** is a sub-issue
of it.

- **Map**: a `spec` issue holding the Notes / Decisions-so-far / Fog body.
- **Child ticket**: a sub-issue with the question in the body. The ticket type
  (`research`/`prototype`/`grilling`/`task`) is a `type:<kind>` label; create it on first use.
- **Blocking**: a `Blocked by #N, #N` line near the top of the body. A ticket is unblocked when
  every issue it names is closed.
- **Frontier**: `gh issue list --label ready-for-agent` filtered to issues that are open, unblocked
  and unassigned; lowest number wins.
- **Claim**: `gh issue edit <N> --add-assignee @me` before any work.
- **Resolve**: comment the answer, `gh issue close <N> --reason completed`, then append a context
  pointer (gist + issue URL) to the map issue's Decisions-so-far.

## Existing features

| Feature | Spec issue |
|---|---|
| Explore — unified folder view of a repository | [#1](https://github.com/johncclayton/resty-desktop/issues/1) |

## History

Before 2026-10-10 the tracker was local markdown under `.scratch/<feature-slug>/`. The Explore
feature's spec, research record and five implementation tickets were migrated to issues #1–#6 on
that date and the local copies deleted; the `verification/` harness was left on disk because it is
scripts, not tickets.
