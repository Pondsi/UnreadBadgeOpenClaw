# Changelog

## 1.1.3 — 2026-09-09

- SKILL.md now references the screenshot via an absolute URL: the registry
  resolves relative image paths against the page URL (not the artifact root),
  which broke the image on the skill page. GitHub-rendered docs keep relative
  paths.
- Added a license note in SKILL.md clarifying that the bundled LICENSE is
  MIT-style **with mandatory attribution**, even if registry metadata labels it
  "MIT-0".
- No script changes.

## 1.1.2 — 2026-09-09

- Added `screenshots/` with real sidebar captures (Chinese + English UI) and
  linked them from README / SKILL / 说明.md, so the badge style is visible at a
  glance.
- No script changes.

## 1.1.1 — 2026-09-09

Fixed a **resurrecting badge** bug in `scripts/unread-mark-keepalive.js`
(reported by the maintainer): after a mark had been read and cleared by the
gateway, the keep-alive could re-create it ~90 minutes later.

- Root cause: the read-time heuristic (`lastReadAt > created`) was evaluated
  first and the `agentStatus`-gone check additionally required `unread === false`.
  When the operator read the session at (or just before) the mark creation
  moment, the cleared mark was judged "unread" and renewed.
- Fix: the gateway is the owner of the mark — a missing `agentStatus` now always
  wins, so a cleared mark is never resurrected. Only marks still present on the
  gateway and not yet read are renewed.
- No other behavior changes; `unread-mark.js` is unchanged.

## 1.1.0 — 2026-09-09

Renamed to **UnreadBadgeOpenClaw** (ClawHub slug `unreadbadgeopenclaw`; the old
slug `session-unread-marks` keeps redirecting).

- Full documentation overhaul to the project release standard: 8-language
  README / SKILL / LICENSE / SPONSORS, Chinese 说明.md, GitHub issue templates
  and security policy, checksums, changelog.
- MIT-style license with mandatory attribution (Pondsi).
- No script behavior changes versus 1.0.0 — both scripts byte-identical.

## 1.0.0 — 2026-09-09

First release under the project name **UnreadBadgeOpenClaw** (previously
published on ClawHub as `session-unread-marks`; the old slug redirects here).

- `scripts/unread-mark.js` — set an unread badge on one session: flag icon +
  `[New reply] HH:mm` on success, alert icon + `[Failed] HH:mm` on failure;
  one atomic `sessions.patch` RPC; silent-fail (always exit 0).
- `scripts/unread-mark-keepalive.js` — renew live marks every 90 min to
  outlast the 120-min gateway TTL cap; 7-day hard fallback; drops records for
  read/gone/cleared sessions via `sessions.list` (no local DB dependency);
  `--dry-run` / `--limit` supported.
- `references/internals.md` — sidebar rendering-chain analysis, full list of
  native clear points, verification playbook.

Why an icon plus text: with "Show message preview" disabled, the sidebar only
renders the attention icon channel — a pure-text note is invisible. The icon
guarantees visibility; the note adds context.

---

Pondsi (+MiMo-v2.5/v2.5pro+deepseek-v4-flash/pro+deepseek-v4.1-flash-expires-on-0910+GLM5.3-flash+Gemini3.1-pro+Qwen3.8-27b+Gemini3.8-flash) — automatically committed by OpenClaw
