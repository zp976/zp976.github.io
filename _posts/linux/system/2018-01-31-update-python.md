---
layout: post
title: "升级python-从2.7.5升级到2.7.13"
date: 2018-01-30 22:20:00 +0800 
categories: linux
tag: Linux
---
* content
{:toc}

### 安装gcc,依赖

    yum install gcc
    yum install zlib-devel bzip2-devel openssl-devel ncurses-devel
    yum -y install tcl-devel tk-devel
<!-- more -->
### 下载安装包
    
    wget https://www.python.org/ftp/python/2.7.13/Python-2.7.13.tar.xz
### 解压

    xz -d Python-2.7.13.tar.xz
    tar xvf Python-2.7.13.tar
### 安装

    cd Python-2.7.13
    ./configure --prefix=/usr/local/python-2.7.13 --enable-shared CFLAGS=-fPIC
    make && make install
### 删除由make命令产生的文件
    
    make clean　　
### 删除由./configure产生的文件

    make distclean
### 将老版本python更换

    mv /usr/bin/python /usr/bin/python2.7.5
### 更换默认python

    建议：export PATH="/usr/local/python-2.7.13/bin:$PATH"
    或者
    ln -s /usr/local/python-2.7.13/bin/python2.7   /usr/bin/python

### 修改 yum中的python 

    将#!/usr/bin/python改为 #!/usr/bin/python2.7.5
    vim /usr/bin/yum

### 下载setuptools

    wget --no-check-certificate https://pypi.python.org/packages/source/s/setuptools/setuptools-1.4.2.tar.gz
### 安装setuptools

    tar -xvf setuptools-1.4.2.tar.gz
    cd setuptools-1.4.2
    python setup.py install
### 安装pip工具
    
    cd ..
    wget "https://pypi.python.org/packages/source/p/pip/pip-8.1.1.tar.gz#md5=6b86f11841e89c8241d689956ba99ed7"
    tar xzf pip-8.1.1.tar.gz
    cd pip-8.1.1
    python setup.py install
    #升级python
    pip install --upgrade pip
    pip install numpy pandas matp
### 安装其他依赖：
    
    yum install mysql mysql-devel mysql-libs  #MySQL-python 依赖mysql，否则提示错误
    pip install MySQL-python
    
### yum 安装其他程序可能报错

    Downloading packages:
    Traceback (most recent call last):
     File "/usr/libexec/urlgrabber-ext-down", line 22, in <module>
    from urlgrabber.grabber import \
    ImportError: No module named urlgrabber.grabber
### 解决方案：

    vi /usr/libexec/urlgrabber-ext-down
    #把头部的python改成和/usr/bin/yum中一样的
