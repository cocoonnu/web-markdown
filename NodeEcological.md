# 第一章 Nodejs 环境配置

## 1.1 安装 NVM 管理版本

**安装方式如下：**

- 参考文章：https://zhuanlan.zhihu.com/p/646970780

- 如果之前安装过 Nodejs 那么一定要卸载！不管是 C 盘还是 D 盘，然后还有自定义的环境变量也一并删除！
- 安装 NVM 最新版：https://github.com/coreybutler/nvm-windows/releases
- 安装目录都选择 D 盘，默认已经帮我们配好了 NVM、Nodejs 的环境变量
- 切换镜像源：
  1. 打开 NVM 的安装目录里面的 setting.txt 写入 `node_mirror: https://npmmirror.com/mirrors/node/`
  2. 或者执行命令：`nvm node_mirror https://npmmirror.com/mirrors/node/`（阿里云）



**NVM 的所有命令：**

```bash
$ nvm v                       # 显示nvm版本
$ nvm off                     # 禁用node.js版本管理(不卸载任何东西)
$ nvm on                      # 启用node.js版本管理
$ nvm install <version>       # 安装node.js的命名 version是版本号
$ nvm uninstall <version>     # 卸载node.js是的命令，卸载指定版本的nodejs，当安装失败时卸载使用
$ nvm ls                      # 显示所有安装的node.js版本
$ nvm list available          # 显示可以安装的所有node.js的稳定版本
$ nvm use <version>           # 切换到使用指定的nodejs版本
$ nvm install stable          # 安装最新稳定版
$ nvm alias default 14.10.0   # 设置环境默认node版本
```



**两个注意点：**

- 有了 NVM 之后，千万不要再去使用 Nodejs 安装包安装其他版本
- 使用 NVM 切换 Nodejs 版本之后，每个版本的全局包都独立，切换版本后需要再另外下载
- npm 和 Nodejs 进行了捆绑，切换 Nodejs 版本会自动切换 npm 的版本



**根据项目自动切换版本**

- 进入 `.zshrc` 添加以下脚本：

  ```bash
  autoload -U add-zsh-hook
  load-nvmrc() {
    local node_version="$(nvm version)"
    local nvmrc_path="$(nvm_find_nvmrc)"
    if [ -n "$nvmrc_path" ]; then
      local nvmrc_node_version=$(cat "$nvmrc_path")
      if [ "$nvmrc_node_version" != "$node_version" ]; then
        nvm use --silent "$nvmrc_node_version"
      fi
    fi
  }
  add-zsh-hook chpwd load-nvmrc
  load-nvmrc
  ```

- 在项目中添加 `.nvmrc` 文件即可打开终端是自动使用 NVM 切换指定的版本

  ```
  v18.16.0
  ```



**npm 常用命令：**

- `npm init -y` ：初始化一个 package.json 文件
- `npm i` 或 `npm install` ：安装项目中所有依赖，`npm i --force` 强制安装依赖
- `npm uninstall [package name]`：卸载项目中的依赖
- `npm update [package name]`：升级项目中的依赖
- `npm i [package name] -S/--save`：安装到 dependencies（生产环境）
- `npm i [package name] -D/--save-dev`：安装到 devDependencies（开发环境） 
- `npm install -global/-g <package name>`：全局安装依赖




## 1.2 使用 NRM 切换镜像源

可以直接使用 npm 命令来查看或者设置当前 npm（包括 yarn） 的镜像源：

```bash
# 查看当前的下载包镜像源
$ npm config get registry

# 将下载包镜像源切换为淘宝镜像源
$ npm config set registry=https://registry.npm.taobao.org
```



或者下载一个全局的工具 NRM 来进行镜像源的管理：`npm i nrm -g`

**注意是直接切换全局的镜像源，包括 npm、yarn**

```bash
$ nrm add <registry> <url>  # 添加一个镜像源，通常是公司内部镜像源

$ nrm use <registry>  # 切换镜像源

$ nrm del <registry> # 删除镜像源

$ nrm ls # 列出所有镜像源
```



