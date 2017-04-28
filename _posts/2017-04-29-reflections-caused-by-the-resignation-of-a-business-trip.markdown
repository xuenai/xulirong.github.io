---
layout: post
title:  "XSS"
date:   2017-04-29 00:01:55
categories: IT
author : huanghui
---
express -e ./  安装express
npm start 启动项目
nodejs 设置不开启浏览器保护 ---->res.set('X-XSS-Protection', 0);
xss=<img src="null" onerror="alert(1)"/>
<p onclick="alert('点我')">点我</p>
xss=<iframe src="//baidu.com/t.html"></iframe>

存储型：存储型XSS和反射XSS的差别仅在于，提交的代码会存储在服务器端（数据库，内存，文件系统等），下次请求目标页面时不用再提交XSS代码

