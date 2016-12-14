# HTML & CSS : design and build websites
用于阅读查漏补缺

## HTML元素用来表示

1. 网页结构
2. 语义信息

### 语义化标记
使用这些标记的原因是为其他程序服务，像屏幕阅读器朗读时加重语气，或者搜索引擎突出引用。  

- \<strong\>\</strong\>
- \<em\>\</em\>
- \<blockquote\>\<blockquote\>  //浏览器会对其中间内容进行缩进
- \<q\>\</q\>//段落中较短的引用，但IE不支持，所以少用
- \<abbr\>\</abbr\> //使用缩写词，用标签的title属性显示显示完整形态。HTML4中专门的标签\<acronym\>,HTML5后只用\<abbr\>

	\<p\>\<abbr title="Professor"\>Prof\</abbr\> David is a nice guy.\</p\>

- \<cite\>\</cite\> //引用一部作品时（书籍、影视等）浏览器表示为斜体
- \<dfn\>\</dfn\>//新术语，给出定义的时候。浏览器表示为斜体，Safari和chrome不改变外观
- \<address\>\</address\>//页面设计者的信息，斜体
- \<ins\>\</ins\>//插入文本的内容，下划线
- \<del\>\</del\>//本文删除的文本，删除线
- \<s\>\</s\>//表示不准确或者不相关却不应该被删除的内容，从中贯穿的线

	<p>Laptop:</p>
	<p><s>Was $790</s></p>
	<p>Now $490 </p>

## 列表分为三种：

- 有序列表
- 无序列表
- 定义列表
	- 由\<dl\>\<dt\>\<dd\>组成，通常包含一系列术语及其定义
	- \<dt\>\<dd\>成对出现在\<dl\>内，有时可能一个dt有两个dd，或两个dt有一个dd


## 图像
### img元素中，alt属性
用于详细描述图片，因此可以用于屏幕阅读软件和搜索引擎‘

**align属性已经不再使用在HTML5中**

### 创建图像的三条规则

- 使用正确的格式保存图像
	- 网站主要使用jpeg,gif,png

- 以正确的大小保存图像
	- 图像的大小和宽度应该和网站上显示的一致

- 以像素来衡量图像

#### 使用正确的格式保存图像

- 当图片包含多种不同颜色时，JPEG文件
- 当图片包含少种颜色或者大面积同一颜色时，GIF或者PNG文件
- 照片最好保存为JPEG,单色的图片或者徽标保存为GIF

##### 矢量图像
不同于位图，与分辨率无关。  
优势在于可在不影响图像质量的前提下放大图像大小。  

	<s>可伸缩矢量图形（SVG）较新尚未普及</s>
	现在住主流浏览器都支持SVG了

#### 透明度
要创建一个局部透明的图片，涉及以下两种个格式： 

- 透明GIF: 如果图片的透明部分有直边，并且这部分是完全透明，可以选用GIF保存
- 如果图片的透明部分含斜边、圆形，或者透明部分是半透明，或者投影，保存为PNG

\_透明PNG格式不完全支持旧浏览器，例如IE6

### HTML5： 图形和图形说明
将图像和图像说明相关联
\<figure\>
	    <img />
	<br / >
	<figcaption>blablabla</figcation>
	</figure>

## Table表格
\<table\>  
\<tr\>  
\<td\>  
\<th\> 用法和\<td\>一样，作用是表示列或行的标题 ，可以使用scope特性来表示是行标题还是列标题  

	<th scope="row"></th>

浏览器通常用粗体表示\<th\>中的内容，且居中显示这些内容  

__即使一个单元格没有任何内容，仍需要使用\<td\>或者\<th\>来表示一个空单元格。__  
__\<th\>可以帮助那些使用屏幕阅读器的用户，提升搜索引擎为你页面编写索引能力__

