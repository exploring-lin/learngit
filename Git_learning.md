**安装Git**

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

##### 2  把一个文件放到Git仓库

```bash
$ git add Git_learning.md
$ git commit -m "wroto a learning file"
```

（1）简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

（2）用`ls`或者`dir`命令查看当前目录的文件。

##### 3  掌握工作区的状态

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

##### 4  版本回退

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

##### 5  撤销修改

​	（1）use "git restore <file>..." to discard changes in working directory.

​		把文件在工作区的修改全部撤销，这里有两种情况：

​		1）一种是文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

​		2）一种是文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

​		总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

​	（2）use "git restore --staged <file>..." to unstage.

##### 6  删除文件



https://www.liaoxuefeng.com/wiki/896043488029600/900002180232448