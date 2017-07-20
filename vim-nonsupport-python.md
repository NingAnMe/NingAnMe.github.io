# VIM不支持Python的解决办法

### 检查 vim 是不是支持 Python

`anning@NingAnMe:~$ vim --version | grep python`

```
结果如下

+cryptv          +linebreak       **-python**          +vreplace
+cscope          +lispindent      **+python3**         +wildignore
链接方式: gcc   -Wl,-Bsymbolic-functions -fPIE -pie -Wl,-z,relro -Wl,-z,now -Wl,--as-needed -o vim        -lm -ltinfo -lnsl  -lselinux  -lacl -lattr -lgpm -ldl     -L/usr/lib/python3.5/config-3.5m-x86_64-linux-gnu -lpython3.5m -lpthread -ldl -lutil -lm
```

支持 python3 ，不支持 python2

### 卸载安装的 vim

`$ dpkg -l | grep vim`

根据上面显示的内容进行卸载

`$ sudo dpkg -P vim vim-common vim-runtime vim-tiny`

### 安装依赖库

```
sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev \
    libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
    libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
    python3-dev ruby-dev lua5.1 lua5.1-dev git
```
### 下载最新的 vim

`$ git clone https://github.com/vim/vim.git`

### 编译安装最新的 vim

```
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
```

### 将vim设置为默认编辑器

```
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/vim 1

sudo update-alternatives --set editor /usr/bin/vim

sudo update-alternatives --install /usr/bin/vi vi /usr/bin/vim 1

sudo update-alternatives --set vi /usr/bin/vim
```