**注意：切换成 nrm 镜像源之后不一定成功，因为如果项目中存在 .npmrc 或者 .yarnrc 则以这个配置文件的镜像源为准**




## 1.3 常用的包管理工具

### 1.3.1 YARN
官网：https://chore-update--yarnpkg.netlify.app/zh-Hans/

全局安装：`npm i yarn -g`，切换 Nodejs 版本之后需要另外再下载



**常用命令**

```bash
$ yarn init # 同npm init，执行输入信息后，会生成package.json文件

$ yarn install # 安装package.json里所有包，并将包及它的所有依赖项保存进yarn.lock
$ yarn install --flat # 安装一个包的单一版本
$ yarn install --force # 强制安装

$ yarn remove <packageName> # 删除一个包

$ yarn upgrade <packageName>@<version> # 更新一个包的指定版本

$ yarn add <packageName> # 安装一个包的最新版本

$ yarn config set registry http://registry.npm.taobao.org/ # 设置镜像源

$ yarn global add typescript # 全局下载命令（最好使用npm下载全局包）
```



**.yarnrc**

在本地系统中的位置：/Users/cocoon/.yarnrc，另外在单独的项目中也可以配置。通常用于指定这个项目的镜像源，因此无需使用 nrm 来回进行镜像源的切换。还可以指定某个第三方库单独的镜像源：

```
registry "https://npm.ekuaibao.com/"
"@ant-design:registry" "https://registry.npmmirror.com/"
```



**安装本地  tgz**

如果你有一个本地第三方库 tgz，你可以通过一下命令来安装：

```bash
$ yarn add file:./enhance-layer-manager-7.0.3.tgz

$ yarn add file:/Users/cocoon/Downloads/enhance-layer-manager-7.0.3.tgz
```



### 1.3.2 PNPM

使用 pnpm 最少需要 node18.12 以上的版本，另外 pnpm 优点有很多，十分推荐！
| 功能 | npm / yarn | pnpm |
|------|------------|------|
| 初始化项目 | `npm init` / `yarn init` | `pnpm init` |
| 安装依赖（写入 dependencies） | `npm install xxx` / `yarn add xxx` | `pnpm add xxx` |
| 安装依赖（写入 devDependencies） | `npm install xxx -D` / `yarn add xxx -D` | `pnpm add xxx -D` |
| 安装全局依赖 | `npm install -g xxx` / `yarn global add xxx` | `pnpm add -g xxx` |
| 卸载依赖 | `npm uninstall xxx` / `yarn remove xxx` | `pnpm remove xxx` |
| 更新依赖 | `npm update xxx` / `yarn upgrade xxx` | `pnpm update xxx` |
| 安装项目所有依赖 | `npm install` / `yarn install` | `pnpm install` |
| 运行脚本 | `npm run dev` / `yarn dev` | `pnpm dev` |
| 清缓存 | `npm cache clean --force` / `yarn cache clean` | `pnpm store prune` |
| 查看全局依赖 | `npm list -g --depth=0` | `pnpm list -g --depth=0` |



## 1.4 Node 环境问题总结

### 1.4.1 JS 内存编译过载

编译时出现问题：`FATAL ERROR: Reached heap limit Allocation failed - JavaScript heap out of memory`，说明 JS 内存编译过载

只要加大 JS 内存即可：`NODE_OPTIONS="--max-old-space-size=8192"` ，设置好环境变量即可

参考文章：https://blog.csdn.net/m0_38137988/article/details/131554880

```bash
$env:NODE_OPTIONS="--max-old-space-size=8192"
```



### 1.4.2 npx 的使用和理解

`npx` 为 `npm` 内置的命令，一个 `CLI` 工具，用于执行项目中环境包或者全局里 `bin` 目录的可执行命令。此外还可以执行在线 `npm` 库里的可执行命令，因此不用全局下载环境包避免占用存储和污染环境。

`npm run` 命令主要是执行项目中 `package.json` 的脚本命令 `scripts`，其实就是用户自定义命名的自定义的命令

