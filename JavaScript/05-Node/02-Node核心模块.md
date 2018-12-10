## 一 http模块
#### 1.1 简单的web程序性
```JavaScript
const http = require('http');
let server = http.createServer(function (req, res) {
    res.writeHead(200, {'Content-Type': 'text/plain;charset=UTF8'});
    res.end('hello world');
});
server.listen(8000);
```
http.createServer()方法返回的是http模块封装的一个基于事件的http服务器。
req，res分别是http.IncomingMessage和http.ServerResponse的实例。
http.Server的主要事件有：
- request：客户端发起请求时，被处罚，提供req，res参数
- connection：TCP建立连接时候处罚，提供一个scoket参数，是net.Socket的实例。
- close：服务器关闭时，触发。
http.createServer()方法其实就是添加了一个Reuqest事件监听，如下所示：
```JavaScript
const http = require('http');
let server = http.createServer();
server.on('error', function (err) {
    console.log(err);
});
server.on('request', function (req, res) {
    console.log('有用户请求了');
    console.log(req);
});
server.listen(8081, 'localhost');
```  
#### 1.2 Node没有web容器
在Java、php等语言中，还需要一个web容器来存放web资源（如Java的Tomcat，PHP的Apache），而Node没有这样的概念。
所以，Node很难提供一个静态文件服务，也就是说，node.js中，如果看见一个网址是：127.0.0.1:3000/fang，不一定有fang这个文件夹。
即：URL和真实物理文件，是没有关系的，URL是通过了Node的顶层路由设计，呈递某一个静态文件的。
#### 1.3 http模块常见api
http.IncomingMessage是http请求信息，提供了3个事件：
- data：当请求数据到来时触发；
- end：当请求体数据传输完毕时候触发；
- close：当用户请求结束时候触发。
http.IncomingMessage提供的属性有：
- method：请求方式
- headers：请求头
- url：请求路径
- httpVersion：http版本
http.ServerResponse是返回客户端的信息，主要方法有：
- res.writeHead(statusCode,[headers];	//向请求的客户端发送响应头
- res.write(data,[encoding]);	        //向请求发送内容
- res.end([data],[encoding);            //结束请求
#### 1.4 https
```JavaScript
const https = require('https');
const fs = require('fs');
let options = {key: fs.readFileSync('keys/agent2-key.pem'), cert: fs.readFileSync('keyas/agent2-key.pem')};
https.createServer(options, function (req, res) {
    res.writeHead(200);
    res.end('hi');
}).listen(80);
```
## 二 url模块
req.url属性，表示用户的请求URL地址。所有的路由设计，都是通过req.url来实现的。
```JavaScript
const url = require('url');
let urlObj = url.parse('http://www.baidu.com/a/index.html?name=2', true);
console.log('',urlObj); 
//打印结果如下：
Url {
  protocol: 'http:',
  slashes: true,
  auth: null,
  host: 'www',
  port: null,
  hostname: 'www',
  hash: null,
  search: '?name=2',
  query: 'name=2',
  pathname: '/baidu/com/a/index.html/',
  path: '/baidu/com/a/index.html/?name=2',
  href: 'http://www/baidu/com/a/index.html/?name=2' 
}

```
注意：上述如果没有参数true，那么直接会得到Url对形象的字符串。
url.formate(urlObj)：接收一个url对象（注意是对象），返回完整的url地址
url.resolve(from,to)：接收一个base url对象和一个href url对象，像浏览器那样解析，返回一个完整的地址。
```JavaScript
const url = require('url');
let urlObj = {
    'host': 'www.baidu.com',
    'port': 80,
    'protocol': 'https',
    'search': '?q=test',
    'query': '?q=test',
    'path': '/'
};
console.log(url.format(urlObj));                        //https://www.baidu.com?q=test
console.log(url.resolve('http://www.a.com','/image')); //http://www.a.com/image
```
## 三 querystring模块
该模块有2个主要方法：
querystring.parse();	    
将查询字符串反序列化为一个对象，类似JSON.parse()
querystring.stringify();	
将一个对象序列化为一个字符串对象，类似JSON.stringify()
```JavaScript
const querstring = require('querystring');
let str1 = 'username=lisi&password=123';
let obj1 = querstring.parse(str1);    //转换为了对象
let obj2 = {username: 'zs', password: '456'};
let str2 = querstring.stringify(obj2);  //重新转换为字符串
```
用户提交的网址一般包含一定的数据，比如 username=lisi 这样的参数，我们可以通过url.query获取到这些字符串数据，Node提供了querystring对象来对这个字符串数据进行实例化处理：
```JavaScript
var querystring = require(‘querystring’);
urlStr = url.parse(req.url);
console.log(querystring.parse(urlStr));
```
## 四 path模块
```JavaScript
const path = require('path');
let myurl = path.join(__dirname, 'username', '123');
console.log(myurl);     //输出类似这样的绝对路径 E:\ProjectWeb\Test\username\123
```

## 五 文件模块fs
fs模块即：文件模块，是Node的核心模块，提供了操作文件的一些API。
文件模块针对同一个业务提供了 异步、同步两种操作方式，比如读取文件：readFile()  readFileSync()。
#### 5.1 打开文件 open()
> fs.open(path,flags,[mode],callback);
> - path：要打开的文件的路径（注意相对路径要 ./开头，为了兼容Linux和Win）
> - flags：打开文件的方式  读/写
> - mode：设置文件的模式  读/写/执行 分别对应 4/2/2
> - callback：回调
>   - err：打开失败后保存的错误对象，如果成功，err为null
>   - fd：被打开文件的标识

案例：
```JavaScript
const fs = require('fs');
fs.open('./1.html', 'r', function (err, fd) {
    if (err) {
        console.log('err');
    } else {
        console.log('success');
        console.log(fd);    //输出 3 
    }
});
```
#### 5.2 读取文件 readFile
Node中读取文件一般使用fs.read()方法，该方法从一个特定的文件描述fd中读取数据。
> fs.read(fd,buffer,offset,length,position,callback);
> - fd：通过fs.open()方法返回的文件描述符
> - buffer：数据写入的缓冲区
> - offset：缓冲区写入的写入偏移量
> - length：要从文件中读取的字节数
> - position：文件读取的起始位置，如果为null，就会从当前文件指针的位置读取；
> - callback：有err，bytesRead，buffer三个参数，bytesRead表示读取的字节数，buffer为缓冲区对象。

案例：
```JavaScript
const fs = require('fs');
//可选参数-字符集：{'charset':'utf8'}
fs.readFile('./1.html', function (err, data) {
    if (err) {
            throw err;
        } 
    console.log(data.toString());    //data是个Buffer 
});
```
#### 5.3 写入文件 writeFile
异步的将数据写入一个文件，如果文件不存在则创建，如果文件存在，则替换。data参数可以是一个string，也可以是一个buffer。
> fs.writeFile(filename,data,[options],callback);
> fs.appendFile()  该方法也可以将字符串或者缓冲区内容写入文件，
#### 5.4 监听文件 watch
> fs.wathc(filename,[options],[listener]);
观察置顶路径的改变，filename可以是文件或者目录，返回的对象是：fs.FSWatcher。第二个参数为布尔值，默认为true，代表只要文件被监听，就继续执行。
```JavaScript
const fs = require('fs');
fs.watch('./1.html', function (ev, fn) {
    console.log(ev);
    if (fn) {
        console.log(fn + '发生了改变');
    } else {
        console.log('...');
    }
});
```
#### 6.5 文件元信息 stat
> fs.stat(path,[callback]);
```JavaScript
const fs = require('fs');
fs.stat('./1.html', function (err, data) {
    console.log(data);  //输出一系列文件本身信息
});
```
#### 5.6 其他常见API
> fs.appendFile(name,data,[options],callback);
将数据添加到文件末尾（文件不存在则创建）
> fs.unlink(path,callback);			删除一个文件
> fs.exists(path,callback);			判断文件/目录是否存在
> fs.rename(path1,path2,[callback]);重命名文件
> fs.chomd(path,mode,[callback]);	修改权限,如mode取值为：’777’
			获取文件元信息
> fs.mkdir([path,[mode],callback);	创建文件夹
> fs.readdir([path,callback);			读取文件夹
> fs.rmdir([path,callback);			删除文件夹

## 六 压缩模块 zlib
```JavaScript
const zlib = require('zlib');
const fs = require('fs');
let rs = fs.createReadStream('./1.jpg');
let ws = fs.createWriteStream('./2.gz');
let gz = zlib.createGzip();
rs.pipe(gz).pipe(ws);
ws.on('finish',()=>{
    console.log('完成');
});
```
使用gzip与stream优化服务端代码：极大减小响应文件代码。
```JavaScript
const http = require('http');
const zlib = require('zlib');
const fs = require('fs');
http.createServer((req,res)=>{
    let rs = fs.createReadStream(`文件地址`);
	//没有该句会变成下载
    res.setHeader('content-encoding','gzip');	
    let gz = zlib.createGzip();
    rs.pipe(gz).pipe(res);
    rs.on('error',err=>{
        res.writeHeader(404);
        res.write('Not found');
        res.end();
    });
}).listen(8000);

```








