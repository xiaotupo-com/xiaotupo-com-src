---
sidebar_position: 4
description: WSL 使用笔记，该比较记录了一些 WSL 相关的命令已经使用注意事项。
---

# WSL 使用笔记

wsl 常用命令：

```bash
wsl -l -v # 查看已经安装的虚拟机
wsl --shutdown # 关闭所有正在运行的虚拟机
# 虚拟机文件导出
wsl --export 虚拟机名称 保存路径
wsl --export Ubuntu D:\\wsl-ubuntu.tar
# 注销原虚拟机
wsl --unregister Ubuntu
wsl --import 虚拟机名称 目标路径 虚拟机文件路径 --version 2
wsl --import Ubuntu D:\\WSL2\\Ubuntu D:\\wsl-Ubuntu.tar --version 2
```
## 默认系统与用户

```bash
PS C:\Users\freer> wslconfig /list
适用于 Linux 的 Windows 子系统分发:
Ubuntu (默认)
Debian
```

设置默认开启的子系统
```bash
PS C:\Users\freer> wslconfig /setdefault Debian
操作成功完成。
```

## 启动&退出 debian 一

```bash
PowerShell 7.3.9
PS C:\Users\freer> debian.exe
zsf@hasee:~$ exit
logout
PS C:\Users\freer>
```