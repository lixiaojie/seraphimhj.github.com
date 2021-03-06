<meta http-equiv="content-type" content="text/html; charset=UTF-8">
--- 
layout: post 
title: linux常用包管理工具命令
tags: Linux
type: post 
--- 

常用的linux包管理器工具命令, 备忘记录如下：

### APT package handling utility 

安装xxx软件包：apt-get install xxx; 

卸载xxx软件包及其依赖：apt-get remove (--purge) xxx; 

当source_list修改时，更新软件列表：apt-get update; 

升级系统：apt-get upgrade; 

查询xxx软件包信息:apt-cache search xxx; 

查询xxx软件包的完整信息: apt-cache show xxx;

查询xxx软件包的更完整信息及依赖关系: apt-cache showpkg xxx;


### DPKG - package manager for Debian 

- dpkg --info "软件包名" 
  列出软件包解包后的包名称. 
- dpkg -l
  列出当前系统中所有的包.可以和参数less一起使用在分屏查看. (类似于rpm -qa) 
- dpkg -l |grep -i "软件包名"
  查看系统中与"软件包名"相关联的包.
- dpkg -s 
  查询已安装的包的详细信息.
- dpkg -L 
  查询系统中已安装的软件包所安装的位置. (类似于rpm-ql)
- dpkg -S 
  查询系统中某个文件属于哪个软件包. (类似于rpm -qf) 
- dpkg -I
  查询deb包的详细信息,在一个软件包下载到本地之后看看用不用安装(看一下呗). 
- dpkg -i
    手动安装软件包(这个命令并不能解决软件包之前的依赖性问题),
    如果在安装某一个软件包的时候遇到了软件依赖的问题,
    可以用apt-get -f install在解决信赖性这个问题. 
- dpkg -r
  卸载软件包.不是完全的卸载,它的配置文件还存在. 
- dpkg -P
  全部卸载(但是还是不能解决软件包的依赖性的问题)
- dpkg -reconfigure 
  重新配置

