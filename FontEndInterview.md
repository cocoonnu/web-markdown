# 第一章 前端面试题

八股文和前端基础的话推荐这些专栏和网站进行学习：

- https://vue3js.cn/interview/
- https://www.codecrack.cn/zh
- https://juejin.cn/column/7243016090816905275
- https://juejin.cn/post/7023906112843808804
- https://github.com/pro-collection/interview-question



## 第一节

**CSS选择器及其优先级**

- id - 属性、类、伪类 - 标签、伪元素选择器

- https://juejin.cn/post/6905539198107942919#heading-2



**CSS中可继承与不可继承属性有哪些**

- 不可继承性属性：背景、盒子模型、定位、display 等属性，继承性属性：文字、文本系列属性

- https://juejin.cn/post/6905539198107942919#heading-3



**块元素、行内元素、行内块元素的区别、display的属性值及其作用**

- https://juejin.cn/post/6905539198107942919#heading-4



**隐藏元素的方法有哪些**

- https://juejin.cn/post/6905539198107942919#heading-6



**谈谈你对 BFC 的理解**

- https://vue3js.cn/interview/css/BFC.html



**说说 var、let、const 之间的区别**

- 变量提升、暂时性死区、重复声明、块级作用域、修改声明的变量

- https://vue3js.cn/interview/es6/var_let_const.html#%E4%B8%80%E3%80%81var



**ES6中数组新增了哪些扩展**

- 扩展运算符、构造函数：Array.from()、Array.of()、实例对象方法：copyWithin()，find()、findIndex()，fill()，entries()，keys()，values()，includes()，flat()，flatMap()

- https://vue3js.cn/interview/es6/array.html#%E4%B8%80%E3%80%81%E6%89%A9%E5%B1%95%E8%BF%90%E7%AE%97%E7%AC%A6%E7%9A%84%E5%BA%94%E7%94%A8



**ES6 对象新增了哪些扩展**

- 属性名简写、属性名表达式、拓展运算符，关于对象新增的方法

- https://vue3js.cn/interview/es6/object.html#%E4%B8%80%E3%80%81%E5%B1%9E%E6%80%A7%E7%9A%84%E7%AE%80%E5%86%99



**ES6 函数新增了哪些扩展**

- 函数参数允许设置默认值，新增箭头函数，箭头函数与普通函数的区别

- 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象
- 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误
- 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 `rest` 参数代替

- https://vue3js.cn/interview/es6/function.html#%E4%B8%80%E3%80%81%E5%8F%82%E6%95%B0



**介绍一下 undefined 和 null 的区别**

- 讲一下两者的定义，并且列举一下函数入参和解构赋值的时候设置默认值的例子
- https://www.codecrack.cn/zh/javascript/difference-between-undefined-and-null



**0.1 + 0.2 为什么不等于 0.3**

- 根本原因是浮点数的二进制表示，许多看似简单的十进制小数在计算机中无法精确表示，导致计算时产生微小的误差
- 一般的浮点数的比较方法为：x - y == y  就是 true，x - y == z  就是 false  
- https://www.codecrack.cn/zh/javascript/why-decimal-addition-not-equal



## 第二节

**介绍一下原型与原型链的概念**

- 讲解构造函数和实例的对象的关系，隐式原型和原型对象的关系，共享字段和方法还有原型链的查找等等
- https://juejin.cn/post/6844903989088092174
- https://www.codecrack.cn/zh/javascript/prototype-chain#%E5%8E%9F%E5%9E%8B%E6%A8%A1%E5%BC%8F



**如何判定一个属性来自于对象本身， 还是来自于原型链**

- https://github.com/pro-collection/interview-question/issues/1044



**介绍一下 JavaScript 中的 new 操作符**

- https://juejin.cn/post/7244335987575521336#heading-12
- https://www.codecrack.cn/zh/javascript/prototype-chain#%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0



**介绍一下浅拷贝和深拷贝的概念，并利用循环递归的方式手写深拷贝**

