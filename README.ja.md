# Stage Relay

[English](README.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md)

Stage Relayは、大規模かつ複数段階にわたる開発タスクの進捗を管理するためのSkillです。

タスクを開発・テスト・受け入れ確認の各段階に分け、目標、進捗、テスト結果、承認状況をプロジェクト内に記録します。セッションやAgentが変わっても、進捗を失わずに作業を引き継げます。

`npx`でインストールする場合は、事前に[Node.jsと`npx`](NODEJS_SETUP.md)が必要です。Skillファイルを直接コピーする場合は必要ありません。

## 🤖 Codex

### プロジェクトにインストール

このSkillを使用するプロジェクトのディレクトリで実行します。

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent codex --yes
```

### プロジェクト版を更新

プロジェクトのディレクトリで同じコマンドを再実行すると、インストール済みのSkillが最新バージョンに置き換わります。

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent codex --yes
```

### グローバルにインストール

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent codex --global --yes
```

### グローバル版を更新

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent codex --global --yes
```

## 🟠 Claude Code

### プロジェクトにインストール

このSkillを使用するプロジェクトのディレクトリで実行します。

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent claude-code --yes
```

### プロジェクト版を更新

プロジェクトのディレクトリで同じコマンドを再実行すると、インストール済みのSkillが最新バージョンに置き換わります。

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent claude-code --yes
```

### グローバルにインストール

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent claude-code --global --yes
```

### グローバル版を更新

```bash
npx skills add qinodes/stage-relay --skill stage-relay --agent claude-code --global --yes
```
