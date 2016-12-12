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

	<p><abbr title="Professor">Prof</abbr> David is a nice guy.</p>

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
可伸缩矢量图形（SVG）较新尚未普及

#### 透明度
要创建一个局部透明的图片，涉及以下两种个格式： 

- 透明GIF: 如果图片的透明部分有直边，并且这部分是完全透明，可以选用GIF保存
- 如果图片的透明部分含斜边、圆形，或者透明部分是半透明，或者投影，保存为PNG

_透明PNG格式不完全支持旧浏览器，例如IE6

### HTML5： 图形和图形说明
将图像和图像说明相关联
	<figure>
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