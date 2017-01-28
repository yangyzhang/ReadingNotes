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

	ul > li 选择了ul下的所有li元素，而ul > li:first-child 只选择了ul下的第一个li元素
	
	HTML代码：
	
	<ol>
	  <li><a href="##">Link1</a></li>
	  <li><a href="##">Link2</a></li>
	  <li><a href="##">link3</a></li>
	</ol>
	
	CSS代码：
	
	ol > li{
	  font-size:20px;
	  font-weight: bold;
	  margin-bottom: 10px;
	}
	
	ol a {
	  font-size: 16px;
	  font-weight: normal;
	}
	
	ol > li:first-child{
	  color: red;
	}
	
	
	实例
	选择属于其父元素的首个子元素的每个 <p> 元素，并为其设置样式：
	p:first-child
	{ 
	background-color:yellow;
	}
	<body>
	<p>这个段落是其父元素（body）的首个子元素。</p>
	<h1>欢迎访问我的主页</h1>
	<p>这个段落不是其父元素的首个子元素。</p>
	<div>
	<p>这个段落是其父元素（div）的首个子元素。</p>
	<p>这个段落不是其父元素的首个子元素。</p>
	</div>
	<p><b>注释：</b>对于 IE8 及更早版本的浏览器中的 :first-child，必须声明 <!DOCTYPE>。</p>
	</body> 



### CSS3 结构性伪类选择器—last-child

“:last-child”选择器与“:first-child”选择器作用类似，不同的是“:last-child”选择器选择的是元素的最后一个子元素。例如，需要改变的是列表中的最后一个“li”的背景色，就可以使用这个选择器，

	ul>li:last-child{background:blue;}

### CSS3 结构性伪类选择器—nth-child(n)
“:nth-child(n)”选择器用来定位某个父元素的一个或多个特定的子元素。其中“n”是其参数，而且可以是整数值(1,2,3,4)，也**可以是表达式(2n+1、-n+5)和关键词(odd、even)**，但参数n的起始值始终是1，而不是0。也就是说，参数n的值为0时，选择器将选择不到任何匹配的元素。

	ol > li:nth-child(2n){
	  background: orange;
	}

### CSS3 结构性伪类选择器—nth-last-child(n)
“:nth-last-child(n)”选择器和前面的“:nth-child(n)”选择器非常的相似，只是这里多了一个“last”，所起的作用和“:nth-child(n)”选择器有所区别，**从某父元素的最后一个子元素开始计算，来选择特定的元素。**

	ol > li:nth-last-child(5){
	  background: orange;
	}

### CSS3 first-of-type选择器
“:first-of-type”选择器类似于“:first-child”选择器，**不同之处就是指定了元素的类型,其主要用来定位一个父元素下的某个类型的第一个子元素。**

	通过“:first-of-type”选择器，定位div容器中的第一个p元素（p不一定是容器中的第一个子元素），并设置其背景色为橙色。
	
	HTML代码：
	
	<div class="wrapper">
	  <div>我是一个块元素，我是.wrapper的第一个子元素</div>
	  <p>我是一个段落元素，我是不是.wrapper的第一个子元素，但是他的第一个段落元素</p>
	  <p>我是一个段落元素</p>
	  <div>我是一个块元素</div>
	</div>
	
	CSS代码：
	
	.wrapper {
	  width: 500px;
	  margin: 20px auto;
	  padding: 10px;
	  border: 1px solid #ccc;
	  color: #fff;
	}
	.wrapper > div {
	  background: green;
	}
	.wrapper > p {
	  background: blue;
	}
	/*我要改变第一个段落的背景为橙色*/
	.wrapper > p:first-of-type {
	  background: orange;
	}

### CSS3 nth-of-type(n)选择器
当某个元素中的子元素不单单是同一种类型的子元素时，使用“:nth-of-type(n)”选择器来定位于父元素中某种类型的子元素是非常方便和有用的。在“:nth-of-type(n)”选择器中的“n”和“:nth-child(n)”选择器中的“n”参数也一样，**可以是具体的整数，也可以是表达式，还可以是关键词。**

	.wrapper > p:nth-of-type(2n){
	  background: orange;
	}

### CSS3 last-of-type选择器

	.wrapper > p:last-of-type{
	  background: orange;
	}

### CSS3 nth-last-of-type(n)选择器
选择父元素中指定的某种子元素类型，但它的起始方向是从最后一个子元素开始，而且它的使用方法类似于上节中介绍的“:nth-last-child(n)”选择器一样。

	.wrapper > p:nth-last-of-type(3){
	  background: orange;
	}

### CSS3 only-child选择器
“:only-child”选择器选择的是父元素中只有一个子元素，而且只有唯一的一个子元素。也就是说，**匹配的元素的父元素中仅有一个子元素，而且是一个唯一的子元素。**

	li {
	  background: green;
	  padding: 10px;
	  margin-bottom: 5px;
	}
	li:only-child {
	  background: orange;
	}

### CSS3 only-of-type选择器
“:only-of-type”选择器用来选择一个元素是它的父元素的唯一一个相同类型的子元素。这样说或许不太好理解，换一种说法。  
“:only-of-type”是表示一个元素他有很多个子元素，而其中只有一种类型的子元素是唯一的，使用“:only-of-type”选择器就可以选中这个元素中的唯一一个类型子元素。

	.wrapper > div:only-of-type {
	  background: orange;
	}
 
 


## 第七章 CSS3选择器

### CSS3选择器 :enabled选择器
在Web的表单中，有些表单元素有可用（“:enabled”）和不可用（“:disabled”）状态，比如输入框，密码框，复选框等。在默认情况之下，这些表单元素都处在可用状态。那么我们可以通过伪选择器“:enabled”对这些表单元素设置样式。

	div {
	  margin: 30px;
	}
	input[type="text"]:enabled {
	  border: 1px solid #f36;
	  box-shadow: 0 0 5px #f36;
	}
	
	input[type="text"]:disabled{
	  box-shadow: none;
	}

### CSS3选择器 :disabled选择器

“:disabled”选择器刚好与“:enabled”选择器相反，用来选择不可用表单元素。要正常使用“:disabled”选择器，需要在表单元素的HTML中设置“disabled”属性。