- https://vue3js.cn/interview/JavaScript/copy.html#%E4%B8%80%E3%80%81%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E5%AD%98%E5%82%A8



**什么是闭包，它的作用是什么**

- 例如计数器、延迟调用、回调等闭包的应用，其核心思想还是创建私有变量和延长变量的生命周期

- https://vue3js.cn/interview/JavaScript/closure.html#%E4%B8%80%E3%80%81%E6%98%AF%E4%BB%80%E4%B9%88



**谈谈你对 this 对象的理解**

- new 绑定优先级 > 显示绑定优先级 > 隐式绑定优先级 > 默认绑定优先级

- https://vue3js.cn/interview/JavaScript/this.html#%E4%B8%80%E3%80%81%E5%AE%9A%E4%B9%89

- 跟深入理解：https://www.codecrack.cn/zh/javascript/this-binding



**说说 JavaScript 中的事件模型**

- 原生事件模型有两种：原始事件模型、标准事件模型
- 原始事件模型只支持冒泡，实现方式为：`<input type="button" id="btn" onclick="fun1()">`
- 标准事件模型支持冒泡或者捕获，实现方式为：`addEventListener(eventType, handler, useCapture)`
- 一个事件流分为三个阶段：事件捕获阶段 - 处于目标阶段 - 事件冒泡阶段

- https://vue3js.cn/interview/JavaScript/event_Model.html



**React 合成事件是什么**

- React 基于浏览器的事件机制自身实现了一套事件机制，包括事件注册、事件的合成、事件冒泡、事件派发等，这套事件机制被称之为合成事件，目的是为了更好的兼容性和跨平台、减少内存开销
- React 上注册的事件最终会绑定在 document 这个 DOM 上，而不是 React 组件对应的 DOM

- https://juejin.cn/post/7250357906712838205#heading-14



**typeof 与 instanceof 区别**

- https://vue3js.cn/interview/JavaScript/typeof_instanceof.html#%E4%B8%80%E3%80%81typeof



**有哪些常见的 React Hooks**

- https://vue3js.cn/interview/React/React%20Hooks.html



## 第三节

**谈谈 MVVM 架构**

- https://juejin.cn/post/7250012486992511033#heading-6



**双向数据绑定的原理**

- https://juejin.cn/post/7250012486992511033#heading-24



**说一下 Vue 的生命周期**

- https://juejin.cn/post/7250012486992511033#heading-8



**说一下 Reac 生命周期是怎样的**

- https://juejin.cn/post/7250357906712838205#heading-0



**虚拟 DOM 实现原理，如何理解**

- https://juejin.cn/post/7250012486992511033#heading-22



**介绍一下 Rudex 的工作流程**

- https://juejin.cn/post/7250357906712838205#heading-10



## 第四节
**描述一下 React 中的 Diff 算法**

- https://juejin.cn/post/7229598397250109497



**说说对 Fiber 架构的理解，解决了什么问题**

- https://vue3js.cn/interview/React/Fiber.html
- https://juejin.cn/post/7229552637229498405



**Vue 和 React 为什么都要设置 key，为什么不建议用 index 作为 key**

- https://juejin.cn/post/7250012486992511033#heading-26



**React Hooks 原理以及核心是什么**

- https://juejin.cn/post/7250357906712838205#heading-15



**垃圾回收机制是什么，哪些情况会导致内存泄漏**

- https://juejin.cn/post/7244335987575521336#heading-26



## 第五节

**React 中组件之间如何通信**

- https://vue3js.cn/interview/React/communication.html



**说说对 React 中类组件和函数组件的区别**

- https://vue3js.cn/interview/React/class_function%20component.html



**说说对高阶组件的理解和它的应用场景**

- 把通用的逻辑放在高阶组件中，对组件实现一致的处理，从而实现代码的复用

- 所以，高阶组件的主要功能是封装并分离组件的通用逻辑，让通用逻辑在组件间更好地被复用

- https://vue3js.cn/interview/React/High%20order%20components.html



