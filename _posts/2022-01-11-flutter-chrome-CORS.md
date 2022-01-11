# Flutter 开启 Chrome跨域功能

- 修改Flutter_tools源码

Path： sdk/flutter/packages/flutter_tools/lib/src/web/chrome.dart

find  --disable-translate,  add  '--disable-web-security'

- Compile flutter sdk

```shell
cd flutter
rm ./bin/cache/flutter_tools.stamp
rm ./bin/cache/flutter_tools.snapshot

flutter --version
```
