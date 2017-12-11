# 漫谈jQuery(一) -- 样式篇

小酌抒情

前几天和朋友吃饭的时候，碰到了前女友。我们两个人互相看了一眼，擦肩而过，连个招呼都没有打。我忽然想起我们曾经一起吃饭，一起旅游，一起畅想未来。那个时候的我们，坚定地以为我们可以从校服走到婚纱。

可是，感情这东西真可悲啊。前一秒她还觉得你是生命中无比重要的存在，后一秒，你就变得可有可无。可我也觉得，幸好我们没有在彼此的青春中错过。虽然爱不在了，但那些有过的美好记忆，都还在。而我们，都会越来越好。


> JQuery的宗旨是——WRITE LESS,DO MORE，也就是“吃得少，干的多”。让我们广大的程序员能够写更少的代码，做更多的事情。


## 初识jQuery

### 1: 官网
  - 系列
** [进入官网获取最新版本](http://jquery.com/download/ ),jQuery有两个系列分别是1.x和2.x,主要是2.x不再兼容IE6,7,8浏览器,旨在兼容前端开发,由于减少一些代码,所以jQuery2比jQury1更小更轻量**

 - 版本
   1. **压缩版(compressed) :项目发布和上线的时候使用**
   2. **开发版(development):开发版本便于代码修改及调试**
### 2: Node
**[进入Node官网下载并安装NodeJS](https://nodejs.org/zh-cn/)**,配置node环境
在项目根目录执行如下命令
```linux
$ npm init
$ npm i jquery --save
```

JQuery是一个JavaScript脚本库,不需要特别的安装,只需要我们再header页面<head>标签里面,通过script标签引入即可

```html
<!DOCTYPE HTML>
<html>
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
	<script src="node_modules/jquery/dist/jquery.js"></script>
	<title>环境搭建</title>
</head>
<body>
<script type="text/javascript"> alert($) </script>
</body>
</html>
```
弹出如下信息,说明JQuery环境搭建成功
￼
### 3: HelloWord
当页面加载完毕,在页面居中位置显示:"您好！这是白杨的第一个jQuery小程序。"字样
```css
div{
  padding:8px 0;
  font-size:12px;
  text-align:center;
  border:1px solid #ff1113;
}
```
```HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>第一个简单的jQuery程序</title>
	<link rel="stylesheet" href="./../css/base.css">
	<script src="./../node_modules/jquery/dist/jquery.js"></script>
	<script type="text/javascript">
		$(document).ready(function() {
			$("div").html("您好！这是白杨的第一个jQuery小程序。");
		});
	</script>
</head>
<body>
<div></div>
</body>
</html>
```
￼
**代码分析:**
1: $("div").html() 是使用标签选择器获取div标签,对应javaScript 中所有的类选择器
- $("*") ——所有元素
- $("#lastname") ——id="lastname" 的元素
- $(".intro") ——所有 class="intro" 的元素
- $("p") ——所有 <p> 元素
- $(".intro.demo") ——所有 class="intro" 且 class="demo" 的元素
2: JQuery加载页面的三种方法
1.$(document).ready(function(){});
2.$(function(){});
3.jQuery(function($){});
**$(document).ready 的作用是等页面的文档(document)加载完毕后,再执行后续代码,因为我们执行代码的时候,可能会依赖页面的某个元素,我们要确保真正的被加载完后才能正确的使用.**
### 4: jQuery对象与DOM对象
对于才开始接触jQuery库的初学者来说,我们需要明确一点:
```
jQuery对象与DOM对象是不一样的
```
可能一时分不清什么是jquery对象,什么是DOM对象,以及两者的相互转换,通过一个简单的例子,简单区分jQuery对象和DOM对象

```javaScript
<p id="MicroKibaco"></p>
```
如果我们想获取页面上的id为MicroKibaco的元素p,然后给这段文字添加一段文字,"您好,我叫小木箱!是一名Android软件工程师",并且让文字变成红色.

- 普通处理,通过标准的javaScript处理

```javaScript
var p = document.getElementById('MicroKibaco');
p.innerHTML = '您好,我叫小木箱!是一名Android软件工程师';
p.style.color = 'red';
```
通过$("MicroKibaco")方法得到一个
$p的jQuery对象的信息,然后封装了很多的操作方法,调用自己的html和css,得到效果与标准的javaScript处理的结果是一样的.
```javaScript
var $p = $('#MicroKibaco');
$p.html('您好,我叫小木箱!是一名Android软件工程师').css('color','red');
```
那么javaScript操作DOM与JQuery操作DOM有什么区别呢,我们不难发现:

| 操作差异性     | DOM对象 | jQuery对象  |
| :------- | ----: | :---: |
| 包装对象获取 | getElementById('name')取得对象。|  $变量名称 =   $('name') ;|
| 修改     | 用innerHTML对内容修改     |  变量名.html('添加内容').css('属性','值')进行修改 |
| 简洁性    | 需要我们具体知道哪个DOM节点有哪些方法  |  更专注业务逻辑的开发  |
| 兼容性     | 需要关心不同浏览器的兼容性    | 代码也会更加精短 |

### 5: jQuery对象转化成DOM对象
jQuery本质上处理的还是JavaScript代码,它只是对javaScript进行了包装处理,为了是提供更好更方便快捷的DOM处理与开发中经常使用的功能,我们使用jQuery过程中,也能混合JavaScript原生代码一起使用,.在很多场景,他们都是可以操作的DOM对象,jQuery是类数组对象,DOM对象就是一个单独的DOM元素,因此,我们需要jQuery与DOM能够相互转换.
如何将jQuery对象转换成DOM对象?
- 利用数组下标方式读取到jQuery中的DOM对象
#### Html代码
```html
<div>元素一</div>
<div>元素二</div>
<div>元素三</div>
```
#### javaScript代码

```javaScript
var $div = $('div') // jQuery对象
var div = $div[0] // 转化成DOM对象
div.style.color = 'red' // 操作dom对象的属性
```

- 通过jQuery自带的get()方法
jQuery对象自身提供一个.get() 方法允许我们直接访问jQuery中相关的节点,get方法中提供一个元素的索引

```
var $div = $('div') //jQuery对象
var div = $div.get(0) //通过get方法，转化成DOM对象
div.style.color = 'red' //操作dom对象的属性
```
查看源码,看看就知道,get方法实际上是利用第一中方法处理的,只是包装一个get方法让开发者更加直接方便的调用

### 6: DOM对象转化成jQuery对象
相比较jQuery转换成DOM,开发中更多的是将DOM加工成jQuery对象.$(参数)是一个多功能方法,通过传递不同参数而产生不同的作用
```
如果传递给$(DOM)函数的参数是一个DOM对象,jQuery方法会把这个DOM对象给包装成一个新的jQuey对象
```
通过$(dom)方法将普通的dom 对象加工成jQuery 对象之后,我们就可以调用jQuey方法了

#### Html代码
```html
<div>元素一</div>
<div>元素二</div>
<div>元素三</div>
```
#### javaScript代码
```javaScript
var div = document.getElementsByTagName('div'); //dom对象
var $div = $(div); //jQuery对象
var $first = $div.first(); //找到第一个div元素
$first.css('color', 'red'); //给第一个元素设置颜色
```

通过getElementsByTagName获取相应的div节点元素,结果是一个dom合集对象,不过这个对象是一个数组集合(3个div元素)通过$(div)方法转化为jQuery对象中的first与css方法查找第一个元素并且改变其颜色

```html
<!DOCTYPE html>
<html>
<head>
	<meta http-equiv="Content-type" content="text/html; charset=utf-8" />
	<title></title>
	<script src="./../node_modules/jquery/dist/jquery.js"></script>
</head>
<body>
<div>元素一</div>
<div>元素二</div>
<div>元素三</div>
<script type="text/javascript">
var div = document.getElementsByTagName('div'); //dom对象
	//将dom节点div转化为$div的jquery对象
	var $div = $(div); //jQuery对象
	var $first = $div.first(); //找到第一个div元素
	$first.css('color', 'red'); //给第一个元素设置颜色
</script>
```
## jQuery选择器
> 页面的任何操作都需要节点的支撑，开发者如何快速高效的找到指定的节点也是前端开发中的一个重点。jQuery提供了一系列的选择器帮助开发者达到这一目的，让开发者可以更少的处理复杂选择过程与性能优化，更多专注业务逻辑的编写。

### 1: id选择器
一个用来查找的ID，即元素的id属性
```javaScript
$( "#id" )
```
**注意: **id是唯一的，每个id值在一个页面中只能使用一次。

### 2: 类选择器
> 类选择器,顾名思义,就是通过class样式类名来获取节点

**描述: **
```javaScript
$( ".class" )
```
类选择器效率相对低于id选择器,优势就是可以多选,jQuery相对于原生的javaScript相比
jQuery除了选择上的简单，而且没有再次使用循环处理 [Html代码](https://github.com/MicroKibaco/basic_jquery_study/tree/master/html/class-selector.html)


### 3: 全选择器
在css中,经常会在第一行代码中写下这样一行样式

```javaScript
* {padding: 0; margin: 0;}
```
通配符 * 意味着给所有的元素设置默认边距,jQuery我们也可以通过传递 * 选择器来选择选中文档中的元素

描述
```
$("*")
```
不难发现,如果想获取文档里面所有的元素,通过document.getElementByTagName()中传递 * 同样可以获取到,但这里我们需要考虑一个兼容性的问题,比如:
- getElementById的参数在IE8及较低的版本不区分大小写
- E会将注释节点实现为元素，所以在IE中调用getElementsByTagName里面会包含注释节点，这个通常是不应该的
- IE7及较低的版本中，表单元素中，如果表单A的name属性名用了另一个元素B的ID名并且A在B之前，那么getElementById会选中A
- IE8及较低的版本，浏览器不支持getElementsByClassName
幸好有了JQuery的出现,我们省下了很多功夫,不需要做那么多的兼容处理,可想而知,作为一名合格的前端工程师不是那么容易的
### 4: 层级选择器
文档之间总是有着这样或那样的关系,我们可以把节点用于传统家族来描述,文档树可以描述为一个家谱,那么节点与节点之间就存在父子,兄弟,祖孙关系呢
选择器中,层级选择器,就是处理
```
子元素 后代元素 兄弟元素 相邻元素
```
通过一表格对比与层级选择器的区别吧

￼

### 5:基本筛选选择器
筛选选择器用法与CSS中的伪元素类似,选择器用冒号':'开头,通过一个列表,看看基本选择器的描述:

￼
**注意事项: **
- :eq(), :lt(), :gt(), :even, :odd 用来筛选他们前面的匹配表达式的集合元素，根据之前匹配的元素在进一步筛选，注意jQuery合集都是从0开始索引
- gt是一个段落筛选，从指定索引的下一个开始，gt(1) 实际从2开始
### 6.内容筛选选择器

￼
**注意事项: **
- contains与:has都有查找的意思,但是contains查找包含查找文本的元素,has查找包含查找"指定元素"
- 如果contans匹配的文本包含元素的子元素中,同样认为是符合条件的
- parent与empty是相反的,两者所涉及的子元素,包括文本节点
### 7.可见性筛选选择器

￼

### 8.属性筛选选择器

￼

### 9.子元素筛选选择器

￼

### 10.表单元素选择器


￼


### 11.表单对象属性筛选选择器
￼
### 12.特殊选择器this
相信很多刚接触jQuery的人,很多会对$(this)和this的区别模糊不清,
this是javaScript的关键字,指的是上下文对象,简单的说就是方法/属性的所有者
下面一个例子中MicroKibaco就是一个对象,拥有name属性与getName方法,在getName中this指向了所属对象MicroKibaco

```
var MicroKibaco = {
    name:"杨正友",
    getName:function(){
        //this,就是MicroKibaco对象
        return this.name;
    }
}
MicroKibaco.getName(); //杨正友
```
当然在javaScript中this是动态的,也就是上下文对象都是可以被动态改变的(可以通过call,apply等方法)
同样在DOM中this就是指向这个html元素对象,因为this就是DOM元素的引用
假如给页面的一个p元素绑定一个事件
```javaScript
p.addEventListener('click',function(){
    //this === p
    //以下两者的修改都是等价的
    this.style.color = "red";
    p.style.color = "red";
},false);
```
通过addEventListener绑定事件的时间回调中,this指向的是当前dom对象,所以再次修改这样对象的样式,只需要通过this获取到引用即可
```
 this.style.color = "red"
```
有木有觉得这样的操作很不方便,如果通过jQuery处理就会简单多了

```javaScript
$('p').click(function(){
    //把p元素转化成jQuery的对象
    var $this= $(this)
    $this.css('color','red')
})
```
总体:
**
1.this,表示当前上下文对象是一个html对象,可以调用html对象所拥有的属性和方法
2.$(this),代表的上下文对象是一jquery的上下文对象,调用jQuery的属性和方法
**

## jQuery的属性与样式
###1. attr() 与 removevAttr()
#### attr()有四个表达式

1.attr(传入属性名):获取属性的值

2.attr(属性名,属性值):设置属性的值

3.attr(属性值,函数值):设置属性的函数值

4.attr(attributes):给指定元素设置多个属性值，即:{属性名一:"属性值一",
  属性值二:"属性值二",......}

### removevAttr()删除方法

.removeAttr(attriteName):为匹配的元素集合中的每一个元素中移除一个属性(attribute)


###2. .html()及.text()
读取 和 修改元素的html结构或者元素的文本内容是常见的DOM操作对象,jQuery针对这样的对象处理提供了两个便捷的方法 .html() 和 text()

### .html()
获取集合中的第一个匹配的html内容 或 设置每一个匹配元素的html内容
### text()
得到匹配元素集合中每个元素的文本内容结合,包括他们的后代,或设置匹配元素集合中每个元素文本的指定内容

差异:
**.html处理的是元素内容，.text处理的是文本内容**

### .val()
html(),.text()和.val()的差异总结：
1..html(),.text(),.val()三种方法都是用来读取选定元素的内容；只不过.html()是用来读取元素的html内容（包括html标签），.text()用来读取元素的纯文本内容，包括其后代元素，.val()是用来读取表单元素的"value"值。其中.html()和.text()方法不能使用在表单元素上,而.val()只能使用在表单元素上；另外.html()方法使用在多个元素上时，只读取第一个元素；.val()方法和.html()相同，如果其应用在多个元素上时，只能读取第一个表单元素的"value"值，但是.text()和他们不一样，如果.text()应用在多个元素上时，将会读取所有选中元素的文本内容。
2..html(htmlString),.text(textString)和.val(value)三种方法都是用来替换选中元素的内容，如果三个方法同时运用在多个元素上时，那么将会替换所有选中元素的内容。
3..html(),.text(),.val()都可以使用回调函数的返回值来动态的改变多个元素的内容。
### 增加样式.addClass()
1. .addClass(className):为每个匹配元素所要增加的一个或者多个样式

2. .assClass(function(index,currentClass)):这个函数返回一个或更多用
   空格隔开的要增加的样式。

注意事项: .addClass()方法不会增加一个样式类名。它只是简单的添加一个
          样式类名到元素上！
### 删除样式.removeClass()
.removeClass()方法

1. .removeClass([className]):每个匹配元素移除的一个或多个用空格隔开的样式名

2. .removeClass(function(index,class)):一个函数，返回一个或多个将要被移除的样式
   名

注意事项：如果一个样式类名作为一个参数，只有这样式类会被从匹配的元素集合中删
          除。如果没有样式名作为参数，那么所有的样式类将被移除
### 切换样式.toggleClass()
.toggleClass( )方法：在匹配的元素集合中的每个元素上添加或删除一个或多个样式类,取决于这个样式类是否存在或值切换属性。即：如果存在（不存在）就删除（添加）一个类
(1).toggleClass( className )：在匹配的元素集合中的每个元素上用来切换的一个或多个（用空格隔开）样式类名
(2).toggleClass( className, switch )：一个布尔值，用于判断样式是否应该被添加或移除
(3).toggleClass( [switch ] )：一个用来判断样式类添加还是移除的 布尔值
(4).toggleClass( function(index, class, switch) [, switch ] )：用来返回在匹配的元素集合中的每个元素上用来切换的样式类名的一个函数。接收元素的索引位置和元素旧的样式类作为参数
### 样式操作.css()
.css() 方法：获取元素样式属性的计算值或者设置元素的CSS属性
获取：
1.    .css( propertyName ) ：获取匹配元素集合中的第一个元素的样式属性的计算值
2.    .css( propertyNames )：传递一组数组，返回一个对象结果
设置：
1.  .css(propertyName, value )：设置CSS
2   .css( propertyName, function )：可以传入一个回调函数，返回取到对应的值进行处理
3   .css( properties )：可以传一个对象，同时设置多个样式
### .css()与.addClass()设置样式的区别
.css与.addClass 区别：

    .addClass()方法是通过增加class名的方式，那么这个样式是在外部文件或者内部样式中先定义好的，等到需要的时候在附加到元素上
    通过.css()方法处理的是内联样式，直接通过元素的style属性附加到元素上的
ps:通过.css方法设置的样式属性优先级要高于.addClass方法

总结：一般是静态的结构，都确定了布局的规则，可以用addClass的方法，增加统一的类规则
如果是动态的HTML结构，在不确定规则，或者经常变化的情况下，一般多考虑.css()方式
### 元素的数据存储

data这个方法可以静态用和动态用：

1静态：$.data(ele,key,value);里面三个参数分别代表要存储数据的节点、数据名称、数据内容；

2动态：ele.data(key,value)；表示某个节点存的数据名和数据内容。
其实不用管他什么静态动态的，会用就行了，这两个的区别就在节点ele那里，即例子的第一个参数ele那里。这个ele可以作为data方法的调用者（选择者） ，也可以作为 被选择者（被调用）。jquery方法的通用思想是：传入一个参数代表取值，传入两个参数代表设置这个节点的这个值。

附上本篇文章的github地址方便大家查阅:https://github.com/MicroKibaco/basic_jquery_study
------------------最后------------------
天赋，努力，思考和执行等等，总是需要的。与其纠结，不如迈步！一边走一边调整，我们会到达我们期待的远方。那时，你会笑着回忆你此刻的痛苦。




