#socketio/chat说明文档

================
说明 intro
================
This is a test project created by express4.x and the purpose is to test socket.io 1.3.3 API. 
这是一个用于socket.io 1.3.3 api 的测试
  ～架构用express4.x
  ～渲染模板用ejs,即直接用html
  ~在单位服务器上用的项目名为chat，在github上是socketio,在家是直接git clone https://github......
  ~在单位服务器为ubuntu12.x,在家是最新的14.x
  ~单位端口用3000，客户端用chrome(其实是360极速浏览器),在家因为在unbuntu下，只有firefox,所以只能用9000，点解？详见下面详细描述。所以在bin/www和views/index.html中经常会变化。

=========================
重要的体会和具体说明
=========================
1. 在firefox中要使用websocket，得在地址栏输入about:config，把websocket打开，否则就会报错：ws://.... 无法连接

2. 不同浏览器的报错方式不一样： 
	a. 如果express服务启动在x端口,比如8000，我发现在html页面中连接socket时，必须要加入端口号：“io("http://localhost:8000")”,不能这样写：“io("http://localhost")”,甚至随便写一个端口如io('http://localhost:3320'),这样就错了，必然报ERR_CONNECTION_REFUSED错误(chrome)，或者交叉同源报错(firefox)
	b. 在Firefox的console中报如下错误是正常的： 无法建立到 ws://localhost:9000/socket.io/?EIO=3&transport=websocket&sid=GRjJwdKhFRsZmZajAAAF 服务器的连接。 我估计情况是这样的：执行完之后释放
	   同样情况下如果用chrome就不报任何错误，事实上也的确无问题；

   总之，在chrome中调试看上去比较正常，firefox比较奇怪,建议用chrome
 

3. express和socket.io使用的是同一个端口

4. html中如下连接websocket的语句都是正确的：
	a. io.connect();
	b. io.connect('http://localhost:8000’) //端口号必须同express http sever端口号一样
	c. io('');
	d. io('http://localhost:8000')

5. html中以下连接语句是错误的：
	a. io.connect('http://localhost')  io('http://localhost')
	b. 或者给出错误的端口号
