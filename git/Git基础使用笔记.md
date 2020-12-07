[toc]
# Git

## 廖雪峰教程

### 安装并配置git
`sudo apt-get install git`  
`git config --global user.name "username"`  
`git config --global user.email "email"`  

### 版本库的基础操作

#### 初始化git仓库
`git init`(在合适的目录中运行)  

#### 添加文件到版本库/从版本库中删除文件
`git add <file>...`  
`git rm <file>...`  

#### 提交暂存库中的修改至版本库
`git commit -m <message>`  

#### 查看工作区状态/查看修改内容
`git status`  
`git diff`  
`git diff HEAD -- <file>`  

#### 查看提交历史/查看命令记录
`git log`  
`git log --pretty=oneline`  
`git reflog`  

#### 版本切换
`git reset --hard HEAD^`(回退1版)  
`git reset --hard HEAD~1`(回退1版)  
`git reset --hard d3e6f32`(回退至提交id对应的版本)  

#### 撤销工作区的修改/撤销暂存区的修改
`git restore <file>...`  
`git restore --staged <file>...`  

### 远程仓库

#### 创建ssh-key 将用户主目录下的`.ssh/id_rsa.pub`添加到github中
`ssh-keygen -t rsa -C "email"`  

#### 关联远程库并进行首次推送
`git remote add origin git@github.com/xxx`  
`git push -u origin master`  

#### 克隆远程库
`git clone git@github.com/xxx`  

#### 推送修改至远程仓库
`git push origin master`  

### 分支管理

#### 创建并切换分支
`git switch -c dev` (等价于下面两条命令的组合)  
`git branch dev`  
`git switch dev`  

#### 查看分支
`git branch`  

#### 删除分支
`git branch -d branch-name` (普通分支：未修改或者已经合并完成的分支)  
`git branch -D branch-name` (强行删除：修改后未进行合并的分支)  

#### 合并分支至当前分支
合并分支产生冲突时，手动修改冲突文件，重新添加并提交  
`git merge dev`  
`git merge --no-ff -m "message" dev` (普通合并模式，有合并历史)  
`git log --graph --pretty=oneline --abbrev-commit` (查看分支合并情况)  

### BUG相关

#### 保留当前现场以便切换到其他分支
`git stash` (保留现场)  
`git stash pop` (恢复现场，等价于下面两条语句)  
`git stash apply`  
`git stash drop`  

#### 复制特定提交到当前分支（常用于修复BUG）
`git cherry-pick <commit>`  

### 多人协作相关

#### 查看远程库相关信息
`git remote -v`  

#### 从本地推送分支至远程库
`git push origin dev`  

#### 提交失败时，第一次先建立关联并抓取已有的分支
`git branch --set-upstream dev origin/dev`  
`git pull origin dev`  

#### 整理本地未push的历史记录为直线
`git rebase`  

### 标签管理

#### 创建标签
`git tag v1.0`  
`git tag v0.9 8bfc362`  
`git tag -a v0.1 -m "message" a355bc8`  

#### 查看标签列表与标签信息
`git tag`  
`git show v1.0`  

#### 推送标签到远程
`git push origin v1.0`  
`git push origin --tags`  

#### 删除标签
`git tag -d v0.9`  
`git push origin :refs/tags/v0.9`  

### 多个远程库
`git remote add gitee git@gitee.com:xxx`  
`git remote add github git@github.com:xxx`  

### 忽略特殊文件

#### 添加`.gitignore`文件到库中
```
# 注释

# 所有的.class文件忽略掉
*.class 

# 将该文件排除在忽略名单外，即App.class需要添加到库中
!App.class
```

`git add -f App.class` (强行添加忽略的文件)  
`git check-ignore -v App.class` (检查文件被哪条规则忽略)  

### 配置别名

#### 配置文件在 .git/config 或 ~/.gitconfig 中
`git config --global alias.st status`  
`git st`  