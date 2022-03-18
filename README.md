ssh-deploy-cli
前端轻量化部署脚手架，支持测试、预发、线上等多环境自动化部署，支持多环境配置扩展，配置好后仅需一条命令即可完成整个部署流程。


## 前提条件
确保可以通过ssh连接服务器

> node版本 >= 9.0.0

注：建议使用nvm进行node版本控制（[https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)）。

## 安装
全局安装 ssh-deploy-cli（建议不要安装在项目中）
```
npm ssh-deploy-cli -g
```

安装完成后，通过 `deploy -V` 或 `deploy --version` 查看当前安装版本，以确定是否安装成功。

```
deploy -V ｜ deploy --version
```

如若出现以下提示，通过 nvm 升级 Node 到 9.0.0 版本以上即可。
```
You ar using Node v8.15.1, but this version of fe-deploy requres Node >=9.0.0 .
Please upgrage your Node version.
```


## 使用
### 1.初始化部署模板
```
deploy init
```

### 2.配置部署环境
部署配置文件位于deploy文件夹下的`deploy.config.js`,
一般包含`dev`（测试环境）、`pre`（预发环境）和`prod`（线上环境）三个配置，再有多余的环境配置形式与之类似，如果只有一个环境，则可以删除另一个多余的配置（比如只有`prod`线上环境，请删除`dev`测试环境配置）。

具体配置信息请参考配置文件注释：
```
module.exports = {
  projectName: 'xxx',         // 项目名称
  dev: {                                // 测试环境
    name: '测试环境',
    script: "npm run build-dev",        // 测试环境打包脚本
    host: '10.240.176.99',              // 开发服务器地址
    port: 22,                           // ssh port，一般默认22
    username: 'root',                   // 登录服务器用户名
    password: '123456',                 // 登录服务器密码
    distPath: 'dist',                   // 本地打包dist目录
    webDir: '/var/www/html/dev/i18n',   // 测试环境服务器地址
  },
  pre: {                                // 预发环境
    name: '预发环境',
    script: "npm run build-dev",        // 预发环境打包脚本
    host: '10.240.176.99',              // 开发服务器地址
    port: 22,                           // ssh port，一般默认22
    username: 'root',                   // 登录服务器用户名
    password: '123456',                 // 登录服务器密码
    distPath: 'dist',                   // 本地打包dist目录
    webDir: '/var/www/html/dev/i18n',   // 预发环境服务器地址
  },
  prod: {                               // 线上环境
    name: '线上环境',
    script: "npm run build",            // 线上环境打包脚本
    host: '10.240.176.99',              // 开发服务器地址
    port: 22,                           // ssh port，一般默认22
    username: 'root',                   // 登录服务器用户名
    password: '123456',                 // 登录服务器密码
    distPath: 'dist',                   // 本地打包dist目录
    webDir: '/var/www/html/prod/i18n'   // 线上环境服务器地址
  }
  // 其他环境，参照这个格式即可
}
```

### 3.查看部署命令
配置好`deploy.config.js`，运行
```
deploy --help
```
查看部署命令

### 4.测试环境部署
测试环境部署采用的时`dev`的配置
```
deploy dev
```
先有一个确认，确认后进入部署流程，完成6步操作后，部署成功！！！


### 5.线上环境部署
线上环境部署采用的时`prod`的配置
```
deploy prod
```
部署流程和测试环境相同：

## 接入
