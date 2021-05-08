# Jenkins的安装

[TOC]

## 简介

> Jenkins是一个开源软件项目，是基于Java开发的一种持续集成工具，用于监控持续重复的工作，旨在提供一个开放易用的软件平台，使软件项目可以进行持续集成

## 安装

1. 拉取镜像
	```shell
	docker pull jenkins/jenkins
	```
	
2. 创建jenkins工作目录并授权，可以根据需要自行调整目录路径

   ```
   mkdir -p /var/jenkins_home/
   chown 777 /var/jenkins_home/
   ```
3. 创建并启动容器

   ```
   docker run -itd --name jenkins \
   -p 9666:8080 \
   -p 50000:50000 \
   -v /var/jenkins_home:/var/jenkins_home \
   -v /etc/localtime:/etc/localtime jenkins/jenkins
   ```

   参数说明：

   `-d` 后台运行镜像
   `–name` `myjenkins` 容器别名
   `-p 9666:8080` 将镜像的8080端口映射到服务器的9666端口。
   `-p 50000:50000` 将镜像的50000端口映射到服务器的50000端口
   `-v /var/jenkins_home:/var/jenkins_home` 其中`/var/jenkins_home`目录为容器jenkins工作目录，我们将硬盘上的一个目录挂载到这个位置，方便后续更新镜像后继续使用原来的工作目录。
   `-v /etc/localtime:/etc/localtime` 让容器使用和服务器同样的时间设置。

4. 查看jenkins是否启动成功，如果status为up则表示启动成功
   ```
   docker ps -l
   ```
5. 访问Jenkins， 使用服务器的IP地址和端口号

   **访问jenkins地址，ip修改为服务器ip，端口改为容器8080端口映射到服务器的9666端口**

6. 输入admin密码

   admin密码在下面的文件中可以找出

   ```
   cat /var/jenkins_home/secrets/initialAdminPassword
   ```
7. 安装必要的插件