### JavaScript: (Ps:参考 W3school)

##### JS的组成:

ECMAScript : 核心部分 ,定义js的语法规范

DOM: document Object Model 文档对象模型 , 主要是用来管理页面的

BOM : Browser Object Model  浏览器对象模型, 前进,后退,页面刷新, 地址栏, 历史记录, 屏幕宽高



##### JS的语法:

变量弱类型: var i = true

区分大小写

语句结束之后的分号 ,可以有,也可以没有

写在script标签

##### JS的数据类型:

- 基本类型
  - string
  - number
  - boolean 
  - undefine
  - null
- 引用类型
  - 对象, 内置对象
- 类型转换
  - js内部自动转换 

##### JS的运算符和语句:

- 运算符和java 一样
  - "===" 全等号: 值和类型都必须相等
  - == 字符串匹配, 值相等就可以了
- 语句和java 一样

##### JS的输出

- alert()  直接弹框
- document.write()  向页面输出
- console.log() 向控制台输出
- innerHTML:  向页面输出



- 获取页面元素: document.getElementById("id的名称");

#### JS的开发步骤

```html
1. 确定事件
   1.DOMEvent, onclick,onload,onfocus,onblur,onunload等
2. 通常事件都会出发一个函数
3. 函数里面通常都会去操作页面元素,
做一些交互动作
    var a = document.getElementById("ID").value;
a.innerHTML= "<><>";
a.innerText="ohhh";

```



--- ---

 

###  DOM: 

######  什么是DOM:

         Document Object Model : 管理我们的文档   增删改查规则 

###### HTML中的DOM操作：

```html
一些常用的 HTML DOM 方法：
  getElementById(id) - 获取带有指定 id 的节点（元素） 
  appendChild(node) - 插入新的子节点（元素） 
  removeChild(node) - 删除子节点（元素） 

  一些常用的 HTML DOM 属性：
  innerHTML - 节点（元素）的文本值 
  parentNode - 节点（元素）的父节点 
  childNodes - 节点（元素）的子节点 
  attributes - 节点（元素）的属性节点 


查找节点：
getElementById() 返回带有指定 ID 的元素。 
getElementsByTagName() 返回包含带有指定标签名称的所有元素的节点列表（集合/节点数组）。 
getElementsByClassName() 返回包含带有指定类名的所有元素的节点列表。 

增加节点：
createAttribute() 创建属性节点。 
createElement() 创建元素节点。 
createTextNode() 创建文本节点。 
insertBefore() 在指定的子节点前面插入新的子节点。 
appendChild() 把新的子节点添加到指定节点。 

删除节点：
removeChild() 删除子节点。 
replaceChild() 替换子节点。 

修改节点：
setAttribute()  修改属性
setAttributeNode()  修改属性节点
```



--- ---

### JQuery：



#### JQuery的作用:

```
1. 写更少的代码,做更多的事情: write Less ,Do more
2. 将我们页面的JS代码和HTML页面代码进行分离
```

#### JQ中根据ID查找元素

```html
全都是根据选择器去找的
#ID{}
.类名{}
$("#ID的名称")
```

#### JQ和JS之间的转换

                     1. JQ对象,只能调用JQ的属性和方法
                      2.JS对象 只能调用JS的属性和方法

```javascript
function changeJS(){
				var div = document.getElementById("div1");
//				div.innerHTML = "JS成功修改了内容"
				//将JS对象转成JQ对象
				$(div).html("转成JQ对象来修改内容")
			}
			
			$(function(){
				//给按钮绑定事件
				$("#btn2").click(function(){
					//找到div1
//					$("#div1").html("JQ方式成功修改了内容");
					//将JQ对象转成JS对象来调用
					var $div = $("#div1");
//					var jsDiv = $div.get(0);
					var jsDiv = $div[0];
					jsDiv.innerHTML="jq转成JS对象成功";
				});
			});
```

#### JQ的开发步骤: 

(将我们页面的JS代码和HTML页面代码进行分离)

```JavaScript
//1. 导入JQ相关的文件
//2.  文档加载完成事件: $(function)  : 页面初始化的操作: 绑定事件, 启动页面定时器
//3. 确定相关操作的事件
//4. 事件触发函数
//5. 函数里面再去操作相关的元素


```

#### $ 的意義

- $就是jQuery的别称，而jQuery就是jQuery库提供的一个函数.

- - 这个函数的作用是根据 () 里的参数进行查找和选择html文档中的元素， 函数作用之一就是GetElementByID的代替，但()内不仅可以是ID，还可以是各类选择器

  - \$就是jquery对象，$()就是jQuery()，在里面可以传参数，作用就是获取元素



--- ----



### JQuery中的选择器

让我们能够更加精确找到我们要操作的元素	

##### 基本选择器

- ID选择器 :     #ID的名称
- 类选择器:     以 . 开头  .类名
- 元素选择器:    标签的名称
- 通配符选择器:   * 
- 选择器,选择器:  选择器1,选择器2



##### 层级选择器

- 子元素选择器:   选择器1 > 选择器2
- 后代选择器:  选择器1 儿孙
- 相邻兄弟选择器 :  选择器1 + 选择器2 : 找出紧挨着的一个弟弟
- 找出所有弟弟:  选择器1~ 选择器2   : 找出所有的弟弟

