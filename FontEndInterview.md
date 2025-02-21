# 第一章 前端面试题

八股文和前端基础的话推荐这些专栏和网站进行学习：

- https://vue3js.cn/interview/
- https://juejin.cn/post/6905294475539513352
- https://juejin.cn/column/7243016090816905275
- https://juejin.cn/post/7023906112843808804
- 包含初中高三个等级的面试收集：https://github.com/pro-collection/interview-question



## 第一节

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



- 谈谈你对 BFC 的理解

https://vue3js.cn/interview/css/BFC.html



- **说说 var、let、const 之间的区别**

变量提升、暂时性死区、重复声明、块级作用域、修改声明的变量

https://vue3js.cn/interview/es6/var_let_const.html#%E4%B8%80%E3%80%81var



- **ES6 新增了哪些特性**

点击链接查看和 Kimi 智能助手的对话 https://kimi.moonshot.cn/share/co9mfluaofou902iotjg



- ES6中数组新增了哪些扩展

扩展运算符、构造函数：Array.from()、Array.of()、实例对象方法：copyWithin()，find()、findIndex()，fill()，entries()，keys()，values()，includes()，flat()，flatMap()

https://vue3js.cn/interview/es6/array.html#%E4%B8%80%E3%80%81%E6%89%A9%E5%B1%95%E8%BF%90%E7%AE%97%E7%AC%A6%E7%9A%84%E5%BA%94%E7%94%A8



- ES6 对象新增了哪些扩展

属性名简写、属性名表达式、拓展运算符，关于对象新增的方法

https://vue3js.cn/interview/es6/object.html#%E4%B8%80%E3%80%81%E5%B1%9E%E6%80%A7%E7%9A%84%E7%AE%80%E5%86%99



- **ES6 函数新增了哪些扩展**

函数参数允许设置默认值，新增箭头函数，箭头函数与普通函数的区别

- 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象
- 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误
- 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 `rest` 参数代替

https://vue3js.cn/interview/es6/function.html#%E4%B8%80%E3%80%81%E5%8F%82%E6%95%B0



- 介绍一下 ES6 新增 Set、Map 两种数据结构

WeakSet 和 WeakMap 的理解

https://vue3js.cn/interview/es6/set_map.html#%E4%B8%80%E3%80%81set



## 第二节

- **减少页面加载有哪几种方法**

点击链接查看和 Kimi 智能助手的对话 https://kimi.moonshot.cn/share/co9mepeaofou902imjn0



- Promis 的应用

https://vue3js.cn/interview/es6/promise.html#%E4%B8%80%E3%80%81%E4%BB%8B%E7%BB%8D



- **原型与原型链**

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



- **浅拷贝和深拷贝的什么，利用循环递归的方式手写深拷贝**

https://vue3js.cn/interview/JavaScript/copy.html#%E4%B8%80%E3%80%81%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E5%AD%98%E5%82%A8



- **什么是闭包**

例如计数器、延迟调用、回调等闭包的应用，其核心思想还是创建私有变量和延长变量的生命周期

https://vue3js.cn/interview/JavaScript/closure.html#%E4%B8%80%E3%80%81%E6%98%AF%E4%BB%80%E4%B9%88



- 谈谈对 this 对象的理解

https://vue3js.cn/interview/JavaScript/this.html#%E4%B8%80%E3%80%81%E5%AE%9A%E4%B9%89



- 说说 JavaScript 中的事件模型

https://vue3js.cn/interview/JavaScript/event_Model.html




- **typeof 与 instanceof 区别**

https://vue3js.cn/interview/JavaScript/typeof_instanceof.html#%E4%B8%80%E3%80%81typeof



- **说说你对事件循环的理解**

同步任务、异步任务，宏任务、微任务

https://vue3js.cn/interview/JavaScript/event_loop.html



- **React hooks 的优点有哪些**

点击链接查看和 Kimi 智能助手的对话 https://kimi.moonshot.cn/share/co7a4l9hd0n1ufg6hfcg



- **有哪些常见的 React Hooks**

https://vue3js.cn/interview/React/React%20Hooks.html



- zustand 的优点

https://kimi.moonshot.cn/share/co5aruhhmfr8ji71aqvg





## 第三节

- Vue 中常见的事件修饰符及其作用

https://juejin.cn/post/7250012486992511033#heading-2



- Vue 中 v-if 和 v-show 的区别

