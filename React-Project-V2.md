# 第一章 多功能问卷系统开发

开源工具库收集：

dnd-kit 可拖拽组件：https://juejin.cn/post/7163620889924206629



## 1.1 项目初始化构建

项目初始化主要学习一下 Webpack5 项目的搭建（包括前端环境搭建、底层代码打包、环境变量导出、静态资源加载、各种开发语言的支持等），Prettier、Eslint 和 Husky 搭配实现代码检查，React 主架构搭建（包括依赖包安装、组件库安装、React-Router 路由系统搭建、Zustand 状态管理库安装等），最后是一些常用工具库的安装（包括 Echarts、Axios、@ekd/enhance-layer-manager 等）

> 下面的项目笔记书写顺序不一定按上面描述顺序来写



### 1.1.1 封装全局监听实例

首先我想开始学习封装一个全局监听实例 app 对象。用到的依赖是：`@ekuaibao/messagecenter`，其导出的 MessageCenter 类。然后在根组件位置引入一个  GlobalWatchEvent 全局监听组件。即可实现发布全局的发布订阅。**监听实例优点：**当有些函数或者 hook 只能在函数组件中使用时，利用这个实例可以实现在组件外也可以了



我们在任意页面任务组件调用触发：

```ts
// 触发事件和传入函数参数，无法获取函数返回值
app.emit(EVENT_NAME.globalTestEvent, { name: 'cocoon' })

// 可获取函数返回值，但是返回结果为异步的
const res = await app.invoke(EVENT_NAME.globalTestEvent, { name: 'cocoon' })
```



src/utils/tools/app_utils.ts

```ts
import MessageCenter from '@ekuaibao/messagecenter'

class AppContext extends MessageCenter {
  ......
}

const app = new AppContext()
export { app }
```



src/main/components/GlobalWatchEvent.tsx

```tsx
import React, { useEffect } from 'react'
import { app } from '@/utils/tools/app_utils'
import { EVENT_NAME } from '@/consts/eventListener'

const GlobalWatchEvent = () => {
  useEffect(() => {
    app.watch(EVENT_NAME.globalTestEvent, globalTestEventFn) // 在这里监听事件
    return () => {
      app.un(EVENT_NAME.globalTestEvent, globalTestEventFn)
    }
  }, [])

  const globalTestEventFn = (params: any) => {
    console.log('globalTestEvent', params)
  }
  return <></>
}

export default GlobalWatchEvent
```



### 1.1.2 封装全局弹窗监听事件

上一节我们封装了一个全局监听的实例，这一节我们开始进阶：实现在任意组件中打开一个自定义的弹窗组件事件。

1. 首先我们要封装一个全局的监听组件放在根组件中，组件位置：src/main/components/GlobalLayerManager.tsx。这里引用了 `@ekd/enhance-layer-manager`，这个库来实现打开弹窗的效果。

```tsx
import React from 'react'
import { EnhanceLayerManager } from '@ekd/enhance-layer-manager'
import { routerLayerList } from '@/routers/routerList'
import { app } from '@/utils/tools/app_utils'
import { EVENT_NAME } from '@/consts/eventListener'
import type { ILayerManagerProps } from '@ekd/enhance-layer-manager'

@EnhanceLayerManager((props) => props.layers) // layers 为我们自定义的弹窗组件，由此得到一个 layerManager
class LayerManager extends React.Component<ILayerManagerProps & { layers: any }> {
  componentDidMount() {
    app.watch(EVENT_NAME['@@:open:layer'], this.handleOpenLayer) // 监听打开弹窗事件
    app.watch(EVENT_NAME['@@:close:layer'], this.handleCloseLayer) // 监听关闭弹窗事件
  }

  componentWillUnmount() {
    app.un(EVENT_NAME['@@:open:layer'], this.handleOpenLayer)
    app.un(EVENT_NAME['@@:close:layer'], this.handleCloseLayer)
  }

  handleOpenLayer = (key: string, props: any, isSingle?: boolean) => {
    const { layerManager } = this.props
    // 打开弹窗组件的代码，存入弹窗 key 和 组件参数 props
    return isSingle ? layerManager?.open(key, props) : layerManager?.push(key, props)
  }

  handleCloseLayer = () => {
    const { layerManager } = this.props
    layerManager?.close()
  }

  render() {
    return <></>
  }
}

const GlobalLayerManager = () => {
  return <LayerManager layers={routerLayerList} /> // 由这里传入弹窗组件匹配规则
}

export default GlobalLayerManager
```



2. 为了方便调用弹窗的监听事件，我们直接在 app 实例中封装两个方法 open、close，代码位置：src/utils/tools/app_utils.ts

```ts
class AppContext extends MessageCenter {
  open<T>(key: string, props?: any, ...params: any[]): Promise<T> {
    return this.invoke(EVENT_NAME['@@:open:layer'], key, props, ...params)
  }

  close(...params: any[]) {
    return this.invoke(EVENT_NAME['@@:close:layer'], ...params)
  }
}
```



3. 最后就是如何创建我们自定义的弹窗了，首先我们得写一份弹窗路径规则，然后就是自定义弹窗组件的封装

