Language: [🇺🇸](./README.md) [🇯🇵](./README.ja.md)

[![Deploy](https://github.com/yKicchan/awesome-marp-template/actions/workflows/deploy.yml/badge.svg)](https://github.com/yKicchan/awesome-marp-template/actions/workflows/deploy.yml)

# Awesome Marp Template

このリポジトリは [Marp](https://marp.app/) を最強に活用したスライドを、超簡単に作成できるテンプレートリポジトリです。

## 🚀 機能一覧

- 🚀 [GitHubActions](./.github/workflows/deploy.yml) による [GitHubPages](https://yKicchan.github.io/awesome-marp-template/) への自動デプロイ
- 🖼️ タイトルスライドの OGP 画像設定サポート
- 🚄 Markdown 拡張構文による軽量なスライド作成
- 🎨 CSS ユーティリティクラスによる多彩なスライド表現
- 🔧 新しいスライドをテンプレートから簡単に作成できるスクリプト

このリポジトリを利用したデモスライドは [GitHubPages](https://yKicchan.github.io/awesome-marp-template/demo) を参照してください。  
Markdown 拡張構文や CSS ユーティリティクラスを使って、あなただけのオリジナルスライド環境を構築しましょう！

## 📂 ディレクトリ構造

主要なディレクトリとファイルの内容は以下の通りです。  
必要に応じて自分好みにカスタマイズしてください！

```plaintext
.
├── .marprc.yml     # Marp CLI の設定ファイル
├── engine.mjs      # Marp CLI の Engine 拡張
├── scripts/
│   ├── check       # スライドの OGP の URL が正しいかチェックするスクリプト
│   ├── init        # リポジトリのセットアップを行うスクリプト
|   └── new         # 新しいスライドをテンプレートから作成するスクリプト
├── src/            # スライド用のディレクトリで、デプロイされる
│    └── demo/      # デモ用のスライドディレクトリ
├── template/       # テンプレートスライド用ディレクトリ
└── themes
    ├── global.css  # スライド全体に影響させるカスタムテーマ
    ├── index.css   # カスタムテーマのエントリーポイント
    └── utility.css # スライドで利用する各種ユーティリティクラス
```

## ✅ 必須要件

| ツール                            | バージョン   |
|--------------------------------|---------|
| [Node.js](https://nodejs.org/) | 20.18.0 |
| [pnpm](https://pnpm.io/)       | 9.15.1  |

> [!tip]
> Node.js は [nodenv](https://github.com/nodenv/nodenv) 等のバージョンマネージャを使ったインストールを推奨します。

## 🎉 使い方

### 0. リポジトリの作成

1. [テンプレートからリポジトリを作成する](https://docs.github.com/ja/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template#creating-a-repository-from-a-template) を参考にリポジトリを作成します
2. GitHubActions から GitHubPages にデプロイできるように [ドキュメント](https://docs.github.com/ja/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%A0-github-actions-%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%95%E3%83%AD%E3%83%BC%E3%81%AB%E3%82%88%E3%82%8B%E5%85%AC%E9%96%8B) に従ってリポジトリの設定を変更します
3. GitHub 上での設定が完了したら `$ git clone` でローカルにリポジトリをダウンロードします

### 1. リポジトリのセットアップ

- リポジトリ内に存在する URL などの各種設定を、あなたの ID やリポジトリ名に変更します
- 簡単に変更できるよう [専用のスクリプト](./scripts/init) を用意しました

```bash
$ scripts/init
```

- 表示される内容に従って、あなたの GitHub ユーザーID と Repository 名を入力してください
  - 入力が完了すると、スクリプトが自動で設定を変更します
- 必要に応じて追加で言語やタイムゾーンを変更してください
  - [.marprc.yml](./.marprc.yml) には言語の設定が、[.github/workflows/deploy.yml](./.github/workflows/deploy.yml) にはタイムゾーンの設定が記述されています

> [!warning]
> スクリプト内で `sed` コマンドを使用しています。  
> Mac (BSD) では問題ありませんが、Linux (GNU) ではオプションの指定が異なるためエラーが発生する可能性があります。  
> Linux (GNU) ユーザーは[スクリプト内の `sed` コマンド](https://github.com/yKicchan/awesome-marp-template/blob/main/scripts/init#L55-L66)を適宜修正してください。

### 2. 依存関係のインストール

[Marp CLI](https://github.com/marp-team/marp-cli) や [markdown-it](https://github.com/markdown-it/markdown-it) の各種プラグインを利用可能にするため、依存関係をインストールします。

```bash
$ pnpm install
```

### 3. スライドの作成

- `src` ディレクトリ内にスライドを作成します
- [テンプレート](./template) から新しいスライドを簡単に作成できる [コマンド](./scripts/new) を用意しました

```bash
# 新しいスライドを作成する
$ pnpm new <slidename>
# グルーピングしたい場合は src 下ディレクトリを分割して作成することも可能
$ pnpm new path/to/<slidename>
```

コピー元となるテンプレートスライドは [template](./template) ディレクトリ内に存在します。  
ぜひ自分好みにカスタマイズしてください！

### 4. スライドの編集・確認

スライドは [Marp CLI](https://github.com/marp-team/marp-cli) の機能を利用して、ブラウザ上でリアルタイムに確認できます。

```bash
# src ディレクトリ下のスライドを編集する場合
$ pnpm dev
# テンプレートスライドを編集する場合
$ pnpm dev:tmp
```

> [!warning]
> このリポジトリは [Marp CLI](https://github.com/marp-team/marp-cli) の [Engine](https://github.com/marp-team/marp-cli?tab=readme-ov-file#engine) 機能を使って拡張しています。  
> そのため VSCode 拡張機能の [`marp-vscode`](https://github.com/marp-team/marp-vscode) が一部利用できません。  
> 詳しくは [@marp-team/marp-vscode/issues/85#issuecomment-543798586](https://github.com/marp-team/marp-vscode/issues/85#issuecomment-543798586) を参照してください。

以上で基本的な使い方は終了です！🎉

## 🙌 Marp をもっと楽しむ 🙌

Marp は [Marpit](https://marpit.marp.app/) の機能を使ってスライドのデザインをカスタマイズすることができます。  
また、 [Marp CLI](https://github.com/marp-team/marp-cli) の [Engine](https://github.com/marp-team/marp-cli?tab=readme-ov-file#engine) 機能を使って、Markdown の構文を拡張することも可能です。

このリポジトリでは主に下記2点でカスタムしています。

- [themes](./themes) ディレクトリ内の CSS ファイルで、デザインのカスタマイズとユーティリティクラスの定義
- [markdown-it](https://github.com/markdown-it/markdown-it) の各種プラグインを利用して、Markdown 構文を拡張  

それぞれ詳しい使い方を以下に記述します。

### テーマのカスタマイズ

- テーマの定義は [themes/index.css](./themes/index.css) に記述しています
  - 例えば Marp のデフォルトのテーマを変更したり、 (後述する[`markdown-it-prism`](https://github.com/jGleitz/markdown-it-prism)の導入によって可能となった) Syntax highlighting のスタイルを変更する場合に編集してください
- スライド全体に影響を与える追加のカスタムテーマは [themes/global.css](./themes/global.css) に記述しています
  - これを編集して、自分だけのオリジナルテーマを作成しましょう！
- スライドで利用できる便利なユーティリティクラスは [themes/utility.css](./themes/utility.css) に記述しています
  - 例えばテキストのサイズを変更したり、要素の列表示に対応するためのクラスを追加しています
  - デフォルトで便利な CSS クラスをいくつか用意していますが、必要に応じて自分好みにカスタマイズしてください！

> [!tip]
> ユーティリティクラスの設計は [Tailwind CSS](https://tailwindcss.com/) が参考になります

### Markdown 拡張構文の利用

Markdown 拡張の設定は [engine.mjs](./engine.mjs) に記述しています。  
おすすめの [markdown-it](https://github.com/markdown-it/markdown-it) プラグインを導入済みです。

- [`markdown-it-container`](https://github.com/markdown-it/markdown-it-container)
- [`markdown-it-attrs`](https://github.com/arve0/markdown-it-attrs)
- [`markdown-it-mark`](https://github.com/markdown-it/markdown-it-mark)
- [`markdown-it-ins`](https://github.com/markdown-it/markdown-it-ins)
- [`markdown-it-prism`](https://github.com/jGleitz/markdown-it-prism)
- [`markdown-it-textual-uml`](https://github.com/manastalukdar/markdown-it-textual-uml)

それぞれのプラグインについては公式ドキュメントを参照してください。

## ✨究極の Marp スライド作成術✨

最後にこのリポジトリの真髄である Markdown 拡張構文と、カスタムテーマの合体奥義を紹介します💪  
実際の表示は [デモスライド](https://yKicchan.github.io/awesome-marp-template/demo) で確認できます。

### `{.class}` で CSS クラスの付与

[`markdown-it-attrs`](https://github.com/arve0/markdown-it-attrs) の機能を利用して、特定の要素に CSS クラスを付与することができます。

```markdown
This is a paragraph.{.gray}
```

この入力は以下の HTML に変換されます。

```html
<p class="gray">This is a paragraph.</p>
```

`.gray` クラスは [themes/utility.css](./themes/utility.css) に定義している文字色をグレーにするクラスです。  
これにより、スライド内で特定の要素に対して簡単にスタイルを適用することができます。  
以下のように複数のクラスを同時に指定することも可能です。

```markdown
This is a small and gray paragraph.{.text-sm .gray}
```

### `==` と `{.class}` で特定の文字列のみ装飾する

[`markdown-it-mark`](https://github.com/markdown-it/markdown-it-mark) と [`markdown-it-attrs`](https://github.com/arve0/markdown-it-attrs) の合わせ技で、特定の文字列のみを装飾することができます。

```markdown
This is a ==red=={.red} text.
```

この入力は以下の HTML に変換されます。

```html
<p>This is a <mark class="red">red</mark> text.</p>
```

[`markdown-it-mark`](https://github.com/markdown-it/markdown-it-mark) によって `==` で囲った特定の文字列をインライン要素 `<mark>` にし、そこにクラスを付与することで、特定の文字列のみを簡単に装飾することができます。

### [`markdown-it-container`](https://github.com/markdown-it/markdown-it-container) でブロックごとにスタイルを変更する

`:::`  で囲むことで、ブロックごとにスタイルを変更することができます。  
このリポジトリでは `:::c` と `:::_` をあらかじめ用意しています。

#### `:::c` で列表示

```markdown
:::c
Column 1

Column 2

Column 3
:::
```

この入力は以下の HTML に変換されます。

```html
<div class="c">
  <p>Column 1</p>
  <p>Column 2</p>
  <p>Column 3</p>
</div>
```

`.c` クラスは [themes/utility.css](./themes/utility.css) に定義している `flex-container` の設定です。  
これにより、スライド内で列挙された要素を簡単に列表示にすることができます。

#### `:::_` でグルーピング

```markdown
:::_
Group 1

Group 2

Group 3
:::
```

この入力は以下の HTML に変換されます。

```html
<div class="_">
  <p>Group 1</p>
  <p>Group 2</p>
  <p>Group 3</p>
</div>
```

`._` クラスは**未定義のダミークラス**です。  
具体的なユースケースは、複数の要素に一括でスタイルを適応する場合や、スタイルを変更したくはないがグルーピングのみ行いたい時に活躍します。

```markdown
:::_ {.blue}
This is a blue text.

This is a blue text.

This is a blue text.
:::
```

```markdown
::::c
:::_
## Left column
This is a left column text.
:::
:::_
## Right column
This is a right column text.
:::
::::
```

なお、上記のようにネストする場合は `:` の数を増やして区別します。

### `{name=filename}` でコードブロックにファイル名を表示する

このリポジトリでは、簡単にコードブロックにファイル名を表示できる機能を用意しています。  
`{name=filename}` をコードブロックの後ろに追加することで、ファイル名を表示することができます。

````markdown
```js {name=index.js}
const message = "Thank you for using Awesome Marp Template!";
console.log(message);
```
````

表示は以下の通りになります。

![コードブロックにファイル名を表示](https://github.com/user-attachments/assets/e4c5aee9-5ed1-4826-aa24-fe766c8426b1)

このユーティリティの実装詳細は [themes/utility.css](./themes/utility.css) を参照してください。

> [!warning]
> Marp の利用するテーマによって実装方法が異なります。
> このリポジトリの初期の `gaia` テーマから変更する場合は修正が必要です。
> 特に、`default` での実装はかなり難しいです。
> この機能を利用したい場合は、実装方法を自分で発明するか、`gaia` か `uncover` テーマの選択を推奨します。

### アラートデザインを使用する

このリポジトリでは、簡単にアラートデザインを適用できる機能を用意しています。  
`.note` `.important` `.tip` `.warning` `.caution` のクラスを使用することで、アラートデザインを適用できます。

![アラートデザイン](https://github.com/user-attachments/assets/98b1a1a5-4458-444d-a1a3-cececdc0d9c2)

---

以上でこのリポジトリの説明は終了です！  
ぜひこのテンプレートを参考にして、 Marp を最大限活用したスライド作成を楽しんでください！✨
