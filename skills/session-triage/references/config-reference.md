# 設定項目の説明（config.json）

値の意味が分からないときだけ読む。既定値は同じフォルダの上にある `config.example.json`。

| 項目 | 意味 |
|---|---|
| `owner` | 本文で「本人」と呼ぶ人の呼び方（例: 「あなた」「田中さん」） |
| `language` | タイトル・一覧・ログを書く言語（`ja` / `en`） |
| `data_dir` | 前回の判定（`state.json`）とログ（`log.md`）の置き場 |
| `report_path` | 本人の確認事項の一覧（Markdown）の出力先 |
| `emoji` | 5つの状態の絵文字。キーは state.json の `status` にも使う |
| `legacy_emoji` | 以前使っていて、見つけたら付け替える絵文字 |
| `folder_rules` | 作業フォルダ（cwd）から【フォルダ】のラベルを決めるルール（下を参照） |
| `folder_fallback_strip_prefixes` | ルールに当たらないとき、最後のフォルダ名から外す接頭辞 |
| `skip_title_prefixes` | タイトルを変えないセッションのタイトルの頭（他の定期実行など） |
| `self_title_marker` | このスキルの定期実行を見分ける言葉（既定「セッション整理」） |
| `nightly_archive` | 夜のまとめアーカイブ。`enabled`・`start`・`end`（`HH:MM`）・`min_idle_minutes` |
| `timezone` | 時刻の判定に使うタイムゾーン（IANA 名。例: `Asia/Tokyo`） |
| `notify` | 要確認・送信待ちが増えたときに macOS 通知を出すか |
| `max_sessions` | 1回で見るセッションの上限 |

## folder_rules の書き方

上から順に当て、最初に当たったものを使う。cwd の区切りは `/` として比べる。

- `{"contains": "/my-web-app", "label": "Webアプリ"}`：cwd にその文字列が含まれていれば当たり
- `{"regex": "/clients/([^/]+)", "label": "顧客:$1"}`：正規表現で当たり。`label` の `$1` は1つ目のカッコの中身に置き換える
