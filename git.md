## Git是什么？

Git是目前世界上最先进的分布式版本控制系统（没有之一）。

Git有什么特点？简单来说就是：高端大气上档次！

那什么是版本控制系统？

如果你用Microsoft Word写过长篇大论，那你一定有这样的经历：

想删除一个段落，又怕将来想恢复找不回来怎么办？有办法，先把当前文件“另存为……”一个新的Word文件，再接着改，改到一定程度，再“另存为……”一个新文件，这样一直改下去，最后你的Word文档已经堆积如山

过了一周，你想找回被删除的文字，但是已经记不清删除前保存在哪个文件里了，只好一个一个文件去找，真麻烦。

看着一堆乱七八糟的文件，想保留最新的一个，然后把其他的删掉，又怕哪天会用上，还不敢删，真郁闷。

更要命的是，有些部分需要你的财务同事帮助填写，于是你把文件Copy到U盘里给他（也可能通过Email发送一份给他），然后，你继续修改Word文件。一天后，同事再把Word文件传给你，此时，你必须想想，发给她之后到你收到她的文件期间，你作了哪些改动，得把你的改动和他的部分合并，真困难。

于是你想，如果有一个软件，不但能自动帮我记录每次文件的改动，还可以让同事协作编辑，这样就不用自己管理一堆类似的文件了，也不需要把文件传来传去。如果想查看某次改动，只需要在软件里瞄一眼就可以，岂不是很方便？

这个软件用起来就应该像这个样子，能记录每次文件的改动：
![](https://hexoljj.oss-cn-shenzhen.aliyuncs.com/img/202112032012541.png)
![](https://hexoljj.oss-cn-shenzhen.aliyuncs.com/img/202112032013107.png)
这样，你就结束了手动管理多个"版本"的史前时代，进入到版本控制的21世纪。

!> [廖雪峰的官方网站](https://www.liaoxuefeng.com/)

---


## Git 应用

!> Git的安装略过


下面是将本地仓库推送到远端代码托管平台(例如`Coding`)的示例:

```bash
git init   #初始化一个仓库
git add .   #添加所有文件到暂存区（先交给git管着）
git commit -m "fuck"  #提交到git仓库，-m后面是注释
git remote add origin https://e.coding.net/tpcn/wiki/wiki.git  #网址要根据情况变化
git push -u origin master  #推送到远程仓库
```

?> 这时，本地仓库应该就同步到Coding上面了

---

!> 如果我创建了一个项目，然后通过下面的命令 push 到了 coding 上。

```bash
git remote add coding  git@e.coding.net:tpcn/wiki/wiki.git
git push -u coding master
```

如何再将这个项目 push 到其他远程仓库呢？

**使用 git remote add 命令**
1. 如下命令查看远程仓库的情况，可以看到只有一个叫 coding 的远程仓库。

```bash
git remote -v
```

![git1](https://hexoljj.oss-cn-shenzhen.aliyuncs.com/img/202112041351451.jpg)

2. 使用如下命令再添加一个远程仓库（这里以github为例）

```bash
git remote add github https://[token]ngithub.com/ljjtpcn/docsify-demo.git
```

![git2](https://hexoljj.oss-cn-shenzhen.aliyuncs.com/img/202112041355516.png)

3. 再次查看远程仓库的情况，可以看到已经有两个远程仓库了。然后再使用相应的命令 push 到对应的仓库就行了。

4. 删除方法:
```bash
git remote rm github #表示删除github的远程仓库
```


在使用Git的过程中，有些时候我们只想要git服务器中的最新版本的项目，对于本地的项目中修改不做任何理会，就需要用到Git pull的强制覆盖，具体代码如下：

```bash
$ git fetch --all
$ git reset --hard main/main 
$ git pull
```