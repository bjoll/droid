# Issue tracker

This repo tracks issues on **GitHub Issues** at `bjoll/droid`. Use the `gh` CLI for all operations.

## Wayfinding operations

How wayfinder concepts map onto this tracker:

- **Map**: an issue labelled `wayfinder:map` (currently [#1](https://github.com/bjoll/droid/issues/1)). Its tickets are **native sub-issues** of the map issue.
- **Ticket type**: a `wayfinder:<type>` label (`research`, `prototype`, `grilling`, `task`).
- **Claim**: assign yourself before doing any work — `gh issue edit <n> --add-assignee @me`. Open + unassigned = unclaimed.
- **Blocking**: GitHub's **native issue dependencies** (rendered in the issue sidebar as "Blocked by"). Wire an edge with:

  ```sh
  gh api -X POST repos/bjoll/droid/issues/<blocked>/dependencies/blocked_by -F issue_id=<blocker-database-id>
  # database id: gh api repos/bjoll/droid/issues/<n> --jq .id
  ```

  Read a ticket's blockers (and their open/closed state) with:

  ```sh
  gh api repos/bjoll/droid/issues/<n>/dependencies/blocked_by --jq '.[] | {number, state}'
  ```

- **Sub-issue linking** (create-then-wire): after creating a ticket, attach it to the map:

  ```sh
  gh api -X POST repos/bjoll/droid/issues/1/sub_issues -F sub_issue_id=<ticket-database-id>
  ```

- **Close / resolve**: post the resolution as a comment — the decision, the alternatives it beat, and what follows from it — then close:
  `gh issue comment <n> --body "..."` then `gh issue close <n>`.
- **Frontier query** (open, unblocked, unclaimed tickets of the map): list open unassigned candidates, then drop any with an open blocker:

  ```sh
  gh issue list --state open --no-assignee --json number,title,labels
  # for each candidate: gh api repos/bjoll/droid/issues/<n>/dependencies/blocked_by --jq '[.[] | select(.state=="open")] | length'   # 0 = unblocked
  ```

  The map issue itself (label `wayfinder:map`) is not a ticket — skip it.
- **Assets**: files created while resolving a ticket live in the repo (e.g. `docs/`), committed and linked from the issue — never pasted into it.
