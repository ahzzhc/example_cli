# node 脚手架开发小记

## 脚手架开发流程

1. 脚手架创建（npm init）
2. 脚手架开发（分包，命令注册，参数解析，帮助文档）
3. 脚手架本地调试（npm link）

```
// 链接本地脚手架
cd your-cli-dir
npm link
// 链接本地库文件
cd your-lib-dir
npm link
cd your-cli-dir
npm link your-lib
// 取消链接本地库文件
cd your-lib-dir
npm unlink
cd your-cli-dir
npm unlink your-lib
rm -rf node_modules
npm install
// npm link your-lib:将当前项目中node_modules下指定的库文件链接到node全局node_modules下的库文件
// npm link:将当前项目链接到node全局node_modules中作为一个库文件，并解析bin配置创建可执行文件
// npm unlink:将当前项目从node全局node_modules中移除
// npm unlink your-lib:将当前项目中的库文件移除
```

4. 脚手架发布（npm publish）

## chalk(命令行 UI)

解决问题：

1. ansi 转移字符如何汇总和定义
2. 特殊字符如\n、\u001b 如何处理
3. 如何解决链式调用

源码要点：

1. 自定义 imports 引用(#)
2. 通过构造者模式 createBuilder 批量生成方法
3. 通过工厂模式生成 chalk 实例
4. 原型上方法的挂载和替换

## ora(loadingUI)

源码要点：

1. class 私有属性(#)
2. BufferListStream 输入流缓冲
3. 命令行光标的显示与隐藏
4. 命令行清屏操作

## inquirer(命令行交互)

## 多 package 项目管理

workspace：

```
// 创建项目 npm init -w a
// 项目创建后，会在项目顶级目录下创建node_modules并存储所有package的依赖
// 为某个特定的workspace安装依赖(npm install ** -w a)
// 更新所有依赖(npm install -ws)
```

lerna 执行流程:  
判断本地是否存在 lerna->

1. 有本地版本，加载本地 lerna/cli.js
2. 无本地版本，加载 lerna/index.js -> 初始化 yargs -> 执行 command builder -> 执行 command handler -> 执行 command constructor -> 执行 runCommand -> 执行 initialize -> 执行 execute

## 项目搭建

1. 脚手架 1-创建项目模板(从 npm 仓库下载)
2. 脚手架 2-前端仓库下载（从 github/gitee 下载）
3. 脚手架 3-eslint/jest 自动化
4. 教授架 4-代码自动提交仓库
