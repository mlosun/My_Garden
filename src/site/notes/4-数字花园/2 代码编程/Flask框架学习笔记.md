---
{"dg-publish":true,"permalink":"/4-数字花园/2 代码编程/Flask框架学习笔记/","created":"2025-05-25","updated":"2025-05-26"}
---


> 学习课程：[学会使用Flask框架\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1Bm4y1K7NT/)

## 一、创建项目

### 项目目录结构

> 项目目录结构一般不需要更改，虽然可以通过配置去调整，但是会增加复杂度，不利于学习

- `app.py` 主文件，包含应用配置、路由定义、视图函数
- `templates/` 存放 HTML 模板的目录
- `static/` 存放静态资源的目录，如 css、js、img 等

### 创建 Flask 项目

```python
# app.py

from flask import Flask  # 导入flask库

app = Flask(__name__)  # 实例化 Flask 类

@app.route('/') # 定义路由的装饰器
def hello(): # 该路由的视图函数
	return 'hello world' # 最终返回到视图的内容

if __name__ == 'main':
	app.run()
```

### 运行 Flask 项目

```zsh
python app.py
```

## 二、请求参数

### GET 请求方式

```python
from flask import request

@app.route('/search', methods=['GET'])  # 默认支持 'GET' ，也可不显式指定 methods=['GET']
def search():
	query = requset.args.get('query') # 获取名为 ‘query’ 的参数值
	return f'搜索查询：{ query }'

# 当访问 http://127.0.0.1/search?query=张三 时
# 即可将 query=张三 通过GET方法传参
```

### POST 请求方式

```python
from flask import request

@app.route('/submit', methods=['POST']) # 默认不支持 'POST' ，需要显式指定 methods=['POST']
def submit():
	username = request.form.get('username') # 获取表单字段 'username' 的值
	password = request.form.get('password') # 获取表单字段 'password' 的值
	return f'用户名：{ username }，密码：{ password }'
```

## 三、页面模板

> flask 内置了 jinja2 模板引擎

### 模板表看

在 python 侧返回模板时附带参数，在 html 侧嵌入参数标签。

```python
# app.py

@app.route('/tmp')
def tmp():
	msg = 'hello world'
	return render_template('tmp.html', msg) # 返回 模板页面 和 模板参数
```

```html
<!-- templates/tmp.html-->

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>页面标题</title>
</head>
<body>
	<h1>{{ msg }}</h1> <!-- {{ msg }} 即为模板参数的调用标签-->
</body>
</html>
```

### 逻辑判断

```python
# app.py

@app.route('/tmp')
def tmp():
	num = 5
	return render_template('tmp.html', num)
```

```html
<!-- templates/tmp.html-->

{% if num > 5 %}
<p>当num大于5 时，显示这个文本</p>
{% elif num == 5 %}
<p>当num等于5 时，显示这个文本</p>
{% else %}
<p>当num不大于5也不等于5时，显示这个文本</p>
{% endif %}
```

### 循环处理

```python
# app.py

@app.route('/tmp')
def tmp():
	teams = [
		{'id':'1001', 'name':'唐三藏', 'gender':'男', 'age':45},
		{'id':'1002', 'name':'孙悟空', 'gender':'男', 'age':23},
		{'id':'1003', 'name':'猪悟能', 'gender':'男', 'age':22},
		{'id':'1004', 'name':'沙悟净', 'gender':'男', 'age':19},
	]
	return render_template('tmp.html', teams)
```

```html
<!-- templates/tmp.html-->

<table>
	<tr>
		<th></th>
		<th>编号</th>
		<th>姓名</th>
		<th>性别</th>
		<th>年龄</th>
	</tr>
	{% for team in teams %}
	<tr>
		<td>{{ loop.index }}</td> <!--loop.index 从1开始， loop.index0 从0开始-->
		<td>{{ team.id }}</td>
		<td>{{ team.name }}</td>
		<td>{{ team.gender }}</td>
		<td>{{ team.age }}</td>
	</tr>
	{% endfor %}
</table>
```

