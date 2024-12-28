---
title: "準備"
---

## 必要なツール

次のツールをインストールしてください。

- [IntelliJ IDEA](https://www.jetbrains.com/idea/)
- [Android Studio](https://developer.android.com/studio?hl=ja)

## コードをセットアップ

starter コードをセットアップしてください。

```sh
git clone https://github.com/CASL0/fcm-topics-codelab-kotlin.git
cd fcm-topics-codelab-kotlin
git checkout starter
```

IDE でプロジェクトを開いてください。

- `StockNewsApp`を Android Studio で開いてください。
- `StockNewsServer`を IntelliJ IDEA で開いてください。

## Firebase の設定

### Firebase のプロジェクト作成

1. [Firebase コンソール](https://console.firebase.google.com/?hl=ja)を開き、「プロジェクトを追加」をクリックします。
2. プロジェクト名「StockNews」を入力し[続行]をクリックします。
   ![プロジェクト作成](https://storage.googleapis.com/zenn-user-upload/5cd3feef4011-20231127.png)
3. Google アナリティクスは本書では不要なので、「このプロジェクトで Google アナリティクスを有効にする」のチェックは外します。
4. [続行]>[プロジェクトの作成]をクリックします。

### プロジェクトにアプリを追加

1. [プロジェクトの概要 ⚙]>[プロジェクトの設定]>[全般]>[マイアプリ]>[アプリを追加]をクリックします。
2. Android のアイコンをクリックします。
   ![アプリ追加](https://storage.googleapis.com/zenn-user-upload/8d0141bd2f66-20231127.png)
3. 以下の値を入力します。

   - Android パッケージ名：io.github.casl0.stocknews
     （`StockNewsApp/app/build.gradle.kts`の applicationId）
   - アプリのニックネーム：空欄
   - デバッグ署名証明書 SHA-1：空欄
     ![アプリの登録](https://storage.googleapis.com/zenn-user-upload/c7533bfb0760-20231127.png)

4. [アプリの登録]をクリックし、google-services.json をダウンロードします。
5. ダウンロードした google-services.json を`StockNewsApp/app`ディレクトリに配置します。
