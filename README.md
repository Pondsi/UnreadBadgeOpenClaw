# UnreadBadgeOpenClaw

[![ClawHub](https://img.shields.io/badge/ClawHub-unreadbadgeopenclaw-blue)](https://clawhub.ai/pondsi/skills/unreadbadgeopenclaw)
[![License](https://img.shields.io/badge/License-MIT--style%20%2B%20attribution-green)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-OpenClaw%20Control%20UI-orange)](https://openclaw.ai)

Persistent **unread badges** for OpenClaw session rows in the Control UI
sidebar: a colored flag/alert **icon** plus a short timestamp **note**, set
when a reply completes or fails, cleared natively when you actually read the
session. Works even with "Show message preview" disabled.

## What it looks like

A finished reply puts a **flag** badge with the time on the session row; a
failure puts an **alert** badge. The mark stays until you actually read the
session — no sound needed to know where to look.

| 简体中文界面 | English UI |
|---|---|
| ![Sidebar unread mark (中文)](screenshots/sidebar-mark-zh.png) | ![Sidebar unread mark (English)](screenshots/sidebar-mark-en.png) |

## Which package should I install?

| | GitHub repo (this) | ClawHub artifact |
|---|---|---|
| Content | Full project: portable core + `.github/` (issue templates, security policy) + git metadata | Audited portable core only |
| Install | `git clone` + copy `scripts/` | `clawhub install unreadbadgeopenclaw` |
| Version | Same tag as ClawHub release | Same tag |
| Best for | Source browsing, issues, contributions | One-command install into OpenClaw |

Both contain the identical core: `scripts/unread-mark.js`,
`scripts/unread-mark-keepalive.js`, `references/internals.md`.

## Quick start

```bash
# Reply completed → flag icon + "[New reply] HH:mm"
node scripts/unread-mark.js --key <sessionKey> --event done

# Reply failed → alert icon + "[Failed] HH:mm"
node scripts/unread-mark.js --key <sessionKey> --event warn

# Keep unread marks alive past the 120-min TTL (run every 90 min, max 7 days)
node scripts/unread-mark-keepalive.js
```

Schedule the keep-alive with an OpenClaw automation, cron, or Task Scheduler.
Full parameter reference in [SKILL.md](SKILL.md); deep internals in
[references/internals.md](references/internals.md); 中文详细说明见
[说明.md](说明.md).

## Why the icon matters

The sidebar subtitle chain is
`attentionNote ?? agentStatusNote ?? runHeadline ?? messagePreview ?? subtitle`.
When "Show message preview" is off, only `attentionNote ?? headline` render —
a pure-text note becomes invisible. The `attention` **icon** rides a separate
always-rendered channel. This skill therefore always sets an icon (`flag` for
success, `alert` for failures) and treats the note as a bonus.

## Design principles

- **Silent failure** — every error path exits 0; a notification helper must
  never break the pipeline it reports for.
- **Native lifecycle** — no shadow state to "resurrect" read marks: opening
  the session, sending a new message, TTL expiry, and the 7-day fallback are
  the only clear points.
- **Portable core** — two Node scripts, no dependencies, cross-platform path
  discovery for the local `openclaw` CLI. State stays in
  `$OPENCLAW_STATE_DIR/unread-marks.json` (default `~/.openclaw`).

## Compatibility

OpenClaw with the `sessions.patch` / `sessions.list` gateway RPC (current
stable). Windows / macOS / Linux.

## Sponsors

If you find this helpful, consider supporting its development — see
[SPONSORS.md](SPONSORS.md).

## License

MIT-style with mandatory attribution — see [LICENSE](LICENSE).

---

Pondsi (+MiMo-v2.5/v2.5pro+deepseek-v4-flash/pro+deepseek-v4.1-flash-expires-on-0910+GLM5.3-flash+Gemini3.1-pro+Qwen3.8-27b+Gemini3.8-flash) — automatically committed by OpenClaw