**说说你是如何提高组件的渲染效率的**

- 父组件渲染导致子组件渲染，子组件并没有发生任何改变，这时候就可以从避免无谓的渲染

- https://vue3js.cn/interview/React/improve_render.html



**双向数据绑定是什么，如何简单的手动实现**

- 先讲一遍 MVVM 架构，再讲一下 Vue 是如何实现双向数据绑定的，手写双向数据绑定的原理

- https://vue3js.cn/interview/vue/bind.html



**说一说 Javascript 本地存储的方式有哪些，区别及应用场景**

- https://vue3js.cn/interview/JavaScript/cache.html



**说说 Javascript 数字精度丢失的问题，以及如何解决**

- 计算机存储双精度浮点数需要先把十进制数转换为二进制的科学记数法的形式，因为存储时有位数限制（64位），并且十进制的浮点数在转换为二进制数时会出现无限循环，会造成二进制的舍入操作(0舍1入)，当再转换为十进制时就造成了计算误差

- https://vue3js.cn/interview/JavaScript/loss_accuracy.html



**如何判断一个元素是否在可视区域中**

- https://vue3js.cn/interview/JavaScript/visible.html



**什么是 CSRF 攻击**

- https://juejin.cn/post/7256702654578409532#heading-0



**进程与线程的概念**

- 进程是操作系统对一个正在运行的程序的抽象表示，负责管理程序的执行和资源分配，它存在堆内存分配和栈内存分配
- 在操作系统中，每个进程都有自己的地址空间、状态和控制信息。进程可以独立运行，与其他进程离开来，互不干扰

- 线程是进程中的一个执行路径，是进程的组成部分，**在同一个进程中的多个线程共享进程的资源，并且并行执行**
- 每个进程至少包含一个主线程，主线程用于执行进程的主要业务逻辑，其他线程可以作为辅助线程来完成特定的任务

- https://www.codecrack.cn/zh/javascript/event-loop#%E4%BB%80%E4%B9%88%E6%98%AF%E8%BF%9B%E7%A8%8B



**介绍一下浏览器的渲染过程**

- Chrome 浏览器通过多进程的架构设计来加载多个网页，主要包括以下三个进程：网络进程、浏览器进程、渲染进程
- 浏览器给渲染进程采用了多线程，它主要包含了以下线程：渲染主线程、合成线程、网络线程、定时器线程、事件处理线程
- 渲染主线程负责解析 `HTML`、`CSS` 和 `JavaScript`，构建 `DOM` 树、`CSSOM` 树和渲染树，并进行页面布局和绘制，它还处理用户交互，执行 `JavaScript` 代码以及其他页面渲染相关的任务

- http://codecrack.cn/zh/javascript/event-loop#%E6%B8%B2%E6%9F%93%E4%B8%BB%E7%BA%BF%E7%A8%8B%E6%98%AF%E5%A6%82%E4%BD%95%E5%B7%A5%E4%BD%9C%E7%9A%84



**说说你对浏览器事件循环的理解**

- 首先 JavaScript 是一门单线程语言，当渲染主线程执行一些 JavaScript 中的**事件处理、定时器和异步操作**等异步任务时，为了防止主线程阻塞，主线程会和其他线程通过消息队列进行通信来防止阻塞

- 比如当渲染主线程正在执行一个 `JavaScript` 函数，执行到一半的时候碰到了一个定时器，也就是 `setTimeout`。因为在我们的渲染进程里面是有定时器线程的，定时器线程监听到有这个定时器操作。**那么该线程会将 `setTimeout` 里面的回调函数作为一个异步任务放入消息队列中进行排队**

- 因此事件循环就是首先执行完成**主线程的同步任务**，再依次执行**消息队列中的异步任务**，如果在异步任务里面再碰到异步任务，那么按照前面的步骤依此循环，直到所有任务执行完成

- 同步任务：变量和函数的声明和计算、普通函数调用、DOM 操作、for / while / if / switch 等语句

