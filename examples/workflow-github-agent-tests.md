---
tracker:
  kind: github
  apiKey: $GITHUB_TOKEN
  projectSlug: "ceyhunozgun/agent-tests"
  activeStates: ["open"]
  terminalStates: ["closed"]
  assignee: "ceyhunozgun"
workspace:
  rootDir: /tmp/hatice-workspaces
hooks:
  afterCreate: "gh repo clone ceyhunozgun/agent-tests . && npm install"
polling:
  intervalMs: 15000
agent:
  provider: codex
  maxConcurrentAgents: 3
  maxTurns: 1
codex:
  path: codex
  sandbox: workspace-write
  approvalPolicy: never
server:
  port: 4000
---
You are an expert software engineer working on the **agent-tests** Node.js sample project.

Solve the following GitHub issue:

**{{ issue.identifier }}: {{ issue.title }}**

{{ issue.description }}

## Instructions
- Work in the provided workspace directory
- Implement the requested function in `src/lib.js`
- Keep existing working helpers (`add`, `greet`) intact
- Run `npm test` and make sure all tests pass
- Commit your changes with a clear message when done
- Prefer small, focused changes over large rewrites
