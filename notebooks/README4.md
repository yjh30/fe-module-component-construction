## 搭建kkl-cli脚手架
> [仓库地址](https://github.com/yjh30/kkl-cli)

1、安装辅助模块
```bash
npm i -S commander inquirer handlebars ora chalk shelljs
```

2、创建步骤

- 确定是否生成项目
- 收集用户输入package包字段信息（项目名，项目描述，仓库地址）
- 克隆组件模版仓库
- 更新package.json，将收集到的用户输入字段填充package.json
- 更新README.md，描述组件的介绍，安装，使用（需用户后续自行完善）
- 本地初始化.git目录，切换为组件目录并执行git init进行初始化，服务于第三方githooks或husky模块
- 选择是否进行npm install
- 生成项目成功输出提示

3、安装kkl-cli

```bash
npm view kkl-cli // 查看最新发布的版本
npm list kkl-cli // 查看本地安装版本
npm i -g kkl-cli@latest // 安装最新版本
```

4、初始化组件项目
```bash
kkl init kkl-ui-swipe-gesture
cd kkl-ui-swipe-gesture
npm i
```

5、发布私有npm组件包

发布之前，你需要设置私有npm注册地址 & 注册私有npm账户
```bash
npm set registry http://10.0.1.100:4873
npm adduser --registry http://10.0.1.100:4873

cd myProject
npm publish
```

