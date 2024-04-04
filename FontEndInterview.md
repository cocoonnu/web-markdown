# 第一章 前端面试题

## 3.31

- 盒模型

CSS 的盒模型主要包括以下两种，可通过 box-sizing 属性进行配置：

content-box：默认属性。width 只包含 content
border-box：width 包含 (content、padding、border)



- CSS选择器及其优先级

id - 属性、类、伪类 - 标签、伪元素选择器

https://juejin.cn/post/6905539198107942919#heading-2



- CSS中可继承与不可继承属性有哪些

不可继承性属性：背景、盒子模型、定位、display 等属性

继承性属性：文字、文本系列属性

https://juejin.cn/post/6905539198107942919#heading-3



- 块元素、行内元素、行内块元素的区别

https://juejin.cn/post/6905539198107942919#heading-4



- 隐藏元素的方法有哪些

https://juejin.cn/post/6905539198107942919#heading-6



- 说说var、let、const之间的区别

变量提升、暂时性死区、重复声明、块级作用域、修改声明的变量

https://vue3js.cn/interview/es6/var_let_const.html#%E4%B8%80%E3%80%81var



- ES6中数组新增了哪些扩展

**扩展运算符**、构造函数：Array.from()、Array.of()、实例对象方法：copyWithin()，find()、findIndex()，fill()，entries()，keys()，values()，includes()，flat()，flatMap()

https://vue3js.cn/interview/es6/array.html#%E4%B8%80%E3%80%81%E6%89%A9%E5%B1%95%E8%BF%90%E7%AE%97%E7%AC%A6%E7%9A%84%E5%BA%94%E7%94%A8



- ES6 对象新增了哪些扩展

属性名简写、属性名表达式、拓展运算符，关于对象新增的方法，分别有以下：
```js
Object.is()
Object.assign()
Object.getOwnPropertyDescriptors()
Object.setPrototypeOf()，Object.getPrototypeOf()
Object.keys()，Object.values()，Object.entries()
Object.fromEntries()
```
https://vue3js.cn/interview/es6/object.html#%E4%B8%80%E3%80%81%E5%B1%9E%E6%80%A7%E7%9A%84%E7%AE%80%E5%86%99



- ES6 函数新增了哪些扩展

函数参数允许设置默认值，新增箭头函数，箭头函数与普通函数的区别

- 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象
- 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误
- 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 `rest` 参数代替

https://vue3js.cn/interview/es6/function.html#%E4%B8%80%E3%80%81%E5%8F%82%E6%95%B0



- 介绍一下 ES6 新增 Set、Map 两种数据结构

WeakSet 和 WeakMap 的理解

https://vue3js.cn/interview/es6/set_map.html#%E4%B8%80%E3%80%81set



## 4.01

- 什么是线程，什么是进程？

**线程**是操作系统能够进行运算调度的最小单位，它被包含在进程之中，是进程中的实际运作单位。一个进程可以包含多个线程，这些线程共享进程的资源，如内存空间、文件句柄等。不同线程之间可以并行执行，每个线程都有自己的堆栈和局部变量，但它们共享全局变量和静态变量。

**进程**是计算机中的程序关于某数据集合上的一次运行活动，是系统进行资源分配和调度的基本单位。一个进程可以包含多个线程，同时也拥有独立的地址空间。进程之间通常是相互独立的，每个进程都有自己的内存空间和系统资源，它们之间的通信需要特殊的机制来实现，比如进程间通信（IPC）。

简而言之，进程是系统进行资源分配和调度的基本单位，而线程是进程中的实际运作单位，用于完成进程内的各种任务。



- 减少页面加载有哪几种方法？

压缩资源文件：对 HTML、CSS 和 JavaScript 文件进行压缩，去除空白字符和注释，以减小文件大小，从而加快下载速度。

使用缓存：利用浏览器缓存机制，将页面所需的资源文件（如图片、样式表、脚本）设置为可缓存，以便在用户再次访问时可以直接从本地加载，减少网络请求。

延迟加载：将不是立即需要的资源，如图片、视频或某些 JavaScript 文件，延迟到页面其他内容加载完成后再进行加载，以提高初始页面加载速度。

使用 CDN：将静态资源部署到内容分发网络（CDN），使用户可以从距离较近的服务器获取资源，减少网络延迟和提高下载速度。

