---
layout: post
title: “Vim切换Normal模式变慢”问题解决
date: 2017-11-14 23:02:11.000000000 +09:00
tags: Vim
---

#### 问题

准备把 Vim 用起来，今天在装 YouCompleteMe 插件。插件还没装好，反倒遇到了其他的问题：Vim 由 Insert 模式切换为 Normal 模式时，产生了明显的延迟感。急忙去 Google 和 Baidu 查询解决方法，结果半天都没搜出几个结果。

#### 解决
最后把关键词改为英文搜索，才得救！
在 `.vimrc` 文件中增加一行配置如下：
```bash
set timeoutlen=1000 ttimeoutlen=0
```

参考资料：
- [Eliminating delays on ESC in vim and zsh](https://www.johnhawthorn.com/2012/09/vi-escape-delays/)
- [Delay when switching insert mode to normal mode](https://github.com/vim-airline/vim-airline/issues/124)