### CSS3选择器 :checked选择器
在表单元素中，单选按钮和复选按钮都具有选中和未选中状态。（大家都知道，要覆写这两个按钮默认样式比较困难）。在CSS3中，我们可以通过状态选择器“:checked”配合其他标签实现自定义样式。而“:checked”表示的是选中状态。

	通过“:checked”状态来自定义复选框效果。
	
	HTML代码
	
	<form action="#">
	  <div class="wrapper">
	    <div class="box">
	      <input type="checkbox" checked="checked" id="usename" /><span>√</span>
	    </div>
	    <lable for="usename">我是选中状态</lable>
	  </div>
	
	  <div class="wrapper">
	    <div class="box">
	      <input type="checkbox"  id="usepwd" /><span>√</span>
	    </div>
	    <label for="usepwd">我是未选中状态</label>
	  </div>
	</form> 
	
	CSS代码：
	
	form {
	  border: 1px solid #ccc;
	  padding: 20px;
	  width: 300px;
	  margin: 30px auto;
	}
	
	.wrapper {
	  margin-bottom: 10px;
	}
	
	.box {
	  display: inline-block;
	  width: 20px;
	  height: 20px;
	  margin-right: 10px;
	  position: relative;
	  border: 2px solid orange;
	  vertical-align: middle;
	}
	
	.box input {
	  opacity: 0;
	  position: absolute;
	  top:0;
	  left:0;
	}
	
	.box span {
	  position: absolute;
	  top: -10px;
	  right: 3px;
	  font-size: 30px;
	  font-weight: bold;
	  font-family: Arial;
	  -webkit-transform: rotate(30deg);
	  transform: rotate(30deg);
	  color: orange;
	}
	
	input[type="checkbox"] + span {
	  opacity: 0;
	}
	
	input[type="checkbox"]:checked + span {
	  opacity: 1;
	}

![][image-14]

### CSS3选择器 ::selection选择器
“::selection”伪元素是用来匹配突出显示的文本(用鼠标选择文本时的文本)。浏览器默认情况下，用**鼠标选择**网页文本是以“深蓝的背景，白色的字体”显示的

有的时候设计要求,不使用上图那种浏览器默认的突出文本效果，需要一个与众不同的效果，此时“::selection”伪元素就非常的实用。不过在Firefox浏览器还需要添加前缀。

	CSS代码：
	
	::-moz-selection {
	  background: red;
	  color: green;
	}
	::selection {
	  background: red;
	  color: green;
	}

**注意：**

1. IE9+、Opera、Google Chrome 以及 Safari 中支持 ::selection 选择器。
2. Firefox 支持替代的 ::-moz-selection。

### CSS3选择器 :read-only选择器
“:read-only”伪类选择器用来指定处于只读状态元素的样式。简单点理解就是，元素中设置了“readonly=’readonly’”

	input[type="text"]:-moz-read-only{
	  border-color: #ccc;
	}
	input[type="text"]:read-only{
	  border-color: #ccc;
	}

### CSS3选择器 :read-write选择器
“:read-write”选择器刚好与“:read-only”选择器相反，主要用来指定当元素处于非只读状态时的样式。

### CSS3选择器 ::before和::after
::before和::after这两个主要用来给元素的前面或后面插入内容，这两个常和"content"配合使用，**使用的场景最多的就是清除浮动。**

	.clearfix::before,
	.clearfix::after {
	    content: ".";
	    display: block;
	    height: 0;
	    visibility: hidden;
	}
	.clearfix:after {clear: both;}
	.clearfix {zoom: 1;}

单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素


## 第八章 CSS3中的变形与动画

### CSS3变形--旋转 rotate()
旋转rotate()函数通过指定的角度参数使元素相对原点进行旋转。它主要在二维空间内进行操作，设置一个角度值，用来指定旋转的幅度。如果这个值为正值，元素相对原点中心顺时针旋转；如果这个值为负值，元素相对原点中心逆时针旋转。

![][image-15]

	将文本旋转回到原来水平位置。
	.wrapper {
	  margin: 100px auto;
	  width: 300px;
	  height: 200px;
	  border: 2px dotted blue;
	}
	
	.wrapper div{
	  width: 300px;
	  height: 200px;
	  line-height: 200px;
	  text-align: center;
	  background: green;
	  color: #fff;
	  -webkit-transform: rotate(-20deg);
	  -moz-transform: rotate(-20deg);
	  transform:rotate(-20deg);
	}
	.wrapper span {
	  display:block;
	 -webkit-transform: rotate(20deg);
	 -moz-transform: rotate(20deg);
	  transform:rotate(20deg);
	 }
	
	.wrapper span{}中为神马要加display：block;才起作用？
	内联元素也就是行内元素不能更改宽度与高度，只能根据内容来确定要显示的大小，自然就无法旋转等，所以一定要将其转化为块元素它才会具有占据一整行的特性，也就能自由更改宽度和高度。

### CSS3中的变形--扭曲 skew()
扭曲skew()函数能够让元素倾斜显示。它可以将一个对象以其中心位置围绕着X轴和Y轴按照一定的角度倾斜。这与rotate()函数的旋转不同，rotate()函数只是旋转，而不会改变元素的形状。skew()函数不会旋转，而只会改变元素的形状。

Skew()具有三种情况：

- skew(x,y)使元素在水平和垂直方向同时扭曲（X轴和Y轴同时按一定的角度值进行扭曲变形）；

![][image-16]

第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则值为0，也就是Y轴方向上无斜切。

- skewX(x)仅使元素在水平方向扭曲变形（X轴扭曲变形）

![][image-17]

- skewY(y)仅使元素在垂直方向扭曲变形（Y轴扭曲变形）

![][image-18]

	示例演示：
	
	通过skew（）函数将长方形变成平行四边形。
	
	HTML代码：
	
	<div class="wrapper">
	  <div>我变成平形四边形</div>
	</div>
	
	CSS代码：
	
	.wrapper {
	  width: 300px;
	  height: 100px;
	  border: 2px dotted red;
	  margin: 30px auto;
	}
	.wrapper div {
	  width: 300px;
	  height: 100px;
	  line-height: 100px;
	  text-align: center;
	  color: #fff;
	  background: orange;
	  -webkit-transform: skew(45deg);
	  -moz-transform:skew(45deg) 
	  transform:skew(45deg);
	}

### CSS3中的变形--缩放 scale()

缩放 scale()函数 让元素根据中心原点对对象进行缩放。
缩放 scale 具有三种情况：

1.  scale(X,Y)使元素水平方向和垂直方向同时缩放（也就是X轴和Y轴同时缩放）

![][image-19]

	div:hover {
	  -webkit-transform: scale(1.5,0.5);
	  -moz-transform:scale(1.5,0.5)
	  transform: scale(1.5,0.5);
	}
 


** 注意：Y是一个可选参数，如果没有设置Y值，则表示X，Y两个方向的缩放倍数是一样的。**

