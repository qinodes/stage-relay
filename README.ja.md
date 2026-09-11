# Stage Relay

[English](README.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md)

Stage Relayは、大規模かつ複数段階にわたる開発タスクの進捗を管理するためのSkillです。

タスクを開発・テスト・受け入れ確認の各段階に分け、目標、進捗、テスト結果、承認状況をプロジェクト内に記録します。セッションやAgentが変わっても、進捗を失わずに作業を引き継げます。

## インストール

Node.jsと`npx`が必要です。

現在のプロジェクトにインストールする場合は、このSkillを使用するプロジェクトのディレクトリで実行します。

```bash
npx skills add qinodes/stage-relay
```

グローバルにインストールする場合：

```bash
npx skills add qinodes/stage-relay --global
```

## 更新

```bash
npx skills update stage-relay
```

グローバルインストールを更新する場合は、`--global`を追加してください。