## 三、路由基础

flask 中使用 `@app.route` 设置请求和处理函数之间的映射

```python
@app.route('/')
def index():
	return 'hello world'
```

路由中可以使用变量来传递参数

```python
@app.route('/user/<username>')
def profile(username):
	return f'用户名：{username}'
```

路由中可以设置处理方法

```python
@app.route('/login', methods=['GET','POST'])
def login():
	if request.method == 'POST':
		# 处理登录表单提交
		return '登录中...'
	else:
		return '显示登录表单'
```

使用 redirect 可以跳转到另一个页面

```python
@app.route('/old')
def old_page():
	return redirect('/new')
```

设置错误信息展示

```python
@app.errorhandler(404)
def not_found_error(error):
	return '页面未找到', 404
```

## 四、使用蓝图

蓝图允许将应用分成多个模块，每个模块可以包含一组相关的路由和视图

### 创建蓝图

```python
# auth.py

from flask import Blueprint

auth_bp = Blueprint('auth', __name__)
```

### 设置路由和视图

```python
# auth.py

@auth_bp.route('/login')
def login():
	return '登录页'

@auth_bp.route('/register')
def register():
	return '注册页'
```

### 注册蓝图（绑定）

```python
# app.py

from flask import Flask
from auth import auth_bp # 从 auth 里导入 auth_bp 这个蓝图

app = Flask(__name__) # 实例化主应用

app.register_blueprint(auth_bp, url_prefix='/auth') # 将 auth_bp 这个蓝图，注册到主应用 app，并设定蓝图url前缀
```

最终：
- 访问 `/auth/login` 到登录页
- 访问 `/auth/register` 到注册页

## 五、开发方式对比

| FBV（以**函数**为基础开发）                               | CBV（以**类**为基础开发）                              |
| ----------------------------------------------- | --------------------------------------------- |
| 简单性：最简单的方法，每个视图函数都是一个独立的 Python 函数，处理特定的 URL 请求 | 结构化：可以更好地组织代码，特别适合于编写复杂的视图逻辑，将视图逻辑组织到不同的类方法中  |
| 直观：视图函数非常直观，每个函数代表一个特定的路由处理程序，易于理解              | 继承和重用：可以轻松的创建和继承类，以实现视图的重用和扩展，提高了代码的可维护性和可扩展性 |
| 自由度：使用函数方式来处理各种路由和请求，自由度很高，特别适合于编写简单的视图         | 复杂性：类方式方法可能更复杂一些，它涉及类和方法的概念，需要更多的学习和理解        |
| 易于测试：函数视图易于测试，因为他们是普通的 Python 函数，可以轻松的进行单元测试    | 灵活性：类方式开发允许你使用不同的方法处理同一个 URL 的不同 HTTP 请求      |

前述的笔记均为 FBV 开发方式，根据目前的技术水平，也不太会涉及到 CBV 的开发方式，故暂不对 CBV 相关内容进行整理。

## 六、Flask-SQLAlchemy 学习

[Flask 学习-12.Flask-SQLAlchemy 连接 mysql 数据库 - 上海-悠悠 - 博客园](https://www.cnblogs.com/yoyoketang/p/16615745.html)
[Flask 学习-13.Flask-SQLAlchemy 新建模型和字段 - 上海-悠悠 - 博客园](https://www.cnblogs.com/yoyoketang/p/16616702.html)
[Flask 学习-14.Flask-SQLAlchemy ORM操作数据库增删改查 - 上海-悠悠 - 博客园](https://www.cnblogs.com/yoyoketang/p/16617172.html)
[Flask 学习-77.Flask-SQLAlchemy 一对一关系增删改查 - 上海-悠悠 - 博客园](https://www.cnblogs.com/yoyoketang/p/16723108.html)
[Flask 学习-78.Flask-SQLAlchemy 一对多关系 - 上海-悠悠 - 博客园](https://www.cnblogs.com/yoyoketang/p/16729771.html)