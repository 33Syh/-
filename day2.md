## 1.补充400和401、403状态码

**400: 客户端请求的语法错误，服务器无法理解**

​	产生原因：

​	前端提交数据的字段名称和字段类型与后台的实体没有保持一致

​	前端提交到后台的数据应该是json字符串类型，但是前端没有将对象JSON.stringify转化成字符串。

​	解决方法：

​	对照字段的名称，保持一致性

​	将obj对象通过JSON.stringify实现序列化	

**401: 请求要求用户的身份认证**

**403: 服务器理解请求客户端的请求，但是拒绝执行此请求**



## 2.几个很实用的BOM属性对象方法?

**个人理解**: 

BOM跟浏览器本身相关,  DOM是指的浏览器解析道的html,因为html是css和js的综合结果,所以DOM包含css和js, 这样就很好理解了.

出于个人理解所以有以下区分:

**BOM对象**: 

浏览器自动弹出的内容alert,confirm,prompt,浏览器的跳转location.href,history.back(),浏览器的屏幕大小screen.width,还有我不太不常用的获取浏览器信息navigator.appName(//获取浏览器的名字)等相关的,还有浏览器开关:window.open,window.close

其实不管是location还是screen、width、history等等都是window的子对象





## 3.WebSocket的实现和应用

#### websocket基础

初次接触 WebSocket 的人，都会问同样的问题：我们已经有了 HTTP 协议，为什么还需要另一个协议？它能带来什么好处？

答案很简单，因为 HTTP 协议有一个缺陷：通信只能由客户端发起。

举例来说，我们想了解今天的天气，只能是客户端向服务器发出请求，服务器返回查询结果。HTTP 协议做不到服务器主动向客户端推送信息。

这种单向请求的特点，注定了如果服务器有连续的状态变化，客户端要获知就非常麻烦。我们只能使用["轮询"](https://www.pubnub.com/blog/2014-12-01-http-long-polling/)：每隔一段时候，就发出一个询问，了解服务器有没有新的信息。最典型的场景就是聊天室。

轮询的效率低，非常浪费资源（因为必须不停连接，或者 HTTP 连接始终打开)

![image-20200730172701276](/Users/shanyinhuan/Library/Application Support/typora-user-images/image-20200730172701276.png)



其他特点包括：

（1）建立在 TCP 协议之上，服务器端的实现比较容易。

（2）与 HTTP 协议有着良好的兼容性。默认端口也是80和443，并且握手阶段采用 HTTP 协议，因此握手时不容易屏蔽，能通过各种 HTTP 代理服务器。

（3）数据格式比较轻量，性能开销小，通信高效。

（4）可以发送文本，也可以发送二进制数据。

（5）没有同源限制，客户端可以与任意服务器通信。

（6）协议标识符是`ws`（如果加密，则为`wss`），服务器网址就是 URL。

![image-20200730172853756](/Users/shanyinhuan/Library/Application Support/typora-user-images/image-20200730172853756.png)



明白了websocket的原理, 那么实现和应用也就很容易回答了, 

#### 实现:

Step 1 建立TCP连接（这一步是一切的基础，和HTTP一样）

Step 2 通过TCP连接，发送HTTP Get 请求，其中包含关键的Upgrade: websocket header。

Step 3 Server收到HTTP请求后，会把Step 1的TCP连接的用户层协议从HTTP转变为WebSocket。至此，HTTP部分就退出舞台了，WebSocket开始接管一切。

#### 应用

各种**实时**状态的更新, 比如 

社交聊天、弹幕、多玩家游戏、协同编辑、股票基金实时报价、体育实况更新、视频会议/聊天、基于位置的应用、在线教育、智能家居等需要高实时的场景