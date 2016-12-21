# JavaScript面向对象编程指南

#### JavaScript 数据类型
1. number
2. string 
3. boolean
4. undefined
5. null
6. object

#### type of 类型
1. number
2. string
3. boolean
4. undefined
5. object 
6. function

##### type of
	1. type of Infinity  //number
	2. 一个数字可以表示层1e1（或者1e+1、1E1、1E+1）这样的指数形式，意思是在数字1后面加1个0，也就是10。 2e+3的意思是在数字2后面加3个0，也就是2000.
	3. Infinity - Infinity //NaN
	4. var b = “  true ” ;
	     type of b; // “string”
	
	5.  >>> var b = “one”;
	      >>> ! b; //false
	
	字符串”one”是被转换成布尔值true
	
	6. NaN == NaN; //false
	7. type of NaN  // number
 
#### 优先级
	1. 以下特定值为false
	    空字符串“”
	    null
	    undefined
	    数字0
	    数字NaN
	    布尔值false
	2.  ! 优先级最高， &&的优先级高于||
	尽量使用括号
	
	3. 惰性求值
	如果在一个连续的逻辑操作中，操作结果在最后一个操作完成之前就已经明确了的话，那么该操作往往就不必再继续执行。因为这已经不会对最终结果产生任何影响。例如
	>>> true || false || true || false
	true
	
	如果在一个逻辑表达式中遇到一个非布尔类型的操作数，那么该操作数的值就会成为该表达式所返回的结果，例如
	>> true && “something”
	“something”
	
	>>true || “something ”
	true
	
	var mynumber = my number || 10;
	如果变量mynumber已经被定义了，就保留其原有值，否则就将它初始化为10. 但若是初始值为0，就不能这样定义了。


#### undefined 和 null
	1. type of undefined // undefined
	     type of null  // object
	
	2.  1 + undefined  //NaN
	     1 + null // 1
	3.   1 * undefined  //NaN
	     1 * null // 0
	4. “” + null // “null”
	    “” + undefined   // “undefined”

###### 检查变量是否存在时，更好的选择是使用type of  
    if (typeof somevar !== “undefined”) {result = “yes”;}
但这个也仅适用于被初始化的变量

##### 错难题:
1. var a; typeof a;
2. 10 %"0";
3. undefined == null
4. typeof “2e+2”
5. var a = b = 1; b为全局变量，区别于var a = 1,b = 1;

	function foo(){
		var a = b = 1;
	}
	foo();
	console.log(typeof a);
	console.log(typeof b);



答案： 

1. undefined 
2. NaN
3. true
4. string
5. "undefined"
	"number"
## 函数
#### 函数声明
	    function sum (a,b){
	        var c = a + b;
	        return c;
	}
	
	组成部分：
	        1. function子句
	        2. 函数名称,即这里的sum
	        3. 参数a,b
	        4. 函数块
	        5. return 子句


#### arguments （类似数组的对象）
	    返回函数所接收的所有参数
	    例子：完善sum()，使之能对任意数量的参数执行求和运算
	    function sumdif() {
	        var res = 0;
	          for (var i = 0; i <arguments.length; i++) {
	             res += arguments[i];
	              }
	          return res;
	        }
	    sumdif(1,1,2,2,3);
	
	    ❗️注意 是 i < … 不是 i <= …

#### 预定义函数
	    1. parseInt()
	        难题:
	            parseInt(’123’);//123
	            parseInt(‘abc’);//NaN
	            parseInt(‘abc123’);//NaN
	            parseInt(‘123abc’);//123
	            parseInt(‘123abc123’);//123
	
	        注意点：parseInt可以有第二参数，决定是十进制还是十六进制还是八进制等
	            0x开头固定为十六进制
	            0开头固定位八进制
	    2. parseFloat
	        基本同parseInt，但是只有一个参数，仅支持十进制，并且parseFloat可以接受指数parseFloat（’123e-2’）
	
	    3. isNaN
	
	    4. isFinite 检查一个既非infinity也非NaN的数字

#### URI的编码与反编码 ： 转义在URI或URL中有特殊含义的字符
	    1. encodeURI 返回一个可用的URL
	    2. encdoeURIComponent 认为传递的仅仅是URL的一部分 
	    反转函数 decodeURI decodeURIComponent

#### eval() 将其输入字符串当做JavaScript代码执行
	    尽量避免使用

#### alert() 由宿主环境提供——浏览器
	    会阻塞当前浏览器线程 

#### 全局变量 与局部变量
	    难题例子
	        var a =123;
	        function f() {
	            alert (a);
	            var a = 1;
	            alert (a);
	            }
	        f();
	
	    第一个alert //undefined 
	    因为函数域始终优先于全局域，所以局部变量a会覆盖掉所以的与它同名的全局变量。尽管在alert()第一次被调用时，a还没有被正式定义（即该值为undefined），但该变量本身已经存在于本地空间了

#### 函数也是数据类型
##### 函数标识记法（函数表达式）
###### 区别于函数声明，函数声明会被预先处理
	        var f = function() {return 1;}
	        typeof f //“function”
##### 匿名函数
	        function (a) { return a;}

##### 匿名回调函数
	function mutiplytwo (a,b,c,callback){
	    var res = [];
	    for(var i =0;i<3;i++){
	        res[i] = callback(arguments[i]*2);
	              }
	    return res;
	        }
	
	mutiplytwo(2,2,34,function(a){return a+2});
	❗️注意此处的callback，用于呼叫回调函数
	        以及回调函数需要return

##### 自调函数：
	        匿名函数的自行调用
	        (
	            function() {
	                alert(‘boo’);
	                    }
	        ) ()
	
	        即将匿名函数放入一对括号中，然后外面紧跟一对括号即可
	        第二对括号起立即调用的作用，同时它也是向匿名函数传递参数的地方
	
	        (
	            function(name) {
	                alert(‘Hello’ + name + ‘!’) ;
	                    }
	        ) (‘dude’)