2. scaleX(x)元素仅水平方向缩放（X轴缩放）
3. scaleY(y)元素仅垂直方向缩放（Y轴缩放）

**注意： scale()的取值默认的值为1，当值设置为0.01到0.99之间的任何值，作用使一个元素缩小；而任何大于或等于1.01的值，作用是让元素放大。**

### CSS3中的变形--位移 translate()
translate()函数可以将元素向指定的方向移动，类似于position中的relative。或以简单的理解为，使用translate()函数，可以把元素从原来的位置移动，而不影响在X、Y轴上的任何Web组件。

translate我们分为三种情况：

1. translate(x,y)水平方向和垂直方向同时移动（也就是X轴和Y轴同时移动）
2. translateX(x)仅水平方向移动（X轴移动
3. translateY(Y)仅垂直方向移动（Y轴移动）


让不知道宽度和高度的元素实现水平、垂直居中。

	.wrapper {
	      padding: 20px;
	      background:orange;
	      color:#fff;
	      position:absolute;
	      top:50%;
	      left:50%;
	      border-radius: 5px;
	      -webkit-transform:translate(-50%,-50%);
	      -moz-transform:translate(-50%,-50%);
	      transform:translate(-50%,-50%);
	    }
 
 

1. top：50%，left：50%，是将色块的左上角定位在了屏幕的中央，但是，整体并不在中央；
2. translate的百分比是根据自身的宽度和高度来定的，translate(-50%,-50%) 配合 top：50%，left：50% 实现了居中

关于translate和position：

relative的区别：  
相同点：两者都是相对于本身移动位置  
区别：
 1. 当元素原来已经有position:absolute的时候，这时候你想相对于本身移动，可以使用translate
2. 做动画的时候translate更适合，不会引起页面的重排和重绘 
3. 关于transform类的，可以使用GPU加速，提高浏览器的性能？

 总之：transform更适用于动画 

### CSS3中的变形--矩阵 matrix()
matrix() 是一个含六个值的(a,b,c,d,e,f)变换矩阵，用来指定一个2D变换，相当于直接应用一个a b c d e f变换矩阵。就是基于水平方向（X轴）和垂直方向（Y轴）重新定位元素,此属性值使用涉及到数学中的矩阵，我在这里只是简单的说一下CSS3中的transform有这么一个属性值，

### CSS3中的变形--原点 transform-origin
任何一个元素都有一个中心点，默认情况之下，其中心点是居于元素X轴和Y轴的50%处。

在没有重置transform-origin改变元素原点位置的情况下，**CSS变形进行的旋转、位移、缩放，扭曲等操作都是以元素自己中心位置进行变形**。但很多时候，我们可以通过transform-origin来对元素进行原点位置改变，使元素原点不在元素的中心位置，以达到需要的原点位置。

### CSS3中的动画--过渡属性 transition-property
CSS3中新增加了一个新的模块transition，它可以通过一些简单的CSS事件来触发元素的外观变化，让效果显得更加细腻。简单点说，就是通过鼠标的单击、获得焦点，被点击或对元素任何改变中触发，并平滑地以动画效果改变CSS的属性值。

	在CSS中创建简单的过渡效果可以从以下几个步骤来实现：
	第一，在默认样式中声明元素的初始状态样式；
	第二，声明过渡元素最终状态样式，比如悬浮状态；
	第三，在默认样式中通过添加过渡函数，添加一些不同的样式。


- transition-property:指定过渡或动态模拟的CSS属性
	- transition-duration:指定完成过渡所需的时间
	- transition-timing-function:指定过渡函数
	- transition-delay:指定开始出现的延迟时间  


transition-property用来指定过渡动画的CSS属性名称，而这个过渡属性只有具备一个中点值的属性（需要产生动画的属性）才能具备过渡效果，其对应具有过渡的CSS属性主要有：

![][image-20]

	div {
	  width: 200px;
	  height: 200px;
	  background: red;
	  margin: 20px auto;
	  -webkit-transition-property: width;
	  transition-property: width;
	  -webkit-transition-duration:.5s;
	  transition-duration:.5s;
	  -webkit-transition-timing-function: ease-in;
	  transition-timing-function: ease-in;
	  -webkit-transition-delay: .18s;
	    transition-delay:.18s;
	}
	div:hover {
	  width: 400px;
	}

特别注意：当“transition-property”属性设置为all时，表示的是所有中点值的属性。  
用一个简单的例子来说明这个问题：  
假设你的初始状态设置了样式“width”,“height”,“background”,当你在终始状态都改变了这三个属性，那么all代表的就是“width”、“height”和“background”。如果你的终始状态只改变了“width”和“height”时，那么all代表的就是“width”和“height”。


### CSS3中的动画--过渡所需时间 transition-duration

transition-duration属性主要用来设置一个属性过渡到另一个属性所需的时间，也就是从旧属性过渡到新属性花费的时间长度，俗称持续时间。

### CSS3中的动画--过渡函数 transition-timing-function
transition-timing-function属性指的是过渡的“缓动函数”。主要用来指定浏览器的过渡速度，以及过渡期间的操作进展情况，其中要包括以下几种函数：

![][image-21]

### CSS3中的动画--过渡延迟时间 transition-delay
ransition-delay属性和transition-duration属性极其类似，不同的是transition-duration是用来设置过渡动画的持续时间，而**transition-delay主要用来指定一个动画开始执行的时间，也就是说当改变元素属性值后多长时间开始执行**。

有时我们想改变两个或者多个css属性的transition效果时，只要把几个transition的声明串在一起，用逗号（“，”）隔开，然后各自可以有各自不同的延续时间和其时间的速率变换方式。但需要值得注意的一点：第一个时间的值为 transition-duration，第二个为transition-delay。

	例如：a{ transition: background 0.8s ease-in 0.3,color 0.6s ease-out 0.3;}

## 第九章 CSS3中的变形与动画

### CSS3 Keyframes介绍
Keyframes被称为关键帧，其类似于Flash中的关键帧。在CSS3中其主要以“@keyframes”开头，后面紧跟着是动画名称加上一对花括号“{…}”，括号中就是一些不同时间段样式规则。

	@keyframes changecolor{
	  0%{
	   background: red;
	  }
	  100%{
	    background: green;
	  }
	}

在一个“@keyframes”中的样式规则可以由多个百分比构成的，如在“0%”到“100%”之间创建更多个百分比，分别给每个百分比中给需要有动画效果的元素加上不同的样式，从而达到一种在不断变化的效果。

**经验与技巧**：在@keyframes中定义动画名称时，其中0%和100%还可以使用关键词from和to来代表，其中0%对应的是from，100%对应的是to。

