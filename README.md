# 🦞 LGTM Lobster

A SOUL.md personality and configuration template for building a fun, opinionated GitHub PR agent with [OpenClaw](https://github.com/openclaw/openclaw).

Lobster monitors your repos, reviews PRs, triages issues, and keeps you in the loop — all while cracking the occasional claw pun.

## What's in the box

| File | Purpose |
|---|---|
| `SOUL.md` | Agent personality, workflows, autonomy rules, and state management |
| `HEARTBEAT.md` | Polling checklist — runs on a schedule via OpenClaw's heartbeat system |
| `config.example.yaml` | Template for your private config (tokens, repos, org) |
| `.gitignore` | Keeps secrets out of version control |

## How it works

Lobster runs on [OpenClaw's heartbeat system](https://docs.openclaw.ai/gateway/heartbeat). On each cycle (default: every 30 minutes), it:

1. Reads `HEARTBEAT.md` for what to check
2. Reads `MEMORY.md` (in the OpenClaw workspace) for what it's already seen
3. Queries the GitHub API for new activity
4. **Compares against state** — only notifies you about genuinely new stuff
5. Updates `MEMORY.md` with new high-water marks
6. If nothing changed: replies `HEARTBEAT_OK` and stays silent

**No duplicate notifications.** If Lobster already told you about a comment, it won't tell you again.

## Key concepts

### Autonomy Tiers
Lobster doesn't just YOLO every action. Every operation falls into one of three tiers:

- **Tier 1 — Act Freely**: Read-only stuff. Polling, analyzing, summarizing locally.
- **Tier 2 — Act, Then Notify**: Posts comments, adds labels, opens draft PRs — then tells you about it.
- **Tier 3 — Propose, Then Wait**: Approvals, merges, marking PRs ready — requires your explicit OK.

When in doubt, Lobster escalates.

### State Tracking
Lobster uses OpenClaw's file-based memory (`MEMORY.md` + daily logs) to track:
- Last poll timestamp
- Seen PR numbers and their latest comment/review/commit IDs
- Comments posted by the operator and their latest reply IDs

This prevents stale re-notifications and lets Lobster pick up exactly where it left off after a restart.

### Personality
Lobster is a teammate, not a linter. Expect:
- 🦞 Claw emojis
- Lobster puns (when they land naturally)
- Self-deprecating AI humor
- Zero snark toward teammates — constructive and respectful, always

## Getting started

LGTM Lobster is a **SOUL.md template** — it defines the agent's personality and rules. You'll need [OpenClaw](https://github.com/openclaw/openclaw) (or a compatible agent framework) to actually run it.

### 1. Set up OpenClaw
Follow the [OpenClaw installation guide](https://github.com/openclaw/openclaw#installation) to get the agent framework running on your machine or server.

### 2. Configure Lobster
```bash
cp config.example.yaml config.yaml
```
Edit `config.yaml` with your GitHub username, org, repos, and a [Personal Access Token](https://github.com/settings/tokens) with `repo` and `read:org` scopes.

### 3. Load the agent files
Copy `SOUL.md` and `HEARTBEAT.md` into your OpenClaw agent workspace directory (typically `~/.openclaw/workspace/`). Refer to the [OpenClaw SOUL.md docs](https://open-claw.me/configuration/soul) and [Heartbeat docs](https://docs.openclaw.ai/gateway/heartbeat) for exact paths.

### 4. Start the agent
Start OpenClaw as usual — Lobster will take it from there. On the first heartbeat cycle, it will build its initial state baseline silently, then start notifying you of new activity on subsequent cycles. 🦞

## Customization

The SOUL.md is yours to fork and modify. Some things you might want to adjust:
- **Autonomy tiers** — move actions between tiers based on your team's comfort level
- **Communication style** — dial the puns up or down
- **Workflows** — add or remove capabilities
- **Future integrations** — the Atlassian section is a placeholder, ready to fill in

## Security

This repo is designed to be public. All secrets and environment-specific values live in `config.yaml`, which is gitignored. The SOUL.md contains no org names, repo names, usernames, or tokens.

**Never commit `config.yaml`.**

## License

MIT
