---
layout: post
title:  "websocket学习nodejs版本"
date:   2017-04-29 15:00:11
categories: IT
author : huanghui
---

创建文件server.js,内容如下：
```javascript
var WebSocketServer = require('ws').Server,
wss = new WebSocketServer({ port: 8080 });
var hh = 1;
wss.on('connection', function (ws) {
    var sendStockUpdates = function (ws) {
        if (ws.readyState == 1) {
        	hh += 1;
            console.log("更新", JSON.stringify({"hh": hh}));
            ws.send(JSON.stringify({"hh": hh}));
        }
    }
    var clientStockUpdater = setInterval(function () {
        sendStockUpdates(ws);
    }, 1000);
    ws.on('message', function (message) {
        var stockRequest = JSON.parse(message);
        console.log("收到消息", stockRequest);
        sendStockUpdates(ws);
    });
    ws.on('close', function () {
        if (typeof clientStockUpdater !== 'undefined') {
            clearInterval(clientStockUpdater);
        }
    });
});
```
创建文件client.js,内容如下：
```javascript
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>WebSocket test</title>
    <script>
    var ws = new WebSocket("ws://localhost:8080");
    ws.onopen = function(e) {
        console.log('Connection to server opened');
        stock_request = { "stocks": ["huanghui"] };
        ws.send(JSON.stringify(stock_request));
    };

    // WebSocket message handler
    ws.onmessage = function (e) {
        console.log(e);
        var stocksData = JSON.parse(e.data);
        console.log(stocksData);
        
    };

    function sendMessage() {
        ws.send($('#message').val());
    };
    
    </script>
</head>
<body >
</body>
</html>
```
运行如下命令：
cnpm install ws --save-dev
node server.js