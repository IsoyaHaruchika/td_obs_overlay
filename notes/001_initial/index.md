---
created: 2026-02-25 12:10
status: done
prev:
next:
  - "[[../002_twitch_chat/index]]"
source: "[[permanent/touchdesigner-obs-overlay]]"
---

# 環境構築とOBS連携検証

## 仮説

TouchDesigner（NON-COMMERCIAL版）からOBSへSpoutまたはNDI経由で映像を送り、オーバーレイとして合成できる。

## 評価基準

| 指標 | 目標値 | 現在値 |
|------|--------|--------|
| 映像連携 | 安定動作 | - |
| 遅延 | < 100ms | - |
| CPU負荷 | < 30% | - |

**成功条件**:
- TouchDesignerで作成した映像がOBSに表示される
- 透過（アルファチャンネル）が正しく機能する
- 長時間安定動作する

**失敗条件**:
- 映像が表示されない / 頻繁に切断される
- 遅延が大きすぎる（> 500ms）

## リサーチ

### 参考資料

- [TouchDesigner公式](https://derivative.ca/) - ダウンロード・ドキュメント
- [Spout](https://spout.zeal.co/) - Windows用テクスチャシェアリング
- [obs-spout2-plugin](https://github.com/Off-World-Live/obs-spout2-plugin) - OBS Spoutプラグイン
- [obs-ndi](https://github.com/Palakis/obs-ndi) - OBS NDIプラグイン

### 発見

（リサーチから学んだことを記録）

## タスク

### Phase 1: 環境構築

- [ ] TouchDesignerインストール（NON-COMMERCIAL版）
- [ ] Spoutインストール
- [ ] OBS Spout2プラグインインストール

### Phase 2: 接続テスト

- [ ] TouchDesignerでSpout出力を設定
- [ ] OBSでSpoutソースを追加
- [ ] 映像が表示されることを確認
- [ ] 透過テスト

### Phase 3: 基本オーバーレイ

- [ ] 簡単なテキスト表示
- [ ] 背景透過の確認
- [ ] 安定性テスト（30分連続）

## 実験ログ

（実験結果をここに追記）

## 結論

（完了時に記入）
