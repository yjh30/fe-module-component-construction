## 投入生产使用

#### 组件包名规范，私有前缀@kkl
- 通过kkl-cli生成的组件项目，包名为类似@kkl/ui-swipe-gesture，私有前缀@kkl/，为了避免与npm包名重名，同时区分为公司私有包

- 通过kkl-cli生成项目，输入项目名kkl-ui-popup，package.json包名配置为@kkl/ui-popup

#### vue模块化组件导出.vue文件
vue模块化组件导出.vue文件能够减少通过构建后组件文件的体积

#### 构建配置
// webpack.base.conf.js
```js
// 对私有npm组件进行转换
module.exports = {
  module: {
    rules: [{
        test: /\.vue$/,
        loader: 'vue-loader',
        options: vueLoaderConfig,
        exclude(modulePath) {
          if (modulePath.match(/@kkl/i)) {
            return false
          }
        }
    }]
  }
}
```
// webpack.server.config.js
```js
const nodeExternals = require('webpack-node-externals')
// 服务端构建排除node_modules中的私有npm包
module.exports = {
  mode: 'production',
  externals: nodeExternals({
    // 不要外置化 webpack 需要处理的依赖模块。
    // 你可以在这里添加更多的文件类型。例如，未处理 *.vue 原始文件，
    // 你还应该将修改 `global`（例如 polyfill）的依赖模块列入白名单
    whitelist: [/\.(css|vue)$/, /@kkl\/[0-9a-z]+/i]
  })
}
```