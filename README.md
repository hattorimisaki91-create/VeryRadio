# ラジオ【Very】無料枠・試験公開キット v0.7

既存v0.6のサーバーとAndroidソースに、DockerfileとRender Blueprint設定を追加した**デプロイ準備版**です。クラウドへの公開・Android APKのビルド・実端末間の音声疎通は未実施です。

## Renderでの試験公開手順（無料プランが選択できる場合）
1. このフォルダをGitHubの**非公開リポジトリ**に登録。銀行口座や秘密鍵を登録しないこと。
2. RenderのNew > Blueprintからリポジトリを選び、`render.yaml`を読み込む。無料プランが提供されない場合は作成を中止すること。
3. 公開されたURLの `/health` にアクセスし、`status: ok`と`payout_enabled: false`を確認。
4. `/rooms`でルーム一覧を確認し、`wss://<Renderが発行したホスト名>/ws`でWebSocket接続テスト。
5. Androidの `android/app/src/main/assets/index.html` 内の接続先URLを公開したWSS URLに設定し、Android Studioでビルド・端末2台でテスト。

## 制約・警告
- Render等の無料プランの提供条件・休眠・使用上限は変更されます。無料枠での常時接続や4時間連続配信は保証されません。
- このサーバーは**認証なし**。URLを知る第三者が接続できるため、身内の限定テスト以外に公開しないでください。
- SQLiteは一時領域で、再起動・再デプロイ時にデータが消えます。複数インスタンスでルーム状態を共有しません。
- WebRTCはシグナリングのみ。TURNサーバーなしでは回線によって音声接続が失敗します。
- いいねの不正防止は不十分。ポイントは試算のみ、**現金交換可能ポイントは常に0**。現金振込はできません。
- E〜Sランクと7日目からの毎日降格判定はサーバーに未統合です。
- 実際のAPKビルドにはAndroid SDK/Gradleが必要です。

## ローカルでの起動
```
docker build -t very-radio-trial .
docker run --rm -p 8000:8000 very-radio-trial
```
確認URL: http://localhost:8000/health
