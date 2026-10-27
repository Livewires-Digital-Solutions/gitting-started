# Git cheat sheet

## Setup

```bash
git --version
git config --global user.name "Sami"
git config --global user.email "me@sam1.space"
git config --global init.defaultBranch main
git config --global --list
```

GitHub uses a personal access token as the password for HTTPS pushes.

## Daily loop

```bash
git status
git diff
git add <file>
git commit -m "type: message"
git log --oneline
```

## Start a repo

```bash
git init
git clone <url>
```

## Branch

```bash
git checkout -b my-branch
git checkout main
git branch
```

## Remotes

```bash
git remote -v
git remote add fork <url>
git push -u fork my-branch
git pull origin main
```

`origin` is the original LiveWires repo. `fork` is your copy.

## Conventional commits

```
type(scope): summary
```

```bash
git commit -m "feat(people): add sami profile"
git commit -m "fix(nav): correct broken link"
git commit -m "docs: update setup guide"
git commit -m "chore: initialize repository"
```

Types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`.

## Open a pull request

1. Push your branch to `fork`.
2. Open the URL Git prints.
3. Base: `Livewires-Digital-Solutions/gitting-started` → `main`.
4. Compare: your fork → your branch.
5. Check **Files changed** shows one file.
6. Create the PR.

## Inspect

```bash
git status
git diff
git diff --staged
git log --oneline -10
git remote -v
git branch -vv
```

## Undo

| Goal | Command | After push? |
|---|---|---|
| Unstage a file, keep the edit | `git restore --staged <file>` | Yes |
| Throw away local edits | `git restore <file>` | Yes, edit is gone |
| Fix the last commit message | `git commit --amend -m "Message"` | No |
| Undo the last commit, keep changes | `git reset --soft HEAD~1` | No |
| Undo a pushed commit | `git revert <sha>` | Yes |
| Find a lost commit | `git reflog` | Yes |

Do not run `git reset --hard` yet.

## Fixes

```bash
# Wrong folder
pwd

# Git does not know who you are
git config --global user.name "Sami"
git config --global user.email "me@sam1.space"

# Push rejected
git pull
git push

# Remote already exists
git remote -v
git remote set-url fork <url>

# Authentication failed
# Use a personal access token as the password
```

## Vocabulary

| Word | Meaning |
|---|---|
| **Repository** | Project plus its history |
| **Commit** | A snapshot with a message and author |
| **Staging area** | Changes selected for the next commit |
| **Branch** | A parallel line of commits |
| **Remote** | A nickname for a repo URL |
| **Origin** | The original LiveWires repo |
| **Fork** | Your copy of a repo on GitHub |
| **Clone** | A copy of a repo on your laptop |
| **Pull request** | A request to merge your branch |
| **Merge** | Combine two lines of history |

## Rules

1. Never commit secrets.
2. Do not force-push shared branches.
3. Pull before you push.
4. One branch, one purpose.
5. Run `git status` before you panic.
