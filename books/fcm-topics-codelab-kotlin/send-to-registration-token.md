---
title: "特定の端末へプッシュ通知を送信する"
---

# スターターサーバーの構成

サーバーアプリは以下のエンドポイントを含んでいます。

- POST http://localhost:8090/api/v1/tokens/{token}/messages
  - FCM 登録トークンを指定し、当該端末へプッシュ通知を送信します。
- POST http://localhost:8090/api/v1/topics/{topic}/messages
  - トピックを指定し、同トピックを購読している端末にプッシュ通知を送信します。
- POST http://localhost:8090/api/v1/messages
  - トピック条件を指定し、条件を満たす端末にプッシュ通知を送信します。
  - `X-Topic-Condition`ヘッダにトピック条件を指定します（例：`'Technology' in topics || 'Automotive' in topics`）

主なコード

- `messages/controller/MessageController.kt`
  - 上記のエンドポイントを扱うコントローラー。
- `messages/service/MessageService.kt`
  - FCM のメッセージ送信処理を呼び出すユースケース層。
- `helper/message/FcmSender.kt`
  - `initFirebaseSDK`: firebase-admin SDK を初期化します。
  - `sendMessageToFcmRegistrationToken`: FCM 登録トークンを指定し、当該端末へプッシュ通知を送信します。
  - `sendMessageToFcmTopic`: トピックを指定し、同トピックを購読している端末にプッシュ通知を送信します。
    - スターターコードではプレースホルダーとなっています。（後に実装します）
  - `sendMessageToFcmTopicCondition`: トピック条件を指定し、条件を満たす端末にプッシュ通知を送信します。
    - スターターコードではプレースホルダーとなっています。（後に実装します）

# サービスアカウントを設定する

firebase-admin SDK が FCM API の呼び出しを認証できるようにサービスアカウントを次の手順でセットアップします。

1. Firebase コンソールを開きます。
2. [プロジェクトの概要 ⚙]>[プロジェクトの設定]>[サービスアカウント]>[新しい秘密鍵を生成]をクリックし、キーファイルをダウンロードします。
3. ダウンロードしたファイルを`service-account.json`にリネームし、`StockNewsServer/src/main/resources`に配置します。

# 登録トークンを指定して端末へプッシュ通知を送信する

[StockNewsServer](https://github.com/CASL0/fcm-topics-codelab-kotlin/tree/main/StockNewsServer)を IntelliJ IDEA で開き、[Run▷]をクリックしサーバーを起動してください。

Android アプリのログに出力されていた登録トークンを確認し、以下のコマンドで API をリクエストします。

```sh
curl --location 'http://localhost:8090/api/v1/tokens/[tokenを貼り付けてください]/messages' \
--header 'Content-Type: application/json' \
--data '{
    "title": "テストメッセージ",
    "body": "特定の端末へプッシュ通知を送信する - テスト"
}'
```

Android アプリがフォアグラウンドにある場合は logcat に以下のログが出力されます。

- `Notification received with data-payload {}, title テストメッセージ, body 特定の端末へプッシュ通知を送信する - テスト`

Android アプリがバックグラウンドにある場合は通知が表示されます。

![](https://storage.googleapis.com/zenn-user-upload/8d96c9954fbc-20231209.png)
