# R&D INDEX

## プロジェクト概要

**開始日**: 2026-02-25

### ゴール

TouchDesignerを使って、Twitch配信用の汎用参加者管理オーバーレイシステムを構築する。
視聴者がコメントで参加希望を出し、配信者がMIDIコントローラーで管理する。

### スコープ

**対象**:
- TouchDesigner環境構築
- OBSとの映像連携（Spout/NDI）
- 参加者管理UI
- コメント連携
- 試合フロー管理

**対象外**:
- 配信プラットフォーム自体の開発
- 複数PC間の連携（Phase 1では）

### 評価基準

| 指標 | 目標値 | 説明 |
|------|--------|------|
| OBS連携安定性 | 3時間連続動作 | 配信中に落ちない |
| 参加者表示遅延 | < 1秒 | コメント→表示の遅延 |
| UI操作性 | 片手操作可能 | 配信中に操作しやすい |

**成功の定義**: 実際の配信で参加者管理オーバーレイとして使用できる

### 技術的制約

- ツール: TouchDesigner (NON-COMMERCIAL)
- 出力: OBS Studio
- 映像連携: Spout or NDI
- OS: Windows

### 優先度

1. [高] TouchDesigner → OBS 映像連携
2. [高] 参加者テーブルUI
3. [中] コメント自動取得
4. [中] 試合開始/終了フロー
5. [低] 演出エフェクト

---

## 現在のフォーカス

**アクティブノート**: なし（次: Step 2 OBS連携）

**状況**: Step 1完了、実装方針策定済み

---

## ノート一覧

| # | タイトル | ステータス | 概要 |
|---|----------|------------|------|
| 001 | [initial](notes/001_initial/index.md) | done | 環境構築とOBS連携検証 |
| 002 | [twitch_chat](notes/002_twitch_chat/index.md) | done | Twitchチャット取得方法のリサーチ |
| 003 | [spec](notes/003_spec/index.md) | done | システム仕様書 |
| 004 | [implementation](notes/004_implementation/index.md) | done | 実装方針 |

---

## 参考資料

- [[permanent/touchdesigner-obs-overlay]] - 事前調査まとめ
