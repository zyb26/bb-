# shell 是命令行解释器；负责接收用户的命令-->调用操作系统的内核来执行这些命令
# shell 有很多种类 sh bash csh ksh zsh
linux 系统中默认安装的都是bash
git 中的git bash here 也是用的bash

3. 根目录下
cat /etc/shells 查看根目录下的shells这个文件 (记录了系统中所有的shell版本)

--------------------------------------------------------------------------------------------------------
## 如何查看系统用的哪个shell为默认
3. echo $HOME 用来存储当前系统的家目录
/root
4. echo $PATH 用来存储当前系统的查找路径  <-- 系统会在这些路径中查找各种命令的执行文件
/usr/bin:/ 很多
5. echo $SHELL
/bin/bash   当前系统中默认使用的的shell命令的(系统的环境变量)             /bin 所有的二进制执行文件目录
6. echo $0  查看当前正在执行的脚本的名称                echo 就是bash里面的一个脚本
-bash
7. $0 和$SHELL区别
$SHELL 系统的环境变量
$0     当前正在执行的脚本名称
8. 切换
/bin/sh 
$SHELL 系统的环境变量没变
$0     当前正在执行的脚本名称变为sh
这就是在不同版本的shell切换的方法  exit 退出

----------------------------------------------------------------------------------------------------------------
## 如何编写一个最简单的shell脚本
vim hello.sh
第一行: #!/bin/bash  路径  #！/bin/zsh
echo "Hello Shell" 输出
date    显示当前时间
whoami  显示当前用户

## 执行:想要执行一个脚本文件 必须要增加权限
chmod a+x hello.sh     为所有用户添加执行权限；虽然root用户有最高权限；但是一些文件并没有可执行的权限
./hello.sh

----------------------------------------------------------------------------------------------------------
## shell 脚本示例

#!/bin/bash

is_prime() {
    num=$1
    if [ $num -lt 2 ]; then
        echo "false"
        return
    fi

    for ((i=2; i*i<=num; i++)); do
        if [ $((num % i)) -eq 0 ]; then
            echo "false"
            return
        fi
    done

    echo "true"
}

read -p "请输入一个整数： " num
result=$(is_prime $num)
if [ "$result" == "true" ]; then
    echo "$num 是素数"
else
    echo "$num 不是素数"
fi

------------------------------------------------------------------------------------------------------------------
# 编写一个简单的shell

#!/bin/bash  默认使用bash

echo "请输入您的名字:"
read name    # 读取用户的输入并保存为name变量
echo "您好， $name"

## 执行
bash game.sh
./game.sh  这种直接执行的方式需要给脚本文件加一个执行权限 chmod +x game.sh (可以 ls -l game.sh 来查看权限)
------------------------------------------------------------------------------------------------------------------
# 如何让.sh文件接收参数  $就是接收变量
echo "请输入您的名字:"
name=$1
channel=$2
echo "您好，$name，欢迎来到$channel!"

## 执行
./game.sh 1 2
您好， 1， 欢迎来到2！
------------------------------------------------------------------------------------------------------------------
也可以直接把 name channel 放到环境变量值
终端直接输入 name=1 channel=2  只是普通的变量并不是环境变量
修改脚本文件
echo "请输入您的名字"
echo "您好，$name, 欢迎来到$channel"

终端直接输入 echo $name echo $channel
尝试直接在脚本文件中使用
./game.sh
终端执行 export name=1 channel=2 变为环境变量了
./game.sh
就正常输出了
另一个问题就是 export 的环境变量只在当前有效；退出后就会失效
如何永久有效: Shell 会在启动的时候读取一些文件；家目录下的 .bashrc 和.profile 文件
.profile 是用户登录的时候执行且只执行一次 就第一个终端有变量
.bashrc  是每打开一个终端都执行
.profile 内部会调用 .bashrc
除了家/root目录  上一级的根目录下 /etc/bash 中的bash.bashrc存储的环境变量也是对所有用户都有效的
在家目录下的 .bashrc 最后面加入两行 export name=1 export channel=2
-----------------------------------------------------------------------------------------------
别名: 在.bashrc中 可以定义一些别名: alias ll='ls-alF'
---------------------------------------------------------------------------------------------------
linux中: shuf -i 1-10 -n 1             生成的范围、生成的个数
简单脚本:
#!/bin/bash
number = shuf -i 1-10 -n 1   当我们使用命令生成 来给变量赋值的时候要写成 `shuf -i 1-10 -n 1` shell 才会把这个命令的输出结果当成整体来处理
$()也可以
echo $number
echo "请输入一个随机数字"
read guess
if [[$guess eq $number]]; then
        echo "猜对了"
else 
        echo "猜错了"
fi
-----------------------------------------------------------------------------------------------
循环
#!/bin/bash
number = `shuf -i 1-10 -n 1`
while [[$guess -ne $number]]
do # 表示循环的开始
read guess
if [[$guess -eq $number]]; then
        echo "猜对了! 是否继续? (y/n) :"
        read choice
        if [[$choice = "y"]] || [[$choice = "Y"]]; then
                continue
        else:
                break
elif [[$guess -lt $number]]; then
        echo "猜小了"
else
        echo "大了"
fi
done
---------------------------------------------------------------------------------------------------