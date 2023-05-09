---
title: WSL2内使用windows上的Clash代理
date: 2023-05-09 17:26:50
category: wsl
uri: wsl2-use-windows-clash-proxy
tags: 
  - wsl
  - clash
---

```shell
export https_proxy=http://host.docker.internal:7890;export http_proxy=http://host.docker.internal:7890;export all_proxy=socks5://host.docker.internal:7890
```

在 WSL 中，需要将 HTTP_PROXY 和 HTTPS_PROXY 环境变量设置为 Windows 系统的本地回环地址和代理端口号。

其中，host.docker.internal 是 Windows 系统的本地回环地址，port 是代理服务器的端口号。

如果希望这些环境变量在每次启动 WSL 时自动设置，可以将上述命令添加到 `.bashrc` 或者 `.zshrc` 文件中。
