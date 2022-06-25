# apt 和 apt-get 之间有什么区别？

使用ubuntu的朋友一定会接触一个命令就是apt-get 。
使用该工具安装各种应用程序那叫一个爽。
在 Ubuntu 16.04 发行后，apt使用渐渐频繁起来。

那么，apt-get 与 apt 命令之间到底有什么区别呢？

如果它们有类似的命令结构，为什么还需要新的 apt 命令呢？

是否 apt 真的比 apt-get 更好？

普通用户应该使用新的 apt 命令还是坚持旧有习惯继续使用 apt-get 呢？

## 一、 概念

![apt 和 apt-get 之间的区别](E:\学习笔记\Typora\Linux\apt和apt-get的区别.assets\20201231175218555.png)


1. Apt-get
  Advanced Package Tool，又名apt-get，是一款适用于Unix和Linux系统的应用程序管理器。

  最初于1998年发布，用于检索应用程序并将其加载到Debian Linux系统。主要用于自动从互联网的软件仓库中搜索、安装、升级、卸载软件或操作系统。

  Apt-get成名的原因之一在于其出色的解决软件依赖关系的能力。其通常使用.deb-formatted文件，但经过修改后可以使用apt-rpm处理红帽的Package Manager（RPM）文件。

  Apt-get在Linux社区得到广泛使用，成为用来管理桌面、笔记本和网络的重要工具。随着Linux在企业中的普及，Windows和Mac用户了解如何使用apt-get加载应用程序有一定的好处。

  另外，随着单片机设备如Raspberry Pi的热度增加，apt-get在这些平台上是比较便捷的应用加载方式。如果你想要加载的应用需要程序库或另一个应用程序才能正常工作，apt-get会帮你找到并加载所需的程序库或应用代码。

  apt-get当前的稳定版本是1.0.9.2，在2014年10月发布。

  使用apt-get的主流Linux系统包括Debian和Ubuntu变异版本。大多数情况下，从命令行运行该工具。桌面上有几个图形前端可以使用，包括Synaptic Package Manager、Ubuntu Software Center、Aptitude和Kpackage。

  Raspberry Pi和Beaglebone Black nanoLinux版用户可以很容易地使用apt-get加载程序，因为这些系统通常来自Ubuntu或Debian代码。是debian，ubuntu发行版的包管理工具，与红帽中的yum工具非常类似。

  apt-get命令一般需要root权限执行，所以一般跟着sudo命令。

2. Apt
  apt 命令行实用程序于2014年推出第一个稳定版本，用于 Debian 发行版 .deb 软件包安装。它最初在不稳定的Debian版本中使用，然后在Debian 8中成为标准。

  在 Ubuntu 16.04 发行后，apt 开始流行，并以某种方式取代了 apt-get 。

  随着 apt install package 命令的使用频率和普遍性逐步超过 apt-get install package，越来越多的其它 Linux 发行版也开始遵循 Ubuntu 的脚步，开始鼓励用户使用 apt 而不是 apt-get。

  大多数人不了解 apt 和 apt-get 之间的区别，并且经常在使用一个或另一个时感到困惑。

  两者都是开源命令行工具，用于管理软件包，例如安装，更新，升级和删除。

  但是，它们之间仍然存在一些差异。

  让我们看一些替代 apt-get 的 apt 命令，要查看这些命令，可以键入 apt help 或通过在终端中键入 apt man 来访问apt 手册页。它将显示与apt 相关的所有信息。

  ![apt help ](E:\学习笔记\Typora\Linux\apt和apt-get的区别.assets\20210104220630137.png)

## 二、 apt-get和apt之间的区别

apt 和 apt-get 之间的第一个区别是命令本身。
例如，如果要使用 apt-get update 更新系统存储库索引，则可以运行：

`#apt-get update`

![ ](E:\学习笔记\Typora\Linux\apt和apt-get的区别.assets\20210104220455946.png)


使用 apt 则输入命令：

`#apt update`

