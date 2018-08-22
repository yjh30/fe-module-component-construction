## 代码美化及提交规范

#### 1、使用 [prettier](https://prettier.io/docs/en/) 美化代码
优点：相对eslint自动对代码进行美化，团队无须为规则、习惯争议，适合团队编码规范
结合eslint
```bash
npm i -D prettier eslint-plugin-prettier eslint-config-prettier
```
```js
// .eslilntrc.js
module.exports = {
  "plugins": ["plugin:prettier/recommended"],
  "rules": {
    "prettier/prettier": "error"
  }
}
```
结合ghooks & lint-staged
```bash
npm i -D ghooks lint-staged
```
```js
// package.json
"config": {
  "ghooks": {
    "pre-commit": "lint-staged"
  }
},
"lint-staged": {
  "./src/**/*.{js,vue}": [
    "./node_modules/.bin/eslint --fix",
    "./node_modules/.bin/prettier --write",
    "git add"
  ]
}
```

#### 2、commit提交流 支持Angular的Commit message格式
> [Angular规范](https://github.com/angular/angular/blob/master/CONTRIBUTING.md#-commit-message-guidelines)

安装方式1:
```bash
npm i -g commitizen
commitizen init cz-conventional-changelog --save --save-exact
```
安装方式2:
```bash
npm i -D cz-conventional-changelog
```
```js
// 手动配置 package.json
"config": {
  "commitizen": {
    "path": "./node_modules/cz-conventional-changelog"
  }
}
```

#### 3、验证Commit message规范
```bash
npm i -D validate-commit-msg
```
```js
// package.json
"config": {
  "ghooks": {
    "commit-msg": "validate-commit-msg"
  }
}
```

#### 4、生成changelog
安装conventional-changelog-cli
```bash
npm i -D conventional-changelog-cli
```
不重写之前的previous changelog
```bash
node_modules/.bin/conventional-changelog -p angular -i CHANGELOG.md -s
```
重写之前的previous changelog
```bash
node_modules/.bin/conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

#### 5、package.json完整配置
```js
"scripts": {
  "changelog": "node_modules/.bin/conventional-changelog -p angular -i CHANGELOG.md -s -r 0"
},
"config": {
  "commitizen": {
    "path": "./node_modules/cz-conventional-changelog"
  },
  "ghooks": {
    "pre-commit": "lint-staged",
    "commit-msg": "validate-commit-msg"
  }
},
"lint-staged": {
  "./src/**/*.{js,vue}": [
    "./node_modules/.bin/eslint --fix",
    "./node_modules/.bin/prettier --write",
    "git add"
  ]
}
```

备注：husky 与 githooks模块勿混用(只安装一个)，否则导致githooks配置失效，删除node_modules重新安装
