# kongctl-namespace

ブログ記事「[【kongctl】namespaceとtagの概念と使い方](https://qiita.com/fukafukaCat/items/b755ae14ea1ac187cfbd)」で作成したコードを保存しているリポジトリです。
## 概要

- namespaceとtagの挙動を確認できます。
- namespaceは指定しなければdefaultを指定します。namespaceに指定したもののみを操作対象とします。
  - 手動作成したものと、namespaceに指定されないものは操作対象外となります。
- tagは指定しなければすべてのEntityを対象とします。指定した場合は指定したtagが付与されているEntityのみを操作対象とします。
  - tagを指定する場合、tagに指定しなかったtagが付与されたEntityは操作対象外となります。

## 今回の環境
- decK 1.69.0
- kongctl 1.21.0
- Kong Konnect
- Ubuntu 24.04.5(WSL)

## フォルダ構成

```
.
├ gateway/       
│　├ namespace.yml         # namespace 手順#1
│　├ change-namespace.yml  # namespace 手順#2
│　├ tag.yml               # tag 手順#1
│　├ change-tag.yml        # tag 手順#2
│　└ reset-tag.yml         # tag 手順#3
├ namespace_1.yml          # namespace 手順#1
├ namespace_2.yml          # namespace 手順#2
├ tag_1.yml                # tag 手順#1
├ tag_2.yml                # tag 手順#2
└ tag_3.yml                # tag 手順#3
```

## 各ファイルの役割

| ファイル                 | decK/kongctl      | 役割 |
| -------------------- | -------------------- | --- |
| `namespace.yml`          | decK    | namespace_1.yml用 |
| `change-namespace.yml`   | decK    | namespace_2.yml用 |
| `tag.yml`                | decK    | tag_1.yml用 |
| `change-tag.yml`         | decK    | tag_2.yml用 |
| `reset-tag.yml`          | decK    | tag_3.yml用 |
| `namespace_1.yml`        | kongctl | defaultに2つとfuka-testに1つCPPを作成 |
| `namespace_2.yml`        | kongctl | fuka-test-cpのみ残す |
| `tag_1.yml`              | kongctl | 異なるtagを付与したEntityの作成 |
| `tag_2.yml`              | kongctl | 指定したtagのみに変更を適用 |
| `tag_3.yml`              | kongctl | key-auth以外のEntityを削除 |


## 実行コマンド例
```bash
kongctl plan --mode sync -f namespace_1.yml --output-file plan_1.json
kongctl diff --plan plan_1.json
kongctl sync --plan plan_1.json
```