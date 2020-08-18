# Linux

## 目录结构

1. Linux 中一切皆文件
2. 根目录 root ,/，所有的文件都挂载在这个节点下

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

## 常用的目录基本命令

#### 目录管理

**ls：查看目录**

```shell
# ls 查看目录
-a(all):查看全部文件，包括隐藏文件。
-l:列出所有文件，包含文件的属性和权限，但是不包括隐藏文件。
-al:所有的linux参数可以同时使用。查看包括隐藏文件的所有文件。包括属性和权限
```

**cd：切换目录**

```shell
# cd + 目录名（绝对路径都是以/开头，相对路径.或者..开头）
```

**pwd：显示当前用户所在的目录**

```shell
# pwd  显示当前用户所在的目录
root@haiying:/home/blog# pwd
/home/blog
```

**mkdir：创建一个目录**

```shell
# mkdir 创建目录
-p：递归创建多级目录
root@haiying:/home# mkdir -p test/test2/test3   #创建多级目录
root@haiying:/home# ls
blog  haiying  test
root@haiying:/home# cd test
root@haiying:/home/test# ls
test2
```

**rmdir：删除目录**

```shell
# rmdir + 目录名   只能删除没有子目录的目录
-p +多级目录名    # 递归删除多级目录
root@haiying:/home# rmdir -p test/test2/test3
```

**cp：复制文件或者目录**

```shell
# cp 原来的地方  新的地方
# 拷贝文件
root@haiying:/home/test# cp hello.md /home/test2  拷贝hello.md到test目录
# 拷贝目录 cp -r A/* B 拷贝A文件夹下的所有非隐藏文件到B文件夹
root@haiying:/home# cp -r /home/test/* /home/test2
root@haiying:/home# ls
blog  haiying  test  test2
```

**rm：移除目录或者文件**

```shell
rmdir:只能移除目录
rm:移除文件或者目录
# 参数：
-f(force):强制删除。忽视警告
-r(reverse):递归删除。
-rf:强制删除所有文件。非常危险。（rm -rf /会删除根目录下的所有文件，也就是常见的删库跑路）
-i:互动，删除时进行询问。
```

**mv：移动文件或者目录**

```shell
# mv 原来的目录  新的目录
-f：强制移动
-u:只替换已经更新过的文件
# 重命名
mv test test2 # 将当前目录下的test重命名为test2
```

#### 文件属性

##### 文件属性

Linux 系统是一种典型的多用户系统，不同的用户处于不同的地位，拥有不同的权限。为了保护系统的安全性，Linux 系统
对不同的的用户访问同一文件（包括目录文件）的权限做了不同的规定。
在 Linux 中我们可以使用`ll`或者`ls -l`来显示一个文件的属性以及文件所属的用户和组，如：

```shell
root@haiying:/# ll
total 970068
drwxr-xr-x   2 root root      4096 Jun 18 09:58 bin/
drwxr-xr-x   3 root root      4096 Jun 18 10:04 boot/
drwxr-xr-x  18 root root      3740 Aug  9 18:02 dev/
lrwxrwxrwx   1 root root        34 Jun 18 09:58 initrd.img -> boot/initrd.img-4.15.0-106-generic
...
```

每个文件的属性由一下几个部分来确定（如下图）
![](https://imgkr2.cn-bj.ufileos.com/9be23ba0-1432-4892-a187-79658cfca4fb.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=jE9KqJv9oX34qmGF4%252Bj31dp34wk%253D&Expires=1597820802)

每个文件的属性由左边第一部分的**10**个字符来确定：

**文件类型**

其中第一个字符用来描述文件类型：

实例中，/bin 的第一个属性用 d 表示。d 在 Linux 中代表该文件是一个目录文件。
在 Linux 中第一个字符代表这个文件是目录，文件或者链接文件等等。

```shell
# 参数解释
[d]:目录
[-]:普通文件
[l]:链接文档(link file)，类似于windows中的快捷方式
```

接下来的字符中，以 3 个为一组，且均为【rwx】的三个参数组合，顺序也是 rwx。其中，

[r]：代表可读(read)

[w]：代表可写(write)

[x]：代表可执行(execute)

[-]：表示没有该权限

其中第一组（1-3 位）确定**属主**（该文件的所有者）拥有该文件的权限。

第二组（4-6 位）确定**属组**（所有者的同组用户）拥有该文件的权限。

第三组（7-9 位）确定**其他用户**拥有该文件的权限。

##### 修改属性

**chgrp：修改文件属组**（很少使用）

```shell
# chgrp(change group) [-R] 属组名 文件名
```

**chown：更改文件属主，也可以同时更改文件属组**

```shell
# chown [–R] 属主名 文件名
# chown [-R] 属主名：属组名 文件名
```

**chmod：更改9个文件属性（非常重要）**

```shell
# chmod [-R] xyz 文件或者目录名
```

Linux文件属性有两种设置方式，一种是数字，一种是符号。

```shell
# r:4  w:2  x:1  -:0    
# 可读可写可执行      rwx = 4+2+1=7  最大的权限就是777  chmod  777 + filename
# 可读可写不可执行    rw- = 4+2+0 = 6

```

每种身份(owner/group/others)各自的权限是累加的，例如当权限为：[-rwxrwx---]则代表：

owner=rwx=4+2+1=7

group=rwx=4+2+1=7

others=---=0+0+0=0

因此，该文件的权限数字就是770。

![chmod](https://imgkr2.cn-bj.ufileos.com/76b24313-5315-4f3e-b991-bedf962ae0b6.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=65A1u2lqkl3iPNpmLgVdYyqfDSM%253D&Expires=1597823175)

