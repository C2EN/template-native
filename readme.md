```angularjs
<!-- 定义模板 -->
<script type="text/template" id='template'>
<%for(var i=0;i<items.length;i++){%>
	<div class="item">
			<a href="#" class='cover'><img src="<%=items[i].path%>" alt=""></a>
			<div class="bottom">
				<a href="#"><%=items[i].name%></a>
			<div class='rightBox'>
				<span class='icon-heart'><%=items[i].star%></span>
				<span class='icon-comment'><%=items[i].message%></span>
			</div>
		</div>
	</div>
<%}%>
</script>

<!-- 自己的代码 -->
<script type="text/javascript">
	// 为按钮绑定点击事件
	document.querySelector(".getMore").onclick = function () {
		// 直接调用ajax
		/*
			url:请求的url
			data:发送的数据
			method:请求的方法
			success:请求成功以后 调用的函数
			datatype:json
		*/
		$.ajax({
			url:"02.getMore.php",
			data:undefined,
			method:"get",
			success:function(data){
				// console.log(data);

				// 转化为js对象
				var jsArr = JSON.parse(data);
				// console.log(jsArr);

				// 为了使用方便 将 数组 包装到一个对象中
				var obj = {
					items:jsArr
				};

				// 调用 模板引擎的 方法 填充数据
				// 参数1 id 参数2 对象
				var resultStr = template('template',obj);
				console.log(resultStr);

				// 放到界面上
				document.querySelector(".container").innerHTML = resultStr;
			}
		})
	}

```