# Excellence Lead Tools

Copilot agent and prompt files for MediVerse Engineering Excellence Leads (Team Forge & Team Connect).

## Files

- `excellence_lead.agent.md` — VS Code Copilot agent definition for daily operations dashboard
- `excellence_lead_daily_update.prompt.md` — Usage guide, labeling conventions, and JQL queries

## Setup

1. Copy the `.agent.md` file into your repo's `.github/instructions/` directory
2. Set up Jira labels as described in the prompt file
3. Invoke with: `@Excellence Lead — Give me my daily update for Team Forge.`

## Requirements

- VS Code with GitHub Copilot
- Atlassian MCP server configured
- Jira labels created per the labeling convention

See the [Confluence requirements page](https://teladochealth.atlassian.net/wiki/spaces/mediverse) for the full collaboration spec.