```bash
npx create-react-app@latest my-project
```

```bash
npm run dev
```



### 1.4.3 Eslint 配置不生效

在项目安装依赖的环节通常需要严格匹配 node 版本和装包软件，比如公司项目严格按照 node16 和 cnpm 下载依赖，cnpm 装包的时候会忽略各个依赖之间的冲突和兼容行，类似于强制安装了



### 1.4.4 安装依赖需要注意的点

首先确定自己的 node 版本和 react 版本，不能直接下载最新的包！

当依赖下载完后如何要降版本则会出现很多奇怪的 bug，所以依赖只能升而不能降！



# 第二章 Nodejs 基础学习

Nodejs 基础学习（博客）：https://www.inode.club/node/what.html

Nodejs 遵循 Commonjs 模块化开发：

1. 使用 `module.exports` 或 `export` 导出

```ts
module.exports.name = 'cocoon';
module.exports = {
    name: 'cocoon',
    say() {
        console.log(module.exports.name);
    }
}
```

2. 使用 require 进行导入：`const obj = require('./module')`



## 2.1 path 模块学习

path 模块学习：https://juejin.cn/post/7176102367723520056

1. `path.join`：只作为路径字符串拼接，`path.resolve`：把路径解析最终生成绝对路径
2. `__dirname`：全局变量，表示当前执行文件所在目录的完整目录名
3. `__filename`：全局变量，表示当前执行文件所在目录的完整文件名

```js
// 获取当前文件目录下的index.ts的绝对路径
const resolvePath = path.resolve(__dirname, './index.ts');
```



## 2.2 全局环境变量配置

在 Nodejs 中通常从 `process.env` 获取环境变量，全局可使用



**使用 dot-env 载入环境变量**

1. 在 `.env`、`.env.development`、`.env.local` 中定义环境变量，通过 dot-env 入口读取
2. 参考文档：https://juejin.cn/post/6993224664705138702

```js
// config/env.js
const path = require("path");
const fs = require("fs");
const dotEnv = require("dotenv");

// 先构造出.env*文件的绝对路径
const appDirectory = fs.realpathSync(process.cwd());
const resolveApp = (relativePath) => path.resolve(appDirectory, relativePath);
const pathsDotenv = resolveApp(".env");

// 按优先级由高到低的顺序加载.env文件
dotEnv.config({ path: `${pathsDotenv}.local` })  // 加载.env.local
dotEnv.config({ path: `${pathsDotenv}.development` })  // 加载.env.development
dotEnv.config({ path: `${pathsDotenv}` })  // 加载.env

// 打印一下此时的process.env
console.log(process.env.NAME); // zhangsan
console.log(process.env.AGE); // 20
console.log(process.env.COUNTRY); // China
console.log(process.env.LOCAL_ENV); // local
```



**使用 cross-env 注入环境变量**

1. 运行跨平台设置和使用环境变量的脚本，在启动脚本时注入环境变量
2. 参考文档：https://juejin.cn/post/7088493140205633544

```bash
npm install --save-dev cross-env
```

```json
"scripts": {
  "build": "cross-env NODE_ENV=production webpack --config build/webpack.config.js"
}
```

```ts
process.env.NODE_ENV = 'production'
```



## 2.3 进程与线程学习

进程与线程（太难太枯燥了）：https://www.inode.club/node/processAndThread.html

process 对象：https://juejin.cn/post/6913498911973834759

cluster、child_process 进程相关模块学习：https://juejin.cn/post/7202809170378522680

本章主要是过一下 process 对象暴露的 API 的一些使用和学习

```ts
process.argv、process.nextTick(fn)、process.env、process.stdin、process.stdout、process.memoryUsage、process.uptime
```



## 2.4 Stream 模块学习

流（Stream）是一个抽象的数据接口，`Node.js` 中很多对象都实现了流，流是 `EventEmitter` 对象的一个实例，总之它是会冒数据（以 `Buffer` 为单位），或者能够吸收数据的东西，它的本质就是让数据流动起来