- 异步任务：定时器相关、I/O 相关、事件监听、Promise 等语句 

- http://codecrack.cn/zh/javascript/event-loop#%E6%B8%B2%E6%9F%93%E4%B8%BB%E7%BA%BF%E7%A8%8B%E6%98%AF%E5%A6%82%E4%BD%95%E5%B7%A5%E4%BD%9C%E7%9A%84



**Node.js 事件循环机制和浏览器的有什么不同**

- 先介绍 Nodejs 的事件循环机制的理解，再介绍具体的区别
- 区别一：process.nextTick 是 Node.js 中用于注册比其他所有异步任务还早执行的微任务

- 区别二：Nodejs 的事件循环分成多个阶段（timers, poll, check 等）

- 区别三：Node.js 借助 libuv 实现复杂事件循环

- https://vue3js.cn/interview/NodeJS/event_loop.html



**谈谈你对异步的理解，并讲一下什么是宏任务和微任务**

- 最简单的理解异步：`JavaScript` 是一门单线程的编程语言，意味着在一个特定的时间点，只能有一个代码块在执行。当执行一个同步任务时，如果任务需要很长时间才能完成，如网络请求、文件读取等，整个程序会被阻塞，导致用户界面无响应，甚至造成卡顿的问题。而异步编程使得我们可以在主线程执行同步代码的同时，处理耗时的异步操作，例如网络请求、文件读写等，以提高程序的性能和用户体验。在 `JavaScript` 中，通过事件循环机制，异步编程实现了一种非阻塞的执行方式，使得浏览器能够高效地处理各种任务，同时保持用户界面的响应性
- 上一个问题我们讲到异步任务存储于消息队列中，消**息队列又分为宏任务队列和微任务队列。**微任务通常在一个宏任务执行完毕后立即执行，而不需要等待其他宏任务，这使得微任务的执行优先级比宏任务高
- 宏任务：setTimeout 和 setInterval、I/O 操作、DOM 事件、requestAnimationFrame、**script 标签**
- 微任务：Promise 的 resolve 和 reject 回调、async/await 中的异步函数、MutationObserver
- 由于 script 标签是一个宏任务，因此整个浏览器循环应该是 先执行 `宏任务` -> `同步代码` -> `微任务`，直到当前宏任务中的微任务清理完毕，继续执行下一个宏任务，以此类推
- https://www.codecrack.cn/zh/javascript/event-loop#%E4%BB%80%E4%B9%88%E6%98%AF%E5%BC%82%E6%AD%A5



**说说地址栏输入 URL 敲下回车后发生了什么**

- URL 解析、DNS 查询、TCP 连接、HTTP 请求、响应请求、响应资源解析、页面渲染

- https://vue3js.cn/interview/http/after_url.html

- 超详细版文档：https://juejin.cn/post/7316775422187061300



**对浏览器的缓存机制的理解？强缓存和协商缓存？**

- https://juejin.cn/post/7256702654578409532#heading-3



## 第六节

**说说 TCP 为什么需要三次握手和四次挥手**

- https://vue3js.cn/interview/http/handshakes_waves.html



**说说 HTTP 常见的状态码有哪些，适用场景**

- https://vue3js.cn/interview/http/status.html



**CSS 加载会造成阻塞吗**

- https://juejin.cn/post/7256702654578409532#heading-5



**重排（回流）和重绘有什么区别，什么会引发重排，什么会引发重绘**

- https://juejin.cn/post/7256702654578409532#heading-6



**什么是同源策略**

- 同源策略是一种规定，它是浏览器最核心也是最基本的安全功能，如果缺少了同源策略浏览器的安全功能将会受到影响。所谓同源是指：域名、协议、端口相同，同源策略又分为以下两种：XMLHttpRequest 同源策略、DOM 同源策略

- https://juejin.cn/post/7256702654578409532#heading-9



**如何解决跨域问题**

- CORS：跨域资源共享，只要服务端添加一个 `Access-Control-Allow-Origin` 请求头设置为我们的目标域名，这个 HTTP 头就决定浏览器允许我们获取跨域请求的响应

