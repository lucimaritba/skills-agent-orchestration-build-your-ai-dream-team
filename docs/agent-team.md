# Agent team

I will use this custom agent team to build Mona's Project Pulse dashboard. GitHub Copilot CLI in a Codespace will orchestrate the work.

- **Planner** (Claude Opus 4.7): researches the repository, dependencies, documentation, and edge cases, then creates an implementation plan. Definition: `.github/agents/planner.agent.md`.
- **Designer** (Gemini 3.1 Pro): shapes the dashboard's user experience, accessibility, information hierarchy, interactions, visual clarity, and responsive behavior. Definition: `.github/agents/designer.agent.md`.
- **Coder** (GPT-5.5): implements the assigned application logic and files, follows existing patterns, and validates the changes. Definition: `.github/agents/coder.agent.md`.
- **Orchestrator** (Claude Opus 4.7): coordinates the specialists, assigns file scopes and phases, manages parallel or sequential work, and verifies the integrated result. Definition: `.github/agents/orchestrator.agent.md`.