浏览器的支持情况：  
Chrome 和 Safari 需要前缀 -webkit-；Foxfire 需要前缀 -moz-。

	@keyframes changecolor{
	  0%{
	    background: red;
	  }
	  20%{
	    background:blue;
	  }
	  40%{
	    background:orange;
	  }
	  60%{
	    background:green;
	  }
	  80%{
	    background:yellow;
	  }
	  100%{
	    background: red;
	  }
	}
	div {
	  width: 300px;
	  height: 200px;
	  background: red;
	  color:#fff;
	  margin: 20px auto;
	}
	div:hover {
	  animation: changecolor 5s ease-out .2s;
	}

### CSS3中调用动画

animation-name属性主要是用来调用 @keyframes 定义好的动画。需要特别注意: animation-name 调用的动画名需要和“@keyframes”定义的动画名称完全一致（区分大小写），如果不一致将不具有任何动画效果。


语法：

	animation-name: none | IDENT[,none|DENT]*;

1. IDENT是由 @keyframes 创建的动画名，上面已经讲过了（animation-name 调用的动画名需要和“@keyframes”定义的动画名称完全一致）；
2. none为默认值，当值为 none 时，将没有任何动画效果,这可以用于覆盖任何动画。

注意：需要在 Chrome 和 Safari 上面的基础上加上-webkit-前缀，Firefox加上-moz-。

	<body>
	<div><span></span></div>
	
	</body>
	
	@keyframes around{
	  0% {
	    transform: translateX(0);
	  }
	  25%{
	    transform: translateX(180px);
	  }
	  50%{
	     transform: translate(180px, 180px); 
	  }
	  75%{
	    transform:translate(0,180px);
	  }
	  100%{
	    transform: translateY(0);
	  }
	}
	div {
	  width: 200px;
	  height: 200px;
	  border: 1px solid red;
	  margin: 20px auto;
	}
	div span {
	  display: inline-block;
	  width: 20px;
	  height: 20px;
	  background: orange;
	  border-radius: 100%;
	  animation-name:around;
	  animation-duration: 10s;
	  animation-timing-function: ease;
	  animation-delay: 1s;
	  animation-iteration-count:infinite;
	}

### CSS3中设置动画播放时间
animation-duration主要用来设置CSS3动画播放时间，其使用方法和transition-duration类似，是用来指定元素播放动画所持续的时间长，也就是完成从0%到100%一次动画所需时间。单位：S秒

	@keyframes toradius{
	  from {
	    border-radius: 0;
	  }
	  to {
	    border-radius: 100%;
	  }
	}
	div {
	  width: 200px;
	  height: 200px;
	  line-height: 200px;
	  text-align: center;
	  color: #fff;
	  background: green;
	  margin: 20px auto;
	}
	div:hover {
	  animation-name: toradius;
	  animation-duration: 10s;
	  animation-timing-function: ease-in-out;
	  animation-delay: .1s;
	}

### CSS3中设置动画播放方式
**animation-timing-function**属性主要用来设置动画播放方式。主要让元素根据时间的推进来改变属性值的变换速率，简单点说就是动画的播放方式。

	animation-timing-function:ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier(<number>, <number>, <number>, <number>) [, ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier(<number>, <number>, <number>, <number>)]*


### CSS3中设置动画开始播放的时间
**animation-delay**属性用来定义动画开始播放的时间，用来触发动画播放的时间点。和transition-delay属性一样，用于定义在浏览器开始执行动画之前等待的时间。

### CSS3中设置动画播放次数
**animation-iteration-count**属性主要用来定义动画的播放次数。

	animation-iteration-count: infinite | <number> [, infinite | <number>]*

1. 其值通常为整数，但也可以使用带有小数的数字，其默认值为1，这意味着动画将从开始到结束只播放一次。
2. 如果取值为infinite，动画将会无限次的播放。

### CSS3中设置动画播放方向
**animation-direction**属性主要用来设置动画播放方向，其语法规则如下：

	animation-direction:normal | alternate [, normal | alternate]*

其主要有两个值：normal、alternate

1. normal是默认值，如果设置为normal时，动画的每次循环都是向前播放；
2. 另一个值是alternate，奇数次播放动画是按顺序播放各帧动画，偶数次播放动画是按逆序播放各帧动画。

### CSS3中设置动画的播放状态
**animation-play-state**属性主要用来控制元素动画的播放状态。

参数：
其主要有两个值：running和paused。

其中running是其默认值，主要作用就是类似于音乐播放器一样，可以通过paused将正在播放的动画停下来，也可以通过running将暂停的动画重新播放，这里的重新播放不一定是从元素动画的开始播放，而是从暂停的那个位置开始播放。另外如果暂停了动画的播放，元素的样式将回到最原始设置状态。

	@keyframes move {
	  0%{
	    transform: translateY(90px);
	  }
	  15%{
	    transform: translate(90px,90px);
	  }
	  30%{
	    transform: translate(180px,90px);
	  }
	  45%{
	    transform: translate(90px,90px);
	  }
	  60%{
	    transform: translate(90px,0);
	  }
	  75%{
	    transform: translate(90px,90px);
	  }
	  90%{
	    transform: translate(90px,180px);
	  }
	  100%{
	    transform: translate(90px,90px);
	  }
	}
	
	div {
	  width: 200px;
	  height: 200px;
	  border: 1px solid red;
	  margin: 20px auto;
	}
	span {
	  display: inline-block;
	  width: 20px;
	  height: 20px;
	  background: orange;
	  transform: translateY(90px);
	  animation-name: move;
	  animation-duration: 10s;
	  animation-timing-function: ease-in;
	  animation-delay: .2s;
	  animation-iteration-count:infinite;
	  animation-direction:alternate;
	  animation-play-state:running;
	}
	div:hover span {
	  animation-play-state:paused;
	}

### CSS3中设置动画时间外属性

**animation-fill-mode**属性定义在动画开始之前和结束之后发生的操作。主要具有四个属性值：none、forwards、backwords和both。其四个属性值对应效果如下：

![][image-22]

	@keyframes redToBlue{
	  from{
	    background: red;
	  }
	  20%{
	      background:green;
	  }
	  40%{
	      background:lime;
	  }
	  60%{
	      background:yellow;
	  }
	  to{
	    background:blue;
	  }
	}
	
	div {
	  width: 200px;
	  height: 200px;
	  background: red;
	  margin: 20px auto;
	  animation-name:redToBlue;
	  animation-duration: 20s;
	  animation-timing-function: ease;
	  animation-delay: 1s;
	  animation-fill-mode: backwards; 
	}



