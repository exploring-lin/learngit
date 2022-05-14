**安装Git**

​	**文章背景：**



[TOC]

##### 1  配置文件

​	Git安装完成后，还需要最后一步设置，在命令行输入：

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

​	（1）~/.gitconfig 文件：用户目录下的配置文件只适用于该用户。若使用 git config 时用 --global 选项，读写的就是这个文件。

```bash
$ git config user.name
$ git config user.email
```

​	（2）如果想检查一下看看有没有设置成功，可以再输入git config user.name然后回车，如果设置成功了就会显示你刚刚设置的用户名；同理，可以用git config user.email来查看你设置的邮箱。

##### 2  管理文件

###### 2.1  把一个文件放到Git仓库

```bash
$ git add Git_learning.md
$ git commit -m "wroto a learning file"
```

（1）简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

（2）用`ls`或者`dir`命令查看当前目录的文件。

###### 2.2  掌握工作区的状态

（1）要随时掌握工作区的状态，使用`git status`命令。

（2）如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

```bash
$ git diff
$ git diff HEAD
$ git diff --cached
```

​	1）比较工作区和暂存区的修改；

​	2）比较工作区和上一次commit后的修改；

​    3）比较暂存区和上一次commit后的修改。

###### 2.3  撤销修改

​	（1）use "git restore <file>..." to discard changes in working directory.

​		把文件在工作区的修改全部撤销，这里有两种情况：

​		1）一种是文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

​		2）一种是文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

​		总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

​	（2）use "git restore --staged <file>..." to unstage.

###### 2.4  删除文件

```bash
$ git rm test.txt
```

​	（1）命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。

​	（2）`git rm test.txt` 相当于是删除工作目录中的test.txt文件，并把此次删除操作提交到了暂存区。

##### 3  版本回退

```bash
$ git log
$ git log --pretty=oneline
```

​	（1）`git log`命令显示从最近到最远的提交日志。

​	（2）如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数。

```bash
$ git reset --hard HEAD^
$ git log
$ git reset --hard 1094a
$ git reflog
```

​	（1）上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

​	（2）穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。

​	（3）Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。

​	（4）重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

##### 4  远程仓库

###### 4.1  GitHub账号的设置

​	（1）创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```bash
$ ssh-keygen -t rsa -C "youremail@example.com"
```

​	你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

​	如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

​	（2）登陆GitHub，打开“Settings”，“SSH and GPG keys”页面。然后，点“New SSH key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。点“Add Key”，你就应该看到已经添加的Key。

###### 4.2  删除远程库

```bash
$ git remote -v
$ git remote rm origin
```

​	（1）`git remote -v`查看远程库信息。

​	（2）删除远程库，可以用`git remote rm `命令。此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

###### 4.3  从远程库克隆

```bash
$ git clone git@github.com:michaelliao/gitskills.git
```

​	（1）Git支持多种协议，包括`https`，但`ssh`协议速度最快。

###### 4.4  关联远程库

```bash
$ git remote add origin git@github.com:exploring-lin/learngit.git
```

​	（1）要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`。

​	（2）关联一个远程库时必须给远程库指定一个名字，`origin`是默认习惯命名。

​	（3）关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容。

​	（4）此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改。

##### 5  分支管理

###### 5.1  创建与合并分支

```bash
$ git switch -c dev
$ git branch
$ git switch master
$ git merge dev
$ git branch -d dev
```

​	（1）创建并切换到新的`dev`分支。

​	（2）`git branch`命令会列出所有分支，当前分支前面会标一个`*`号。

​	（3）直接切换到已有的`master`分支。

​	（4）`git merge`命令用于合并指定分支到当前分支。

​	（5）合并完成后，就可以放心地删除`dev`分支了。

​	（6）创建分支：`git branch `。

###### 5.2  解决冲突

```bash
$ git log --graph --pretty=oneline --abbrev-commit
```

​	（1）用带参数的`git log`也可以看到分支的合并情况。

​	（2）当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

###### 5.3  分支策略

```bash
$ git merge --no-ff -m "merge with no-ff" dev
$ git log --graph --pretty=oneline --abbrev-commit
```

​	（1）合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

​	（2）合并后，我们用`git log`看看分支历史。

![image-20220514111452726](C:\Users\Sam_Lin\AppData\Roaming\Typora\typora-user-images\image-20220514111452726.png)





https://www.liaoxuefeng.com/wiki/896043488029600/900004111093344