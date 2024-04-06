# Section4-远程仓库

Git 是分布式版本控制系统，同一个 Git 仓库，可以分布到不同的机器上。怎么分布呢？最早，肯定只有一台机器有一个原始版本库，此后，别的机器可以“克隆”这个原始版本库，而且每台机器的版本库其实都是一样的，并没有主次之分。

但是我们不需要搭建服务器，因为这个世界上有个叫 GitHub 的神奇的网站

## 1. 仓库设置

本地 Git 仓库和 GitHub 仓库之间的传输是通过 SSH 加密的，所以，需要一点设置

1. 创建 SSH Key

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

一路回车，使用默认值即可，由于这个 Key 也不是用于军事目的，所以也无需设置密码。

`id_rsa` 和 `id_rsa.pub` 两个文件，这两个就是 SSH Key 的秘钥对，`id_rsa` 是私钥，不能泄露出去，`id_rsa.pub` 是公钥，可以放心地告诉任何人。

2. 登陆 GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意 Title，在 Key 文本框里粘贴 `id_rsa.pub` 文件的内容：

> 为什么 GitHub 需要 SSH Key 呢？因为 GitHub 需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而 Git 支持 SSH 协议，所以，GitHub 只要知道了你的公钥，就可以确认只有你自己才能推送。  
> 当然，GitHub 允许你添加多个 Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的 Key 都添加到 GitHub，就可以在每台电脑上往 GitHub 推送了。  
> 最后友情提示，在 GitHub 上免费托管的 Git 仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。  
> 如果你不想让别人看到 Git 库，有两个办法，一个是交点保护费，让 GitHub 把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个 Git 服务器，因为是你自己的 Git 服务器，所以别人也是看不见的。这个方法我们后面会讲到的，相当简单，公司内部开发必备。

## 2. 添加远程库

1. 在 Github 上 Create a new repo

2. 关联本地仓库
   `$ git remote add origin git@github.com:michaelliao/learngit.git`
   添加后，远程库的名字就是 `origin`，这是 Git 默认的叫法，也可以改成别的，但是 `origin` 这个名字一看就知道是远程库。

3. 把本地库的所有内容推送到远程库上

   ```
   $ git push -u origin master
   ```

   把本地库的内容推送到远程，用 `git push` 命令，实际上是把当前分支 master 推送到远程。

   由于远程库是空的，我们第一次推送 master 分支时，加上了-u 参数，Git 不但会把本地的 master 分支内容推送的远程新的 master 分支，还会把本地的 master 分支和远程的 master 分支关联起来，在以后的推送或者拉取时就可以简化命令。

   现在只要输入

   ```
   $ git push origin master
   ```

   就把本地 master 分支的最新修改推送至 GitHub，现在，你就拥有了真正的分布式版本库！

## 3. SSH 警告

因为 Git 使用 SSH 连接，而 SSH 连接在第一次验证 GitHub 服务器的 Key 时，需要你确认 GitHub 的 Key 的指纹信息是否真的来自 GitHub 的服务器，输入 `yes` 回车即可。

Git 会输出一个警告，告诉你已经把 GitHub 的 Key 添加到本机的一个信任列表里了：

## 4. 删除远程库

如果添加的时候地址写错了，或者就是想删除远程库，可以用 `git remote rm <name>`命令。使用前，建议先用 `git remote -v` 查看远程库信息

此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到 GitHub，在后台页面找到删除按钮再删除。

## 5. 从远程库克隆

1. 首先，登陆 GitHub，创建一个新的仓库

2. 我们勾选 Initialize this repository with a README，这样 GitHub 会自动为我们创建一个`README.md`文件。创建完毕后，可以看到`README.md`文件

3. 现在，远程库已经准备好了，下一步是用命令git clone克隆一个本地库：