精简页面内容：删除不必要的元素和代码，减少 HTTP 请求次数，优化页面结构和布局，以降低页面加载时间。

异步加载：对于不影响首屏展示的内容，可以采用异步加载的方式，如使用<script>标签的async和defer属性，使页面在下载 JavaScript 文件时能够同时加载其他内容。



- Promis 的应用

https://vue3js.cn/interview/es6/promise.html#%E4%B8%80%E3%80%81%E4%BB%8B%E7%BB%8D



- 原型与原型链

```js
function Cat() {}
const cat = new Cat()

// 原型链
cat.__proto__ = Cat.ProtoType
Cat.ProtoType.__proto__ = Object.Prototype
Object.Prototype = null
```

ProtoType 称为构造函数的原型，当要获取一个对象的属性和方法时，就可以通过原型链层层追溯

https://juejin.cn/post/6844903989088092174



- 浅拷贝和深拷贝的什么，利用循环递归的方式手写深拷贝

https://vue3js.cn/interview/JavaScript/copy.html#%E4%B8%80%E3%80%81%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E5%AD%98%E5%82%A8



- 什么是闭包

例如计数器、延迟调用、回调等闭包的应用，其核心思想还是创建私有变量和延长变量的生命周期

https://vue3js.cn/interview/JavaScript/closure.html#%E4%B8%80%E3%80%81%E6%98%AF%E4%BB%80%E4%B9%88



- 谈谈对 this 对象的理解

https://vue3js.cn/interview/JavaScript/this.html#%E4%B8%80%E3%80%81%E5%AE%9A%E4%B9%89



- 说说 JavaScript 中的事件模型

https://vue3js.cn/interview/JavaScript/event_Model.html




- typeof 与 instanceof 区别

https://vue3js.cn/interview/JavaScript/typeof_instanceof.html#%E4%B8%80%E3%80%81typeof



- 说说你对事件循环的理解

同步任务、异步任务，宏任务、微任务

https://vue3js.cn/interview/JavaScript/event_loop.html




- react 与 vue 数组中 key 的作用是什么

diff算法需要比对虚拟dom的修改，然后异步的渲染到页面中，当出现大量相同的标签时，vnode会首先判断key和标签名是否一致，如果一致再去判断子节点一致，使用key可以帮助diff算法提升判断的速度，在页面重新渲染时更快消耗更少

https://q.shanyue.tech/fe/react/72



- 什么是 virtual DOM

打开了函数式 UI 编程的大门，dom 把渲染过程抽象化了，从而使得组件的抽象能力也得到提升，并且可以适配 DOM 以外的渲染目标。Virtual DOM 在牺牲(牺牲很关键)部分性能的前提下，增加了可维护性

https://q.shanyue.tech/fe/react/70



- React hooks 的优点有哪些

点击链接查看和 Kimi 智能助手的对话 https://kimi.moonshot.cn/share/co7a4l9hd0n1ufg6hfcg



- 有哪些常见的 React Hooks？

https://vue3js.cn/interview/React/React%20Hooks.html



- zustand 的优点

https://kimi.moonshot.cn/share/co5aruhhmfr8ji71aqvg





## 4.02

从今天开始主要针对这篇专栏进行八股文的背诵：https://juejin.cn/column/7243016090816905275

- Computed 和 Watch 的区别
- 常见的事件修饰符及其作用
- v-if 和 v-show 的区别
- data 为什么是一个函数而不是对象
- 谈谈MVVM架构
- 使用 Object.defineProperty() 来进行数据劫持有什么缺点？
- 双向数据绑定的原理
- 说一下Vue的生命周期
- 说说 Vue Router 的 hash模式
- Reac生命周期是怎样的?
- 虚拟DOM实现原理?
- setState到底是异步还是同步?
- React如何进行组件/逻辑复用?
- redux的工作流程?
- Vuex 是什么？核心流程？



## 4.03
从今天继续针对这篇专栏进行八股文的背诵：https://juejin.cn/column/7243016090816905275

- Vue3.0有什么更新
- defineProperty和proxy的区别
- Diff 算法
- Vue 为什么要设置 key？
- 为什么不建议用index作为key?
- React 合成事件是什么？
- 用过哪些 React Hook
- React Hooks 原理？



