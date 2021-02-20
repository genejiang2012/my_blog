# 阿里云Centos 升级到Vim8

[TOC]

## 概述

当前阿里云Centos中VIM的版本是7， 需要升级到8

## 查看python和 vim的版本

1. 查看vim中支持的python版本

   ```
   [root@iZbp17x826kn36gp8wscduZ tmp]# vim --version | grep python
   +cryptv          +linebreak       +python/dyn      +viminfo
   +cscope          +lispindent      -python3         +vreplace
   
   ```

   可以看到python3是不支持的

2. 查看python和vim版本

   ```
   [root@iZbp17x826kn36gp8wscduZ tmp]# which python
   /usr/bin/python
   [root@iZbp17x826kn36gp8wscduZ tmp]# which python3
   /usr/bin/python3
   [root@iZbp17x826kn36gp8wscduZ tmp]# which vim
   /usr/bin/vim
   
   ```

   

## 删除旧的VIM

删除旧的VIM

```
[root@iZbp17x826kn36gp8wscduZ ~]# yum list installed | grep -i vim
vim-common.x86_64                    2:7.4.629-6.el7                   @base    
vim-enhanced.x86_64                  2:7.4.629-6.el7                   @base    
vim-filesystem.x86_64                2:7.4.629-6.el7                   @base    
vim-minimal.x86_64                   2:7.4.629-6.el7                   @anaconda
[root@iZbp17x826kn36gp8wscduZ ~]# yum remove vim-enhanced vim-common vim-filesystem vim-minimal
```

## 安装依赖

```
[root@iZbp17x826kn36gp8wscduZ ~]# yum install -y gcc make ncurses ncurses-devel
[root@iZbp17x826kn36gp8wscduZ ~]# yum install ctags git tcl-devel \
    ruby ruby-devel \
    lua lua-devel \
    luajit luajit-devel \
    python python-devel \
    perl perl-devel \
    perl-ExtUtils-ParseXS \
    perl-ExtUtils-XSpp \
    perl-ExtUtils-CBuilder \
    perl-ExtUtils-Embed
```

## 下载VIM8

```
[root@iZbp17x826kn36gp8wscduZ ~]# git clone clone https://github.com/vim/vim.git | cd vim

```



## 修改配置

```
./configure --with-features=huge \
--enable-multibyte \
--enable-rubyinterp=dynamic \
--with-ruby-command=/usr/bin/ruby \
--enable-pythoninterp=dynamic \
--with-python-config-dir=/usr/lib64/python2.7/config \
--enable-python3interp=dynamic \
--with-python3-config-dir=/usr/lib64/python3.6/config-3.6m-x86_64-linux-gnu \
--enable-cscope \
--enable-gui=auto \
--enable-gtk2-check \
--enable-fontset \
--enable-largefile \
--disable-netbeans \
--with-compiledby="genejiang2012@outlook.com" \
--enable-fail-if-missing \
--prefix=/usr/local
```

参数说明如下：

--with-features=huge：支持最大特性

--enable-rubyinterp：打开对ruby编写的插件的支持

--enable-pythoninterp：打开对python编写的插件的支持

--enable-python3interp：打开对python3编写的插件的支持

--enable-luainterp：打开对lua编写的插件的支持

--enable-perlinterp：打开对perl编写的插件的支持

--enable-multibyte：打开多字节支持，可以在Vim中输入中文

--enable-cscope：打开对cscope的支持

--with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu/ 指定python 路径

--with-python3-config-dir=/usr/lib/python3.5/config-3.5m-x86_64-linux-gnu/ 指定python3路径

--prefix=/usr/local/vim：指定将要安装到的路径(自行创建)

## 安装

```
[root@iZbp17x826kn36gp8wscduZ ~]# make | make install
```

## 确认安装

```
[root@iZbp17x826kn36gp8wscduZ ~]# vim --version | grep python

+comments          +libcall           +python/dyn        +visual
+conceal           +linebreak         +python3/dyn       +visualextra
```

## 配置插件

1. 将windows下的_vimrc文件复制到``~``路径下
2. 重命名```_vimrc```为```.vimrc```
3. vimrc文件是从windows下复制过来的， 所有存在^M， 字符的问题
4. 用dos2unix转换一下：``` dos2unix .vimrc```
5. 打开.vimrc, 用```BundleInstall```来安装所有插件



## 遇到的问题

1. 从github上下载vim源代码包， 太慢
2. 下载好后， 解压显示下载不完全