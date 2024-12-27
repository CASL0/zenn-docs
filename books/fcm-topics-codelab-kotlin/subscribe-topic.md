---
title: "トピックの購読/購読解除を実装する"
---

メッセージの内容をトピックで分類し、受信したいトピックを絞り込むことができます。

Android アプリ側で購読したいトピックを切り替える方法を実装していきます。

## トピックの購読を実装する

アプリ画面上に各トピックの購読・購読解除を呼び出すトグルが並んでいます。

`MainViewModel.kt`を開いてください。トグル切り替え時のイベントハンドラ内で呼び出される`subscribeToStockCategory`メソッドがプレースホルダーとなっているので、実装していきます。

[subscribeToTopic](<https://firebase.google.com/docs/reference/android/com/google/firebase/messaging/FirebaseMessaging?hl=ja#subscribeToTopic(java.lang.String)>) API を使用し、次のコードのように実装します。

```kotlin
FirebaseMessaging.getInstance().subscribeToTopic(topicName.toString())
                .addOnSuccessListener {
                    Log.i(
                            TAG,
                            "Subscribed to topic: $topicName"
                    )
                }
```

## トピックの購読解除を実装する

また、トグル切り替え時のイベントハンドラ内で呼び出され、購読解除を行う`unsubscribeFromStockCategory`メソッドを実装していきます。

[unsubscribeFromTopic](https://firebase.google.com/docs/reference/android/com/google/firebase/messaging/FirebaseMessaging?hl=ja#public-taskvoid-unsubscribefromtopic-string-topic) API を使用し、次のコードのように実装します。

```kotlin
FirebaseMessaging.getInstance().unsubscribeFromTopic(topicName.toString())
                .addOnSuccessListener {
                    Log.i(
                            TAG,
                            "Unsubscribed from topic: $topicName"
                    )
                }
```

次の章でトピックを指定し、メッセージをマルチキャストします。
