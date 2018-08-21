## 搭建npm私有服务器verdaccio

> 官方文档：https://verdaccio.org/docs/en/configuration

#### 安装verdaccio
```bash
npm install -g verdaccio
```

#### 在linux机器上创建针对verdaccio的用户
```bash
sudo adduser npmuser
sudo su npmuser // 切换用户
sudo passwd vmikuko@123 // 修改密码
```

#### 启动verdaccio服务
```bash
sudo npm install -g forever
forever start `which verdaccio`
```

#### 电脑重启后重启verdaccio服务
```bash
crontab -e
```

#### 查看/修改verdaccio配置
```bash
cat/vi ~/.config/verdaccio/config.yaml
```

#### 默认配置
```
storage: ./storage
auth:
  htpasswd:
    file: ./htpasswd
uplinks:
  npmjs:
    url: https://registry.npmjs.org/
packages:
  '@*/*':
    access: $all
    publish: $authenticated
    proxy: npmjs
  '**':
    proxy: npmjs
logs:
  - {type: stdout, format: pretty, level: http}
```