##### 函数内部重写自己
	        function a() {
	            alert (‘A!’);
	            a = function (){
	                alert (‘B!’);
	                        }
	                    }
	
	        这样我们第一次调用该函数时，
	            1. alert(‘A’) 将会被执行
	            2. 全局变量 a 将会被重新定义，并被赋予新的函数
	        如果该函数再次被调用的话，被执行的就是alert(‘B’)了
	
	        var a = function (){
	             function somesetup(){
	                  var setup = 'done';
	                                        }
	              function actualWork(){
	                      alert('worky-worky');
	                                      }
	              somesetup();
	              return actualWork;
	               } ();
	
	        注意初次被载入以及再次调用 。注意return后面actualWork没有()

#### 作用域
	    有函数作用域，即函数内定义的变量，函数外是不可见的
	    但在代码块中定义的（例如某个if或for语句中,它在代码块外是可见的
	
	    难题例子：
	    function f1( ) { var a  = 1; f2 ( ); }
	    function f2 ( ) { return a; }
	    f1();
	    // a is not defined; 
	
	    f2被定义时，a是不可见的。
	    即使f2还没有被定义，我们也可以知道f1()的定义中对f2()的调用，对f1而言，在其所知的作用域中的任何东西都是可用的

#### 难题：
	    1. parseInt (1e1) 
	    2. parseInt (‘1e1’)   
	    3.  parseFloat(’1e1’)


#### 答案：
	    1. 10
	    2. 1  //当做字符串 只提取第一个数
	    3. 10


## 第四章 对象
### 4.1
#### 对象的组成 （和数组类似）
	    🌰 var hero ={
	        breed: ‘Turtle’,
	        occupation: ‘Ninja’
	                };
	
	        1. 变量名 hero   
	        2. 和[ ]不同，对象使用{ }
	        3. 逗号分割元素
	        4. key/value之间用冒号分割
	        5. 有的时候可以在key上加引号，但是不建议。但特殊时候必须加：保留字/含空格等/以数字开头

#### 两种方法访问对象属性
	1. 中括号 hero[‘occupation’]
	2. 点号表示法 hero.occupation

#### 构造器函数
	    var hero  = new Hero();
	
	     难题例子
	    function Hero(name){
	        this.name  = name;
	        this.whoAreYou = function() {
	                    return “” I’m “” + this.name;
	                                }
	                    }
	    >>> var h1 = new Hero( ‘Dona’  );
	    >>> h1.whoAreYou(); // “ I’m Dona ”
	    但是！  如何没有new
	    >>> var h = Hero ( ’Tom ’);
	    >>> type of h //“undefined”
	    因为没有使用new，所以不是在创建一个新的对象，而是函数调用，所以这里的this是全局对象

#### 构造器属性
	    >>> var o = { }; 
	    >>> o.constructor; // Object ()
	    >>> typeof o.constructor; //“function”


#### instanceof操作符
	    测试一个对象是不是右某个指定的构造器函数所创建的
	        🌰 
	            >>> function Hero ( ) { }
	            >>> var h = new Hero ( );
	            >>> var o = { }; 
	            >>> h instanceof Hero; //true
	            >>> h instanceof Object; //true
	            >>> o instanceof Object; //true
	        注意❗️ 不是 h instance Hero() 因为不是函数调用


#### 传递对象 ：
 ❗️❗️ 当我们拷贝某个对象或者将它传递给某个函数时，传递的都是该对象的引用。所以我们在引用上的任何改动，都会影响原对象


#### 对象比较：
 只有两个引用指向同一个对象时，=== 为true，其他都为false，即使他们拥有相同的属性和方法


### 4.2
#### 4.2.1 Object
	        1. 创建对象：
	            var o  = { }
	            var o = new Object( )
	        2. 无论多么复杂的对象，都是继承自object，并拥有它所有的方法

#### 4.2.2  Array
##### join()

	var arr = [1,2,3]
	arr.join()//"1,2,3"
	arr.join("_")//"1_2_3"