### 跨列/跨行
如果表格中的某个单元格跨越多个列,我们可以在\<th\>或者\<td\>元素中使用**colspan**特性表明单元格所要跨越的列数。  
同理**rowspan**

	<td colspan="2">blabla</td>
### 长表格
三种元素区分表格第一行、主题内容、最后一行 

- \<thead\>
- \<tbody\>
- \<tfoot\>

这些元素会帮助使用屏幕阅读浏览器的人,并且可以按照不同表格中其余部分的方式来定义这些元素的样式

### 旧代码：逐渐淘汰不再使用
宽度与间隔：  

- width
- cellpadding
- cellspacing 

边框与背景: 

- border 
- bgcolor

## 表单
### \<form\> 元素
action特性：值为一个页面的URL，这个页面用来在用户提交表单时接收表单中的信息  
method特性分为两种： get/ post 

#### GET 特性：  

表单中的值被放在action的URL末尾，适用于以下情形：

- 短表单（如搜索框）
- 只是用Web服务器检索数据的情形（不发送那些要在数据库中添加或者删除的数据）

#### POST特性 ：
表单中的值被放在HTTP头信息中进行发送，适用以下情境：

- 允许用户上传文件
- 非常长
- 含敏感信息（包含密码等）
- 向数据库中添加或者删除信息

**如果没有method特性，默认使用GET**

### 单行输入框

	Username: 
	<input type="text" name="username" maxlength="30"/>

- size被淘汰，代表宽度
- name对表单控件进行标识，并和值一同传送到服务器
- maxlength输入字符的限制

### 密码框

	Password: 
	<input type = “password”" name="password" maxlength="30"/>

**尽管密码在屏幕上被隐藏，但并不代表密码控件中的数据将被安全发送到服务器，所以不要使用这种方式发送敏感数据例如信用卡号，应该设置SSL**

### 文本域（多行文本框）
cols和rows逐渐被淘汰

	<textarea name="comments">Enter your comments...</textarea>

### 单选按钮

	<input type="radio" name="gender" value="female" checked="checked"/> female
	<input type="radio" name="gender" value="male" /> male

- name特性：单选时name应该相同
- checked 
- value

### 复选框

	<input type="checkbox" name="service" value="rock" checked="checked"/ >rock
	<input type="checkbox" name="service" value="romance" / >romance
	<input type="checkbox" name="service" value="country" / >contry

- name特性：同一个问题回答name应该相同
- checked 
- value

### 下拉列表框

	<select name="bla">
	  <option value ="volvo" checked="checked">Volvo</option>
	  <option value ="saab">Saab</option>
	  <option value="opel">Opel</option>
	  <option value="audi">Audi</option>
	</select>

- name
- value
- checked

### 多选下拉列表框

	<select name="bla" multiple="multiple">
	  <option value ="volvo" checked="checked">Volvo</option>
	  <option value ="saab">Saab</option>
	  <option value="opel">Opel</option>
	  <option value="audi">Audi</option>
	</select>

- name
- value
- checked
- multiple

### 文件上传域

	<input type="file" name="pic"  />

**必须将form里的method特性改成POST**

### 提交按钮

	<input type="submit" value="Submit" />

- type
- name(optional)
- value(显示在按钮上的)

### 图像按钮
图像形式的提交按钮

	<input type="image" src="submit.gif" alt="Submit" />

### 隐藏字段

	<input type="hidden" name="country" value="Norway" />

但可以通过view resource看到

### 标签表单控件label

	<form>
	  <label for="male">Male</label>
	  <input type="radio" name="sex" id="male" />
	  <br />
	  <label for="female">Female</label>
	  <input type="radio" name="sex" id="female" />
	</form>

**注释："for" 属性可把 label 绑定到另外一个元素。请把 "for" 属性的值设置为相关元素的 id 属性的值。**

### 组合表单元素

	<form>
	  <fieldset>
	    <legend>health information</legend>
	    height: <input type="text" />
	    weight: <input type="text" />
	  </fieldset>
	</form>

