# macOS 使用 Charles 对 iOS 模拟器进行抓包


## 前期准备：
1. 打开 Charles；
2. 打开任一模拟器；
3. 关闭电脑上的代理软件或代理服务。
## 设置
1. 打开 Charles，点击顶部菜单栏的 Proxy -> 勾选 macOS Proxy；
2. 继续在 Charles 里，点击顶部菜单栏的 Help -> SSL Proxying -> Install Charles Root Certificate in iOS Simulators；
3. 打开模拟器 -> 设置 App -> 通用 -> 关于本机 -> 滑到底部 -> 证书信任设置，点开后会看到 Charles Proxy CA（…），这时把证书开关打开；
4. 打开模拟器的 Safari 浏览器，在地址栏输入 chls.pro/ssl，这时会弹出弹窗提示你安装描述文件，点允许安装；
5. 回到设置 App -> 通用 -> 滑到下面 -> 描述文件 -> 看到 Charles Proxy CA（…）-> 点击证书 -> 点击导航栏右上角安装 Charles 的描述文件；
6. 打开电脑的系统偏好设置 App -> 网络 -> 记住你当前连接网络的 IP（如当前连接了 Wi-Fi）-> 点击右下角的高级 -> 弹出的窗口里 -> 点击代理 -> 选中【网页代理(HTTP)】，在地址栏和端口填入刚刚记住的 IP 地址和端口8888（如果不是8888，请到 Charles -> Proxy 里查看具体的端口），同理，下方的【安全网页代理(HTTPS)】也一样输入 IP:Port，填好后点击“好”并应用；
7. 打开模拟器，打开你的 App 或网页抓取你需要的数据吧。

***注意：抓包结束后，请按步骤6回到电脑系统设置页，把网页代理和安全网页代理去掉，否则关掉 Charles 后电脑上不了网。***
