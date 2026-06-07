# CLAUDE.md — Git Story Adventure

This file is for **Person B's Claude agent**. It provides complete context and step-by-step instructions so the agent can execute this Git exercise with minimal friction.

---

## What This Repo Is

A collaborative "Choose Your Own Adventure" story used to practice:
- Feature branching
- Pull requests
- Merge conflicts and resolution

You are working as **Person B**. Person A owns the repo and has already set it up.

---

## Your Role (Person B)

You will:
1. Branch off `main`
2. Append a story continuation to `story.txt`
3. Commit and push
4. Open a Pull Request
5. Resolve a merge conflict after Person A's PR is merged
6. Merge your PR

---

## Repository Layout

```
main
├── story.txt        ← The shared story file — you will edit this
├── README.md        ← Human-readable instructions
└── CLAUDE.md        ← This file
```

---

## Git Workflow — Step by Step

### Step 1: Clone and verify

```bash
git clone <repo-url>
cd git-story-adventure
git log --oneline   # Should show Person A's initial commit
cat story.txt       # Read the opening paragraph before writing
```

### Step 2: Create your branch

Always branch off an up-to-date `main`:

```bash
git checkout main
git pull
git checkout -b person-b-branch
```

### Step 3: Write your story continuation

Open `story.txt` and **append** (do not replace) 2–3 sentences where Sam **calls a friend for help** instead of going to the lighthouse alone.

Keep the tone consistent with the opening. Do not alter any existing text — only add to the end.

### Step 4: Commit your changes

```bash
git add story.txt
git commit -m "Person B: Sam calls a friend for help"
```

Commit message format: short, present-tense, descriptive. One line is fine.

### Step 5: Push and open a Pull Request

```bash
git push -u origin person-b-branch
```

Then open a PR on GitHub: `person-b-branch → main`

- Title: `Person B: Sam calls a friend for help`
- Body: Brief description of what you added to the story
- Do NOT merge yet — wait for Person A to merge their PR first

---

## Handling the Merge Conflict

After Person A merges their PR, yours will show a conflict. Here is the exact resolution process:

### Step 1: Update main and merge it into your branch

```bash
git checkout main
git pull
git checkout person-b-branch
git merge main
```

Git will output something like:
```
Auto-merging story.txt
CONFLICT (content): Merge conflict in story.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### Step 2: Inspect the conflict

```bash
cat story.txt
```

You will see conflict markers in the file:

```
<<<<<<< HEAD
[Your sentences — Sam calls a friend]
=======
[Person A's sentences — Sam goes to the lighthouse alone]
>>>>>>> main
```

### Step 3: Resolve the conflict

Edit `story.txt` to combine both continuations into a coherent story. A good approach:
- Keep both paths — turn it into a true branching story (e.g., "Sam almost called a friend, but then decided to go alone...")
- Or weave them together narratively so the story flows naturally

**Remove all conflict markers** (`<<<<<<<`, `=======`, `>>>>>>>`). The file should read as clean prose when you're done.

### Step 4: Stage, commit, and push

```bash
git add story.txt
git commit -m "Resolve merge conflict: combine both story continuations"
git push
```

### Step 5: Merge the PR

Go to GitHub and merge your PR (`person-b-branch → main`). The conflict is resolved, so it should be mergeable now.

---

## Key Rules

- **Never force-push to main.** Main is the shared branch.
- **Never commit directly to main.** Always use a feature branch.
- **Always pull before branching.** Stale branches cause unnecessary conflicts.
- **Conflict markers must be fully removed** before committing a resolution. Git will reject the commit if they remain.
- **Only edit `story.txt`.** Do not modify README.md or CLAUDE.md unless instructed.

---

## Checking Your Work

Before declaring the task complete, verify:

```bash
# You are on main and it is up to date
git checkout main && git pull

# story.txt contains the full story: opening + both continuations, no conflict markers
cat story.txt
grep -E "(<<<<<<<|=======|>>>>>>>)" story.txt && echo "CONFLICT MARKERS STILL PRESENT" || echo "Clean"

# Your branch was merged (PR closed on GitHub)
git log --oneline | head -5
```

The GitHub repo link is the deliverable. Submit it once `main` contains the resolved, merged story.

---

## Useful Git Commands Reference

| Task | Command |
|------|---------|
| See current branch | `git branch` |
| See all branches | `git branch -a` |
| Check status | `git status` |
| See what changed | `git diff` |
| View commit history | `git log --oneline` |
| Abort a bad merge | `git merge --abort` |
| See remote PR status | `gh pr list` (requires GitHub CLI) |
| Open PR from CLI | `gh pr create --base main --head person-b-branch --title "..." --body "..."` |

---

## If Something Goes Wrong

**Accidentally committed to main:**
```bash
git log --oneline   # find the commit hash
git revert <hash>   # create a revert commit (safe, non-destructive)
git push
```

**Merge went wrong, want to start over:**
```bash
git merge --abort          # if merge is in progress
git checkout person-b-branch
git reset --hard origin/person-b-branch   # reset to last pushed state
```

**Branch is behind and conflicts are a mess:**
```bash
git checkout main && git pull
git checkout person-b-branch
git rebase main   # cleaner history than merge; resolve conflicts the same way
```

---

## Coordination Notes

- Communicate with Person A before merging. The exercise is designed so Person A merges first.
- If you are unsure whether Person A has merged yet, check: `git fetch && git log --oneline origin/main`
- The conflict is **intentional** — it is the point of the exercise, not a mistake to avoid.
