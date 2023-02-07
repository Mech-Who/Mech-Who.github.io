# HEXO-BLOG

## 一、目的

1. 尝试搭建Hexo博客,完成之前没能完成的事情,之前遇到了困难,本地可以运行,但是github上总是build失败,所以这次想完成它
2. 尝试将自己的笔记逐步搬运到这上面,节省我自己的电脑硬盘空间,同时复习过去所学的各种知识
3. 练习网页搭建相关的各种技能
4. 建立属于自己的知识库,与飞书知识库可能会同步

## 二、所需环境

1. NodeJs

## 三、过程记录

### 1.本地运行

1. npm install -g hexo-cli # 安装hexo脚手架,建立基本工具
2. hexo -v # 检查hexo版本
3. hexo init Mech-Who.github.io # 建立并初始化博客文件夹,init后面的就是文件夹的名字,可以自己命名
4. cd Mech-Who.github.io # 进入博客目录进行网站的环境配置
5. npm install # npm工具安装相关的依赖
6. hexo generate # 可以简写为hexo g,作用是生成相关的静态文件
7. hexo server # 本地启动hexo服务器,然后可以在浏览器输入localhost:4000访问博客

### 2.Github建站访问

1. 将本地运行好的博客相关的内容全都上传的github仓库,仓库名要求是:
	<用户名>.github.io
2. 本地安装hexo-deployer-git工具:
	npm install hexo-deployer-git --save
3. 修改hexo的配置文件_config.yml,在博客目录下,文件最后的Deployment部分修改为以下内容:
	```yaml
	# Deployment
	## Docs: https://hexo.io/docs/one-command-deployment
	deploy:
  		type: git
  		repo: https://github.com/Mech-Who/Mech-Who.github.io.git
  		branch: main
	```
4. 使用以下命令将站点推送到github
	hexo deploy # hexo博客部署,可以简写为hexo d

## 四、仓库分支

1. main - 部署分支
2. write - 博客编辑分支(本地使用)

## 五、问题记录

## 六、参考

1. 搭建参考博客: https://blog.csdn.net/weixin_45019350/article/details/121901433
2. 问题解答参考博科: https://blog.csdn.net/weixin_58068682/article/details/116609960
3. Hexo文档: https://hexo.io/zh-cn/docs/