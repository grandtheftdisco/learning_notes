===== FORCE PUSH SAFELY =====
`git push origin your-branch --force-with-lease`

###`--force-with-lease` vs `--force:`
- `--force`: Blindly overwrites remote (dangerous if others pushed)
- `--force-with-lease`: Checks if remote changed since your last pull
  - If someone else pushed: rejects (protects their work)
  - If no changes: allows force push (safe)

After rebase, local and remote diverged:
- Local = correct (rebased on new foundation)
- Remote = outdated (old foundation)
- Force push = tell GitHub "my local is truth"

Common mistake: Seeing ⇡⇣ and pulling = rebase loop hell!
Solution: Always `force-with-lease` after rebasing

