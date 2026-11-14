---
name: resume
description: Resume a coding task from the project's HANDOFF.md. Reconcile the handoff with the actual repository and continue from the exact next action without overwriting newer work.
disable-model-invocation: true
---

# Resume from project handoff

Use `HANDOFF.md` in the current workspace/repository root as the starting brief. The repository and the latest user instructions remain the source of truth if they conflict with the handoff.

## Procedure

1. **Find the handoff.** Check `HANDOFF.md` at the Git worktree root, then the opened workspace root. If the user supplied a path, check that path first. Do not search unrelated folders or another project's files.
2. **Read the entire handoff.** Extract the goal, success criteria, constraints, current state, repository evidence, verification, exact next actions, and safety notes.
3. **Verify the live repository.** Before editing, inspect the project root, current branch/`HEAD`, `git status --short`, relevant staged/unstaged diffs, and the files named in the handoff. Check whether newer commits or edits have appeared since the handoff was generated.
4. **Reconcile differences.** The current code and Git state outrank stale handoff statements. Preserve all current user changes, including uncommitted and untracked files. Do not reset, checkout, stash, overwrite, or revert work merely to match the handoff.
5. **Restore task context.** Reconstruct the intended outcome from the handoff and the current conversation. Keep the user's exact requirements and constraints. Treat assumptions and unresolved questions as unverified until checked.
6. **Continue, don't restart.** Begin with the first still-valid item under `Exact next actions`. Do not rebuild completed features or perform unrelated refactors. If the next action is clear and safe, proceed with the work rather than asking the user to repeat the task.
7. **Verify changes.** Run relevant checks when available. Report actual results and checks not run. Do not claim success without evidence.
8. **Keep the handoff current.** After meaningful progress, update `HANDOFF.md` using the same structure as the handoff skill, or invoke `/handoff` if available. Preserve still-relevant context and remove stale status.

## If the handoff is missing or incomplete

- If no `HANDOFF.md` can be found, say so and ask for its location or the previous session's handoff content. Do not invent context.
- If the file exists but a key detail is missing, inspect the repository and available conversation first. Ask only for information that cannot be recovered safely.
- If the handoff is stale, explain the specific mismatch briefly and use the live repository state.

## Finish

Briefly state what you understood, what you continued, what changed, and the verification results. Do not claim access to another agent's private conversation history; only the handoff and accessible project artifacts are shared.
