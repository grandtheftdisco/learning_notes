## ===== RESOLVING CONFLICTS: `--ours` vs `--theirs` =====
‼️CONFUSING: These flags mean OPPOSITE things in `rebase` vs `merge`!

During REBASE (`git rebase main`):
- `--ours`   = version from branch you're rebasing ONTO (`main`)
- `--theirs` = version from YOUR branch (the one being rebased)

During MERGE (`git merge [feature-branch]`):
- `--ours`   = version from YOUR current branch
- `--theirs` = version from branch being merged in

Example from `rebase`:
`git checkout --theirs [file_name]`
= "Keep my branch's version, discard `main`'s version"

Quick resolution commands:
`git checkout --ours <file>`    - Keep destination branch version
`git checkout --theirs <file>`  - Keep your branch version
`git add <file>`                - Mark as resolved
`git rebase --continue`         - Continue rebase

TIP: During `rebase`, think REverse:
- "theirs" = yours (your branch)
- "ours" = destination (`main`)

