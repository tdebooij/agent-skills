---
name: tim-pr-review
description: "Tim's personal PR review workflow. Checks a pull request against the 9to5-web-dev skill's conventions plus general correctness, security, and overengineering concerns, then walks Tim through issues one at a time in severity order with fix options. Use when Tim asks to review a PR, says '/tim-pr-review', or asks to check a branch/PR against 9to5-web-dev standards."
---

# Tim's PR Review

A personal, interactive review workflow — one issue at a time, in severity order, with fix options Tim picks from. Not a dump of findings; a conversation.

## 1. Resolve the target

- Argument given is a PR number, branch name, or GitHub PR link → use it directly.
- Argument is "current" or omitted and a branch is checked out that isn't main → review that branch's diff against main.
- Otherwise ask Tim for a PR number, branch, or GitHub link.
- The PR must already exist on GitHub — use `gh pr view`/`gh pr diff` to pull the diff and metadata, don't just diff local git state.

## 2. Review

Load the `9to5-web-dev` skill and check the diff against it first — that's the primary lens. On top of that, also flag:

- General correctness and security bugs (same bar as `/code-review`).
- Overengineering: prefer the simpler solution; flag unrequested abstractions, premature generalization, or complexity that isn't earning its place.
- Missing backend support: if the frontend is working around something the backend should provide (an endpoint, a field, a computed value), flag it as an issue to raise with the backend team — don't treat the workaround itself as the fix to suggest.

Classify each finding as **blocking**, **major**, or **minor**:
- **Blocking** — breaks functionality, a security issue, or violates a hard 9to5-web-dev rule. Must be fixed before merge.
- **Major** — meaningfully wrong pattern, real bug risk, or significant overengineering. Should be fixed.
- **Minor** — style, small inconsistency, nice-to-have simplification. Worth flagging, not worth blocking on.

## 3. Report the count, then go one at a time

Open with the tally: "Found N issues — X blocking, Y major, Z minor."

Then present findings **one at a time**, most severe first (blocking → major → minor; ties broken by whatever's most impactful). For each:

- A concise description of the issue (file:line, what's wrong, why it matters).
- The realistic options for fixing it (usually 2-3, including "leave as-is" when that's defensible). Lead with the option you'd actually pick and say why.

Present the fix options as a multiple-choice question (e.g. the built-in AskUserQuestion tool) rather than plain text, when the environment supports it. Do not move on to the next issue, or start implementing, until Tim has answered — no proceeding on an assumed or default choice.

Wait for Tim's choice. If he specifies something other than a listed option, treat that as the direction — implement it. Once implemented, show a brief confirmation of what changed, then move to the next issue. Don't batch multiple issues into one turn.

## 4. Browser review on request

If Tim says anything that reads as wanting to look at it live — "open the browser," "let me see it," "pull it up," "I want to check this visually" — open the built-in browser to the relevant page/PR so he can log in, inspect, and annotate. Don't wait for the exact phrase "browser."
