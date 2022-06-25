# Ubuntu安装Node环境

## 一、安装npm工具

首先通过ubuntu包管理工具进行npm的安装:

`sudo apt install npm -y`

其中`-y`表示询问均默认为yes,就不需要自己输入y了

可以通过`npm -v`验证是否安装成功

## 二、安装n工具(nodejs)

安装好npm之后,就可以使用npm安装n工具了

`sudo npm install n -g`

其中`-g`表示全局安装,大概是指不需要为之配环境变量?

## 三、安装node

然后就可以通过n工具进行node的安装,各个版本都可以

`sudo n <nodeVersion>`

比如

`sudo n lst`: 安装最新版(lastest)

`sudo n 14.18.2`: 安装14.18.2版本

## 四、更新npm

安装完node之后可以进行npm的更新

`npm install npm -g`