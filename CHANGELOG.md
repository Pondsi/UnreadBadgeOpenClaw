# Changelog

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