fieldset 元素可将表单内的相关元素分组。  
\<fieldset\> 标签将表单内容的一部分打包，生成一组相关表单的字段。  
当一组表单元素放到 \<fieldset\> 标签内时，浏览器会以特殊方式来显示它们，它们可能有特殊的边界、3D 效果，或者甚至可创建一个子表单来处理这些元素。

- \<fieldset\> 标签没有必需的或唯一的属性。
- \<legend\> 标签为 fieldset 元素定义标题。

### HTML5表单验证

	<form action="demo_form.asp" method="get">
	  Name: <input type="text" name="usr_name" required="required" />
	  <input type="submit" />
	</form>

required 属性规定必需在提交之前填写输入字段。
如果使用该属性，则字段是必填（或必选）的。  
只有chrome和opera支持。

#### HTML5日期、邮件、URL控件

	Date: <input type="date" name="user_date" />

改成email/url即可

## iframe内敛框架
建立一个小窗口，显示另一个网页  
常见于载入google地图

- src
- width
- height
- scrolling(H5不再支持)
- frameborder(H5不再支持)
- seamless 不希望出现滚动条的地方

## \<meta /\>
\<meta\> 标签位于文档的头部，不包含任何内容。\<meta\> 标签的属性定义了与文档相关联的名称/值对。

### name属性 和 content属性 成对出现

name属性

- author
- description
- keywords
- generator
- revised
- robots(noindex:不许搜索引擎将此页面加入搜索结果，nofollow:收录此页面但不收录此页面的其他链接页面)

## http-equiv 属性 和 content属性 成对出现

- author
- expires
- pragma

## Flash
待补

## 行内(内联)元素(inline)和块级元素(block)的区别：

 - 行内元素与块级元素直观上的区别：
	- 行内元素会在一条直线上排列，都是同一行的，水平方向排列
	- 块级元素各占据一行，垂直方向排列。块级元素从新行开始结束接着一个断行。
- 块级元素可以包含行内元素和块级元素。行内元素不能包含块级元素。
- 行内元素与块级元素属性的不同，主要是盒模型属性上
	- 行内元素设置width无效，height无效(可以设置line-height)，margin上下无效，padding上下无效

详细阅读：
http://blog.csdn.net/chen\_zw/article/details/8713205
http://www.imooc.com/article/6753

行内块元素的兼容性使用？  
兼容性：display:inline-block;display:inline;zoom:1;  
http://www.jb51.net/css/418589.html

## 使用外部CSS
\<link\>

- href(CSS路径)
- type(页面所链接文档的类型) text/css
- rel(表明HTML页面和被连接文件的关系) stylesheet


内部CSS  
\<style\>尽量避免使用

## CSS选择器（最常用）

- 通用选择器 \*{}
- 类型选择器（元素选择器）a{}
- class选择器
- id选择器
- 子元素选择器 p\>a{}
- 后代选择器 p a{}
- 相邻兄弟选择器 h1 + p{} 位于h1元素后的第一个p元素，对其他p元素不起作用
- 普通兄弟选择器 p\~ul{} p之后所以的ul元素

## 颜色

- RGB值（每个0\~255）
- 十六进制编码
- 颜色名称
- HSL(CSS3引入)

### 对比度

- color和background-color对比度低时，难以阅读
- 较高时，容易阅读，但大量文字时，难以阅读
- 白色背景上深灰文本，或者黑色背景上灰白文本，增加可读性

### CSS3：opacity
0.0\~1.0  
rgba(0,0,0,0.5) 最后一位数是opacity  
以防浏览器不识别rgba，应该在之前加上rgb  


### CSS3：HSL
通过色调，饱和度，明度值确定颜色

色调：0-360  
饱和度：0%-100%（0%某种灰色） 
明度：0%黑色 100%白色  

HSLA（0，20%，100%，0.5） 最后一位opacity

## 文本
### 字体术语

