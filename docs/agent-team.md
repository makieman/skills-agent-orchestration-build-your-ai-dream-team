# Agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate the work for Mona's Project Pulse dashboard.

| Agent | Model | Responsibility | Definition |
| --- | --- | --- | --- |
| Planner | Claude Opus 4.7 (copilot) | Researches the codebase, dependencies, edge cases, and turns them into an implementation plan. | `.github/agents/planner.agent.md` |
| Orchestrator | Claude Opus 4.7 (copilot) | Breaks the work into phases, delegates to specialist agents, and verifies the result fits together. | `.github/agents/orchestrator.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements code, fixes bugs, and keeps behavior explicit, deterministic, and testable. | `.github/agents/coder.agent.md` |
| Designer | Gemini 3.1 Pro (copilot) | Handles UI/UX, accessibility, visual clarity, and dashboard styling. | `.github/agents/designer.agent.md` |

