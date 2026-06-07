# Git Story Adventure

A collaborative "Choose Your Own Adventure" story used to practice core Git workflows: feature branches, pull requests, merging, and conflict resolution.

---

## Collaborators

| Role     | Responsibility |
|----------|----------------|
| Person A | Repo owner, initial story setup |
| Person B | Collaborator — added by Person A |

---

## The Exercise

You and your partner will each write a **different continuation** of the same story, on **separate branches**, then open pull requests and resolve the resulting merge conflict.

### The Story So Far

See [`story.txt`](./story.txt) for the opening. Your job is to continue it.

---

## Workflow Overview

```
main
 └── ending-a   ← Person A's story continuation
 └── ending-b   ← Person B's story continuation
```

Both branches edit `story.txt`. When both PRs are merged, a merge conflict will occur — and that's the point.

---

## Commit Message Format

This repo enforces **[Conventional Commits](https://www.conventionalcommits.org/)**. Every commit must follow:

```
<type>[optional scope]: <description>
```

Valid types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`

Examples:
- `feat(story): Sam heads to the lighthouse alone`
- `fix(story): resolve merge conflict combining both continuations`
- `chore: initial repo setup`

A `commit-msg` hook rejects messages that don't match. If your commit fails, read the error — it shows exactly what's expected.

---

## Step-by-Step Instructions

### Person A

1. Create a branch: `git checkout -b ending-a`
2. Open `story.txt` and append 4–5 sentences continuing the story (Sam goes to the lighthouse alone).
3. Commit: `git add story.txt && git commit -m "feat(story): Sam heads to the lighthouse alone"`
4. Push: `git push -u origin ending-a`
5. Open a Pull Request on GitHub: `ending-a → main`
6. **Do not merge yet** — wait for Person B to open their PR.
7. Once both PRs are open, merge Person A's PR first.
8. Then help Person B resolve the conflict (see below).

### Person B

1. Make sure you're on `main` and up to date: `git checkout main && git pull`
2. Create a branch: `git checkout -b ending-b`
3. Open `story.txt` and append 4–5 sentences continuing the story (Sam calls a friend instead).
4. Commit: `git add story.txt && git commit -m "feat(story): Sam calls a friend for help"`
5. Push: `git push -u origin ending-b`
6. Open a Pull Request on GitHub: `ending-b → main`
7. After Person A's PR is merged, your PR will show a conflict. Resolve it (see below).

---

## Resolving the Merge Conflict

After Person A's PR is merged, Person B should:

```bash
# Update your local main
git checkout main
git pull

# Switch back to your branch
git checkout ending-b

# Merge main into your branch to surface the conflict locally
git merge main

# Git will mark story.txt with conflict markers:
# <<<<<<< HEAD          ← your changes
# =======
# >>>>>>> main          ← Person A's changes

# Open story.txt, decide how to combine both continuations, remove all conflict markers
# Then:
git add story.txt
git commit -m "fix(story): resolve merge conflict combining both continuations"
git push

# The PR on GitHub will now be mergeable — merge it!
```

---

## Done?

Submit your GitHub repo link. The final `story.txt` on `main` should contain the opening paragraph plus both continuations woven together.
