---
created: 2026-02-25 12:20
status: active
prev: [[../001_initial/index.md]]
next:
  - [[../003_spec/index.md]]
---

# Twitchチャット取得方法のリサーチ

## 仮説

TouchDesignerでTwitchのチャットをリアルタイムに取得し、参加者管理システムに連携できる。

## 評価基準

| 指標 | 目標値 | 現在値 |
|------|--------|--------|
| 取得遅延 | < 1秒 | - |
| 安定性 | 3時間連続 | - |
| 実装難易度 | 中程度 | - |

**成功条件**:
- Twitchチャットをリアルタイムで取得できる
- 特定のコマンド（例: `!参加`）をフィルタリングできる
- TouchDesigner内でユーザー名を抽出できる

## リサーチ結果

### 方法1: TouchDesigner用コンポーネント（推奨）

既存のTouchDesigner用Twitchチャットコンポーネントが複数存在する。

#### Twitch Chat Component (by alphamoonbase)

**ダウンロード**: [OLIB](https://olib.amb-service.net/component/twitch-chat)

**セットアップ**:
1. OAuthトークンを取得: https://twitchapps.com/tmi/
2. パラメータを設定:
   - OAuth Token
   - Channel（配信チャンネル名）
   - Nickname（自分のアカウント名）
3. Activeをオンにする

**機能**:
- メッセージ送信: messageパラメータに入力してsendをパルス
- メッセージ受信: 受信したメッセージが出力にappend
- フィルタリング: キーワードテーブルで特定メッセージを検出
- コールバック:
  - `UnfilteredMessage`: 全メッセージで発火
  - `FilteredMessage`: フィルタ条件に一致した時に発火

#### Twitcher Component

**特徴**:
- 認証プロセスを内蔵（外部サイト不要）
- Twitch API v5対応
- PubSub API対応（チアー、サブスク、購入通知など）

### 方法2: WebSocket DAT で直接接続

TouchDesignerのWebSocket DATを使用してTwitch IRCに直接接続する方法。

**接続情報**:
- サーバー: `irc.chat.twitch.tv`
- ポート: `6667`（通常）/ `6697`（SSL）
- WebSocket: `wss://irc-ws.chat.twitch.tv:443`

**認証フロー**:
```
PASS oauth:<token>
NICK <username>
JOIN #<channel>
```

**PINGへの応答**:
Twitchは定期的に`PING`を送信。`PONG`で応答しないと切断される。

### 方法3: Python経由（外部プロセス）

TouchDesigner外部でPythonスクリプトを実行し、結果をTouchDesignerに渡す。

**ライブラリ**:
- [twitch-chat-irc](https://pypi.org/project/twitch-chat-irc/) - シンプルなIRCクライアント
- [python-twitch-irc](https://pypi.org/project/python-twitch-irc/) - 高機能IRC

**使用例**:
```python
from twitch_chat_irc import TwitchChatIRC

connection = TwitchChatIRC()
connection.listen('channel_name', on_message=callback)
```

## 比較

| 方法 | 難易度 | 安定性 | 機能 | 推奨度 |
|------|--------|--------|------|--------|
| Twitch Chat Component | 低 | 高 | 基本 | ★★★ |
| Twitcher | 中 | 高 | 高機能 | ★★☆ |
| WebSocket DAT直接 | 高 | 中 | カスタム可 | ★☆☆ |
| Python外部 | 中 | 中 | 柔軟 | ★☆☆ |

## 参加者検出のフロー案

```
Twitch Chat
    │
    ▼
┌─────────────────────┐
│ Twitch Chat Component│
│   (WebSocket DAT)    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  フィルタリング     │
│  "!参加" を検出     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  ユーザー名抽出     │
│  Table COMPに追加   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  オーバーレイUI更新 │
└─────────────────────┘
```

## 次のステップ

1. [ ] Twitch Chat Componentをダウンロード
2. [ ] OAuthトークンを取得
3. [ ] 接続テスト
4. [ ] `!参加` コマンドのフィルタリング実装
5. [ ] ユーザー名のTable COMP連携

## 参考資料

- [Twitch Chat in TouchDesigner - Interactive & Immersive HQ](https://interactiveimmersive.io/blog/touchdesigner-resources/twitch-chat-in-touchdesigner/)
- [Twitch Chat Component - Derivative](https://derivative.ca/community-post/asset/twitch-chat/63083)
- [Parsing Twitch Chat Commands in TouchDesigner](https://interactiveimmersive.io/blog/python/parsing-twitch-chat-commands-in-touchdesigner/)
- [twitch-chat-irc - PyPI](https://pypi.org/project/twitch-chat-irc/)
- [Twitch公式 chatbot-python-sample](https://github.com/twitchdev/chatbot-python-sample)

## 実験ログ

（実験結果をここに追記）

## 結論

（完了時に記入）
