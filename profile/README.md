# Tently: AI code review for GitHub pull requests

[Tently](https://tently.dev) is an AI code reviewer for GitHub that finds regressions and
decision drift in pull requests. It checks every change against the code that depends on it and
against the architectural decisions your team has already made. It runs alongside your existing
AI code reviewer. It does not replace it.

Most AI reviewers read only the diff. Two kinds of problems live outside it:

- **Regressions.** A change breaks code that calls it, in files the pull request didn't touch.
- **Decision drift.** A change goes against a design decision the team made on purpose, like
  "all model calls go through the shared client".

Tently learns your team's decisions from merged pull requests, review threads and docs (ADRs,
READMEs, `CLAUDE.md`), your team approves them, and every pull request is checked against them.
Findings land on the PR as a check run and inline comments, with the evidence attached.

## One decision store, two gates

| Gate | When | How |
| --- | --- | --- |
| **Pull request review** | Every PR | The Tently GitHub App posts a check run and inline review comments |
| **Write time** | While Claude Code, Cursor or Codex writes code | [`@tently/mcp`](https://github.com/tently-team/tently-mcp): `npx @tently/mcp init` |

## Data handling

Tently never stores your source code. Each job clones with a short-lived installation token into
a temporary workspace that is deleted when the job ends. It stores only what it derives:
decisions, findings and metadata.

## Links

- Website: [tently.dev](https://tently.dev). Tently is in early access; join the waitlist there.
- Dashboard: [app.tently.dev](https://app.tently.dev)
- MCP server: [tently-team/tently-mcp](https://github.com/tently-team/tently-mcp) ·
  [npm](https://www.npmjs.com/package/@tently/mcp)
- Contact: [info@tently.dev](mailto:info@tently.dev)