##### slice() 提取字符串的某个部分
arr.slice([从这开始]，(到这结束))
arr.slice([从这开始]）

	var arr=[1,2,3,4,5]
	arr.slice(1,3);//[2,3]
	arr.slice(1);//[2,3,4,5]
 

##### splice()   插入,删除或者替换数组的元素

	var arr = [1,2,3,4,5]
	arr.splice(2)//return [3,4,5]
	arr[1,2]//原来的arr被修改
	
	arrayObject.splice(index,howmany,item1,.....,itemX) 

#### 4.2.3 Function
	        1.
	        >>>function myfunc(a) {return a;}
	        >>> myfunc.constructor //Function ()
	
	        2. Function对象也有length属性  记录的是这个function的参数数量

##### 4.2.3.2  Function对象的方法

	            call () 和apply () 通过这个两个方法，能让对象去借用其他对象的方法为己用。

![][image-1]
![][image-2]
  
	    这种情况我们可以调用say()
	
	    >>> some_obj.say.call (my_obj, ‘ Dude’);
	    “Heya Dude, I am a Scripting guru”
	
	    如果我们没有将对象传递给call的首参数，或者传递给它的是null,调用对象会被默认为全局对象
	
	    apply() 不同的就是参数的传递形式，这里目标函数所需要的参数都是通过一个数组来传递的
	
	    下面两行代码都是等效的
  
￼![][image-3]

##### 4.2.3.3  arguments对象
	        1. arguments.callee  则该函数在被调用时就会被返回自身的应用
	            🌰 例子
	                >>> function f() { return arguments.callee;}
	                >>> f()  // f ()
	
	        2. 用arguments.callee  实现匿名函数的递归调用
	            🌰 例子
	                （
	                    function (count ){
	                        if(count <5){
	                            alert(count) ;
	                            arguments.callee(++count);
	                                    }
	                                }
	                    ）(1)


#### 4.2.4 Boolean
	        >>> var b = new Boolean();  
	        注意b是一个对象，不是一个基本的布尔值
	        如果要获得这样的基本类型值，用valueOf方法（继承自Object对象）
	        >>> var n = new Boolean ();
	        >>> typeof b //“object”
	        >>> typeof b.valueOf() //“boolean”
	        >>> b.valueOf() //false
	
	        >>>Boolean ( { } ) //true
	
	        >>>var b1 = new Boolean(true)
	        >>>b1.valueOf() //true
	
	        >>>var b2 = new Boolean(false)
	        >>>b2.valueOf() //false
	
	        >>> Boolean (b1) //true
	        >>> Boolean (b2) //true

#### 4.2.6 String
	        >>> var s = new String (“ Potato”);
	
	        >>> s.toUpperCase() //“POTATO”
	        >>> s.toLowerCase() //“potato”
	        >>> s.charAt (0); // “P”
	        >>> s.indexOf(‘o’); //1  第一个遇到的
	        >>> s.indexOf(“o”, 2) //从index2开始
	        >>> s.lastIndexOf(‘o’)
	        >>>s.indexOf(‘Po’)  //0 如果找不到-1
	
	        区别 substring 和 slice  对第二个数是负数的处理
	            1. substring会视为从0开始计数   //substring (!,0)
	            2. slice会将它与字符串的长度相加 //slice(1,s.length-1)
	
	        split  可视为join的反操作，后者将一个数组合并成一个字符串
	        >>> s.split(“ “) //[‘couch’, ‘potato’]
	
	        concat用于追加字符串
	        >>>s.concat(“es”) //“potatoes”
	
	        所有这些都是新字符串，不会改变原字符串

#### 4.2.7 Math
	        Math.random() 返回的是0-1之间的某个数
	        100 * Math.random() 返回 0-100之间的某个数
	
	        想获得某个max和min之间的值， 公式 (（max - min ）* Math.random()  ) + min
	
	        Math.floor
	        Math.ceil
	        Math.round


#### 4.2.8 Date
	        var udate = new Date(2012,10,1);

￼

	🌰 2012年5月20日是星期几
	    >>> var d = new Date(2012,5,20);
	    >>> d.getDay(); //
	    ❗️因为0是是从星期日开始计数的，所以3是星期三


#### 4.2.9. RegExp

##### 创建RegExp对象:
	        1. var re  = new RegExp  (“j.*t”);
	        2. var re = /j.*t/;

##### 4.2.9.1 RegExp对象的属性
	        1. global   ///g 找出所有匹配的位置
	        2. ignoreCase   /// i
	        3.multiline    /// m
	        4. lastIndex
	        5. source
	
	        >>> var re = new RegExp(“j.*t”,”gim”);
	        >>> var re = /“j.*t”/gim;


##### 4.2.9.2 RegExp对象的方法
	        两种查找匹配内容的方法 
	        test() 返回boolean
	        exec() 匹配字符串组成的数组
	        参数都是一个字符串
	
	        >>>/j.*t/.test(“Javascript”)  //false
	        >>>/j.*t/i.test(“Javascript”)  //true
	
	        >>>/j.*t/i.exec(“Javascript”) [0] //“Javascript”

##### 4.2.9.3 正则表达式  作为string的参数

	        方法：
	            1. match() 返回匹配内容的数组
	            2. search() 返回第一个匹配内容所在的位置
	            3. replace()  将匹配文本替换成指定的字符串
	            4. split() 根据正则表达式将目标字符串分割成若干个数组元素
	
	
	            >>> var s = new String (“HelloJavascriptWorld”);
	            >>> s.match(/a/); [“a”]
	            >>> s.match(/a/g); [“a” , “a”]
	
	            🌰 用户数email地址，用JavaScript将email的前半部分提炼出来，作为后面用户名的建议
	            >>> var email = “xysy0506@163.com”
	            >>> var username = email.replace(/(.*)@(.*)/,”$1”) ;
	            >>> username ; // xysy0506 
	
	            $1 代表第一个括号里的

##### 4.2.9.6 回调式替换
	            var glob;
	            var callback = function(){
	                        glob = arguments;
	                        return arguments[1];
	                               }
	
	            var re = /(.*)@(.*)\.(.*)/;
	
	            var email = "xysy0506@163.com";
	
	            email.replace(re,callback);  //xysy0506
	
	            >>>glob;
	
	            ["xysy0506@163.com", "xysy0506", "163", "com", 0, "xysy0506@163.com"]
	
	
	            首参数是正则表达式匹配的内容
	            尾参数是被搜索的字符串
	            尾参数之前的参数是匹配内容所在的位置
	            剩下的参数是regex模式分组的所有匹配字符串组

#### 4.2.10 Error对象
 
	        try{
	            iDontExist();
	            }catch (e){
	                //do nothing 发生异常才执行
	                }finally{
	                    // do nothing 无论发不发生异常都执行
	                    }
	
	        Error对象的两个基础属性
	            e.name
	            e.message

🌰
![][image-4]
![][image-5]  
￼![][image-6]

￼
#### 易误解
try{
 
	try{
	    throw new Error("oops");
	}
	finally{
	    console.log{"finally"};
	}
}
catch(e){
	console.error("oops",e.message);
}
￼
##### 框中的这层因为没有catch所以会跳到外层的catch来处理，但需要先执行finally
执行后：finally
	    outer
	    oops

#### 难题：




￼![][image-7]

![][image-8]

![][image-9]

￼

##### 答案：
	1.Here, this === window because C() was called without new. Also, o === window because new F() returns the object returned by C(), which is this, and this is window. 
	
	2. object  因为constructor create的都是object 不是boolean
	
	3.> var c = [1, 2, [1, 2]]; > c.sort(); > c; [1, Array[1,2], 2]
	
	This is because sort() compares strings. [1, 2].toString() is "1,2", so it comes after "1" and before "2". The same thing with join():
	> c.join('--'); > c; "1--1,2--2"


### 第五章 原型 prototype
#### 5.1 原型属性
在函数被创建的时候，属性中就包括了prototype属性，初始值为一个空的对象。

	>>>typeof foo.prototype //"object"
 
赋予这个空对象的一些属性和方法，并不会对foo函数本身造成什么影响，但不能对用作构造器

##### 步骤
	1. 建个function
	function Gadget(name,color){
	this.name = name;
	this.color = color;
	}
	
	2. prototype添加东西
	Gadget.prototype = {
	    prcie:100,
	    rating: 3
	};
	
	3.使用原型的方法和属性
	>>>var newtoy = new Gadget('webcam','black');
	>>>newtoy.name;//"webcame"
	>>>newtoy.price // "100"
 
###### 最重要的是live概念，因为在JavaScript中，对象都是通过引用的方式传递的，所以我们随时可以修改原型，并且与之相关的对象也会继承这个改变

	也就是说，根据上面的例子，我们再给Gadget增加一个方法
	Gadget.prototype.get= function (what){
	    return this[what];  
	        };
	>>>newtoy.get("price");//100
	
	即newtoy在get方法前已经创立，还是可以使用新添加的get，就是因为是对象live的


#### 5.1.4
如果遇上对象的自身属性与原型属性同名的话：对象自身属性的优先级高于原型属性

##### hasOwnProperty()

	>>>newtoy.hasOwnProperty('name');//true
	>>>newtoy.hasOwnproperty('price');//fasle
 
#### 5.15 isPrototypeOf()
当前对象是否是另一个对象的原型

	例子：
	1. 定义一个简单对象monkey
	var monkey = {
	hair : true;
	};
	
	2. 创建一个Human()的构造器函数，并将其原型属性设置为指向monkey
	function Human(name){
	    this.name = name;
	}
	Human.prototype = monkey;
	
	3. 新建一个George的Human对象
	>>> var george = new Human('George');
	>>> monkey.isPrototypeOf(george)//true

#### 5.16 仅在Firefox存在的\_proto\_
并不等于prototype，是某个实体的对象的属性
而prototype的属性是属于构造函数的属性
\_proto\_只能在学习或者调试的环境下使用

### 5.2 扩展内建对象
内建对象的构造函数（例如Array,String,Object和Function）都是可以通过其原型进行扩展的

#### 5.2.2 一些原型陷阱
处理原型问题时，注意以下两种行为：

- 将原型对象执行完全替换的时候，可能会触发原型链中的某种异常（exception）
- prototype.constructor属性是不可靠的

即我们将prototype替换，但\_proto\_这个属性，能使对象仍然使用原来的prototype里的东西

###### 当我们重写某个对象的prototype时，重置相应的constructor属性是一个好习惯

### 5.4 练习题

1.Create an object called shape that has a type property and a getType() method:
 

	var shape = {
	type : "",
	getType  = function (){
	return this.type
	};

## 第六章 继承

### 6.1原型链
通过原型来实现继承关系链
#### 6.1.1原型链例子
	function Shape(){
	    this.name = 'shape';
	    this.toString = function(){return this.name;}
	}
	
	function TwoDShape(){
	    this.name = '2D shape';
	}
	
	fucntion Triangle(side,height){
	    this.name = 'Triangele';
	    this.side = side;
	    this.height = height;
	    this.getArea = function(){return this.side * this.height / 2;}
	}
	
	TwoDShape.prototype = new Shape();
	Triangle.prototype = new TwoDShape();
	
	//我们将对象的prototype属性重写时，需要重置对constructor属性
	TwoDShape.prototype.constructor = TwoDShape;
	Triangle.prototype.constructor = Triangle;
 
 
#### 6.1.2 将共享属性迁移到原型中去
###### 强调！必须在扩展原型对象之前完成继承关系的构建
![][image-10]
![][image-11]

### 6.2 new F()
不懂，待补


### 6.3 uber ——子对象访问父对象的方式

不懂，待补


# 第六章需要重新阅读


## 第七章 浏览器环境
### 7.2 BOM与DOM
页面的JavaScript代码有一系列可以访问的对象，可以分为两组：

- 当前载入页面所拥有的对象（文档） DOM
- 页面外事物所拥有的对象（浏览器窗口和桌面屏幕）BOM

### 7.3 BOM
可以通过全局对象window和window.screen来访问这些BOM对象

#### 7.3.1 window对象
环境中所以的全局变量都是window的属性，JavaScript核心函数也都是window对象的方法，window对象还有一个作用，提供各种关于浏览器环境的私有数据，例如window对象中各种frame、iframe等等

#### 7.3.2 window.navigator
navigator是一个用于反映浏览器本身及其功能信息的对象。
navigator.userAgent是一个用于浏览器识别的长字符串，但我们不要依赖这种用户带你字符串，因为很难追踪到所有版本，而且用户可以对该字符串进行修改，伪装成其他浏览器
  
用特性监听法比较好，也就是直接检验浏览器是否有该功能

#### 7.3.3 firebug的备忘功能
在控制台输入navigator，就可以得到一份完整的属性列表，以及这些属性的当前值

#### 7.3.4 window.location
location属性是一个用于存储当前载入页面URL信息的对象。  

- location.href显示的是完整的URL
- location.hostname显示相关的域名

循环列出location对象的完整属性列表

	for(var i in location) {console.log(i + ' = "' + location[i] + '"')} 
	
	href
	hash
	host
	hostname
	pathname
	port
	protocol
	search

location对象还提供三个方法，分别是reload()、assign()和replace()  
location.replace方法与assign基本相同，只不过它不会再浏览器的历史记录表中留下记录

#### 7.3.5 window.history
window.history属性允许我们在同一个浏览器会话中存储有限数量的访问记录。
 
	>>>window.history.length //5
	>>>window.history\[0\] //不被允许
但我们可以用history.forward()  
history.back() 进行浏览器的后退和前进  
或则还可以  
    history.go(-1) ;//history.back()
	history.go(0);//重置当前页面
	history.go(1);//history.forward();

#### 7.3.6 window.frames
window.frames属性是当前页面中所以frame元素的集合。这里没有对frame和iframe做出区分。无论当前页面中是否存在frame元素，window.frames属性总是存在的，并指向了window本身  

每一个frame元素都包含一个别的页面，这些页面也有自己的全局window对象。 

	<iframe name="myframe" src="about:blank" />
访问iframe元素的window对象：
 
	>>>window.frames[0]
	>>>window.frames[0].window
	>>>frames[0].window
	>>>frames[0]

我们也可以通过子元素来访问父级页面：  
 
	>>>frame[0].parent === window; //true

通过一个**top**的属性，可以访问到当前最顶层页面（即包含所有其他frame元素的页面）中的任何frame元素
 
	>>>window.frame[0].window.top === window //true

**self**属性，作用基本等于window
 
	>>>self === window //true

如果frame元素拥有name属性，可以通过名字来访问
 
	>>>window.frames['myframe'] === window.frames[0] // true

#### 7.3.7 window.screen
提供浏览器以外的桌面信息  
可以查看当前屏幕的实际状态（如分辨率） 
 
	>>>screen.width //1440
	>>>screen.availWidth //1440
	>>>screen.height//900
	>>>screen.availHeight //847

height指总分辨率，availHeight指出去操作系统菜单（例如windows的任务栏）以外的子区域

#### 7.3.8 window.open()/close()
##### window.open()打开新窗口

- 新窗口的URL
- 新窗口的名字，同于form标签
- 还有一个逗号分割的功能性列表，例如：
	- 尺寸的可调整性
	- 弹出窗的长与宽
	- 状态栏—设置状态栏的可见性
window.open()会返回一个新建浏览器实例的window对象
 

	var win  = window.open('http://www.baidu.com','baidu','width=300,height=300,resizable=yes');

**注意添加http://，没有的话是在当前页面下的子页面/baidu.com**
通过检查win是否为falsy值来判断弹出窗是否被屏蔽了

#### 7.3.9 window.moveTo()/resizeTo()
	window.moveTo(100,100) 将当前浏览器窗口移动到屏幕坐标x=100,y=100的位置（指的是窗口左上角的坐标）
	window.moveBy(10,10) 将窗口的当前位置右移10个单位，并同时下移10个单位
	    resizeTo(x,y)和rezieBy类似，不过是调整窗口的大小
	❗️并不建议使用这些方法来解决问题

#### 7.3.10
##### window.alert()
##### window.prompt()
提供一定的文本输入功能

	>>> var answer = prompt('What's your name?');
	        console.log(answer); //input

- 按cancel或者X以及ESC退出，会返回null
- 没有输任何东西就单击OK或者回车，会返回”” 空字符串
- 还可以接受第二个字符串参数，主要用做输入框的默认值
##### window.confirm()
	为用户提供两个选项——ok与cancel   
	
	
	var answer = confirm('Are you cool?');
	
	
	        console.log(answer); //true or false

#### 7.3.11
##### window.setTimeout() 指定毫秒数后执行某段既定代码
 
	>>>function boo() {alert('Boo!';)}
	>>> var id = setTimeout(boo,2000);  //返回该函数的超时ID
	>>>clearTimeout(id); //取消当前的超时

##### window.setInterval() 每隔一段毫秒数重新执行这段代码
 
	>>>function boo() {console.log('Boo!';)}
	>>> var id = setInterval(boo,2000);  //返回该函数的超时ID
	>>>clearInterval(id); //取消当前的超时

#### 7.3.12 window.document
bom对象，但是方法和属性也属于DOM对象所涵盖的范围

### 7.4 DOM
#### 7.4.2.1文档节点
所以节点都有自己的nodeType, nodeName, nodeValue等属性  
在DOM中有12种节点，每种类型（nodeType）用一个数字表示，最常用的是：  

1. 元素（1）
2. 属性（2）
3. 文本（3）

#### 7.4.2.3子节点
是否存在子节点，用该节点的`hasChildNodes()`方法  
可以通过`ChildNodes`**数组集合**来访问它们  
难题：
这里body元素有几个子节点？？  

	<body>
	        <p>first paragrah</p>
	        <p><em>second</em>paragraph</p>
	        <p>final</p>
	        <!-- and that's about it -->
	</body>

答案：9个！ 3个段落加上1个注释是4个节点，这4个节点之间的空白处至少有3个文本节点，这样就有7个节点，另外body与第一个p节点之间有一个空白处，第八个节点，comment元素和\</body\>元素也有一个空白处，那又是一个文本节点，一共9个文本节点

#### 7.4.2.4 属性
通过元素的`hasAttributes()`方法来检查该元素中是否存在属性  
可以通过索引值，或属性名来访问一个属性。  
`>>>bd.childNodes[1].attributes[0].nodeName //"class"`  
`>>> bd.childNodes[1].attributes['class'] `  
也可以调用`getAttribute()`方法来获取相关的属性值  

#### 7.4.2.5 访问标签中的内容
1. 可以通过该元素的`textContent`属性来获取段落中的文本内容（IE不适用）
2. 通过`innerHTML`属性（主流浏览器支持），不属于标准DOM
区别：  
![][image-12]

#### 7.4.2.6 DOM访问的快捷方法

-  getElementsByTagName()
- getElementsByName()
- getElementById()

如果要访问元素的属性，有多种解决办法：

	>>>document.getElementsByTagName('div')[1].getAttribute('id')
	"logo"
	>>>document.getElementsByTagName('div')[1].id
	"logo"

但这种方法对`class`属性不管用，因为”class”这个词在ECMAScript设置成保留字，需要改用className

	>>>document.getElementsByTagName('div')[1].className
	"opener"

#### 7.4.2.7 兄弟节点、body元素、及首尾子节点

- nextSibling
- previousSibling
- firstChild  等价于 childNodes[0]
- lastChild  等价于 childNodes[childNodes.length-1]

#### 7.4.3 DOM节点的修改

- 修改样式： style属性
	`>>>my.style.border ="1px solid red";`
	但CSS属性中的短线（即-）在JavaScript中是不可用的，处理办法是直接跳过-并将下一个单词的首字母大写
	`>>>my.style.fontWeight = 'bold'`

- 表单  
	`var inputs = document.getElementsByTagName('input'); `
	`>>>inputs[1].name;` 
	`>>>inputs[1].value = 'my query';` 
	`>>>inputs[3].value = inputs[3].value.replace(/Lu/,'Tri') ;`


		var inputs = document.getElementsByTagName('input');
		inputs[8].value = inputs[8].value.replace(/百度/, 'google');
		function test() {
		  var st = inputs[8].style;
		  st.visibility = (st.visibility == 'hidden') ? 'visible' : 'hidden';
		}
		
		var myint = setInterval(test,1000);

#### 7.4.4 新建节点
- 通常用`createElement()`和`createTextNode()`这两个办法来创建新节点
- `appendChild()`将新节点添加到DOM树里

```
    >>>var myp = document.createElement('p');
    >>>myp.innerHTML="yet another";
    >>>document.body.appendChild(myp);
```
- `cloneNode()`拷贝现有节点也是创建节点的一种方式：
	包含一个布尔类型的参数：
	- true=深拷贝，包括所有子节点
	- false=浅拷贝，不包括子节点，只针对当前节点
```
    <p><em>second</em>paragraph</p>
    >>>var el = document.getElementsByTagName('p')[1];
    >>>document.body.appendChild(el.cloneNode(false))//浅拷贝了p这个元素
    相当于：
    >>>document.body.appendChild(document.createElement('p'));
    可以只拷贝EM元素:
    >>>document.body.appendChild(el.firstChild.cloneNode(false)); //书中此部分错了
    只拷贝内容为second
    >>>document.body.appendChild(el.firstChild.firstChild.cloneNode(false));
```
- `insertBefore(newItem,existingItem)`指定新节点插入哪个元素的前面
- `removeChild(item)`移除节点  
	`>>>var myp = document.getElementByTagName('p')[1];`  
	`>>>var removed= document.body.removeChild(myp);`//可以保存该方法返回值，后面可以继续使用
- `replaceChild(newitem,olditem)`移除一个节点的同时，将另一个节点放在该位置


#### 7.4.6只适用于HTML的DOM对象
#### 7.4.6.1访问文档的基本方法
- `document.images`所以`image`的合集
- `document.links`
	- 是一个列表，包含了页面中所有的含有`href`属性的a标签
- `document.anchors`
	- 包含所以带`name`属性的链接
- `document.forms`
	- `document.forms.elements`获得一系列的`input`字段和按钮
	- `document.forms.elements[0].disable = true`获得这个对象的attributes属性 、
	- 如果有name属性的话，也可以通过名字访问
		`>>>document.forms[0].elements['search'];`//array notation
		`>>>document.forms[0].elements.search;`//object property

#### 7.4.6.2 document.write() 很少用
`document.write()`方法，在当前页面在载入时插入一些HTML元素  
`<p>It is now <script>document.write("<em>"+new Date() +"</em>");</script></p>`

`document.writeln`末尾自动加入换行符

#### 7.4.6.3 Cookie、Title、Referrer、Domain
- `document.cookie`实际上是一个字符串，其中存储了用于往返服务器端与客户端之间的cookie信息。每当服务器向浏览器发送页面时，HTTP头信息中往往包含一些用于设置cookie的内容。以便于在客户端再向服务器发送请求时返回带有该头信息的cookie
- `document.title`是被用来修改页面在浏览器串口中所显示的标题的。并没有修改\<title\>标签本身的值，只改变了其在浏览器窗口显示内容。所以，该集合并不等价于`document.getElementsByTagName(’title’)[0]`
- `document.referrer`记录我们之前所访问过的页面URL，与浏览器请求页面时所发送的HTTP头信息中的Referer值是相同【注意拼写不同】
- `document.domain`可以对当前所载入页面的域名进行访问，对于跨域调用非常有效

`>>>window.location === document.location` //true

### 7.5 事件
#### 7.5.1 内联HTML属性法
通过标签的特定属性来添加事件  
`<div onclick="alert('Ouch!')">click</div>`

#### 7.5.2 元素属性法

	<div id="mytest">click me</div>
	  <script type="text/javascript">
	    var mytest = document.getElementById("mytest")
	    mytest.onclick = function(){
	        alert("ouch!");
	        alert("ouch again!");
	  }
	  </script>

#### 7.5.3 DOM事件监听器
`addEventListener()`给单击事件赋予相关的监听器
- 首参数是一个事件类型的参数
-  第二个是函数指针，可以是匿名函数，也可以现存函数
- 第三个参数：false (7.5.4)

	<div id="mytest">click me</div>
	  <script type="text/javascript">







	    var mytest = document.getElementById("mytest")







	    function ouch(){







	        alert("ouch!");







	        alert("ouch again!");







	  }















	    mytest.addEventListener('click',ouch);







	  </script>

#### 7.5.4 捕捉法和冒泡法
事件传播链：  

- 捕捉法
	- 首先发生在document,然后依次往下传递给body, 等等
- 冒泡法
	- 首先发生在链接上，然后逐层向上冒泡，直至document对象

DOM Level2建议：  
事件传播分为三个阶段：在标签上使用捕捉法，然后使用冒泡法  
也就是从document到相关链接或者标签，然后回到document
`eventPhase`属性可以告诉某一事件当前所处的阶段

Firefox、Opera、Safari基本完整实现了上述三个阶段，只有IE还依然坚持只使用冒泡法

因素影响事件的传播：  
- 通过`addEventListener()`的第三个参数，决定是否采用捕捉法来处理事件，然而为了让代码适用于更多的浏览器，最好始终设置为`false`，即只使用冒泡法来处理事件
- 在监听器函数中阻断事件的传播，使其停止冒泡。使用`stopPropagation()`方法
- 事件委托。假如一个`<div>`中有10个按钮，每个按钮需要一个监听器，但更聪明的方法是为整个\<div\>设置一个监听器

在IE中使用事件捕捉的方法：  只适用于处理鼠标类事件，对于其他类型的事件例如键盘类不起作用
- setCapture()
- releaseCapture()

#### 7.5.5 阻断传播
使用`stopPropagration()`  

`addEventListener()`的对立面是`removeEventListener()`，但需要的注意的是无法移除匿名函数所定义的监听器，因为匿名函数是彼此独立的，即便函数体完全相同。

 事实上`stopPropagation`和`cancelBubble`的作用是一样的，都是用来阻止浏览器默认的事件冒泡行为。
不同之处在于`stoppropagation`属于W3C标准，试用于Firefox等浏览器，但是不支持IE浏览器。相反`cancelBubble`不符合W3C标准，而且只支持IE浏览器。所以很多时候，我们都要结合起来用。不过，`cancelBubble`在新版本chrome,opera浏览器中已经支持。


#### 7.5.6 防止默认行为
使用`preventDefault()`

 
	<a href="http://www.baidu.com">baidu</a>
	<a href="http://www.baidu.com">baidu</a>
	<a href="http://www.baidu.com">baidu</a>
	<a href="http://www.baidu.com">baidu</a>
	<a href="http://www.baidu.com">baidu</a>
	<a href="http://www.baidu.com">baidu</a>
	
	<script type="text/javascript">
	var links = document.getElementsByTagName('a');
	for (var i = 0;i<links.length;i++){
	    links[i].addEventListener('click',
	        function(e){
	            if(!confirm("Are you sure you want to follow this link?")){
	                e.preventDefault();
	            }
	
	    },false);
	}
	
	</script>

#### 7.5.7 跨浏览器事件监听器
IE的不同之处：
- IE没有`addEventListener()`,IE5开始提供了`attachEvent()`
- 对于单击事件来说，使用`attachEvent()`等同于使用`onclick`属性
- 只使用冒泡法
- 没有`stopPeopagration`方法，使用`cancelBuble()`设置为true
- 没有`preventDefault()`方法，使用`returnValue`设置为false
- 没有`removeEventListener(）`使用`detachEvent()`
- 没有`target`属性，使用`srcElement`

![][image-13]
![][image-14] 

#### 7.5.8 事件类型
![][image-15]

### 7.6 XMLHttpRequest 对象
XMLHttpRequest()是一个用来构建HTTP请求的JavaScript对象（构造器）  
正式使用是IE7，逐渐被其他浏览器所接受，形成一种通用的跨浏览器实现，也就是AJAX。 无需刷新整个页面来更新内容。

AJAX就是JavaScript和XML之间所建立的一种异步联系
- 异步，因为代码在发送HTTP请求之后，不需要停下来等待服务器相应，可以继续执行其他任务，待相关信息到达时自然会收到通知（通常以事件的形式出现）
- JavaScript——XHR对象就是用JavaScript来创建的

关于XMLHttpRequest对象的用法，主要分为两个有效步骤：
- 发送请求——这个步骤中，需要完成XMLHttpRequest对象的构建，并为其设置事件监听器
- 处理相应——这个步骤中，事件监听器会在服务器的响应信息到达时发出通知，然后代码就会忙于从中提取有用的信息

#### 7.6.1 发送请求
1. 创建对象`var xhr = new XMLHttpRequest();`
2. 为该对象设置一个能触发readystatechange事件的事件监听
	-  `xhr.onreadystatechange = myCallback;`
3. 调用其`open()`方法 `xhr.open('GET', 'somefile.txt', true);`
	- 第一个参数是HTTP请求的类型(包括GET、POST、HEAD等)
	- 第二个参数是所请求目标的URL
	- 第三个参数的布尔值，决定请求是否按照异步的方式进行(是就为`true`，否为`false`)
4. 发送请求`xhr.send(' ');`
	- `send()`在发送请求时附带上任何数据。
	- GET类请求，这里所发送的是一个空字符串，因为该数据将被包含在URL中
	- POST类请求，这就成了被包含在表单数据`key=value&key2=value2`中的一个查询字符
5. 请求被发送出去后，代码和用户就可以将注意力转向其他任务。待它收到服务器响应时，会自动启动回调函数`myCallbck`

#### 7.6.2 处理相应
已经为`readystatechange`事件设置了监听器  
每个XHR对象中都有一个叫做`readystate`的属性，一旦改变这个值，就会触发`readystatechange`事件。  
`readystate`属性的状态值如下:
- 0——未初始化状态
- 1——载入请求状态
- 2——载入完成状态
- 3——请求交互状态
- 4——请求完成状态

当`readyState`的值为4时，意味着服务器端的响应信息已经返回，可以开始处理了。
在`myCallback`函数中，除了确定`readyState`的值为4，还必须检查一下HTTP请求的状态码。因为如果目标URL实际上并不存在，就会收到一个值为404的状态码（表示未找到文件），正常的情况下`xhr.status`的值为200。

确定了`xhr.readyState`的值为4，并且`xhr.status`的值为200，就可以通过`xhr.responseText`来访问目标URL中内容了。


	function myCallback(){
	    if (xhr.readyState < 4){
	        return; //not ready yet
	    }
	    if (xhr.status !== 200){
	            alert ('Error!!');//the HTTP status code is not OK
	            return;
	    }
	    //all is fine, do the work
	    alert(xhr.responseText);
	}

#### 7.6.3  在早于7的IE版本中创建XMLHttpRequest对象
在早于7的IE版本中，XMLHttpRequest对象是以ActiveX对象的形式存在的，因此创建XHR方式会有些小小的不同  
具体如下:  
`var xhr = new ActiveXObject('MSXML2.XMLHTTP.3.0');`  
`MSXML2.XMLHTTP.3.0' `是要创建对象的标识符，并且还有几个不同版本

	var ids=['MSXML2.XMLHTTP.3.0',
	              'MSXML2.XMLHTTP',
	            'Microsoft.XMLHTTP];
	var xhr;
	if(typeof window.XMLHttpRequest === 'function'){
	    xhr = new XMLHttpRequest();
	}else{
	    for (var i = 0; i < ids.length;i++){
	        try{
	            xhr = new ActiveXObject (ids[i]);
	            break;
	        }catch(e){}
	    }
	}

ids包含了ActiveX对象的ID列表，先测试一下是否支持XMLHttpRequest对象，如果不是，则通过历遍ids中的可能项来尝试着创建着对象  
`catch(e)`可以捕获其中创建失败的项目并使循环继续

#### 7.6.4 A代表异步
异步发送了两个请求

	var xhr = new XMLHttpRequest();
	xhr.onreadystatechange = (function (myxhr){
	        return function(){myCallback(myxhr);}//闭包
	})(xhr);//(回调函数)
	xhr.open('GET','somefile.txt',true);
	xhr.send('');

在这种情况下，myCallback将会以参数的形式接收相关的XHR对象，避免了全局空间的问题。也意味着当该请求再次获得响应信息时，原来的xhr变量就可以被第二次请求重置甚至销毁了。因为我们在闭包内保留了该对象的原有信息

#### 7.6.5 X代表XML
XHR对象除了`responseText`属性外，还有`responseXML`的属性。  
如果向一个XML文档发送一个HTTP请求，该属性就会指向该XML的DOM document对象。这样就可以对它调用例如`getElementById()`等方法

#### 7.6.6 实例

	静态主页：
	<body>
	<div id="text">Text will be here</div>
	<div id="html">HTML will be here</div>
	<div id="xml">XML will be here</div>
	</body>
	
	三个文件所载入的分别是：
	- content.txt ——一段简单的文本，内容为"I am a text file"
	- content,html—— 一段HTML代码，具体如下:
	I am <strong>formatted</strong><em>HTML</em>
	- content.xml——一个XML文档，内容如下：
	<root>
	    I'm XML data.
	</root>
	
	在控制台中输入相关代码，向三个文件发送请求，并将它们各自的内容载入相关的<div>中
	function request(url,callback){
	    var xhr = new XMLHttpRequest();
	    xhr.onreadystatechange = (function(myxhr){
	        return function(){
	        callback(myxhr);
	}
	})(xhr);
	xhr.open('GET',url,true);
	xhr.send('');
	}
	
	request(
	    'http://www.phpied.com/files/jsoop/content.txt',
	    function(o){
	        document.getElementById('text').innerHTML = o.responseText;
	}
	);
	
	request(
	    'http://www.phpied.com/files/jsoop/content.html',
	    function(o){
	        document.getElementById('html').innerHTML = o.responseText;
	}
	);
	request(
	    'http://www.phpied.com/files/jsoop/content.xml',
	    function(o){
	        document.getElementById('xml').innerHTML = o.responseXML.getElementsByTagName('root')[0].firstChild.nodeValue;
	}
	);

在XML文档里，`documentElement`所指向的是根节点`<root>`，在HTML文档里，指向的根节点的`<html>`

### 第七章补充:
- 通过`innerHTML`或者`innerText/textContent`属性来进行
- 通过`nodeValue`或者`setAttribute()`以及对象属性中的相关属性来进行

## 第八章 编程模式与设计模式
**模式**就是专门为某些常见问题开发的、优秀的解决方案。

编程模式：
### 8.1.1 行为隔离
一个页面通常是三个要素：
- 内容（HTML）
- 外观（CSS）
- 行为（JavaScript）
### 8.1.2 命名空间
定义一个全局变量，并将其他变量和方法定义为该变量的属性。  

1.  将对象用做命名空间

		    1. 新建一个全局变量MYAPP
		    var MYAPP = MYAPP || {};
		    2. 将要用到的变量作为MYAPP的属性：
		    MYAPP.event = {};
		    3. 为其添加方法
		    MYAPP.event = {
		        addListener: function (e){},
		        removeListener: function (e){};
	}

2. 命名空间中的构造器应用constructor

	 
		    DOM工具本身就定义一个Element构造器。
		    MYAPP.dom = {};
		    MYAPP.dom.Element = function (type, prop){
		    var tmp = document.createElement(type);
		    for (var i in prop){
		        tmp.setAttribute(i,prop[i]);
		    }
		    return tmp;
		    }
		    var  el = new MYAPP.dom.Element(
		    'a'.
		    {href:'http://phpid.com'}
		    );

3. namespace()方法
	很多库中（比如YUI）都实现了一个叫做namespace的工具方法，其调用方法如下：  
	`MYAPP.namespace('dom.style');`  
	等价于：  
	MYAPP.dom = {};
	MYAPP.dom.style = {}

### 8.1.3 初始化分支
不同浏览器对于相同或者相似的方法可能不同的实现。  
定义一个命名空间，并声明了一些事件处理方法。   
然后根据具体浏览器特性探测结果，被赋予不同的实现。

### 8.1.4 延迟定义
与初始化分支模式很相似。不同在于，该模式下的分支只有在相关函数的弟一次被调用时才会发生   
它在第一次被调用时，检查浏览器支持功能，下一次再调用方法，就会直接调用它选择的新方法了

### 8.1。5 配置对象
当一个函数的参数多于三个时，不容易记住顺序，可以将这些参数陈哥某一个对象的属性。
- 不用考虑顺序
	- 可以跳过某些参数的设置
	- 函数的扩展性更强
	- 代码可读性更好

	MYAPP.dom.Button = function (text,conf){
			var type =conf.type || 'submit';
			var font = conf.font || 'Verdana';
			//...
	}
	使用方法：
	var config = {
		font:'Arial, Verdana, sans-serif',
	color: 'white';
	};
	new MYAPP.dom.Button('puuush',config);

### 8.1.6 私有属性和方法
因为JavaScript没有特殊语法来标记私有属性，但可以使用局部变量和函数的方式来实现类似的权限控制

### 8.1.11 JSON
JSON是一种轻量级的数据交换格式，当使用XMLHttpRequest()接收服务器端的数据时，一般使用JSON而不是XML。JSON是JavaScript Object Notation.  
JSON格式由对象和数组标记的数据构成。

	{
	'name':'Stoyan',
	'family':'Stefanov',
	'book':['phpBB2', 'phpBB UG', 'PEAR']'
	}
	假如我们发送一个XHR请求得到了一个JSON字符串，它保存在XHR的responseText属性中
	然后用eval()将该字符串转换成JavaScript对象
	var obj = eval ( ' ( ' +xhr.responseText + ') ' );
	由于eval()有安全隐患，最后使用JavaScript库来处理
	var obj = JSON.parse(xhr.responseText);

### 设计模式
- 创建型模式：涉及对象的创建与初始化
- 结构型模式：描述了如何组合对象以提供新的功能
- 行为型模式：描述了对象之间如何通信
#### 8.2.1 单件模式1
单件是一个创建型的设计模式。需要创建一种类型或者一个类的唯一对象时，使用这个模式。  
最基本的单件模式： `var single = {};`

#### 8.2.2 单件模式2

	function Logger() {
		if (typeof global_log === "undefined"){
		global_log =this;
	}
	return global_log;
	}
	var a = new Logger();
	var b = new Logger();
	alert(a === b); //true
	缺点就是使用了全局变量，在任何时候都有可能被覆盖
	解决方式，使用构造器

#### 8.2.3 工厂模式
也是创建对象的创建型模式。当我们有多个相似的对象而又不知道应该先使用哪种时，考虑工厂模式[
]()
	MYAPP.dom.factory =function(type){
			return new MYAPP.dom(type);
	}
	var o = MYAPP.dom.factory(type);
	o.url = 'http://...'
	o.insert();

#### 8.2.4 装饰器模式
是一种结构型模式，考虑的是如何拓展对象的功能

#### 8.2.5 观察者模式
行为型模式




[image-1]:	7.png
[image-2]:	8.png
[image-3]:	9.png
[image-4]:	1.png
[image-5]:	2.png
[image-6]:	3.png
[image-7]:	4.png
[image-8]:	5.png
[image-9]:	6.png
[image-10]:	10.png
[image-11]:	11.png
[image-12]:	12.png
[image-13]:	13.png
[image-14]:	14.png
[image-15]:	15.png