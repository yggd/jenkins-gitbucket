# Jenkins導入備忘

## プラグイン一覧を抽出する。

```sh
$ curl -sSL "http://<username:password@host:port>/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins" | perl -pe 's/.*?<shortName>([\w-]+).*?<version>([^<]+)()(<\/\w+>)+/\1 \2\n/g'|sed 's/ /:/' > plugins.txt
```

## PRイベントはWebHookがJenkinsに到達するがビルドが始まらない。

GitHub Organization Foler pluginの内部PRジョブはWebHookが届かないため、
  - Jenkinsのプロジェクト> Child Scan Triggers は"他のビルドが起動していなければ定期的に起動"にチェックを入れ、間隔を1分(負荷軽減にもっと長めに取るべき？)を設定すること。

