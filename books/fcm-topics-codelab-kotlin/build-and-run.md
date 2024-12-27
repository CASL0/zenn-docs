---
title: "スターターアプリをビルド・実行する"
---

## スターターアプリの構成

- `MainActivity.kt`
  - ViewModel を読み込んで`StockNewsApp`コンポーザブルを表示します。購読/購読解除したいトピックのトグルがリスト表示されています。
- `MainViewModel.kt`
  - `StockNewsApp`に対応する ViewModel で、UiState ホルダーです。購読/購読解除してるトピックの状態を保持します。
  - `toggleSubscribed`はトピックのトグル更新時に呼び出されるメソッドです。トピックの購読するためのメソッド`subscribeToStockCategory`および購読解除するためのメソッド`unsubscribeFromStockCategory`はプレースホルダーになっています。本書の後半でこれらのメソッドを実装します。
- `StockNewsApplication.kt`

  - `onCreate`で FCM の登録トークン作成処理を実行してます。作成した登録トークンをログに出力しています。

    ```kotlin
    FirebaseMessaging.getInstance().token.addOnCompleteListener {
              if (it.isSuccessful) {
                  Log.i(
                          TAG,
                          "FCM Registration Token is: ${it.result}"
                  )
              } else {
                  Log.i(
                          TAG,
                          "FCM Registration failed",
                          it.exception
                  )
              }
          }
    ```

- `StockNewsMessagingService.kt`

  - FCM からのメッセージ受信処理を含む`FirebaseMessagingService`を継承したクラスです。**通知を自動的に表示する機能**を含んでいます。
  - `onNewToken`: FCM 登録トークンが作成または更新されるときに呼び出されます。

    - 本アプリではトークンをログ出力しています。

      ```kotlin
      override fun onNewToken(token: String) {
        super.onNewToken(token)
        Log.i(
          TAG,
          "FCM Registration Token created or refreshed: $token"
        )
      }
      ```

  - `onMessageReceived`: メッセージが受信され、アプリがフォアグラウンドにあるときに呼び出されます。

    - 本アプリでは受信したメッセージ内容をログ出力しています。

      ```kotlin
      override fun onMessageReceived(message: RemoteMessage) {
        super.onMessageReceived(message)
        Log.i(
          TAG,
          "Notification received with data-payload ${message.data}, title ${message.notification?.title}, body ${message.notification?.body}"
        )
      }
      ```

- `model/StockCategories.kt`
  - ストックカテゴリとそれを識別するトピック名のリスト。

## アプリを実行し FCM 登録トークンを作成する

[StockNewsApp](https://github.com/CASL0/fcm-topics-codelab-kotlin/tree/starter/StockNewsApp)を
Android Studio で開き、[Run▷]をクリックしアプリを実行してください。

アプリ起動時に、FCM の登録トークン作成処理が走ります。
Logcat に以下のようなログが出力されるので、作成された登録トークンを確認します。

```text
FCM Registration Token is: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
