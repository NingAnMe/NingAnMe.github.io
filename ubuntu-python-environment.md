# Ubuntu系统Python工作学习一体化环境详细配置

![touxiang.png](http://othja876s.bkt.clouddn.com/xiaoguotu.png)

### 升级系统

`sudo apt-get update`

`sudo apt-get upgrade`

### 系统设置

系统-语言-英文-重启-修改中文文件名 ; 系统-语言-中文-重启-保留英文文件名

系统-亮度和锁屏

系统-外观

系统-软件和更新-附加驱动

### 科学上网

**shadowsocks-qt5**

[shadowsocks-qt5-github-wiki](https://github.com/shadowsocks/shadowsocks-qt5/wiki)

**genpac**

[genpac-gihub](https://github.com/JinnLynn/genpac)

系统-网络-自动-pac ：file:///home/username/autopac.pac

**浏览器**

google-chrome

### 英语

**anki**

[anki用户手册](https://apps.ankiweb.net/docs/manual.html)

**chrome-anki划词助手**

[anki 划词制卡助手-github](https://github.com/ninja33/anki-dict-helper)

**anki connect（anki划词助手配套文件）**

[anki划词助手配套文件](https://ninja33.github.io/20160817/anki-connect/#more)

### Python版本和编译

因为 python2 和 python3 在工作中都会用到，建议都安装，包括常见的编译环境

```
    # 安装 Python 发布版本，dev包必须安装，很多用pip安装包都需要编译
    
    sudo apt-get install python2.7 python2.7-dev python3.6 python3.6-dev
    # 很多pip安装的包都需要libssl和libevent编译环境
    sudo apt-get install build-essential libssl-dev libevent-dev libjpeg-dev libxml2-dev libxslt-dev python-dev python3-dev libncurses5-dev
```

**安装 pip**

`sudo apt-get install python-pip`

**安装 virtualenv**

`sudo pip install virtualenv`

**安装 virtualenvwrapper**

`sudo pip install virtualenvwrapper`

[python 虚拟环境virtualenv/virtualenvwrapper设置](http://www.jianshu.com/p/44ab75fbaef2)

[Python--Virtualenv简明教程](http://www.jianshu.com/p/08c657bd34f1)

### 环境配置

**安装配置 vim**

安装vim
```
# 卸载安装的 vim

dpkg -l | grep vim

# 根据上面显示的内容进行卸载

sudo dpkg -P vim vim-common vim-runtime vim-tiny

# 安装依赖库

sudo apt-get  libncurses5-dev libgnome2-dev libgnomeui-dev \
    libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
    libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
    python3-dev ruby-dev lua5.1 lua5.1-dev git

# 下载最新的 vim

git clone https://github.com/vim/vim.git

# 编译安装最新的 vim

cd vim

./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp \
            --enable-pythoninterp \
            --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu \
            --enable-perlinterp \
            --enable-luainterp \
            --enable-gui=gtk2 --enable-cscope --prefix=/usr

make VIMRUNTIMEDIR=/usr/share/vim/vim80

sudo make install

# 将vim设置为默认编辑器

sudo update-alternatives --install /usr/bin/editor editor /usr/bin/vim 1

sudo update-alternatives --set editor /usr/bin/vim

sudo update-alternatives --install /usr/bin/vi vi /usr/bin/vim 1

sudo update-alternatives --set vi /usr/bin/vim
```

vim的配置文件[.vimrc](https://github.com/NingAnMe/NingAnMe.github.io/.vimrc)

**安装 Vunder **

`git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

`PluginInstall` 将插件都安装到当前的配置环境中

**安装 youcompleteme**

```
# 将youcompleteme clone 下来
git clone https://github.com/Valloric/YouCompleteMe.git
# 进入目录 将依赖克隆下来
cd YouCompleteMe
git submodule update --init --recursive
# 将准备好的YouCompleteMe目录移动到~/.vim/bundle/YouCompleteMe
cp ./YouCompleteMe ~/.vim/bundle/YouCompleteMe
# 使用 cmake 和 python-dve 进行编译
mkdir ycm_build
cd ycm_build
cmake -G "Unix Makefiles" . ~/.vim/bundle/YouCompleteMe/third_party/ycmd/cpp
cmake --build . --target ycm_core
# 如果编译过程没有出错,就可以在Vunder安装了
```

**安装 zsh **

`sudo apt-get install zsh -y`

把Zsh设置为当前用户的默认Shell

`chsh -s /bin/zsh`

**安装 oh-my-zsh**

`sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`

**配置 ~/.zshrc**

```
export ZSH=$HOME/.oh-my-zsh
# rt ZSH=$HOME/.oh-my-zsh
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
# source /usr/local/bin/virtualenvwrapper.sh
# source ~/.iterm2_shell_integration.`basename $SHELL`
```

**安装 zsh 配色**

16.04以上版本,直接选中 编辑-首配置-配色-solarized

或者安装 配色

```
$ git clone https://github.com/Anthony25/gnome-terminal-colors-solarized.git
$ cd gnome-terminal-colors-solarized
$ ./install.sh
```

**安装 git**

`$ sudo apt-get install git`

*git 教程*

[Git中.gitignore的配置语法](http://www.jianshu.com/p/ea6341224e89)

[廖雪峰 git 教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)


**Python风格指南**

[Python风格指南](https://lizhe2004.gitbooks.io/code-style-guideline-cn/content/python/python-pep8.html)


### 参考资料

[在Ubuntu下配置舒服的Python开发环境](http://xiaocong.github.io/blog/2013/06/18/customize-python-dev-environment-on-ubuntu/)

[Vim与Python真乃天作之合：将Vim打造为强大的Python开发环境](http://www.jianshu.com/p/bc19b91354ef)

[所需即所获：像 IDE 一样使用 vim](https://wizardforcel.gitbooks.io/use-vim-as-ide/content/)

[把vim配置成顺手的python轻量级IDE](http://www.jianshu.com/p/f0513d18742a)

[开源世界旅行手册](https://www.gitbook.com/book/wizardforcel/os-world-trip/details)

[Python开发生态环境简介](https://github.com/dccrazyboy/pyeco/blob/master/pyeco.rst)