- serif衬线字体（笔末额外的装饰）：适用于大量文字的阅读
	- Georgia
	- Times
	- Times New Roman
- sans-serif无衬线字体：设计更加简洁
	- Arial
	- Verdana
	- Helvetica
- monospace等款字体：显示代码
	- Courier
	- Courier New
- cursive草书字体：手写风格
	- Comic Sans MS
	- Monotype Corsiva
- fantasy虚幻字体：装饰字体，用于标题，不适合文章
	- Impact
	- Haettenschweiler

**浏览器至少支持每组字体中的一种，所以通常在偏爱的字体后面加上通用字体名**  

	如果想要衬线字体serif：
	font-family:Georgia,Times,serif;

### font-size

- px
- %(浏览器默认16px为100%)
- em(一个m的宽度)

所以后面两个，如果用户改变浏览器默认值，则会改变。px根据分辨率改变大小。

### font-weight:

- normal
- bold

### font-style

- normal 
- italic(斜体)
- oblique（倾斜）

### text-transform

- uppercase
- lowercase
- capitalize 每个单词都首字母大写

### text-decoration

- none(任何效果都删除)
- underline
- overline
- line-through
- blink(不可取annoying)

### line-height
行间距 就是一个字的最下边到下一排字的最上边的距离  

初始值最好设定为1.4em\~1.5em之间，这样用户调整自己的字体大小，也不会影响行间距，不要使用px

### letter-spacing/word-spacing

### text-align 对齐方式
控制文本的对齐方式

- left
- right
- center
- justify (文本两端对齐)

### vertical-align 垂直对齐
通常用于内联元素

### text-indent 文本缩进
将元素的首行文字进行缩进，通常用em或者px进行定义。可以使用负值，这样文字就推出了屏幕外。（针对看不见图片的人或者搜索引擎）

### CSS3 text-shadow
四个值:

- 阴影向左或向右的距离
- 向上或向下的距离
- 模糊度
- 阴影颜色

### overflow
盒子内容超过盒子本身如何显示：

- visible(默认状态)
- hidden (将溢出内容隐藏)
- scroll (被修剪，增加滚动条，查看其余内容)
- auto(如果被修剪，就已scroll状态出现)

### border-width

- border-top-width 等

### border-style

- solid
- dotted
- dash
- hidden/none

- border-top-style等

### border-color/border
border:1px solid black;

### 内容居中
内容在盒子上居中，将左右边距设为auto

### IE6盒子模型
盒子的padding和margin包含在他的宽度上  
解决方法：
提供DOCTYPE申明，使用HTML5,HTML4严格版

### 内联元素和块级元素的转换display

- inline
- block
- inline-block
	- 使块级元素像内联元素那样浮动
- none
	- 使用这个属性注意：不应该在内联盒子里创建块级元素

### visibility
允许隐藏盒子，但保留空间

- hidden
- visible

### CSS3边框图像

- URL
- 切割图片的位置
- 如何处理直边
	- stretch
	- repeat
	- round
	p.one {
		            -moz-border-image: url("images/dots.gif") 11 11 11 11 stretch;
		            -webkit-border-image: url("images/dots.gif") 11 11 11 11 stretch;
		            border-image: url("images/dots.gif") 11 11 11 11 stretch;}

