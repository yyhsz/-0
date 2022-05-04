# git

## 分支开发

1. 切回 master `git checkout master`
2. 拉取远程 master `git pull origin master`
3. 切回 feature `git checkout master`
4. 在 feature 合并 master `git merge master` 或  `git rebase master`
5. 解决冲突 review 代码...
6. 切回 master `git checkout master`
7. 在 master 合并 feature `git merge feature`
8. 推送远端 `git push origin master`
