### `Git & Github ` 的关系 
- `Git `
> `Git `是一个工具，它可以使用命令行，你可以通过各种命令往仓库推送、下载、合并、解决冲突各种各样的问题。

- `Github `
> 是一个免费的额一个空间，通过`Github `共享代码。 

### Git 常用命令 
- `git init `新建一个空的仓库 
- `git remote add origin 远程仓库地址 `连接远程仓库 
- `git status `查看状态
- `git add . `添加文件
- `git commit -m '注释' `提交添加的文件并备注说明
- `git push -u origin master `将本地仓库文件推送到远程仓库
- `git log `查看变更日志
- `git reset --hard `版本号前六位 回归到指定版本
- `git branch `查看分支
- `git branch newname `创建一个叫newname的分支
- `git checkout newname `切换到叫newname的分支上
- `git merge newname `把newname分支合并到当前分支上
- `git pull origin master `将master分支上的内容拉到本地上
### 错误
> git push -f 
>> ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/aucode/Personaldocument.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details. 
