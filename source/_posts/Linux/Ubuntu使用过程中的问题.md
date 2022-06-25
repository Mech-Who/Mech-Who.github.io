# Ubuntu使用过程中的问题

1. 安装软件的过程中遇到了Package has no installation candidate的问题:

   > #### apt-get install <packagename>
   >
   > Package gdm is not available, but is referred to by another package.
   > This may mean that the package is missing, has been obsoleted, or
   > is only available from another source
   >
   > ##### E: Package <packagename> has no installation candidate

   搜到的解决方法是:

   ```cmd
   apt-get update
   apt-get upgrade
   apt-get install <packagename>
   ```

   下面还有添加第三方地址:

   ```cmd
   sudo add-apt-repository "deb http://archive.canonical.com/ lucid partner"
   sudo apt-get update
   ```

2. 如何查找安装的软件的目录

   1. `dkpg -l <packagename>`
      1. 查看软件信息,但是查看不了安装目录
   2. `dkpg -L <packagename>`
      1. 查看软件目录,可以查看安装目录
   3. `aptitude show <packagename>`
      1. 也是查看软件信息,比dkpg信息要全,不过aptitude需要先安装才能使用
   4. `which <shellOrder>`
      1. 在环境变量Path中查找shell命令的位置,也不好说他好不好用orz