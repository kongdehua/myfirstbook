# 跟随Typescript的轮子制造者
## 前言
  前端这些年发展非常迅速，社区里涌现了一堆优秀的轮子，比如:Vue、React、 Angular、jQuery、axios等。它们解决着不同领域下的问题。使用这些轮子能够
极大地帮助我们提升生产力，有些人甚至基于这些轮子二次开发了一些轮子，比
如element-ui、ant-design等组件库。我们在享受这些轮子给我们带来便利的时
候，有时候也需要面临一些问题，某些轮子不能满足我们的特殊业务需求，找不
到合适的轮子等。因此我们不仅需要会使用轮子，也需要有造轮子的实力。

  2019年前端技术发展越来越迅速，其中Typescript更是受到越来越多的开发者
的青睐，在GitHub上搜索`star 数大于 1w`的项目，我们可以看到很多知名的开
源项目如vscode、angular、ant-design、ionic、deno等都使用TypeScript开发
。19年上升最快的Vue.js 3.0也正在用TypeScript重构，尤大神都忍不住发出了
”真香“的言论。

  TypeScript的火爆程度夸张，大有成为下一代前端开发语言的趋势，TypeScript
作为JavaScript语言的超集。它为JavaScript添加了可选择的类型标注大大增强
了代码的可读性和可维护性。同时它提供最新的和不断发展的JavaScript特性能
让我们建立更健壮的组件。

  越来越多的轮子将用TypeScript开发和重构，我们如果想造轮子也应该使用TypeScript
这把利器。

## 如何开始
  我们造轮子首先会初始化一个项目，但需要配置一大堆东西，比如`package.json`、
`.editorconfig`、`package.json`等，还包括一些构建工具，如`rollup`、`webpack` 
以及它们的配置。

  当我们使用TypeScript去写一个项目的时候，还需要配置TypeScript的编译配置
文件`tsconfig.json`以及`tslin.json`文件。

  这些茫茫多的配置往往会让一个想从零开始写项目的同学望而却步，如果有一个
脚手架帮我们生成这些初始化文件多好。确实已经有这样的工具，主角`TypeScript 
library starter`登场。

## TypeScript library starter
  它是一个开源的TypeScript开发基础库的脚手架工具，可以帮助我们快速初始化
一个TypeScript项目，我们可以去它的官网学习和使用它。

### 使用方式

```
  git clone https://github.com/alexjoverm/typescript-library-starter.git 
ts-axioscd ts-axios
  npm install
```

  先通过 `git clone` 把项目代码拉下来到我们的`ts-axios`目录然后运行`npm 
install`安装依赖，并且给项目命名，仍然使用`ts-axios`。

  安装好依赖后我们先来预览一下这个项目的目录结构：

```
  |--- CONTRIBUTING.md
  |             |--- README.md
  |
  |--- LINCENSE
  |--- code-of-conduct.md
  |--- node_modules
  |--- package-lock.json
  |--- package.json
  |--- rollup.config.js    // rollup 配置文件
  |--- src                 // 源码目录
  |--- test                // 测试目录
  |--- tools               // 发布到GitHub pages以及发布到npm的一些配置脚本工具
  |--- tsconfig.json       // TypeScript编译配置文件
  |--- tslint.json         // TypeScript lint文件
  |

```

### 优秀工具集成
使用TypeScript library starter创建的项目集成了很多优秀的开源工具

* 使用 `RoolupJS` 帮助我们打包；
* 使用 `Prettier` 和 `TSLint` 帮助我们格式化代码以及保证代码风格一致性；
* 使用 `TypeDoc` 帮助我们自动生成文档，并部署到GitHub Pages。
* 使用 `Jest` 帮助我们做单元测试；
* 使用 `Commitizen` 帮助我们生成规范化的提交注释；
* 使用 `Semantic release` 帮助我们管理版本和发布；
* 使用 `husky` 帮助我们更简单地使用git hooks；
* 使用 `Conventional changelog` 帮助我们通过代码提交信息，自动生成change log。

工欲善其事、必先利其器，我们现在已经搭好了一个项目的雏形，接下来就要开始编写轮子的代码了。

## 轮子的设计
一般轮子的特点专注于做某一块事情，为了更直观和具体。我们以一个非常知名的前端开源库axios为例，站在轮子制造者的角度上，来讨论一个优秀的轮子是如何设计出来的。

### 核心功能
axios核心专注于发送http请求，并且在此基础上扩展了很多使用的和好用的feature。如下：

* 在浏览器端使用 XMLHttpRequest 对象通讯
* 在 Node.js 端使用 http request 通讯
* 支持 Promise API
* 支持请求和相应的拦截器
* 支持请求数据和响应数据的转换
* 支持请求的取消
* JSON 数据的自动转换
* 客户端防止 XSRF

