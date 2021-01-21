#### git install
- [淘宝镜像](https://npm.taobao.org/mirrors/git-for-windows/)
- 安装完成后输入用户名和邮箱
    - git config --global user.name " "
    - git config --global user.email " " 
#### git update
- command `git update-for-windows`  
#### create repository
- 进入空的文件目录 `git init`命令 出现.git文件说明已创建好版本库（仓库）
- .git 文件一般都是隐藏的，可通过`ls -ah`命令来查看
#### 提交文件
- `git add filename`命令可以将文件添加值仓库（repository），没有返回消息
- `git commit -m "说明文字"`命令可以将添加到仓库的文件提交至仓库，有返回消息
-  `git status`命令可以实时查看仓库文件的修改情况
- `git diff`命令可以查看修改后和修改前文件的变化情况（文件改动后未提交前可用）
#### 文件版本回退
- `git log`命令显示从最近到最远的提交日志
    - 如果嫌日志信息过多，可以添加参数`git log --pretty=oneline`
- `git reset --hard HEAD^`命令可以将文件回退至上个版本
    - HEAD表示当前版本，后跟^表示上个版本，如果回退版本较多，可使用HEAD^~100
    ##### 回退之后如何返回
    - 如果命令行窗口暂时未关闭，可以找到想返回版本的commit id   
    通过命令`git reset --hard commit id`,id只需要前几位就可以了
    - 如果隔天想返回版本，可以通过`git reflog`查看使用的历史命令来查找commit id
#### 工作区和缓存区
1. 工作区（working directory）
    - 自己项目所创建的文件目录即为工作区
2. 缓存区 || 暂存区
    - .git版本库中有stage的暂存区，会为项目自动创建第一个分支`master`，以及指向第一个分支的指针`HEAD`
3. `git add`是将工作区文件的改动提交至暂存区（stage），`git commit`将暂存区的文件提交至版本库
4. 每次文件改动如果不用`git add`提交至暂存区，就不会被`git commti`提交至版本库
#### 撤销修改
- `git checkout -- filename`|| `git restore filename`撤销工作区未提交文件的修改
- `git restore --stage filename`撤销已经提交至暂存区的文件修改，回到add之前的状态
#### 删除文件
- `git rm`命令用于删除文件,-f参数可强制删除文件
- 被删除的文件如果已经提交至版本库，则删除后可以从版本库进行还原
#### 远程仓库
1. 注册github账号
2. 本地电脑创建.ssh文件夹
```js
    ssh-keygen -t rsa -C "email.com"
```
3. 将.ssh文件夹下的公私文件（id_rsa.pub）内容添加至github账号setting-->ssh and GpG keys
4. 连接github远程仓库
    - 新建github仓库 create repository
    - 首次连接远程仓库时需要进行ssh指纹信息验证
        - 本地gitbush输入命令`ssh -T git@github.com`，输入yes
    - 关联远程仓库`git remote add origin git@server-path/repository-name.git`
    - 关联成功后首次使用`git push -u origin master`将本地文件添加至远程库
    - 关联成功后首次使用`git push -u origin master`将本地文件添加至远程库
    - [push相关问题解决](https://blog.csdn.net/huashao888/article/details/105564282)
5. 从远程仓库clone项目
    - `git clone url`命令可以从github远程仓库clone项目
    - git支持多种协议，`https` `ssh` 
    - `https`协议推送时需要每次输入口令，且速度较ssh慢
    - `ssh`协议不需要每次输入口令，且速度最快
#### 分支管理
1. 创建合并分支
    - `git branch <name> || git checkout -b <name>`都可以创建一个分支
    - `git checkout -b <name>`表示创建一个分支，并切换到新创建的分支上**废弃**
    - `git switch -c <branchName>`用于创建并切换到一个不存在的分支
    - `git branch`命令可以列出所有分支，并在当前分支前面添加*号
    - `git checkout <branchName> || git switch <branchName>(new)`用于切换分支，后者是新增方法
    - `git merge <branchName>`用于合并分支，合并到当前分支`branchName`为被合并分支
    - `git branch -d <branchName>`用于删除分支，分支被合并后可直接删除无用分支
    - `git branch -D <branchName>`用于强行删除未合并的分支
    *git鼓励大量使用分支（branch）*
2. 分支合并冲突
    - 当不同分支对同一个文件做了修改，且指针相同时，会出现冲突
    - 需要手动修改文件后再提提交后可修复冲突
    - `git log --graph --pretty=oneline --abbrev-commit`用于查看分支合并情况
3. 分支管理原则
    - `git merge --on-off -m "close fasr forward mode"`
    - 分支合并时，一般情况下git会使用fast forward模式，删除分支后丢失分支信息
    - `--on-off`参数可强制关闭fast forward模式，merge时创建新的commit，保留分支信息
    - 由于合并后会创建新的commit，所以应加上`-m "description"`参数
    - 分支策略
        - `master`分支应该是非常稳定的，只用于发布新版本，不能在上面干活
        - 干活一般在dev分支上面，完成后合并至master分支
4. BUG修复
    - 修复BUG时，新开分支，修复完成后将新开分支合并至主分支。
    - 如果当前有未完成工作，可以先“储藏”当前分支工作区内容`git stash`
    - `git stash list`用于查看储藏的工作内容列表
    - `git stash apply || git stash pop`用于恢复储藏区的内容
    - `git stash apply`恢复内容，但是不删除git stash的内容，需使用`git stash drop`来删除
    - `git stash pop`恢复内容并删除储藏区内容
#### OTHERS
- `git remote -v`用于查看远程库信息
- `git push origin <branchName>`用于推送分支修改，推送失败，使用`git pull`抓取远程有冲突的新提交
- `git checkout -b <branchName> origin/<branchName>`用于在本地创建和远程仓库对应的分支，`branchName`最好一致
- `git branch --upstream <branchName> origin/<branchName>`建立本地分支和远程分支的关联
