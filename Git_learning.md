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





https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192