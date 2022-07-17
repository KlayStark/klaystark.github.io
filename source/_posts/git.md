---
title: Git简介
date: 2019-11-15 11:20:14
tags:
---
简介
Git GUI 是一个可视化图形页面；
Git Bash和Git CMD是命令输入窗口；
Git中的Bash是基于CMD的，在CMD的基础上增添一些新的命令与功能。所以建议在使用的时候，用Bash更加方便。

$ mkdir learngit
$ cd learngit
$ pwd

pwd命令用于显示当前目录。

$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/

通过git init命令把这个目录变成Git可以管理的仓库

如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。


第一步，用命令git add告诉Git，把文件添加到仓库：
$ git add readme.txt
执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。
第二步，用命令git commit告诉Git，把文件提交到仓库：
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."


• 要随时掌握工作区的状态，使用git status命令。
• 如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

• HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
• 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
• 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。




Hexo -> markdown

更改主题：theme：

hexo g（g代表generate），生成博客静态文件
每次修改文章后，都需要通过hexo clean清理一下，
然后通过hexo g重新生成，
最后也不要忘了通过hexo s重新启动Hexo。


将需要更换的主题下载并解压缩到theme/yourThemeName目录下，yourThemeName是你给主题取的名字，
如我用的主题是next，只需要解压缩到Hexo/themes/next目录下即可,
当然你也可以直接在Hexo目录下执行git clone https://github.com/theme-next/hexo-theme-next themes/next，
解压完成后，修改_config.yaml文件中的theme属性，默认是landscape，修改为next：