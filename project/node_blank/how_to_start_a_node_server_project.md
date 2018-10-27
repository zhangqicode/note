1.先在 github 上创建了一个项目，添加了 README、gitignore 文件、license

2.将项目 clone 到本地，在目录中执行 npm init

3.在根目录创建 index.js 入口文件，在 package.json 中的 scripts 中添加 start 为 node ./index.js  
这样我们就可以使用 npm start 命令启动项目，同理可以配置其它快捷命令，如 npm test 等

4.创建 server 目录，在其中的 index.js 文件中生成 ZZServer 对象并 export 出来，共根目录的入口文件调用  
server 目录下主要处理的工作是启动服务，配置路由，初始化数据库等

5.安装 express，一个轻量级的 web server  
在 server 目录下 index.js 文件中实例化一个 express 对象 app  
用 get 方法注册接受 get 请求的路径  
```
app.get('/', (req, res) => res.send('Hello World!'));  
```  
用 listen 方法监听端口，即相当于启动 server