JS 基础这一块面试题也得加强：https://juejin.cn/post/7244335987575521336#heading-0

- 为什么0.1+0.2 ! == 0.3，精度丢失问题
- typeof null 输出 object 的原因分析
- 箭头函数的 this 指向情况：https://juejin.cn/post/7310415386405765159
- JS 的 new 操作符做了哪些事情
- 垃圾回收机制
- 哪些情况会导致内存泄漏



## 4.04

- React中组件之间如何通信？

https://vue3js.cn/interview/React/communication.html



- 说说对React中类组件和函数组件的理解？有什么区别？

https://vue3js.cn/interview/React/class_function%20component.html



- 说说对高阶组件的理解？应用场景?

把通用的逻辑放在高阶组件中，对组件实现一致的处理，从而实现代码的复用

所以，高阶组件的主要功能是封装并分离组件的通用逻辑，让通用逻辑在组件间更好地被复用

https://vue3js.cn/interview/React/High%20order%20components.html




- 说说你是如何提高组件的渲染效率的？

父组件渲染导致子组件渲染，子组件并没有发生任何改变，这时候就可以从避免无谓的渲染

https://vue3js.cn/interview/React/improve_render.html



- Vue组件之间的通信方式都有哪些？

https://vue3js.cn/interview/vue/communication.html



- Vue3.0 所采用的 Composition Api 与 Vue2.x 使用的 Options Api 有什么不同？

https://vue3js.cn/interview/vue3/composition.html



- **双向数据绑定是什么，如何简单的手动实现？（难点）**

先讲一遍 MVVM 架构，再讲一下 Vue 是如何实现双向数据绑定的，手写双向数据绑定的原理

https://vue3js.cn/interview/vue/bind.html



- **什么是 Diff 算法（难点）**

https://juejin.cn/post/7250012486992511033#heading-25



- Javascript 本地存储的方式有哪些？区别及应用场景？

https://vue3js.cn/interview/JavaScript/cache.html



- 说说 Javascript 数字精度丢失的问题，如何解决？

计算机存储双精度浮点数需要先把十进制数转换为二进制的科学记数法的形式，**因为存储时有位数限制（64位），并且某些十进制的浮点数在转换为二进制数时会出现无限循环，会造成二进制的舍入操作(0舍1入)，当再转换为十进制时就造成了计算误差**

https://vue3js.cn/interview/JavaScript/loss_accuracy.html



- 如何判断一个元素是否在可视区域中？

https://vue3js.cn/interview/JavaScript/visible.html



- 什么是 CSRF 攻击？

https://juejin.cn/post/7256702654578409532#heading-0



- **进程与线程的概念**

https://juejin.cn/post/7256702654578409532#heading-2



- **对浏览器的缓存机制的理解？强缓存和协商缓存？**

https://juejin.cn/post/7256702654578409532#heading-3



- 浏览器的渲染过程

https://vue3js.cn/interview/http/after_url.html#%E9%A1%B5%E9%9D%A2%E6%B8%B2%E6%9F%93



# 第二章 项目难点

## 小智问卷

- 介绍项目

首先进入全部问卷，展示我的列表卡片渲染，讲解一下这里展示了当前用户所有的问卷信息列表，展示卡片的所有按钮，列表实现了响应式排列、顶部可通过过滤条件获取问卷列表。展示星标问卷、回收站等页面。

讲解项目中封装了全局弹窗组件，点击个人中心进行展示。然后退出登录，展示用户登录页和注册页，讲解发送验证码的使用，前端封装了滑动验证的模态框，后端实现了阿里云手机发送验证码业务。

之后页面展示问卷编辑器，选中画布上的问卷组件即可修改组件的信息。展示左侧添加可复用的问卷组件。展示拖拽排序，展示上方编辑器工具栏。点击发布问卷，展示问卷统计页面和图表信息。

点击投放问卷进入答卷表单页面，回答一个表单后提交即可，演示到此结束。



- 为什么想做这样一个项目

毕业设计、接触过问卷系统的使用、开发一套实用性网站系统、用到自己学过的技术栈、全栈开发、巩固编程能力

点击链接查看和 Kimi 智能助手的对话 https://kimi.moonshot.cn/share/co6kvhhkqq4ojc0mpg90



- 问卷编辑器开发

