# demo-actions
原生js模拟用户行为插件

## 演示地址
http://gongshunkai.github.io/demo/%E6%A8%A1%E6%8B%9F%E7%94%A8%E6%88%B7%E8%A1%8C%E4%B8%BA/demo.html

## 使用
1. Actions.tap 模拟tap
```javascript
var actions1 = Actions.tap('index-kw',{
	onError:function(msg){
		console.log(msg);
	},
	onReady:function(x,y){
		$('#test-block').show().css({'left':x,'top':y});
	},
	onFinish:function(x,y){
		$('#test-block').hide()
	}
});
```

2. Actions.input 模拟输入
```javascript
var actions2 = Actions.input('index-kw',{
	keywords:keywords,
	onError:function(msg){
		console.log(msg);
	},
	onReady:function(){
		
	},
	onChange:function(keyword){
		$('#index-kw')[0].value+=keyword;
	},
	onFinish:function(){
		
	}
});
```

3. Actions.scroll 模拟触摸滚动
```javascript
var actions3 = Actions.scroll({
	target:target,
	timer:timer || 10,
	step:step || 10,
	onError:function(msg){
		console.log(msg);
	},
	onReady:function(){
		
	},
	onBefore:function(x,y){
		$('#test-block').show();
	},
	onMoving:function(x,y){
		$('#test-block').css({'left':x,'top':y});
	},
	onAfter:function(x,y){
		$('#test-block').hide();
	},
	onChange:function(y){
		if(y == c_blocka_h){
			Actions.tap(c_blocka[0],{
				onError:function(msg){
					console.log(msg);
				},
				onReady:function(x,y){
					$('#test-block').show().css({'left':x,'top':y});
				},
				onFinish:function(x,y){
					$('#test-block').hide()
				}
			}).set();
		}else if(y == nextpage_h){
			Actions.tap(nextpage[0],{
				onError:function(msg){
					console.log(msg);
				},
				onReady:function(x,y){
					$('#test-block').show().css({'left':x,'top':y});
				},
				onFinish:function(x,y){
					$('#test-block').hide()
				}
			}).set();
		}else if(y == 10){
			alert(y)
		}
	},
	onFinish:function(){
		
	}
});
```

4. set方法返回promise对象以便异步统一管理，依次执行不同的行为
```javascript
var b = actions1.set();
b.then(function(data){
	return actions2.set();
})
.then(function(data){
	return actions3.set();
})
.then(function(data){
	return actions4.set();
})
.then(function(data){
	alert('模拟完毕');
});
```