- JSONP：它的原理就是利用 `<script>` 标签没有跨域限制，通过 `<script>` 标签 src 属性，发送带有 `callback` 函数的 **GET请求**，服务端将接口返回数据拼凑到 `callback` 函数中，返回给浏览器，从而前端再利用 `callback` 函数拿到返回的数据

- Proxy：网络代理模式，有以下几种解决方案：1. 我们可以通过 `webpack` 为我们起一个本地服务器作为请求的代理对象，通过该服务器转发请求至目标服务器，得到结果再转发给前端 2. 此外还可通过一些 node 服务端比如 express 实现代理请求转发 3. 最后是直接可以在服务器上配置 Nginx 实现反向代理从而实现跨域

- https://juejin.cn/post/7256702654578409532#heading-10

- https://vue3js.cn/interview/vue/cors.html



## 第七节

**async await 原理以及如何捕捉错误**

- https://vue3js.cn/interview/JavaScript/event_loop.html#%E4%B8%89%E3%80%81async%E4%B8%8Eawait



**git rebase 和 git merge 的区别是什么**

- https://juejin.cn/post/7257441472458604599#heading-7



**JS 继承有哪些？有什么优缺点？**

- 原型链继承、构造函数继承、组合继承、使用 `Object.create` 实现浅拷贝对象、寄生组合式继承（class 语法糖采用形式）

- https://vue3js.cn/interview/JavaScript/inherit.html



**能不能从零开始搭建一套 webpack 工程化**

- https://www.codecrack.cn/zh/engineer/what-webpack-does-when-importing-modules



**什么是变量提升和函数提升**

- https://www.cnblogs.com/liuhe688/p/5891273.html



## 第八节

**常量枚举和普通枚举有什么区别**

- 普通枚举 `enum A {...}` 和常量枚举 `const enum A {...}` 之间的区别主要在于 `TS` 的编译结果上有所差别

- 普通枚举 `enum A {...}`, 会将其编译为一个 `JS` 对象, **对象内就是枚举成员和值的一个相互映射**

- 常量枚举 `const enum A {...}`, 编译后不会生成任何代码, 会删除 `TS` 部分内容, 对于使用到的成员只会进行值的替换

- 由此可见, 使用 `常量枚举` 会有更好的性能, 避免额外的性能开销
- https://juejin.cn/post/7305473943572643877



**数组去重有哪些实现方法**

- 使用 lodash 里面的 uniq 或者 uniqBy：https://www.lodashjs.com/docs/lodash.uniqBy



**TS 中 interface和 type 区别**

- 总体来说，`interface` 更适合用于面向对象编程，特别是在类的设计和继承中。`type` 更加灵活，适用于更复杂的类型组合和类型别名的场景。在大多数项目中，`interface` 和 `type` 是可以互补使用的。

- 根据多个层面和应用场景进行介绍：https://www.codecrack.cn/zh/typescript/type-and-interface-differences-in-typescript



**React 中 setState 到底是异步还是同步**

- 合成事件和生命周期里，setState 是异步的（因为 React 批量更新优化，等事件执行完后再更新）

- 原生事件 和 setTimeout 里，setState 是同步的（没有批量更新）

- 需要最新的 state，用 prevState 回调

- https://juejin.cn/post/7250357906712838205#heading-3



**说一说 `==`、`===` 和 `Object.is` 的区别**

- `==`：会进行隐式类型转换

- `===`：不会隐式转换，严格类型判断。但是 `+0 === -0`、`NaN !== NaN`

- `Object.is`：解决了 `+0 === -0`、`NaN !== NaN` 的问题！更加标准化判断

- https://blog.csdn.net/MRlaochen/article/details/118557765



**什么是显式类型转换和隐式类型转换**

- 学习文档里面有，复习顺序是显式类型转换->运算符->隐式类型转换
- 简单文档：https://vue3js.cn/interview/JavaScript/type_conversion.html



