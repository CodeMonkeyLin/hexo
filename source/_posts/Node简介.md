---
title: NodeJS简介及使用
comments: true
date: 2018-06-13 17:29:46
tags:
    - nodejs
    - express
---

## Node.js是什么?
Node.js 是一种建立在Google Chrome’s v8 engine上的 non-blocking (非阻塞）, event-driven （基于事件的） I/O平台. Node.js平台使用的开发语言是JavaScript，平台提供了操作系统低层的API，方便做服务器端编程，具体包括文件操作、进程操作、通信操作等系统模块



## Node.js可以用来做什么？

* express/koa等）
* 即时通讯(socket.io)
* api（移动端，pc，h5）
* http proxy（淘宝首页）
* 前端构建工具(grunt/gulp/bower/webpack/fis3…)
* 写操作系统（NodeOS）
* 跨平台打包工具（以前叫Node-WebKit现在叫nw.js）
* 命令行工具（比如cordova）

## Nodejs相关管理体系

* 项目管理：npm,grunt
* Web开发：express,ejs,hexo, socket.io, restify, cleaver, stylus, browserify,cheerio
* 工具包：underscore,moment,connet,later,log4js,passport,passport(oAuth),domain,require,reap,
* 数据库：mysql,mongoose,redis
* 异步：async,wind
* 部署：pm2

## Express基本使用

* 静态服务器   
* 路由
* 中间件
* 模板引擎整合
* 常用API基本使用

## 图书管理系统构建
* 开启服务器
``` bash
    const express = require('express');
    const app = express();
    // 监听端口
    app.listen(3000,()=>{
        console.log('running...');
    });
```

* 启动静态资源服务
``` bash
    app.use('/www',express.static('public'));
```

* 使art-template模板引擎
``` bash
    const template = require('art-template');
    // 设置模板引擎
    app.set('view engine','art');
    // 使express兼容art-template模板引擎
    app.engine('art', require('express-art-template'));
```

* 处理post请求
``` bash
    const bodyParser = require('body-parser');
    // 处理请求参数
    // 挂载参数处理中间件（post）
    app.use(bodyParser.urlencoded({ extended: false }));
    // 处理json格式的参数
    app.use(bodyParser.json());
```

* 连接数据库
``` bash
    const mysql = require('mysql');
    // 创建数据库连接
    const connection = mysql.createConnection({
        host: 'localhost', // 数据库所在的服务器的域名或者IP地址
        user: 'root', // 登录数据库的账号
        password: '123456', // 登录数据库的密码
        database: 'letao' // 数据库名称
    });
    // 执行连接操作
    connection.connect();

    // 操作数据库(数据库操作也是异步的)
    connection.query(sql,data, function(error, results, fields) {
        if (error) throw error;
        callback(results);
    });
    // 关闭数据库
    connection.end();
```

* 数据接口输出
    ``` bash
    res.send,res.json,res.jsonp都可以进行数据输出
    这里采用res.render配合模板引擎进行数据渲染，如 res.render('index',{list : result});
    //第一个参数为路由地址，第二个参数为渲染的数据
```

项目链接  <https://github.com/CodeMonkeyLin/Node-->

