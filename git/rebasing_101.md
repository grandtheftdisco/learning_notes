Rebasing is like moving your building to a new foundation

Main branch:
  Floor C (newest)
  Floor B
  Floor A (foundation)

Your branch started from Floor A and built:
  Your Floor F
  Your Floor E
  Your Floor D
  -------
  Floor A (old foundation)

After rebasing:
  Your Floor F
  Your Floor E
  Your Floor D
  -------
  Floor C (new stuff from `main`)
  Floor B (new stuff from `main`)
  Floor A (original foundation)

KEY POINTS:
- Your work stays in order (D, E, F)
- It's just built on top of new foundation (B, C)
- NOT like shuffling/mixing - your commits stay together
- Conflicts = both you and main changed the same thing

Rebasing steps:
1. `git checkout your-branch`
2. `git branch your-branch-backup`  (safety!)
3. `git rebase main`
4. Fix conflicts if any
5. `git add [fixed-files]`
6. `git rebase --continue`
7. `git push origin your-branch --force-with-lease`

Emergency abort:
`git rebase --abort`

===== AFTER REBASING: STARSHIP UI SYMBOLS [specific to my machine] =====
`~/[path_to_repo] on 🌱 [branch_name] [📦⇕⇡4⇣3]`

⇡4 = 4 commits ahead (to `push`)
⇣3 = 3 commits behind (to `pull`)

IMPORTANT: After rebasing, DO NOT pull!
- ⇡ = your rebased commits (correct, new foundation)
- ⇣ = old pre-rebase commits on remote (outdated)
- Pulling would undo your rebase and create a mess!
- Instead: force push with `--force-with-lease`
  - see `force_pushing_safely.md` in this dir for more deets