页面组件下新建 router.layers.ts，参数可以直接参考 antd 的 ModalProps

```ts
import { getModelDefaultOptions } from '@/utils/layerOptions'
import type { ModelOptions } from '@/utils/layerOptions'

export default [
  {
    ...getModelDefaultOptions(),
    key: '@directory-specification:CreateGroupModal',
    title: '新建分组',
    width: 580,
    maskClosable: false,
    getComponent: () => import('./layers/DemoLayer'),
  },
] as ModelOptions
```

```tsx
import React from 'react'
import type { ILayerProps } from '@ekd/enhance-layer-manager'

const DemoLayer = ({ layer }: ILayerProps) => {
  const clickFn = () => {
    layer.emitOk({ hhh: 'hi' }) // 弹窗回调
  }

  return <div onClick={clickFn}>test</div>
}
export default DemoLayer
```

在项目任意位置调用事件即可：

```ts
const res = await app.open('@directory-specification:CreateGroupModal', { kk: 123 })
```



### 1.1.3 项目路由系统搭建

项目路由系统包含多个功能：页面缓存、页面切换、登录权限校验、路由组件懒加载等。接下来介绍路由系统底层是如何一步一步构建的。路由搭建的 API 主要还是使用 React-Router 提供，路由匹配使用 Routes 规则，而不是 useRoutes 路由表。

1. 第一步先得到文件路由表，代码位置：src/routers/routerList.ts

```ts
import type { IRoutersData } from './types'

// 全局根路由页面，已支持layout的path: '/app'
const globalRouterList: IRoutersData = [
  {
    path: '/',
    redirect: '/app/home',
  },
  {
    path: '/login',
    component: () => import('@/views/Login'),
  },
]

const files = require.context('../views', true, /(router|router.layers)\.(js|ts)$/)
const routerList: IRoutersData = [] // layout路由表
const routerLayerList: IRoutersData = [] // 弹窗组件匹配规则

files.keys().forEach((key) => {
  const child = files(key).default
  if (/router.layers/g.test(key)) {
    routerLayerList.push(...child)
    return
  }
  routerList.push(...child)
})

export { routerList, globalRouterList, routerLayerList }
```

```ts
// router.ts layout下的嵌套路由
import type { IRoutersData } from '@/routers/types'

export default [
  {
    path: '/app/home',
    component: () => import('@/views/Home'),
  },
] as IRoutersData
```



2. 第二步设计路由表组件 Routes，然后放在根组件下从而实现全局路由匹配。代码位置：`src/routers/index.tsx`

```tsx
class Routers extends React.Component<any, RoutersState> {
  render() {
    return (
      <Routes>
        {globalRouterList?.map((item) => {
          return interceptorRoute(item)
        })}
        {'这里定义了一个全局根路由layout'}
        <Route path="/app" element={<BaseLayout />}>
          {routerList.map((item) => {
            return interceptorRoute(item)
          })}
          <Route path="*" element={<NoMatch />} key="noMatch" />
        </Route>
        <Route path="*" element={<NoMatch />} key="noMatch" />
      </Routes>
    )
  }
}
```



3. 常用路由 API 和方法预览：React-Router 的 hooks 和组件外路由跳转：`src/utils/tools/router_utils.ts`





# 第二章 项目后端构建

## 2.1 Java 学习记录

### 2.1.1 面向对象编程学习

多态的概念：https://www.liaoxuefeng.com/wiki/1252599548343744/1260455778791232

> `Person p = new Student()` 一个实际类型为 Student，引用类型为 Person 的实例。多态具有一个非常强大的功能，就是允许添加更多类型的子类实现功能扩展，却不需要修改基于父类的代码。



`final`修饰符有多种作用：

- `final`修饰的方法可以阻止被覆写；
- `final`修饰的class可以阻止被继承；
- `final`修饰的字段必须在创建对象时初始化，随后不可修改。
- https://www.liaoxuefeng.com/wiki/1252599548343744/1260455778791232



面向抽象编程的本质就是：

- 上层代码只定义规范（例如：`abstract class Person`）；
- 不需要子类就可以实现业务逻辑（正常编译）；
- 具体的业务逻辑由不同的子类实现，调用者并不关心。
- https://www.liaoxuefeng.com/wiki/1252599548343744/1260456371027744



接口类型的定义：

- 如果一个抽象类没有字段，所有方法全部都是抽象方法，就可以把该抽象类改写为接口：`interface`。
- 在接口中，可以定义`default`方法，实现类时可以不必覆写`default`方法。

- https://www.liaoxuefeng.com/wiki/1252599548343744/1260456790454816



静态字段的定义：

- 在一个`class`中定义的字段，我们称之为实例字段。还有一种字段，是用`static`修饰的字段，称为静态字段.
- 调用实例方法必须通过一个实例变量，而调用静态方法则不需要实例变量，通过类名就可以调用。
- **因为静态方法不属于实例，因此，静态方法内部，无法访问`this`变量，也无法访问实例字段，它只能访问静态字段。**
- https://www.liaoxuefeng.com/wiki/1252599548343744/1260464690677856
