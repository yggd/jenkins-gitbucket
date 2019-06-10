# Jenkins導入備忘

## プラグイン一覧を抽出する。

```sh
$ curl -sSL "http://<username:password@host:port>/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins" | perl -pe 's/.*?<shortName>([\w-]+).*?<version>([^<]+)()(<\/\w+>)+/\1 \2\n/g'|sed 's/ /:/' > plugins.txt
```

