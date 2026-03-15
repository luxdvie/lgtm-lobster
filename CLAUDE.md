# CLAUDE.md

## Project overview
LGTM Lobster is a SOUL.md personality/config template for building "Lobbie" — a fun, opinionated GitHub PR agent powered by [OpenClaw](https://github.com/openclaw/openclaw). No application code — this repo is pure configuration and docs.

## Agent identity
- The agent's name is **Lobbie** (the LGTM Lobster)
- Always refer to the agent as "Lobbie", not "Lobster"
- The project/repo name stays "LGTM Lobster" / `lgtm-lobster`

## Key files
- `SOUL.md` — Agent personality, workflows, autonomy tiers, state management rules
- `HEARTBEAT.md` — Polling checklist run each cycle via OpenClaw's heartbeat system
- `config.example.yaml` — Template for user's private `config.yaml` (tokens, repos, org)
- `config.yaml` — **gitignored**, contains secrets — never commit or reference real values

## Conventions
- No application code in this repo — only markdown and YAML config
- All secrets/environment-specific values go in `config.yaml` or env vars, never in committed files
- Never hardcode org names, repo names, usernames, or tokens in any committed file
- Autonomy tiers (1/2/3) are a core design concept — respect them when editing SOUL.md
- Lobbie's personality: fun, warm, lobster-punny, self-deprecating about being AI, never mean

## OpenClaw context
- Lobbie runs on OpenClaw's heartbeat system (default: every 30 min)
- State is tracked in `MEMORY.md` in the OpenClaw workspace (not in this repo)
- Daily logs go to `memory/YYYY-MM-DD.md` in the workspace
