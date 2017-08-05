#### git安装
Windows：[Git for Windows](https://git-for-windows.github.io/)
Mac：[git-osx-installer download](https://sourceforge.net/projects/git-osx-installer/) 
#### 如何判断Git是否安装成功？
在命令行中输入git，出现Git命令列表即为成功 Git的所有操作命令都要以 git 开头，Git命令列表中列举了一些最常用的Git命令，并附有解释
#### 创建新的git仓库
mkdir test （新建文件夹test）
cd test （切换到test目录）
pwd （显示当前目录）
touch a.md （新建a.md文件） 
PS：在进行任何 Git 操作之前，都要先切换到 Git 仓库目录
PPS：为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文 
这个时候先随便操作一个命令，比如 git status ，可以看到如下提示 意思就是当前目录还不是一个Git仓库 
###### git init 将目录变成Git可以管理的仓库
此时已建立好一个空仓库（empty Git repository），可看见目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。
如果没有看到.git目录，是因为这个目录是默认隐藏的，用'ls -ah'命令就可看见
PS：若未创建文件夹，直接输入git init 命令，则会吧主目录初始化成一个git仓库，需要删除.git目录'rm -rf ~/.git' 
###### git status查看状态
可以看到a.md这个文件未被跟踪（Untracked files） 
###### git add
输入git add a.md，再输入git status此时提示以下文件 Changes to be committed ， 意思就是 a.md 文件等待被提交，当然你可以使用 git rm --cached 这个命令去移除这个缓存。 
###### git commit
输入 git commit -m "first commit" commit 是提交的意思，-m后面输入本次提交的说明，执行了以上命令代表我们已经正式进行了第一次提交。 
提交的时候,如果出现这些提示,说明你还没自报家门,没有声明你是谁!也人性化的告诉了你使用申明方法去声明你的身份!  
'git config --global user.email "you@example.com"'  
'git config --global user.name "Your Name"'
然后再次提交下, 显示下面这样就说明提交成功了 这个时候再输入 git status ，会提示 nothing to commit 
##### 为什么Git添加文件需要add，commit一共两步呢？
因为commit可以一次提交很多文件，所以你可以多次add不同的文件,只做一次提交!
###### git log
可以查看所有产生的 commit 记录 可以看到已经产生了一条 commit 记录，而提交时候的附带信息叫 "first commit" 。 
###### git branchbranch 
即分支的意思，分支的概念很重要，尤其是团队协作的时候，假设两个人都在做同一个项目，这个时候分支就是保证两人能协同合作的最大利器了。
举个例子，A, B俩人都在做同一个项目，但是不同的模块，这个时候A新建了一个分支叫a， B新建了一个分支叫b，这样A、B做的所有代码改动都各自在各自的分支，互不影响，等到俩人都把各自的模块都做完了，最后再统一把分支合并起来。
执行 git init 初始化git仓库之后会默认生成一个主分支 master ，也是你所在的默认分支，也基本是实际开发正式环境下的分支，一般情况下 master 分支不会轻易直接在上面操作的，你们可以输入 git branch 查看下当前分支情况： 
如果我们想在此基础上新建一个分支呢，很简单，执行 git branch a 就新建了一个名字叫 a 的分支，这时候分支 a 跟分支 master 是一模一样的内容，我们再输入 git branch 查看的当前分支情况： 
但是可以看到 master 分支前有个 * 号，即虽然新建了一个 a 的分支，但是当前所在的分支还是在 master 上，如果我们想在 a 分支上进行开发，首先要先切换到 a 分支上才行，所以下一步要切换分支
###### git checkout a 
可以看到当前我们在的分支已经是a了 那有人就说了，我要先新建再切换，未免有点麻烦，有没有一步到位的
###### git checkout -b a
这个命令的意思就是新建一个a分支，并且自动切换到a分支。 有新建分支，那肯定有删除分支，假如这个分支新建错了，或者a分支的代码已经顺利合并到 master 分支来了，那么a分支没用了，需要删除，这个时候执行
###### git branch -d a 
就可以把a分支删除了。 
###### git branch -D
有些时候可能会删除失败，比如如果a分支的代码还没有合并到master，你执行 git branch -d a 是删除不了的，它会智能的提示你a分支还有未合并的代码，但是如果你非要删除，那就执行 git branch -D a 就可以强制删除a分支 
###### git tag
我们在客户端开发的时候经常有版本的概念，比如v1.0、v1.1之类的，不同的版本肯定对应不同的代码，所以我一般要给我们的代码加上标签，这样假设v1.1版本出了一个新bug，但是又不晓得v1.0是不是有这个bug，有了标签就可以顺利切换到v1.0的代码，重新打个包测试了。 所以如果想要新建一个标签很简单，比如 git tag v1.0 就代表我在当前代码状态下新建了一个v1.0的标签，输入 git tag 可以查看历史 tag 记录。 想要切换到某个tag怎么办？也很简单，执行 #######git checkout v1.0 这样就顺利的切换到 v1.0 tag的代码状态了。