将div的默认样式改成黑色就很好看清楚了。如果没有animation-delay的话没有区别，加了delay：1s之后，

1. none在delay的1s内会呈现初始样式效果。
2. backwards在delay的1s内会呈现第一帧的样式效果。
3. forwards会在动画结束之后保持最后一帧的样式效果。
4. both会在delay的1s内呈现第一帧的样式效果，并且在动画结束之后保持最后一帧的样式效果。

## 第十章 布局样式相关

### CSS3 多列布局——Columns

	columns：<column-width> || <column-count>

- \<column-width\>
	- 主要用来定义多列中每列的宽度
- \<column-count\>
	- 主要用来定义多列中的列数

	举例：要显示2栏显示，每栏宽度为200px，代码为：
	 
	columns: 200px 2;

	.columns {
	  width: 500px;
	  padding: 5px;
	  border: 1px solid green;
	  margin: 20px auto; 
	  -webkit-columns: 150px 3;
	  -moz-columns: 150px 3;
	  -o-columns:150px 3;
	  -ms-columns: 150px 3;
	  columns: 150px 3;
	}

### CSS3 多列布局——column-width
column-width的使用和CSS中的width属性一样，不过不同的是，column-width属性在定义元素列宽的时候，既可以单独使用，也可以和多列属性中其他属性配合使用。其基本语法如下所示 ；

column-width: auto | \<length\>

- auto
	- 如果column-width设置值为auto或者没有显式的设置值时，元素多列的列宽将由其他属性来决定，比如前面的示例就是由列数column-count来决定。
- \<length\>
	- 使用固定值来设置元素列的宽度，其主要是由数值和长度单位组成，不过其值只能是正值，不能为负值。

	.columns {
	  padding: 5px;
	  border: 1px solid green;
	  width: 900px;
	  margin: 20px auto;
	  column-width:200px;
	  -webkit-column-width:200px;
	  -o-column-width:200px;
	  -moz-column-width:200px;
	  -ms-column-width:200px;
	  -webkit-column-count:3;
	  -moz-column-count:3;
	  -o-column-count:3;
	  -ms-column-count:3;
	  column-count:3;
	}

### CSS3 多列布局——column-count

column-count属性主要用来给元素指定想要的列数和允许的最大列数。其语法规则：

	column-count：auto | <integer>

- auto
	- 此值为column-count的默认值，表示元素只有一列，其主要依靠浏览器计算自动设置。
- \<integer\>
	- 此值为正整数值，主要用来定义元素的列数，取值为大于0的整数，负值无效。
### CSS3 列间距column-gap

column-gap主要用来设置列与列之间的间距，其语法规则如下：

	column-gap: normal || <length>

- normal
	- 默认值，默值为1em（如果你的字号是px，其默认值为你的font-size值）。
- \<length\>
	- 此值用来设置列与列之间的距离，其可以使用px,em单位的任何整数值，但不能是负值

### CSS3 列表边框column-rule
column-rule主要是用来定义列与列之间的**边框宽度、边框样式和边框颜色**。简单点说，就有点类似于常用的border属性。但column-rule是不占用任何空间位置的，在列与列之间改变其宽度不会改变任何列的位置。

为了能有效区分栏目列之间的关系，可以为其设置一个列边框

语法规则：

	column-rule:<column-rule-width>|<column-rule-style>|<column-rule-color>

- column-rule-width
	- 类似于border-width属性，主要用来定义列边框的宽度，其默认值为“medium”，column-rule-width属性接受任意浮点数，但不接收负值。但也像border-width属性一样，可以使用关键词：medium、thick和thin。
- column-rule-style
	- 类似于border-style属性，主要用来定义列边框样式，其默认值为“none”。column-rule-style属性值与border-style属值相同，包括none、hidden、dotted、dashed、solid、double、groove、ridge、inset、outset。
- column-rule-color
	- 类似于border-color属性，主要用来定义列边框颜色，其默认值为前景色color的值，使用时相当于border-color。column-rule-color接受所有的颜色。如果不希望显示颜色，也可以将其设置为transparent(透明色)

### CSS3 跨列设置column-span

column-span主要用来定义一个分列元素中的子元素能跨列多少。column-width、column-count等属性能让一元素分成多列，不管里面元素如何排放顺序，他们都是从左向右的放置内容，但有时我们需要基中一段内容或一个标题不进行分列，也就是横跨所有列，此时column-span就可以轻松实现，此属性的语法如下。
`column-span: none | all`


将第一个标题跨越所有列，代码：

	column-span:all;
	
	h2,
	p:nth-child(2n){
	  -webkit-column-span:all;
	  -moz-column-span:all;
	  -o-column-span:all;
	  -ms-column-span:all;
	  column-span:all;
	}

### CSS3 盒子模型

在CSS3中新增加了box-sizing属性，能够事先定义盒模型的尺寸解析方式，其语法规则如下：

	box-sizing: content-box | border-box | inherit

- content-box
	- 默认值，其让元素维持W3C的标准盒模型，也就是说元素的宽度和高度（width/height）等于元素边框宽度（border）加上元素内距（padding）加上元素内容宽度或高度（content width/ height），也就是element width/height = border + padding + content width / height
- border-box
	- 重新定义CSS2.1中盒模型组成的模式，让元素维持IE传统的盒模型（IE6以下版本和IE6-7怪异模式），也就是说元素的宽度或高度等于元素内容的宽度或高度。从上面盒模型介绍可知，这里的内容宽度或高度包含了元素的border、padding、内容的宽度或高度（此处的内容宽度或高度＝盒子的宽度或高度—边框—内距）。
- inherit
	- 使元素继承父元素的盒模型模式

![][image-23]

### CSS3 伸缩布局

CSS3引入了一种新的布局模式——**Flexbox布局**，即伸缩布局盒模型（Flexible Box），用来提供一个更加有效的方式制定、调整和分布一个容器里项目布局，即使它们的大小是未知或者动态的，这里简称为Flex。


综合而言，Flexbox布局功能主要具有以下几点：

1. 屏幕和浏览器窗口大小发生改变也可以灵活调整布局；
2. 可以指定伸缩项目沿着主轴或侧轴按比例分配额外空间（伸缩容器额外空间），从而调整伸缩项目的大小；
3. 可以指定伸缩项目沿着主轴或侧轴将伸缩容器额外空间，分配到伸缩项目之前、之后或之间；
4. 可以指定如何将垂直于元素布局轴的额外空间分布到该元素的周围；
5. 可以控制元素在页面上的布局方向；
6. 可以按照不同于文档对象模型（DOM）所指定排序方式对屏幕上的元素重新排序。也就是说可以在浏览器渲染中不按照文档流先后顺序重排伸缩项目顺序。


