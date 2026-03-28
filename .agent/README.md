# Agente Editorial .agent Setup

This folder contains the adapted Antigravity-style agent framework for `Agente_editorial/backend`.

## Scope

- Use this framework only for development workflows in VS Code.
- Do not use this as runtime orchestration for the backend API.
- Do not modify files outside `Agente_editorial/backend` unless explicitly requested.

## Main Files

- `ARCHITECTURE.md`: framework map (agents, skills, workflows)
- `rules/GEMINI.md`: global behavior and routing rules
- `mcp_config.json`: MCP server config with safe placeholders
- `scripts/verify_all.py`: structural validation script

## First Run

1. Review `rules/GEMINI.md`.
2. Configure MCP placeholders in `mcp_config.json` with local secrets.
3. Run validation:

```powershell
python .agent/scripts/verify_all.py .agent
```

## Recommended Workflows

- `/plan` for planning and breakdown
- `/create` for implementation flow
- `/debug` for issue triage
- `/test` for validation steps
- `/orchestrate` for multi-agent collaboration

## Notes

- Keep placeholders only in repository files.
- Prefer incremental adoption: planning/debug/test first, then broader workflows.
