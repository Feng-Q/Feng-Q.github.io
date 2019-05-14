# Get和Post

## 最直接的区别

* Get一般向服务器请求数据，Post一般向服务器传送数据；
* Get请求的参数是放在URL里的，Post请求的参数是放在请求body里的；
* Get请求的URL传参有长度限制，而Post请求没有长度限制；
* Get传送数据量较小，不大于2KB。Post传送数据量较大，一般默认为不受限制，但理论上，IIS4中最大量为80KB，IIS5中为100KB；
* Get请求的参数只能是ASCII码，而Post请求传参没有这个限制；
* Get的安全性比Post低，但执行效率比Post高；
* GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留；

## 本质上的区别

**没有区别。**

Get和Post是HTTP协议中的两种发送请求的方法。

HTTP是基于TCP/IP的关于数据在万维网中如何通信的协议。

HTTP的底层是TCP/IP。所以GET和POST的底层也是TCP/IP，也就是说，GET/POST都是TCP链接。GET和POST能做的事情是一样的。你要给GET加上request body，给POST带上url参数，技术上是完全行的通的。

## 还有一个区别

GET产生一个TCP数据包；POST产生两个TCP数据包。

对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；

而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。

因为POST需要两步，时间上消耗的要多一点，看起来GET比POST更有效。因此Yahoo团队有推荐用GET替换POST来优化网站性能。但这是一个坑！跳入需谨慎。为什么？

1. GET与POST都有自己的语义，不能随便混用。

2. 据研究，在网络环境好的情况下，发一次包的时间和发两次包的时间差别基本可以无视。而在网络环境差的情况下，两次包的TCP在验证数据包完整性上，有非常大的优点。

3. 并不是所有浏览器都会在POST中发送两次包，Firefox就只发送一次。
