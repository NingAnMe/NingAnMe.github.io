---
title: 安装 oh-my-zsh
---
### 下载oh-my-zsh

```
marsloo@mars-Ideapad-V460:~$ sudo apt-get update
marsloo@mars-Ideapad-V460:~$ sudo apt-get install zsh -y
```

### 用 wget 安装

`sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"``

### oh-my-zsh的github介绍

[oh-my-zsh-github](https://github.com/robbyrussell/oh-my-zsh/wiki)

### h-my-zsh的配置在~/.zshrc文件中

```
export ZSH=$HOME/.oh-my-zsh
ZSH_THEME="gnzh"
DISABLE_UPDATE_PROMPT=true
plugins=(git autojump sudo httpie colored-man-pages)
source $ZSH/oh-my-zsh.sh
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
# Aliases configuration
alias ll='ls -lrth'
alias la='ls -lrtha'
alias grep="grep --color=auto"
alias vi='vim'
alias mysql='/usr/local/mysql/bin/mysql'
alias mysqladm='/usr/local/mysql/bin/mysqladmin'
alias mysqld='/usr/local/mysql/bin/mysqld'
alias -s c=vim
alias -s txt=vim
alias -s gz='tar -xzvf'
alias -s tgz='tar -xzvf'
alias -s zip='unzip'
alias -s bz2='tar -xjvf'
alias -s jpg='imgcat'
alias -s gif='imgcat'
alias -s png='imgcat'

export PROJECT_HOME=$HOME/learnspace
export WORKON_HOME=$HOME/Envs
if [ ! -d $PROJECT_HOME ]; then
    mkdir -p $PROJECT_HOME
fi
if [ ! -d $WORKON_HOME ]; then
    mkdir -p $WORKON_HOME
fi
# Virtualenvwrapper
source /usr/local/bin/virtualenvwrapper.sh
source ~/.iterm2_shell_integration.`basename $SHELL`

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
```

[主题](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)

### 把Zsh设置为当前用户的默认Shell

`chsh -s /bin/zsh`

### 重启一下电脑

`reboot`