![ ](E:\学习笔记\Typora\Linux\apt和apt-get的区别.assets\20210104220529622.png)


apt update 命令不仅更新存储库索引，还告知存储库中是否可用软件以及有多少新版本可用。

### 1. 命令对比

| apt-get              | apt              | 功能                             |
| -------------------- | ---------------- | -------------------------------- |
| apt-get              | apt              | 安装软件包                       |
| apt-get remove       | apt remove       | 删除软件包                       |
| apt-get remove       | apt remove       | 更换所有包                       |
| apt-get purge        | apt purge        | 移除软件包及配置文件             |
| apt-get upgrade      | apt upgrade      | 更新所有软件包（自动处理依赖项） |
| apt-get autoremove   | apt autoremove   | 自动删除不需要的包               |
| apt-get dist-upgrade | apt full-upgrade | 在升级软件包时自动处理依赖关系   |
| apt-cache search     | apt search       | 搜索应用程序                     |
| apt-cache show       | apt show         | 显示装细节                       |

+ 删除不必要的依赖apt-get autoremoveapt autoremove删除具有相关配置的软件包apt-get purgeapt purge

+ 在上表中，如果将 apt-get 替换为 apt，则所有命令都相同，除了 apt upgrade 命令。
  旧的 apt-get upgrade 命令更新系统中当前存在的所有软件包，它不会在系统上安装或删除现有软件包。
  新的 apt upgrade 命令将安装作为可升级软件包的依赖项添加的软件包。尽管类似于 apt-get 升级，但它也不会删除以前安装的软件包。

+ apt show 命令以字母顺序打印输出，并隐藏 apt-cache show命令显示的不太重要的信息。

+ apt 和 apt-get 之间的区别不仅限于命令，新的 apt 命令中已添加了另一个视觉功能，以使最终用户满意。每当在使用 apt 升级，apt 完全升级或 apt dist升级时更新软件包时，都会看到一个进度条，通知该过程的进度。

  ![apt install](E:\学习笔记\Typora\Linux\apt和apt-get的区别.assets\20210104221909389.png)

  > 当使用 apt remove 或 apt purge 删除软件包时，它也会出现。

+ 此外，如果我们运行 apt list --upgradeable，它还会显示一些颜色，以提供有关存储库提供最新版本的软件包的清晰概述。

### 2. 两个新命令

除了替换命令外，apt 引入了两个新命令：

| 新的apt命令      | 功能                                 |
| ---------------- | ------------------------------------ |
| apt list         | 列出包含条件的包（已安装，可升级等） |
| apt edit-sources | 编辑源列表                           |

1. apt list
   当 apt list 命令与–installed或–upgradeable一起使用时，它将列出已安装，可安装或需要升级的软件包。
2. apt edit-sources
   使用此命令时，它将在编辑器中打开sources.list文件进行编辑。
   apt-get 仍然不能完全被 apt 取代，而且我认为它永远不会被完全终止。你可能正在考虑应该选择什么：apt 或 apt-get。在我看来，选择apt 是值得的，因为它提供了软件包管理的所有必需功能，并且更快，更友好且易于使用。

## 三、使用apt还是apt-get？

目前还没有任何 Linux 发行版官方放出 apt-get 将被停用的消息，至少它还有比 apt 更多、更细化的操作功能。对于低级操作，仍然需要 apt-get。

既然两个命令都有用，那么我该使用 apt 还是 apt-get 呢？

作为一个常规 Linux 用户，系统极客建议大家尽快适应并开始首先使用 apt。
不仅因为广大 Linux 发行商都在推荐 apt，更主要的还是它提供了 Linux 包管理的必要选项。

最重要的是，apt 命令选项更少更易记，因此也更易用，所以没理由继续坚持 apt-get。

最后给大家提供两点使用上的建议：

+ apt 可以看作 apt-get 和 apt-cache 命令的子集, 可以为包管理提供必要的命令选项。
+ apt-get 虽然没被弃用，但作为普通用户，还是应该首先使用 apt。
  