1. `source.pipe(dest)`，`source` 和 `dest` 就是通过 pipe 连接，让数据从 `source` 流向了 `dest`。

2. 参考文档：https://www.inode.club/node/stream.html



**以上传文件作为一个简单案例**

```ts
const http = require('http')
const fs = require('fs')
const path = require('path')

const server = http.createServer(function(req, res) {
  const fileName = path.resolve(__dirname, 'data.txt')
  let stream = fs.createReadStream(fileName) // stream -> source（数据端）
  stream.pipe(res) // res -> dest（读入数据端）
})
server.listen(8000)
```



**一个通过 post 请求微信小程序的地址生成二维码的需求**

1. 通过请求得到一个二维码文件流，然后流入指定的文件中
2. response 也是一个 stream 对象，作为 source，流入 ws 中

```ts
/*
 * 微信生成二维码接口
 * params src 微信url / 其他图片请求链接
 * params localFilePath: 本地路径
 * params data: 微信请求参数
 * */
const downloadFile = async (src, localFilePath, data) => {
  try {
    const ws = fs.createWriteStream(localFilePath)
    return new Promise((resolve, reject) => {
      ws.on('finish', () => {
        resolve(localFilePath)
      })
      if (data) {
        request({
          method: 'POST',
          uri: src,
          json: true,
          body: data,
        }).pipe(ws)
      } else {
        request(src).pipe(ws)
      }
    })
  } catch (e) {
    logger.error('wxdownloadFile error: ', e)
    throw e
  }
}
```



**一个文件拷贝的例子**

```ts
const fs = require('fs')
const path = require('path')

// 两个文件名
const fileName1 = path.resolve(__dirname, 'data.txt')
const fileName2 = path.resolve(__dirname, 'data-bak.txt')
// 读取文件的 stream 对象
const readStream = fs.createReadStream(fileName1)
// 写入文件的 stream 对象
const writeStream = fs.createWriteStream(fileName2)
// 通过 pipe执行拷贝，数据流转
readStream.pipe(writeStream)
// 数据读取完成监听，即拷贝完成
readStream.on('end', function() {
  console.log('拷贝完成')
})
```



## 2.5 Buffer 对象学习

Buffer 介绍参考文档：https://www.inode.club/node/buffer.html

在 Node.js 中，Buffer 对象是用于处理二进制数据的类。以下是一些常用的 Buffer API：

1. `Buffer.alloc(size[, fill[, encoding]])`：创建一个指定大小的新的 Buffer 对象，并用指定的 fill 值填充。可选的 encoding 参数指定填充值的编码，默认为 'utf8'。

2. `Buffer.from(array)`：根据给定的数组创建一个新的 Buffer 对象。

3. `Buffer.from(string[, encoding])`：根据给定的字符串创建一个新的 Buffer 对象。可选的 encoding 参数指定字符串的编码，默认为 'utf8'。

4. `buffer.length`：返回 Buffer 对象的字节长度。

5. `buffer.toString([encoding[, start[, end]]])`：将 Buffer 对象转换为字符串。可选的 encoding 参数指定字符串的编码，默认为 'utf8'。可选的 start 和 end 参数指定要转换的字节范围，默认为整个 Buffer。

6. `buffer.toJSON()`：返回一个包含 Buffer 对象内容的 JSON 表示。

7. `buffer[index]`：获取或设置指定索引位置的字节值。

8. `buffer.slice([start[, end]])`：返回一个新的 Buffer 对象，包含原始 Buffer 对象的指定字节范围。可选的 start 和 end 参数指定字节范围，默认为整个 Buffer。

9. `buffer.copy(target[, targetStart[, sourceStart[, sourceEnd]]])`：将原始 Buffer 对象的内容复制到目标 Buffer 对象中。可选的 targetStart、sourceStart 和 sourceEnd 参数指定复制的字节范围，默认为整个 Buffer。

10. `Buffer.isBuffer(obj)`：检查一个对象是否为 Buffer 对象。



