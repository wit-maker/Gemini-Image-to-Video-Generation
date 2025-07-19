# kamuicode Workflows

Claude Code SDK と kamuicode MCP を活用したAI生成ワークフロー集

## 🌟 概要

GitHub ActionsでClaude Code SDKとkamuicode MCPを使用してAIコンテンツを生成するワークフローテンプレート集です。目的に応じて最適なワークフローを選択できます。

## 📦 ワークフロー一覧

### 🏗️ [Module Workflow](./module-workflow/)
モジュール化されたAI動画生成システム。再利用可能なコンポーネントとマルチエージェント協調により、高品質なコンテンツを効率的に生成します。

**⚠️ 注意**: モジュールは再利用性と品質向上のため継続的に調整される可能性があります。

### 🎵 [Music Video Workflow](./music-video-workflow/)
音楽と動画を統合した音楽動画を自動生成。Google Lyria + Imagen4 + Hailuo-02 Proの組み合わせ。

### 📹 [Video Workflow Template](./video-workflow-template/)
基本的な動画生成ワークフロー。学習用途や簡単な動画作成に最適。

### 🎬 [Video with Background Removal](./video-background-removal-workflow/)
背景除去機能を含む動画生成ワークフロー。

### 🔍 [Gemini I2V Analysis](./gemini-i2v-workflow/)
Gemini APIと連携した画像から動画生成の分析ワークフロー。

## 🚀 クイックスタート

1. **用途に合うワークフローを選択**
2. **該当フォルダのSETUP.mdを参照**
3. **必要なSecretsとMCP設定を追加**
4. **ワークフローを実行**

## 📋 ワークフロー選択ガイド

| 用途 | 推奨ワークフロー | 特徴 |
|------|------------------|------|
| 高品質・大規模生成 | Module Workflow | モジュール化、マルチエージェント |
| 音楽動画作成 | Music Video | 音楽+動画統合 |
| 学習・基本用途 | Video Template | シンプル、導入しやすい |
| 背景除去が必要 | Background Removal | 特殊処理対応 |
| 分析重視 | Gemini I2V | Gemini統合分析 |

## 🛠️ 必要な環境

- Claude Code SDK
- kamuicode MCP
- Anthropic API Key
- GitHub Actions

## 🤝 貢献

新しいワークフローテンプレートの追加やバグ修正のPRを歓迎します。

## 📄 ライセンス

MIT License

---

🤖 **Powered by [Claude Code SDK](https://docs.anthropic.com/en/docs/claude-code) & kamuicode MCP**