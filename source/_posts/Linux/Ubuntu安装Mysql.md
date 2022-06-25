# Ubuntu安装Mysql

## 一、删除旧版本(可选)

1. 通过以下命令,进行旧版本软件的删除

​		`sudo apt purge mysql-*`

2. 删除相关的配置文件

​		`sudo rm -rf /etc/mysql/ /var/lib/mysql`

3. 使用autoremove命令(不懂的话,不要使用,容易导致误删配置文件)

   > apt-get命令:
   >
   > clean - 删除包缓存中的**所有**包
   >
   > autoclean - 将已经删除了的软件包的.deb安装文件从硬盘中删除掉
   >
   > remove - 卸载软件包
   >
   > autoremove - 卸载所有自动安装且不再使用的软件包
   >
   > purge - 卸载并清除软件包的配置

​		`sudu apt autoremove`

​		`sudu apt autoclean`

## 二、安装mysql

1. 通过以下命令可以进行mysql软件的安装:

   `	sudo apt install mysql-server mysql-client libmysqlclient-dev -y`

2. 可以使用`netstat`命令验证是否安装成功(`netstat`需要安装`net-tools`包才可以使用)

   `sudo netstat -tap | grep mysql`

3. 也可以使用以下命令验证是否安装成功

   `mysql -v`

## 三、mysql设置密码

1. 使用以下命令进入mysql命令行:

   `mysql -u root -p`

   然后会让你输入密码,此时因为是第一次登录,直接输入回车即可成功登录。

2. 修改密码

   1. 通过以下命令查询mysql用户信息(使用finalshell的话,可能会输入命令后命令行变成乱码!)

      `select user,host,authentication_string from mysql.user;`

      ![image-20220501112359785](E:\学习笔记\Typora\Linux\Ubuntu安装Mysql.assets\image-20220501112359785.png)

   2. 应用mysql数据库

      `use mysql;`

   3. 首先置空密码

      `update user set authentication_string='' where user='root';`

   4. 刷新MySQL的系统权限相关表

      `flush privileges;`

      或者回到linux命令行,通过以下命令重启mysql服务也可以

      `sudo  service mysql restart`

   5. 然后通过以下命令设置密码

      `alter user 'root'@'localhost' identified with mysql_native_password by '123456';` 

## 四、远程访问配置

1. 修改配置文件

   `vim /etc/mysql/mysql.conf.d/mysqld.cnf`

   找到`bind-address`

   并将其值从`127.0.0.1`修改为`0.0.0.0`

   修改完成后,重新启动mysql服务

   `sudo service mysql restart`

2. 创建一个新用户用于远程连接

   `create user 'admin'@'%' identified by '123456';`

   用户名为`admin`,密码为`123456`

   赋予相应的权限,`*.*`表示所有权限均可访问

   `grant all on *.* to 'admin'@'%';`

   再次刷新权限信息

   `flush privileges;`

3. 进行远程连接测试

   ![image-20220501144526904](E:\学习笔记\Typora\Linux\Ubuntu安装Mysql.assets\image-20220501144526904.png)

## 五、其他

查看mysql历史命令

`cat  ~/.mysql_history`