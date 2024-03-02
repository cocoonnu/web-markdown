# 第一章 前端问卷系统开发

项目底层依赖一个公司前辈搭建一套代码，已具备代码检查、状态管理、路由导航、路由拦截、请求拦截、反向代理、全局弹窗配置、组件库初始化等基础配置，依赖的源码地址如下：https://github.com/cocoonnu/questionnaire-survey-web/tree/87716d40c2b3842bdd2eb9afcd3a5f4243df7ae5



## 1.1 项目初始化搭建指南

项目初始化主要学习一下 Webpack5 项目的搭建（包括前端环境搭建、底层代码打包、环境变量导出、静态资源加载、各种开发语言的支持等），Prettier、Eslint 和 Husky 搭配实现代码检查，React 主架构搭建（包括依赖包安装、组件库安装、React-Router 路由系统搭建、Zustand 状态管理库安装等），最后是一些常用工具库的安装（包括 Echarts、Axios、@ekd/enhance-layer-manager 等）



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





# 第二章 后端问卷系统开发