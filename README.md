# zenn-docs

Zenn の記事・本を管理します。

## Getting Started

コマンドパレット（Ctrl+Shift+P）から[Open Folder in Container]を選択し、DevContainer で開きます。

### 記事の作成

```sh
npx zenn new:article
```

### 本の作成

```sh
npx zenn new:book
```

### プレビュー

```sh
npx zenn preview
```

## Contributing

[husky](https://github.com/typicode/husky)の pre-commit を設定してください。

```sh
yarn prepare
```

### markdownlint の設定

既定値からの変更点を記載します。

#### MD013

1. `code_blocks`を false に変更
   - 理由：短い行が適さない言語があるため