## 第九节

**React18 有什么新特性**

- https://juejin.cn/post/7290815534207189033



**为什么有时候⽤ translate 来改变位置⽽不是 position 定位**

- https://juejin.cn/post/6905539198107942919#heading-13



**SPA首屏加载速度慢的怎么解决**

- https://vue3js.cn/interview/vue/first_page_time.html



**SSR 解决了什么问题，有做过 SSR 吗**

- https://vue3js.cn/interview/vue/ssr.html



**讲一讲 Redux 的概念和使用**





# 第二章 算法与手写

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



# 第三章 难点与经验

## 小智问卷

- 介绍项目

首先进入全部问卷，展示我的列表卡片渲染，讲解一下这里展示了当前用户所有的问卷信息列表，展示卡片的所有按钮，列表实现了响应式排列、顶部可通过过滤条件获取问卷列表。展示星标问卷、回收站等页面。

讲解项目中封装了全局弹窗组件，点击个人中心进行展示。然后退出登录，展示用户登录页和注册页，讲解发送验证码的使用，前端封装了滑动验证的模态框，后端实现了阿里云手机发送验证码业务。

之后页面展示问卷编辑器，选中画布上的问卷组件即可修改组件的信息。展示左侧添加可复用的问卷组件。展示拖拽排序，展示上方编辑器工具栏。点击发布问卷，展示问卷统计页面和图表信息。

点击投放问卷进入答卷表单页面，回答一个表单后提交即可，演示到此结束。



- 为什么想做这样一个项目

毕业设计、接触过问卷系统的使用、开发一套实用性网站系统、用到自己学过的技术栈、全栈开发、巩固编程能力



- 问卷编辑器开发

首先第一个难点就是问卷编辑器的开发，不仅要配置问卷组件数据结构，使其能够灵活扩展和复用。另外还要便于大量问卷数据进行存储。图层、画布、属性表单，三者的数据如何联动？

1. `src/components/QuestionGenerator/QuestionCheckbox/components/Component.tsx` 组件负责画布展示
2. `src/components/QuestionGenerator/QuestionCheckbox/components/PropComponent.tsx` 组件负责提供属性表单
3. `src/views/EditQuestion/index.tsx` 页面组件只需根据问卷生成器提供的问卷配置进行规范的渲染即可
4. 然后前端只需维护好的问卷组件列表 `questionComInfoList`，调用保存接口时返回给后端存储即可



- 答卷表单的开发

首先是基于 Antd 的 From 进行了二次封装，使得无需编写冗余的 tsx 代码只需要一份简单的配置对象即可一键式生成一份表单。然后再在答卷生成页面 `src/views/AnswerForm/components/FormWrapper.tsx` 中编写了一个函数进行问卷组件类型到表单组件类型的映射，从而利用 `questionComInfoList` 一键式生成答卷表单





## 合思档案

关于公司项目能学到的经验就是：

1. 首次接触到企业级别的大型项目，从搭建开发环境到项目运行起来踩了一点坑但也学到的经验。

2. 公司是进行多人开发的，于是针对 Git 的掌握程度也得到了提高，熟悉了常用的分支操作、合并操作、处理冲突还有发版提交
3. 学习了丰富的组件封装思想，像复杂的页面级通用表格组件还有根据后端返回的档案数据动态生成页面级查询组件
4. 学到了与后端进行接口联调的经验，更深入的了解了从反向代理到接口响应的流程
5. 参与了产品需求迭代的周期性开发，有了和产品、测试修复缺陷的沟通经验



## 公务云平台





# 第四章 非技术面

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



# 第五章 面试记录

- 大智慧（1000-9999）技术一面

```ts
// node事件循环机制和浏览器有什么不同
// 数组去重有哪些实现方法
// 判断一个对象（直接判断内部的值）是否相等
// react 的useMemo和useCallback传入多个依赖变量应该如何进行性能优化
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
// 如何实现拖拽排序，底层原理是什么，哪些html标签支持拖拽
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

