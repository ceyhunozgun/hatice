---
tracker:
  kind: github
  apiKey: $GITHUB_TOKEN
  projectSlug: "ceyhunozgun/agent-tests"
  activeStates: ["open"]
  terminalStates: ["closed"]
  assignee: "ceyhunozgun"
workspace:
  rootDir: /tmp/hatice-workspaces-preview
preview:
  enabled: true
  basePort: 3100
  host: 127.0.0.1
hooks:
  afterCreate: "gh repo clone ceyhunozgun/agent-tests . && npm install"
  beforeRun: "(PORT=\"$hatice_PREVIEW_PORT\" nohup node --watch src/index.js > .hatice-preview.log 2>&1 & echo $! > .hatice-preview.pid)"
  beforeRemove: "if [ -f .hatice-preview.pid ]; then kill $(cat .hatice-preview.pid) 2>/dev/null || true; fi"
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
- Create a branch named `hatice/issue-<number>` from `main` before making changes
- Run `npm test` locally and do not commit or publish anything unless all tests pass
- After tests pass, commit your changes with a clear message
- Push the branch to `origin`
- Create a GitHub pull request targeting `main`, with `Closes #<number>` in the body
- Keep the local app preview running while the task is active and mention its preview URL in the pull request description
- The preview server runs in watch mode: add the card first so it shows its red HTTP 404 state, then implement the endpoint and let the watcher reload the server so the card turns green without a manual restart
- Poll the endpoint every 1 second; on success show the returned value and the response `Date` header, and on failure show a prominent red `ERROR` with the HTTP status
- Prefer small, focused changes over large rewrites
