////////////// getting a list of touched files on a branch ///////////////

With status indicators (M/A/D for Modified/Added/Deleted):
  `git diff main...HEAD --name-status`

Just the file names:
  `git diff main...HEAD --name-only`

- Replace `main` with whatever your base branch is, and `HEAD` refers to your current branch tip.
- The `...` syntax shows all changes since the branch diverged from `main`.
