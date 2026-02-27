# EcoRide Git Cheatsheet

This file contains the Git commands needed for this project.

## 1. Clone Repository (first time only)

```bash
git clone https://github.com/harish885/ecoride.git
cd ecoride
```

What it does:
- Downloads the project to your local machine.

## 2. Switch to Your Branch

```bash
git checkout harish
# or
git checkout virginia
# or
git checkout yon
```

What it does:
- Moves you to your personal working branch.

## 3. Check Current Branch

```bash
git branch --show-current
```

What it does:
- Shows which branch you are currently on.

## 4. Check Working Status

```bash
git status
```

What it does:
- Shows changed files, staged files, and branch status.

## 5. Pull Latest Changes from Your Branch

```bash
git pull origin <your-branch>
```

Example:

```bash
git pull origin harish
```

What it does:
- Brings latest commits from GitHub into your current branch.

## 6. Get Latest `main` into Your Branch

```bash
git fetch origin
git merge origin/main
```

What it does:
- Downloads latest remote changes and merges `main` updates into your branch.

## 7. Stage Files for Commit

```bash
git add .
```

Or stage specific files:

```bash
git add README.md sql/ddl/users.sql
```

What it does:
- Marks file changes to be included in the next commit.

## 8. Commit Changes

```bash
git commit -m "Add users table and migration"
```

What it does:
- Saves a local snapshot of staged changes with a message.

## 9. Push Your Branch

```bash
git push origin <your-branch>
```

Example:

```bash
git push origin virginia
```

What it does:
- Uploads your branch commits to GitHub.

## 10. Merge a Branch into `main` (maintainer flow)

```bash
git checkout main
git pull origin main
git merge origin/<teammate-branch>
git push origin main
```

Example:

```bash
git merge origin/yon
```

What it does:
- Brings teammate completed work into `main` and publishes it.

## 11. Sync All Team Branches with `main`

```bash
git checkout main
git pull origin main

git checkout harish
git merge main
git push origin harish

git checkout virginia
git merge main
git push origin virginia

git checkout yon
git merge main
git push origin yon

git checkout main
```

What it does:
- Keeps all team branches updated with the same latest content.

## 12. Resolve Merge Conflicts

After conflict appears:

```bash
git status
# manually edit conflicted files
git add <fixed-file>
git commit -m "Resolve merge conflict"
git push origin <your-branch>
```

What it does:
- Finalizes merge after conflict resolution and publishes fix.

## 13. View Commit History

```bash
git log --oneline --decorate --graph -20
```

What it does:
- Shows recent commit history in compact format.

## 14. Useful Safe Commands

```bash
git branch -vv
```
- Shows local branches and tracking status.

```bash
git fetch --all
```
- Updates remote references without modifying your files.

```bash
git diff
```
- Shows unstaged line-by-line changes.

```bash
git diff --staged
```
- Shows changes already staged for next commit.

## Team Rule Reminder

- Always check branch before committing.
- Never commit directly to `main` unless doing integration work.
- Push your branch daily.
