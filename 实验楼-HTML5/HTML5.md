# HTML5

## 认识HTML5

### 1. 什么是HTML5
目前Firefox、Google Chrome、Opera、Safari（版本4以上）、Internet Explorer 9已支援HTML5技术。

### 2.HTML5新特性
#### 2.1 新增拥有具体含义的标签
HTML5新标准中直接添加了拥有具体含义的HTML标签比如：\<article\>、\<footer\>、\<header\>、\<nav\>、\<section\>

#### 2.2 新增更加智能的表单类型
在HTML5的标准中直接添加了智能表单，让这一切都变得那么的简单，比如 calendar、date、time、email、url、search

#### 2.3 让Web程序更加的独立，减少了对第三方插件的依赖。
在HTML5标准中原生的就支持音频、视频、画布等技术。让WEB程序更加独立，更好的适应多种形式的客户端。

#### 2.4 对本地离线存储的更好的支持
HTML5 提供了两种在客户端存储数据的新方法：  

• localStorage - 没有时间限制的数据存储  
• sessionStorage - 针对一个 session 的数据存储

#### 2.5 HTML5即时二维绘图 ,既画布的引入
HTML5 的canvas元素使用 JavaScript 在网页上绘制图像。并拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。

#### 2.6 JS支持多线程
在不影响UI update及浏览器与用户交互的情况下, 前端做大规模运算，只能通过 setTimeout 之类的去模拟多线程 。而新的标准中，JS新增的HTML5 Web Worker对象原生的就支持多线程。

#### 2.7 WebSockets让跨域请求、长连接、数据推送变得简单
WebSockets是在一个(TCP)接口进行双向通信的技术，PUSH技术类型。WebSocket是html5规范新引入的功能，用于解决浏览器与后台服务器双向通讯的问题，使用WebSocket技术，后台可以随时向前端推送消息，以保证前后台状态统一，在传统的无状态HTTP协议中，这是“无法做到”的。

#### 2.8 更好的异常处理
HTML5(text/html)浏览器将在错误语法的处理上更加灵活。HTML5在设计时保证旧的浏览器能够安全地忽略掉新的HTML5代码。与HTML4.01相比，HTML5给出了解析的完整规则，让不同的浏览器即使在发生语法错误时也能返回完全相同的结果。

#### 2.9 文件API让文件上传和操纵文件变得那么简单
由于项目中经常遇到用Web应用中控制操作本地文件，而之前都是使用一些富客户端技术比如flash，ActiveX，Silverlight等技术。在HTML5的新的提供的 HTML5 File API 让JS可以轻松上阵了。

## HTML5的新的结构元素介绍
### 一、HTML5与HTML4的区别

- 一、HTML5与HTML4的区别
	- 取消了一些过时的HTML4的标签
		- 其中包括纯粹显示效果的标记，如\<font\>和\<center\>，它们已经被 CSS完全取代.
		- 其他取消的属性:acronym, applet, basefont, big, center, dir, font, frame, frameset, isindex, noframes, strike,tt

	- 添加了一些新的元素
		- 更加智能的表单元素：date, email, url等; 更加合理的标签：\<section\>, \<video\>, \<progress\>, \<nav\>, \<meter\>, \<time\>, \<aside\>, \<canvas\>等
	- 文件类型声明
		- 仅有一种类型，\<!DOCTYPE html\>

- 二、HTML5的新结构标签

![][image-1]

- **\<section\>  **
	- 定义文档中的节。它用来表现普通的文档内容或应用区块，但section元素标签并非一个普通的容器元素，它表示一段专题性的内容，一般会带有标题。

	<section>
	    <h1>section是什么？</h1>
	    <h2>一个新章节</h2>
	    <article>
	        <h2>关于section</h2>
	        <p>section的介绍</p>
	        ...
	    </article>
	</section>

- ** \<article\>** 
	-  特殊的section标签，它比section具有更明确的语义，它代表一个独立的、完整的相关内容块。当我们描述一件具体的事物的时候，通常鼓励使用article来代替section。
	- article会有标题部分（通常包含在header内），也可以包含footer
	- article可以嵌套，内层的article对外层的article标签有隶属关系。

	<article>
	    <header>
	        <hgroup>
	            <h1>这是一篇介绍HTML 5结构标签的文章</h1>
	            <h2>HTML 5的革新</h2>
	        </hgroup>
	        <time datetime="2011-03-20">2011.03.20</time>
	    </header>
	    <p>文章内容详情</p>
	</article>

