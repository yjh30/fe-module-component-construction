## 搭建kkl-cli脚手架
1、安装辅助模块
```bash
npm i -S commander inquirer handlebars ora chalk shelljs
```

2、创建步骤

- 确定是否生成项目
- 获取用户输入package包字段信息（目录名，项目描述，仓库地址）
- 克隆组件模版仓库
- 更新README.md


3、使用kkl-cli
安装
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
npm publish
```

