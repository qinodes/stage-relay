# Stage Relay

[English](README.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md)

Stage Relay 是用於大型、多階段開發任務的進度追蹤 Skill。

它會將任務拆分成可開發、測試與驗收的階段，並把目標、進度、測試結果及驗收狀態記錄在專案中。即使更換 Session 或 Agent，也能依據記錄接續工作，不會遺失開發進度。

使用前需要安裝 Node.js 與 `npx`。

## Codex

### 安裝到專案

請在要使用此 Skill 的專案目錄中執行：

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent codex --yes
```

### 更新專案版本

在專案目錄中重新執行相同指令，即會以最新版本覆蓋已安裝的 Skill：

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent codex --yes
```

### 全域安裝

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent codex --global --yes
```

### 更新全域版本

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent codex --global --yes
```

## Claude Code

### 安裝到專案

請在要使用此 Skill 的專案目錄中執行：

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent claude-code --yes
```

### 更新專案版本

在專案目錄中重新執行相同指令，即會以最新版本覆蓋已安裝的 Skill：

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent claude-code --yes
```

### 全域安裝

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent claude-code --global --yes
```

### 更新全域版本

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent claude-code --global --yes
```
