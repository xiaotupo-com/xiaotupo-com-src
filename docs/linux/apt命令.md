---
sidebar_position: 2
description: apt 是一个在 Debian和Ubuntu中的Shell前端软件包管理器。
---

`apt` 是一个在 `Debian`和`Ubuntu`中的`Shell`前端软件包管理器。

`apt` 命令提供了查找、安装、升级、删除某一个、一组甚至全部软件包的命令，`apt` 命令需要用超级管理员权限才可以 执行。

## 语法

```bash
apt [options] [command] [package ...]
```

- `options`: 可选，包括` -h` （帮助），`-y` （当安装过程提示选择全部为 "yes"），`-q` （不显示安装的过程）等等。
- `command`: 要进行的操作。
- `package`: 安装的包名。

## 常用命令

- 列出所有可更新的软件清单：`sudo apt update`
- 升级软件包：`sudo apt upgrade`
  - 列出可更新的软件包及版本信息：`apt list --upgradeable`
  - 升级软件包，升级前先删除需要更新的软件包：`sudo apt full-upgrade`
- 安装指定的软件命令：`sudo apt install <package-name>`
- 更新指定的软件：`sudo apt update <package_name>`
- 显示软件包具体信息，例如：版本号，安装大小，依赖关系等等：`sudo apt show <package_name>`
- 删除软件包命令：`sudo apt remove <package_name>`
- 清理不再使用的依赖和库文件：`sudo apt autoremove`
- 移除软件包及配置文件：`sudo apt purge <package_name>`
- 查找软件包：`sudo apt search <keyword>`
- 列出所有已安装的包：`apt list --installed`
- 列出所有已安装的包的版本信息：`apt list --all-versions`

## 安装软件已存在不升级：--no-upgrade

```bash
sudo apt install <package_name> --no-upgrade
```



## 只升级，不更新

```bash
sudo apt install <package_name> --only-upgrade
```

