# ninth-house

**Aries Tech Garden** — Zettelkasten 方式のデジタルガーデンを公開するための、自作静的サイトジェネレーター（SSG）。

Obsidian で書いたフラットな Markdown の Vault を入力に、タグページ（MOC）・バックリンク・全文検索を自動生成した静的サイトを出力し、Cloudflare Pages で配信する。

## ステータス

仕様策定完了、実装未着手。

## 技術スタック

| 領域 | 採用 |
|---|---|
| 言語 | Node.js / TypeScript |
| 執筆環境 | Obsidian（フォルダ階層なしのフラットVault） |
| 全文検索 | Pagefind |
| 数式 | KaTeX（ビルド時にHTMLへ変換） |
| コードハイライト | shiki（ビルド時にHTMLへ変換） |
| 配色 | Catppuccin（Mocha / Latte） |
| ホスティング | Cloudflare Pages |
| 画像ホスティング | Cloudflare R2 |

クライアントへ配信する JavaScript は、検索・ライトボックス・ランダムノート・配色切り替えのみに留める。数式とコードハイライトはビルド時に静的HTMLへ落とす。

## 設計方針

- **フォルダ階層を作らない。** 分類はタグだけで行う。
- **手動メンテを増やさない。** MOC・一覧・バックリンクはすべて自動生成する。
- **検索で見つかればよい。** リンクを辿れるかを根拠にした機能は過剰要件とみなす。
- **機能は「入れるが最小限」で刻む。** 欲しい機能でも、リッチな実装は求めない。
- **公開はオプトイン。** フロントマターに `publish: true` があるノートだけをビルドする。

## ビルドとデプロイ

```
Obsidian Vault
  └─(手動 git push)→ GitHub
        └─(Cloudflare Pages の Git 連携)→ ssg-build && pagefind --site dist
```

## ドキュメント

仕様の詳細は **[docs/spec.md](docs/spec.md)** を参照。コンテンツモデル、URL設計、各ページ仕様、Markdown処理、配色トークンの割り当て、および「実装しないもの」とその理由を記載している。
