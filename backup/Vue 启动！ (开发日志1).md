## 前言
3月16日

开完了会议，确定好了方向，我需要提供的是控制打印机的代码，还有监控程序...

哦对了，还有渲染视频



本人开发方向主要偏向后端，前端写的依托答辩

于是...开启了vue的学习之旅...

为什么不学react呢...来不及了啊喂!!!



## Vue 启动！
### 速读开发文档
let me see see开发文档

[https://cn.vuejs.org/guide/quick-start](https://cn.vuejs.org/guide/quick-start)



文档中提到了，可以通过script标签引入vue，这太棒了，这意味我能省很多测试时间，甚至不用搭建专门的测试环境

```php
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

> 注意:
>
> <font style="color:rgb(33, 53, 71);">“这里我们使用了 </font>[unpkg](https://unpkg.com/)<font style="color:rgb(33, 53, 71);">，但你也可以使用任何提供 npm 包服务的 CDN，例如 </font>[jsdelivr](https://www.jsdelivr.com/package/npm/vue)<font style="color:rgb(33, 53, 71);"> 或 </font>[cdnjs](https://cdnjs.com/libraries/vue)<font style="color:rgb(33, 53, 71);">。当然，你也可以下载此文件并自行提供服务。</font>
>
> <font style="color:rgb(33, 53, 71);">通过 CDN 使用 Vue 时，不涉及“构建步骤”。这使得设置更加简单，并且可以用于增强静态的 HTML 或与后端框架集成。但是，你将无法使用单文件组件 (SFC) 语法。”</font>
>



##### 一些基本的操作
安装好node.js 创建vue项目

```php
npm create vue@latest
```

嗯...看起来是个脚手架

```php
✔ Project name: … <your-project-name>
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add an End-to-End Testing Solution? … No / Cypress / Nightwatch / Playwright
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formatting? … No / Yes
✔ Add Vue DevTools 7 extension for debugging? (experimental) … No / Yes

Scaffolding project in ./<your-project-name>...
Done.
```

> <font style="color:rgb(33, 53, 71);">“如果不确定是否要开启某个功能，你可以直接按下回车键选择 </font>`No`<font style="color:rgb(33, 53, 71);">。”</font>
>

<font style="color:rgb(33, 53, 71);"></font>

> 运行dev
>

```php
cd <your-project-name>
npm install
npm run dev
```

> 发布
>

```php
npm run build
```



## <font style="color:rgb(33, 53, 71);">通过 CDN 使用 Vue</font>
上文也提到了可以直接使用script标签引入Vue框架，现在来看看

```php
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

### <font style="color:rgb(33, 53, 71);">使用全局构建版本</font>
```php
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">{{ message }}</div>

<script>
  const { createApp, ref } = Vue

  createApp({
    setup() {
      const message = ref('Hello vue!')
      return {
        message
      }
    }
  }).mount('#app')
</script>
```

### <font style="color:rgb(33, 53, 71);">使用 ES 模块构建版本</font>
```php
<div id="app">{{ message }}</div>

<script type="module">
  import { createApp, ref } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'

  createApp({
    setup() {
      const message = ref('Hello Vue!')
      return {
        message
      }
    }
  }).mount('#app')
</script>
```

> ##### 需要注意
> <font style="color:rgb(33, 53, 71);">如果直接在浏览器中打开了上面的</font><font style="color:rgb(33, 53, 71);"> </font>`index.html`<font style="color:rgb(33, 53, 71);">，你会发现它抛出了一个错误，因为 ES 模块不能通过</font><font style="color:rgb(33, 53, 71);"> </font>`file://`<font style="color:rgb(33, 53, 71);"> </font><font style="color:rgb(33, 53, 71);">协议工作，也即是当你打开一个本地文件时浏览器使用的协议。</font>
>
> <font style="color:rgb(33, 53, 71);">由于安全原因，ES 模块只能通过 </font>`http://`<font style="color:rgb(33, 53, 71);"> 协议工作，也即是浏览器在打开网页时使用的协议。为了使 ES 模块在我们的本地机器上工作，我们需要使用本地的 HTTP 服务器，通过 </font>`http://`<font style="color:rgb(33, 53, 71);"> 协议来提供 </font>`index.html`<font style="color:rgb(33, 53, 71);">。</font>
>

<font style="color:rgb(33, 53, 71);"></font>

##### 二者的区别
###### 使用全局构建版本
+ **引入方式**：通过 `<script>` 标签直接引入 `vue.global.js` 文件。
+ **使用特点**：
    - 所有顶层 API 都挂在全局对象 `Vue` 上，可以直接通过 `Vue` 访问和使用。
    - 示例：

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<div id="app">{{ message }}</div>
<script>
  const { createApp, ref } = Vue;
  createApp({
    setup() {
      const message = ref('Hello vue!');
      return { message };
    }
  }).mount('#app');
</script>
```

+ **优点**：简单直接，无需额外配置，适合快速上手和小型项目。
+ **缺点**：无法使用单文件组件（SFC）语法，代码组织和复用性受限。

###### 使用 ES 模块构建版本
+ **引入方式**：通过 `<script type="module">` 标签，并使用 `import` 语句引入 `vue.esm-browser.js` 文件。
+ **使用特点**：
    - 使用 ES 模块语法，支持现代 JavaScript 的模块化开发。
    - 示例：

```html
<div id="app">{{ message }}</div>
<script type="module">
  import { createApp, ref } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js';
  createApp({
    setup() {
      const message = ref('Hello Vue!');
      return { message };
    }
  }).mount('#app');
</script>
```

+ **优点**：支持更灵活的模块化开发，可以结合构建工具使用，适合大型项目。
+ **缺点**：需要浏览器支持 ES 模块，且代码结构相对复杂。



> 现在项目时间这么赶　仕方がないなぁ
>
> 似乎只能选全局构建了呢
>



##### 题外
嗯...有点没看懂，滚回去翻简介了

真的，在开始项目之前真心建议好好看看简介

[https://cn.vuejs.org/guide/introduction](https://cn.vuejs.org/guide/introduction)

嗯...

我看到了什么声明式开发，组件，这让我想起了Spring

> ###### <font style="color:rgb(6, 6, 7);">1. 声明式开发</font>
> + **<font style="color:rgb(6, 6, 7);">Java SSM 框架</font>**<font style="color:rgb(6, 6, 7);">：在 Java 的 SSM 框架（Spring、Spring MVC、MyBatis）中，开发人员通过配置文件（如 XML）或注解来声明组件的行为和关系。例如，在 Spring 中，可以通过 </font>`@Controller`<font style="color:rgb(6, 6, 7);">、</font>`@Service`<font style="color:rgb(6, 6, 7);">、</font>`@Repository`<font style="color:rgb(6, 6, 7);"> 等注解来声明不同层次的组件。</font>
> + **<font style="color:rgb(6, 6, 7);">Vue</font>**<font style="color:rgb(6, 6, 7);">：在 Vue 中，通过模板语法（如 </font>`{{ }}`<font style="color:rgb(6, 6, 7);">）和组件选项（如 </font>`data`<font style="color:rgb(6, 6, 7);">、</font>`methods`<font style="color:rgb(6, 6, 7);">）来声明界面和数据的关系。这种声明式的方式使得开发更加直观和高效。</font>
>
> ###### <font style="color:rgb(6, 6, 7);">2. 组件化开发</font>
> + **<font style="color:rgb(6, 6, 7);">Java SSM 框架</font>**<font style="color:rgb(6, 6, 7);">：在 SSM 框架中，可以将应用分解为多个模块，每个模块负责不同的功能。例如，Spring 的 IoC 容器管理着各个 Bean 的生命周期和依赖关系，实现了模块间的松耦合。</font>
> + **<font style="color:rgb(6, 6, 7);">Vue</font>**<font style="color:rgb(6, 6, 7);">：Vue 的组件化开发允许将界面分解为独立的组件，每个组件有自己的模板、逻辑和样式。这与 SSM 框架中的模块化开发思想相似，都强调代码的复用性和可维护性。</font>
>
> ###### <font style="color:rgb(6, 6, 7);">3. 配置与约定</font>
> + **<font style="color:rgb(6, 6, 7);">Java SSM 框架</font>**<font style="color:rgb(6, 6, 7);">：SSM 框架通过配置文件或注解来定义应用的行为，同时也遵循一定的约定（如 Spring 的自动配置）。这使得开发更加灵活，同时减少了样板代码的编写。</font>
> + **<font style="color:rgb(6, 6, 7);">Vue</font>**<font style="color:rgb(6, 6, 7);">：Vue 也提供了一些约定，如组件的命名规则、选项的定义等。同时，Vue 的配置文件（如 </font>`vue.config.js`<font style="color:rgb(6, 6, 7);">）允许开发者根据需要进行定制化配置。</font>
>

<font style="color:rgb(6, 6, 7);">看起来有些相似...很好，这让我对接下来的工作充满信心</font>

<font style="color:rgb(6, 6, 7);"></font>

<font style="color:rgb(6, 6, 7);">单文件组件：“</font><font style="color:rgb(33, 53, 71);">在大多数启用了构建工具的 Vue 项目中，我们可以使用一种类似 HTML 格式的文件来书写 Vue 组件，它被称为</font>**<font style="color:rgb(33, 53, 71);">单文件组件</font>**<font style="color:rgb(33, 53, 71);"> (也被称为 </font>`*.vue`<font style="color:rgb(33, 53, 71);"> 文件，英文 Single-File Components，缩写为 </font>**<font style="color:rgb(33, 53, 71);">SFC</font>**<font style="color:rgb(33, 53, 71);">)。顾名思义，Vue 的单文件组件会将一个组件的逻辑 (JavaScript)，模板 (HTML) 和样式 (CSS) 封装在同一个文件里。下面我们将用单文件组件的格式重写上面的计数器示例：</font><font style="color:rgb(6, 6, 7);">”</font>

> 这看起来就是把前端三大件封装在了一起
>



##### Vue的两种Api风格
###### <font style="color:rgb(6, 6, 7);">选项式 API 与组合式 API</font>
<font style="color:rgb(6, 6, 7);">Vue 提供了两种主要的 API 风格来书写组件逻辑：选项式 API（Options API）和组合式 API（Composition API）。</font>

###### <font style="color:rgb(6, 6, 7);">选择建议</font>
<font style="color:rgb(6, 6, 7);">学习阶段</font>

+ <font style="color:rgb(6, 6, 7);">如果你是 Vue 的新手，或者更习惯面向对象的编程风格，</font>**<font style="color:rgb(6, 6, 7);">选项式 API</font>**<font style="color:rgb(6, 6, 7);"> 可能更容易上手。它的结构清晰，符合传统的组件化思维。</font>
+ <font style="color:rgb(6, 6, 7);">如果你对函数式编程更熟悉，或者希望更灵活地组织和复用逻辑，可以尝试 </font>**<font style="color:rgb(6, 6, 7);">组合式 API</font>**<font style="color:rgb(6, 6, 7);">。它提供了更强大的逻辑复用能力。</font>

<font style="color:rgb(6, 6, 7);">生产项目</font>

+ **<font style="color:rgb(6, 6, 7);">低复杂度场景</font>**<font style="color:rgb(6, 6, 7);">：如果你的项目不需要复杂的逻辑复用，或者主要是一些渐进增强的应用场景，</font>**<font style="color:rgb(6, 6, 7);">选项式 API</font>**<font style="color:rgb(6, 6, 7);"> 是一个不错的选择，简单直接。</font>
+ **<font style="color:rgb(6, 6, 7);">高复杂度场景</font>**<font style="color:rgb(6, 6, 7);">：如果你打算用 Vue 构建完整的单页应用，尤其是需要处理复杂的业务逻辑和状态管理，</font>**<font style="color:rgb(6, 6, 7);">组合式 API + 单文件组件</font>**<font style="color:rgb(6, 6, 7);"> 是更推荐的方式，它提供了更高的灵活性和代码复用性。</font>

> 嗯，做单页应用吧，组合式，决定了
>



### 剩下的区域以后再来探索吧~
累了，收工



