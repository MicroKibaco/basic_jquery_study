### 动画基础
#### 隐藏元素的hide方法
jQuery中隐藏元素的hide方法,当提供hide方法一个参数时，.hide()就会成为一个动画方法。.hide()方法将会匹配元素的宽度，高度，以及不透明度，同时进行动画操作
```javaScipt
		// 点击buttom2 执行动画隐藏

		$("button:last").click(function() {
			$("#a2").hide({
				              duration: 3000,
				              complete: function() {
					              alert('执行3000ms动画完毕')
				              }
			              })
		});
```

#### 显示元素show()方法
让元素从隐藏到显示
```javaSript
   $("button").click(function() {
        $("#a1").hide(3000).show(3000)
    });
```

#### 显示与隐藏切换toggle方法
这是最基本的操作，处理元素显示或者隐藏，因为不带参数，所以没有动画。通过改变CSS的display属性，匹配的元素将被立即显示或隐藏，没有动画。
```javaSricpt
    $("button:last").click(function() {
        $(".right").toggle(3000)
    });
```

### 上卷下拉效果
#### 下拉动画slideDown
```javaScript
<script type="text/javascript">
	//点击button
	//执行3秒隐藏
	//执行3秒显示
	$("button:first").click(function() {
		$("#a1").slideDown(3000)
	});
</script>
<div class="right">
	<h4>测试二</h4>
	<div id="a2">hide-show</div>
	<button>点击slideDown执行回调</button>
</div>
<script type="text/javascript">
	//点击button
	//执行3秒隐藏
	//执行3秒显示
	$("button:last").click(function() {
		$("#a2").slideDown(3000,function(){
			alert('动画执行结束')
		})
	});
</script>
```

#### 上卷动画slideUp
因为动画是异步的，所以要在动画之后执行某些操作就必须要写到回调函数里面
```javaScript
   $("button:last").click(function() {
            $("#a2").slideUp(3000,function(){
                alert('动画执行结束')
            })
        });
```

#### 下拉切换slideToggle
slideDown与slideUp是一对相反的方法。需要对元素进行上下拉卷效果的切换，jQuery提供了一个便捷方法slideToggle用滑动动画显示或隐藏一个匹配元素
基本的操作：slideToggle();

这是最基本的操作，获取元素的高度，使这个元素的高度发生改变，从而让元素里的内容往下或往上滑。

提供参数：.slideToggle( [duration ] ,[ complete ] )

同样的提供了时间、还有动画结束的回调。在参数对应的时间内，元素会完成动画，然后出发回调函数

同时也提供了时间的快速定义，字符串 'fast' 和 'slow' 分别代表200和600毫秒的延时

slideToggle("fast")
slideToggle("slow")
注意：

display属性值保存在jQuery的数据缓存中，所以display可以方便以后可以恢复到其初始值
当一个隐藏动画后，高度值达到0的时候，display 样式属性被设置为none，以确保该元素不再影响页面布局
```javaScript
	$("button").click(function() {
		$("#a1").slideToggle(3000)
	});
```

#### 淡入动画fadeIn
淡入的动画原理：操作元素的不透明度从0%逐渐增加到100%
如果元素本身是可见的，不对其作任何改变。如果元素是隐藏的，则使其可见
```javaScript
<script type="text/javascript">
	//【显示】按钮
	$("#btnFadeIn").click(function() {
		var v = $("#animation").val();
		if (v == "1") {
			$("p").fadeIn();
		} else if (v == "2") {
			$("p").fadeIn("slow");
		} else if (v == "3") {
			$("p").fadeIn(3000);
		} else if (v == "4") {
			$("p").fadeIn(2000, function() {
				alert("显示完毕!");
			});
		} else if (v == "5") {
			$("p").fadeIn(1000, "linear");
		} else if (v == "6") {
			$("p").fadeIn({
				              duration: 1000
			              });
		}
	});

	// 【隐藏】按钮
	$("#btnHide").click(function() {
		$("p").hide();
	});
</script>
```

