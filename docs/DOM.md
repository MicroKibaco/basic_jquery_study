# DOM节点的创建
## DOM创建点及节点属性
### 创建流程
* 创建元素: document.createElement
* 设置属性: setAtrribute
* 添加文本: innerHTML
* 加入文档: appendChild

### 问题
- 每一个元素节点都必须单独创建
- 节点是属性需要单独设置,而且设置的接口不是统一
- 添加到指定的元素位置不灵活
- 浏览器的兼容问题处理

```javaScript
	var body = document.querySelector('body');
	document.addEventListener('click', function () {
		// 创建两个div元素
		var rightDiv = document.createElement('div');
		var rightaaron = document.createElement('div');

		// 给2个div设置不同的属性
		rightDiv.setAttribute('class', 'right');
		rightaaron.className = 'arron';
		rightaaron.innerHTML = '动态创建DIV元素节点';

		// 2个div合并成包含关系
		rightDiv.appendChild(rightaaron);

		// 绘制到页面的body
		body.appendChild(rightDiv);
	},false)
```

### jQuery节点创建与属性处理
- 创建元素节点: $("<div></div>")
- 创建文本节点: $("<div>我是文本节点</div>")
- 创建为属性节点: $("<div id='test' class='aaron'>我是文本节点</div>")/$("<div class='right'><div class='aaron'>动态创建DIV元素节点</div></div>")
```javaScript
	var $body = $('body');
	$body.on('click', function() {
		//通过jQuery生成div元素节点
		var div = $("<div class='right'><div class='aaron'>动态创建DIV元素节点</div></div>")
		$body.append(div)
	})
```

# DOM节点的插入
## DOM内部插入append()与appendTo()
￼
appned()和appendTo都能实现内容的添加,不过append内容在方法的前面.appendTo()方法在内容的前面
```javaScript
<script type="text/javascript">

	$("#bt2").on('click', function() {
		//.appendTo()刚好相反，内容在方法前面，
		//无论是一个选择器表达式 或创建作为标记上的标记
		//它都将被插入到目标容器的末尾。
		$('<div class="appendTo">通过appendTo方法添加的元素</div>').appendTo($(".content"))
	})

</script>
```

### DOM外部插入after()和before()

￼
1. before 与 after 都是相对选中元素外部增加元素节点,2个方法都可以直接或间接接收Html字符串,DOM元素,元素数组,或jQuery对象,用来插入到集合每个元素的前面或者后面
2. 两个方法都支持多参数的传递

注意点:
  1. after向元素的后边添加html代码,如果元素后面有元素了,那后面的元素向后移
 2. before向元素的前面添加html代码,如果元素前面有元素了,那前面的元素前移,然后将html代码插入

```javaScript
 $("#bt1").on('click', function() {
        //在匹配test1元素集合中的每个元素前面插入p元素
        $(".test1").before('<p style="color:red">before,在匹配元素之前增加</p>', '<p style="color:red">多参数</p>')
    })
    </script>
    <script type="text/javascript">
    $("#bt2").on('click', function() {
        //在匹配test1元素集合中的每个元素后面插入p元素
        $(".test2").after('<p style="color:blue">after,在匹配元素之后增加</p>', '<p style="color:blue">多参数</p>')

    })
```

### DOM内部插入prepend()与prependTo()
- append() 向每个匹配元素内部追加内容
- prenpend()向每个匹配元素内部前置内容
- appendTo() 把所有匹配的的元素追加到指定元素的集合中
- prependTo() 把所有匹配的元素前置到另一个元素集合中

￼
```javaScript
 $("#bt1").on('click', function() {
        //找到class="aaron1"的div节点
        //然后通过prepend在内部的首位置添加一个新的p节点
        $('.aaron1')
            .prepend('<p>prepend增加的p元素</p>')
    })
    $("#bt2").on('click', function() {
        // 找到class="aaron2"的div节点
        // 然后通过prependTo内部的首位置添加一个新的p节点
        $('<p>prependTo增加的p元素</p>')
            .prependTo($('.aaron2'))
    })
```
### DOM外部插入insertAfter()与insertBefore()

```javaScript
    $("#bt1").on('click', function() {
        //在test1元素前后插入集合中每个匹配的元素
        //不支持多参数
        $('<p style="color:red">测试insertBefore方法增加</p>', '<p style="color:red">多参数</p>').insertBefore($(".test1"))
    })
    $("#bt2").on('click', function() {
        //在test2元素前后插入集合中每个匹配的元素
        //不支持多参数
        $('<p style="color:red">测试insertAfter方法增加</p>', '<p style="color:red">多参数</p>').insertAfter($(".test2"))
    })

```

