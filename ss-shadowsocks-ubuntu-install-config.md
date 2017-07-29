---
title: 在 Ubuntu 上部署 shaodowsocks, 并优化速度
---

## 需要掌握的基本技能

- 使用ssh工具连接Linux VPS进行相关操作。

- 了解ubuntu系统版本。

- 会vim的基本操作。

## 需要的资源

- 搬瓦工VPS一个，ubuntu 16.04版本。**请购买KVM架构的VPS服务器版本。**如果不知道什么是KVM，百度查阅相关资料。否则到后面速度优化无法进行。不优化速度根本看不了 youtube 1080高清。

### 使用的服务

- shadowsocks-libev 是 shadowsocks 服务的 C 语言重写版本，软件体积小，速度快，适合在小内存服务器中使用，如搬瓦工最便宜的服务器。

- TCP BBR拥塞控制技术。目的是要尽量跑满带宽，可以明显加快ss服务的速度，看1080高清无压力，效果不比锐速差。

### 优化速度，部署TCP BBR

只有 KVM 架构的 VPS 服务器才能更新 Linux 内核版本,上面提到了.

通过ssh连接VPS，推荐使用Xshell。

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/4219173-fdf0de25e64faffa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

连接后开始执行下面的命令。

下载最新的 Linux 内核。因为只有内核版本在4.9版本以上才能开启 BBR 。

`wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.11/linux-image-4.11.0-041100-generic_4.11.0-041100.201705041534_amd64.deb`

安装最新内核

`dpkg -i linux-image-4.*.deb`

更新 grub 系统引导文件

`update-grub`

重启服务器

`reboot`

开机后执行 `uname -r` 命令看看是不是内核4.11版本。

执行 `lsmod | grep bbr`，如果结果中没有 tcp_bbr 的话就依次执行下面五条命令

```modprobe tcp_bbr
echo "tcp_bbr" >> /etc/modules-load.d/modules.conf
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
```

执行下面两条命令查看结果中是否都有*bbr*，如果有的话，说明 tcp bbr 模块已经启动。

```sysctl net.ipv4.tcp_available_congestion_control
sysctl net.ipv4.tcp_congestion_control
```

## 开始部署ss服务

添加安装时使用的源

`sudo add-apt-repository ppa:max-c-lv/shadowsocks-libev`

更新软件

`sudo apt-get update`

安装 shadowsocks-libev服务

`sudo apt install shadowsocks-libev`

到此为止，shadowsocks服务已经安装到VPS服务器当中了。

下面要做的就是配置shadowsocks服务。

安装vim编辑器

`sodu apt-get install vim`

打开shadowsocks配置文件

`sudo vim /etc/shadowsocks-libev/config.json`

打开后将下面的内容粘贴到这个文件中，然后修改相关内容后保存。

```
{
     "server":"**修改为你的VPS地址，如101.22.33.204**",
     "server_port":8388,
     "local_address": "127.0.0.1",
     "local_port":1080,
     "password":"**修改为你希望的连接密码，如ninganme**",
     "timeout":300,
     "method":"aes-256-cfb",
     "fast_open": false
}
```

其他的内容不需要修改，除非你知道是做什么的。例如 8388 是连接的时候远程服务器的端口号。

然后打开 shadowsocks服务,并在后台运行,输完命令后敲一下回车。

`nohup ss-server -c /etc/shadowsocks-libev/config.json &`

到此为止，shadowsocks服务已经在你的服务器部署完毕了，你可以使用手机或者电脑连接测试了。

linux 系统使用 shadowsocks-qt5 连接,windows ios 和 安卓系统使用 shaodowsocks 连接