#### 淡出动画fadeOut
```javaScript
	//【显示】按钮

	$("#btnShow").click(function() {
		$("p").show();
	});

	//【隐藏】按钮

	$("#btnFadeOut").click(function() {
		var v = $("#animation").val();
		if (v == "1") {
			$("p").fadeOut();
		} else if (v == "2") {
			$("p").fadeOut("slow");
		} else if (v == "3") {
			$("p").fadeOut(3000);
		} else if (v == "4") {
			$("p").fadeOut(2000, function() {
				alert("隐藏完毕!");
			});
		} else if (v == "5") {
			$("p").fadeOut(1000, "linear");
		} else if (v == "6") {
			$("p").fadeOut({
				               duration: 1000
			               });
		}
	});
```

#### 淡入效果fadeTo
调用fadeTo, 它会基于当前的opacity数值进一步进行渐变
(连续)点击多次 他会不停的出入(对于toggle来说, 若是有回调函数, 则回调函数会被多次执行, 如多次弹出弹窗)
```javaScript
	//【切换显示/隐藏】按钮
	$("#btnFadeSwitch").click(function() {
		var v = $("#animation").val();
		if (v == "1") {
			$("p").fadeTo("slow", 0.5);
		} else if (v == "2") {
			$("p").fadeTo(1000, 0.2);
		} else if (v == "3") {
			$("p").fadeTo(1000, 0.9, function() {
				alert('完成')
			});
		}
	});
```

#### toggle与slideToggle以及fadeToggle的比较

##### toggle、sildeToggle以及fadeToggle的区别：
toggle：切换显示与隐藏效果
sildeToggle：切换上下拉卷滚效果
fadeToggle：切换淡入淡出效果
当然细节上还是有更多的不同点:
##### toggle与slideToggle细节区别：
toggle：动态效果为从右至左。横向动作，toggle通过display来判断切换所有匹配元素的可见性
slideToggle：动态效果从下至上。竖向动作，slideToggle 通过高度变化来切换所有匹配元素的可见性

```javaScript
<script type="text/javascript">
	$("#exec").click(function() {
		var v = $("#animation").val();
		var $aaron = $("#aaron");
		if (v == "1") {
			// 数值的单位默认是px
			$aaron.animate({
				               width  :300,
				               height :300
			               });
		} else if (v == "2") {
			// 在现有高度的基础上增加100px
			$aaron.animate({
				               width  : "+=100px",
				               height : "+=100px"
			               });
		} else if (v == "3") {
			$aaron.animate({
				               fontSize: "5em"
			               }, 2000, function() {
				alert("动画 fontSize执行完毕!");
			});
		} else if (v == "4") {
			// 通过toggle参数切换高度
			$aaron.animate({
				               width: "toggle"
			               });
		}
	});
</script>
```

#### animate

1. 动画的完成和回调函数的执行是异步的, 如在跳出对话框后, 延时点击确认, 再返回页面, 动画已然完成; 若在progress的回调函数中先alert, 再console.log, 但在alert时停顿确认, 返回时, console只会执行一次, 而不是在每一步动画完成都调用, 因为在回调函数被alert阻塞时, 动画已经异步完成了~

2. progress有三个参数, 第一个参数好像是更具体的包含elem等属性的对象; 第二个是进度, 但是是从0~1, 需要取到小数点后面的值, 如arguments[1].toFixed(2); 第三个参数是duration值, 在progress过程中会逐渐变小到0, 类似于倒计时

3. step的回调函数中有两个参数, 第一个是需要完成动画效果的当前的css属性值, 第二个是一个包含elem等属性的更具体的对象

疑问: progress和step在应用时有啥区别? 个别参数不一样? step有now, progress没有吗(好像只能去elem里的style里去找?)?

