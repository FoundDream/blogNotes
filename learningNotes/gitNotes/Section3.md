# Section3-时光机穿梭

## 1. 查看当前状态

`git status` 可以让我们掌握当前仓库的状态  
`git diff` 可以让我们看看具体如何修改

## 2. 版本回退

当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在 Git 中被称为 commit。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个 commit 恢复，然后继续工作，而不是把几个月的工作成果全部丢失。

`git log`命令显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline` 参数：

> 一大串类似 `1094adb...`的是 `commit id`（版本号），和 SVN 不一样，Git 的 `commit id` 不是 1，2，3……递增的数字，而是一个 SHA1 计算出来的一个非常大的数字，用十六进制表示，而且你看到的 `commit id` 和我的肯定不一样，以你自己的为准。为什么 `commit id` 需要用这么一大串数字表示呢？因为 Git 是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用 1，2，3……作为版本号，那肯定就冲突了。

首先，Git 必须知道当前版本是哪个版本，在 Git 中，用 HEAD 表示当前版本，也就是最新的提交 1094adb...（注意我的提交 ID 和你的肯定不一样），上一个版本就是 HEAD^，上上一个版本就是 HEAD^^，当然往上 100 个版本写 100 个^比较容易数不过来，所以写成 HEAD~100。

现在，我们要把当前版本 回退到上一个版本 ，就可以使用 git reset 命令：
`$ git reset --hard HEAD^`

最新的那个版本 append GPL 已经看不到了！好比你从 21 世纪坐时光穿梭机来到了 19 世纪，想再回去已经回不去了，肿么办？

办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个 append GPL 的 commit id 是 1094adb...，于是就可以指定回到未来的某个版本：

> Git 的版本回退速度非常快，因为 Git 在内部有个指向当前版本的 `HEAD` 指针，当你回退版本的时候，Git 仅仅是把 `HEAD` 从指向 append GPL：

在 Git 中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到上一个版本时，再想恢复到最新版本，就必须找到最新版本的 `commit id`。Git 提供了一个命令 `git reflog` 用来记录你的每一次命令：

## 3. 工作区和暂存区

Git 和其他版本控制系统如 SVN 的一个不同之处就是有暂存区的概念。

### 工作区（Working Directory）

就是你在电脑里能看到的目录

### 版本库（Repository）

工作区有一个隐藏目录.git，这个不算工作区，而是 Git 的版本库。

Git 的版本库里存了很多东西，其中最重要的就是称为 stage（或者叫 index）的暂存区，还有 Git 为我们自动创建的第一个分支 master，以及指向 master 的一个指针叫 HEAD。

![git版本库](../../img/gitNotes/git.jpg)

## 4. 管理修改

如果不放到暂存区，就不会放到版本库

## 5. 撤销修改

1. 修改未添加到缓存区

`git add` 命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行 `git commit` 就可以一次性把暂存区的所有修改提交到分支。

命令`git checkout -- readme.txt` 意思就是，把 `readme.txt` 文件在工作区的修改全部撤销，这里有两种情况：

一种是 `readme.txt` 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是 `readme.txt` 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次 `git commit` 或 `git add` 时的状态。

2. 修改已经添加到缓存区

命令 `git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区

`git reset` 命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用 `HEAD` 时，表示最新的版本。

最后用`git checkout -- readme.txt`删除修改

## 6. 删除文件

一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用 rm 命令删了，现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令 `git rm` 删掉，并且 `git commit`

> 小提示：先手动删除文件，然后使用 git rm <file>和 git add<file>效果是一样的。

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

```git
$ git checkout -- test.txt
```

`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

!> 注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！

## 7. 小结

场景 1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景 2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令 `git reset HEAD <file>`，就回到了场景 1，第二步按场景 1 操作。

场景 3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。