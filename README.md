# Yorisoi Daily — よりそいデイリー

認知症のケア・介護・医療・制度のニュースを毎日自動収集してお届けする日刊サイト。
ナレッジベース [Yorisoi Knowledge (care-knowledge)](https://yorisoi.osamusic.org/) の姉妹サイトです。
記事は [note](https://note.com/yorisoi_daily) にも掲載しています。

## 構成

- Hugo + [PaperMod](https://github.com/adityatelange/hugo-PaperMod) テーマ（care-knowledge と共通）
- GitHub Pages に GitHub Actions（`.github/workflows/hugo.yml`）で自動デプロイ
- ドメインは Cloudflare プロキシ経由（DNS はオレンジ雲・SSL モード「フル」）
- テーマカラーは「よりそいオレンジ」（`assets/css/extended/custom.css`、care-knowledge と共通）

## 記事の生成

記事（`content/posts/yorisoi-YYYY-MM-DD-*.md`）は別リポジトリ
`../care-news-code`（news-agent パイプライン）がローカル cron（毎日 12:00 JST）で
生成・コミットする。**このリポジトリでは記事を手で書かない**。
frontmatter の `description:` も導入文からパイプラインが自動抽出する。

## 「役に立った」ボタン

各記事の末尾に表示されるフィードバックボタン（care-knowledge と共通の仕組み）。

- 表示部: `layouts/_partials/comments.html`（PaperMod の comments フック。
  ナレッジサイトへの誘導ボックスもここにある）
- 集計 API: 同一ドメインの `/likes?path=<記事パス>`。実体は Cloudflare Worker
  `yorisoi-likes`（`~/ai/yorisoi-likes`、KV に「ホスト名:パス」単位で保存）

## デプロイ

`main` ブランチへの push で GitHub Pages に自動デプロイされます。
