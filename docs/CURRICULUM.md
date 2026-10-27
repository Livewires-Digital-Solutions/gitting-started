# Gitting Started — Curriculum

A 60-minute, hands-on introduction to Git and GitHub for interns who have never used either.

**Audience:** 5–30 interns, no prior industry experience. Everyone has a laptop and a GitHub account.
**Format:** Live demo, two main labs, and a short pull lab. Everyone follows along.
**Deck:** https://gitting-started.sam1.space
**Exercise repo:** https://github.com/Livewires-Digital-Solutions/gitting-started

---

## Learning outcomes

By the end of the hour, each intern can:

1. Explain the difference between Git and GitHub.
2. Install Git, configure their name and email, and authenticate a push.
3. Create a local repository, stage a change, commit it, and read the log.
4. Fork a repository, clone `origin`, add a `fork` remote, push a branch, and open a pull request.
5. Pull changes from `origin`.
6. Write a conventional commit message.
7. Name the safety rules: no secrets, no force-pushing shared branches, pull before push.

## Non-goals

Rebase, cherry-pick, submodules, Git LFS, GitHub Actions, SSH keys, release management, and complex branching strategies. Mention that they exist; do not teach them.

## Why this shape

One hour is enough for **one mental model and one complete loop**:

```
install → configure → edit → add → commit → push → pull request → pull
```

`origin` is the LiveWires repository. `fork` is the intern's copy. This avoids the usual `origin`/`upstream` confusion: pull from `origin`, push to `fork`. Branch commands use `git checkout`, not `git switch`, because interns will see `checkout` in most existing documentation.

The labs avoid merge conflicts so nobody gets stranded. Merge conflicts are a follow-up session.

---

## Run of show

| Time | Segment | Mode | What happens |
|---|---|---|---|
| 0:00–0:04 | Welcome + outcomes | Talk | Three outcomes: commit, push, pull request. |
| 0:04–0:09 | Mental model | Talk + diagram | Git vs GitHub, commits, staging, the loop. |
| 0:09–0:16 | Install + configure | Hands-on | OS install, `git --version`, identity, personal access token. |
| 0:16–0:20 | Commit anatomy + conventional commits | Talk | `type(scope): summary`. |
| 0:20–0:30 | **Lab 01 — First repo** | Guided | `init`, `add`, `commit`, `log`. Two commits. |
| 0:30–0:35 | Remotes and forks | Demo | `origin` vs `fork`, repo vs clone vs branch. |
| 0:35–0:50 | **Lab 02 — First pull request** | Guided | Fork → clone origin → add fork → checkout → commit → push → PR. |
| 0:50–0:54 | Pull + **Lab 03** | Demo + hands-on | Instructor merges a PR and updates `LIVE.md`; everyone pulls `origin`. |
| 0:54–0:58 | Safety + undo | Talk | Secrets, force-push, `restore`, `revert`, `reflog`. |
| 0:58–1:00 | Recap + questions | Talk | Six commands, four ideas. |

**Buffer policy:** if running behind, cut the undo table and the first-week slide. Never cut install/configure or Lab 02's push/PR step.

---

## Labs

### Lab 01 — Your first repository (10 min)

```bash
mkdir git-lab
cd git-lab
git init
# create README.md
git status
git add README.md
git commit -m "chore: initialize git lab"
# edit README.md
git diff
git add README.md
git commit -m "docs: add first note"
git log --oneline
```

**Success:** two commits, clean working tree.

### Lab 02 — Your first pull request (15 min)

Each intern forks the repo, clones the original as `origin`, adds their fork as `fork`, and opens a PR.

```bash
git clone https://github.com/Livewires-Digital-Solutions/gitting-started.git
cd gitting-started
git remote add fork https://github.com/<handle>/gitting-started.git
git remote -v
git checkout -b add-<handle>
cp people/_template.md people/<handle>.md
# edit the file
git add people/<handle>.md
git commit -m "feat(people): add <name> profile"
git push -u fork add-<handle>
```

**Success:** PR shows one changed file and "Able to merge" against LiveWires `main`.

### Lab 03 — Pull the team's work (4 min)

```bash
git checkout main
git pull origin main
git log --oneline -3
cat LIVE.md
```

**Success:** the live update is present locally.

---

## Pre-work (send 48 hours before)

> Bring a laptop with Git installed and a GitHub account you can sign in to.
> 1. Create a free GitHub account at github.com.
> 2. Install Git: Windows `winget install --id Git.Git -e --source winget`; macOS `xcode-select --install`; Linux `sudo apt install git`.
> 3. Run `git --version`.
> 4. Reply with your GitHub username.
> 5. If any step fails, join 10 minutes early.

The session covers install and configuration again, but pre-work reduces setup time.

---

## Facilitator pre-flight

- [ ] Open the deck, the exercise repo, and a terminal on the projector.
- [ ] Confirm a HTTPS push works with a personal access token on the demo machine.
- [ ] Merge one seeded PR or push a change to `LIVE.md` for Lab 03.
- [ ] Turn off notifications and Slack.
- [ ] Zoom the terminal to 18–20pt.
- [ ] Have `CHEATSHEET.md` open in a second tab.
- [ ] Watch chat during labs.
- [ ] Post the deck and repo links in the meeting chat at the start.

## Contingencies

| Problem | Response |
|---|---|
| Several people cannot install Git | Pair them with someone who is set up; share the cheat sheet. Do not debug one laptop in front of the room. |
| Lab 01 runs long | Skip the second commit; Lab 02 still teaches staging and committing. |
| GitHub is down | Demo locally, show `git log`, and walk through the PR flow on the slides. |
| Push asks for a password | Use a personal access token. GitHub does not accept account passwords. |
| PR shows many files | They cloned the wrong repo or selected the wrong base. Check `git remote -v` and the PR base/compare. |
| PR has a conflict | `git pull origin main`, resolve, push. Do not let it consume the room. |
| Someone commits to `main` in their fork | Fine for this lab; they can still open a PR. Explain branches as the habit. |

## Assessment

The artifacts are the assessment:

- Two local commits with the intern's name.
- A pushed branch on their fork.
- An open pull request against the base repo.
- A successful `git pull origin main`.

## Follow-up session ideas

- Merge conflicts: create one, resolve it, `git merge --abort`.
- Code review: useful comments and responding to review.
- Branching strategies: trunk-based vs Git Flow.
- Interactive rebase, force-with-lease, reflog.
- GitHub Issues, Projects, and Actions.