￼
### DOM节点删除之empty()的基本用法
如果我们通过empty方法移除里面div的所有元素，它只是清空内部的html代码，但是标记仍然留在DOM中
```javaScript
	$("button").on('click', function() {
		//通过empty移除了当前div元素下的所有p元素
		//但是本身id=test的div元素没有被删除
		$("#test").empty()
	})
```

### DOM节点删除之remove()的有参用法和无参用法
```javaScript
	$("button:first").on('click', function() {
		//删除整个 class=test1的div节点
		$(".test1").remove()
	})

	$("button:last").on('click', function() {
		//找到所有p元素中，包含了3的元素
		//这个也是一个过滤器的处理
		$("p").remove(":contains('3')")
	})
```
- remove比empty好用的地方就是可以传递一个选择器表达式用来过滤将被移除的匹配元素集合，可以选择性的删除指定的节点

- 我们可以通过$()选择一组相同的元素，然后通过remove（）传递筛选的规则，从而这样处理

### DOM节点删除之保留数据的删除操作detach()
detach方法是JQuery特有的，所以它只能处理通过JQuery的方法绑定的事件或者数据

```javaScript
$('p').click(function (e) {
	alert(e.target.innerHTML)

});

var p;
$("#bt1").click(function () {

	if (!$("p").length) return;// 去重
	p = $("p").detach()
});

$("#bt2").click(function () {
	// 把p元素在添加到页面中
	// 事件还是存在的
	$("body").append(p);
});
```

### DOM节点删除之detach()和remove()区别
```javaScript
	//给页面上2个p元素都绑定时间
	$('p').click(function(e) {
		alert(e.target.innerHTML)
	});

	$("button:first").click(function() {
		var p = $("p:first").remove();
		p.css('color','red').text('p1通过remove处理后,点击该元素,事件丢失');
		$("body").append(p);
	});

	$("button:last").click(function() {
		var p = $("p:first").detach();
		p.css('color','blue').text('p2通过detach处理后,点击该元素事件存在');
		$("body").append(p);
	});
```

### DOM拷贝clone()
```javaScript
    // 只克隆节点
	// 不克隆事件
	$('.aaron1').on('click',function () {
		$(".left").append( $(this).clone().css('color','red') )
	});
	// 克隆节点
	// 克隆事件
	$(".aaron2").on('click',function () {
		console.log(1);
		$(".left").append( $(this).clone(true).css('color','blue'))
	});
```
### DOM替换replaceWith()和replaceAll()
- replaceAll()和.replaceWith()功能类似，主要是目标和源的位置区别
- replaceWith()与.replaceAll() 方法会删除与节点相关联的所有数据和事件处理程序
- replaceWith()方法，和大部分其他jQuery方法一样，返回jQuery对象，所以可以和其他方法链接使用
- replaceWith()方法返回的jQuery对象引用的是替换前的节点，而不是通过replaceWith/replaceAll方法替换后的节点
```javaScript
    <script type="text/javascript">
    //只克隆节点
    //不克隆事件
    $(".bt1").on('click', function() {
        //找到内容为第二段的p元素
        //通过replaceWith删除并替换这个节点
        $(".right > div:first p:eq(1)").replaceWith('<a style="color:red">replaceWith替换第二段的内容</a>')
    })
    </script>
    <script type="text/javascript">
    //找到内容为第六段的p元素
    //通过replaceAll删除并替换这个节点
    $(".bt2").on('click', function() {
        $('<a style="color:red">replaceAll替换第六段的内容</a>').replaceAll('.right > div:last p:last');
    })
    </script>
```


### DOM包裹wrap()方法
简单的看一段代码：
<p>p元素</p>
给p元素增加一个div包裹
$('p').wrap('<div></div>')
最后的结构，p元素增加了一个父div的结构
<div>
    <p>p元素</p>
</div>

```javaScript
    $("#bt1").on('click', function() {
        //在test1元素前后插入集合中每个匹配的元素
        //不支持多参数
        $('<p style="color:red">测试insertBefore方法增加</p>', '<p style="color:red">多参数</p>').insertBefore($(".test1"))
    })
    $("#bt2").on('click', function() {
        //在test2元素前后插入集合中每个匹配的元素
        //不支持多参数
        $('<p style="color:red">测试insertAfter方法增加</p>', '<p style="color:red">多参数</p>').insertAfter($(".test2"))
    })
```

### DOM包裹unwrap()方法
- .remove()是自杀，.empty()是自宫， 而这个unwrap就是自脱衣

