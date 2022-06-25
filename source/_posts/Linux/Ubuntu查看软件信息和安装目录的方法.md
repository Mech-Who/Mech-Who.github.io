# Ubuntu查看软件信息和安装目录的方法

1. `dpkg -l` 列出已经安装了的所有包
2. `dpkg -L <packageName>`列出当前包的所有相关目录
3. `aptitude show <packageName>`列出当前包的相关信息,aptitude工具需要自行安装
4. `which <packageShell>`在环境变量中找到命令的位置
5. `whereis <packageName>`给出主要的相关目录