# Node.js express 模板的使用（ejs + express )

关键词 ： ejs node express

---

 [TOC]
 
##下载安装
###1.安装express模块
```bash
 cd <项目文件夹路径>
 cnpm install express --save
```
</br>
</br>
###2.安装模板引擎
```bash
 cd <项目文件夹路径>
 cnpm install ejs  --save
```
##组织文件结构
整个项目文件夹的结构如下：
>####**views**
 ---home.html
 ---article.html
>####**app.js**
>####**package.json**
>####**README.md**
>####**.gitignore**

其中app.js是入口文件，views文件夹下面放置的是需要渲染的模板文件，package.json是整个项目的配置文件，.gitignore文件里面写明文件pull到github时不需要上传的文件或文件夹，如 `node_modules`文件夹


##编写app.js
```node
//加载express模块
const express = require('express');

//加载ejs模块
const ejs = require('ejs');

//加载path模块，path模块中包含许多处理文件路径的工具
const path = require('path');

//创建一个express实例
let app = express();

//注册模板文件的后缀名为html，默认为ejs
app.engine('html', ejs.__express);

//设置模板文件存放的目录，默认是与app.js同级下views文件夹
//path.join()用于路径拼接，可以根据当前的操作系统的类型正确选用文件路径拼接字符，linux是/,window是\
app.set('views', path.join(__dirname, '/views'));

//设置模板文件的后缀名为html，避免了res.render('home.html',...)的繁琐
app.set('view engine', 'html');


//路由挂载
app.get('/', function(req, res) {

	//render函数除了用数据渲染页面之外，还有sendFile('home.html')的作用。
	res.render('home', {
		title: 'home',
		content: 'This is home page.'
	});

});
app.get('/article', function(req, res) {

	res.render('article', {
		title: 'article',
		content: 'This is acticle page.'
	});

});

//使用8080端口
app.listen(8080);
console.log("The server is running on 8080");
```
##编写home.html和article.html
- home.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title><%=title%></title>
</head>
<body>
	<%=content%>
</body>
</html>
```

- article.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title><%=title%></title>
</head>
<body>
	<%=content%>
</body>
</html>
```

##运行程序

    node app.js
打开浏览器键入：localhost:8080 和 localhost:8080/article

![此处输入图片的描述][1]

##最后
本例子只是简单阐明node，express还有ejs之间的组织结构关系，更多的ejs语法可以参见 https://segmentfault.com/a/1190000004286562



参考资料：
【1】http://www.cnblogs.com/rubylouvre/p/3421805.html

【2】http://github.com/visionmedia/ejs

【3】https://segmentfault.com/a/1190000004286562


  [1]: http://www.kexinweb.com/images/node-blog/12.png
  [2]: http://www.kexinweb.com/images/node-blog/13.png
  
