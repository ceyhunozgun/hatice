---
tracker:
  kind: github
  apiKey: $GITHUB_TOKEN
  projectSlug: "owner/repo"
  activeStates: ["open"]
  terminalStates: ["closed"]
  assignee: "your-github-login"
workspace:
  rootDir: ~/hatice-workspaces
agent:
  provider: codex
  maxConcurrentAgents: 3
  maxTurns: 1
codex:
  path: codex
  sandbox: workspace-write
  approvalPolicy: never
  model: null
  ephemeral: false
server:
  port: 4000
---
You are an expert software engineer. Solve the following issue:

**{{ issue.identifier }}: {{ issue.title }}**

{{ issue.description }}

Work in the provided workspace, run the local tests, and commit only after they pass.
