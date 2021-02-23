# oh-my-zsh的安装及配置



[TOC]

## 查看系统已装好的shell

输入命令`cat /etc/shells`

```
[root@iZbp17x826kn36gp8wscduZ ~]# cat /etc/shells
/bin/sh
/bin/bash
/usr/bin/sh
/usr/bin/bash
```

## 安装zsh

1、检查是否已经安装了zsh，输入 `zsh --version` 查看版本信息，若安装了，这个命令会输出zsh当前版本号

2、若没有安装zsh，则在终端执行：

- 若 Redhat Linux，执行 `sudo yum install zsh`
- 若 Ubuntu Linux，执行 `sudo apt-get install zsh`

### 设置使用 zsh

在终端执行 `chsh -s $(which zsh)`，根据提示输入当前用户的密码

### 安装git

在终端执行 `sudo apt-get install git` 或者 `yum install git`

### 安装 oh-my-zsh

```
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```

## 重启

重启系统， shell变成oh-my-zsh

## 主题

配置主题, 可以通过修改`~/.zshrc`中的环境变量`ZSH_THEME`来完成，我最后挑中了`agnoster`

```
ZSH_THEME="agnoster"
```

## 插件

下载插件

```
git clone https://github.com/zsh-users/zsh-autosuggestions.git .oh-my-zsh/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git .oh-my-zsh/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-completions.git .oh-my-zsh/plugins/zsh-completions
```

修改`.zshrc`

```
plugins=(
  git z zsh-autosuggestions extract web-search zsh-syntax-highlighting 
)
```



