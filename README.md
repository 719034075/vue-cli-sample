# vue-cli-sample

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

# 简介

这个一个我自己手动搭建的多环境`vue-cli`。里面包含了以下内容：

+ linter工具：ESLinter
+ 多编辑器编码统一：EditorConfig

需要环境：

+ node.js
+ 浏览器

IDE：

+ webstorm

考虑到网络问题，下面涉及到`npm`安装的内容的，可以用`cnpm`替换。速度可能会更快。


# 搭建步骤

## Step1 用vue-cli自动建立项目

1. 全局安装`vue-cli`

```cmd
npm install -g vue-cli
```

2. 在目标位置运行

```cmd
# projectname 换成你要的项目名字
vue init webpack projectname
```

会让你回答一些问题
```cmd
//项目名，可以直接回车
? Project name vue-cli-sample
//项目描述，可以直接回车

? Project description A Vue.js project

//项目作者，可以直接回车
? Author zeuc

//Vue构建，既然已经说了推荐，就选第一个了
? Vue build (Use arrow keys)
> Runtime + Compiler: recommended for most users
  Runtime-only: about 6KB lighter min+gzip, but templates (or any Vue-specific HTML) are ONLY allowed in .vue files - render functions are required elsewhere

// 选y
? Install vue-router? (Y/n)

// 是否使用ESLint，我选y，不想用的选n
? Use ESLint to lint your code? (Y/n)

// 我选择业界比较严格的Airbnb
? Pick an ESLint preset (Use arrow keys)
  Standard (https://github.com/standard/standard)
> Airbnb (https://github.com/airbnb/javascript)
  none (configure it yourself)

// 是否建立单元测试，我选y
? Set up unit tests (Y/n)

// 选择单元测试框架，我选第二个
? Pick a test runner
  Jest
> Karma and Mocha
  none (configure it yourself)

// 是否安装e2e测试 ，我选择y
? Setup e2e tests with Nightwatch(Y/n)?

// 我选择第三项，一会儿自己安装
? Should we run `npm install` for you after the project has been created? (recommended)
  Yes, use NPM
  Yes, use Yarn
> No, I will handle that myself
```

回答完之后会看到

```cmd
   vue-cli · Generated "vue-cli-sample".

# Project initialization finished!
# ========================

To get started:

  cd vue-cli-sample
  npm install (or if using yarn: yarn)
  npm run lint -- --fix (or for yarn: yarn run lint --fix)
  npm run dev

Documentation can be found at https://vuejs-templates.github.io/webpack
```

进入项目目录，下载相关的依赖包

```cmd
npm install
```

## Step2 配置EditorConfig（不需要的话可以跳过）

webstorm配置EditorConfig

1. `ctrl+alt+s`打开设置。
2. `editor>code style`下面有一个`Enable EditorConfig support`选中前面的复选框，启动支持。
3. 后面有个`export`按钮是用来导出当前IDE的`.editorconfig`配置文件,不过`vue-cli`自带这个文件了。

之后就可以根据自己的需求来配置`.editorconfig`配置文件。
`ctrl+alt+L`根据你的配置格式化当前文件。

## Step3 配置Linter（不需要的话可以跳过）

我使用的是业内比较严格的`Airbnb`标准。

在webstorm中配置

`Ctrl+alt+S`打开设置。
`Languages&Frameworks->JavaScript->Code Quality Tools->ESLint`
把`Enable`复选框勾中即可。

之后就可以根据自己的需求配置`.eslintrc`文件


## Step3

