# 文件夹的权限以及文件夹的作用
1. pwd 获取当前文件夹所在的位置

2. 直接cd / 或者    cd .. 进入到根目录

3. 复制文件         cp file2.txt file3.txt

4. 移动/重命名文件:  move file3.txt file4.txt

5. 删除文件：        rm file4.txt       remove

6. 创建目录:         mkdir hello

7. 创建多级目录:      mkdir hello1/hello2

8. 递归复制目录:      cp -r hello1 hello_copy  # 复制到同一个目录下了

9. 查看当前目录所有的文件和目录大小: du 或者 tree

10. 删除目录:        rmdir hello1 文件夹内的是空的才可以    

11. 递归删除:        rm -r hello1 递归删除文件夹内的所有文件夹及文件

12. 目录复制:        cp -r /path1/to/source_directory /path2/to/destination_directory

13. Linux 常用的命令

    命令一般是参数名 和 参数组成的 -参数
    ls -l  获取文件的详细信息
    ls -a  显示包含隐藏文件的所有文件
    ls -h  以人类可读的方式显示文件的大小
    ls -t  可以按照修改时间进行排序
    ls -t -r 可以逆序显示    可以组合显示 也可以 ls -tr
## rm 命令是十分危险的 不可恢复

## 根目录下的文件及作用  ll列出一个目录下的详细文件/目录  home 或者root 是家目录代表我们进入系统的默认目录
使用的主要是/root
/bin：这个目录包含许多用户可执行的基本命令程序（二进制文件），这些命令对于启动、修复系统等操作至关重要
/boot：这个目录存放的是系统启动时所需的核心文件，比如引导加载程序（如 GRUB）所需的各种文件。
/dev：在这个目录中，你会找到设备特殊文件，它们代表系统中的设备和设备接口，例如硬盘(/dev/sda)、终端(/dev/tty)等。
/etc：该目录包含系统的配置文件，以及启动、关闭脚本等。它是管理网络、服务、用户等系统设置的文件存放地。 我们安装的mysql等软件的配置文件一般也在这里
/lib：这个目录包含系统库文件，即动态链接共享库，它们是支持/bin和/sbin下的二进制文件运行的必需库文件。
/home：普通用户:这里是用户的主目录所在的地方，每个用户在系统中都有一个属于自己的目录，通常以用户名命名，并用来存储个人文件和设置。
/root：超级用户:root用户是系统最高权限的用户，拥有对系统进行任何修改的能力;/root目录通常只包含root用户的家目录，其中存储root用户的个人配置文件和其他专属数据

drwxr-xr-x    2 root   root  4096 Apr 15  2020      boot/
drwxr-xr-x    5 root   root   440 Apr 24 11:47      dev/
drwxr-xr-x    1 root   root  4096 Apr 24 12:22      etc/
drwxr-xr-x    2 root   root  4096 Apr 15  2020      home/
lrwxrwxrwx    1 root   root     7 Oct  3  2023      lib -> usr/lib/        		 # 链接 左边lib指的是文件快捷方式 右边指的是文件本身
lrwxrwxrwx    1 root   root     9 Oct  3  2023      lib32 -> usr/lib32/    	 # 创建软链接 ln -s hello.txt link.txt
lrwxrwxrwx    1 root   root     9 Oct  3  2023      lib64 -> usr/lib64/                     源文件       非常小的快捷方式
lrwxrwxrwx    1 root   root    10 Oct  3  2023      libx32 -> usr/libx32/
drwxr-xr-x    2 root   root  4096 Oct  3  2023      media/                		  # 创建硬链接 ln hello.txt link.txt
drwxr-xr-x    2 root   root  4096 Oct  3  2023      mnt/                  		    # ls -i 可以查看节点 两个文件的i节点相同 指向同一个
drwxr-xr-x    1 root   root  4096 Apr 24 11:47      opt/                  		     # 当我们修改一个内容另一个文件也会随着变化
dr-xr-xr-x 2650 root   root     0 Apr 24 11:47      proc/                 		     # echo "hello" > hello.txt
drwxr-xr-x   15 root   root  4096 Apr 24 12:22      root/                 		   # cat link.txt
drwxr-xr-x    1 root   root  4096 Apr 24 11:47      run/                              # 硬链接删除一个文件另一个文件还可以正常访问 rm hello.txt
               拥有者  所属组      文件最近被创建/修改的日期                        # 如果删除软连接的原文件则连接会失效 

​																												软连接可以指向文件/目录 硬链接只能指向文件

