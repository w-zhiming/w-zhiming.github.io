 # vscode 无法输出JS log
 
 ## 修改 launch.json, 添加 "outputCapture": "std"
    
 ```
  "configurations": [
    {
        "type": "node",
        "request": "launch",
        "outputCapture": "std",
        "name": "Launch Program",
        "program": "${workspaceFolder}/server.js",
        "args": [
            "--debug-brk",
            "--colors",
        ],
    },
 ```