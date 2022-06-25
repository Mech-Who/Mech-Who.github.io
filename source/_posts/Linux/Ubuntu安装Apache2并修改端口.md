# Ubuntu 安装Apache2和修改Apache2端口

## 一、背景

Linux系统：[Ubuntu](http://www.linuxidc.com/topicnews.aspx?tid=2) 20.04

本机为了给朋友部署一个简单的静态页面,然后使用了Apache2,现在因为个人需要,需要用nginx,结果发现80端口被Apache2占了,因此要修改端口

## 二、Apache2安装

安装很简单：

`apt install apache2`

> 然后再安装nginx的时候会自动启动失败，因为我的Apache2占着80端口和443端口呢。

## 三、Apache2监听端口修改

1. 通过whereis apache2查找安装目录,发现目录为:`/etc/apache2`

   打开该目录下的`ports.conf`文件，

   把所有的80端口改成**要监听的端口**1，443改成**要监听的端口**

   然后看文件注释上说也要修改/etc/apache2/sites-enabled/000-default文件

	2. 打开`/etc/apache2/sites-enabled/000-default`

    把`<VirtualHost *:80>`中的80修改成**要监听的端口1**

	3. 验证一下

    然后看到根目录在/var/www下面

    到/var/www/目录看到有index.html文件

    ```html
    <html><body><h1>It works!</h1>
    <p>This is the default web page for this server.</p>
    <p>The web server software is running but no content has been added, yet.</p>
    </body></html>
    ```

    现在重新启动apache2

    `service apache2 restart`

    并有报错

    ```shell
    \* Restarting web server apache2
    apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1 for ServerName
     ... waiting apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1 for ServerName   [ OK ]
    ```

    此时可以打开/etc/apache2/apache2.conf文件,添加一句：`ServerName localhost`

    再次重启后错误消失。

    打开网页，输入`localhost:<修改后要监听的端口1>`地址，看到Index.html页面显示出来了,验证成功。