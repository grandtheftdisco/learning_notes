## ===== GIT RESET EXPLAINED =====
Three types: `--soft`, `--mixed` (default), and `--hard`

`git reset HEAD` (same as `git reset --mixed HEAD`):
- Unstages files (moves from staging area back to working directory)
- Does NOT modify your actual code changes
- Safe - only affects what's ready to commit, not the files themselves

`git reset --soft <commit>`:
- Moves `HEAD` to specified commit
- Keeps all changes staged (ready to commit)
- Safe - preserves all your work

`git reset --mixed <commit>` (or just `git reset <commit>`):
- Moves `HEAD` to specified commit
- Unstages changes (not ready to commit, but still in files)
- Safe - preserves all your work in working directory

`git reset --hard <commit>`:
- Moves `HEAD` to specified commit
- DELETES all uncommitted changes
- ‼️DANGEROUS - you lose work that wasn't committed
- Use _only_ when you're certain you want to discard changes

Example workflow:
`git status`                    - See what's staged
`git reset HEAD`                - Unstage everything (code unchanged)
`git add specific-file.txt`     - Stage only what you want
`git commit -m "message"`       - Commit just that file

Visual:
Working Directory (your actual files)
  ↕️ `git add` / `git reset HEAD`
Staging Area (what's ready to commit)
  ↕️ `git commit` / `git reset --soft`
Repository (committed history)
