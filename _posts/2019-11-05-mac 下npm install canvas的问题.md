# OSX 上npm安装canvas

1. 启用xcode工具：
`xcode-select --install`
2. 执行安装 `npm install --save canvas`
3. 如果依旧报错，则在进行安装 pkg-config & cario

    ```bash
    brew install pkg-config
    ```

4. 解决Package libffi  was not found in the pkg-config search path.

```bash
    # edit bash_profile, add environment.
    #vim ~/.bash_profile
    export PKG_CONFIG_PATH=/usr/local/Cellar/libffi/3.2.1/lib/pkgconfig/
```
