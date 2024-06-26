# Section9-自定义 Git

## 1. 忽略特殊文件

有些时候，你必须把某些文件放到 Git 工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件啦，等等，每次 `git status` 都会显示 `Untracked files ...`，有强迫症的童鞋心里肯定不爽。

好在 Git 考虑到了大家的感受，这个问题解决起来也很简单，在 Git 工作区的根目录下创建一个特殊的`.gitignore` 文件，然后把要忽略的文件名填进去，Git 就会自动忽略这些文件。

忽略文件的原则是：

1.  忽略操作系统自动生成的文件，比如缩略图等；

2.  忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如 Java 编译产生的.class 文件；

3.  忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

如果某些文件已经被屏蔽，你还是想添加，那你可以用`-f` 强制添加

```
$ git add -f App.class
```

或者你发现，可能是`.gitignore` 写得有问题，需要找出来到底哪个规则写错了，可以用 `git check-ignore` 命令检查：

```
$ git check-ignore -v App.class
```

> 把指定文件排除在`.gitignore` 规则外的写法就是`!`+文件名，所以，只需把例外文件添加进去即可。

## 2. 配置别名

有没有经常敲错命令？比如 `git status`？`status` 这个单词真心不好记。

如果敲 `git st` 就表示 `git status` 那就简单多了，当然这种偷懒的办法我们是极力赞成的。

```
$ git config --global alias.st status
```

`--global` 参数是全局参数，也就是这些命令在这台电脑的所有 Git 仓库下都有用。

## 3. 配置文件

配置 Git 的时候，加上`--global` 是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

配置文件放哪了？每个仓库的 Git 配置文件都放在`.git/config` 文件中：

别名就在`[alias]`后面，要删除别名，直接把对应的行删掉即可。

而当前用户的 Git 配置文件放在用户主目录下的一个隐藏文件`.gitconfig` 中：

配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。

## 4. 搭建 Git 服务器

搭建 Git 服务器需要准备一台运行 Linux 的机器，强烈推荐用 Ubuntu 或 Debian，这样，通过几条简单的 `apt` 命令就可以完成安装。

暂时没有这个需求，我也不会使用 Linux，需要的话，直接看[原文章](https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664)吧
