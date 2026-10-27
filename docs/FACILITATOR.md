# Facilitator runbook

For the **Gitting Started** session. Slides: <https://gitting-started.sam1.space>

## Before the room opens

- [ ] Deck loaded on the projector; press `F` for fullscreen.
- [ ] Terminal open at a clean folder, font size 18–20pt.
- [ ] A HTTPS push works with a personal access token on the demo machine.
- [ ] Two browser tabs: the exercise repo and your fork.
- [ ] Notifications off.
- [ ] Second facilitator watching chat, if possible.
- [ ] Deck and repo links pasted into the meeting chat.
- [ ] `LIVE.md` has no update for today; you will add one during Lab 02.

## Run of show

| Time | Segment |
|---|---|
| 0:00 | Welcome and outcomes |
| 0:04 | Mental model |
| 0:09 | Install and configure |
| 0:16 | Commit anatomy and conventional commits |
| 0:20 | Lab 01 |
| 0:30 | Remotes and forks |
| 0:35 | Lab 02 |
| 0:50 | Pull and Lab 03 |
| 0:54 | Safety and undo |
| 0:58 | Recap and questions |

## During Lab 02: the merge queue

1. Watch the PR list at <https://github.com/Livewires-Digital-Solutions/gitting-started/pulls>.
2. Open a PR, check **Files changed** = 1, then **Merge pull request**.
3. Merge two or three PRs early so the room sees the merged state.
4. Push the live-notes update so Lab 03 has something to pull:

```bash
git clone https://github.com/Livewires-Digital-Solutions/gitting-started.git
cd gitting-started
printf -- '- %s — First PRs merged. Pull to see this line.\n' "$(date +%H:%M)" >> LIVE.md
git add LIVE.md
git commit -m "docs: update live notes"
git push
```

Or edit `LIVE.md` directly on GitHub and commit to `main`.

5. Leave the remaining PRs for after the session, or merge them while people are packing up. Every intern should get a merged PR.

## Demo reset

```bash
rm -rf /tmp/git-demo && mkdir /tmp/git-demo && cd /tmp/git-demo
git init
printf '# Demo\n' > README.md
git add README.md
git commit -m "chore: first commit"
git log --oneline
```

## Things that will happen

| Symptom | What is wrong | What to say |
|---|---|---|
| `git push` asks for a password | No token | "Use your personal access token. GitHub stopped accepting passwords." |
| `origin` is the fork | Cloned the fork instead of LiveWires | `git remote -v`; remove and re-clone the original |
| `fork` remote missing | Skipped `git remote add fork` | Add it, then push again |
| PR has 30 files | Wrong base or wrong branch | Check base/compare; redo the branch from `origin/main` |
| `nothing to commit` | File not saved | "Save the file, then `git status`." |
| `Author identity unknown` | Config missing | Run the two config commands; `git commit --amend --reset-author` for the last commit |
| `src refspec ... does not match any` | No commit on the branch | `git status`, `git log`, `git branch` |
| Push rejected | Origin moved | `git pull origin main`, then push |

## Rules for the facilitator

- Do not debug one laptop in front of the room.
- Narrate what you type: the command, then why.
- Show the error. A live `fatal:` message is more useful than a perfect demo.
- Stop talking during labs. Circulate.
- Protect the outcomes. If time is short, cut the undo table, never the install/config or push/PR steps.

## After the session

- Merge every remaining PR, even the imperfect ones.
- Send the deck, repo, and cheat sheet links.
- Optional follow-up: a 30-minute merge-conflict lab using two branches that edit the same line in `LIVE.md`.
