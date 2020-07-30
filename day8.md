## 1.HTML全局属性(global attribute)有哪些（包含H5）？

全局属性, 也就是一些html标签每个标签都能用的属性, (我看到这个问题后想到的是) title, style, id, class

查资料后发现有如下:

accesskey 规定激活元素的快捷键；
class 规定元素的一个或多个类名（引用样式表中的类）；
contenteditable 规定元素内容是否可编辑；
contextmenu 规定元素的上下文菜单。上下文菜单在用户点击元素时显示。
data-* 用于存储页面或应用程序的私有定制数据。
dir 规定元素中内容的文本方向。
draggable 规定元素是否可拖动。
dropzone 规定在拖动被拖动数据时是否进行复制、移动或链接。
hidden  样式上会导致元素不显示，但是不能用这个属性实现样式。
id 规定元素的唯一 id。
lang 规定元素内容的语言。
spellcheck 规定是否对元素进行拼写和语法检查。
style 规定元素的CSS行内元素。
tabindex 规定元素的tab键次序。
title 规定有关元素的额外信息。
translate 规定是否应该翻译元素内容。

## 2.在页面上隐藏元素的方法有哪些？

display:none;

visibility:hidden

opcity:0

z-index:-999

**transform: scale(0);  缩放到0**

**transform: rotateX(90deg)或者 transform: rotateY(90deg)   转到视觉平行看不到**

height:0,width:0; overflow:hidden;

## 3.去除字符串中最后一个指定的字符

题目: 'aaaabbbbccccaaaadd'去掉最后一个a

```
let str ='aaaabbbbccccaaaaDD'
//逻辑代码
console.log(str,'=》',str1)
```



- **思路1:将字符串反转, 找到后指定字符串的角标, 按照角标去掉, 再反转过来**

syh的答案:(**错误**) 

```
//再说一遍, 这是错的
let str1 ='aaaabbbbccccaaaaDD'
str1 = str1.reverse()
console.log( str1.indexOf('a'))
str1.substring(str1.indexOf('a'),1)
str1.reverse()
```

写到浏览器看了一下, 有问题,  我日, str没有reverse()方法, 只有arr有, 不管, 转成数组也要用这个方法

```javascript
let arr = str.split('')
let rearr = arr.reverse()
arr.splice(rearr.indexOf('a'),1)
str1 = arr.reverse().join('')
```



- **思路2: 字符串拼接的方法**

```javascript
let indexNum = str.lastIndexOf('a')
let str1 = str.substring(0,indexNum)+str.substring(indexNum+1,str.length)
```



- **思路3: 正则**

  关于查找替换, 都可以用正则

```javascript
 // 正则
let str1 = str.replace(/(.*?)a/,'$1');
console.log(str,'=》',str1)	
```

```html
知识点1
		*表示零次或多次
		.*在一起就表示任意字符出现零次或多次, 后面加上需要匹配的字符串
		
知识点2
		有?就是不开启贪婪模式, 没有?就是不开启贪婪模式
		
知识点3
		所谓贪婪模式, 举个例子 ⬇️
		a.*b，它将会匹配最长的以a开始，以b结束的字符串。开启贪婪模式如果用它来搜索aabab的话，它会匹配整个字符串aabab

本题目		
		str的replace这个方法本身的意思就是替换字符串中第一个符合条件的字符 
		不开启贪婪模式,就是按照正常的语法走,
		开启贪婪模式, 也就是一直往后走, 匹配最后一个
```

关于贪婪模式,详细介绍请见博客, https://blog.csdn.net/sinat_32336967/article/details/94761771

*(关于这个题目, 其实有很多方法, 但是总是离不开两个点, 各种方法找到对应角标, 各种方法进行替换或者删掉)*

**这道题复习到的, 关于字符串和数组的方法⬇️ 这几个比较常见 很常用, 必须记住**

```
数组转字符串 arr.join('')
字符串转数组 str.split('')
字符串没有反转方法 
数组反转方法 arr.reverse()
数组和字符串获取角标(第一个) arr.indexOf('a') str.indexOf('a')
数组和字符串获取角标(最后一个) arr.lastIndexOf('a') str.indexOf('a')
字符串截取 str.substring(start,end)
```

