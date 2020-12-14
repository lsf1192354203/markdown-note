### Git的入门命令：

### 初始化创建本地仓库

* **git init**

* **touch a.txt或  echo.>b.txt**:创建文件

### Vim编辑模式

* **i **添加文字描述，如果输入中文：则：  <font color=red>右键——设置——环境------set LANG =zh_CN.UTF-8</font>
* **git config --global core.quotepath false**---------->这样不会对0x80以上的字符进行quote,中文显示正常
* **Esc**:退出编辑模式
* **ZZ**:保存退出   

### 快捷方式：

* 重复上一个操作，按向上箭头

### head 查看文件前n行：  *head --help*

* 用法：head [选项]… [文件]…
* 注意：head查看文件的前n行，默认n=10

#### <font color=red>miaov--------Git</font>

* **git 三个工作区：**工作目录、暂存区（stage)、版本区（git仓库）
* **cd命令：**
  * cd  /My-Python/sound ----------------->进入多个层级的目录
  * cd  ../..------------------------------>返回父级目录
* **利用Git 创建一个库：**
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
    * ——git config  --global --unset user.name------>删除用户名
    * ——git config  --global --unset user.email------->删除邮箱
    * ——git config  --local user.name  “lsf1192354203"
    * ——git config  --local user.email   “1192354203@qq.com"
    * ——git config -list-------------------->>查看所有配置项
* **git status**：查看当前仓库所在目录的文件状态
  * **git status -s **==git status --short 简化打印内容
  * **short符号**
    * **n**:未追踪文件
    * **A**：添加到暂存区的
    * **M**：被修改但是未放入暂存区的
    * **MM**:被修改后放入暂存区，并且又再次修改
    * **M  **:被修改后放入暂存区的
* **git add demo.html**:[master  +2 ~0 -0 !]是工作区2个文件，!是冲突，修改0个，减少0个文件，绿色代表暂存区，红色代表工作区。-----------由工作区------>暂存区
* **git add .**将修改后的所有文件全部提交到暂存区
* **git commit**-------->由暂存区到-----版本区
* **git commit -m "change file description"**
* **git commit -a -m "file description"**---->简写方式，由工作区--------->版本库

### 打印记录

* **git log**打印修改的记录,按回车键可以查看剩余的记录，退出按**q**键
* **git log -p**：查看详细提交信息
* **git log -n**：查看n条提交信息

### 对比

* **git diff**----->工作区与暂存区的差异
* **git diff --cached**:-------->对比的是暂存区与版本区的差异
* **git diff HEAD**:-------->对比的是工作区与版本区的差异

### 撤销

* **git reset HEAD git.js**:从暂存区恢复至工作区，清空暂存区
* **git checkout --git.js**:从版本区恢复至工作区。
  * git switch:用来切换分支
  * git restore filename:用来还原工作区的文件，
* **git commit --amend**:已经提交后的发现有问题的文件，撤销之前的提交，git commit -m "change git .js"  --amend。

### 删除

* **git rm test.txt**:在工作区创建了一个test.txt文件，然后git add暂存区，之后在工作区删除test.txt,此时暂存区还有test.txt,这时候用**git rm test.txt**来删除暂存区文件
* **git rm -f test.txt**:在工作区创建了一个test.txt文件，然后git add暂存区，之后删除暂存区test.txt,此时工作区test.txt也被删除了
* **git rm --cached test.txt**:在工作区创建了一个test.txt文件，然后git add暂存区，之后删除暂存区test.txt,此时工作区test.txt仍存在

### 移动文件

* **git rm a.txt  文件夹名字（fold）/a.txt**==**git mv a.txt fold**:将a.txt 文件移动到fold文件夹里
* **移动的命令相当于**：
  * **mv file_from file_to **
  * **git rm file_from **
  * **git add file_to**

### 重命名文件

* **git mv readme.txt readme.md**:将文件readme.txt重命名readme.md

### 恢复

* **git checkout commit_id filename**:不小心误删了工作区的文件，可以通过此命令恢复，指定文件的还原
* **git reset --hard commit_id **:恢复到之前的版本，这个还原操作是对版本的还原
  * **git reset --hard HEAD^**:^代表往回往下走一步
  * **git reset --hard HEAD~num**:num代表往回往下走num步

* **git reflog**:再回到恢复之前
### 同步到远程仓库

* **git remote**:查看远程仓库的名称,可以修改远程仓库名称**git remote add origin [远端仓库的真实地址]（https://github.com/lsf1192354203/markdown-note.git）**
* **git remote -v**:可以查看这个远端仓库对应的地址
* **git push origin master**:origin----->远端仓库名，master----->对应的分支

### 多人协作解决冲突

eg:如果合作伙伴修改了文件并提交了，同时你没有更新，直接修改了同一个文件，这时提交会报错。一下是解决冲突的方式：

* **git fetch**：把远端的仓库拉取过来，但是并不合并；需要通过手动的方式进行合并
  * git diff master origin/master
    * origin master 是两件事，origin/master是一件事
    * master是 一个本地分支
    * origin/master是远程分支（它是名为“origin"的远程分支的本地副本，名为”master“
* **git merge origin/master**:
* **git pull**:直接拉取过来直接合并

### 开源项目的协作
eg:如何参与到没有权限的开源项目中：

* fork：其实是开了一个新的分支，克隆了一个整体的版本放到当前用户名下
* pull request

### Git下的分支处理

* **git branch**:查看当前分支
* **git branch new1**:创建分支new1
* **git checkout new1**:切换分支new1
* **git checkout -b new2**:简写：创建new2分支并切换到new2分支
* **git merge new1**:合并new1分支
* **git checkout new2**:----->git commit -a -m-------->git checkout main
* **git branch --merged**:查看的是main合并的分支
* **git branch --no-merged**:查看的是main没有合并的分支
* **git branch -d new1**:删除new1分支<font color=red>没有合并的分支是不允许删除的</font>
* **git branch -D new2**:强制删除没有合并的分支
* **git branch**:查看分支
* **git branch -a**:查看所有分支。

**<font color=blue>github上的分支</font>**

* **git push**
* github上直接创建

### Git 下的tag标签处理

* **git tag**:查看标签。

* **git checkout tag_name**:(<font color=red>提示：git 处于一个detached HEAD状态。【detached 分离的】，因为tag相当于是一个快照，是不能更改它的代码的</font>)切换分支
* 其实**tag**和**branch**是一样的操作
* 






























