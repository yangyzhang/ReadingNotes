# 十天精通CSS3

目前主流浏览器chrome、safari、firefox、opera、甚至360都已经支持了CSS3大部分功能了，IE10以后也开始全面支持CSS3了。

在编写CSS3样式时，不同的浏览器可能需要不同的前缀。它表示该CSS属性或规则尚未成为W3C标准的一部分，是浏览器的私有属性，虽然目前较新版本的浏览器都是不需要前缀的，但为了更好的向前兼容前缀还是少不了的。


![][image-1]

## 第二章 边框
### CSS3边框 圆角效果 border-radius

	border-radius:10px; /* 所有角都使用半径为10px的圆角 */ 
	border-radius: 5px 4px 3px 2px; /* 四个半径值分别是左上角、右上角、右下角和左下角，顺时针 */ 

**实心上半圆**  
方法：把高度(height)设为宽度（width）的一半，并且只设置左上角和右上角的半径与元素的高度一致（大于也是可以的）。

	div{
	        height: 50px;/*是width的一半*/
	        width:100px;
	        background:#9da
	        border-radius:50px; /*半径至少设置为height的值*/
	}

**实心圆**  
方法：把高度(height)设为宽度（width）的一半，并且只设置左上角和右上角的半径与元素的高度一致（大于也是可以的）。  

	div{
	        height:  100px; /*与width设置一致*/
	        width:100px;
	        background: #9da;
	        border-radius: 50px; /*四个圆角值都设置为宽度或高度值的一半*/
	}

### CSS3边框 阴影 box-shadow（一）
box-shadow是向盒子添加阴影。支持添加一个或者多个。

	box-shadow: X轴偏移量 Y轴偏移量 [阴影模糊半径] [阴影扩展半径] [阴影颜色] [投影方式];

![][image-2] 

X 轴偏移量:  左右偏移 （负数向左）
Y 轴偏移量:  上下偏移 （负数向上 ）

**添加多个阴影**

	.box_shadow{
	    box-shadow:4px 2px 6px #f00（右下）, -4px -2px 6px #000（左上）, 0px 0px 12px 5px #33CC00 inset （内部）;
	}

### CSS3边框 阴影 box-shadow（二）
1、**阴影模糊半径**与**阴影扩展半径**的区别  

**阴影模糊半径**：此参数可选，其值只能是为正值，如果其值为0时，表示阴影不具有模糊效果，其值越大阴影的边缘就越模糊；  
**阴影扩展半径**：此参数可选，其值可以是正负值，如果值为正，则整个阴影都延展扩大，反之值为负值时，则缩小；

2、X轴偏移量和Y轴偏移量值可以设置为负数

### CSS3边框 为边框应用图片 border-image
顾名思义就是为边框应用背景图片，它和我们常用的background属性比较相似。例如：

	background:url(xx.jpg) 10px 20px no-repeat;

想象一下：一个矩形，有四个边框。如果应用了边框图片，图片该怎么分布呢？ 图片会自动被切割分成四等分。用于四个边框。

可以理解为它是一个切片工具，会自动把用做边框的图片切割。怎么切割呢？为了方便理解，做了一张特殊的图片，由9个矩形（70\*70像素）拼成的一张图（210\*210像素），并标注好序号，是不是像传说中的九宫图，如下

![][image-3]

根据border-image的语法：

![][image-4]
![][image-5]
![][image-6]
![][image-7]

## 第三章 颜色相关
### CSS3颜色 颜色之RGBA
RGB是一种色彩标准，是由红(R)、绿(G)、蓝(B)的变化以及相互叠加来得到各式各样的颜色。RGBA是在RGB的基础上增加了控制alpha透明度的参数。

	color：rgba(R,G,B,A)

以上R、G、B三个参数，正整数值的取值范围为：0 - 255。百分数值的取值范围为：0.0% - 100.0%。超出范围的数值将被截至其最接近的取值极限。并非所有浏览器都支持使用百分数值。A为透明度参数，取值在0\~1之间，不可为负值。

	background-color:rgba(100,120,60,0.5);


### CSS3颜色 渐变色彩 
CSS3 Gradient 分为线性渐变(linear)和径向渐变(radial)。  
W3C 语法已经得到了 IE10+、Firefox19.0+、Chrome26.0+ 和 Opera12.1+等浏览器的支持。

![][image-8]

参数：  
**第一个参数**:指定渐变方向，可以用“角度”的关键词或“英文”来表示

![][image-9]

第一个参数省略时，默认为“180deg”，等同于“to bottom”。  
**第二个和第三个参数**，表示颜色的起始点和结束点，可以有多个颜色值。

	background-image:linear-gradient(to left, red, orange,yellow,green,blue,indigo,violet);

## 第四章 文字与字体

### CSS3文字与字体 text-overflow 与 word-wrap

	text-overflow:ellipsis; 
	overflow:hidden; 
	white-space:nowrap;
 
