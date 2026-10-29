---
description: Start or resume the gated SDLC through its single Orchestrator entry point.
argument-hint: Project idea, clarification answer, artifact approval, or release-action approval.
---

Delegate to the `sdlc-orchestrator` subagent (via the Agent tool) to run the SDLC Orchestrator, passing along: $ARGUMENTS

The orchestrator reads `.github/copilot-instructions.md`, `.github/sdlc-log.md`, `.github/sdlc-status.md`, `.claude/input/userstory.md`, and the existing artifacts, then resumes from the earliest incomplete stage. Do not regenerate approved work or pass a pending human approval gate.

If a project idea or clarification answer is supplied above, use it to update the current stage's work. If an artifact is approved, proceed only to the next permitted stage. If rejected, revise that artifact and resubmit it. Treat approvals for commit, push, remote PR creation, and merge as separate, explicit actions.

This command is the Claude Code CLI equivalent of `.claude/prompts/start-sdlc.prompt.md`, which is specific to the VS Code Local harness.
