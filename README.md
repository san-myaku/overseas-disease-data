# Overseas Disease Public Data

職場PCで公開情報を確認するための、結果データ専用リポジトリです。

公開しているのは、農林水産省動物検疫所の公開ページから生成した
`data/latest.json`と、この説明だけです。収集・解析コード、GitHub Actions、
テスト、職場PC用HTML、認証情報、メール設定、既報状態は含みません。

## Raw URL

```text
https://raw.githubusercontent.com/san-myaku/overseas-disease-data/main/data/latest.json
```

`sources.maff_hpai.status`が`ok`なら最新取得成功、`error`なら取得失敗時の
前回成功データです。表示内容は確認支援用であり、最終判断はJSON内の出典URLから
農林水産省公式ページを確認してください。
