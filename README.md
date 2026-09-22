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

画面とメールを揃えるため、`summary.highlights`にメール本文と同じ報告対象イベントの要約、`summary.new_counts`に情報源ごとの新規件数を含みます。`records`は今回の新規報告に属する全明細（メール添付CSV相当）で、必要な場合に画面の折り畳みから確認します。期間内の既報を含む全件スナップショットは公開しません。

`run_status`が`error`の場合は、最新取得に失敗したため前回成功データを保持しています。
`history.json`は直近90回の実行時刻、成功・失敗、集計値、情報源別状態だけを保持します。収集コード、ログ、秘密情報は含みません。
`monitoring`の状態名と詳細は、日次メールの「他ソース更新監視・条件監査」欄と同じ結果を公開用に整形したものです。
表示内容は確認支援用であり、最終判断はJSON内の出典URLから各公式ページを確認してください。
