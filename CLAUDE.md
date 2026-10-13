# CLAUDE.md

このファイルは、このリポジトリで作業する Claude Code 向けのガイドです。人向けの説明は `README.md` にある。

## プロジェクト概要

ITパスポート試験の学習サイト **「ITパスポート用語ドリル」**。運営者は Yuki-fe（個人・副業）。姉妹サイト「FE用語ドリル」（デスクトップの `claude FE対策サイト`、リポジトリ `yuki-fe/fe-drill`）の仕組みをもとに作った。

- **サイト**: https://yuki-fe.github.io/ip-drill/ （GitHub Pages。リポジトリ `yuki-fe/ip-drill` の `main` ブランチの `/docs`）
- 用語の単語帳（カード・4択・書いて答える・復習・一覧）、用語ごとの解説ページ、分野別ミニテスト（`test.html`）、略語クイズと早見表（`abbr.html`）
- FE と同じ用語には `fe` で FE用語ドリルの id を持たせ、用語ページから FE の同じ用語へリンクする
- お問い合わせは FE と同じ Google フォーム https://forms.gle/s4yB1xMbcoRqZps2A
- Instagram・LINE ボットとのつながりはまだ作っていない（FE 側の `line-bot/` が担当する予定）

## よく使うコマンド

```powershell
python build.py                         # docs/ を作り直す（エラー・注意が出たら直す）
python -m http.server 8000 -d docs      # http://localhost:8000 で確認
```

- Windows のコンソールは cp932 なので、日本語を出力するスクリプトは `PYTHONIOENCODING=utf-8` を付けて動かす
- build.py は Python の標準ライブラリだけで動く

## 公開までの流れ

1. 編集する
2. `python build.py`
3. 運営者が **GitHub Desktop** で commit → push する（運営者はコマンドの git に慣れていない。手順は GitHub Desktop の画面で説明する）
4. 数分で公開サイトに反映される

## 決まりごと

- ユーザーへの回答は **日本語**。運営者は初心者寄りなので、手順は画面のボタン名まで具体的に書く
- `docs/` は生成物。直接編集しない（ただし GitHub Pages が使うので commit はする）
- `data/terms.json` の `id` は URL になるので、公開後に変えたり使い回したりしない
- localStorage の名前は `ip-drill-` で始める（FE用語ドリルと同じオリジンなので、名前が同じだと進み具合が混ざる）
- 受ける人は IT が初めての人も多い。用語の説明はやさしい言葉で書く
- 「公式」「IPA」など試験の主催者と関係があるように見える言葉、「必ず合格」など確かめられない言い切りは使わない
- 広告は「PR」の表示を消さない（ステルスマーケティング規制）
- 用語の説明は AI の支援で作ったもの。法律（改正が多い。例: 下請法 → 取適法、プロバイダ責任制限法 → 情報流通プラットフォーム対処法）や数値を足すときは特に確かめる
- トークン・合言葉・個人情報はリポジトリに入れない。リポジトリは **公開**
- 手順書・計画などの資料は FE 側の `notes/`（公開しない）で作る
