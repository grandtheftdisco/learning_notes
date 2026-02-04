## ===== GIT RESET VS GIT RESTORE =====
Both can undo changes, but they work differently

`git restore` (modern, specific):
- Introduced in Git 2.23 (2019) to be clearer than reset
- Has TWO separate jobs:

1. `git restore <file>`
   - Discards changes in working directory
   - Resets file to last committed state
   - ‼️ DANGEROUS - you lose uncommitted work
   Example: `git restore myfile.txt`  - throws away your edits

2. `git restore --staged <file>`
   - Unstages file (opposite of `git add`)
   - Moves file from staging back to working directory
   - ✅ SAFE - your changes stay in the file
   Example: `git restore --staged myfile.txt`  - Unstage, but keep changes

`git reset` (older, multi-purpose):
- More powerful but more confusing
- Can move `HEAD`, unstage files, and discard changes
- Has three modes: `--soft`, `--mixed (default)`, and `--hard`

Common commands compared:

Unstage a file (safe):
`git restore --staged <file>`   - Modern way
`git reset HEAD <file>`         - Old way (same result)

Discard changes in file (‼️ DANGEROUS):
`git restore <file>`            - Modern way
`git checkout -- <file>`        - Old way (same result)

Move `HEAD` to previous commit:
`git reset --soft HEAD~1`       - Only `reset` can do this

RECOMMENDATION:
- Use `git restore` for file operations (clearer intent)
- Use `git reset` for commit operations (moving `HEAD`)

Example workflow:
`git add file1.txt file2.txt file3.txt`      - Stage 3 files
`git restore --staged file2.txt`             - Oops, unstage file2 (keep changes)
`git commit -m "Add file1 and file3"`        - Commit other 2
`git restore file2.txt`                      - Discard file2 changes entirely

