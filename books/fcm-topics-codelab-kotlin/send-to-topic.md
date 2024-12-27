---
title: "トピックを購読している端末にマルチキャストする"
---

## トピックメッセージ送信を実装する

`FcmSender.kt`を開いてください。トピックメッセージ送信用のメソッド`sendMessageToFcmTopic`がプレースホルダーとなっているので実装していきます。

`message`インスタンスに`setTopic`で引数で受けたトピック名を設定します。

```kotlin
val message = Message.builder()
            .setNotification(
                Notification.builder()
                    .setTitle(messageEntity.title)
                    .setBody(messageEntity.body)
                    .build()
            )
            .setTopic(topicName)
            .build()
return FirebaseMessaging.getInstance().send(message)
```

## トピックを購読した端末でプッシュ通知を受信する

トピックメッセージを送信し、当該トピックを購読している端末でプッシュ通知を受信することを確認します。

1. Android アプリを実行し、「Technology」トグルを有効に変更します。
   ![トグル切り替え](https://storage.googleapis.com/zenn-user-upload/58094528d196-20231210.png)
2. サーバーを起動し、次のコマンドで API をリクエストします。

   ```sh
   curl --location 'http://localhost:8090/api/v1/topics/Technology/messages' \
   --header 'Content-Type: application/json' \
   --data '{
    "title": "テストメッセージ",
    "body": "トピックを購読している端末にマルチキャストする - テスト"
   }'
   ```

3. Android 端末でプッシュ通知の受信を確認します。
   1. アプリがフォアグラウンドにある場合は logcat にログが出力されます。
   2. アプリがバックグラウンドにある場合は通知が表示されます。

## トピック条件メッセージ送信を実装する

トピックは論理演算子で組み合わせることができます。

1. `&&`：`'Technology' in topics && 'Automotive' in topics`とすると、`Technology`及び`Automotive`の両方を購読している端末にメッセージを送信します。
2. `||`：`'Technology' in topics || 'Automotive' in topics`とすると、`Technology`及び`Automotive`の少なくとも一方を購読している端末にメッセージを送信します。

`FcmSender.kt`を開いてください。トピック条件メッセージ送信用のメソッド`sendMessageToFcmTopicCondition`がプレースホルダーとなっているので実装していきます。

`message`インスタンスに`setCondition`で引数で受けたトピック名を設定します。

```kotlin
val message = Message.builder()
            .setNotification(
                Notification.builder()
                    .setTitle(messageEntity.title)
                    .setBody(messageEntity.body)
                    .build()
            )
            .setCondition(topicCondition)
            .build()
return FirebaseMessaging.getInstance().send(message)
```

## 条件を満たす端末でプッシュ通知を受信する

1. Android アプリを実行し、「Technology」及び「Automotive」トグルを有効に変更します。
   ![トグル複数切り替え](https://storage.googleapis.com/zenn-user-upload/bab1b1e842ce-20231210.png)
2. サーバーを起動し、次のコマンドで API をリクエストします。

   ```sh
   curl --location 'http://localhost:8090/api/v1/messages' \
   --header 'Content-Type: application/json' \
   --header 'X-Topic-Condition: '\''Technology'\'' in topics && '\''Automotive'\'' in topics' \
   --data '{
    "title": "テストメッセージ",
    "body": "トピックを購読している端末にマルチキャストする - トピック条件テスト"
   }'
   ```

3. Android 端末でプッシュ通知の受信を確認します。
   1. アプリがフォアグラウンドにある場合は logcat にログが出力されます。
   2. アプリがバックグラウンドにある場合は通知が表示されます。

また、「Automotive」トグルを無効に切り替えて、上記の API リクエストをしても、プッシュ通知を受信しないことを確認してください。
