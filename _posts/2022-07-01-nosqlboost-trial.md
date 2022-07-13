

# NoSQLBooster for MongoDB trail



- 下载工具

  ```shell
  npm install asar -g

- 进入 NoSQLBooster for MongoDB.app/Contents/Resources

    ```shell
    asar extract app.asar app
    ```

- 修改 app\shared\lmCore.js 里的 MAX_TRIAL_DAYS 和 TRIAL_DAYS 值

  ```shell
  MAX_TRIAL_DAYS=999999,TRIAL_DAYS=999999
  ```
  
- 回到NoSQLBooster for MongoDB.app/Contents/Resources 进行打包
	
  ```shell
  asar pack app app.asar
  ```
  
- 删除app 文件夹
  
  ```shell
  rm -rf app 
  ```
  
  
  
  
