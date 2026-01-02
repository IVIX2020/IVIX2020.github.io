---
title: astroで挫折した件
date: 2025-11-28
description: 「語彙力」って、単なる知識の量だと思ってませんか？もし言葉が僕らの思考や世界認識を根本から規定しているとしたら？言語が持つ「ヤバい真実」を、サピア＝ウォーフ仮説から深掘りします。
tags:
  - language
  - psychology
  - philosophy
  - self-improvement
slug: vocabulary-world-resolution
---
astroは静的なサイトを構築するためのフレームワークだ。
GitHub Pagesを利用してページを公開しようと奮闘した結果見事玉砕したので記録したい。

正直、本当に何が原因なのか謎。

自分の要領が悪いだけなのは百も承知として、謎は謎のまま、引っかかった唯一のポイントをまとめたい。

## blog以下のコンテンツが表示されない問題

astroのファイル構成は次のようになっている。

**ビルド前**
``` text
my-project/
├── .github
│   ├── workflow
│   │   ├── deploy.yml # ここでGitHub Actionsでの挙動を指定
├── node_modules/       # 依存パッケージ (npm install で生成)
├── src/
│   ├── components/     # 再利用可能な UI 部品 (*.astro, *.tsx, etc.)
│   ├── content/        # コンテンツコレクション (ブログ記事, データなど)
│   │   ├── blog/       # ブログ記事の Markdown ファイル (*.md, *.mdx)
│   │   └── config.ts   # コンテンツコレクションのスキーマ定義
│   ├── layouts/        # ページの骨格となるレイアウト (*.astro)
│   ├── pages/          # ルーティングに対応するファイル
│   │   ├── index.astro       # ホームページ ( / )
│   │   ├── about.md          # About ページ ( /about )
│   │   └── blog/
│   │       ├── index.astro   # ブログ一覧 ( /blog )
│   │       └── [...slug].astro # 動的ルーティング ( /blog/post-name )
│   └── styles/         # グローバル CSS
├── public/             # 静的アセット (ビルドで処理されず、そのまま dist/ にコピー)
│   ├── favicon.svg
│   └── images/
├── package.json        # プロジェクト情報と依存関係
└── astro.config.mjs    # Astro の設定ファイル
```

**ビルド後(静的サイト、distフォルダ内に作られる)**
``` text
my-project/
└── dist/                 # ビルド出力ディレクトリ
    ├── assets/           # ビルド処理されたファイル (ハッシュ化された CSS/JS)
    │   └── main.css
    ├── index.html        # ホームページ ( / )
    ├── about/
    │   └── index.html    # /about ページ
    ├── blog/
    │   ├── index.html    # /blog ページ
    │   └── 20260102-post-name/
    │       └── index.html # 個別ブログ記事 (カスタムスラッグに対応)
    └── favicon.svg       # public/ からコピーされた静的ファイル
```

僕の悩みはビルド後でいうところの`blog`ディレクトリ内のコンテンツが表示されない(404)ことだ。
最初はページ内の要素のリンク周り（BASEURLがうまく働いていないとか、`.../blog`でなく`.../blog/`でなきゃダメなのかとか）を疑ったが、それが原因ではないらしい。

`npm run dev`でローカルホスト上で見る分には問題なくページ遷移もされる。

仕方ないのでdist内のフォルダ自体を確認しようと試みた。
ちなみにdistはGitHub Remote Repogitory上に作成される。
ビルド自体をGitHub Actionsを利用して、Remote Repogitory上で行なっているからだ
（この辺の設定は`.github/workflow/deploy.yml`に記述）。

GitHub Actionsは、pushしたタイミングで自動で走って動作させられるプログラム的なものらしい。

## dist内のファイルを見ても正しく作成されている

で、GitHub Actionsの個別のWorkflowページを開くと、そこからArtifactsと呼ばれる、実行後の成果品みたいなものを落としてこれる。

ここでいうとそれがdist内のファイルをZipにしたもので、Actionsが稼働した結果生成された公開用のファイルをローカルで展開して確認することができるわけ。

**結果として、何も問題がなかった**。

少なくとも、blog配下のindex.htmlや個別のページ（記事タイトルと同名のディレクトリ内にindex.htmlとして生成される）自体が間違いなく存在するし、ページ同士のリンク要素を確認しても問題がなさそう。

正直、途方に暮れてしまった。

ここまでの作業はastroのデフォルトのテンプレートを使ったのだが、藁にもすがる思いで、個人が作成した別のastroテンプレートをゼロから導入することにした。
......が、ここから私の要領の悪いところが全開で、色々とgit周りをミスった結果、元々作っていたオリジナルのプロジェクトファイル（ローカルリポジトリ）を新しいリモートリポジトリで上書きしてしまったりだの、なんやかんやでかえってややこしい結果に。

意志力と時間を使い果たした結果、一旦元々のquartzを使ったブログにリセットした次第である。

## 実はastro.config.mjsでも引っかかってたり

そもそも、astroの最も根幹的なconfigであろうと思われる`astro.config.mjs`からしてよくわかってない。
中身的にはこんな感じ。

``` javascript
import { defineConfig } from 'astro/config'
import svelte from '@astrojs/svelte'
import mdx from '@astrojs/mdx'
import remarkGfm from 'remark-gfm'
import remarkSmartypants from 'remark-smartypants'
import rehypeExternalLinks from 'rehype-external-links'
import remarkObsidianCallout from './src/remark/remark-obsidian-callout.js';

// https://astro.build/config
export default defineConfig({
  site: 'https://ivix2020.github.io', 
  integrations: [mdx(), svelte()],
  markdown: {
    shikiConfig: {
      theme: 'nord',
    },
    remarkPlugins: [remarkGfm, remarkSmartypants,remarkObsidianCallout],
    rehypePlugins: [
      [
        rehypeExternalLinks,
        {
          target: '_blank',
        },
      ],
    ],
  },
})
```

これのsiteというところにGitHub PagesのベースURLを入れるのは間違いないみたいなんだが、PagesのURLはアカウントに対して一つしか持てないので（多分）、本来はリポジトリを分けて運用したかった。

私の場合は

 - astro -> 日々の想いを綴るブログ + 成果物などの公開
 - quartz -> wikiっぽい感じのデジタルガーデン、いわばobsidian（セカンドブレイン）をpublicise した感じ

で作りたかったので、既存のquartzとはURLを分けて運用したかった。
```
import { defineConfig } from 'astro/config'

export default defineConfig({
  site: 'https://astronaut.github.io',
  base: '/my-repo',
})
```

上みたいな感じで、baseという項目に、独立したリポジトリを割り当てる感じ。
ところが私にとってはこれもうまくいかなかった。

ページ内の自動生成リンクが、BASE URLをhttps://ivix2020.github.ioとしか見てくれないのだ
（`https://ivix2020.github.io/garden`として見てもらうべきところ）。

これも本当意味わからなかった。

どうも公式を後から読むと、仕様らしい。
つまりリンクとかの飛ぶ先は手動で書き換えなくてはいけないようなのだ。
なんで？

## 結局

どうもastroにはまだまだ慣れないので、しばらくはquartzで運用したい。
でもそのうちまたリベンジしたいな。
表示がリッチだし、サイトに複雑な構造を持たせられるのは魅力的。