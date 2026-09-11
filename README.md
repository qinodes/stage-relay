# Stage Relay

[English](README.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md)

Stage Relay is a progress-tracking skill for large, multi-stage development tasks.

It divides work into development, testing, and acceptance stages while recording goals, progress, test results, and approval status in the project. This allows a new session or agent to continue the work without losing context.

## Install

Requires Node.js and `npx`.

To install for the current project, run this command from the project directory:

```bash
npx skills add qinodes/stage-relay
```

When prompted to select agents:

- **Codex:** No additional selection is needed. Codex is included in `Universal (.agents/skills)`.
- **Claude Code:** Under `Additional agents`, highlight `Claude Code (.claude/skills)`, press `Space` to select it, then press `Enter`.

To install for both without the interactive prompt:

```bash
npx skills add qinodes/stage-relay --agent codex claude-code
```

To install globally:

```bash
npx skills add qinodes/stage-relay --global
```

## Update

```bash
npx skills update stage-relay
```

Add `--global` when updating a global installation.
