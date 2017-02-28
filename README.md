####AngularJS四大核心特性
- MVVM模式
- 模块化
- ng系列指令系统
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
- 
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

####过滤器
> 语法：```{{value | filterName :条件1:条件2: .... }}``` 可以对一个对象添加多个过滤器

- ```{{100 | currency:"￥"}}```货币过滤器
- ```{{"abcd" | uppercase}}```格式化为大写
- ```{{"ABCD" | lowercase}}```格式化为小写
- ```ng-repeat = "item in Array | orderBy : key : true | flase``` 排列数组
- ```{{23423.42342 | number:2}}```小数点过滤器
- ```{{"1234567" | limitTo:4}}```限制位数


####路由