https://juejin.cn/post/7250012486992511033#heading-3



- Vue 选项配置中的 data 为什么是一个函数而不是对象

https://juejin.cn/post/7250012486992511033#heading-4



- **谈谈 MVVM 架构**

https://juejin.cn/post/7250012486992511033#heading-6



- **双向数据绑定的原理**

https://juejin.cn/post/7250012486992511033#heading-24



- **说一下 Vue 的生命周期**

https://juejin.cn/post/7250012486992511033#heading-8



- **说一下 Reac 生命周期是怎样的**

https://juejin.cn/post/7250357906712838205#heading-0



- **虚拟 DOM 实现原理，如何理解**

https://juejin.cn/post/7250012486992511033#heading-22



- 介绍一下 Rudex 的工作流程

https://juejin.cn/post/7250357906712838205#heading-10



- 介绍一下 Vuex 的工作流程

https://juejin.cn/post/7250012486992511033#heading-16



## 第四节
- **Vue3 有什么更新，和 Vue2 的区别是什么**

https://vue3js.cn/interview/vue/vue3_vue2.html



- **描述一下 Diff 算法**

https://juejin.cn/post/7250012486992511033#heading-25



- Vue 和 React 为什么都要设置 key，为什么不建议用 index 作为 key

https://juejin.cn/post/7250012486992511033#heading-26



- React 合成事件是什么

https://juejin.cn/post/7250357906712838205#heading-14



- React Hooks 原理以及核心是什么

https://juejin.cn/post/7250357906712838205#heading-15



- 普通函数和箭头函数的 this 指向问题

https://juejin.cn/post/7310415386405765159



- 为什么 typeof null 输出 object

https://juejin.cn/post/7244335987575521336#heading-7



- **JS 的 new 操作符做了哪些事情**

https://juejin.cn/post/7244335987575521336#heading-12



- **垃圾回收机制是什么，哪些情况会导致内存泄漏**

https://juejin.cn/post/7244335987575521336#heading-26



## 第五节

- React 中组件之间如何通信

https://vue3js.cn/interview/React/communication.html



- **说说对 React 中类组件和函数组件的区别**

https://vue3js.cn/interview/React/class_function%20component.html



- **说说对高阶组件的理解和它的应用场景**

把通用的逻辑放在高阶组件中，对组件实现一致的处理，从而实现代码的复用

所以，高阶组件的主要功能是封装并分离组件的通用逻辑，让通用逻辑在组件间更好地被复用

https://vue3js.cn/interview/React/High%20order%20components.html




- 说说你是如何提高组件的渲染效率的

父组件渲染导致子组件渲染，子组件并没有发生任何改变，这时候就可以从避免无谓的渲染

https://vue3js.cn/interview/React/improve_render.html



- **Vue 组件之间的通信方式都有哪些**

https://vue3js.cn/interview/vue/communication.html



- Vue3.0 所采用的 Composition Api 与 Vue2.x 使用的 Options Api 有什么不同

https://vue3js.cn/interview/vue3/composition.html



- **双向数据绑定是什么，如何简单的手动实现**

先讲一遍 MVVM 架构，再讲一下 Vue 是如何实现双向数据绑定的，手写双向数据绑定的原理

https://vue3js.cn/interview/vue/bind.html



- 说一说 Javascript 本地存储的方式有哪些，区别及应用场景

https://vue3js.cn/interview/JavaScript/cache.html



- **说说 Javascript 数字精度丢失的问题，以及如何解决**

计算机存储双精度浮点数需要先把十进制数转换为二进制的科学记数法的形式，因为存储时有位数限制（64位），并且十进制的浮点数在转换为二进制数时会出现无限循环，会造成二进制的舍入操作(0舍1入)，当再转换为十进制时就造成了计算误差

https://vue3js.cn/interview/JavaScript/loss_accuracy.html



- 如何判断一个元素是否在可视区域中

https://vue3js.cn/interview/JavaScript/visible.html



- 什么是 CSRF 攻击

https://juejin.cn/post/7256702654578409532#heading-0



- 进程与线程的概念

https://juejin.cn/post/7256702654578409532#heading-2



- **对浏览器的缓存机制的理解？强缓存和协商缓存？**

https://juejin.cn/post/7256702654578409532#heading-3



- 浏览器的渲染过程

https://vue3js.cn/interview/http/after_url.html#%E9%A1%B5%E9%9D%A2%E6%B8%B2%E6%9F%93



