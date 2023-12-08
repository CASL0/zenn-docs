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