text-overflow只是用来说明文字溢出时用什么方式显示，要实现溢出时产生省略号的效果，还须定义强制文本在一行内显示（white-space:nowrap）及溢出内容为隐藏（overflow:hidden），只有这样才能实现溢出文本显示省略号的效果

word-wrap也可以用来设置文本行为，当前行超过指定容器的边界时是否断开转行。

### CSS3文字与字体 嵌入字体@font-face
@font-face能够加载服务器端的字体文件，让浏览器端可以显示用户电脑里没有安装的字体。

	语法：
	
	@font-face {
	    font-family : 字体名称;
	    src : 字体文件在服务器上的相对或绝对路径;
	}

这样设置之后，就可以像使用普通字体一样在（font-\*）中设置字体样式。

	p {
	    font-size :12px;
	    font-family : "My Font";
	    /*必须项，设置@font-face中font-family同样的值*/
	}

### CSS3文字与字体 文本阴影text-shadow
text-shadow可以用来设置文本的阴影效果。

	语法：
	
	text-shadow: X-Offset Y-Offset blur color;


- X-Offset：表示阴影的水平偏移距离，其值为正值时阴影向右偏移，反之向左偏移；      
- Y-Offset：是指阴影的垂直偏移距离，如果其值是正值时，阴影向下偏移，反之向上偏移；
- Blur：是指阴影的模糊程度，其值不能是负值，如果值越大，阴影越模糊，反之阴影越清晰，如果不需要阴影模糊可以将Blur值设置为0；
- Color：是指阴影的颜色，其可以使用rgba色。

	text-shadow: 0 1px 1px #fff

## 第五章 与背景相关的样式
### CSS3背景 background-origin
设置元素背景图片的原始起始位置。

	语法：
	
	background-origin ： border-box | padding-box | content-box;

参数分别表示背景图片是从边框，还是内边距（默认值），或者是内容区域开始显示。

![][image-10]

**需要注意的是，如果背景不是no-repeat，这个属性无效，它会从边框开始显示。**

	background:#ccc url(http://static.mukewang.com/static/img/logo_index.png) no-repeat; 
	background-origin: content-box;

### CSS3背景 background-clip
用来将背景图片做适当的裁剪以适应实际需要。

	语法：
	
	background-clip ： border-box | padding-box | content-box | no-clip

参数分别表示从边框、或内填充，或者内容区域向外裁剪背景。no-clip表示不裁切，和参数border-box显示同样的效果。

![][image-11]

### CSS3背景 background-size
设置背景图片的大小，以长度值或百分比显示，还可以通过cover和contain来对图片进行伸缩。

	语法：
	
	background-size: auto | <长度值> | <百分比> | cover | contain

取值说明：

1. auto：默认值，不改变背景图片的原始高度和宽度；
2. \<长度值\>：成对出现如200px 50px，将背景图片宽高依次设置为前面两个值，当设置一个值时，将其作为图片宽度值来等比缩放；
3. \<百分比\>：0％\~100％之间的任何值，将背景图片宽高依次设置为所在元素宽高乘以前面百分比得出的数值，当设置一个值时同上；
4. cover：顾名思义为覆盖，即将背景图片等比缩放以填满整个容器；
5. contain：容纳，即将背景图片等比缩放至某一边紧贴容器边缘为止。

### CSS3背景 multiple backgrounds
多重背景，也就是CSS2里background的属性外加origin、clip和size组成的新background的多次叠加，缩写时为用逗号隔开的每组值；  
用分解写法时，如果有多个背景图片，而其他属性只有一个（例如background-repeat只有一个），表明所有背景图片应用该属性值。

	语法缩写如下：
	
	background ： [background-color] | [background-image] | [background-position][/background-size] | [background-repeat] | [background-attachment] | [background-clip] | [background-origin],...

可以把上面的缩写拆解成以下形式：

	background-image:url1,url2,...,urlN;
	
	
	background-repeat : repeat1,repeat2,...,repeatN;
	backround-position : position1,position2,...,positionN;
	background-size : size1,size2,...,sizeN;
	background-attachment : attachment1,attachment2,...,attachmentN;
	background-clip : clip1,clip2,...,clipN;
	background-origin : origin1,origin2,...,originN;
	background-color : color;

注意：

1. 用逗号隔开每组 background 的缩写值；
2. 如果有 size 值，需要紧跟 position 并且用 "/" 隔开；
3. 如果有多个背景图片，而其他属性只有一个（例如 background-repeat 只有一个），表明所有背景图片应用该属性值。
4. background-color 只能设置一个。

就是讲的多张图片可以只用写一个标签，只需要写属性的时候用逗号隔开每张图片的属性设置就可以实现图片想要的效果了


