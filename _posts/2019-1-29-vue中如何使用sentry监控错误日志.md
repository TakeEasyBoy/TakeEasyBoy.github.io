---
layout: post
author: chao
title: vue中如何使用Sentry进行错误日志监控
---
vue中使用**Sentry**进行js错误日志监控

[sentry官网](https://sentry.io)
[官方文档传送门](https://docs.sentry.io/clients/javascript/integrations/vue/)
使用github账号登陆,新建一个组织,然后新建项目,

### 安装插件
```
cnpm i raven-js -S
```
### 使用
```
/main.js
import Vue from 'vue';
import Raven from 'raven-js';
import RavenVue from 'raven-js/plugins/vue';

const sentyDSN = process.env.NODE_ENV === 'test' ?
                'https://生成的api-test':
                'https://生成的api-prod'
process.env.NODE_ENV === 'test' && Raven.config(
	sentyDSN,  //
	{
		environment: process.env.NODE_ENV
	},
	{
		release:'staging@1.0.1'
	}
	)
	.addPlugin(RavenVue, Vue)
	.install()
// 注意,一定记得区分开发环境,否则开发环境的错误也会被提交到sntry去,并且本地是不会显示错误信息的
if(process.env.NODE_ENV !== 'development' ){
	Vue.config.errorHandler = function(err, vm, info) {
		Raven.captureException(err)
	}
}

new Vue({
  el: '#app',
  router,
  store, //将store注册到vue实例中
  template: '<App/>',
  components: { App }
})

```

# vue配合webpack中使用sentry错误日志系统

使用**sentry-webpack-plugin**,自动将生成的js map文件上传
[sentry官网](https://github.com/getsentry/sentry-webpack-plugin)


## webpack.prod.conf配置

```
安装 cnpm i @sentry/webpack-plugin -D
```

```
const SentryPlugin = require('@sentry/webpack-plugin')
new SentryPlugin({
  release: "staging@1.0.1",                           //发布的版本
  include: path.join(__dirname,'../dist/static/js/'), //需要上传到sentry服务器的资源目录,会自动匹配js 以及map文件
  ignore: ['node_modules', 'webpack.config.js'],  //  忽略文件目录,当然我们在inlcude中制定了文件路径,这个忽略目录可以不加
  configFile :`${__dirname}/sentry.properties`,   //  使用了类似于java的properties配置文件,里面包含了 -o组织 -p项目 以及authtoken
  urlPrefix : "~/static/js"           //  线上对应的url资源的相对路径 比如我的域名是 http://mydomin.com/,静态资源都在 static文件夹里面,
}),
```


## configfile:sentry.properties

```
# 生成的token
auth.token=61fbcb5798db46f7970dfb7aacc30389b72828188dfb493a9955a3141693d18d
# 默认的上传地址
defaults.url=https://sentry.io/
# 组织名
defaults.org=yunhe
# 项目名
defaults.project=vue_test
```
