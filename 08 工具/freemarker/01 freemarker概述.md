# Freemaker概述

FreeMarker 是一款 模板引擎： 即一种基于模板和要改变的数据， 并用来生成输出文本(HTML网页，电子邮件，配置文件，源代码等)的通用工具。 
它不是面向最终用户的，而是一个Java类库，是一款程序员可以嵌入他们所开发产品的组件。
模板编写为FreeMarker Template Language (FTL)。
它是简单的，专用的语言， 不是像PHP那样成熟的编程语言。 
那就意味着要准备数据在真实编程语言中来显示，比如数据库查询和业务运算， 之后模板显示已经准备好的数据。
在模板中，你可以专注于如何展现数据， 而在模板之外可以专注于要展示什么数据。

![Figure](D:\Notes\mds\javaweb-md\08 工具\freemarker\01 freemarker概述.assets\overview.png)

这种方式通常被称为 MVC (模型 视图 控制器) 模式，对于动态网页来说，是一种特别流行的模式。
它帮助从开发人员(Java 程序员)中分离出网页设计师(HTML设计师)。
设计师无需面对模板中的复杂逻辑， 在没有程序员来修改或重新编译代码时，也可以修改页面的样式。
而FreeMarker最初的设计，是被用来在MVC模式的Web开发框架中生成HTML页面的，它没有被绑定到 Servlet或HTML或任意Web相关的东西上。
它也可以用于非Web应用环境中。

# 模板 + 数据模型 = 输出

需要向用户展示一个HTML页面，类似：

```html
<html>
<head>
  <title>Welcome!</title>
</head>
<body>
  <h1>Welcome John Doe!</h1>
  <p>Our latest product:
  <a href="products/greenmouse.html">green mouse</a>!
</body>
</html>
```

这里的用户名(上面的"Welcome John Doe!")，应该是登录这个网页的访问者的名字。
并且最新产品的数据应该来自于数据库，这样它才能随时更新(green mouse)。
那么不能直接在HTML页面中输入它们， 不能将静态的HTML代码写死。
此时，我们认识下 **模板**。 
模板只是会包含一些 FreeMarker 将它们变成动态内容的指令，和静态HTML没有太大区别：

```html
<html>
<head>
  <title>Welcome!</title>
</head>
<body>
  <h1>Welcome ${user}!</h1>
  <p>Our latest product:
  <a href="${latestProduct.url}">${latestProduct.name}</a>!
</body>
</html>
```

这个模板文件应该被存放在Web服务器上，就像通常存放静态HTML页面那样。
当有人来访问这个页面， FreeMarker框架(技术)将会介入执行，然后动态转换模板。
过程就是用最新的数据内容替换模板中 `${*...*}` 的部分， 之后将结果发送到访问者的Web浏览器中。
访问者的Web浏览器就会接收到例如第一个HTML示例那样的内容 (也就是没有FreeMarker指令的HTML代码)，访问者也不会察觉到服务器端使用的FreeMarker。 (当然，存储在Web服务器端的模板文件是不会被修改的；替换也仅仅出现在Web服务器的响应中。)

请注意，模板并没有包含程序逻辑来查找当前的访问者是谁，或者去查询数据库获取最新的产品。 
显示的数据 是在 FreeMarker 之外准备的，通常是一些 "真正的" 编程语言(比如Java) 所编写的代码。
这里我们引出**数据模型**的概念。
为模板准备的数据整体被称作为 **数据模型**。 模板作者要关心的是，数据模型是树形结构(就像硬盘上的文件夹和文件)，在视觉效果上， 数据模型可以是：

```
(root)
  |
  +- user = "Big Joe"
  |
  +- latestProduct
      |
      +- url = "products/greenmouse.html"
      |
      +- name = "green mouse"
```

> 上面只是一个形象化显示；数据模型不是文本格式，它来自于Java对象。 
> 对于Java程序员来说，root就像一个有 `getUser()` 和 `getLatestProduct()` 方法的Java对象， 也可以有 `"user"` 和 `"latestProducts"` 键值的Java `Map`对象。相似地，`latestProduct` 就像是有 `getUrl()` 和 `getName()` 方法的Java对象。

总的来说，模板和数据模型是FreeMarker来生成输出(比如第一个展示的HTML)所必须的：模板 + 数据模型 = 输出