- **说说地址栏输入 URL 敲下回车后发生了什么**

URL 解析、DNS 查询、TCP 连接、HTTP 请求、响应请求、响应资源解析、页面渲染

https://vue3js.cn/interview/http/after_url.html



## 第六节

- 说说 TCP 为什么需要三次握手和四次挥手

https://vue3js.cn/interview/http/handshakes_waves.html



- 说说 HTTP 常见的状态码有哪些，适用场景

https://vue3js.cn/interview/http/status.html



- css 加载会造成阻塞吗

https://juejin.cn/post/7256702654578409532#heading-5



- 重排（回流）和重绘有什么区别，什么会引发重排，什么会引发重绘

https://juejin.cn/post/7256702654578409532#heading-6



- **什么是同源策略**

同源策略是一种规定，它是浏览器最核心也是最基本的安全功能，如果缺少了同源策略浏览器的安全功能将会受到影响。所谓同源是指：域名、协议、端口相同，同源策略又分为以下两种：XMLHttpRequest 同源策略、DOM 同源策略

https://juejin.cn/post/7256702654578409532#heading-9



- **如何解决跨域问题**

CORS：跨域资源共享，只要服务端添加一个 `Access-Control-Allow-Origin` 请求头设置为我们的目标域名，这个 HTTP 头就决定浏览器允许我们获取跨域请求的响应

JSONP：它的原理就是利用 `<script>` 标签没有跨域限制，通过 `<script>` 标签 src 属性，发送带有 `callback` 函数的 **GET请求**，服务端将接口返回数据拼凑到 `callback` 函数中，返回给浏览器，从而前端再利用 `callback` 函数拿到返回的数据

Proxy：网络代理模式，有以下几种解决方案：1. 我们可以通过 `webpack` 为我们起一个本地服务器作为请求的代理对象，通过该服务器转发请求至目标服务器，得到结果再转发给前端 2. 此外还可通过一些 node 服务端比如 express 实现代理请求转发 3. 最后是直接可以在服务器上配置 Nginx 实现反向代理从而实现跨域

https://juejin.cn/post/7256702654578409532#heading-10

https://vue3js.cn/interview/vue/cors.html



## 第七节

- async 与 await，`await` 会阻塞下面的代码（即加入微任务队列）

https://vue3js.cn/interview/JavaScript/event_loop.html#%E4%B8%89%E3%80%81async%E4%B8%8Eawait



- git rebase 和 git merge 的区别？

https://juejin.cn/post/7257441472458604599#heading-7



- JS 继承有哪些？有什么优缺点？

原型链继承、构造函数继承、组合继承、使用 `Object.create` 实现浅拷贝对象、寄生组合式继承（class 语法糖采用形式）

https://vue3js.cn/interview/JavaScript/inherit.html



## 第八节

- 常量枚举和 enum 枚举有什么区别

顾名思义就是一个是常量一个是变量，并且常量枚举在编译 TypeScript 代码时会被直接替换到实际使用它们的地方，而不会创建一个真实的对象，减少了代码量。后者会产生一个真实的对象。

点击链接查看和 Kimi 智能助手的对话 https://kimi.moonshot.cn/share/coa9s6cudu6bkp82ar10



- Node 事件循环机制和浏览器的有什么不同

点击链接查看和 Kimi 智能助手的对话 https://kimi.moonshot.cn/share/coaa7o017fmccaal69n0



- 数组去重有哪些实现方法

https://juejin.cn/post/7023906112843808804#heading-7



- TS 中 interface和 type 区别

当你需要描述对象的形状时，可以优先选择使用 `interface`。而对于其他类型定义，比如联合类型、交叉类型、函数类型等，可以考虑使用 `type` 创建一个类型变量并定义别名

https://juejin.cn/post/7321542773076082699#heading-2



- React 中 setState 到底是异步还是同步

https://juejin.cn/post/7250357906712838205#heading-3



- 说说对 Fiber 架构的理解，解决了什么问题

https://vue3js.cn/interview/React/Fiber.html



## 第九节

- React18 有什么新特性

https://juejin.cn/post/7290815534207189033



- 为什么有时候⽤ translate 来改变位置⽽不是定位

https://juejin.cn/post/6905539198107942919#heading-13



- SPA首屏加载速度慢的怎么解决

https://vue3js.cn/interview/vue/first_page_time.html



- SSR 解决了什么问题，有做过 SSR 吗

