# Ubuntu系统Python工作环境配置

### 升级系统

`sudo apt-get update`

`sudo apt-get upgrade`

### 系统设置

系统-语言-英文-重启-修改中文文件名 ; 系统-语言-中文-重启-保留英文文件名

系统-亮度和锁屏

系统-外观

系统-网络-自动-pac

系统-软件和更新-附加驱动

### 科学上网

**shadowsocks-qt5**

[shadowsocks-qt5-github-wiki](https://github.com/shadowsocks/shadowsocks-qt5/wiki)

**genpac**

[genpac-gihub](https://github.com/JinnLynn/genpac)

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

### 环境配置

**安装 bash-it**

`git clone http://github.com/revans/bash-it.git ~/.bash_it`
`~/.bash_it/install.sh`

安装完成后将下面的代码附加到~/.bashrc的后面：

```
    if [ -f ~/.bash_profile ]; then
        . ~/.bash_profile
    fi
```

[bash-it-github](https://github.com/Bash-it/bash-it)

**安装 git**

`$ sudo apt-get install git`

[Git中.gitignore的配置语法](http://www.jianshu.com/p/ea6341224e89)
[廖雪峰 git 教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)

**安装 git-flow**

[Using git-flow to automate your git branching workflow](https://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/)

[A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)

**安装 pip**
`$ sudo apt-get install python-pip`

**安装 virtualenv**

`sudo pip install virtualenv`

[Python--Virtualenv简明教程](http://www.jianshu.com/p/08c657bd34f1)

**安装 virtualenvwrapper**

`sudo pip install virtualenvwrapper`

[python 虚拟环境[virtualenv/virtualenvwrapper]设置](http://www.jianshu.com/p/44ab75fbaef2)

**Python风格指南**

[Python风格指南](https://lizhe2004.gitbooks.io/code-style-guideline-cn/content/python/python-pep8.html)

### 编辑器

**VIM**

shell终端自带vim学习手册：输入指令`vimtutor`

[可视化学习 vim](http://www.openvim.com/)

[所需即所获：像 IDE 一样使用 vim](https://wizardforcel.gitbooks.io/use-vim-as-ide/content/)

[Vim与Python真乃天作之合：将Vim打造为强大的Python开发环境](http://www.jianshu.com/p/bc19b91354ef)

**Pycharm**

[https://www.jetbrains.com/help/pycharm/installation-and-launching.html\#linux](https://www.jetbrains.com/help/pycharm/installation-and-launching.html#linux)

[https://www.jetbrains.com/help/pycharm/using-vim-editor-emulation-in-pycharm.html](https://www.jetbrains.com/help/pycharm/using-vim-editor-emulation-in-pycharm.html)

[http://www.cnblogs.com/zhaozihan/p/6297217.html](http://www.cnblogs.com/zhaozihan/p/6297217.html)


### 参考资料

[在Ubuntu下配置舒服的Python开发环境](http://xiaocong.github.io/blog/2013/06/18/customize-python-dev-environment-on-ubuntu/)

[开源世界旅行手册](https://www.gitbook.com/book/wizardforcel/os-world-trip/details)

[Python开发生态环境简介](https://github.com/dccrazyboy/pyeco/blob/master/pyeco.rst)

[Vim与Python真乃天作之合：将Vim打造为强大的Python开发环境](http://www.jianshu.com/p/bc19b91354ef)

[所需即所获：像 IDE 一样使用 vim](https://wizardforcel.gitbooks.io/use-vim-as-ide/content/)

