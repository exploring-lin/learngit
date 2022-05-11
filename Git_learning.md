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

