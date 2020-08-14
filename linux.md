# Linux

## 目录结构

1. Linux中一切皆文件
2. 根目录root ,/，所有的文件都挂载在这个节点下

```shell
# 命令 ls /
root@haiying:~# ls /
bin   home            lib64       opt   sbin      tmp      vmlinuz.old
boot  initrd.img      lost+found  proc  srv       usr
dev   initrd.img.old  media       root  swapfile  var
etc   lib             mnt         run   sys       vmlinuz
```

**对各个目录的解释：**

```shell
/bin:bin是Binary的缩写，这个目录存放着最经常使用的命令。（不要修改）
/boot:存放的是启动Linux时的一些核心文件，包括一些连接文件和镜像文件。（不要修改这个目录）
/dev:dev是device(设备)的缩写，用于存放一些外部连接的设备。在Linux中存放设备和存放文件的方式是相同的。
/mnt:也是用来临时挂载一些外部文件系统，比如光盘驱动等。我们通常将光驱挂载到/mnt上，然后进入该目录就可以查看光驱内容了。(通常还会用来挂载一些本地的文件)。
/etc:这个目录用来存放所有的系统管理所需要的配置文件和子目录。比如nginx的配置文件,redis的配置文件等。(非常重要)
/home:用户的主目录（相当于windows中的administrator）。在Linux中可以创建多个用户，每个用户都有自己的目录，一般该目录名是以用户的账号命名的。（就跟windows中除了有administrator管理员用户，还可以自己创建用户）
/lib:这个目录存放的是系统最基本的动态连接共享库，其作用类似于windows中的DLL文件。（不要修改）
/lost+found:存放突然关机的一些文件。（不重要）
/opt:这是给主机额外安装软件所摆放的目录,类似于windows安装程序默认放置的文件目录。比如安装一个mysql数据库等就放到这个目录。（非常重要）
/root:该目录为系统管理员，也称作超级权限者的用户主目录。
/sbin:sbin是super user(超级管理员)的缩写，这里存放的是系统管理员使用的系统管理程序。
/usr:普通的用户目录，这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于windows下的program files目录。（非常重要）
/tmp:这个目录是用来存放一些临时文件,用完即丢的一些文件可以放在这里。比如一些安装包，解压缩之后就可以删除了。
/var:这个目录存放着不断被扩充的东西，我们习惯将哪些经常被修改的目录存放在这个目录下，包括各种日志文件等。
/www:存放服务器网站相关的资源。比如各种环境，各种网站项目。（非常重要）
```

**创建属于自己的账户：**

```shell
cd /home;
mdkir blog;# 相当于创建了一个blog的账号，以后所有与blog相关的内容都放到这个目录下
root@haiying:/home# ls
blog  haiying
root@haiying:/home# cd blog
root@haiying:/home/blog# ls
app  blog-data  shared  #所有与blog相关的内容都放到这个目录下
```





