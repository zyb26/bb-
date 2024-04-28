# 你想要fork的代码(上游仓库)---------->你fork的代码(远程仓库)---------->你电脑中的代码(本地仓库)
# 你想要fork的代码(上游仓库)<----------你fork的代码(远程仓库)<----------你电脑中的代码(本地仓库)
# 每个仓库主分支是master，还可以有其它分支
# 上游仓库的表示为 upstream，远程仓库表示为origin。


# 1. 首先要确认是否建立了主项目的远程源：
# git remote -v
如果只显示自己的两个源（fetch, push）如下：
origin ....  (fetch)
origin ....  (push)

# 2. 配置远程仓库地址：
在命令行中，进入你fork的仓库的本地目录，并添加一个指向原始仓库（即你fork的仓库来源）的远程仓库地址。通常，原始仓库会被称为"upstream"（上游仓库）。假设原始仓库的URL为https://github.com/original-user/original-repo.git，执行以下命令：

# git remote add upstream https://github.com/original-user/original-repo.git



# 3. 拉取原始仓库的更新：
现在，你需要从上游仓库（原始仓库）拉取最新的更改。

# git fetch upstream


# 4. 合并更新
在将上游仓库的更新拉取到本地后，你可以将这些更新合并到你的本地主分支（通常是master/main分支）。
# git checkout master  # 切换到你的主分支，如果不是master分支，请将其替换为你的主分支名称
# git merge upstream/master  # 将上游仓库的更新合并到你的主分支
或者变基
git checkout master
git rebase upstream/master

# 5. 修改提交
git add -u #-u表示只增加文件修改，不添加新创建的文件
git commit -m "本次提交的描述"

# 6. 推送到自己的仓库
# git push origin master  # 如果不是master分支，请将其替换为你的主分支名称
git remote -v # 查看远程link
git push [自己的仓库url名] [分支名] #例如git push origin master 或者git push [my_repo_url] new_branch


# 7. 推送到官方仓库
 # 如果没有官方的url地址，需要增加上游地址，这里命名为upstream
git remote add upstream git@github.com:facebookresearch/maskrcnn-benchmark.git（官方ssh）
# 合并官方仓库分支和本地自己修改的分支
git fetch origin
git merge origin/master
# 推送到官方仓库master分支
git push upstream master 

# 8. 与上游保持一致
# 获取上游更新
git fetch upstream
git checkout master
# merge
git merge upstream/master

# 推送到自己的仓库
git push origin master






