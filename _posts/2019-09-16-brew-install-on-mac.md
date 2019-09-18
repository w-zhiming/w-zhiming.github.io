
## mac上使用国内镜像安装brew

### 安装brew

- 将brew的install文件下载本地

```
    $ cd
    $ curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install
```

- 修改install文件的镜像源
```
    $ vim brew_install 

    #BREW_REPO = "https://github.com/Homebrew/brew”.freeze

    #CORE_TAP_REPO = "https://github.com/Homebrew/homebrew-core".freeze

    BREW_REPO = "git://mirrors.ustc.edu.cn/brew.git".freeze

    CORE_TAP_REPO = "git://mirrors.ustc.edu.cn/homebrew-core.git”.freeze

    #就是“BREW_REPO”和“CORE_TAP_REPO”这两项，将其修改为清华的镜像
```
- 安装
```
    $ /usr/local/bin/ruby ~/brew_install
```
- 修改PATH变量
```
    $ vim /etc/profile

    export PATH=/usr/local/bin:$PATH

    $ source /etc/profile
```
- 验证
```
    $ brew doctor
```
- 安装wget

```
    $ brew install wget 
```

### 修改brew的源为国内的源
```
    // 执行下面这句命令，更换为中科院的镜像：
    git clone git://mirrors.ustc.edu.cn/homebrew-core.git/ /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1

    // 把homebrew-core的镜像地址也设为中科院的国内镜像

    cd "$(brew --repo)" 

    git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

    cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" 

    git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

    // 更新
    brew update
```