Flexbox规范版本众多，浏览器对此语法支持度也各有不同，接下来的内容以最新语法版本为例向大家展示：

- 创建一个flex容器
	-  任何一个flexbox布局的第一步是需要创建一个flex容器。为此给元素设置display属性的值为flex。在Safari浏览器中，你依然需要添加前缀-webkit，

		.flexcontainer{ display: -webkit-flex; display: flex; }

- Flex项目显示
	- Flex项目是Flex容器的子元素。他们沿着主要轴和横轴定位。默认的是沿着水平轴排列一行。你可以通过flex-direction来改变主轴方向修改为column，其默认值是row。

- Flex项目列显示

	.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: column; flex-direction: column; }

- .Flex项目移动到顶部
	- 如何将flex项目移动到顶部，取决于主轴的方向。如果它是垂直的方向通过align-items设置；如果它是水平的方向通过justify-content设置。

`.flexcontainer{ -webkit-flex-direction: column; flex-direction: column; -webkit-justify-content: flex-start; justify-content: flex-start; }`


- Flex项目移到左边
	- flex项目称动到左边或右边也取决于主轴的方向。如果flex-direction设置为row，设置justify-content控制方向；如果设置为column，设置align-items控制方向。

- Flex项目移动右边

	.flexcontainer{ display: -webkit-flex; display: flex; -webkit-flex-direction: row; flex-direction: row; -webkit-justify-content: flex-end; justify-content: flex-end; }

- 7.水平垂直居中
	- 在Flexbox容器中制作水平垂直居中是微不足道的。设置justify-content或者align-items为center。另外根据主轴的方向设置flex-direction为row或column。

- Flex项目实现自动伸缩
- 您可以定义一个flex项目，如何相对于flex容器实现自动的伸缩。需要给每个flex项目设置flex属性设置需要伸缩的值。

	.bigitem{ -webkit-flex:200; flex:200; }  .smallitem{ -webkit-flex:100; flex:100; }

## 第十一章 Media Queries 与 Responsive 设计

### Media Queries——媒体类型（一）
在本节中，将会学到如何使用CSS3中的Media Queries模块来让一个页面适应不同的终端（或屏幕尺寸），从而让你的页面让用户有一个更好的体验。

**Media Queries**

Media Queries是CSS3新增加的一个模块功能，其最大的特色就是通过CSS3来查询媒体，然后调用对应的样式。其实这个功能在CSS2.1中就有出现过，只不过那个时候此功能并不强大，我们最常见的就是给打印设备添加打印样式。随着时代的变化，这个模块功能越来越强大。

了解Media Queries我们需要了解其中的两个重要部分，第一个是媒体类型，第二个是媒体特性。下面的内容我们简单的来了解这两个部分：

#### 一、媒体类型

**媒体类型（Media Type）**在CSS2中是一个常见的属性，也是一个非常有用的属性，可以通过媒体类型对不同的设备指定不同的样式。

W3C总共列出了10种媒体类型。如下表所示：

- All
	- 所有设备
- Braille
	- 盲人用点字法触觉回馈设备
- Embossed
	- 盲文打印机
- Handheld
	- 便携设备
- Print
	- 打印用纸或打印预览视图
- Projection
	- 各种投影设备
- Screen
	- 电脑显示器
- Speech
	- 语音或音频合成器
- Tv
	- 电视机类型设备
- Tty
	- 使用固定密度字母栅格的媒介，比如电传打字机和终端

**其中Screen、All和Print为最常见的三种媒体类型。**

### media queries——媒体类型（二）
在实际中媒体类型有近十种之多，实际之中常用的也就那么几种，不过媒体类型的引用方法也有多种，常见的有：**link标签、@import和CSS3新增的@media几种：**

#### link方法
link方法引入媒体类型其实就是在\<link\>标签引用样式的时候，通过link标签中的media属性来指定不同的媒体类型。如下所示。

	<link rel="stylesheet" type="text/css" href="style.css" media="screen" />
	<link rel="stylesheet" type="text/css" href="print.css" media="print" />

#### @import方法
@import可以引用样式文件，同样也可以用来引用媒体类型。@import引入媒体类型主要有两种方式，一种是在样式中通过@import调用另一个样式文件；另一种方法是在\<head\>\</head\>标签中的\<style\>\</style\>中引入，但这种使用方法在IE6\~7都不被支持，如样式文件中调用另一个样式文件时，就可以指定对应的媒体类型。

	@importurl(reset.css) screen;   
	@importurl(print.css) print;
	在<head>中的<style>标签中引入媒体类型方法。
	
	<head>
	<style type="text/css">
	    @importurl(style.css) all;
	</style>
	</head>


#### @media方法
@media是CSS3中新引进的一个特性，被称为媒体查询。在页面中也可以通过这个属性来引入媒体类型。@media引入媒体类型和@import有点类似也具有两方式。
（1）在样式文件中引用媒体类型：

	@media screen {
	   选择器{/*你的样式代码写在这里…*/}
	}

（2）使用@media引入媒体类型的方式是在\<head\>标签中的\<style\>中引用。

	<head>
	<style type="text/css">
	    @media screen{
	    选择器{/*你的样式代码写在这里…*/}
	}
	</style>
	</head>


### Media Queries使用方法
Media Queries要如何使用？

Media Queries的使用方法如下。

	@media 媒体类型and （媒体特性）{你的样式}

Media Queries在实际项目中常用的方式:

-  最大宽度max-width
	- “max-width”是媒体特性中最常用的一个特性，其意思是指媒体类型小于或等于指定的宽度时，样式生效。如：

	@media screen and (max-width:480px){
	 .ads {
	   display:none;
	  }
	}
	表示的是：当屏幕小于或等于480px时,页面中的广告区块（.ads）都将被隐藏。

- 最小宽度min-width
	- “min-width”与“max-width”相反，指的是媒体类型大于或等于指定宽度时，样式生效。

	@media screen and (min-width:900px){
	.wrapper{width: 980px;}
	}


