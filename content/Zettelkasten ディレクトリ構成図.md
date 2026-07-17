## Zettelkasten ディレクトリ構成図
このナレッジベースは、Zettelkasten（ツェッテルカステン）メソッドおよびPARAメソッド（Projects, Areas, Resources,Archives）の考え方をハイブリッドに組み合わせた、非常に洗練された情報整理システムになっています。日々の気づき（Fleeting Notes）から、文献メモ（Literature
  Notes）、そして抽象化された永久ノート（Permanent Notes）へと知識が美しく昇華されるプロセスを考慮した構造です。

  ---

  📌 ディレクトリ構造ツリー
``` text
1 / (Zettelkasten Root)
    2 ├── .obsidian/               # Obsidianのシステム設定、プラグイン、テーマ
    3 ├── 00_Projects/             # 現在進行中、または完了した具体的な個別プロジェクト
    4 │   ├── Karaoke_Vocal_English/     # 英語カラオケ・ボーカルプロジェクト
    5 │   ├── Miniature_Study_Escape/    # ミニチュア脱出ゲーム開発
    6 │   ├── Shiki_Renkan/              # 四季連関プロジェクト
    7 │   └── Unity_Escape_Practice/     # Unity脱出ゲーム練習
    8 ├── 00_Workflows/            # ナレッジベースの運用マニュアル、テンプレート、手順書
    9 │   ├── slide_creation_workflow.md
   10 │   ├── tagging_guideline.md
   11 │   └── youtube_audio_download_workflow.md
   12 ├── 01_Sources/              # 外部からのインプット、文献情報源、英語例文集の素材
   13 │   ├── literature.base
   14 │   └── English Sentenses.md
   15 ├── 02 EverGreenNotes/       # 長期的に参照・アップデートし続ける「枯れない」知的資産
   16 │   └── スマートノートの技術 - 覚えておくべきこと.pdf
   17 ├── 02_Inbox/                # 日々の気づき、読書メモ、一時的な着想（Fleeting Notes）
   18 │   ├── ADHDは現実の退屈さに耐えられない.md
   19 │   ├── 物語の持つ機能.md
   20 │   └── （その他、日常、学術、思考プロセスに関する大量のメモ）
   21 ├── 03_Incubator/            # アイデアの温床。Inboxから一歩進め、構造化や思考の地図（MOC）を練る場所
   22 │   ├── Map日本人の四度嗜好.md
   23 │   ├── Map日本音楽の難しさ.md
   24 │   └── canvasで知識をまとめる実験.canvas
   25 ├── 04_PermanentNotes/       # 十分に抽象化・体系化された永続的な知のストック
   26 │   ├── Gagaku MOC.md              # 雅楽関連のコンテンツマップ
   27 │   ├── 弱者の戦略_summary.md
   28 │   └── 演劇入門_logic_box_summary.md
   29 ├── 05_Assets/ / 07_Assets/  # メディア、画像などの静的アセット類
   30 ├── 06_Flashcards/           # 暗記学習（Spaced Repetition / Anki用）のカードデータ
   31 │   └── English words.md
   32 ├── 08_Logs/                 # 日付ごとのデイリーログ、ジャーナル（日々のアクティビティ記録）
   33 │   └── 2026-06-27.md
   34 ├── 99_Archives/             # 過去の成果物、使わなくなった古いワークフロー等の退避場所
   35 │   └── gemini_video_workflow_ver1.md
   36 ├── 99_Temp/                 # 一時的・実験的なファイル置き場
   37 ├── ChatGPT_MD/              # AI（ChatGPT）連携用フォルダ・Markdown出力
   38 ├── dictionary/              # ITツール、開発環境、言語表現などの「自分専用辞書」
   39 │   ├── bun.md
   40 │   ├── Obsidian.md
   41 │   └── Comfy UI.md
   42 ├── GeminiHelper/            # Gemini CLIのログ、チャット履歴、ワークスペース設定
   43 │   ├── chat_*.md                  # 過去の対話履歴
   44 │   └── gemini-workspace.json
   45 ├── Inbox/ / Kobo-Inboxes/   #各種連携や電子書籍リーダー（Kobo等）からの一次自動取り込み用
   46 │   └── 傷つきやすいアメリカの大学生たち.md
   47 ├── README_assets/           # README等に埋め込む画像やダイアグラム
   48 └── (Root Files)             #未整理の雑記、Excalidraw（思考図解）、管理用自動化スクリプト
   49     ├── create_notes.py            # ノート作成自動化用のPythonスクリプト
   50     ├── 画風探求用.excalidraw       # 手書きの視覚的思考ボード
   51     └──
      （Blender、Unity、ボイトレ、創作論、料理レシピなどの多岐にわたる雑記ノート
      群）
```
    

  ---

  🔍 各フォルダの役割と詳細
  1. ⚙️ システム・管理系 (00_Workflows, GeminiHelper, .obsidian)
   * .obsidian:
     Obsidianの設定、インストール済みプラグイン、CSSスニペットなどのバックエンド
     環境。
   * 00_Workflows:
     「ナレッジベースをどう維持するか」「スライドや動画をどう作るか」といった、
     システムの再現性を高めるためのマニュアルが保管されています。
   * GeminiHelper / ChatGPT_MD:
     AIエージェントとの協調作業プロセスやログが記録されており、過去の知的対話を
     見返すインデックスとなります。

  2. ⚡️ インプット・一時受け入れ系 (02_Inbox, Inbox, Kobo-Inboxes, 01_Sources)
   * 02_Inbox / Inbox:
     知識の「玄関口」。SNSで見かけた面白い議論、読書中に思いついた閃き、ふとした
     疑問など、形式を整える前の生データ（Fleeting
     Notes）がここにストックされます。
   * Kobo-Inboxes: 電子書籍リーダー Kobo
     から自動抽出したハイライトを一時的に保管し、のちの「Literature
     Notes（文献ノート）」に加工するための場所です。
   * 01_Sources:
     辞書、書籍、動画などの「情報ソース」そのもののログや、英語の構文集。

  3. 🌱 熟成・体系化系 (03_Incubator, 04_PermanentNotes, 02 EverGreenNotes)
   * 03_Incubator:
     Inboxから拾い上げた素材を繋ぎ合わせ、「これはどういう意味か？」を深掘りする
     中間プロセス。Obsidian
     Canvasなどを使った視覚的な結びつきの模索がここで行われます。
   * 04_PermanentNotes:
     完全に消化され、自分の言葉として抽象化された「永続的ノート（知的ストック）
     」。MOC（Map of
     Content/目次ノート）を活用し、複雑なトピックがいつでも取り出せる形で保管さ
     れます。
   * 02 EverGreenNotes:
     時が経っても古びず、人生や仕事において何度も読み返し、更新し続けるべき「主
     軸のナレッジ」。

  4. 🚀 アウトプット・プロジェクト系 (00_Projects, Root Files)
   * 00_Projects:
     実際に具体的なゴールを持つ活動領域。「脱出ゲーム開発」「英語カラオケ」「四
     季連関」など、Zettelkastenに蓄積された知識をエネルギーとして、具体的なアウ
     トプットを生み出している現場です。
   * Root Files (直下のノート群):
     まだ各フォルダに分類されていない進行中の雑多なアイデア、Blenderのノード構築
     術、ボイトレの科学的アプローチ、Excalidrawを使った図解などが一時的に広がっ
     ているクリエイティブな「作業デスク」です。

  ---

  🔄 ノートのライフサイクル（Zettelkastenの血流）

  知識がこのディレクトリをどのように旅していくかのイメージです。

    1   [ 外部インプット / 電子書籍 ]
    2              ↓
    3      Kobo-Inboxes / Inbox      ─── (一次受け取り)
    4              ↓
    5           02_Inbox             ─── (走り書き / Fleeting Notes)
    6              ↓
    7         03_Incubator           ─── (接続と熟成 / Canvas & Map)
    8              ↓
    9      04_PermanentNotes         ─── (構造化・抽象化 / 永続ノート)
   10              ↓
   11   00_Projects / Output         ─── (具体的プロジェクト・制作物への応用)

  非常に機能的に役割分担がなされており、クリエイティブな実験と長期的なナレッジ蓄
  積が無理なく同居できる素晴らしい構造になっています。是非この構成図を日々の整理
  や、AIアシスタントとの連携にお役立てください！


[^1]: 豚バラと大根のサラダがいいかも。明太子パスタと。
