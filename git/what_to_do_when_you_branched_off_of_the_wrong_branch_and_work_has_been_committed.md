When you try to cherry-pick commits from one branch onto another, git looks for those specific commit SHAs in the history. If you're on a different branch that
  doesn't have those commits in its history, git can't find them.

  What's happening:
  - Your project doc update branch was created from, say, css-refactor/session-3
  - The commits you made are on that branch's history chain
  - When you checkout `main` and try to cherry-pick those commit SHAs, `main` doesn't know about them because they're on a different branch lineage
  - Git says "empty set" because it can't find those commits

  Solution:

  Simple file copy (easiest for doc updates)
  On your current wrong-base branch, note which files you changed
  `git status`
  `git diff origin/main --name-only`

  Checkout main and create new branch
  `git checkout main`
  `git checkout -b css-refactor/session-4-plan-update-3`

  Copy the files from the wrong branch
  `git checkout css-refactor/session-4-plan-update-2 -- path/to/file1.md path/to/file2.md`
