# Triage Labels

The skills speak in terms of five canonical triage roles. This file maps those roles to the actual
label strings used in this repo's issue tracker.

This repo uses the defaults: each label string equals its role name. The tracker is GitHub Issues on
the fork (see `issue-tracker.md`), so a label is a real GitHub label object — created once, applied
with `gh issue edit --add-label`.

| Label in mattpocock/skills | Label in our tracker | Meaning                                  |
| -------------------------- | -------------------- | ---------------------------------------- |
| `needs-triage`             | `needs-triage`       | Maintainer needs to evaluate this issue  |
| `needs-info`               | `needs-info`         | Waiting on reporter for more information |
| `ready-for-agent`          | `ready-for-agent`    | Fully specified, ready for an AFK agent  |
| `ready-for-human`          | `ready-for-human`    | Requires human implementation            |
| `wontfix`                  | `wontfix`            | Will not be actioned                     |

When a skill mentions a role (e.g. "apply the AFK-ready triage label"), use the corresponding label
string from this table.

Edit the right-hand column to match whatever vocabulary you actually use.

## Notes

- `wontfix` already existed as a GitHub default label (`#ffffff`, "This will not be worked on") and
  is reused rather than duplicated — the role and the stock label mean the same thing. The other four
  were created for this repo.
- Apply **one** triage label at a time; they are mutually exclusive states.
- All five are **pre-work** states. There is deliberately no completion label: a finished issue is
  **closed as completed** (`gh issue close <N> --reason completed`), which is GitHub's own
  representation and needs no vocabulary of its own. The `resolved` string that the local-markdown
  era borrowed from the wayfinding vocabulary is gone.
- `spec` is not a triage label — it marks a feature's tracking issue, and such an issue also carries
  whichever triage label reflects its state.
