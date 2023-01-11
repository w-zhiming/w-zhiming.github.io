# Mac 使用国内镜像安装brew

## 安装brew

- 将brew的install文件下载本地

```bash
    curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install
```

- 修改install文件的镜像源

```bash
    vim brew_install

    #BREW_REPO = "https://github.com/Homebrew/brew”.freeze

    #CORE_TAP_REPO = "https://github.com/Homebrew/homebrew-core".freeze

    BREW_REPO = "git://mirrors.ustc.edu.cn/brew.git".freeze

    CORE_TAP_REPO = "git://mirrors.ustc.edu.cn/homebrew-core.git”.freeze

    #就是“BREW_REPO”和“CORE_TAP_REPO”这两项，将其修改为清华的镜像
```

- 安装

```bash
    /usr/local/bin/ruby ~/brew_install
```

- 修改PATH变量

```bash
    vim /etc/profile

    export PATH=/usr/local/bin:$PATH

    source /etc/profile
```

- 验证
`brew doctor`


- 安装wget
`brew install wget`


## 修改brew的源为国内的源

``` bash
    # 执行下面这句命令，更换为中科院的镜像：
    git clone git://mirrors.ustc.edu.cn/homebrew-core.git/ /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1

    // 把homebrew-core的镜像地址也设为中科院的国内镜像
    cd "$(brew --repo)" 
    git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

    cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" 
    git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

    # 更新, 注意这里需要等待一会，因为要更新资源。
    brew update
    
```



## 复原步骤
``` bash 
# 步骤一
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git
# 步骤二
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core
# 步骤三
$ brew update

```

## brew 安装后的软件位置

- 配置文件在/usr/local/etc中
- 安装文件在/usr/local/Cellar中
- 二进制可执行程序的软连接在/usr/local/bin中

## brew command
- 诊断homebrew
` brew doctor`
 
- 更新homebrew
`brew update`

- 查看已安装的包
` brew list`

- 安装包
 `brew install packageName`

- 卸载包
 `brew uninstall packageName`

- 查找包
 `brew search packageName`

- 查看包信息
 `brew info packageName` 

```
