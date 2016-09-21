### git学习笔记
#### 一、git安装
1. 在linux上安装git
```
sudo apt-get install git
```
2. 在Windows上安装git

       到`https://git-for-windows.github.io`下载，，然后按默认选项安装即可。
3. 配置

  安装完成后，还需要最后一步设置，在命令行输入：
  ```
  $ git config --global user.name "Your Name"
  $ git config --global user.email "email@example.com"
  ```

#### 二、初始化git仓库
创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：
```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```
pwd命令用于显示当前目录。在我的Mac上，这个仓库位于/Users/michael/learngit。

如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。

第二步，通过git init命令把这个目录变成Git可以管理的仓库：
```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。
