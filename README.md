####AngularJS四大核心特性
- MVVM模式
- 模块化
- ng系列指令系统，指令间交互
- 数据单/双向绑定

####指令系统
- ```ng-app```定义了angular启动程序，页面加载完毕会自动初始化。
- ```ng-model```数据双向绑定指令，如果当前作用域没有找到指定的变量会声明。
- ```ng-cloak```解决代码闪烁问题，需要设置css样式 [ng-cloak] {display:none;}
- ```ng-bind && {{}}```数据单向绑定。
- ```ng-bind-html```单向绑定innerHTML片段。
- ```ng-bind-template```规定要使用模板替换的文本内容。
- ```ng-class```
	- 动态绑定一个或多个class类
	- 值为：数组 | 对象 | 字符串
	- 如果是多个字符串用空格分开
- ```ng-repeat```数据遍历指令，兼容重复数据 ：track by $id


####事件指令
- ```ng-click``` 点击事件
- ```ng-change```
	- input标签change事件
	- 需要搭配ng-model使用
	- 自测对file无效
	- 该事件不会覆盖原生事件，并且两者同时出发
- ```ng-blur```失去焦点事件
- ```ng-checked```规定元素是否被选中 true | flase
- ```ng-disabled```规定一个元素是否被禁用 true | flase


####自定义指令
- 指令类型

- 创建指令
```
app.directive('myDire',function () {
    return {
	    //指令类型
		restrict:"AECM",
		
		//更新DOM，
		link:function(scope,ele,attrs,m){
			//scope:在我们没有为scope指定属性的时候，它代表的就是父级controller的scope，默认会向上查找。
			//ele:是指令的jQlite(jQuery的子集)包装DOM元素，如果在引入angularjs之前之前引入了jQuery,那么这个元素就是jQuery。
			//attrs:包含了指令所在元素的属性集合对象。
			//m:访问被继承者指令。
		},
		
		//规定了指令被Angular编译和链接（link）后生成后的HTML标记
		template:"<div ng-... >hello word</div>"，
		
		//引入一个外部模板
		templateUrl:"URL",
		
		//规定生成的HTML标记是否替换当前指令的HTML元素
		replace:true | false，

		//指定scope作用域的范围
			`false`//默认值，共享父级作用域。
			`true`//继承父级作用域并创建指令自己的作用域。
			`{}`//创建指令独立的作用域，与父级毫无关系。
				//单向
				`@`//可以在以上独立作用域中使用父级作用域的scope
				//双向
				`=`//可以在以上独立作用域中使用父级作用域的scope，有一个地方需要注意：当前元素的属性名的值不用再加上{{}}这个表达式了，因为这里父scope传递的是一个真实的scope数据模型，而不是简单的字符串，所以这样我们就可以传递简单的字符串、数组、甚至复杂的对象给指令的scope。
				//调用父scope的方法
				`&`//注意一点：当前元素的属性不再加{{}}表达式，并且要用小括号调用。
					//传参方式：
						//实参：自定义指令内部`{p:"hello"}`
						//形参：外部模板
		 scope:(true|false)||({})，
		 
		//继承指定的指令，找不到向上找，找不到会报错。
		require:""，//?:兼容方式,不报错，^:向上查找
		
		//当指令与指令之间需要交互时用到
		controller:function($scope){
			$scope.num = 10;//不能被继承者调用
			this.name = "张三";//可以被继承者调用
		}，
		
    }
});
```
- 使用指令
	- ```<my-dire></my-dire>```元素指令
	- ```<div my-dire></div>```属性指令
	- ```<div class="my-dire"></div>```类名指令
	- ```<!-- directive:my-dire -->```注释指令 


####过滤器
> 语法：```{{value | filterName :条件1:条件2: .... }}``` 可以对一个对象添加多个过滤器

- ```{{100 | currency:"￥"}}```货币过滤器
- ```{{"abcd" | uppercase}}```格式化为大写
- ```{{"ABCD" | lowercase}}```格式化为小写
- ```ng-repeat = "item in Array | orderBy : key : true | flase``` 排列数组
- ```{{23423.42342 | number:2}}```小数点过滤器
- ```{{"1234567" | limitTo:4}}```限制位数


####路由


####服务
> angularjs中可以使用内建服务，还可以使用自己创建的服务。

- $location
	- ```$location.abcUrl```获取当前页面的url地址
	- ```$location.port```返回端口号
	- ```$location.host```返回域名
	- ```$location.portocol```返回http协议
	- ```...```
- $http
	- ```$http.get("url").then(function( res ){ var data = res.data })```  向服务器请求数据
- $timeout
	- ```$timeout(function(){ console.log("两秒后执行"); },2000)``` 定时器服务
- $interval
	- ```$interval(function(){ console.log("每两秒执行"); },2000)```定时器服务
- 创建自定义服务 
```
app.service("serviceName",function(){
	this.fn = function(x){
		console.log("自定义服务");
	}
});
```
- 使用自定义服务
```
app.controller("myCtrl",["serviceName",function(serviceName){
	serviceName.fn();
}])
```
- 过滤器中使用自定义服务 
```
app.filter('myFormat',['serviceName', function(serviceName) {
    return function(x) {
        return serviceName.fn(x);
    };
}]);
```