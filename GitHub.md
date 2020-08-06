# GitHub入门与实战

1. Git和GitHub的区别

   ​	GitHub是为开发者提供Git仓库的托管服务。GitHub上公开的软件源代码全都由Git进行管理。

   源代码是放到Git仓库中的。

2. pull request

   指开发者在本地对源代码进行更改后，向GitHub中托管的Git仓库请求合并的功能。

3. watch功能

   将某代码库的仓库添加到watch中，便能在第一时间掌握最新版本的新功能或BUG修正的信息。

4. Git属于分散型，可以实现版本管理，版本管理就是管理更新的历史记录。

## Git 的初始化配置

1. 设置姓名和邮箱地址（linux 系统不要加上双引号）

   `git config --global user.name "name"`

   `git config --global user.email "email@email.com"`

   这里设置的姓名和邮箱地址会用在Git的提交日志中，会随着提交日志一同被公开。

2. 提供输出的可读性，使输出变得更容易分辨

   `git config --global color.ui auto`输入该句之后，**.gitconfig**中会增加下面一行：

   ```
   [color]
      ui = auto
   ```

   ## 使用GitHub的前期准备

   1. 在GitHub上创建账号

   2. 设置SSH Key

      运行一下命令创建SSH Key：

      `ssh-keygen -t rsa -C 823398853@qq.com`

      `your_email@example.com`是创建账号时用的邮箱地址。

      id_rsa文件是私有密钥，id_rsa.pub是公开密钥。

   3. 添加公开密钥

      添加公开密钥之后，就可以用私有密钥进行认证了。

      私有密钥验证命令

      `ssh -T git@github.com`

      如果出现错误，重新设置SSH Key

   4. 在GitHub上创建仓库

   5. 公开代码

      5.1 clone已有仓库至本地目录（C:\Users\honglang）

      `git clonegit@github.com:gitfishup/git_tutorial.git`

      认证成功后，仓库便会被clone至仓库名后的目录中。将想要公开的代码提交至这个仓库再push到GitHub的仓库中，代码便会被公开。

      5.2 创建新的文件:在clone的目录下（C:\Users\honglang\git_tutorial）

       git bash 中进入被克隆的git_tutorial，执行*git status*，因为还没有添加至Git仓库，所以新添加的文件是红色的Untracked files。

      5.3 提交新文件到Git仓库中

      `git add hello.c`  通过 git add命令将文件加入暂存区  

      `git commit -m "Add hello.c "` 通过 git commit命令提交。  

      5.4 更新GitHub上的仓库

      `git push`

      ##  通过实际操作学习Git

      ### 4.1 基本操作

      1. *git init* 初始化仓库：要使用Git 进行版本管理，必须先初始化仓库。

         ```shell
         $ mkdir git-tutorial
         $ cd git-tutorial
         $ git init
         Initialized empty Git repository in /Users/hirocaster/github/github-book
      /git-tutorial/.git/
         ```

         git init后，生成了一个*.git* 文件夹，该文件夹的内容称为**附属于该仓库的工作树**。文件的编辑等操作在工作树中进行，然后记录到仓库中，以此管理文件的历史快照。开发者可以通过这种方式获取以往的文件。

         2. *git status*查看仓库的状态

            处于哪个分支，哪些文件没被添加进去。状态中的“commit”指**记录工作树中所有文件的当前状态**。*nothing to commit*表示尚没有可提交的内容，就是说当前我们建立的这个仓库中还没有记录任何文件的任何状态。

         3. *git add* 暂存区添加文件

            ​	要想让文件成为Git仓库的管理对象，就需要用git add命令将其加入暂存区（stage或者Index）中。暂存区是提交之前的一个临时区域。

         4. *git rm --cached <file>*
         
            使用(use "git rm --cached <file>..." to unstage)去移除git add状态
         
         5. *git commit* 保存仓库的历史记录
         
            ​	 *git command*命令可以将当前暂存区中的文件实际保存到仓库的历史记录中。通过这些记录，我们就可以在工作树中复原文件。
         
            5.1 记述一行提交信息
         
            ​	`git commit -m "First Commit"`
         
            5.2 记述详细提交信息
         
            ​	`git commit`
         
            执行之后，出现编辑器编辑、
         
            中止提交：将提交信息留空并直接关闭编辑器。
         
         6. *git log*查看当前状态提交的日志
         
            ​	什么人在什么时候进行了提交或合并，以及操作前后有怎样的差别。
         
            6.1 只显示提交的第一行	
         
            ​		`git log --pretty=short`
         
            6.2 只显示指定目录、文件的日志
         
            ​		只要在git log 命令后加上目录名，便会只显示该目录下的日志。如果加的是文件名，就会只显示与该文件相关的日志。
         
            ​	`git log README.md`
         
            6.3 显示文件的改动
         
            ​	`git log -p`
         
            ​	`git log -p README.md`
         
         7. *git diff*命令查看更改前后的差别
         
            ​	git diff命令可以查看工作树、暂存区、最新提交之间的差别。
         
            7.1 *git  diff  HEAD*查看与最新提交的差别。
         
            ​	在执行git commit 命令之前最好先执行 git diff HEAD 命令，查看本次提交与上次提交之间的差别，等确认完毕后再进行提交。这里的HEAD是指向当前分支中最新一次提交的指针。

      ### 4.2 分支操作

      ​	在进行多个并行作业时，我们会用到分支。

      ​	不同分支中，可以同时进行完全不同的作业。通过灵活运用分支，可以让多人同时高效地进行并行开发。

      1. 查看分支 git branch 

      2. 创建并进入分支  git checkout  -b 

      3. 切换分支     git checkout master

         切换回上一个分支  git checkout -

      4. 合并分支：将feature-A分区合并到主干分支master

         切换到master分区  git checkout master

         合并feature-A分支到master分区  git merge --no-ff feature-A 

      [为了在历史记录中明确记录下本次分支合并，我们需要创建合并提交。因此，在合并时加上 --no-ff参数。  ]

      5. 以图表形式查看分支 git log --graph

      

      ### 4.3 更改提交的操作

      1. 回溯历史版本 

         ​	git reset --hard dsfrgsd423（哈希值）

      2. 查看当前仓库执行过的操作日志

         ​	git reflog

      3. 合并的时候会出现冲突

         - 查看冲突部分并将其解决/删掉

      4. 修改提交信息    git commit --amend

         ​	 git commit --amend

         `[master 23567dfg] Modify Commit Test1 branch 'test1'`

         master后面跟的是master的哈希值，‘test1’是分支的名称

      5. 压缩历史  git rebase -i（不重要）

         在合并特性分支**之前**，如果发现已提交的内容中有些许拼写错误等，不妨提交一个修改，然后将这个修改包含到前一个提交之中，压缩成一个历史记录。

         如果能在最初提交之前就发现并修正这些错误，也就不
         会出现这类提交了。  

      6. 更改/抹去历史

         ​	git rebase -i HEAD~2

      ### 4.4 推送至远程仓库

      1. git remote add 添加远程仓库，该远程仓库是本地仓库的远程仓库

         git remote add origin git@github.com:gitfishup/git_tutorial.git  

         执行上述命令之后，git 会自动创建git@github.com:gitfishup/git_tutorial.git远程仓库，该远程仓库的名称设置为origin（只是一个标记，代表远程仓库的地址）

      2. git push  推送当前分支的内容至远程仓库

         2.1 推送至master分支

         `git push -u origin master`

         执行git push命令，当前分支的内容就会被推送给远程仓库origin的master分支。

         -u 参数可以在推送的同时，将origin仓库的master分支设置为本地仓库当前分支的upstream（上游）。

         添加了这个参数，将来运行git pull命令从远程仓库获取内容时，本地仓库的这个分支就可以直接从origin的master分支获取内容，省去了另外添加参数的麻烦。

         2.2 推送至master意外的分支

         `git push -u origin feature-D `

         执行以上命令，本地仓库的内容就推送至远程仓库的feature分支

      ### 4.5 从远程仓库获取

      1. 获取远程仓库  git clone

         ` git clone git@github.com:gitfishup/git_tutorial.git`

      2. 查看远程仓库的分支

         ​	`git branch -a `

         -a 参数既可以看本地仓库的分支，也可以看远程仓库的分支

      3. 获取远程的feature-D分支到本地仓库

         `git checkout -b feature-D origin/feature-D`

         -b 表示在本地仓库中新建分支，名称为feature-D。 origin/feature-D表示远程仓库的分支。

      4. 修改本地分支feature-D中的文件

      5. 查看修改前后的差别  git  diff

      6. 添加并提交该分支

         ​	`git commit-am “Add feature-D”`

      7. git pull 获取最新的远程仓库分支

         ​	`git pull origin feature-D`

         当多名开发者在同一个分支中进行操作时，为减少冲突情况的发生，建议频繁地进行push和pull操作。

      

      ​	

      

      

   

   ​	