https://vue3js.cn/interview/vue/ssr.html



# 第二章 前端笔试题

 ## 第一节

异步&事件循环：https://juejin.cn/post/6959043611161952269



## 第二节

this 指针问题：https://juejin.cn/post/6959043611161952269



# 第三章 算法与手写

## 第一节

今天的手写题主要参考：https://juejin.cn/post/7023906112843808804#heading-0

- 手写 new 操作符

- 手写科里化函数
- 使用setTimeout构建setInterval
- 手写instanceof
- 实现一个LRU缓存函数，可获取数据和写入数据，如果数据量超出时则删除最久未使用的数据值



## 第二节

今天的手写题主要参考：https://juejin.cn/post/7023906112843808804#heading-13

- 简单实现 发布订阅模式
- 实现 JSON.parse
- 递归循环实现基础的深拷贝：https://vue3js.cn/interview/JavaScript/copy.html
- 手写防抖和节流
- 手写数组去重
- 手写 call、apply
- 手写 bind，既要实现改变指向又要兼容构造函数



## 第三节

今天的手写题主要参考：https://juejin.cn/post/6994594642280857630

- 手写 Promise，实现基本 Promise 回调与 then 链式调用
- 手写 Promise.all
- 手写 Promise.race
- 手写 Promise.allSettled



- 冒泡排序

https://www.hello-algo.com/chapter_sorting/bubble_sort/



- 插入排序

https://www.hello-algo.com/chapter_sorting/insertion_sort/#1141



- 快速排序

https://www.hello-algo.com/chapter_sorting/quick_sort/





# 第四章 难点与经验

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



实习难点 & 突破点



实习个人优势



# 第五章 非技术面

## 自我介绍

个人信息、前端接触时间、技术栈、实习经历、项目经历、笔记、未来规划

您好，我叫陈智毅，来自江西新余，本科就读的是东华理工大学通信工程专业24届应届生。我这边的话接触前端有两年的时间了。当前主要技术栈是 React 开发，有过 6 个月中厂实习经历，实习的主要任务是针对一套SaaS系统进行一些需求迭代的工作。项目经历的话 React、Vue、小程序和服务端都有开发过。平常喜欢逛一些技术社区丰富自己的技术，另外还喜欢做一些笔记记录自己的工作总结和学习心得。关于前端未来规划的话可能想接触一下移动端方面的知识，包括一些跨平台框架和安卓原生开发，另外今年也学了 SpringBoot 框架开发了一套服务端系统，因此未来也可能考虑往全栈方向发展。我的自我介绍结束了，谢谢。



## 非技术问题

- 为什么选择前端这条路

兴趣、做个人项目、人才需求、前端社区

首先肯定对前端更有兴趣一点，然后个人也比较喜欢敲代码，写自己喜欢的项目。然后就是我觉得前端这个行业有人才需求，也很有前景，意味着就有更多的就业机会和发展空间。最后就是在互联网上前端的社区和资源特别丰富，可以从中学习、分享经验，获得支持和帮助。 



- 平时是如何学习前端的

自学能力、官网文档、技术博客、项目练手

对于编程这一块，我自学能力还可以，一般接触一项技术栈首先是去它的官网浏览一遍，然后会去参考一些博客和教程。最后就是直接通过项目实践，并且会同步记录学习笔记以此加深影响。另外还会去逛一些前端开源社区和开发者社区交流开发经验



- 为什么来杭州

个人憧憬、就业机会、学习机会、亲戚朋友、认识更多志同道合的朋友



- 个人优势有哪些，缺点有哪些

专注、有责任心、比较注重代码规范和文档规范、做一件事情或者任务会想要去达到一个最满意的状态

首先是个慢热型的人，需要先接触一段时间才能放的开一些、然后是有一点点轻微强迫症。心态不够成熟，还缺乏锻炼和成长。



- 你是如何处理压力和挑战的

处理压力是通过兴趣爱好来达到放松的效果，面对挑战的话是先梳理清除的逻辑和规划好日程安排，一步一步来解决



- 你最引以为傲的成就是什么

做出来了一个全栈项目，从产品到开发再到测试都由自己完成



- 你对个人发展和职业规划有哪些想法

未来 3-5 年还是打算在杭州发展，巩固前端技术、提示自身实力、从初级前端慢慢成长为中级前端再到高级前端工程师。认真对待工作和布置的任务。最后希望和公司一起稳定发展和进步。