```javaScript
	$("#exec").click(function() {
		var v = $("#animation").val();
		var $aaron = $("#aaron");
		if (v == "1") {
			// 数值的单位默认是px
			$aaron.animate({
				               width  :300,
				               height :300
			               });
		} else if (v == "2") {
			// 在现有高度的基础上增加100px
			$aaron.animate({
				               width  : "+=100px",
				               height : "+=100px"
			               });
		} else if (v == "3") {
			$aaron.animate({
				               fontSize: "5em"
			               }, 2000, function() {
				alert("动画 fontSize执行完毕!");
			});
		} else if (v == "4") {
			//通过toggle参数切换高度
			$aaron.animate({
				               width: "toggle"
			               });
		}
	});
```
#### 停止动画stop
1. stop(true, true) 第二个[jumpToEnd]参数, 是针对当前动画, 若设为true, 则跳到当前动画的最终效果, 而动画队列中的后续动画不再执行
2. stop() 停止当前执行的动画, 马上执行下一个动画
3. 个人理解: 由此可以看出动画本身的执行是一个异步过程, 先全部放入动画队列中,异步调用; 而单个元素动画的执行是同步的, 阻塞的?
```javaScript
$("#exec").click(function() {
		var v = $("#animation").val();
		var $aaron = $("#aaron");
		if (v == "1") {
			//观察每一次动画的改变
			$aaron.animate({
				               height: '50'
			               }, {
				               duration :2000,
				               //每一个动画都会调用
				               step: function(now, fx) {
					               $aaron.text('高度的改变值:'+now)
				               }
			               })
		} else if (v == "2") {
			//观察每一次进度的变化
			$aaron.animate({
				               height: '50'
			               }, {
				               duration :2000,
				               //每一步动画完成后调用的一个函数，
				               //无论动画属性有多少，每个动画元素都执行单独的函数
				               progress: function(now, fx) {
					               $aaron.text('进度:'+arguments[1])
					               // var data = fx.elem.id + ' ' + fx.prop + ': ' + now;
					               // alert(data)
				               }
			               })
		}
	});
```

### jQuery核心
#### each方法的应用
.each只是处理jQuery对象的方法，jQuery还提供了一个通用的jQuery.each方法，用来处理对象和数组的遍历
```javaScript
 $("#exec").click(function() {
        var v = $("#animation").val();
        var $aaron = $("#aaron");
        $aaron.empty();
        if (v == "1") {

            // 遍历数组元素
            $.each(['Aaron', '慕课网'], function(i, item) {
                $aaron.append("索引=" + i + "; 元素=" + item);
            });
        } else if (v == "2") {
            // 遍历对象属性
            $.each({
                name: "张三",
                age: 18
            }, function(property, value) {
                $aaron.append("属性名=" + property + "; 属性值=" + value);
            });
        }
    });
```

#### 查找数组中的索引 inArray
jQuery中查找数组中的索引inArray
在PHP有in_array()判断某个元素是否存在数组中，JavaScript却没有，但是jQuery封装了inArray()函数判断元素是否存在数组中。注意了：在ECMAScript5已经有数据的indexOf方法支持了，但是jQuery保持了版本向下兼容，所以封装了一个inArray方法
```javaScript

    $("#exec").click(function() {
        var v = $("#animation").val();
        var $aaron = $("#aaron");
           $aaron.empty();
        if (v == "1") {

            var index = $.inArray('Aaron',['test','Aaron', 'array','慕课网']);

            $aaron.text('Aaron的索引是: '+ index)

        } else if (v == "2") {

            //指定索引开始的位置
            var index = $.inArray('a',['a','b','c','d','a','c'],2);

            $aaron.text('a的索引是: '+ index)
        }
    });
```

#### 去空格神器trim方法
Query.trim()函数用于去除字符串两端的空白字符
这个函数很简单，没有多余的参数用法
```javaScript
  $("#exec1").click(function() {
        alert("值的长度：" + $("#results1").val().length)
    });

    $("#exec2").click(function() {
         alert("值的长度：" + $.trim($("#results2").val()).length)
    });
```

#### DOM元素的获取get方法
jQuery是一个合集对象，如果需要单独操作合集中的的某一个元素，可以通过.get()方法获取到
```javaScript
	$("#exec").click(function() {
		var v = $("#animation").val();
		var $aaron = $("#aaron a");

		//通过get找到第二个a元素，并修改蓝色字体
		if (v == "1") {
			$aaron.get(1).style.color = "blue"
		} else if (v == "2") {
			//通过get找到最后一个a元素，并修改字体颜色
			$aaron.get(-1).style.color = "#8A2BE2"
		}
	});
```

#### DOM元素的获取index方法
.index( selector 选择器例如“#test1”)
```javaScript
	$("#exec").click(function() {
		var v = $("#animation").val();

		var $span = $("span");
		$span.empty();

		if (v == "1") {
			//找到第一个li的同辈节点中的索引位置
			$span.text($("li").index())
		} else if (v == "2") {

			//通过传递dom查找
			$span.text($("li").index(document.getElementById("test5")))

		} else if (v == "3") {
			//通过传递jQuery对象查找
			$span.text($("li").index($("#test6")))

		}
	});
```


