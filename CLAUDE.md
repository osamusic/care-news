# CLAUDE.md — Yorisoi Daily (care-news)

認知症ケアの日刊ニュースサイト。Hugo + PaperMod、GitHub Pages（main への push で自動デプロイ）、
ドメイン yorisoi-news.osamusic.org は Cloudflare プロキシ経由。
姉妹サイト: Yorisoi Knowledge（`../care-knowledge`、知識ベース）。詳細な構成は README.md を参照。

## 最重要

- **`content/posts/` の記事は自動生成**（`../care-news-code` のパイプラインが毎日 12:00 JST に
  cron でコミットする）。記事本文は原則手で編集しない。表示の問題はテンプレート
  （`layouts/`）か CSS で直す
- ローカル作業中に cron が同じ作業ツリーへコミットすることがある。push 前に
  `git pull --rebase` を忘れない

## 変更時の注意

- **カラーパレット**（`assets/css/extended/custom.css`）: ライトモードの
  `--primary #a8530f` / `--secondary #9a5730` は WCAG AA を満たす値。
  旧値 #d2691e / #e8935a はコントラスト不足なので戻さない
- **PaperMod 更新**: `.github/workflows/hugo.yml` の `PAPERMOD_COMMIT`（SHA 固定）を
  care-knowledge 側と合わせて両方更新する
- **CSP**: `layouts/_partials/extend_head.html` の meta CSP は `connect-src 'self'` のまま
- **記事の `.post-description` は CSS で非表示**（導入文と重複するため。meta/OGP 用にのみ使う）
- **security.txt** の連絡先は yorisoi.daily@gmail.com（個人アドレスにしない）

## 記事末尾の部品

`layouts/_partials/comments.html` に「役に立った」ボタンと、よりそいナレッジへの
誘導ボックスがある（PaperMod の comments フック、`params.comments = true` で有効）。
集計 API は同一ドメインの `/likes`。実体は Cloudflare Worker `yorisoi-likes`
（`~/ai/yorisoi-likes`、`wrangler deploy` で反映）。

## 文体

やさしい日本語、断定しすぎない、必ず相談先につなげる。
