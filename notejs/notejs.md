---
tags:
  - front-tech
create: 2024-01-09 14:24
---

# nodejs 

node升级到指定版本


下载 nvm-windows 安装包

1. 下载地址： [nvm-windows 官方 GitHub 仓库](https://github.com/coreybutler/nvm-windows/releases)。
2. 找到最新的版本（如 `nvm-setup.zip`）。
3. 下载 `nvm-setup.zip` 文件并解压，双击运行安装程序。

```shell
nvm version
nvm list available
nvm install <版本号>
nvm use <版本号>
nvm list
nvm uninstall <版本号>
```

安装 pnpm 

```
npm install -g pnpm
pnpm -v
```

 **pnpm 命令详解**

window 下，要管理员权限。 

`pnpm` 是一个高效的 Node.js 包管理工具，与 `npm` 和 `yarn` 类似，但采用了一种独特的硬链接机制，可以节省磁盘空间并提高速度。以下是常用的 `pnpm` 命令及其功能。

```
pnpm install # 安装项目依赖 这会根据 `package.json` 安装所有依赖。

pnpm add <包名> # 安装特定依赖包
pnpm add <包名> -D # 安装开发依赖
pnpm add <包名> --save-dev
pnpm add -g <包名> # 全局安装：

pnpm remove <包名> 删除项目中的某个依赖
pnpm remove -g <包名> 全局删除某个依赖


pnpm run <脚本名> # 运行 `package.json` 中定义的脚本

pnpm run dev 
pnpm dev


pnpm init # 初始化 `package.json` 文件

pnpm store prune  # 清理 pnpm 缓存目录

pnpm list #  查看项目的依赖树
pnpm doctor #  检查项目依赖是否存在问题

pnpm update <包名> # 更新单个依赖
pnpm update #  更新所有依赖

pnpm config set registry https://registry.npmmirror.com  # 设置淘宝镜像以加速依赖安装
```

```
corepack enable
pnpm i
pnpm dev
```

# typeScript

[[typeScript]]

# vite 

[https://cn.vite.dev/guide/](https://cn.vite.dev/guide/)

