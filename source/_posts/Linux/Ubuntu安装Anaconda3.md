# Ubuntu安装Anaconda3

## 参考博客：

https://blog.csdn.net/m0_50117360

## 一、下载Anaconda3的安装文件并安装

在官网找到安装文件并下载

1. 官方网站：[Anaconda | Anaconda Distribution](https://www.anaconda.com/products/distribution#download-section)
2. 清华镜像源：[anaconda | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)

安装Anaconda3

将下载下来的安装文件放到服务器中：

Ubuntu下应该是：`Anaconda3-5.3.1-Linux-x86_64.sh`

然后执行该文件：

`bash Anaconda3-5.3.1-Linux-x86_64.sh`

然后会提示你进行安装

![image-20220507200330298](E:\学习笔记\Typora\Linux\Ubuntu安装Anaconda3.assets\image-20220507200330298.png)

此时输入回车,会让你查看license terms,然后询问你是否同意

![image-20220507200425241](E:\学习笔记\Typora\Linux\Ubuntu安装Anaconda3.assets\image-20220507200425241.png)

输入yes之后,会让你选择是否要终止安装,或是选择其他的安装目录

![image-20220507200518946](E:\学习笔记\Typora\Linux\Ubuntu安装Anaconda3.assets\image-20220507200518946.png)

如果不需要自定义安装目录的话,直接回车即可,否则输入你要自定义的路径,再按回车即可,然后就开始安装了

安装完成后会问你是否需要帮你初始化,我这里输入了yes,等于帮你配置好环境变量

如果没有让它进行初始化的话,可以自行配置环境变量

一般可以放在`~/.bashrc`文件中

`export PATH="<安装目录>/anaconda3/bin:$PATH"`

安装目录大家根据自己最开始定义的来配置就行

![image-20220507200625965](E:\学习笔记\Typora\Linux\Ubuntu安装Anaconda3.assets\image-20220507200625965.png)

到这里Anaconda3已经安装成功了

但是,它会接着问你,Anaconda和微软合作了,要不要帮你安装VSCode,我的看法是可以但没必要,但是我在图中进行了安装尝试

![image-20220507200933974](E:\学习笔记\Typora\Linux\Ubuntu安装Anaconda3.assets\image-20220507200933974.png)

虽然最后失败了,因为缺少安装anaconda-extension失败了orz

![image-20220507201021505](E:\学习笔记\Typora\Linux\Ubuntu安装Anaconda3.assets\image-20220507201021505.png)

一直问我要不要retry,结果retry又一直失败,最后先选择no退出了,感觉应该没安装成功orz

不过到这里Anaconda3已经安装成功了,所以无关紧要了.

由于配置了~/.bashrc文件,因此要重载一下该文件

`source ~/.bashrc`

然后就可以使用conda命令了

## 常用的conda命令

```shell
#创建虚拟环境
conda create -n your_env_name python=X.X（3.6、3.7等）
 
#激活虚拟环境
source activate your_env_name(虚拟环境名称)
 
#退出虚拟环境
source deactivate your_env_name(虚拟环境名称)
 
#删除虚拟环境
conda remove -n your_env_name(虚拟环境名称) --all
 
#查看安装了哪些包
conda list
 
#安装包
conda install package_name(包名)
conda install scrapy==1.3 # 安装指定版本的包
conda install -n 环境名 包名 # 在conda指定的某个环境中安装包
 
#查看当前存在哪些虚拟环境
conda env list 
#或 
conda info -e
#或
conda info --envs
 
#检查更新当前conda
conda update conda
 
#更新anaconda
conda update anaconda
 
#更新所有库
conda update --all
 
#更新python
conda update python
```









