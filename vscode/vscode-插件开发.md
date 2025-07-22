
vscode 插件开发记录

## 安装工具

1、Node.js（推荐 LTS 版本）

2、VS Code

3、Yeoman 和 VS Code Extension Generator



## 打包和发布

安装 vsce 

```sh 
npm i vsce -g

vsce package

vsce create-publisher your-publisher-name
```

发布前要先注册：

首先访问 [https://login.live.com/](https://login.live.com/) 登录你的`Microsoft`账号，没有的先注册一个。

然后访问： [https://aka.ms/SignupAzureDevOps](https://aka.ms/SignupAzureDevOps)



##  第一个 插件，语音转文字

vscode  copilot : 

```sh
这是一个创建笔记文档的 vscode 插件。 实现一个功能，1）可以快速的创建一个文本，md为后缀。 2）在 editor 打开它。

如何 在 package.json 的 commands 部分注册 voice-md-file.createMdNote

创建这个文件要以日期为文件名， md 为后缀， 如：2025-07-20-103012.md

如何通过 触发 Voice: Start Dictation in Editor  用命令 workbench.action.editorDictation.start

如果在 editor 关闭这个文件 ，则同时 触发 Voice: Stop Dictation in Editor 用 命令 workbench.action.editorDictation.stop

问题： 新创建的文件，无法监听到文件关闭事件： onDidCloseTextDocument  不知道为什么

```


##  Trea 安装本地失败

Trea 不支持安装 0.0.1 版本，不知道这么做的原因是什么。
应该是 用了最新的 vscode 做的开发，trea的有一些接口不支持，所以报这了这个错误。 
![vscode-插件开发-20250721172625128.png](./assets/voscovscode%20插件开发-20250721172625128.png)

## 资料

1、https://liiked.github.io/VS-Code-Extension-Doc-ZH/#/

2、https://www.cnblogs.com/jiftle/p/17834177.html

3、https://www.cnblogs.com/liuxianan/p/vscode-plugin-publish.html


4、B站：https://www.bilibili.com/video/BV1BJ8SeMEbp/?spm_id_from=333.337.search-card.all.click&vd_source=6e6fca9271a12c4f326e671c95904150