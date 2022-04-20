### 背景
Linux 是一种自由和开放源码的类 UNIX 操作系统。

Linux 英文解释为 `Linux is not Unix`。

Linux 是在 1991 由林纳斯·托瓦兹在赫尔辛基大学上学时创立的，主要受到 Minix 和 Unix 思想的启发。

本教程将为大家介绍常用Linux命令。

### Linux下的文件系统

在Linux下**没有**盘符的概念, 只有一个根目录`/`，所有文件都在根目录下（如下图）
![root](../img/linux/pre/1.png)
以下仅介绍常见目录：
+ `/bin`: bin 是 Binaries (二进制文件) 的缩写, 这个目录存放着最经常使用的命令。
+ `/home`: 用户的主目录，在 Linux 中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的，如上图中的 alice、bob 和 eve。
+ `/etc`: etc 是 Etcetera(等等) 的缩写,这个目录用来存放所有的系统管理所需要的配置文件和子目录。
+ `/root`: 该目录为系统管理员，也称作超级权限者的用户主目录。
+ `/opt`: 一般软件可存放在此目录下便于管理。

了解了根目录，接下来介绍**绝对路径与相对路径**

**绝对路径**： 最前面是 `/` 或者 `~`

+ `/` 表示从根目录开始
+ `~` 表示从家目录开始
> 例如： `/home/ljjtpcn/Desktop` 等价于 `~/ljjtpcn/Desktop`

**相对路径**： 最前面不是 `/` 和 `~`

+ `./`表示当前目录，通常可省略不写
+ `../`表示当前目录的上一级目录

### 终端命令格式

`命令 [-选项] [参数]`

#### 命令

终端命令格式中的` [] `代表可选项，也就是有些命令可以不写选项或参数，也能执行。那么，我们就用 Linux 中最常见的 `ls` 命令来解释一下命令的格式。如果按照命令的分类，那么 `ls` 命令应该属于目录操作命令。

```bash
➜  ~ ls   
 aiXcoder           Documents                    Music                     sensors   'udo apt-get autoclean'
 DataGripProjects   Downloads                    node-v16.14.2-linux-x64   software   Videos
 Desktop            install_uget_integrator.sh   Pictures                  tools      work-space
```

#### 选项

`ls` 命令之后不加选项和参数也能执行，不过只能执行最基本的功能，即显示当前目录下的文件名。那么加入一个选项`-a`，会出现什么结果？

```bash
➜  ~ ls -a
 .                    Documents                    node-v16.14.2-linux-x64   .themes
 ..                   Downloads                    .npm                      tools
 aiXcoder             .gconf                       .oh-my-zsh               'udo apt-get autoclean'
 .android             .gnupg                       .persepolis               Videos
 .avfs                .gtkrc-2.0                   Pictures                  .viminfo
 .bash_history        .gvfs                        .pki                      .vimrc
 .bash_logout         .icons                       .presage                  .vscode
 .bashrc              .imwheelrc                   .profile                  .wallaby
 .cache               install_uget_integrator.sh   .psensor                  .wget-hsts
 .cf                  .java                        .Public                   work-space
 .clipboard-pix       .jdks                        .python_history           .Xauthority
 .codota-id           .kchmviewer                  .quokka                   .xinputrc
 .config              .kde                         sensors                   .xsession-errors
 DataGripProjects     .lesshst                     .shell.pre-oh-my-zsh      .xsession-errors.old
 .dbus                .local                       software                  .zcompdump-count-5.7.1
 .deepin-calculator   .m2                          .sogouinput               .zsh_history
 .deepinwine          .mozilla                     .ssh                      .zshrc
 Desktop              Music                        .tabnine                  .zshrc.orig
 .dmrc                .mysql_history               .Templates
```

可以看到显示的内容明显增加了， `-a`的具体含义就是显示所有（包括隐藏）文件。 因为`ls`默认不会显示隐藏文件，所有可用`-a`查看隐藏文件。

> Linux 的选项又分为短格式选项（`-a`）和长格式选项（`--all`）。短格式选项是英文的简写，用一个减号调用,而长格式选项是英文完整单词，一般用两个减号调用。两种格式任选其一即可。
>
> 一般情况下，短格式选项是长格式选项的缩写，也就是一个短格式选项会有对应的长格式选项。当然也有例外，比如 `ls` 命令的短格式选项 `-l` 就没有对应的长格式选项。所以具体的命令选项可以通过帮助命令或者搜索引擎来进行査询。

#### 参数

参数是命令的操作对象，一般文件、目录、用户和进程等可以作为参数被命令操作。**可以为0、1或多个**。如:

```bash
➜  ~ touch test.txt     #在家目录创建test.txt文件
➜  ~ rm test.txt     #删除家目录下的test.txt文件
```

#### 查阅帮助命令

两种方式查询命令对应选项和格式：

1. `command --help` 固定选项显示命令的帮助信息

```bash
➜  ~ ls --help
用法：ls [选项]... [文件]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

必选参数对长短选项同时适用。
  -a, --all                     不隐藏任何以. 开始的项目
  -A, --almost-all              列出除. 及.. 以外的任何项目
      --author                  与-l 同时使用时列出每个文件的作者
  -b, --escape                  以八进制溢出序列表示不可打印的字符
      --block-size=SIZE      with -l, scale sizes by SIZE when printing them;
                               e.g., '--block-size=M'; see SIZE format below
  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                               modification of file status information)
.....................帮助信息太多了放不下，可自己动手实操一下
```

2. `man command`  (man是manual的缩写)，查阅命令手册

```bash
➜  ~ man ls
LS(1)                                              User Commands                                              LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List information about the FILEs (the current directory by default).  Sort entries alphabetically if none of
       -cftuvSUX nor --sort is specified.

       Mandatory arguments to long options are mandatory for short options too.

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..

       --author
              with -l, print the author of each file

       -b, --escape
              print C-style escapes for nongraphic characters

       --block-size=SIZE
Manual page ls(1) line 1 (press h for help or q to quit)
```

> `man`命令使用时的操作键：
>
> `空格`或`f`：显示下一屏
>
> `Enter`：向前滚动一行
>
> `b`：回滚一屏
>
> `q`：退出