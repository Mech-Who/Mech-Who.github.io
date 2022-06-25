# Springboot后端项目部署

参考博客: [(55条消息) Ubuntu部署springboot并设置后台运行和日志监控_DanceDonkey的博客-CSDN博客](https://blog.csdn.net/qq_43750656/article/details/108964955)

1. 查看防火墙是否开启

   `sudo ufw status`

   如果显示`Status:inactive`则表示未开启

   如果是开启状态,则需要通过以下命令关闭防火墙

   `sudo ufw disable`

   其他相关操作,可以参考:[(55条消息) Ubuntu常用防火墙命令_仲夏宁叶香的博客-CSDN博客_ubuntu 防火墙命令](https://blog.csdn.net/M82_A1/article/details/97250290)

2. 创建一个日志文件

   `touch <日志文件名>.log`

3. 持续运行后端项目并后台运行

   `nohup java -jar <jar包名> > <日志文件名>.log 2>&1 &`

   如果在jar包目录则可以直接用jar包名,如果不在则需要用绝对路径,日志文件同理

   后台运行和持续运行相关命令可参考: [(55条消息) Ubuntu中如何使得程序在后台运行_weixin_30919919的博客-CSDN博客](https://blog.csdn.net/weixin_30919919/article/details/98106625)
   
4. 代码中的路径要注意修改为部署用的ip

   1. yaml文件中的
   2. intercepter中的
   3. uploadProperties中的