- 多个媒体特性使用
	- Media Queries可以使用关键词"and"将多个媒体特性结合在一起。也就是说，一个Media Query中可以包含0到多个表达式，表达式又可以包含0到多个关键字，以及一种媒体类型。

	当屏幕在600px~900px之间时，body的背景色渲染为“#f5f5f5”，如下所示。
	@media screen and (min-width:600px) and (max-width:900px){
	  body {background-color:#f5f5f5;}
	}

- 设备屏幕的输出宽度Device Width
	- 在智能设备上，例如iPhone、iPad等，还可以根据屏幕设备的尺寸来设置相应的样式（或者调用相应的样式文件）。同样的，对于屏幕设备同样可以使用“min/max”对应参数，如“min-device-width”或者“max-device-width”。

	<link rel="stylesheet" media="screen and (max-device-width:480px)" href="iphone.css" />
	上面的代码指的是“iphone.css”样式适用于最大设备宽度为480px，比如说iPhone上的显示，这里的“max-device-width”所指的是设备的实际分辨率，也就是指可视面积分辨率。

- not关键词
	- 使用关键词“not”是用来排除某种制定的媒体类型，也就是用来排除符合表达式的设备。换句话说，not关键词表示对后面的表达式执行取反操作，如：

	@media not print and (max-width: 1200px){样式代码}
	上面代码表示的是：样式代码将被使用在除打印设备和设备宽度小于1200px下所有设备中。

- only关键词
	- only用来指定某种特定的媒体类型，可以用来排除不支持媒体查询的浏览器。其实only很多时候是用来对那些不支持Media Query但却支持Media Type的设备隐藏样式表的。其主要有：支持媒体特性的设备，正常调用样式，此时就当only不存在；表示不支持媒体特性但又支持媒体类型的设备，这样就会不读样式，因为其先会读取only而不是screen；另外不支持Media Queries的浏览器，不论是否支持only，样式都不会被采用。如

	<linkrel="stylesheet" media="only screen and (max-device-width:240px)" href="android240.css" />

	在Media Query中如果没有明确指定Media Type，那么其默认为all，如：
	
	<linkrel="stylesheet" media="(min-width:701px) and (max-width:900px)" href="mediu.css" />

	另外在样式中，还可以使用多条语句来将同一个样式应用于不同的媒体类型和媒体特性中，指定方式如下所示。
	
	<linkrel="stylesheet" type="text/css" href="style.css" media="handheld and (max-width:480px), screen and (min-width:960px)" />

### Responsive设计（一）

响应式设计要考虑元素布局的秩序，而且还需要做到“有求必应”，那就需要满足以下三个条件：

- 网站必须建立灵活的网格基础；
- 引用到网站的图片必须是可伸缩的；
- 不同的显示风格，需要在Media Queries上写不同的样式。

要了解Responsive，就得先了解他的一些术语：

1. 流体网格

	流体网格是一个简单的网格系统，这种网格设计参考了流体设计中的网格系统，将每个网格格子使用百分比单位来控制网格大小。这种网格系统最大的好处是让你的网格大小随时根据屏幕尺寸大小做出相对应的比例缩放。

2. 弹性图片

	弹性图片指的是不给图片设置固定尺寸，而是根据流体网格进行缩放，用于适应各种网格的尺寸。而实现方法是比较简单，一句代码就能搞定的事情。

	img {max-width:100%;}
	不幸的是，这句代码在IE8浏览器存在一个严重的问题，让你的图片会失踪。当然弹性图片在响应式设计中如何更好的实现，到目前为止都还存在争议，也还在不断的改善之中。

为每一个断点提供不同的图片，这是一个比较头痛的事情，因为Media Queries并不能改变图片“src”的属性值，那有没有办分法可以解决呢？

解决方法:  
使用background-image给元素使用背景图片，显示/隐藏父元素，给父元素使用不同的图片，然后通过Media Queries来控制这些图片显示或隐藏。

	来看一个断点解决图片自适应的例子。
	
	<img src="image.jpg" data-src-600px="image-600px.jpg" data-src-800px="image-800px.jpg" alt="" />

	对应的CSS代码：
	
	@media (min-device-width:600px){
	img[data-src-600px]{
	  content: attr(data-src-600px,url);
	  }
	}
	@media (min-device-width:800px){
	  img[data-src-800px] {
	  content:attr(data-src-800px,url);
	  }
	}

**请注意：这仅仅是解决响应式图片自适应的一种思路，但这种方案仅仅适配的断点较少。并不太实用，此处仅为扩展同学们的思路。

3. 媒体查询

媒体查询在CSS3中得到了强大的扩展。使用这个属性可以让你的设计根据用户终端设备适配对应的样式。这也是响应式设计中最为关键的。可以说Responsive设计离开了Medial Queries就失去了他生存的意义。

简单的说媒体查询可以根据设备的尺寸，查询出适配的样式。Responsive设计最关注的就是：根据用户的使用设备的当前宽度，你的Web页面将加载一个备用的样式，实现特定的页面风格。

4. 屏幕分辨率

	屏幕分辨简单点说就是用户显示器的分辨率,屏幕分辨率指的是用户使用的设备浏览您的Web页面时的显示屏幕的分辨率

	Responsive设计利用Media Queries属性针对浏览器使用的分辨率来适配对应的CSS样式。因此屏幕分辨率在Responsive设计中是一个很重要的东西，因为只有知道Web页面要在哪种分辨率下显示何种效果，才能调用对应的样式。

5. 主要断点

	主要断点, 简单的描述就是，设备宽度的临界点。在Media Queries中，其中媒体特性“min-width”和“max-width”对应的属性值就是响应式设计中的断点值。简单点说，就是使用主要断点和次要断点，创建媒体查询的条件。而每个断点会对应调用一个样式文件（或者样式代码）

![][image-24]

上图的style.css样式文件运用在Web页面中，但这个样式文件包括了所有风格的样式代码，也就是说所有设备下显示的风格都通过这个样式文件下载下来。当然，在实际中还可以使用另一种方法，也就是在不同的断点加载不同的样式文件，如下图所示。

![][image-25]

上图主要显示的是主要断点，主要断点加载的不同样式文件直接将影响Web的效果。除了主要断点之外，为了满足更多效果时，还可以在这个基础上添次要断点。不过主要断点和次要断点增加之后，需要维护的样式也相应的增加，成本也相对应的增加。因此在实际使用中，需要根据自身产品需求，决定断点。

综合下来，设置断点应把握三个要点：满足主要的断点；有可能的话添加一些别的断点；设置高于1024的桌面断点。

### Responsive布局技巧

在Responsive布局中，可以毫无保留的丢弃：

1. 尽量少用无关紧要的div；
2. 不要使用内联元素（inline）；
3. 尽量少用JS或flash；
4. 丢弃没用的绝对定位和浮动样式；
5. 摒弃任何冗余结构和不使用100%设置。

有舍才有得，丢弃了一些对Responsive有影响的东东，那么有哪些东东能帮助Responsive确定更好的布局呢？

1. 使用HTML5 Doctype和相关指南；
2. 重置好你的样式（reset.css）；
3. 一个简单的有语义的核心布局；
4. 给重要的网页元素使用简单的技巧，比如导航菜单之类元素。

使用这些技巧，无非是为了保持你的HTML简单干净，而且在你的页面布局中的关键部分（元素）不要过分的依赖现代技巧来实现，比如说CSS3特效或者JS脚本。

### Responsive设计——meta标签

meta标签被称为可视区域meta标签，其使用方法如下。

	<meta name=”viewport” content=”” />

在content属性中主要包括以下属性值，用来处理可视区域。

![][image-26]

在实际项目中，为了让Responsive设计在智能设备中能显示正常，也就是浏览Web页面适应屏幕的大小，显示在屏幕上，可以通过这个可视区域的meta标签进行重置，告诉他使用设备的宽度为视图的宽度，也就是说禁止其默认的自适应页面的效果，具体设置如下：

	<meta name=”viewport” content=”width=device-width,initial-scale=1.0” />
	

另外一点，由于Responsive设计是结合CSS3的Media Queries属性，才能尽显Responsive设计风格，但大家都清楚，在IE6-8中完全是不支持CSS3 Media。下面我们一起来看看CSS3 Meida Queries在标准设备上的运用，大家可以把这些样式加到你的样式文件中，或者单独创建一个名为“responsive.css”文件，并在相应的条件中写上你的样式，让他适合你的设计需求。

	脚本下载地址： 
	
	media-queries.js(http://code.google.com/p/css3-mediaqueries-js/)      
	
	 respond.js(https://github.com/scottjehl/Respond)
	
	 <!—[if lt IE9]>
	      <scriptsrc=http://css3-mediaqueries-js.googlecode.com/svn/trunk/css3-mediaqueries.js></script>
	 ​<![endif]>

### Responsive设计——不同设备的分辨率设置

CSS3 Meida Queries在标准设备上的运用，大家可以把这些样式加到你的样式文件中，或者单独创建一个名为“responsive.css”文件，并在相应的条件中写上你的样式，让他适合你的设计需求：

	1.1024px显屏
	
	@media screen and (max-width : 1024px) {                    
	/* 样式写在这里 */          
	}     
	2.800px显屏
	
	@media screen and (max-width : 800px) {              
	/* 样式写在这里 */          
	}     
	3.640px显屏
	
	@media screen and (max-width : 640px) {              
	/* 样式写在这*/            
	}     
	4.iPad横板显屏
	
	@media screen and (max-device-width: 1024px) and (orientation: landscape) {              
	/* 样式写在这 */            
	}     
	5.iPad竖板显屏
	
	@media screen and (max-device-width: 768px) and (orientation: portrait) {         
	/* 样式写在这 */            
	}     
	6.iPhone 和 Smartphones
	
	@media screen and (min-device-width: 320px) and (min-device-width: 480px) {              
	/* 样式写在这 */            
	}     
	

## 第十二章 用户界面与其它重要属性

### 自由缩放属性resize

为了增强用户体验，CSS3增加了很多新的属性，其中resize就是一个重要的属性，它允许用户通过拖动的方式来修改元素的尺寸来改变元素的大小。到目前为止，可以使用overflow属性的任何容器元素。

resize属性主要是用来改变元素尺寸大小的，其主要目的是增强用户体验。但使用方法却是极其的简单，先从其语法入手。

	resize: none | both | horizontal | vertical | inherit

- none
	- 用户不能拖动元素修改尺寸大小。
- both
	- 用户可以拖动元素，同时修改元素的宽度和高度
- horizontal
	- 用户可以拖动元素，仅可以修改元素的宽度，但不能修改元素的高度。
- vertical
	- 用户可以拖动元素，仅可以修改元素的高度，但不能修改元素的宽度。
- inherit
	- 继承父元素的resize属性值。

	例如：通过resize属性，让文本域可以沿水平方向拖大。代码为：
	
	textarea {
	  -webkit-resize: horizontal;
	  -moz-resize: horizontal;
	  -o-resize: horizontal;
	  -ms-resize: horizontal;
	  resize: horizontal;
	}

### CSS3外轮廓属性

外轮廓outline在页面中呈现的效果和边框border呈现的效果极其相似，但和元素边框border完全不同，外轮廓线不占用网页布局空间，不一定是矩形，外轮廓是属于一种动态样式，只有元素获取到焦点或者被激活时呈现。
outline属性早在CSS2中就出现了，主要是用来在元素周围绘制一条轮廓线，可以起到突出元素的作用。但是并未得到各主流浏览器的广泛支持，在CSS3中对outline作了一定的扩展，在以前的基础上增加新特性。outline属性的基本语法如下：

	outline: ［outline-color］ || [outline-style] || [outline-width] || [outline-offset] || inherit

从语法中可以看出outline和border边框属性的使用方法极其类似。outline-color相当于border-color、outline-style相当于border-style，而outline-width相当于border-width，只不过CSS3给outline属性增加了一个outline-offset属性，其取值说明如下

![][image-27]

### CSS生成内容
content配合CSS的伪类或者伪元素，一般可以做以下四件事情：

- none
	- 不生成任何内容
- attr
	- 插入标签属性值
- url
	- 使用指定的绝对或相对地址插入一个外部资源（图像，声频，视频或浏览器支持的其他任何资源）
- string
	- 插入字符串

	实例展示：
	
	在CSS中有一种清除浮动的方法叫“clearfix”。而这个“clearfix”方法就中就使用了“content”，只不过只是在这里插入了一个空格。如下所示：
	
	.clearfix:before,
	
	.clearfix:after {
	
	       content:””;
	
	       display:table;
	
	}
	
	.clearfix:after {
	
	       clear:both;
	
	       overflow:hidden;
	
	}
	

上面这个示例是最常见的，也是最简单的，我们再来看一个插入元素属性值的方法。

假设我们有一个元素：
\<a href="##" title="我是一个title属性值，我插在你的后面"\>我是元素\</a\>
可以通过”:after”和”content:attr(title)”将元素的”title”值插入到元素内容“我是元素”之后：

	a:after {
	
	  content:attr(title);
	
		   color:#f00;
	
	}
	

![][image-28]


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
[image-14]:	14.jpeg
[image-15]:	15.jpeg
[image-16]:	16.jpeg
[image-17]:	17.jpeg
[image-18]:	18.jpeg
[image-19]:	19.jpeg
[image-20]:	20.jpeg
[image-21]:	21.jpeg
[image-22]:	22.png
[image-23]:	22.png
[image-24]:	23.jpg
[image-25]:	24.jpg
[image-26]:	25.jpg
[image-27]:	26.png
[image-28]:	27.jpg