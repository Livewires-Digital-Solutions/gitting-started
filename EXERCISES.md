# Exercises

Three labs. Follow in order. Every lab ends with a checkpoint.

Replace anything in `<angle brackets>` with your own details. Do not type the brackets.

---

## Before we start

### 1. Install Git

**Windows**

```powershell
winget install --id Git.Git -e --source winget
```

**macOS**

```bash
xcode-select --install
```

**Linux (Debian/Ubuntu)**

```bash
sudo apt install git
```

Or download an installer from <https://git-scm.com/downloads>.

Verify:

```bash
git --version
```

### 2. Configure Git

```bash
git config --global user.name "Sami"
git config --global user.email "me@sam1.space"
git config --global init.defaultBranch main
git config --global --list
```

Use your own name and GitHub email. These values appear on every commit.

### 3. Authentication

GitHub does not accept your account password for Git operations over HTTPS. Use a personal access token.

1. GitHub → **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**.
2. **Generate new token (classic)**.
3. Scope: **repo**.
4. Copy the token.
5. When Git asks for a password, paste the token.

Do not paste the token into chat or commit it to a file.

---

# Conventional commits

Format:

```
type(scope): summary
```

Examples:

```
feat(people): add sami profile
fix(nav): correct broken link
docs: update setup guide
chore: initialize repository
```

- Lowercase summary.
- Imperative: `add`, not `added`.
- No period at the end.
- Scope is optional.

Common types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`.

---

# Lab 01: Your first repository

## 1. Create a folder and initialise Git

```bash
mkdir git-lab
cd git-lab
git init
```

`git init` creates a hidden `.git` folder. That folder is the project's history. Never delete it unless you want to throw the history away.

```bash
ls -a
```

## 2. Create a file

Create `README.md` with one line:

```markdown
# My Git Lab
```

Or use the terminal:

**macOS / Linux**

```bash
printf '# My Git Lab\n' > README.md
```

**Windows PowerShell**

```powershell
Set-Content README.md "# My Git Lab"
```

## 3. Stage and commit

```bash
git status
git add README.md
git commit -m "chore: initialize git lab"
```

After `git add`, the file is **staged**. After `git commit`, it is saved in history.

## 4. Make a second commit

Add another line to `README.md`:

```markdown
I made my first commit.
```

Then:

```bash
git diff
git add README.md
git commit -m "docs: add first note"
git log --oneline
git status
```

**Checkpoint**

- [ ] `git log --oneline` shows two commits.
- [ ] Both commits show your name.
- [ ] `git status` says `nothing to commit, working tree clean`.

---

# Lab 02: Your first pull request

In this lab:

- `origin` is the original LiveWires repo.
- `fork` is your copy on GitHub.
- You pull from `origin` and push to `fork`.

## 1. Fork the repo

Open <https://github.com/Livewires-Digital-Solutions/gitting-started> and click **Fork**.

- Owner: your own account.
- Repository name: `gitting-started`.
- Leave **Copy the main branch only** checked.

## 2. Clone the original repo

```bash
git clone https://github.com/Livewires-Digital-Solutions/gitting-started.git
cd gitting-started
git remote -v
```

`origin` should point at LiveWires.

## 3. Add your fork as a remote

```bash
git remote add fork https://github.com/<your-handle>/gitting-started.git
git remote -v
```

**Checkpoint:** `origin` is LiveWires. `fork` is your copy.

## 4. Create a branch

```bash
git checkout -b add-<your-handle>
git branch
```

The branch with `*` is the current branch.

## 5. Create your profile

```bash
cp people/_template.md people/<your-handle>.md
```

Open the file and fill it in. If you use VS Code:

```bash
code people/<your-handle>.md
```

## 6. Commit and push

```bash
git status
git add people/<your-handle>.md
git commit -m "feat(people): add <name> profile"
git push -u fork add-<your-handle>
```

`-u` links the local branch to `fork`, so later pushes can use `git push`.

If Git asks for a password, paste your personal access token.

## 7. Open the pull request

GitHub prints a link after the push. Open it, or go to the original repo and click **Compare & pull request**.

Check:

- **base repository:** `Livewires-Digital-Solutions/gitting-started`
- **base branch:** `main`
- **head repository:** your fork
- **compare branch:** `add-<your-handle>`
- **Files changed:** exactly one file

Use a title like `feat(people): add <name> profile`. Create the PR.

**Checkpoint**

- [ ] The PR page shows **1 file changed**.
- [ ] It says **Able to merge**.
- [ ] The base repo is `Livewires-Digital-Solutions/gitting-started`.
- [ ] The title follows `type: summary`.

---

# Lab 03: Pull the team's work

## 1. Switch to main

```bash
git checkout main
```

## 2. Pull from origin

```bash
git pull origin main
git log --oneline -3
cat LIVE.md
```

`git pull` is **fetch** plus **merge**. `origin` is the LiveWires repo.

**Checkpoint**

- [ ] The latest commit mentions the live update.
- [ ] You can see the new line in `LIVE.md`.
- [ ] `git status` is clean.

---

# When things go wrong

Read the **last line** of the error first.

| Message | What it means | Fix |
|---|---|---|
| `fatal: not a git repository` | Wrong folder | `pwd`, then `cd` to the repo |
| `Author identity unknown` | Git does not know who you are | Run the two `git config` commands |
| `nothing to commit` | No saved changes | Save the file, then `git status` |
| `src refspec ... does not match any` | Nothing committed, or wrong branch | `git status`, `git log --oneline`, `git branch` |
| `Authentication failed` | GitHub wants a token | Use a personal access token as the password |
| `Updates were rejected ... fetch first` | Someone pushed first | `git pull`, then `git push` |
| `remote fork already exists` | You already added the remote | `git remote -v`, then `git remote set-url fork <url>` |
| `LF will be replaced by CRLF` | Windows line endings warning | Ignore it |
| A file opens in `vim` during commit | Git opened an editor | Type `:wq`, press Enter |

## Before asking for help

```bash
git status
git log --oneline -5
```

## If you commit a secret

Tell the facilitator immediately. Deleting the file in a new commit does not remove it from history. Rotate the secret.
