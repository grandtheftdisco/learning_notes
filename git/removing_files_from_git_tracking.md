## ===== REMOVING FILES FROM GIT TRACKING =====
`git rm --cached <file>`

Removes file from git tracking but KEEPS it on your filesystem
Useful for files you want locally but don't want in the repo

Example:
`git rm --cached git_notes.txt`  - Stop tracking, keep file locally
`git rm git_notes.txt`           - Remove from git AND delete file

After running `--cached`:
1. File stays on your computer (can still read/edit)
2. Git stops tracking it (won't show in diffs/PRs)
3. Add file to `.gitignore` to prevent future tracking

Common use case:
`git rm --cached .env`
`echo ".env" >> .gitignore`
`git commit -m "Stop tracking .env file"`

