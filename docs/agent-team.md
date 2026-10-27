# Agent team

I will use this custom agent team to build Mona's Project Pulse dashboard. I will orchestrate the work with GitHub Copilot CLI in a Codespace.

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 5.5 (copilot) | Coordinates the specialist agents, assigns file scopes and phases, manages dependencies, and verifies the integrated result. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 5.5 (copilot) | Researches the project and creates an implementation plan with steps, file assignments, dependencies, parallel work, edge cases, and validation expectations. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.7 Flash (copilot) | Guides the dashboard's usability, accessibility, information hierarchy, interaction flow, responsive layout, and visual design. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements the assigned dashboard files and runnable app support, following existing patterns and validating the changes. | `.github/agents/coder.agent.md` |
