# Git 

---

# 创建版本管理库
1. git全局配置,可随意设置
``` bash
git config --global user.name "lagoria"
git config --global user.email "g3325035137@gmail.com"
```

2. 在当前目录创建.git文件夹,变成git可以管理的仓库  
` git init `

---

# 本地仓库管理
1. 暂存区操作  
将文件添加到暂存区  
` git add filename `  
将修改的文件添加到暂存区  
` git add -u `  
查看暂存区文件  
` git ls-files `  
删除暂存区文件  
` git rm --cached filename `

2. 将暂存区的文件提交到仓库  
` git commit -m '注释' `

3. 查看状态  
` git status `

4. 查看文件修改内容  
` git diff filname `

5. 查看日志  
` git log `

6. 版本回退  
` git reset --hard HEAD^ `

or  
` git reset --hard HEAD~1 `

7. 查看版本号日志  
` git reflog `

8. 撤销工作区文件的修改  
恢复到提交暂存区之前  
` git checkout --filename `  
恢复到上次提交暂存区之前  
```s
git reset HEAD
git checkout --filename
```
恢复到提交仓库区之前  
```
git reset HEAD^
git checkout --filename
```
# 子模块
1. 添加子模块
```bash
git submodule add <url> <path>
```
2. 子模块更新
```bash
git submodule update --init --recursive
```
3. 移除子模块
```bash
git submodule deinit -f <path-to-submodule>
git rm <path-to-submodule>
rm -rf .git/modules/<path-to-submodule>
```

---

# 远程仓库 (github)
1. github注册账户,创建目标仓库.

2. 创建SSH密钥  
	` ssh-keygen -t rsa -C “g3325035137@gmail.com” `

3. 将~/.ssh目录下的id_rsa.pub公钥添加到github中

4. 添加远程仓库  
	` git remote add github git@github.com:username/repository.git `
	
	删除远程仓库  
	`git remote rm origin`
	
	查看远程仓库  
	`git remote show origin`

5. 本地分支推送  
	` git push github master `  

	强制推送(覆盖远程仓库)  
	` git push -f github master `

6. 克隆远程仓库  
	`git clone [git地址]`  
	`git clone --branch [tag标签] [git地址]`  
	`git clone -b [tag标签] --depth=1 [git地址]`  
	
---

# 创建.gitignore文件
为了忽略无关目录或文件  
`vim .gitignore`  
example:  
```
# VS Code Settings
.vscode/
# build files
build/
```

---

# 标签操作

1. 轻量标签

轻量标签（lightweight tag）仅仅是一个指向特定提交的引用，它不会存储任何额外的信息。创建轻量标签的命令如下：
```text
git tag {标签名} {提交ID}
```

例如，创建一个指向最新提交的轻量标签：
```text
git tag v1.0.0
```

2. 附注标签

附注标签（annotated tag）是存储在Git数据库中的一个完整对象，它有一个标签名，标签信息，标签签名等信息。创建附注标签的命令如下：
```text
git tag -a {标签名} -m "{标签信息}" {提交ID}
```

例如，创建一个指向最新提交的附注标签：
```text
git tag -a v1.0.0 -m "Release version 1.0.0" HEAD
```

3. 查看标签

查看当前项目中的所有标签，可以使用以下命令：
```text
git tag
```

如果想查看某个具体标签的信息，可以使用以下命令：
```text
git show {标签名}
```

4. 推送标签

默认情况下，`git push`命令不会将标签推送到远程服务器，需要使用以下命令将标签推送到远程服务器：
```text
git push origin {标签名}
```

如果要一次性推送所有本地标签，可以使用以下命令：
```text
git push origin --tags
```

5. 删除标签

删除本地标签的命令如下：
```text
git tag -d {标签名}
```
删除远程标签的命令如下：
```text
git push origin :refs/tags/{标签名}
```

6. git打tag操作步骤

在Git中打一个tag的操作步骤如下：

1. 查看最新的提交ID，可以使用以下命令：\
    `git log -1 --pretty=format:"%H"`
2. 执行以下命令，创建一个轻量标签：\
    `git tag {标签名} {最新的提交ID}`\
    或者执行以下命令，创建一个附注标签：\
    `git tag -a {标签名} -m "{标签信息}" {最新的提交ID}`\
    其中，{标签名}是标签的名称，{标签信息}是标签的描述，{最新的提交ID}是最新的提交的ID。
3. 将标签推送到远程服务器，可以使用以下命令：\
    `git push origin {标签名}`\
    如果要一次性推送所有本地标签，可以使用以下命令：\
    `git push origin --tags`\
    其中，{标签名}是标签的名称。

**注意：** 创建标签时，如果不指定提交ID，**默认会使用当前所在分支的最新提交作为标签指向的提交**。

---

# 分支操作
1. **列出所有分支**：

使用 `git branch -a` 命令列出所有本地和远程分支。
```bash
git branch -a
```
2. 创建并切换分支  
	` git checkout -b name `
	
	equal to  
	` git branch name `  
	` git checkout name `

3. 删除分支  
	` git branch -d name `  

	删除临时分支  
	` git branch -D temp `

4. 拉取分支  

	拉取到临时分支  
	` git fetch github master:temp `  

	拉取到本地分支
	`git fetch origin `
	`git fetch github master `

5. 合并分支  

	合并临时分支  
	`git merge temp`  

	合并到本地分支
	`git merge origin`
	`git merge github/master`

6. **删除所有本地分支**：

使用 `git branch -D` 命令并跟随一个通配符 `*` 来删除所有本地分支。请注意，这将会删除所有本地分支，包括那些尚未合并到当前分支的分支，所以请确保这是你想要的操作。
```bash
git branch -D $(git branch | grep -v "master")
```

在这个命令中，我使用了 `grep -v "master"` 来排除名为 "master" 的分支，以防你仍需要保留它。如果你想要删除所有分支，包括 "master"，只需移除 `grep -v "master"` 部分。

7. **删除所有远程分支**：

首先，你需要获取远程仓库的所有引用，并使用 `git push` 命令删除它们。这通常涉及到与远程仓库的交互，所以请确保你有足够的权限来执行此操作。
```bash
git for-each-ref --format='%(refname:short)' refs/remotes/origin | xargs -n1 git push origin --delete
```

这个命令会列出所有的远程分支，并逐个删除它们。
