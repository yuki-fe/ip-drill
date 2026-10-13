# ITパスポート用語ドリル

ITパスポート試験の用語を覚える静的サイトです。`python build.py` を実行すると `docs/` に全ページが書き出され、そのまま GitHub Pages で公開できます。サーバもデータベースも要りません。

姉妹サイト「FE用語ドリル」（基本情報技術者試験、リポジトリ `yuki-fe/fe-drill`）の仕組みをもとに作っています。

- 公開URL（予定）: https://yuki-fe.github.io/ip-drill/

## フォルダの中身

| パス | 内容 | 編集するか |
|---|---|---|
| `config.json` | サイト名・公開URL・FE用語ドリルのURL・運営者・アクセス解析・広告の設定 | する |
| `data/terms.json` | 用語データ | する |
| `build.py` | ページを生成するスクリプト。運営者情報・プライバシーポリシーの文面、ミニテストの問題数（`TEST_COUNTS`）もここにある | 文面を変えるとき |
| `static/assets/` | CSS と JavaScript。`app.js` ホームの単語帳、`drill.js` ミニテストと略語クイズ、`term.js` 用語ページの確認問題 | 見た目や機能を変えるとき |
| `docs/` | 生成されたサイト。**直接編集しない**（ビルドのたびに作り直される） | しない |

## 普段の作業

```powershell
cd "C:\Users\admin\Desktop\ip-drill"
python build.py                       # docs/ を作り直す
python -m http.server 8000 -d docs    # http://localhost:8000 で確認（Ctrl+C で終了）
```

`build.py` は、用語の重複や設定の入れ忘れがあると「エラー」「注意」を表示します。

## 用語を追加・修正する

`data/terms.json` に次の形で追記します。

```json
{"id": "0666", "field": "T", "sub": "ネットワーク", "term": "用語名", "desc": "説明文", "abbr": "正式名（略語のときだけ）", "fe": "0138"}
```

- `field` は `S`（ストラテジ系）/ `M`（マネジメント系）/ `T`（テクノロジ系）
- `id` は今ある最大の番号の次にする。**公開後に既存の id を変えたり使い回したりしない**（ページのURLが `terms/0001.html` のように id で決まるため）
- `abbr` を付けると略語クイズと略語の早見表に入る（英語の正式名を書く）
- `fe` は FE用語ドリルの同じ用語の id。付けると用語ページに「FEでも出る」の案内が出る
- 用語名に `（）` を付けると、括弧の中も「書いて答える」で正解になる（例: `製造物責任法（PL法）`）
- 法律の名前や内容、数値を足すときは、元の情報を確かめる（改正が多い）

## 学習の記録

進み具合はブラウザの localStorage に保存します。FE用語ドリルと同じ `yuki-fe.github.io` の上で動くので、保存の名前は FE と分けて `ip-drill-` で始めています（`ip-drill-v1` 覚えた用語、`ip-drill-weak` 復習、`ip-drill-prefs` 設定、`ip-drill-test` ミニテストの結果、`ip-drill-abbr` 略語クイズの設定）。
