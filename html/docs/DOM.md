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

### 
