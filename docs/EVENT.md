## click与dbclick事件
- click 监听用户单击操作
- dbclick 监听用户双击操作

```javaScript
        //this指向button元素
         $("button:eq(0)").?(function() {
            alert(this)
        })

    <div class="test2">
        <p>$('button:first').click(function(e) {alert(this)})</p>
    </div>
    <button>指定触发事件</button>
        $('p').click(function(e) {
            alert(e.target.textContent)
        })
        //this指向button元素
        $("button:eq(1)").click(function() {
            $('p').click() //指定触发绑定的事件
        })
```

## mousedown与mouseup事件
如果用户在一个元素上按下鼠标按键，并且拖动鼠标离开这个元素，然后释放鼠标键，这仍然是算作mouseup事件

按下鼠标按键后，拖动离开这个元素。然后释放鼠标按键。mouseup回调没有执行, 事件没有被触发。
```javaScript
	//绑定一个mousemove事件
	//触发后修改内容
	$(".aaron1").mousemove(function(e) {
		$(this).find('p:last').html('移动的X位置：' + e.pageX)
	})

	//不同函数传递数据
	function data(e) {
		$(this).find('p:last').html('数据:' + e.data)
	}

	function a() {
		$(".right").mousemove(1111, data)
	}
	a();
```

## mouseover与mouseout事件

onmouseover()：鼠标指针移入事件；
onmouseout()：鼠标指针移出事件。

```javaScript
$('h2').mouseover(function(e) {
		alert('触发h2元素绑定的mouseover')
	});
	$("button:eq(0)").click(function(e) {
		$('h2').mouseover() //指定触发绑定的事件
	})

	var n = 0;
	//绑定一个mouseover事件
	$(".aaron1 p:first").mouseover(function(e) {
		$(".aaron1 a").html('进入元素内部,mouseover事件触发次数：' + (++n))
	})

	var n = 0;
	//不同函数传递数据
	function data(e) {
		$(".right a").html('mouseover事件触发次数：' + (++n) + '<br/> 传入数据为 ：'+ e.data)
	}

	function a() {
		$(".right p:first").mouseover('data = 慕课网', data)
	}
	a();

```


## focusin()事件

获取焦点后有一个默认的蓝色边框  去除 可以在css 中加入input:focus
```javaScript

	//input聚焦
	//给input元素增加一个边框
	$("input:first").focusin(function() {
		$(this).css('border','2px solid red')
	})

	//不同函数传递数据
	function fn(e) {
		$(this).val(e.data)
	}

	function a() {
		$("input:last").focusin('杨正友', fn)
	}
	a();
```

### focusout()事件
失去焦点时触发如input元素，用户在点击失去焦的时候，如果开发者需要捕获这个动作
```javaScript

	//input失去焦点
	//给input元素增加一个边框
	$("input:first").focusout(function() {
		$(this).css('border','2px solid red')
	})

	//不同函数传递数据
	function fn(e) {
		$(this).val(e.data)
	}

	function a() {
		$("input:last").focusout('yangzy', fn)
	}
	a();

```

## 表单事件
### blur与focus事件
focus与blur不支持冒泡
```javaScript
    $(".aaron").focus(function() {
        $(this).css('border', '2px solid red')
    })
    $(".aaron1").focusin(function() {
        $(this).find('input').val('冒泡捕获了focusin事件')
    })
    $(".aaron3").blur(function() {
        $(this).css('border', '2px solid red')
    })
    $(".aaron4").focusout(function() {
        $(this).find('input').val('冒泡捕获了focusout事件')
    })
```

### change事件

input和textarea变化后“失去焦点“才触发

```javaScript
	//监听input值的改变
	$('.target1').change(function(e) {
		$("#result").html(e.target.value)
	});

	//监听select：
	$(".target2").change(function(e) {
		$("#result").html(e.target.value)
	})

	//监听textarea：
	$(".target3").change(function(e) {
		$("#result").html(e.target.value)
	})
```

### select事件
当textarea或者文本类型的input元素的文本被选中时，会触发select绑定的事件
```javaScript

	//监听input元素中value的选中
	//触发元素的select事件
	$("input").select(function(e){
		alert(e.target.value)
	});
	$("#bt1").click(function(){
		$("input").select();
	});

	//监听textarea元素中value的选中
	$('textarea').select(function(e) {
		alert(e.target.value);
	});

```

