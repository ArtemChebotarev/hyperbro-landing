---
name: commit-and-push
description: Commit the current change on a task branch, push it and open (or update) a pull request into main. Trigger with "commit and push", "commit this", "ship this", "open a PR", "пушь", or before any push to the hyperbro-landing repo.
---

# Commit and push

Invoking this skill is Artem's confirmation to commit, push the task branch and open its PR — don't ask again before those steps. It is **not** permission to merge: merging publishes the site, and Artem does it himself.

`main` is protected on GitHub (PR required, no direct or force pushes) — never commit on `main` or push to it.

## Steps

1. `git fetch origin`. If the current branch is `main`, fast-forward it (`git pull --ff-only`), then create a task branch (`feat/…`, `fix/…`, `copy/…`, `chore/…`). If already on a task branch, rebase it onto `origin/main` (or merge `origin/main` into it if the branch is already shared in an open PR).
2. Check the change once more in the local preview (`landing` config in `.claude/launch.json`): the changed pages at desktop and phone width, no console errors. Skip only for changes nothing renders (docs, `README.md`, `AGENTS.md`).
3. Review `git status` and `git diff`; stage only the files that belong to the task. Never commit `.DS_Store`, `.claude/settings.local.json`, `.claude/worktrees/`.
4. Commit with a message that says *why*, not just *what*.
5. `git push -u origin <branch>`.
6. If the branch has no PR yet, open one against `main` with `gh pr create`: a short summary of what changed on the site, what was checked, and screenshots or notes for visual changes. If a PR already exists, the push updates it.
7. Give Artem the PR link. Do not merge it and do not enable auto-merge unless he explicitly asks for this PR.

After Artem merges, Pages redeploys in about a minute; `git fetch origin` and fast-forward local `main` before the next task.