```javaScript
	$(".aaron1").on('click', function() {
		//找到所有p元素，删除父容器div
		$('p').unwrap('<div></div>')
	})
	$(".aaron2").on('click', function() {
		//找到所有p元素，删除父容器div
		$('a').unwrap(function() {
			return '<div></div>';
		})
	})
```

### DOM包裹wrapAll()方法
wrapAll是给集合中所有的元素都包上HTML结构
``` javaScript
    $(".aaron1").on('click', function() {
        //给所有p元素，增加父容器div
        $('p').wrapAll('<div></div>');
    })
    $(".aaron2").on('click', function() {
        //wrapAll接受一个回调函数
        //每一次遍历this都指向了合集中每一个a元素
        $('a').wrapAll(function() {
            return '<div></div>'
        })
    })
```

## jQuery遍历
### children()
.children() 找儿子
```javaScript
	$("#bt1").click(function() {
		$('.div').children().css('border', '3px solid red')

	})
$("#bt2").click(function() {
		//找到所有class=div的元素
		//找到其对应的子元素ul，然后筛选出最后一个，给边宽加上颜色
		$('.div').children(':last').css('border', '3px solid blue')
	})
```

### find()方法
find() 找后代
```javaScript
	$("button:first").click(function() {
		$('.left').find('li:last').css('border', '1px solid red')
	})
	$("button:last").click(function() {

		// 找到所有p元素，然后筛选出子元素是span标签的节点
		// 改变其字体颜色

		var $spans = $('span');
		$("p").find($spans).css('color', 'red');
	})
```

### parent()方法
- .parent() 找爸爸
- .detach() 隐身
- .remove 自杀
- .empty 身体被掏空
- .clone 复制 （true全复制 false 浅复制，无事件）
- .replaceWith 删除并替换节点（结合.replaceAll()来记）
- .wrap 每个人加个爸爸
- .unwrap 爸爸没了
- .wrapAll 所有人加个爸爸
- .wrapAll（function）每个人加个爸爸
- .wrapInner 加个儿子
- .children() 找儿子
- .find() 找后代
```javaScript
	$("button:first").click(function() {

		$('.level-3').parent().css('border', '1px solid red')

	})
$("button:last").click(function() {

		// 找到所有class=item-a的父元素
		// 然后给每个ul,然后筛选出最后一个，加上蓝色的边

		$('.item-a').parent(':last').css('border', '1px solid blue')
	})
```

### parents()方法
- .parents()找长辈
```javaScript
	$("button:first").click(function() {
		$('.item-b').parents().css('border', '2px solid red')
	})

	$("button:last").click(function() {
		//找到当前元素的所有祖辈元素,筛选出class="first-div"的元素
		//并且附上一个边
		$('.item-b').parents('.first-div').css('border', '2px solid blue')
	})
```

### closest()方法
closest    只要找到一个合适的就不继续找了。
```javascript
	$("button:first").click(function() {

		$('li.item-1').closest('.level-2').css('border', '1px solid red')

	})
	$("button:last").click(function() {

		var itemB = $('.item-b');
		$('li.item-1').closest(itemB).css('border', '1px solid blue');

	})
```
### next()方法
 next() 找我后面的兄弟

```javaScript

	$("button:first").click(function() {
		$('.item-1').next().css('border', '1px solid red')
	})

$("button:last").click(function() {
		//找到所有class=item-3的li
		//然后筛选出第一个li，加上蓝色的边
		$('.item-2').next(':first').css('border', '1px solid blue')})

```

### prev()方法
prev()我前面的兄弟
```javaScript
	$("button:first").click(function() {
		$('.item-2').prev().css('border', '1px solid red')
	})

	$("button:last").click(function() {

		// 找到所有class=item-2的li
		// 然后筛选出最后一个，加上蓝色的边
		$('.item-3').prev(':last').css('border', '1px solid blue')	})

```

### siblings()方法
siblings()找我所有的兄弟
```javaScript

    $("button:first").click(function() {
      $('.item-2').siblings().css('border', '2px solid red')
    })

    $("button:last").click(function() {
        //找到class=item-2的所有兄弟节点
        //然后筛选出最后一个，加上蓝色的边
       $('.item-2').siblings(':last').css('border', '2px solid blue')
    })

```

### each()方法
each是一个for循环的包装迭代器
```javaScript
	$("button:first").click(function() {
		//遍历所有的li
		//修改每个li内的字体颜色
		$("li").each(function(index, element) {
			$(this).css('color','red')
		})

	})
	$("button:last").click(function() {
		//遍历所有的li
		//修改偶数li内的字体颜色
		$("li").each(function(index, element) {
			if (index % 2) {
				$(this).css('color','blue')
			}
		})
	})
```


