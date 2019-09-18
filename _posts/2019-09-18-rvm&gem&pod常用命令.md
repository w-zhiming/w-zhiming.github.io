- ruby rvm 常用指令
```
$ ruby -v # 查看ruby 版本
$ rvm list known # 列出已知的 ruby 版本
$ rvm install 2.3.0 # 选择指定 ruby 版本进行更新
$ rvm get stable # 更新 rvm
$ rvm use 2.2.2 # 切换到指定 ruby 版本
$ rvm use 2.2.2 --default # 设置指定 ruby 版本为默认版本
$ rvm list # 查询已安装的 ruby 版本
$ rvm remove 1.9.2 # 卸载移除 指定 ruby 版本

$ curl -L https://get.rvm.io | bash -s stable # 安装 rvm 环境
$ curl -sSL https://get.rvm.io | bash -s stable --ruby # 默认安装 rvm 最新版本
$ curl -sSL https://get.rvm.io | bash -s stable --ruby=2.3.0 # 安装 rvm 指定版本
$ source ~/.rvm/scripts/rvm # 载入 rvm
```
- Gem
```
$ gem -v # 查看 gem 版本
$ gem source # 查看 gem 配置源
$ gem source -l # 查看 gem 配置源目录
$ gem sources -a url # 添加 gem 配置源（url 需换成网址）
$ gem sources --add url # 添加 gem 配置源（url 需换成网址）
$ gem sources -r url # 删除 gem 配置源（url 需换成网址）
$ gem sources --remove url # 删除 gem 配置源（url 需换成网址）
$ gem update # 更新 所有包
$ gem update --system # 更新 Ruby Gems 软件

$ gem install rake # 安装 rake，从本地或远程服务器
$ gem install rake --remote # 安装 rake，从远程服务器
$ gem install watir -v 1.6.2 # 安装 指定版本的 watir
$ gem install watir --version 1.6.2 # 安装 指定版本的 watir
$ gem uninstall rake # 卸载 rake 包
$ gem list d # 列出 本地以 d 打头的包
$ gem query -n ''[0-9]'' --local # 查找 本地含有数字的包
$ gem search log --both # 查找 从本地和远程服务器上查找含有 log 字符串的包
$ gem search log --remoter # 查找 只从远程服务器上查找含有 log 字符串的包
$ gem search -r log # 查找 只从远程服务器上查找含有log字符串的包

$ gem help # 提醒式的帮助
$ gem help install # 列出 install 命令 帮助
$ gem help examples # 列出 gem 命令使用一些例子
$ gem build rake.gemspec # 把 rake.gemspec 编译成 rake.gem
$ gem check -v pkg/rake-0.4.0.gem # 检测 rake 是否有效
$ gem cleanup # 清除 所有包旧版本，保留最新版本
$ gem contents rake # 显示 rake 包中所包含的文件
$ gem dependency rails -v 0.10.1 # 列出 与 rails 相互依赖的包
$ gem environment # 查看 gem 的环境

$ sudo gem -v # 查看 gem 版本（以管理员权限）
$ sudo gem install cocoa pods # 安装 CocoaPods（以管理员权限）
$ sudo gem install cocoapods # 安装 CocoaPods（以管理员权限）
$ sudo gem install cocoapods --pre # 安装 CocoaPods 至预览版（以管理员权限）
$ sudo gem install cocoapods -v 0.39.0 # 安装 CocoaPods 指定版本（以管理员权限）
$ sudo gem update cocoapods # 更新 CocoaPods 至最新版（以管理员权限）
$ sudo gem update cocoapods --pre # 更新 CocoaPods 至预览版（以管理员权限）
$ sudo gem uninstall cocoapods -v 0.39.0 # 移除 CocoaPods 指定版本（以管理员权限）
```
- pod
```
$ pod setup # CocoaPods 将信息下载到~/.cocoapods/repos 目录下。如果安装 CocoaPods 时不执行此命令，在初次执行 pod intall 命令时，系统也会自动执行该指令
$ pod --version # 检查 CocoaPods 是否安装成功及其版本号
$ pod install # 安装 CocoaPods 的配置文件 Podfile
```