- **\<aside\>**
	- **aside标签用来装载非正文的内容，被视为页面里面一个单独的部分。**它包含的内容与页面的主要内容是分开的，可以被删除，而不会影响到网页的内容、章节或是页面所要传达的信息。**例如广告，成组的链接，侧边栏等等。**

	<aside>
	    <h1>作者简介</h1>
	    <p>厚德IT</p>
	</aside>

- **\<header\>**
	- header标签定义文档的页眉，通常是一些引导和导航信息。它不局限于写在网页头部，也可以写在网页内容里面。
	- 通常header标签至少包含一个标题标记（h1-h6），还可以包括hgroup标签，还可以包括表格内容、标识、搜索表单、nav导航等

- **\<footer\>**
	- footer标签定义section或document的页脚，包含了与页面、文章或是部分内容有关的信息，比如说文章的作者或者日期。 它和header标签使用基本一样，可以在一个页面中多次使用，如果在一个区段的后面加入footer，那么它就相当于该区段的页脚了

- **\<hgroup\>**
	- hgroup标签是对网页或区段section的标题元素（h1-h6）进行组合。例如，在一区段中你有连续的h系列的标签元素，则可以用hgroup将他们括起来

- **\<figure\>**
	- 用于对元素进行组合。多用于图片与图片描述组合。

	<figure>
	    <img src="img.gif" alt="figure标签"  title="figure标签" />
	    <figcaption>这儿是图片的描述信息</figcaption>
	</figure>

## 增强型表单标签

### 增型表单标签
HTML5中，新标准把文本框提示信息、表单校验、日期选择控件、颜色选择控件、范围控件、进度条、标签跨表单等功能直接加入新的表单标签中。 但在众多现代浏览器中，最新版本的Opera浏览器对新型表单的支持才最为完美。

#### Number类型input标签

	<input type="number" name="demoNumber" min="1" max="100" step="1"/>

name: 标识表单提交时的key值 min: 标识当前输入框输入的最小值 max: 标识当前输入框输入的最大值 step: 标识点击增大/减小的时候，增加/减小的步长

#### Email类型input标签

	<input type="email" name="email" placeholder="请输入注册邮箱"/>

当表单在提交前，此文本框会自动校验是否符合邮箱的正则表达式。

#### URL类型的input标签

	<input type="url" placeholder="请输入网址" name="url"/>

#### Tel类型的input标签

	<input type="tel" placeholder="输入电话" name="phone"/>

#### range类型的input标签

	<input type="range" min="0" max="50" step="5" name="rangedemo" value="0"/>

此类型标签的加入，输入范围内的数据变得非常简单容易，而且非常标准，用户输入可感知体验非常好。另外此标签可以跟表单新增加的output标签一块使用，达到一个联动的效果。

	<form oninput="output.value=parseInt(range.value)"/>
	    <input type="range" min="0" max="100" step="5" name="range" value="0"/>
	    <output name="output">0<output/>
	</form>

就是一个滚动条可以拉动

#### 新的日期、时间、月份、星期input标签
Web项目开发，一定会遇到相关的js日期控件，在HTML5中新加入的表单属性将会使Web开发变得更加简洁。

	<input type="date" name="datedemo"/>

相关的日期属性还包括：month、time、week、datetime-local、datetime

#### 颜色选择input标签

	<input type="color" name="colordemo"/>

#### input标签自动完成功能
有的项目会要求实现自动完成或者输入提示功能，在HTML5的支持下将变得简单。

	<input type="text" autocomplete="on" name="demoAutoComplete" list="autoNames" />
	<datalist id="autoNames">
	       <option  value="实验楼" ></option>
	       <option  value="HTML5" ></option>
	       <option  value="input标签" ></option>
	</datalist>


### HTML5表单新属性

- input表单新增加的特有属性
	- autofocus属性，demo:`<input type="text" autofocus="autofocus"/>`此属性可以设置当前页面中input标签加载完毕后获得焦点。
	- max、min、step：这些上面介绍过，都是跟数字相关。
	- placeholder：提示信息属性。
	- multiple：用于文件上传控件，设置此属性后，允许多个文件。
	- 校验属性：设置了required属性后预示着当前文本框在提交前必须有数据输入，而这一切都是由浏览器自动完成。还添加了pattern正则表达式校验

	<input type="text" autofocus="autofocus" required pattern="\d+"/>

- 另外一个较大的改进就是增加了form属性，也就是说，任何一个标签都可以指定它所属于一个表单，而不是必须在中进行包裹了。

	<input type="text" form="demoform" name="demo"/>

- form表单新增加的属性
	- novalidate属性规定在提交表单时不应该验证 form或input域

	<form action="" method="POST" novalidate="true"></form>

- autocomplete属性规定form或input域应该拥有自动完成功能

## HTML5文件操作API



[image-1]:	1.png