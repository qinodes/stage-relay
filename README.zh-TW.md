# Stage Relay

[English](README.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md)

Stage Relay 是用於大型、多階段開發任務的進度追蹤 Skill。

它會將任務拆分成可開發、測試與驗收的階段，並把目標、進度、測試結果及驗收狀態記錄在專案中。即使更換 Session 或 Agent，也能依據記錄接續工作，不會遺失開發進度。

## 安裝

需要先安裝 Node.js 與 `npx`。

若要安裝到目前專案，請在要使用此 Skill 的專案目錄中執行：

```bash
npx skills add qinodes/stage-relay --skill stage-relay
```

出現 Agent 選擇畫面時：

- **Codex：** 不需要額外選擇，已包含在 `Universal (.agents/skills)`。
- **Claude Code：** 在 `Additional agents` 中移到 `Claude Code (.claude/skills)`，按 `Space` 勾選，再按 `Enter` 確認。

若要跳過選單並同時安裝給兩者：

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent codex claude-code
```

全域安裝：

```bash
npx skills add qinodes/stage-relay --skill stage-relay --global
```

## 更新

```bash
npx skills update stage-relay
```

若為全域安裝，更新時加上 `--global`。
