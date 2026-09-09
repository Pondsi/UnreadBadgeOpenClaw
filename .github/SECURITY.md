# Security Policy

## Reporting a vulnerability

Please **do not** open a public issue for a security problem.

Use GitHub's private vulnerability reporting instead:
<https://github.com/Pondsi/UnreadBadgeOpenClaw/security/advisories/new>

If that is not available to you, open a minimal issue asking for a private channel
**without any technical detail**, and the maintainer will reach out.

Please include, when you can:

- the version (see `CHANGELOG.md`) and host (OpenClaw / other agent harness);
- the exact command and the JSON result, redacted of secrets;
- a description of the impact and, if possible, a minimal reproduction.

## Scope

In scope: the published package — `SKILL.md`, `README.md`, `说明.md`,
`CHANGELOG.md`, `SPONSORS.md`, `LICENSE`, `checksums.txt`,
`scripts/*.js`, `references/*.md`, `sponsors/*`.

## Design boundaries worth knowing

- The scripts talk **only** to the local OpenClaw gateway RPC
  (`sessions.patch` / `sessions.list`) — no external network calls.
- The only file they write is the skill's own state file
  (`unread-marks.json` in the OpenClaw state directory).
- Both scripts **fail silently** (exit 0) by design; stdout lines
  (`[unread-mark] ...`, `[keepalive] ...`) are the debugging channel.
- State records contain session keys and timestamps only — never message
  content.

## Response

Reports are acknowledged as soon as possible. A fix is released with a new
patch version, the ClawHub audit for that version is re-run, and the changelog
entry names the issue without exposing the reporter.
