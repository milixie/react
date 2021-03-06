# React
React学习笔记

### 添加绑定事件

1.引入资源react.js 和 JSXTransformer.js

2.代码如下：

```

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>react</title>
		<script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.13.3/react.js"></script>
		<script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.13.3/JSXTransformer.js"></script>
	</head>
	<body>
		<div id="container"></div>

		<script type="text/jsx">
		var TestClickComponent = React.createClass({
			handleClick: function(event){

				var tipE = React.findDOMNode(this.refs.tip);

				//使用this.refs.tip去索引到组件，但不是真实的dom节点
				//使用React.findDOMNode()得到真实的节点

				if (tipE.style.display === "none") {
					tipE.style.display = 'inline';
				} else {
					tipE.style.display = 'none';
				}

				event.stopPropagation();
				event.preventDefault();

				//使用了原生的event去封装的，具有了原生的event的方法，要去阻止冒泡
			},

			render : function(){
				return (
					<div>
						<button onClick={this.handleClick}>show | hide </button>

						//使用驼峰式写法onClick，方法定义为：this.funName

						<span ref="tip">测试点击</span>  

						//使用ref给值组件起名字，并且使用this.refs.tip去拿到这个组件
					</div>
				);
			}

		});

		var TestInputComponent = React.createClass({

			//初始化state
			getInitialState: function(){
				return {
					inputContent: ""
				};
			},

			changeHandler: function(event){

				this.setState({
					inputContent: event.target.value
					//更新state，绑定到当前target的value
				});

				event.stopPropagation();
				event.preventDefault();
			},

			render: function(){
				return (
					<div>
						<input type="text" onChange={this.changeHandler}/>
						<span>{this.state.inputContent}</span>
					</div>
				);
			}
		});

		React.render(

			//这里必须要包含一个div

			<div>
				<TestClickComponent/>
				<TestInputComponent/>
			</div>

		, document.getElementById('container'));
		</script>
	</body>
</html>

```

3.代码中：

- 定义的标签类使用`var TestClickComponent = React.createClass({})`

- render结构使用`React.render(<div><TestClickComponent/></body>div>, document.getElementById('ddd'));`

- 注意：定义的时候使用到的标签必须外面要包一层`<div>`，render的时候也要包一层`<div>`
