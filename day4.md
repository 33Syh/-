# day4

## 1. tcp三次握手

这个问题对于我来说感觉有点超纲, 但是经过问人和各种百度也尽量理解了

#### **1.先说网络架构:**

网络架构是进行通信连接的一种网络结构。

网络架构是为设计、构建和管理一个通信网络提供一个构架和技术基础的蓝图。网络构架定义了数据网络通信系统的每个方面，包括但不限于用户使用的接口类型、使用的网络协议和可能使用的网络布线的类型。

**网络架构典型的有一个分层结构**。分层是一种现代的网络设计原理，它将通信任务划分成很多更小的部分，每个部分完成一个特定的子任务和用小数量良好定义的方式与其它部分相结合。

#### **2.再说分层**:

网络分层就是将[网络节点](https://baike.baidu.com/item/网络节点/9338583)所要完成的数据的发送或转发、打包或拆包，控制信息的加载或拆出等工作，分别由不同的硬件和软件模块去完成。这样可以将往来通信和网络互连这一复杂的问题变得较为简单。

https://blog.csdn.net/qq_38560742/article/details/88398270



先附上几张聊天记录

![image-20200730163356449](/Users/shanyinhuan/Library/Application Support/typora-user-images/image-20200730163356449.png)

![image-20200730163416832](/Users/shanyinhuan/Library/Application Support/typora-user-images/image-20200730163416832.png)

![image-20200730163448124](/Users/shanyinhuan/Library/Application Support/typora-user-images/image-20200730163448124.png)

![image-20200730163535173](/Users/shanyinhuan/Library/Application Support/typora-user-images/image-20200730163535173.png)

![image-20200730163557298](/Users/shanyinhuan/Library/Application Support/typora-user-images/image-20200730163557298.png)

看完以后大概就差不多理解了, 这个tcp是干啥的,理解如下⬇️

![image-20200730164133019](/Users/shanyinhuan/Library/Application Support/typora-user-images/image-20200730164133019.png)

#### 3.科普完了, 下面开始说tcp三次握手问题

1⃣️ 客户端发SYN报文(TCP/IP建立连接时使用的握手信号)给服务端,服务端进入SYN_SEND状态(请求连接，当你要访问其它的计算机的服务时首先要发个[同步信号](https://baike.baidu.com/item/同步信号/8555402)给该端口,此时的状态叫SYN_SEND状态)

2⃣️客户端接收到SYN后, 回应一个SYN-ACK报文 , 服务端进入SYN_RECV状态([服务端](https://baike.baidu.com/item/服务端/6492316)被动打开后,接收到了客户端的SYN并且发送了ACK时的状态)

3⃣️客户端收到服务器端的SYN报文，回应一个ACK（ACK=y+1）报文，进入Established状态(含义TCP:连接成功，establish的过去式)

![image-20200730170213977](/Users/shanyinhuan/Library/Application Support/typora-user-images/image-20200730170213977.png)



## 2. 写一个方法去掉字符串中的空格

```
let str = '111111fsfs     ddf afdasdsa'
str = str.replace(/\s+/g, "");
str = str.replace(/ /g, "");
console.log('去除所有空格',str)

let str2 = "       222222R    unoob        ";
console.log('去除首尾空格',str2.trim());
```

```
/s 匹配所有空格
```

思路1:直接匹配替换

思路2:找到对应的位置index 然后截取,去掉



## 3.DOM中两个节点之间存在哪些关系?如何在节点之间移动?

**1.DOM中两个节点存在的关系无非3种：**
    1.1.包含与被包含,IE率先引入的contains()方法可检测，例 A.contains(B)，
          即检查节点B是否是节点A的子节点，返回布尔值，现大多数浏览器都支持；
        DOM level 3引入的compareDocumentPosition()，确定节点之间的关系，
          返回值为一个表示关系的位掩码（见图-1）的合(或者是按位或的值，并不知道具体实现)，
          通过按位与操作符“&”可确定关系。例:节点A(例：)在节点B(例：)前--位掩码为4，
          且节点A包含节点B--位掩码为16,则返回值为20，通过"!!(20&16)"这种方式即可返回一个布尔值，
          解析：“20&16”返回16证明节点A包含节点B（即：16），通过!!取得16的布尔值true。
    1.2父与子
        获取父节点：node.parentNode, node.parentElement,两者的区别在于后者只能获取元素，例如：图-2；
        获取子节点：childNodes(以NodeList对象存在的子节点集合),firstChild,lastChild
    1.3同辈（兄弟节点）
        nextSibling，previousSibling  

​    1.4Element Travel API给DOM添加的属性
​        childElementCount,firstElementChild,lastElementChild,nextElementSibling，
​        previousElementSibling  ,他们与之前的方法之间的区别是多了Element，保证只返回元素节点，而之前的方法普通的文本节点及注释节点也会返回,之前的方法在非IE浏览器中还会把元素间的空白符当文本节点返回。
​    1.5children属性（IE9以后）
​        与childNodes不同的地方在于：children只包含元素子节点(IE8及之前的版本可能会包含注释节点)。

**2.如何移动**

document.documentElement     返回文档的根节点<html> 
document.body     <body> 
document.activeElement 返回当前文档中被击活的标签节点(ie) 
event.fromElement        返回鼠标移出的源节点(ie) 
event.toElement       返回鼠标移入的源节点(ie) 
event.srcElement     返回激活事件的源节点(ie) 
event.target         返回激活事件的源节点(firefox) 
当前对象为node 
返回父节点：node.parentNode, node.parendElement, 
返回所有子节点：node.childNodes（包含文本节点及标签节点）,node.children 
返回第一个子节点：node.firstChild 
返回最后一个子节点： node.lastChild 
返回同属上一个子节点：node.nextSibling 