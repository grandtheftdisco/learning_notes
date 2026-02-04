/////////// RUSSIAN DOLL BRANCHING /////////////////

Let's say you have just written a PR for a Branch A, but you need to
start work on Branch B ASAP. It may take awhile for review of Branch
A to be completed, so you decide to simply base Branch B off of Branch A
in its unreviewed state. You realize you're risking having to make changes
to Branch A after review, but time is of the essence.

Complete work on Branch B as needed.

Then, after Branch A merges to main:

  Checkout Branch B
  `git checkout amanda/B`

  Fetch latest from remote
  `git fetch origin`

  Rebase onto main (which now includes Branch A)
  `git rebase origin/main`

  Force push (since `rebase` rewrites history)
  `git push --force-with-lease`

Real Git/GitHub terms:
  - Stacked branches or stacked diffs (most common)
  - Dependent branches
  - Feature branch chains
  - Branch stacking

Companies like Meta (Facebook) use stacked diffs extensively with tools like Phabricator,
and there are even Git tools specifically for managing stacked branches:
  - `git-branchstack`
  - `git-stack`
  - GitHub's own experimental stacked PR features
