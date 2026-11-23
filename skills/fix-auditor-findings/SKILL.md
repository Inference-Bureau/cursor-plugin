---
name: fix-auditor-findings
description: Fix the findings Inference Bureau's Auditor left on the current branch's pull request, then mark each one fixed or not to fix. Use when the user asks to fix Auditor's findings or review comments, or what Auditor flagged on their pull request.
---

# Fix Auditor's findings

Auditor reviews pull requests and leaves findings as review comments. This works through the open ones on the
pull request for the branch that's checked out.

1. Find the pull request. Take the repository (`owner/name`) from `git remote get-url origin` and the branch from
   `git branch --show-current`. Call `list_findings` with `repo` and `branch`, or with `pr` if the user named a number.
   If it says Auditor hasn't reviewed the pull request, or nothing is open, tell the user and stop.
2. Go worst first. For each finding, call `get_finding`: it gives the explanation, the flagged code, a suggested
   replacement if there is one, and a prompt for fixing it. The code may have moved since the review: find the
   flagged code in the file rather than trusting the line numbers.
3. Decide. Fix it when the finding is right. When it's wrong, or right but out of scope, don't change the code: note
   why instead. Ask the user when you're unsure, before changing anything that changes behavior beyond the finding.
4. Check the fix the way the project checks its code (its type checker and the tests for what you touched).
5. Tell the user what you changed and what you left, finding by finding. Mark findings only after the user has seen
   that. `resolve_finding` with `fixed` for those you fixed; `wont_fix` with a one-sentence `note` for those you left.
   Resolving edits the review comment on GitHub, where everyone on the pull request sees it.

Don't commit or push unless the user asks. A finding marked fixed whose flagged code is still there after the push
is flagged again by the next review.
