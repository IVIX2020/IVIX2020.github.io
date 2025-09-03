---
title: 2025-09-03 QuartzとObsidian, そしてGitHub Pagesを連携させてブログを作った
createdAt: 2025-09-03
tags:
  - blog
  - daily
description: QuartzとObsidian、そしてGitHub Pagesを組み合わせて、自分だけの無料ブログを立ち上げた記録。
---

## はじめに
今日は、自分のノート管理環境である **Obsidian** をそのまま活かして、  
**Quartz** と **GitHub Pages** を組み合わせた「自分専用ブログ」を立ち上げました。  
有料サービスである Obsidian Publish を使わずとも、工夫次第で完全無料の公開環境が作れることに挑戦しました。  

## 本文

### セットアップの流れ
- **Quartz を導入**  
  `npx quartz create` を実行して初期化。`content` フォルダが記事置き場になります。  

- **Obsidian Vault と連携**  
  Obsidian 内の「公開したいフォルダ」を Quartz の `content` にシンボリックリンク。  
  → ローカルではそのまま執筆内容が反映され、プレビューも可能。  

- **GitHub Pages で公開**  
  リポジトリを作成し、GitHub Actions を利用して自動でビルド＆公開されるよう設定。  
  `npx quartz sync --no-pull` で Vault のノートを push、数分後には Web 上で記事が見られるようになりました。  

### 苦労したポイント
- **シンボリックリンク問題**  
  ローカルでは正常でも、GitHub 上ではリンク先が存在せず空になることがありました。  
  → `quartz sync` の「symlink dereference」機能で解決。  

- **フロントマター設定**  
  Quartz は `title` や `date` をしっかり指定すると一覧やRSSで綺麗に表示される。  
  → Obsidian の Templater を使い、自動で日付入りタイトルを挿入するテンプレートを作成しました。  

### 感じたメリット
- **完全無料で公開可能**  
  GitHub Pages を使えば、ドメイン代をかけずにすぐ公開できる。  
- **ノートとブログの一元化**  
  Obsidian で日々書いたメモを、そのまま記事に変換できる。  
- **シンプルで軽い**  
  Quartz v4 は見た目もシンプルで、更新やビルドも高速。  

## まとめ
- **Obsidian + Quartz + GitHub Pages** で、無料かつシンプルにブログを公開できた。  
- 最初はシンボリックリンクや GitHub Actions の扱いに戸惑ったが、流れを掴めば快適。  
- これからは日々の学びや記録を **Obsidian → Quartz → GitHub Pages** のルートで公開していきたい。  



> [!quote] 感想
>「自分のノートがそのまま公開ブログになる」という感覚は、想像以上に気持ちがいいものでした。


>



