### Git的入门命令：

初始化创建本地仓库：git init

###### touch a.txt或  echo.>b.txt

创建a.txt文件

###### 

<font color=red>未被追踪：untracked File</font>

###### 重复上一个操作，按向上箭头

git commit 提交

git config --global user.email "you@example.com"

git config --global user.name "your name"

git config -l

###### Vim编辑模式

* i 添加文字  <font color=red>右键——设置——环境set LANG =zh_CN.UTF-8(中午乱码）</font>
* esc退出编辑模式
* ZZ保存退出   

如何查看我们提交上去的信息呢 Git log

**git 三个工作区：**工作目录、暂存区（stage)、版本区（git仓库）

git add filename

git add . 添加所有文件

Git commit

git commit -m "添加描述"

git log <commit-id>

git commit -a -m "添加描述"  或者  git commit -am "描述"

Git log 想退出的话按下小写的q

##### 删除文件

Git status

##### Git rm 文件名  <font color =red>删除git区域中记录的文件，并且不保留在工作目录中</font>

一、在工作目录删除一个文件，git status ,并没有完全删除

Git rm a.txt 回车，git status ,git commit -m "删除了一个文件"

二、git rm b.txt,当前工作目录的b.txt 删除了，Git status,git commit -m "删除"

##### git rm -f 文件名 <font color =red>强制删除文件</font>

##### git rm --cache 文件名 <font color=red>删除git仓库中的，保留工作目录中的文件</font>

git log 如果太多查看补完可以敲回车

##### 移动文件 git mv file_from file_to

mkdir reci

git mv a.txt reci/a.txt

git status

##### 重命名文件名称

touch b.txt

git add.

git commit -m "miaowsu"

git status

<font color=red>**因为移动的原理，导致我们在原地操作移动命令，可以重命名文件夹**</font>

Git add .

git commit -m "移动b文件"

###### 移动的命令相当于以下三条集合

mv file_from file_to

git rm file_from

git add file_to

##### 查看命令

git status

git status -s  [??未追踪到文件，A添加到暂存区的，（）M被修改但是未放入暂存区的，

MM 被修改后放入暂存区的，并且又再次修改的，M（）被修改后放入暂存区]

git log 

git log -p

git log -n



### head 查看文件前n行：  *head --help*

用法：head [选项]… [文件]…
注意：head查看文件的前n行，默认n=10

#### <font color=red>miaov--------Git</font>

* **cd命令：**
  * cd  /My-Python/sound ----------------->进入多个层级的目录
  * cd  ../..------------------------------>返回父级目录
* 利用Git 创建一个库：
  * 1、在github上建立远程仓库
  * 2、git clone https://github.com/lsf1192354203/markdown-note.git
  * 3、cd my_git ------>进入到项目
  * 3、设置贡献者
    * ——name
    * ——email
    * ——git config  --global user.name  “lsf1192354203"
    * ——git config  --global user.email   “1192354203@qq.com"
    * ——git config  --global user.name------>查看用户名
    * ——git config  --global user.email------->查看邮箱
    * ——git config -list-------------------->>查看所有配置项
* **git status**：查看当前仓库所在目录的文件状态
* **git add demo.html**:[master  +2 ~0 -0 !]是工作区2个文件，修改0个，减少0个文件，绿色代表暂存区，红色代表工作区。-----------由工作区------>暂存区
* **git add .**将修改后的所有文件全部提交到暂存区
* **git reset HEAD demo.html**撤回工作区-------暂存区的文件
* **git commit**-------->由暂存区到-----版本区
* **git commit -m "change file description"**
* **git commit -a -m "file description"**---->简写方式，由工作区--------->版本库
* **git log**打印修改的记录
* **git diff**----->工作区与暂存区的差异





  































