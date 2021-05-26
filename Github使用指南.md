<!-- vscode-markdown-toc -->
* 1. [下载与安装](#)
* 2. [基本使用方法](#-1)
	* 2.1. [Git简介](#Git)
	* 2.2. [Git之禅](#Git-1)
	* 2.3. [Git使用](#Git-1)
		* 2.3.1. [0. 预备操作：设置/查看/重置用户名，邮箱，代理](#-1)
		* 2.3.2. [1. 创建本地新的空repository（init命令）](#repositoryinit)
		* 2.3.3. [2. 往里面随便放点什么](#-1)
		* 2.3.4. [3. 跟踪文件（add命令）](#add)
		* 2.3.5. [4. 提交修改，产生一个新的分支（commit命令）](#commit)
		* 2.3.6. [5. 删除文件与撤销删除（rm，checkout命令）](#rmcheckout)
		* 2.3.7. [6. 回退版本（reset命令）](#reset)
		* 2.3.8. [7. 查看版本信息，当前的仓库状态（log，status，reflog命令）](#logstatusreflog)
		* 2.3.9. [8. 分支管理（本节可能一般用不到，但是万一呢，毕竟这是Git的灵魂啊）](#Git-1)
	* 2.4. [GitHub与Git](#GitHubGit)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
##  1. <a name=''></a>下载与安装
到百度上搜索Git然后直接安装就好啦
安装完成后记得在控制台（CMD）尝试输入git并回车，如果显示没有此命令，可能是环境变量的缓存问题，重启以后应该就好了<br>
~~还是不行就找我~~

##  2. <a name='-1'></a>基本使用方法
###  2.1. <a name='Git'></a>Git简介
首先声明：Git和Github没有任何直接关系，请不要被误导了！<br>
~~如果要打个比方的话那就是相当于Porn和PornHub的关系~~<br>
首先，我们要认识到，这是一个**分布式版本控制系统**。什么意思呢？软件在开发过程中会随着时间不断迭代，每一次迭代就会产生一个新的版本。如果当前版本出现问题，或者你想到以前写过一个不错的函数，但是当前版本已经移除它了，如果你没有备份，那么你就出了大问题，你什么都做不了，只能干瞪眼！这时候版本控制系统就派上用场了。用Git对文件进行跟踪、回溯，你可以很快找到你需要的老版本而不需要付出任何代价！所以，请记住，**这仅仅是一个控制软件版本和控制开发分支的一个系统**。

###  2.2. <a name='Git-1'></a>Git之禅
和Python一样，Git也有自己的使用哲学。Git的版本控制由这样几个部分构成：<br>
`工作区`、`暂存区`、`版本库（又称之为仓库，Repository）`。工作区就是我们能看到的文件夹，我们对一切文件修改都是在工作区修改的。当你准备把修改的文件添加跟踪(`add`命令，后面会将)时，数据就存入了暂存区。一旦修改完毕，你提交了修改(`commit`)，数据就从暂存区放入了版本库，并且为这次修改生成了一个新的版本。<br>
**因此，在还没提交之前，你都有机会反悔，通过命令删除存入到暂存区的数据，修改你的版本！**

除了版本管理，Git还有其他版本控制系统没有（或者支持很差）的一个独家功能：分支控制(`branch`)。你可以把分支理解为平行宇宙：你在学习英语的时候，另一个平行宇宙的你（新分支）开始学习日语。等你们都学完了，一旦进行分支合并，那么你就即会日语又会英语了！在多人合作上是很方便的一个功能！<br>
**因此，请多多使用分支功能。官方非常推荐用户大量使用版本分支。无论你是准备测试代码还是和朋友一起写项目，请时刻记得开一个新的分支！**

###  2.3. <a name='Git-1'></a>Git使用
####  2.3.1. <a name='-1'></a>0. 预备操作：设置/查看/重置用户名，邮箱，代理
在使用git之前，我们需要一些预备操作。<br>
在控制台端，#号表示注释。以下代码皆为可以直接运行的shell命令。<br>
##### 用户名和邮箱：
```shell
#设置
git config —-global user.name "君の名前"
git config --global user.email "君のEメール"
#查看
git config --global --get user.name
git config --global --get user.email
#重制
git config --global --unset user.name
git config --global --unset user.name
```
##### 代理
```shell
#设置
git config —-global http.proxy "代理地址"
git config --global https.proxy "同上"
#查看
git config --global --get http.proxy
git config --global --get https.proxy
#重制
git config --global --unset http.proxy
git config --global --unset https.proxy
```
####  2.3.2. <a name='repositoryinit'></a>1. 创建本地新的空repository（init命令）
我们创建一个叫GitLearning的文件夹，作为我们的学习项目。
```shell
mkdir GitLearning # make directory，意思是创建一个文件夹
cd GitLearning # change directory，意思是改变当前目录，即进入到文件夹中
git init # 初始化(initialize)git仓库
explorer . # 呼唤Windows的文件管理器打开当前目录
```
如果能在当前文件管理器下看到一个名称为`.git`的隐藏文件，说明我们的仓库创建成功了。

####  2.3.3. <a name='-1'></a>2. 往里面随便放点什么
用VSCode，VIM往这个文件夹里面写点什么文本文档。什么都可以，但就是不要用记事本，控制台。微软自作聪明往里面添加了BOOM头，这会使文本文档在其他平台开头乱码。<br>
现在我们来创建两个文本文档。内容如下<br>
readme.txt:
```
Hello, Git!
```
file1:
```
Test
```
####  2.3.4. <a name='add'></a>3. 跟踪文件（add命令）
把文件从工作区放入暂存区，这一步是必要的。

```shell
# git add 文件名1 文件名2...
git add readme.txt file1
```
当然，你可以用下面几个批量添加指令，我来一一介绍。<br>
很明显，对于初次添加的我们，可以使用第一个和最后一个命令添加我们新建的文件。<br>
##### git add .
功能：添加所有**新建**的和**被修改的**文件
##### git add -u (git add --update)
功能：添加所有**被删除的**和**被修改的**文件
##### git add -A (git add --all)
功能：上面两个命令的合并功能

####  2.3.5. <a name='commit'></a>4. 提交修改，产生一个新的分支（commit命令）

```shell
# 提交这次修改，并且添加版本信息message（此信息是必须的！）
git commit -m "message"
```
这是我的控制台的输出：

```
PS C:\Users\Haotian\GitLearning> git commit -m "First add"
[master (root-commit) 1076c4c] First add
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file1
 create mode 100644 readme.txt
```
现在，一个新的版本已经添加。但稍后我会教你们如何查看这个版本信息。现在先学学删除文件。
####  2.3.6. <a name='rmcheckout'></a>5. 删除文件与撤销删除（rm，checkout命令）
rm就是remove的意思，这里用指令删除：

```shell
git rm file1
ls # 查看文件夹，发现确实删除了
```

如果我们误删了，但还没提交，怎么快速恢复误删的文件？<br>
用`git checkout -- 文件名`即可，这里我们这样撤销：
```shell
git checkout -- file1
ls
```

文件确实回来了。
####  2.3.7. <a name='reset'></a>6. 回退版本（reset命令）
如果你知道你的版本号，那么你可以直接执行以下命令：

```
git reset --hard 版本号
```
如果你不知道呢？下一小节有教你怎么看版本号。

如果你仅仅是想回退到上一个版本，请这样使用：

```
git reset --hard HEAD^
```
其中HEAD是版本指针，指向当前版本，后面加一个^意思是前一个版本，可以加任意多个^。如果不加，就是回退到当前版本。

####  2.3.8. <a name='logstatusreflog'></a>7. 查看版本信息，当前的仓库状态（log，status，reflog命令）
```shell
git status
```
可以查看当前工作区的状态。假设我们已经删除了file1，但是还没有提交，那么如果我们执行这个命令，会得到以下的输出：

```
PS C:\Users\Haotian\GitLearning> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    file1
```
当然，如果你在工作区添加了文件，你却没有add，它也会告诉你哪些文件没有被跟踪。

现在看看怎么查看版本号。
```shell
git log
```
是从**当前分支**开始打印版本号。<br>
也就是说，如果你有0～4个版本，假设版本更迭顺序是0，1，2，3，4，你当前在版本4，打印的结果便是0，1，2，3，4。<br>
如果你切换到版本2，那么你打印的结果便是0，1，2了。<br>

如果想查看所有历史的版本号，可以用<br>
```shell
git reflog
```
这是我切换版本后的输出，根据这些信息可以切换回版本。<br>
```
PS C:\Users\Haotian\GitLearning> git reflog
1076c4c (HEAD -> master) HEAD@{0}: reset: moving to HEAD^
f63087c HEAD@{1}: commit: Remove file1
1076c4c (HEAD -> master) HEAD@{2}: reset: moving to HEAD
1076c4c (HEAD -> master) HEAD@{3}: commit (initial): First add
```

####  2.3.9. <a name='Git-1'></a>8. 分支管理（本节可能一般用不到，但是万一呢，毕竟这是Git的灵魂啊）
我在开头的`Git之禅`已经介绍过分支了，如果还是不清楚，可以参考这篇文章：
[分支管理](https://www.liaoxuefeng.com/wiki/896043488029600/896954848507552)
这篇文章讲的很好，我就不献丑了。
###  2.4. <a name='GitHubGit'></a>GitHub与Git
这节介绍如何联动GitHub
#### Clone命令
Clone命令是指把远程的放在GitHub上的Repository下载到本地。指令很简单，
```shell
git clone 地址
```
配合代理食用更佳。

#### 提交代码到GitHub (Push)
现在我们把GitLearning上传到GitHub上。
```shell
# 将当前分支重命名为main
git branch -M main
# 连接到远程仓库
git remote add origin https://github.com/chtzs/GitLearning.git
# 提交分支
git push -u origin main
```

注意⚠️ 以上情况仅针对于第一次提交，对于之后的提交，只需要运行代码
```shell
git push origin main
```
即可。

#### 拉取远程代码，更新本地仓库 (Pull)
如果GitHub上已经是最新的代码，但本地仓库还是旧版本，那么可以用以下命令同步：
```
git pull origin
```
