---
title: "AWS CDKのDevContainerテンプレート"
emoji: "🙋"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["devcontainer", "awscdk", "typescript", "vscode", "aws"]
published: true
---

AWS CDK を使って開発するときのテンプレートです。

VSCode の DevContainer をインストールすると開発を開始できます。

https://github.com/CASL0/aws_cdk_typescript_template

# 使い方

ホスト OS の環境変数に、`cdk deploy`用の AWS の IAM とリージョンを設定してください。

- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_DEFAULT_REGION

[aws_cdk_typescript_template](https://github.com/CASL0/aws_cdk_typescript_template)にアクセスし[Use this template]を選択し、新規リポジトリを作成してください。

作成したリポジトリを VSCode で開き、コマンドパレット（Ctrl+Shift+P）から[Dev Containers: Reopen in Container...]を実行し、下記コマンドを実行してください。

```sh
cdk bootstrap
```

開発を開始してください。
