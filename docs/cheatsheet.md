# Git & GitHub Cheat Sheet

## Estado y cambios

```bash
git status
git diff
git diff --staged
```

## Staging

```bash
git add archivo
git add .
git add -p
git restore --staged archivo
```

## Commits

```bash
git commit -m "feat: add feature"
git commit --amend
git show HEAD
```

## Historial

```bash
git log --oneline
git log --oneline --graph --decorate --all
git log -S "texto" --oneline
git blame archivo
```

## Branches

```bash
git branch
git branch -a
git switch main
git switch -c feat/nueva-tarea
git branch -d feat/nueva-tarea
git branch -D feat/nueva-tarea
```

## Remotes

```bash
git remote -v
git remote add origin <url>
git remote set-url origin <url>
git fetch --prune
```

## Pull / Push

```bash
git pull --ff-only
git push
git push -u origin feat/nueva-tarea
git push origin --delete feat/nueva-tarea
```

## Merge

```bash
git switch main
git merge feat/nueva-tarea
git merge --abort
```

## Rebase

```bash
git rebase origin/main
git rebase --continue
git rebase --abort
git rebase -i HEAD~5
```

## Cherry-pick

```bash
git cherry-pick <sha>
git cherry-pick --continue
git cherry-pick --abort
```

## Restore / Reset / Revert

```bash
git restore archivo
git restore --staged archivo
git revert <sha>
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

## Reflog

```bash
git reflog
git switch -c recovery/<nombre> <sha>
```

## Stash

```bash
git stash push -m "wip"
git stash push -u -m "wip"
git stash list
git stash pop
git stash apply stash@{0}
```

## Clean

```bash
git clean -nd
git clean -fd
```

## Tags

```bash
git tag
git tag -a v2.0.0 -m "Release v2.0.0"
git push origin v2.0.0
```

## SSH

```bash
ssh-keygen -t ed25519 -C "tu@email.com"
ssh-add ~/.ssh/id_ed25519
ssh -T git@github.com
```

## GitHub CLI

```bash
gh auth login
gh pr create --fill
gh pr list
gh pr view --web
gh pr checks
gh issue list
```

## Flujo seguro de feature

```bash
git switch main
git pull --ff-only
git switch -c feat/tarea
# cambios
git add -p
git diff --staged
git commit -m "feat: implement task"
git push -u origin feat/tarea
gh pr create --fill
```

## Antes de un comando riesgoso

```bash
git status
git log --oneline --graph --decorate --all -20
git reflog -20
```

Preferí `git push --force-with-lease` sobre `git push --force` cuando realmente necesitás actualizar una rama reescrita.
