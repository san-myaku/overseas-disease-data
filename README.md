# Overseas Disease Public Data

職場PCで公開情報を確認するための、結果データ専用リポジトリです。

公開しているのは、非公開collectorが公式情報から生成した結果JSONと、この説明だけです。
収集・解析コード、GitHub Actions、テスト、職場PC用HTML、認証情報、メール設定、
既報状態は含みません。

## Raw URL

```text
https://raw.githubusercontent.com/san-myaku/overseas-disease-data/main/data/latest.json
https://raw.githubusercontent.com/san-myaku/overseas-disease-data/main/data/history.json
```

`schema_version`が`2`のJSONには、次の結果を含みます。

- WOAH WAHIS、米国APHIS、ブラジルMAPAの発生情報と日本の輸入停止要否判定
- MAFFのHPAI（家きん）輸入停止情報
- MAFFの偶蹄類畜産物の輸入停止情報
- 各情報源の取得状態と一次情報URL（家畜衛生条件監査を含む）
- 英国・MAPA・APHISの更新監視、および家畜衛生条件PDF/判定CSV監査の状態・詳細・問題候補

米国APHISについては、`aphis_map_records`に既存マップ用の直近窓データを、
`aphis_history_records`に取得CSV全行の履歴を分けて保持します。履歴行には州・郡、発生確認日、
`Control Area Released`の原文・正規化日・状態（`active` / `released` / `not_applicable` / `unknown`）を含め、
画面ではMAFFの輸入停止・保留・解除イベントと混同しないよう別ソースの時系列として表示します。

`summary.highlights`と`records`は直近1回の実行分です。同じ報告日内の成功実行で見つかった新規情報は`daily_report.summary`と`daily_report.records`へ累積し、Web画面とCSVはこの日次スナップショットを表示します。後続の0件実行で同日の既報告が消えることはありません。日次スナップショットには報告対象日、初回生成時刻、最終反映時刻、集計回数も含みます。期間内の既報を含む全件スナップショットは公開しません。

GitHub版はPC上のメール版と独立して収集・判定・既報管理を行います。両者は実行時刻と既報状態が別のため、同じ対象日でも件数の完全一致は保証されません。メール版のPCや担当者が利用できなくても、GitHub側だけで公開データを更新できる設計です。

`run_status`が`error`の場合は、最新取得に失敗したため前回成功データを保持しています。定期実行ゲートが公開JSONを読めない場合は更新を中止し、古いローカル同梱JSONで公開値を上書きしません。
`history.json`は直近90回の実行時刻、成功・失敗、集計値、情報源別状態だけを保持します。収集コード、ログ、秘密情報は含みません。
`monitoring`の状態名と詳細は、日次メールの「他ソース更新監視・条件監査」欄と同じ結果を公開用に整形したものです。
表示内容は確認支援用であり、最終判断はJSON内の出典URLから各公式ページを確認してください。
