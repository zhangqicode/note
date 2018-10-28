>Fast, unopinionated, minimalist web framework for Node.js
    
Express 是一个轻量级的 node web server

[官方网站](http://expressjs.com/)

## 如何部署静态资源

具体可以看[文档](http://expressjs.com/en/starter/static-files.html)

公司最近有个业务要求部署一些 gitbook 资源到自己的服务器上，express 部署非常简单

```
app.use('/book/book1', express.static('book1'));
```