## 第1列 d  rwxr-xr-x    
d l c s : 代表 文件类型
rwx  r-x  r-x:  r 代表读     数字表示4
 7    5 p   5    w 代表写              2           在 Linux 中，sudo 是一个命令，用于以管理员权限（root）执行其他命令。
                x 代表执行              1            而 777 是文件或目录的权限设置，表示所有用户都具有读、写和执行权限。
                - 代表没有权限        0            sudo chmod 777 file.txt  你需要是 root 用户或者拥有 sudo 权限的用户。                        
                                                7 = 4 + 2 + 1 = rwx  --> 777 rwxrwxrwx
                权限分配 3个一组: 前面三个代表文件所有者
                                中间三个代表文件所属组用户
                                后面三个代表其他用户

## 如何添加删除权限 chmod
chmod +x hello.txt 对于hello.txt 所有用户增加执行权限
chmod -x hello.txt 减少执行权限

为单独的用户(文件所有者u; 文件所属组用户g; 其他用户o) 来增加权限  user group other
chmod u+x hello.txt

## 创建文件
vim / touch / echo
touch 本来是修改文件的修改时间的 但是 如果没有就会自动创建文件
touch hello.txt
↑ 可以找输入过的命令
echo "hello" > hello.txt 把原本要输入到屏幕的内容重定向到文本中

## windows系统中文件是以盘符开始的 Linux 系统中文件是以根目录开始的
pwd (print work dir) 显示当前所在目录的位置
cd  (change dir) 切换目录
cd / 切换到根目录
cd / 目录的路径 
cd ../.. 切换到上一级目录的上一级
cd - 上一次所在的目录
cd ~ 家目录 root 或者 home
cd bin
ls ls 找到ls的bin文件  ls cat 找到cat的bin文件


# Linux 
内核 : 负责管理系统的硬件；和提供最基本的服务 （设备驱动程序、进程管理、内存管理、文件系统、网络协议栈...）
系统库: 支持程序开发的软件库 （C标准库(libc)、 数学库(libm)、 动态链接库(libdl)、 线程库(libthread)、第三方库...）
Shell: 命令行解释器 是用户使用linux的接口
应用程序: 浏览器 编辑器 各种软件...

# Linux 发行版
archlinux、 manharo、 Red Hat、 CEntOS、 KALI、 Ubuntu、 FreeBSD、 fedora、 debian、alpine
Ubuntu: 适用于个人桌面用户
KALI: 使用于网络安全和渗透测试
alpine: 体积小巧适用于容器化的应用
都是基于linux内核所有的操作和命令都是一样的

# 如何安装和配置Linux系统
虚拟机软件: 
    vmware、virtualBox、Hyper-V(windows 子系统WSL)、
    Mac下安装Multipass、Parallels Desktop、UTM、QEMU
双系统:
容器安装: Docker
云服务器

# Vim操作Linux系统上的一些文件
直接输入vim 可以查看版本信息
默认情况下是命令模式；
输入:进入尾行模式；再输入q命令就是退出 --> :q

vim中存在三种模式:
1. 命令模式下: 
H J K L 来控制光标的移动 ← ↓ ↑ →         ^ 跳转到行首 $ 跳转到行尾(正则表达式也是用的这两个快捷键)
yy 复制光标所在行的内容  ctrl + c
p 粘贴内容到光标的下一行  ctrl v
dd 删除一行的内容        ctrl x
u 撤销
G 跳转到文件的最后一行
gg 跳转到文件的第一行
/Hello 查找就会在光标所在的位置向下查找  n 继续向下找下一个  N与之相反
?hello 光标所在位置向上查找            n 继续向上找上一个  查找的时候和大小写有关的 如果忽略 输入\c 例如 ?hello\C  也可以:尾行模式下输入 set ic 全局忽略大小写

2. 尾行模式: 
: 进入尾行模式 ESC退出尾行模式
模式下输入 set nu 显示行号 set nonumber 关闭行号显示
:40, 50s/Hello/World/g
全局替换: 如果不加g则只替换每行匹配到的第一个
40, 50 代表行号 不指定的话就是只替换光标所在行 : s/Hello/World        :1,$s/hello/world/g  $最后一行
s 代表替换
将Hello 替换为 World

3. 插入模式:
vim hello.txt (如果文件存在就直接打开；不存在就创建一个新的)
命令模式下:---->插入模式 ； i/a/o进入这个模式 ---> 这个模式下就可以写和删除了 ---> 写好按ESC退出到命令模式
保存--> 使用:切换到尾行模式 然后输入wq就可以保存并退出

4. .vimrc 配置文件信息
vim .vimrc 可以把一些常用的命令写入到文件中



