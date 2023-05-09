---
title: Git Bash执行git status中文乱码问题
date: 2023-05-09 10:19:50
category: git
uri: git-bash-git-status-chinese-messy-code
tags: git
---

![截图](/images/20230509103501.png)

```shell
git config --global core.quotepath false
```

此命令用于设置 Git 是否对文件路径中的空格和特殊字符进行转义。

当 `core.quotepath` 配置项被设置为 `true` 时，Git 会对文件路径中的空格、中文和其他特殊字符进行转义，以确保它们在不同的操作系统和终端下都能正常显示。转义后的文件路径会被显示为类似于 `"path\ with\ spaces"` 的形式。

当 `core.quotepath` 配置项被设置为 `false` 时，Git 不会对文件路径进行转义，直接显示文件路径中的空格和特殊字符。这样可以使文件路径更易于阅读，但在某些操作系统和终端下可能会出现显示问题。

当需要查看文件路径时，可以将 `core.quotepath` 配置项设置为 `false`，以便更好地查看文件路径。

如果需要在不同的操作系统和终端下共享代码，可以将 `core.quotepath` 配置项设置为 `true`，以确保文件路径能够正确地显示。


[来源](https://www.zhihu.com/tardis/bd/art/452682481)
