---
name: ship
description: Open a pull request for a finished Octave branch, wait for CI, merge it, and clean up. Use after review passes, or when the owner asks to ship.
---

# Ship

## Before the PR

- Run the branch's validation commands and keep their output.
- Confirm the one review round has no open critical, high, or medium findings.
- Confirm the branch is not `main`.
- Rebase on `origin/main`; never merge `origin/main` into the branch.
- Push the branch with `git push -u origin <branch>`.

## Open the PR

- Before a top-level screen ships, ask the owner to try its key tasks on a real TV with its remote; involve a household member or use a household device only with the owner's word for that run.

- Create it with `gh pr create --base main`.
- Use a Conventional Commit subject as the title.
- Fill in every section of `.github/pull_request_template.md`.
- When the PR loosens a security rule, open the Summary with one plain sentence saying what got looser, or "Nothing got looser."
- Link the plan or issue.
- List every device and server you did not test.

## Wait for CI

- Enable auto-merge with `gh pr merge <number> --auto --rebase --delete-branch`, unless the owner says not to.
- Run `gh pr checks <number> --watch`.
- Hand failing output to `ci-triage`.
- Fix failures in new commits on the branch.
- Never merge with a red or pending required check, and never skip or disable a check to merge.

## Keep the branch current

- Treat a `BEHIND` merge state as stale: run `gh pr update-branch <number> --rebase`.
- Treat a `DIRTY` merge state as a conflict: rebase locally, rerun the checks, and push with `git push --force-with-lease`.
- Use force-with-lease only on your own unmerged branch.

## Merge

- Merge when CI is green and the review round left no critical, high, or medium finding open.
- Merge with `gh pr merge <number> --rebase --delete-branch` when auto-merge is off.
- Never bypass or edit the `main` ruleset to merge.
- Ask before merging a GitHub Actions update.

## After the merge

- Run `git switch main` and `git pull --ff-only`.
- Delete the local branch.
- Report the PR link and merge commit to the owner.
