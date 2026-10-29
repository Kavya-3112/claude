# Contact Management System — Claude Code entry point

This project runs a human-approved, gated SDLC controlled by the `sdlc-orchestrator` subagent. The full workflow rules live in `.github/copilot-instructions.md` — read that file before acting on any SDLC task; this file only orients you to where things are.

## Where to look first (in order)

1. `.github/sdlc-log.json` — concise resume checkpoint (current stage, status, next action)
2. `.github/sdlc-status.md` — current gate/approval status table
3. `docs/decisions/governance-log.md` — full decision/dispute history behind any status row (consult only when a specific entry needs it)
4. `.claude/input/userstory.md` — the approved project input (user stories, acceptance criteria)

## Entry point

Start or resume the SDLC via the `sdlc-orchestrator` subagent (`.claude/agents/sdlc-orchestrator.md`), e.g. with `/start-sdlc`. Specialist agents for each stage live in `.claude/agents/` and are restricted to their assigned stage — do not delegate outside the sequence `.github/copilot-instructions.md` defines.

## App

Client-only contact management web app (no backend). See `README.md` for install/dev/build/test commands.
