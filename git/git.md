#### git install
- [淘宝镜像](https://npm.taobao.org/mirrors/git-for-windows/)
- 安装完成后输入用户名和邮箱
    - git config --global user.name " "
    - git config --global user.email " "   
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
<<<<<<< HEAD
    - 关联成功后首次使用`git push -u origin master`将本地文件添加至远程库2
=======
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
    *git鼓励大量使用分支（branch）*
2. 分支合并冲突
    - 当不同分支对同一个文件做了修改，且指针相同时，会出现冲突
>>>>>>> test
