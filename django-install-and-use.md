---
title: Django 的安装和基本指令
---
## Django环境构建与目录结构

### 安装Django

首先安装pip组件

`sudo apt-get install python3-pip`

如果pip版本过低,可以使用以下命令对其进行升级

`sudo pip3 install --upgrade pip`

安装Django

`sudo pip3 install Django`

### 使用 virtualenv 实现开发环境分离

安装virtualenv

`sudo pip3 install virtualenv`

创建一个虚拟环境

`virtualenv django`

读取环境使用 source 命令

`source ./django/bin/activate`

退出虚拟开发黄静,使用

`deactivate`

### 介绍Django的结构

urls.py

链接入口,关联到对应的 views.py 的一个函数,访问的连接就对应一个函数

views.py

处理用户发出的请求,从 urls.py 中对应而来,渲染 templates 中的网页

models.py

与数据库操作相关,存入或读取数据时使用.不使用数据库的时候,也可以当作一般的类封装文件

forms.py

表单,用户在浏览器上输图提交,对数据的验证工作以及输入框的生成等工作,都依托于次

admin.py

后台文件

settings.py

Django 的设置和配置文件,比如 DEBUG 开关

templates目录

views.py中的函数渲染 templates 中的 html 模板,得到动态内容的网页,也可以使用缓存来提高渲染速度

## Django 基本命令

### 新建一个Django Project

`django-admin.py startproject <project-name>`

### 新建 app

`python3 manage.py startapp <app-name>`

或者

`django-admin.pt startapp <app-name>`

### 同步数据库

```
python manage.py makemigrations
python manege.py migrate
```
当在 models.py 中新增类时,运行它就可以自动在数据库中创建表

### 使用开发服务器

默认情况下,在 8080 端口启动

`python manage.py runserver`

### 清空数据库

选择 yes 会把数据库全部清空掉,只留下空表

`python manage.py flush`

### 创建超级管理员

`python manage.py createsuperuser`

### 导出数据 导入数据

`python manage.py dumpdata <appname> > <appname>.json`

### Django 项目环境终端

这个命令和直接运行python 进入shell 的区别是:你可以在这个shell里面调用当前项目的modle.py中的API,对于操作数据和一些小测试非常方便

`python manage.py shell`

### 数据库命令行

Django 会自动进入在 settings.py 中设置的数据库,这个终端可以执行数据库的SQL语句.

`python manage.py dbshell`

### 直接输入以下命令,查看更多

`python manage.py`

## 视图和连接路由

### 创建新的项目

`django-admin.py startproject <项目名>`

### 在项目的文件中创建新的应用

`python3 manage.py startapp <应用名>`

### 将新定应的应用添加到 settings.py 的 INSTALLED_APPS

Django 就可以自动找到app中的模板文件

```
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    '<新的应用>',
)
```

### 定义视图函数

编辑 views.py 文件,第一行是用来声明文本编码为 utf-8,HttpResponse 是用来向网页返回内容,定义index()函数,第一个函数必须是request,request变量包含了 GET 或者 POST 方式

```
#coding: utf-8
from django.shortcuts import render
from django.http import HttpResponse


def index(request):
    return HttpResponse(u"Hello World!")
```

### 定义视图相关的 URL,即路由配置

编辑 urls.py 文件,从应用文件中引入 views 视图,然后赋值给链接函数

```
from django.conf.urls import url
from django.contrib import admin
from <应用名> import views as <应用名>_views  # new

urlpatterns = [
    url(r'^$', <应用名>_views.index),  # new
    url(r'^admin/', admin.site.urls),
]
```
