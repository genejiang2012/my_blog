# Github连接太慢的问题

[TOC]

## 修改本地hosts文

```text
windows系统的hosts文件的位置如下：C:\Windows\System32\drivers\etc\hosts
mac/linux系统的hosts文件的位置如下：/etc/hosts
```

## 增加[http://github.global.ssl.fastly.net](https://link.zhihu.com/?target=http%3A//github.global.ssl.fastly.net)和[http://github.com](https://link.zhihu.com/?target=http%3A//github.com)的映射##

```text
获取Github相关网站的ip
访问https://www.ipaddress.com，拉下来，找到页面中下方的“IP Address Tools – Quick Links”
分别输入github.global.ssl.fastly.net和github.com，查询ip地址
下面是我的配置
140.82.114.4	github.com
199.232.5.194	github.global.ssl.fastly.net
```

3.命令提示符中输入ping [github.com](https://link.zhihu.com/?target=http%3A//github.com)