### CSS3 box-shadow

	p.one { 
	                -moz-box-shadow: -5px -5px #777777; 
	                -webkit-box-shadow: -5px -5px #777777; 
	                box-shadow: -5px -5px #777777;}

语法
box-shadow: h-shadow v-shadow blur spread color inset;
注释：box-shadow 向框添加一个或多个阴影。该属性是由逗号分隔的阴影列表，每个阴影由 2-4 个长度值、可选的颜色值以及可选的 inset 关键词来规定。省略长度的值是 0。

- h-shadow必需。水平阴影的位置。允许负值。
- v-shadow必需。垂直阴影的位置。允许负值。
- blur可选。模糊距离。
- spread可选。阴影的尺寸。
- color可选。阴影的颜色。请参阅 CSS 颜色值。
- inset可选。将外部阴影 (outset) 改为内部阴影。

### border-radius

- border-top-left-radius:2em;
- border-top-right-radius:2em;
- border-bottom-right-radius:2em;
- border-bottom-left-radius:2em;

## 列表、表单和表格
### list-style-type
控制你项目符号的样式或形状  
常用于ul、ol、li元素  

无序列表:  

- none
- disc•
- circle○
- square■

有序列表：

- decimal 1 2 3
- decimal-leading-zero 01 02 03
- lower-alpha a b c
- upper-alpha A B C
- low-roman ⅰ ⅱ ⅲ
- upper-roman Ⅰ Ⅱ Ⅲ Ⅳ

### list-style-image
可用于ul、li  

	ul
	  {
	  list-style-image:url("/i/arrow.gif");
	  list-style-type:square;
	  }

### list-style-position
表明标记显示的位置

- outside (未使用该属性时的默认状态)
- inside （在文本块内部，文本块会被缩进）

### list-style
允许按任意顺序表示标记的type, image, position

	ul{
	list-style: inside circle;
	}

### 表格：
empty-cells 是否显示空单元格的边框

- show
- hide

border-spacing:控制单元格之间的空隙  

border-collapse: 为单元格增加边框，单元格相邻的地方，边框是外边框的两倍，为了避免这种情况，使用border-collapse  

- collapse:相邻边框合并为一个边框(border-spacing被忽略)
- separate （border-spacing生效）

## 布局
### 控制元素的位置

- 普通流
- 绝对定位
- 相对定位

### position:static
### position:relative
以其在普通流的位置作为起点。
用top/bottom/left/right指定移动

### position:absolute
脱离普通流，不再影响页面其他的位置 

### positon:fixed
固定定位  相对浏览器窗口定位，当窗口滚动时，这类元素的位置保持不变。

### z-index

### float
使用float属性，将文档流的元素在它的父元素里向左或者向右排列，父元素的其他内容会在它的周围浮动  
  
同时需要设置width值，否则显示效果会不一致  

### 用float并排元素
用float将所有盒子左移进行排列。
![][image-1]

段落In 1985… 因为在第三段的下面有足够空间展开，但因为第二段阻挡了左移，所以呈现这样的效果，我们应该用清除浮动

### 清除浮动 clear
clear用于一个盒子的左侧或者右侧不允许浮动。  
元素盒子的边不能和前面的浮动元素相邻

- left
- right
- both
- none

**自己理解：float影响其他元素，但是clear仅仅影响本身，即float让父元素的其他元素环绕自己，但如果其他元素使用clear，就不收影响了，去下一行了。**

### 浮动元素的父元素问题
若一个父元素内只有浮动元素，这个盒子的大小无法自适应撑开。  
两种方法解决：

- 在浮动元素的后面在一个元素，clear:both
- 父元素增加一个属性overflow:hidden

### 利用浮动创建多列式布局
用div表示每一列  

width：设置列宽  
float:排成一行  
margin：设置边距

### 固定宽度布局
不会因为用户的扩大或者缩小浏览器窗口而发生变化。  
设计通常以像素作为衡量单位

### 流体布局
随着浏览器的扩大或者缩小而伸展  
通常使用百分比

### 多个样式表

- @import
	-  HTML文件连接到一个样式表，然后这个样式表内来使用@import来导入其他样式表，且必须在其他其他规则的前面
- link
	- 多个link引入样式表
	- 后出现的css优先级比前面的高

## 图像
为图片指定大小能有助于流畅的加载页面。因为HTML和CSS会在图面前加载，告知图片的大小，可以预留图片空间，这样页面不必等待图片加载完成即可显示出来

### 将图片居中

1. 设display:block;
2. margin: 0 auto;

### 子画面sprite
只需请求一个图像，用background-position移动图像

	
	<!DOCTYPE html>
	<html>
		<head>
			<title>Image Rollovers and Sprites</title>
			<style type="text/css">
				a.button {
					height: 36px;
					background-image: url("images/button-sprite.jpg");
					text-indent: -9999px;
					display: inline-block;} //a为内联元素，设置成inline-block可以设置宽度和高度
				a#add-to-basket {
					width: 174px;
					background-position: 0px 0px;}
				a#framing-options {
					width: 210px;
					background-position: -175px 0px;}
				a#add-to-basket:hover {
					background-position: 0px -40px;}
				a#framing-options:hover {
					background-position: -175px -40px;}
				a#add-to-basket:active {
					background-position: 0px -80px;}
				a#framing-options:active {
					background-position: -175px -80px;}
			</style>
		</head>
		<body>
			<a class="button" id="add-to-basket">Add to basket</a>
			<a class="button" id="framing-options">Framing options</a>
		</body>
	</html>

