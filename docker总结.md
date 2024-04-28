# nvidia-smi
# hostnamectl 显示主机名以及相关的操作系统信息，包括型号
sudo apt install dmidecode
sudo dmidecode -t system
# ubturn 22.04 上面安装docker （官网）
-------------------------------------------------------------------
安装后的操作流程
# 1. 查看服务器上是否存在docker; 查看docker的版本
sudo docker -v
# 2. 查看docker是否启动
sudo service docker start
# 3. 检查Docker服务状态
sudo service docker status
# 4. 查看镜像
docker images
docker images <image_name> （例如：docker images ubuntu） <--指定镜像
# 5. 查看容器
docker ps
docker ps -a
# 6. 拉取Docker Hub上面的镜像
docker pull <image_name>:<tag> 
<image_name> 是要拉取的镜像的名称 <tag> 是镜像的标签，表示其版本或特定的变体;不指定是最新的
eg: docker pull ubuntu  / docker pull ubuntu:20.04

# 7. 启动镜像 --> 变为容器并直接进入容器
docker run -it --name my_container --gpus all -v d:/dockerv :/localfiles -p 22:22 -p 80:8080 ubuntu:20.04

-it : interact 交互式 termial 终端   --------------- 固定写法
-v d:/dockerv :/localfiles: 将本地的d:/dockerv 文件夹包到docker中的:/localfiles 文件夹
-p 22:22: 把容器中的ssh端口映射到服务器/本地 来进行连接
-p 80:8080: 把容器的端口映射到服务器/本地 从而可以https调用容器内部
--name: 容器的名字(我们自己随意命名的)
--gpus all:所有的gpu都可用 
...可以用本地的摄像头等很多的资源的
ubuntu:20.04 --- 指定镜像

# 8. 如何停止容器
docker stop <container_id>
docker stop 容器的名称也可以
# 9. 删除容器/镜像
docker rm 容器名称
docker rmi 镜像名称
docker rm `docker ps -a -q` (`docker ps -a -q` 是linux命令执行后的结果) 删除所有容器
# 10. 如何启动一个已经停止的容器(直接docker run 一个镜像是重新又创建了一个容器, 这样还是原来的容器)
docker start <container_id>
docker start 容器的名称也可以
# 11. 重启一个容器
docker restart <container_id>
# 12. 交互式进入容器
docker exec -it <container_id> /bin/bash

-------------------------------------------------------
进入容器后的操作
# 12. 进入到容器后可以 查看ubturn 的版本
cat /etc/issue
# 13. 进行换源 (可以不进行操作)
apt update
apt install vim -y
vim /etc/apt/sources.list
将文件的内容替换为以下的内容:
...................

--------------------------------------------------------
在容器内部安装ssh 就可以直接ssh来远程连接容器了（前面的端口和服务器已经进行交互了为了可以直接映射出来这个ssh的端口， 不然在服务器内部是连接不到这个ssh的）
# 如果不安装ssh直接在容器内操作也是可以的(可以vscode连接容器)
# 14.  容器内安装ssh软件
apt install openssh-server -y (选6 ; 70上海)
# 15. 改一下这个软件的config
 vim /etc/ssh/sshd_config
找到 # PermitRootLogin prohibit-password 在下面添加一行 (/是vim中的搜索; 搜索到了就解除注释#)
解开root登录: PermitRootLogin yes
解开密码登录: PasswordAuthentication yes
# 16. 保存出来 重启ssh
service ssh restart
service ssh start 启动
# 17. 设置root密码
passwd
之后就可以直接ssh连接登录容器了 （名称随便给； 协议ssh; 主机:服务器的/localhost本地的 端口号:22）

###################################
所有的docker命令都是从服务器的终端/ powershell来敲的    (在容器外部来查看; 内部就是一个linux系统)
容器外: docker ps 就是镜像  -a 就是all 所有的
容器内: ps 就是容器内linux进程

# 容器同时运行时；端口不能冲突

# 最后容器外的操作
# 18. 将我们自己的容器保存为镜像
docker commit -a "服务器/本地用户名" -m "注释信息"    容器的id  我们的镜像名字（写啥都行）:版本
# 19. 跑这个镜像和上面一样
# 20. 把我们的镜像保存成为压缩包(会保存到输入命令的文件夹下)
docker save -o 随便起一个压缩包的名称.tar 我们镜像的id
# 21. 这个压缩包就可以发给别人使用
在这个压缩文件的所在文件夹下； 安装有docker的情况下; 容器外的文件直接加载到容器内部
docker load -i 随便起的那个压缩包的名称.tar 就会变为一个docker软件的镜像了
