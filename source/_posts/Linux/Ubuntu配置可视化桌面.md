# Ubuntu配置可视化桌面

## 一、升级系统

使用以下两条指令进行系统升级：

`sudo apt-get update`

`sudo apt-get upgrade`

## 二、安装经典桌面环境Gnome桌面

也是两条指令

`sudo apt-get install ubuntu-desktop`

`sudo apt-get install gnome`

## 三、自定义安装桌面

6条指令:

`sudo apt-get install x-window-system-core`

`sudo apt-get install gnome-core`

`sudo apt-get install language-pack-gnome-zh-hant`

`sudo apt-get install scim`

`sudo apt-get install gdm`

`sudo apt-get install synaptic`

## 四、安装Linux Mint的桌面环境系统Cinnamon 3.0

4条指令:

`sudo apt-get install --no-install-recommends ubuntu-desktop`

`sudo add-apt-repository ppa:embrosyn/cinnamon`

`sudo apt update`

`sudo apt install cinnamon`

## 五、配置root登陆权限

1. 默认情况不允许用root账号直接登录图形界面

   可以通过修改`vim/usr/share/lightdm/lightdm.d/50-ubuntu.conf`文件来允许root直接登录,增加`<br />greeter-show-manual-login=true allow-guest=false`。

2. 登陆之后每次会弹出一个小错误

   在`/root/.profile`文件中将`mesg n||true`修改为`tty -s && mesg n || true`即可

## 六、注意事项

1. 配置完成之后需要使用以下命令进行重启,然后才能正常使用

   `sudo init 6`

2. 配置完成后必须使用vnc连接才能访问可视化桌面,如果只是ssh连接的话,仍然是命令行形式的连接。

3. 可视化桌面配置完成后需要安装一些软件,否则桌面一片空白,十分难用orz.