对于轮子的使用者，这些feature能让我们知道轮子是做什么的，而对于轮子的制造者，这些feature就是我们的需求。对于这些需求，我们可以划分优先级，优先实现在浏览器端的请求发送逻辑，实现一些基础功能，如请求发送、响应Promise API请求数据、响应数据的转换、JSON数据自动转换、一些异常情况处理，接着再去扩展拦截器、配置化、请求取消等复杂功能，然后扩展一些简单的功能：客户端防止XSRF、上传等，最后开发axios在Node.js端的扩展。

我们的编码思路也就是按优先级的重要程度依次去开发上述功能。

### 接口设计
一个轮子是否优秀取决于它是否好用、使用是否方便。五六年前还是jQuery的时代，jQuery就提供了一个非常好用的$设计抢占了大部分市场。当年百度也出了一个类似的库叫tangram，创建一个DOM对象需要写 `Baidu.T.createDOM(xxx)`，而jQuery只需要`$(xxx)`，高下立判。

axios设计也是非常简单直接，`axios(config)` 就可以完成一个请求的发送。为了减少config中的配置参数，还提供了axios.get、axios.post等接口。为了方便用户拿到相应结果，axios支持了Promise API，我们可以通过 axios(config).then(res=>{}) 的方式拿到响应对象。

axios可以支持非常多的feature，完全得益于config配置参数，对于feature的扩展，我们既可以通过扩展axios的实例或者静态方法来实现，也可以扩展config的字段来实现，原则是怎么方便用户使用怎么来。

### 生命周期
axios本质上就是发送一个请求，拿到响应结果，中途可以去对处理配置参数、请求数据、响应数据，同时也支持一些拦截器的调用，因此我们可以画出它的生命周期。

```
  axios(config)
       |
       |
      \|/
    配置合并
       |
       |
      \|/
  请求拦截器
       |
       |
      \|/
  处理请求数据
       |
       |
      \|/
 是否浏览器环境 --------> http request
       |           N          | 
      Y|                      |       
       |                      |       
      \|/                     |        
      xhr                     |        
       |                      |       
       |                      |       
      \|/                     |        
  处理响应数据  <-------------|             
       |
       |
      \|/
  响应拦截器
       |
       |
      \|/
   拿到响应对象

```

## 轮子开发
axios既是一个函数，又是一个接口，是一个实例对象也拥有一些静态方法。如果我们使用TypeScript开发，
* 该如何设计axios的类型，
* 另外axios对外提供的非常多的API接口、配置参数，
* 我们又该如何使用TypeScript定义这些类型呢，
* 根据生命周期图示，我们可以按照流程中的行为去拆分功能模块，
* 我们如何使用TypeScript做模块拆分和管理的，
* 哪些模块又可以被抽成基础公共模块，
* 在实现整个axios库的过程中如何不断地做代码的优化、抽象和封装，
* 如何使用策略模式实现配置合并，
* 拦截器的Promise链如何设计，
* 如何通过异步分离实现取消功能。

## 单元测试
一个优秀的轮子一定会有单元测试，单元测试是轮子的质量保证，甚至还有测试驱动开发的开发模式。很多同学对单元测试一直处于一种听说过但没用过的状态。其实写单元测试并不难，首先我们要保证feature的测试完整性，保证每个feature的各种情况都能监测到。一个检测测试完整性的常用手段是看测试的覆盖率，通常会我们会要求测试覆盖率达到90%以上。

单元测试有一个非常大的好处是，你可以放心地对你现有的代码做新feature的开发，以及代码的重构，而不用担心代码的改动影响已有功能，我们可以很容易地通过跑单元测试检测我们改动的代码是否有问题。

目前前端测试的框架有很多。比较推荐Jest，它是一个几乎零配置的测试框架，非常易于上手，由facebook团队维护，质量也能得到保证。

## 总结
TypeScript在类型方面的约束，以及提供很多好用的现代JavaScript语法特性，非常适合用它去造一个轮子，当然也非常适合开发大型复杂前端项目。前端的趋势会越来越复杂，TypeScript这个技术栈在未来一定会编程前端必须掌握的开发技能。

至于造轮子能不能设计好用的轮子，轮子能不能满足复杂的需求，对你的JavaScript内功、代码设计能力都是由很高的要求。造轮子的过程就是一个内功修炼的过程。所以如果你不满足于做一个熟练工、一个螺丝钉，想提升自己的核心竞争力，那么从今天开始拿起TypeScript做一个轮子的制造者。
