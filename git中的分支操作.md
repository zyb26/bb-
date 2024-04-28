# 如何将分支与主分支保持同步（都是origin）

# 1. 确保主分支是最新的(拉取仓库中最新的主分支代码)
$ git checkout master
$ git pull origin master

# 2. 切换到分支并拉取最新代码（拉取分支中最新的代码）
$ git checkout your_branch
$ git pull origin your_branch

# 3. 合并主分支到当前分支
$ git checkout your_branch
$ git merge master

# 4. 解决合并冲突
打开包含冲突的文件，并查找冲突标记。
通过手动编辑文件，选择要保留的更改。
保存文件，并使用git add命令将解决冲突后的文件标记为已解决。
最后，使用git commit命令提交解决冲突的更改。

# 5. 推送更新到远程分支
git push origin your_branch

# pycharm 中右下角进行分支签出 先切换到正确的分支进行拉取 再合并 解决冲突 最后 推送