##### 属性选择器:

```
选择器[href]  : 单个属性
```

```html
选择器[href][title] : 多个属性
选择器[href][title='test'] : 多个属性,包含值
```

##### 表单选择器:

```html
:input   找出所有的输入项 : 不单单找出input  textarea select 

:text  找出type类型为 text

:password
```
##### 基本过滤器:

	选择器:first  : 找出的是第一个
	
	:last  
	
	:even   找出索引为偶数
	
	:odd    找出奇数索引
	
	:gt(index) :  大于索引
	
	:lt(index)   小于
	
	:eq(index)  等于



###### 表单对象属性:

```html
找出select中被选中的那一项:

option:selected
```

#### 表单校验:

- > trigger  :  触发事件,但是会执行类似浏览将光标移到输入框内的这种浏览器默认行为

- > triggerHandler : 仅仅只会触发事件所对应的函数

- > is()

  ```校验表单扩展:
  trigger  : 触发浏览器默认行为
  
  triggerHandler : 不会触发
  
  is : 判断
  
  find : 查找
  
  ```


#### 使用JQuery发送请求局部刷新页面

	数据交换格式:
	
		json
	
		xml


	

- 什么是JSON

  [JSON](http://baike.baidu.com/view/136475.htm)([JavaScript](http://baike.baidu.com/view/16168.htm) Object Notation) 是一种轻量级的数据交换格式。它基于[ECMAScript](http://baike.baidu.com/view/810176.htm)的一个子集。 JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习惯（包括[C](http://baike.baidu.com/subview/10075/6770152.htm)、C++、[C#](http://baike.baidu.com/view/6590.htm)、[Java](http://baike.baidu.com/subview/29/12654100.htm)、JavaScript、[Perl](http://baike.baidu.com/view/46614.htm)、[Python](http://baike.baidu.com/view/21087.htm)等）。这些特性使JSON成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成(一般用于提升网络传输速率)。

- JSON格式

  	JSON对象

  ```json
  { key1:value}   
  {"username":"zhangsan","password":"123"}
  ```

  	JSON数组

  ```json
  [{ key1:value},{ key1:value},{ key1:value}]
  ```

  $.get(url,function(data){}) 

--- ---

### JQuery 常用方法:  

```html
$(function)  : 文档加载完成的事件
css()  : 	修改css样式
prop() :    修改属性/ 获取属性 , true&& false 类型选择
attr() :    修改属性/ 获取属性  键值对处理, {"checked","false"}
html() :    修改innerHTML

append : 	给自己添加子节点 
appendTo :  将自己添加到别人家,给自己找一个爹
prepend :   在自己最前面添加子节点
after	:   在自己后面添加一个兄弟
empty	:   清空所有子节点

$(cities).each(function(i,n){
  	
})

$.each(arr,function(i,n){
  
});
```





--- ---



### Bootstrap:

#### BootStrap结构:

###### 全局CSS

- bootStrap中已经定义好了一套CSS的样式表

###### 组件

- BootStrap定义的一套按钮,导航条等组件

###### JS插件

- BootStrap定义了一套JS的插件,这些插件已经默认实现了很多种效果

#### 引入相关的头文件:

```html
<!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
	<link rel="stylesheet" href="../css/bootstrap.css" />
	
	<!--需要引入JQuery-->
	<script type="text/javascript" src="../js/jquery-1.11.0.js" ></script>
	
	<!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
	<script type="text/javascript" src="../js/bootstrap.js" ></script>
	
	<meta name="viewport" content="width=device-width, initial-scale=1">
```
#### Bootstrap 栅格系统的工作原理：

- “行（row）”必须包含在 `.container` （固定宽度）或 `.container-fluid` （100% 宽度）中，以便为其赋予合适的排列（aligment）和内补（padding）。
- 通过“行（row）”在水平方向创建一组“列（column）”。
- 你的内容应当放置于“列（column）”内，并且，只有“列（column）”可以作为行（row）”的直接子元素。
- 类似 `.row` 和 `.col-xs-4` 这种预定义的类，可以用来快速创建栅格布局。Bootstrap 源码中定义的 mixin 也可以用来创建语义化的布局。
- 通过为“列（column）”设置 `padding` 属性，从而创建列与列之间的间隔（gutter）。通过为 `.row` 元素设置负值 `margin` 从而抵消掉为 `.container` 元素设置的 `padding`，也就间接为“行（row）”所包含的“列（column）”抵消掉了`padding`

#### BootStrap的栅格系统

- 响应式设计: 这种设计依赖于CSS3中的媒体查询
- 栅格样式:
  - 设备分辨率大于1200 使用lg样式
  - 设备分辨率大于992 < 1200 使用md样式
  - 设备分辨率大于768 < 992  使用sm样式
  - 设备分辨率小于768使用xs样式

#### BootStrap 考虑以下几个问题:

> 1.导航栏的生成   组件 -> navbar 
>
> 2,轮播图,以及时间控制  JS-> carousel (旋转木马)
>
> ​	<div id="carousel-example-generic" class="carousel slide" data-ride="carousel" data-interval="1000">
>
>

--- ---



#### 注释:

 查找文档有限选择在线文档[w3school](https://www.w3cschool.cn/dict/),其次在选择离线文档.