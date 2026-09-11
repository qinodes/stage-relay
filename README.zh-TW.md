# Stage Relay

[English](README.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md)

Stage Relay 是用於大型、多階段開發任務的進度追蹤 Skill。

它會將任務拆分成可開發、測試與驗收的階段，並把目標、進度、測試結果及驗收狀態記錄在專案中。即使更換 Session 或 Agent，也能依據記錄接續工作，不會遺失開發進度。

## 安裝

需要先安裝 Node.js 與 `npx`。

若要安裝到目前專案，請在要使用此 Skill 的專案目錄中執行：

```bash
npx skills add qinodes/stage-relay
```

全域安裝：

```bash
npx skills add qinodes/stage-relay --global
```

## 更新

```bash
npx skills update stage-relay
```

若為全域安裝，更新時加上 `--global`。