### submit事件
1. 具体能触发submit事件的行为：

    <input type="submit">
    <input type="image">
    <button type="submit">
    当某些表单元素获取焦点时，敲击Enter（回车键）

2. form元素是有默认提交表单的行为，如果通过submit处理的话，需要禁止浏览器的这个默认行为
传统的方式是调用事件对象  e.preventDefault() 来处理， jQuery中可以直接在函数中最后结尾return false即可

## 键盘事件
### keydown()与keyup()事件
keydown是在键盘按下就会触发
keyup是在键盘松手就会触发
```javaScript
	//监听键盘按键
	//获取输入的值
	$('.target1').keydown(function(e) {
		$("em:first").text(e.target.value)
	});

	//监听键盘按键
	//获取输入的值
	$('.target2').keyup(function(e) {
		$("em:last").text(e.target.value)
	});
```

### keypress()事件

在输入中文之后再输入阿拉伯字母就能显示中文了

```javaScript
    //监听键盘按键
    //获取输入的值
    $('.target1').keypress(function(e) {
        $("em").text(e.target.value)
    });
```

## 事件绑定和解除
### on()的多事件绑定
on可多个事件绑定同一个函数
```javaScript
  // 多事件绑定一
	$("#test2").on('mousedown mouseup', function(e) {
		$(this).text('触发事件：' + e.type)
	})
	// 多事件绑定二
	$("#test3").on({
		               mousedown: function(e) {
			               $(this).text('触发事件：' + e.type)
		               },
		               mouseup: function(e) {
			               $(this).text('触发事件：' + e.type)
		               }
	               })
```

### on()高级用法
实际上是给祖先绑定一个事件。子元素通过冒泡将事传递到祖先元素，祖先元素再判断点击的是不是button，如果是，就执行相同的事件。因此，当有很多个相同的按钮需要绑定相同的事件时，可以用事件委托将事件委托给祖先节点，有祖先节点判断子节点是否执行某事件。如果不适用事假委托，那个每一个节点都需要绑定一个事件。
使用方法是：
祖先节点.on(“事件”,”子元素”,”绑定的函数”);
```javaScript
$('body').on('click', 'a', function(e) {
		alert(e.target.textContent)
	})
```

## 事件对象的作用
### jQuery事件对象的属性和方法
1. js中事件是会冒泡的，所以this是可以变化的，但event.target不会变化，它永远是直接接受事件的目标DOM元素；
2. this和event.target都是dom对象
如果要使用jquey中的方法可以将他们转换为jquery对象。比如this和$(this)的使用、event.target和$(event.target)的使用；

```javaScript
 //为 <span> 元素绑定 click 事件
    $("span").click(function() {
        $("#msg").html($("#msg").html() + "<p>内层span元素被单击</p>");
    });
    //为 Id 为 content 的 <div> 元素绑定 click 事件
    $("#content").click(function(event) {
        $("#msg").html($("#msg").html() + "<p>外层div元素被单击</p>");
        event.stopPropagation(); //阻止事件冒泡
    });
    //为 <body> 元素绑定 click 事件
    $("body").click(function() {
        $("#msg").html($("#msg").html() + "<p>body元素被单击</p>");
    });
```

## 自定义事件

trigger方法在绑定on事件元素之上进行。
```javaScript
	//点击更新次数
	$("button:first").click(function(event,bottonName) {
		bottonName = bottonName || 'first';
		update($("span:first"),$("span:last"),bottonName);
	});

	//通过自定义事件调用，更新次数
	$("button:last").click(function() {
		$("button:first").trigger('click','last');
	});

	function update(first,last,bottonName) {
		first.text(bottonName);
		var n = parseInt(last.text(), 10);
		last.text(n + 1);
	}
```
triggerHandler
triggerHandler与trigger的用法是一样的，重点看不同之处：
triggerHandler不会触发浏览器的默认行为
```javaScript

	//给input绑定一个聚焦事件
	$("input").on("focus",function(event,title) {
		$(this).val(title)
	});

	$("#accident").on("click",function() {
		alert("trigger触发的事件会在 DOM 树中向上冒泡");
	});
	//trigger触发focus
	$("button:first").click(function() {
		$("a").trigger("click");
		$("input").trigger("focus");
	});

	//triggerHandler触发focus
	$("button:last").click(function() {
		$("a").triggerHandler("click");
		$("input").triggerHandler("focus","没有触发默认聚焦事件");
	});
```


