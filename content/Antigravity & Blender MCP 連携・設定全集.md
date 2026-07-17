---
categories:
  - "[[Posts]]"
author:
  - "[[Me]]"
url:
created: 2026-07-14
published:
topics: []
status:
---

## 1. Blender 側アドオンの準備

BlenderとMCPを通信させるためには、Blender側でサーバーからのリクエストを受け付けるアドオンが有効化されている必要があります。

1. **アドオンの確認:**
* Blenderを起動し、`Edit > Preferences > Add-ons` を開く。
* `Blender MCP`（または該当するアドオン）がインストールされ、チェックボックスがオンになっていることを確認。


2. **アドオンの設定:**
* アドオン設定内に「Listen Port」等の項目があれば、今回設定したポート番号（`9876`）と一致させてください。
* 「Auto-start on load」設定がある場合は有効にすると便利です。



## 2. MCP サーバーの常駐（ターミナル操作）

Antigravity IDEのビルドプロセスでタイムアウトを防ぐため、サーバーは必ずIDEの外側で立ち上げます。

```bash
# ターミナルで実行して常駐させる
uvx blender-mcp --port 9876

```

## 3. Antigravity IDE の設定

IDEの設定ファイル `mcp_config.json` を編集し、ローカルの常駐サーバーへ接続させる。

* **設定場所:** コマンドパレット（`Cmd + Shift + P`）から `Antigravity: Open MCP Configuration` を実行。
* **設定内容:**

```json
{
  "mcpServers": {
    "blender": {
      "command": "nc",
      "args": ["localhost", "9876"]
    }
  }
}

```

* **反映:** 保存後、Antigravity IDEを必ず再起動してください。

## 4. 連携の確認手順

以下の順序で実行することで、確実にBlenderへコマンドを送信できます。

1. **Blenderを起動**（アドオンが読み込まれている状態）。
2. **サーバーを起動**（ターミナルで `uvx blender-mcp --port 9876`）。
3. **Antigravityを起動**し、ステータスを確認（`Connected` を確認）。
4. Antigravityのチャットエージェントへプロンプトを送信。
* *例: "Create a default cube in Blender."*



## 5. トラブルシューティング

* **「Connection Refused」が出る場合:** ターミナルで `uvx blender-mcp` が停止していないか確認してください。
* **コマンドが送られていない場合:** Blender側の「System Console」（`Window > Toggle System Console`）を開き、コマンド受信ログが出ているか確認してください。
* **通信タイムアウト:** IDEのビルドプロセスと競合しているため、必ずサーバーを先に立ち上げてからIDEを起動する順序を守ってください。

---

これで環境の構築は完璧ですね。これで明日からはトラブルに時間を取られず、制作そのものに注力できるはずです。準備は万端ですが、他に気になっている機能や設定はありますか？