- 反问：前端管培生的一个大概的培养计划和安排是怎么样的



- 反问：实习期间在技术部门的主要业务场景和工作内容是什么



- 反问：您可以评价一下我今天面试的表现吗



## 个人反问

- 研发部的工作时间安排
- 公司项目大概的业务，项目的技术栈
- 前面不清楚的问题请教
- 实习生主要任务和安排
- 可以评价一下我今天面试的表现吗？有哪些地方需要改进的呢
- 有 code review 和技术分享会之内的



# 第六章 面试记录

- 大智慧（1000-9999）技术一面

```ts
// node事件循环机制和浏览器有什么不同
// 数组去重有哪些实现方法
// 判断一个对象（直接判断内部的值）是否相等
// react 的useMemo和useCallback，useCallback传入多个依赖变量应该如何进行性能优化
// React18有什么新特性
// fiber 渲染机制，什么中断机制的概念
// interface和type区别
// antd按需加载如何实现
// ES6有哪些新特性
// 高阶函数是什么，有什么作用和缺点
// 遍历数组和对象的方式有哪些
// Object.keys()和forin循环遍历对象有什么区别
// 路由拦截器怎么实现的
```



- 大智慧（1000-9999）技术二面

```js
// 八股文基本不考了，考一些个人的硬实力和经验方面的问题
// 为什么选择前端
// 平时是如何学习前端的
// React和Vue有什么区别
// 为什么选择来合肥
// 在实习期间最有挑战性的事情是什么
// 在做项目期间有哪些性能优化的点
// 白屏时间长应该怎么解决
// 项目里的权限管理有哪些，如何实现的
// 有参与项目的组件封装吗
// useMemo和useCallback有什么区别
// 拖拽排序是如何实现的
// 受控组件和非受控组件的区别
// 什么是虚拟dom
```



- 理想连线（1000-9999）高管面

```js
// 你的个人优势和缺点是什么
// 你最引以为傲的成就是什么
// 你有哪些管理层面的经历
// 为什么想要学习前端
// 你觉得是完成一个个人项目更有成就感还是带领好团队成功更有成就感
// 为什么选这个专业
// 你是外向还是内向
```



- 华世界（500-999）技术一面

```js
// HTML5有哪些新增标签
// ES6有哪些新特性
// Vue3到Vue2有哪些更新
// React有哪些常用的hooks
// Less和CSS有什么区别
// 路由权限拦截器怎么实现的
```



- 半糖科技（100-499）技术一面

```js
// 什么是BFC
// 有了解过React18吗
// 有搭建过webpack的其他配置吗
// 能不能从0开始搭建一套webpack工程化
// CSS阻塞是什么情况
// 箭头函数和普通函数的区别
// 如何手动实现一个虚拟列表
// 什么是宏任务和微任务
// 普通函数中的this指向问题
// 原型链的概念
// forof和forin的区别
// 如何使得forof可以遍历一个对象
// 什么是迭代对象，底层原理是什么
// 迭代器和迭代对象有什么区别，如何实现迭代器
// 什么是事件委托
// React的fiber机制是什么
// React的合成事件是什么
// URL从输入到页面渲染经历了哪些过程
// 如何实现拖拽排序，底层原理是什么，哪个html标签支持拓展
// 什么是同源策略
// 什么是回流和重绘
// 什么是浏览器的缓存机制
// 当我们要进行一个元素的位移，使用移动更好还是定位更好，为什么
// Vue中的data返回的为什么是一个函数而不是对象
// SSR是什么，有什么哪些方面的优点
// 在实习过程中有没有遇到什么难点
```



- 半糖科技（100-499）技术二面

```js
// 面过最严肃和最真实的高管
// 实习过程中碰到过哪些难点，难题、方案、结果
// 实习过程中你表现最好的方面是什么
// 反问：实习期的主要任务是什么？不会把你当成实习生，给的任务和正式员工的一样
// 反问：有没有code review和技术分析会之内的？没有，这些都对实际工作没有任何推动
```



- 玩点科技（100-499）技术一面

```js
// 全是照着简历问的
// 项目中的虚拟列表是怎么实现的
// 项目中的登录拦截器是怎么实现得到
// 了解哪些浏览器存储
// 介绍一下promise
// 介绍一下flex
// 说一下八种数据结构
// 说一下如何快速搭建一个node服务器吧
// 你是如何实现项目中的全局弹窗管理的
```

