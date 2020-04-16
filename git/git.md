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