## 第六章 CSS3选择器
### CSS3选择器 属性选择器
在CSS2中引入了一些属性选择器，而CSS3在CSS2的基础上对属性选择器进行了扩展，新增了3个属性选择器，使得属性选择器有了通配符的概念
![][image-12]

	<style>
	a[class^=column]{
	    background:red;
	    color:#fff;
	}
	a[href$=doc]{
	    background:green;
	    color:#fff;
	}
	a[title*=box]{
	    background:blue;
	    color:#fff;
	}
	</style>
	
	
	<body>
	<a href="##" class="columnNews">我的背景想变成红色</a>
	<a href="##" class="columnVideo">我的背景想变成红色</a>
	<a href="##" class="columnAboutUs">我的背景想变成红色</a><br/>
	<a href="1.doc">我的背景想变成绿色</a>
	<a href="2.doc">我的背景想变成绿色</a><br/>
	<a href="##" title="this is a box">我的背景想变成蓝色</a>
	<a href="##" title="box1">我的背景想变成蓝色</a>
	<a href="##" title="there is two boxs">我的背景想变成蓝色</a>
	</body>


### CSS3 结构性伪类选择器—root
`:root`选择器，从字面上我们就可以很清楚的理解是根选择器，他的意思就是匹配元素E所在文档的根元素。在HTML文档中，根元素始终是\<html\>。

“:root”选择器等同于\<html\>元素，简单点说：

	:root{background:orange}
	html {background:orange;}

得到的效果等同。  
建议使用:root方法。  
另外在IE９以下还可以借助“:root”实现hack功能。

### CSS3 结构性伪类选择器—not
`:not`选择器称为否定选择器，和jQuery中的:not选择器一模一样，可以选择除某个元素之外的所有元素。就拿form元素来说，比如说你想给表单中除submit按钮之外的input元素添加红色边框，CSS代码可以写成：

	form {
	  width: 200px;
	  margin: 20px auto;
	}
	div {
	  margin-bottom: 20px;
	}
	input:not([type="submit"]){
	  border:1px solid red;
	}

### CSS3 结构性伪类选择器—empty
`:empty`选择器表示的就是空。用来选择没有任何内容的元素，这里没有内容指的是一点内容都没有，**哪怕是一个空格**。

比如说，你的文档中有三个段落p元素，你想把没有任何内容的P元素隐藏起来。我们就可以使用“:empty”选择器来控制。

	HTML代码：
	
	<p>我是一个段落</p>
	<p> </p>
	<p></p>​
	
	CSS代码：
	
	p{
	 background: orange;
	 min-height: 30px;
	}
	p:empty {
	  display: none;
	}​

### CSS3 结构性伪类选择器—target
`:target`选择器称为目标选择器，用来匹配文档(页面)的url的某个标志符的目标元素。

	示例展示
	
	点击链接显示隐藏的段落。
	
	HTML代码：
	
	<h2><a href="#brand">Brand</a></h2>
	<div class="menuSection" id="brand">
	    content for Brand
	</div>
	
	CSS代码：
	
	.menuSection{
	  display: none;
	}
	:target{/*这里的:target就是指id="brand"的div对象*/
	  display:block;
	}

![][image-13]

分析：
1. 具体来说，触发元素的URL中的标志符通常会包含一个#号，后面带有一个标志符名称，上面代码中是：#brand
2. target就是用来匹配id为“brand”的元素（id="brand"的元素）,上面代码中是那个div元素。

**多个url（多个target）处理**：

就像上面的例子，#brand与后面的id="brand"是对应的，当同一个页面上有很多的url的时候你可以取不同的名字，只要#号后对的名称与id=""中的名称对应就可以了。

	如下面例子：
	html代码：  
	
	<h2><a href="#brand">Brand</a></h2>
	<div class="menuSection" id="brand">
	  content for Brand
	</div>
	<h2><a href="#jake">Brand</a></h2>
	<div class="menuSection" id="jake">
	 content for jake
	</div>
	<h2><a href="#aron">Brand</a></h2>
	<div class="menuSection" id="aron">
	    content for aron
	</div>
	
	css代码：
	
	#brand:target {
	  background: orange;
	  color: #fff;
	}
	#jake:target {
	  background: blue;
	  color: #fff;
	}
	#aron:target {
	  background: red;
	  color: #fff;
	}
	
	上面的代码可以对不同的target对象分别设置不的样式。

### CSS3 结构性伪类选择器—first-child
`:first-child`选择器表示的是选择父元素的第一个子元素的元素E。简单点理解就是选择元素中的第一个子元素，**记住是子元素**，而不是后代元素。


[image-1]:	1.png
[image-2]:	2.png
[image-3]:	3.jpeg
[image-4]:	4.jpeg
[image-5]:	5.png
[image-6]:	6.png
[image-7]:	7.png
[image-8]:	8.jpeg
[image-9]:	9.jpeg
[image-10]:	10.png
[image-11]:	11.png
[image-12]:	12.jpeg
[image-13]:	13.jpeg