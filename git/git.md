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