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
1. `tables`を false に変更
   - 理由：可読性のため、インデントで表のカラムをそろえることがあるため
1. `line_length`を 120 に変更（既定値 80）
   - 理由：URL を含んだ行など、80 だと少ないため

#### MD034

zenn は bare url からリンクカードを作成するため
