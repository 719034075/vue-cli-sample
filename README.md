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

# 项目结构

    vue-
        │
        ├─build  项目构建(webpack)相关代码
        │  ├─build.js               生产环境构建代码
        │  ├─check-version.js       检查node、npm等版本
        │  ├─dev-client.js          热重载相关
        │  ├─dev-server.js          构建本地服务器
        │  ├─utils.js               构建工具相关
        │  ├─webpack.base.conf.js   webpack基础配置
        │  ├─webpack.dev.conf.js    webpack开发环境配置
        │  └─webpack.prod.conf.js   webpack生产环境配置
        │
        ├─config  项目开发环境配置
        │  ├─dev.env.js    开发环境变量
        │  ├─index.js      项目一些配置变量
        │  └─prod.env.js   生产环境变量
        │
        ├─src   源码目录
        │  ├─assets         资源目录
        │  ├─common         公共模块
        │  │ ├─constant.js  定义常量
        │  │ ├─http.js      axios封装
        │  │ └─utils.js     常用工具
        │  │
        │  ├─components     vue公共组件
        │  ├─router         路由配置
        │  ├─store          vuex的状态管理
        │  ├─styles         样式文件
        │  ├─App.vue        页面入口文件
        │  └─main.js        程序入口文件，加载各种公共组件
        │
        ├─static       静态文件，比如一些图片，json数据等
        │
        ├─.babelrc            ES6语法编译配置
        │
        ├─.editorconfig       编辑器格式化统一配置
        │
        ├─.eslintignore       eslint需要忽略的文件格式
        │
        ├─.eslintrc.js        eslint-JavaScript规范配置
        │
        ├─.postcssrc.js       postcss配置
        │
        ├─README.md           项目说明
        │
        ├─index.html          入口页面
        │
        ├─package.json        项目基本信息
        │

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


## Step4 配置Vue单元测试（Mocha/Karma + Vue-Test-Utils + Chai）

1. 本地安装karma-chrome-launcher

```cmd
npm install karma-chrome-launcher --save-dev
```

2. 修改karma配置文件

找到`test/unit/karma.conf.js`,把浏览器`PhantomJS`改成`Chrome`。(使用PhantomJS似乎会造成不可预知的错误...)

```js
//karma.conf.js

const webpackConfig = require('../../build/webpack.test.conf');

module.exports = function (config) {
  config.set({
    //browsers: ['PhantomJS'],
    // 修改这里！！！！！
    browsers: ['Chrome'],

    ...
  });
};
```

3. 本地安装Vue-test-utils

```cmd
npm install --save-dev vue-test-utils
```

4. 执行npm run unit

为了确保我们上面几步的顺利，并且我们可以尝试第一次单元测试。在根目录输入

```
npm run unit
```

Vue-cli已经为我们建立了一个`HelloWorld.spec.js`的测试文件
去测试`HelloWrold.vue`
我们可以在`test/unit/specs/HelloWorld.spec.js`下找到这个测试文件。
**(提示: 将来所有的测试文件, 都将放`specs`这个目录下, 并以测试脚本名`.spec.js`结尾命名!)**

然后在终端中出现一大片报告之后，看到下图所示的片段时, 说明本次单元测试通过了。
![](http://onbk0ju0h.bkt.clouddn.com/18-1-17/48549181.jpg)

5. 更多

[Vue单元测试实战教程(Mocha/Karma + Vue-Test-Utils + Chai)](https://www.jianshu.com/p/38a37d5fccb2)

## Step5
