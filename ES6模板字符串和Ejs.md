# ES6模板字符串和Ejs

@(ES6)


### EJS 四步曲
>1.在HTML节后中定义容器 例如：
```
<div id="box"></div>
```
>2.通过AJAX动态获取data数据
```
data=[{a:"a",b:"b",c:"c"},{a:"a",b:"b",c:"c"},{a:"a",b:"b",c:"c"}]
```
>3.造模板 搭建HTML结构导入数据
>给script标签加上type="text/template"表示的是HTML模板，加个id="mainTemplate"是为了方便第四部获取这个HTML模板用的。
>boxData：是你自己定义的数据的名字 它是模板数据 我们呢还需要把他跟AJAX获取出来的数据相关联
```
<script type="text/template" id="mainTemplate">
		<ul>
		<%$.each(boxData,function(index,item){%>
			//处理li
			<li>
			<span><%=item.a%></span>
			<span><%=item.b%></span>
			<span><%=item.c%></span>
			</li>
		<%})%>
		</ul>
	</script>
```
>4.通过ejs.render将HTML结构，模板数据，data数据渲染出来
>ejs.render（模板的HTML结构，{模板数据：真实数据(一般都是通过ajax获取出来的数据)）
  -    获取HTML模板
```
var boxHTML=$("#boxTemplate").html();
```
  -     ejs.render()
```
var result=ejs.render(boxHTML,{boxData:data})
```
>5.放在页面上
```
$("#box").html(result);
```
|
>EJS语法：
			1.<% JS代码%>
			2.<%=输出的内容%>：是在HTML上真实展示的东西，可以是变量