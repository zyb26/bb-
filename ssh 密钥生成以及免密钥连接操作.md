# git ssh秘钥生成：https://blog.csdn.net/baidu_38645830/article/details/115357758

把~/.ssh中的 id_rsa.pub公钥复制到github / gitlib 对应的 密钥位置
一台电脑连接一个
就可以直接好了


# 把本机的公钥粘贴到服务器的authorized_keys文件中
# Vscode免密连接

## Local（Windows/Linux）

* Windows系统生成的公/私钥文件位于：`C:\Users\[用户名]\.ssh\`​
* Linux系统生成的公/私钥文件位于：`~/.ssh/`​

## Remote（Linux）

---

1. 进入~/.ssh/路径。

```bash
cd ~/.ssh
```

2. 创建authorized_keys文件。若文件已存在，则跳过此步。

```bash
touch authorized_keys
```

3. 将local端刚生成的公钥（.pub）内容copy至刚创建authorized_keys中。
4. 重启ssh服务：直接新开一个命令行/ssh窗口，或在当前窗口执行`systemctl restart sshd`​

## Remote（GitHub/GitLab）

---

在`Setting -> SSH Keys`​里添加local端刚生成的.pub文件即可。

```shell
Host 192.15.16.17 # 主机名，可以认为给服务器定义了一个别名，便于你区分和查看，我这里直接使用的ip
    HostName 192.15.16.17 # 服务器ip地址
    User jackeylove # 用户名
    IdentityFile ~/.ssh/id_rsa # 你的私钥文件路径
```

可以把服务器的公钥粘贴到github中 ssh来clone代码
‍# GitHub 可以通过左下角 的developer settings  --> Personal access tokens --> Tokens(生成一个密码) http方式clone 账户名 + 密码