### CSS3：渐变
不同浏览器的设置也不同，下面例子是线性渐变

	<!DOCTYPE html>
	<html>
		<head>
			<title>Gradient</title>
			<style type="text/css">
				#gradient {
					/* fallback color */
					background-color: #66cccc; 
					/* fallback image */
					background-image: url("images/fallback-image.png"); 
					/* Firefox 3.6+ */
					background-image: -moz-linear-gradient(#336666, #66cccc);
					/* Safari 4+, Chrome 1+ */
					background-image: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#66cccc), to(#336666));
					/* Safari 5.1+, Chrome 10+ */
					background-image: -webkit-linear-gradient(#336666, #66cccc); 
					/* Opera 11.10+ */
					background-image: -o-linear-gradient(#336666, #66cccc);
	   				height: 150px;
					width: 300px;}
			</style>
		</head>
		<body>
			<div id="gradient">
			</div>
		</body>
	</html>

## HTML5布局
以前都用\<div\>将每个归类   
HTML5进行了分类，有助于屏幕阅读软件和搜索浏览器

### \<header\>\<footer\>
可以用在：

- 每个网站顶部的主页眉和底部的主页脚
- 页面中单独的\<article\>或\<section\>的页眉和页脚

### \<nav\>导航
### \<article\>
\<article\>可以彼此嵌套

### \<aside\>附属信息

- 在\<article\>内部出现时，应该包含与当前文章相关的信息，而不必涉及页面的整体信息
- 在\<article\>外部出现时，应该包含与整个页面相关的内容

### \<section\>部分
将相关的内容集中在一块，而且每个部分通常都带有一个标题。  

由于\<section\>集中了相关的项目，因此它可能包含具有相同主题或者用途的多个不同\<article\>元素  
相反，如果页面内有一篇很长的文章，\<section\>也可以用来将这篇文章分成几个部分  

\<section\>不能用来做整个页面的容器，应该用\<div\>

### \<hgroup\>标题组
将一个或者多个h1到h6组合在一块，将它们当做一个标题看待

### \<figure\>\<figcaption\>
用来包含一篇文章中引用的任何内容  
\<figure\> 标签规定独立的流内容（图像、图表、照片、代码等等）。
figure 元素的内容应该与主内容相关，但如果被删除，则不应对文档流产生影响。  
所以文章中不可缺少的部分不要用

请使用 \<figcaption\> 元素为 figure 添加标题（caption）。

### 为块级元素添加链接
HTML5新用法

### 让浏览器识别新元素

	header,section,footer,aside,nav,artcle,figure{
			display:block;
	}

IE9之前 JavaScript  HTML5shiv   HTML5shim

## 实用信息
### SEO

- 站内优化
- 站外优化

#### 站内优化
在七个位置加入搜索这个网站的关键词

- 页面标题\<title\>
- URL
- 标题h1-hn
- 正文二到三次的关键词
- 链接文本（而不是单纯的单击这里）
- 图像的alt
- 页面描述\<meta\>

[image-1]:	1.png