首先第一个难点就是问卷编辑器的开发，不仅要配置问卷组件数据结构，使其能够灵活扩展和复用。另外还要便于大量问卷数据进行存储。图层、画布、属性表单，三者的数据如何联动？

1. `src/components/QuestionGenerator/QuestionCheckbox/components/Component.tsx` 组件负责画布展示
2. `src/components/QuestionGenerator/QuestionCheckbox/components/PropComponent.tsx` 组件负责提供属性表单
3. `src/views/EditQuestion/index.tsx` 页面组件只需根据问卷生成器提供的问卷配置进行规范的渲染即可
4. 然后前端只需维护好的问卷组件列表 `questionComInfoList`，调用保存接口时返回给后端存储即可



- 答卷表单的开发

首先是基于 Antd 的 From 进行了二次封装，使得无需编写冗余的 tsx 代码只需要一份简单的配置对象即可一键式生成一份表单。然后再在答卷生成页面 `src/views/AnswerForm/components/FormWrapper.tsx` 中编写了一个函数进行问卷组件类型到表单组件类型的映射，从而利用 `questionComInfoList` 一键式生成答卷表单



## Vue3 项目

Vue3 项目由于电脑本地没有拉取代码，无法本地调试，具体代码设计可以查看 Github 上的项目，里面也有记录这个项目的开发笔记，Vue3 项目和小程序项目都是去年上半年写的，这边可能不太好做演示。这两个技术栈我这边入职前肯定会复习复习，再写个小项目练练手。



## 公司项目

关于公司项目能学到的经验就是：

1. 首次接触到企业级别的大型项目，从搭建开发环境到项目运行起来踩了一点坑但也学到的经验。

2. 公司是进行多人开发的，于是针对 Git 的掌握程度也得到了提高，熟悉了常用的分支操作、合并操作、处理冲突还有发版提交
3. 学习了丰富的组件封装思想，像复杂的页面级通用表格组件还有根据后端返回的档案数据动态生成页面级查询组件
4. 学到了与后端进行接口联调的经验，更深入的了解了从反向代理到接口响应的流程
5. 参与了产品需求迭代的周期性开发，有了和产品、测试修复缺陷的沟通经验



# 第三章 非技术面

- 自我介绍

个人信息、前端接触时间、技术栈、实习经历、项目经历、笔记、未来规划

您好，我叫陈智毅，来自江西新余，本科就读的是东华理工大学通信工程专业24届应届生。我这边的话接触前端有两年的时间了。当前主要技术栈是 React 开发，有过 6 个月中厂实习经历，实习的主要任务是针对一套SaaS系统进行一些需求迭代的工作。项目经历的话 React、Vue、小程序和服务端都有开发过。平常喜欢逛一些技术社区丰富自己的技术，另外还喜欢做一些笔记记录自己的工作总结和学习心得。关于前端未来规划的话想多接触一下移动端的方向，包括跨平台框架和安卓原生开发，另外今年也学了 SpringBoot 框架开发了一套服务端系统，因此未来也考虑往全栈方向发展。我的自我介绍结束了，谢谢。



- 为什么选择前端这条路

兴趣、做个人项目、人才需求、前端社区

首先肯定对前端更有兴趣一点，然后个人也比较喜欢敲代码，写自己喜欢的项目。然后就是我觉得前端这个行业有人才需求，也很有前景，意味着就有更多的就业机会和发展空间。最后就是在互联网上前端的社区和资源特别丰富，可以从中学习、分享经验，获得支持和帮助。 



- 平时是如何学习前端的

自学能力、官网文档、技术博客、项目练手

对于编程这一块，我自学能力还可以，一般接触一项技术栈首先是去它的官网浏览一遍，然后会去参考一些博客和教程。最后就是直接通过项目实践，并且会同步记录学习笔记以此加深影响。另外还会去逛一些前端开源社区和开发者社区交流开发经验



- 更倾向于什么样的办公环境



# 第四章 算法与手写

## 4.04

今天的手写题主要参考：https://juejin.cn/post/7023906112843808804#heading-0

- 手写 new 操作符

- 手写科里化函数
- 使用setTimeout构建setInterval
- 手写instanceof
- 实现一个LRU缓存函数，可获取数据和写入数据，如果数据量超出时则删除最久未使用的数据值

