---
name: handoff
description: Save the current coding session into a concise, verified HANDOFF.md in the project root so another AI agent can continue the exact task. Use when switching agents, nearing a usage limit, pausing work, or ending a session.
disable-model-invocation: true
---

# Handoff the current session

Create or replace `HANDOFF.md` in the current workspace/repository root. This file must be readable by another coding agent opening the same project.

## Procedure

1. **Establish the project root.** Prefer the Git worktree root (`git rev-parse --show-toplevel`). If Git is unavailable, use the opened workspace root. Save `HANDOFF.md` there, never only in an OS temp directory.
2. **Use the available conversation context.** Capture the user's actual goal, requirements, constraints, terminology, decisions, corrections, and the latest requested task. Do not claim to have reviewed the entire chat transcript if only part of it is available.
3. **Inspect the repository before writing.** Use available terminal and file tools to check:
   - current branch and `HEAD` commit;
   - `git status --short`;
   - relevant unstaged and staged diffs (`git diff` and `git diff --cached`);
   - files directly related to the active task;
   - relevant test/build results already produced in this session.
   Do not run destructive commands. Do not stage, commit, reset, stash, checkout, or modify application code.
4. **Separate evidence from assumptions.** Label important details as `Verified in repository`, `Established in conversation`, or `Unverified / needs checking`. Never invent test results, implementation status, file paths, decisions, or command output.
5. **Write a useful continuation brief, not a chat transcript.** Preserve exact requirements and values where changing them would matter. Summarize repetition. Reference existing specs, plans, ADRs, issues, commits, diffs, and other artifacts by path/URL instead of copying them.
6. **Make the next step executable.** Identify the exact task in progress, what remains, the immediate next action, relevant files to inspect, and how to verify the result. If work was interrupted mid-change, state precisely what is incomplete and what must not be overwritten.
7. **Protect privacy and work.** Redact credentials, tokens, passwords, private keys, personal data, and sensitive customer information. Do not copy `.env` contents or secrets from diffs. Mention secret-bearing file names only when needed, never their values.
8. **Keep it compact.** Aim for a one-screen summary where practical, but retain details required to resume accurately. Prefer bullets and paths over long explanations. Remove stale information from the previous handoff rather than blindly appending it.

## Required HANDOFF.md structure

# Project Handoff

- Generated: date/time and timezone only if known; otherwise date only or `unknown`.
- Project root:
- Git branch / HEAD:
- Working tree: clean / modified / unknown.
- Handoff focus: use the supplied argument if present; otherwise infer from the active task.

## 1. Goal and success criteria
The user's objective and what counts as done.

## 2. Requirements and constraints
Exact functional requirements, important values, preferences, boundaries, and things not to change.

## 3. Current state
- Completed (verified):
- In progress / partially implemented:
- Not started:
- Blockers / unresolved questions:

## 4. Repository evidence
List relevant changed/untracked files and a short description of their role. Summarize important diffs without copying large patches. State explicitly if Git/diff inspection was unavailable.

## 5. Decisions and context
Important decisions and reasons, including rejected approaches only when relevant. Attribute each item to repository evidence or conversation context.

## 6. Verification
Commands/tests actually run and their observed results. Clearly list checks not run. Never imply a check passed if it was not executed.

## 7. Exact next actions
Numbered, ordered steps for the next agent. Start with the immediate next action. Include relevant paths and verification criteria.

## 8. Suggested skills
Only name skills that are known to exist in the current project/environment and explain briefly why they may help. If none are known, write `None identified; inspect available skills before use.` Do not invent skill names.

## 9. Safety notes
Uncommitted user work, fragile areas, destructive operations to avoid, and any assumptions that must be checked before editing.

## Final checks
- Confirm `HANDOFF.md` exists at the project root and is not saved only in `%TEMP%`, `/tmp`, or another private location.
- Re-read the written file once for contradictions, missing next steps, and accidentally included secrets.
- Do not alter application code as part of handoff creation.
- Report the exact path and a brief summary. Do not claim that another agent has already received or loaded it.

## Optional argument
If the user supplies a focus after `/handoff`, treat it as the priority for the handoff, but still include other active work that would be dangerous to lose.
