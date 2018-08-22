## 创建基于vue ssr的组件模版
> 基于webpack4，koa2, koa-webpack，vue ssr官网文档：https://ssr.vuejs.org/zh/

> [vue ssr组件模版库](https://github.com/yjh30/vue-ssr-component-tpl)

#### webpack4
- 配置mode选项（development, production）
- vue-loader/lib/plugin

```js
const VueLoaderPlugin = require('vue-loader/lib/plugin')
module.exports = {
  mode: 'development',
  plugins: [
    // 魔法插件
    new VueLoaderPlugin()
  ]
}
```

#### koa-webpack（webpack-dev-middleware and webpack-hot-client）
> 开发模式热更新，[完整代码](https://github.com/yjh30/vue-ssr-component-tpl/blob/master/build/setup-dev-server.js)

```js
  // dev middleware
  const clientCompiler = webpack(clientConfig)

  koaWebpack({
    compiler: clientCompiler
  })
  .then(middleware => {
    app.use(middleware)

    clientCompiler.plugin('done', stats => {
      stats = stats.toJson()
      stats.errors.forEach(err => console.error(err))
      stats.warnings.forEach(err => console.warn(err))
      if (stats.errors.length) return

      clientManifest = JSON.parse(readFile(
        middleware.devMiddleware.fileSystem,
        'vue-ssr-client-manifest.json'
      ))
      update()
    })
  })
```

#### koa2中间件构成
> [koa-compose](https://github.com/koajs/compose/blob/master/index.js)

```js
Promise.resolve(Promise.resolve(promise))
```

#### Promise题外话
```js
const p = new Promise((resolve, reject) => {
  reject()
})
p.catch(() => {})
console.log(p) // rejected promise

const p1 = new Promise((resolve, reject) => {
  reject()
}).catch(() => {})
console.log(p1) // resolved promise
```


