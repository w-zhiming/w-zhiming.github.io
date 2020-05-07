# zch & oh my zch config

```bash
# see current shell
echo $SHELL

# see if has zsh package at bin
cat /etc/shells

# install zsh
sudo yum install -y zsh

#change shell
chsh -s /bin/zsh

# install oh my zch.
 sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

## install plugin.
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# config .zshrc

vim ~/.zshrc

# set config
ZSH_THEME="ys"
plugins=(git z vscode zsh-autosuggestions zsh-syntax-highlighting)

# grap .bashprofile to .zshrc 
# source ~/bashprofile

# run .zshrc
soruce ~/.zshrc

```
