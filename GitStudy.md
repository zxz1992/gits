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
#### 三、添加文件到Git仓库
分两步：
* 第一步，使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
```
$ git add readme.txt
```
* 第二步，使用命令`git commit`，完成。
```
$ git commit -m "wrote a readme file"
[master (root-commit) cb926e7] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
 ```

#### 四、版本切换
在Git中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到某一版本时，再想恢复到之前的版本，就必须找到这一版本的`commit id`。Git提供了一个命令`git reflog`用来记录你的每一次命令：
```
$ git reflog
ea34578 HEAD@{0}: reset: moving to HEAD^
3628164 HEAD@{1}: commit: append GPL
ea34578 HEAD@{2}: commit: add distributed
cb926e7 HEAD@{3}: commit (initial): wrote a readme file
```
`HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。


#### 五、创建合并分支
在版本回退里，你已经知道，每次提交，`Git`都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在`Git`里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。

一开始的时候，`master`分支是一条线，`Git`用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：
![](http://www.liaoxuefeng.com/files/attachments/0013849087937492135fbf4bbd24dfcbc18349a8a59d36d000/0)

当我们创建新的分支，例如`dev`时，`Git`新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：
![](http://www.liaoxuefeng.com/files/attachments/001384908811773187a597e2d844eefb11f5cf5d56135ca000/0)

你看，`Git`创建一个分支很快，因为除了增加一个`dev`指针，改改HEAD的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：
![](http://www.liaoxuefeng.com/files/attachments/0013849088235627813efe7649b4f008900e5365bb72323000/0)

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。`Git`怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：
![](http://www.liaoxuefeng.com/files/attachments/00138490883510324231a837e5d4aee844d3e4692ba50f5000/0)

__小结：__

* 查看分支：git branch

* 创建分支：git branch <name>

* 切换分支：git checkout <name>

* 创建+切换分支：git checkout -b <name>

* 合并某分支到当前分支：git merge <name>

* 删除分支：git branch -d <name>
#### 六、远程仓库
1. 添加远程库
首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

![](http://www.liaoxuefeng.com/files/attachments/0013849084639042e9b7d8d927140dba47c13e76fe5f0d6000/0)

在Repository name填入`learngit`，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：

![](http://www.liaoxuefeng.com/files/attachments/0013849084720379a3eae576b9f417da2add578c8612a2e000/0)

现在，我们根据GitHub的提示，在本地的`learngit`仓库下运行命令：
```
$ git remote add origin git@github.com:michaelliao/learngit.git
```
添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。

把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。

2. 从远程库克隆
首先，登陆GitHub，创建一个新的仓库，名字叫`gitskills`：

![](http://www.liaoxuefeng.com/files/attachments/0013849085474010fec165e9c7449eea4417512c2b64bc9000/0)

我们勾选`Initialize this repository with a README`，这样`GitHub`会自动为我们创建一个`README.md`文件。创建完毕后，可以看到`README.md`文件：
![](http://www.liaoxuefeng.com/files/attachments/0013849085607106c2391754c544772830983d189bad807000/0)

现在，远程库已经准备好了，下一步是用命令`git clone`克隆一个本地库：
```
$ git clone git@github.com:michaelliao/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.

$ cd gitskills
$ ls
README.md
```