# 第三章 Webpack 基础学习

先把 `Webpack` 的一些基础配置和常用的 `loader`、`plugin` 过一遍，然后手动搭建项目实操一下。

中文文档官网：https://www.webpackjs.com/



## 3.1 Webpack 常用配置

### 3.1.1 入口和上下文

上下文 `context` 定义入口文件所处目录的绝对路径的字符串，默认使用 Node.js 进程的当前工作目录

https://www.webpackjs.com/configuration/entry-context/#context

```js
context: path.resolve(__dirname, 'app') // 使得从当前工作目录的app目录下开始查找
```



入口 `entry` 定义开始应用程序打包过程的一个或多个起点，单页应用：一个入口起点，多页应用：多个入口起点

作为一个对象时，其一个对象属性即作为一个 `chunk` 的入口，对象属性中又有：`import`、`filename`、`depenOn` 等属性

https://www.webpackjs.com/configuration/entry-context/#entry

```js
// 只有一个入口文件，默认打包一个chunk为main.js
entry: './src/index.js'
```

```js
// 会打包多个 chunk：home、shared、catalog
entry: {
  home: './home.js',
  shared: ['react', 'react-dom', 'redux', 'react-redux'],
  catalog: {
    import: './catalog.js',
    filename: 'pages/catalog.js',
    dependOn: 'shared',
    chunkLoading: false,
  },
}
```



### 3.1.2 output 输出配置

`output` 指示 `webpack` 如何去输出、以及在哪里输出你的「`bundle` 和其他你所打包或使用 `Webpack` 载入的任何内容」

https://www.webpackjs.com/configuration/output/

```js
output: {
  filename: "bundle.js",
  path: path.resolve(__dirname, "dist"),
  clean: true,
  publicPath: 'assets/',
}
```



### 3.1.3 构建模式 mode

提供 `mode` 配置选项，告知 `Webpack` 使用相应模式的内置优化，并会将 `process.env.NODE_ENV` 同步设置

https://www.webpackjs.com/configuration/mode/

```bash
npm run weback --mode=development
```

```js
module.exports = (env, argv) => {
  config.mode = argv.mode
  if (argv.mode === 'development') {
    config.devtool = 'source-map'   	
  }
  return config
}
```



### 3.1.4 控制 source map

通过属性 `devtool` 控制是否生成，以及如何生成 `source map`，生成 `map` 文件有利于开发环境调试，而生产环境则不需要

https://www.webpackjs.com/configuration/devtool/



### 3.1.5 代理配置 devServer

通过 `webpack-dev-server` 这个库进行快速启动一个开发应用程序，通过 `http-proxy-middleware` 可实现反向代理，两个配置都在 `devServer` 中编写即可。具体配置查文档就行：https://www.webpackjs.com/configuration/dev-server/



## 3.2 Webpack 常用加载

### 3.2.1 加载样式文件

当样式文件被入口文件引入时，需要给 `Webpack` 配置 `Loader` 才能打包成功

`CSS`、`Sass`、`Less` 文件加载，并且 `Loader` 数组的顺序不能改变



```bash
npm install less sass
npm install --save-dev css-loader style-loader
npm install --save-dev sass-loader less-loader
```

```js
module: {
  rules: [
    {
      test: /\.css$/,
      use: ['style-loader', "css-loader"],
    },
    {
      test: /\.s[ac]ss$/i,
      use: ['style-loader', "css-loader", "sass-loader"],
    },
  ],
},
```



## 3.3 Webpack 基础优化策略

这里只讲基础优化不会深入，优化可以从两个方面入手：1. 开发环境构建速度 2. 生产环境构建体积和缓存策略。这里推荐一篇 webpack 实际上手的文章，优化策略都是按一个一个的点来描述和配置的：https://juejin.cn/post/7111922283681153038#heading-18

------





# 第四章 前端工程化总结

https://github.com/cocoonnu/web-projects/blob/main/Markdown/React%20ecology/React-Project.md
