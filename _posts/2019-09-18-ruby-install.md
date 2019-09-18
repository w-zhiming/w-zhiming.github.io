### Install rvm
1. 安装mpapis公钥。但是，正如安装页面所记录的，您可能需要gpg。Mac OS X不附带gpg，因此在安装公钥之前，您需要安装gpg。我用Homebrew安装了gpg ：
```
brew install gnupg 
```
2. 安装完gpg之后，你可以安装mpapis公钥：
```
gpg --keyserver hkp://pgp.mit.edu --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```
3. 安装最新版本的Ruby的RVM
```
\curl -sSL https://get.rvm.io | bash -s stable --ruby
```
安装成功，推出重新打开终端

4. 安装ruby
```
# rvm list known
# rvm install 2.6.0
```

5. gem 更新源
```
  gem sources -l
  gem sources --add https://gems.ruby-china.com/ --remove https://ruby.taobao.org/
  gem sources -l
  gem update --system
```

