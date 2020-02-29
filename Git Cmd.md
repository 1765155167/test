# git
## git 命令
### git init
### git add <file>
### git add .
### git commit -m "create pro"
git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。
### git diff
### git log
### git reset --hard HEAD^ 回退上一个版本
### git reset --hard HEAD~3 回退上三个版本
### git reset --hard 0894 转到0894（通过给git log查看）的版本
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
### git diff HEAD -- readme.txt 查看修改的内容
### git checkout -- readme.txt 回到最近一次commit或者add的状态
### git checkout -- test.txt 误删除的文件恢复
### git reset HEAD <file> 撤销git add的文件
### .gitignore 文件可以让git忽略一些文件
### 配置别名
```java
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
//将"log --color --graph --pretty=format:..." 命令用lg替换
```
## 文件恢复
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
## 关联一个远程仓库
要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
# git分支
1. git checkout -b dev 创建并切换分支
2. git switch -c dev 创建并切换分支
3. git branch 查看所有分支
4. git branch dev 创建dev分支
5. git branch -d dev 删除dev分支
6. git checkout dev 切换到dev分支
7. git switch master 切换到已有分支
8. git merge dev 合并分支到master
9. git log --graph --pretty=oneline --abbrev-commit 查看分支情况
10. git stash 保存现场
11. git stash list 查看保存的现场
12. git stash pop 恢复现场并且删除stash
13. git cherry-pick <commit> 把某个提交复制到当前分支中
14. git branch -D <name> 强行删除一个没有合并的分支
15. git remote -v 查看远程信息
16. git push origin <branch-name> 推送分支
17. git pull 抓取分支
18. git checkout -b <branch-name> origin/<branch-name> 在本地创建和远程分支对应的分支
19. git rebase 将本地为push的分支提交整理成直线

# 多人协作的工作模式
1. 首先，可以试图用git push origin <branch-name>推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
5. 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
6. ，使用，本地和远程分支的名称最好一致；

# 标签
标签用于更加方便的获取代码commit太多
1. git tag v0.9 在最近的commit上打一个标签 
2. git tag v0.9 f52c633 在commit为f52c633的提交时打一个标签v0.9
3. git tag -a v0.1 -m "version 0.1 released" 1094adb 创建一个带说明的标签
4. git tag 查看所有标签
5. git show <tagname> 查看标签信息
6. git tag -d v0.1 删除本地标签
7. git push origin v1.0 推送某个标签到远程
8. git push origin --tags 推送全部尚未推送到远程的标签
9. 删除远程标签 首先git tag -d v0.9删除本地标签 后git push origin :refs/tags/v0.9
标签不是按时间顺序列出，而是按字母排序的
# 参与一个开源项目
1. 在GitHub上，可以任意Fork开源仓库；克隆一份到自己的仓库然后在自己的仓库中进行修改
2. 自己拥有Fork后的仓库的读写权限；
3. 可以推送pull request给官方仓库来贡献代码。
Git有很多图形界面工具，这里我们推荐SourceTree，它是由Atlassian开发的免费Git图形界面工具，可以操作任何Git库。