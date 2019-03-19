# css部分奇特用法总结

## 01 css选择器中:first-child与:first-of-type的区别
+ :first-child选择器是css2中定义的选择器，从字面意思上来看也很好理解，就是第一个子元素。比如有段代码：

![](https://images0.cnblogs.com/blog/130623/201402/261609099832424.png)

+ p:first-child  匹配到的是p元素,因为p元素是div的第一个子元素；

h1:first-child  匹配不到任何元素，因为在这里h1是div的第二个子元素，而不是第一个；

span:first-child  匹配不到任何元素，因为在这里两个span元素都不是div的第一个子元素；

然后，在css3中又定义了:first-of-type这个选择器，这个跟:first-child有什么区别呢？还是看那段代码：

![](https://images0.cnblogs.com/blog/130623/201402/261609107566595.png)

+ p:first-of-type  匹配到的是p元素,因为p是div的所有类型为p的子元素中的第一个；

h1:first-of-type  匹配到的是h1元素，因为h1是div的所有类型为h1的子元素中的第一个；

span:first-of-type  匹配到的是第三个子元素span。这里div有两个为span的子元素，匹配到的是它们中的第一个。

 

所以，通过以上两个例子可以得出结论：

:first-child 匹配的是某父元素的第一个子元素，可以说是结构上的第一个子元素。

:first-of-type 匹配的是某父元素下相同类型子元素中的第一个，比如 p:first-of-type，就是指所有类型为p的子元素中的第一个。这里不再限制是第一个子元素了，只要是该类型元素的第一个就行了。

+ 同样类型的选择器 :last-child  和 :last-of-type、:nth-child(n)  和  :nth-of-type(n) 也可以这样去理解。


## 02 css3 - 选择器first-child、last-child、nth-child、nth-last-child、nth-of-type


### 01.first-child（IE7兼容）、last-child（IE8不兼容)


![](https://img-blog.csdn.net/20170427095716267?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZXJkb3V6aGFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


 html:
   
	<body>
	  <h2>列表</h2>
	  <ul>
	    <li>列表项目1</li>
	    <li>列表项目2</li>
	    <li>列表项目3</li>
	    <li>列表项目4</li>
	  </ul>
	</body>
css:

	<style>
    ul {list-style: none;}
    li:first-child {/*给第一个列表项目设置样式 兼容IE7*/
      background-color: pink;
    }
    li:last-child { /*给最后一个列表项目设置样式 IE8不兼容*/
      background-color: red;
    }
	</style>
解析： 一个页面中无论有几个ul列表，只要设置first-child、last-child，那么所有ul列表项的第一个和最后一个列表项目都会有设置的样式。


### 02. nth-child、nth-last-child （IE8不兼容）


![](https://img-blog.csdn.net/20170427100715702?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZXJkb3V6aGFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


html:

	<body>
	  <h2>列表</h2>
	  <ul>
	    <li>列表项目1</li>
	    <li>列表项目2</li>
	    <li>列表项目3</li>
	    <li>列表项目4</li>
	    <li>列表项目5</li>
	    <li>列表项目6</li>
	  </ul>
	</body>
css:

	<style>
    ul {list-style: none;}    
    li:nth-child(3) { /*表示li元素中，第三个元素 IE8不兼容*/
      background-color: pink;
    }
    li:nth-last-child(2) { /*表示li元素中，倒数第二个元素 IE8不兼容*/
      background-color: red;
    }
	</style>


### 03. 对奇数、偶数使用样式


![](https://img-blog.csdn.net/20170427101619762?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZXJkb3V6aGFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


html:

	<ul>
	    <li>列表项目1</li>
	    <li>列表项目2</li>
	    <li>列表项目3</li>
	    <li>列表项目4</li>
	    <li>列表项目5</li>
	    <li>列表项目6</li>
	</ul>
css:

	<style>
    ul {list-style: none;}
    li:nth-child(odd) {/*表示li元素中，从1开始 奇数为pink*/
      background-color: pink;
    }
    li:nth-child(even) {/*表示li元素中，从1开始 偶数为灰色*/
      background-color: #ccc;
    }
	</style>

解析： li:nth-child(odd)含义：li的父元素ul的儿子中，从1开始数，奇数儿子设置样式为xxx; 
当父元素为列表时，因为只有列表项目一种子元素，不会出现问题；当父元素是div时，就不止一种子元素，会引起问题。如下： 
例如：设置div元素中为奇数标题h2背景颜色

	html:
	
	<div>
	    <h2>文章标题A</h2>
	    <p>我是一个小段落。。。</p>
	    <h2>文章标题B</h2>
	    <p>我是一个小段落。。。</p>
	    <h2>文章标题C</h2>
	    <p>我是一个小段落。。。</p>
	    <h2>文章标题D</h2>
	    <p>我是一个小段落。。。</p>
	</div>
	
	css:
	
	h2:nth-child(odd) {
	      background-color: pink;
	}
执行结果为：


 
![](https://img-blog.csdn.net/20170427103104110?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZXJkb3V6aGFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


解析： h2:nth-child(odd)含义是：h2的父元素div 的所有儿子中 为奇数的儿子 设置背景颜色；而不是所有h2中为偶数的h2设置样式； 
解决方法： nth-of-type可以避免则会中问题产生


### 04. nth-of-type（IE8不兼容）：只针对同类型的元素进行计算


![](https://img-blog.csdn.net/20170427104028421?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZXJkb3V6aGFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


css:

	h2:nth-of-type(odd) { /*所有h2标签中为奇数的设置样式*/
	    background-color: pink;
	}
	h2:nth-of-type(even) { /*所有h2标签中为偶数的设置样式*/
	    background-color: #ccc;
	}
解析： h2:nth-of-type(odd)含义：在所有h2标签中，只要是奇数h2就设置样式；只针对h2标签，与父元素无关；


### 05. 循环使用样式 li:nth-child(4n+1)


![](https://img-blog.csdn.net/20170427105049966?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZXJkb3V6aGFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


html：

	<ul>
	   <li>列表项目1</li>
	   <li>列表项目2</li>
	   <li>列表项目3</li>
	   <li>列表项目4</li>
	   <li>列表项目5</li>
	   <li>列表项目6</li>
	   <li>列表项目7</li>
	   <li>列表项目8</li>
	   <li>列表项目9</li>
	   <li>列表项目10</li>
	   <li>列表项目11</li>
	   <li>列表项目12</li>
	</ul>
css：

	<style>
	    ul {list-style: none;}
	    li:nth-child(4n+1) { /*表示li元素中，4个li为一组循环 第一个li设置为*/
	      background-color: red;
	    }
	    li:nth-child(4n+2) { /*表示li元素中，4个li为一组循环 第二个li设置为*/
	      background-color: pink;
	    }
	    li:nth-child(4n+3) {
	      background-color: #ccc;
	    }
	    li:nth-child(4n+4) {
	      background-color: yellow;
	    }
	</style>
解析： 

4n含义：四个li元素为一组循环； 

4n+1含义：这一组循环中，第一个样式； 

4n+2含义：这一组循环中，第二个样式； 

4n+3含义：这一组循环中，第三个样式； 

4n+4含义：这一组循环中，第四个样式；



--------------------- 
作者：erdouzhang 
来源：CSDN 
原文：https://blog.csdn.net/erdouzhang/article/details/70842177 


## 03. css花样选择器

### 01. >（子选择器）

	#a>p{　　 // 使用 > 号，让选择器选择id="a"的所有子类（直接子类）
	
	html:
	<div id="a">
    <p>11111111111111</p>
    <p>22222222222222</p>
    <div>
	　　<p>333333333</p>
	　	</div><!--该<p>在<div>中-->
	</div>
	
	css:
	<style>
        #a>p
        {
            background-color:Red; 
            }
    </style>

结果:

![](https://images0.cnblogs.com/blog2015/743207/201507/251615357656052.png)

### 02. +（相邻选择器）

h1+p，选择紧接在另一个元素后的元素，而且二者有相同的父元素。只会选择第一个相邻的匹配元素。

	html:

	<div id="a">
    <h1>11111111111111</h1>
    <p>22222222222222</p>
    <p>33333333333333</p><!--只会选择第一个相邻的匹配元素-->
    <div>
      <p>44444444444</p>
    </div>
	</div>
	
	css:

	h1+p{
        background-color:Red; 
    }

结果:


![](https://images2015.cnblogs.com/blog/743207/201510/743207-20151012215355272-1561419380.png)


### 03. ~(匹配选择器)

	#b~p，匹配所有在#b元素之后的同级p元素。

	<style>
		h1~p
        {
            background-color:Red; 
            }
	</style>


	<div id="a">
	    <h1>11111111111111</h1>
	    <p>22222222222222</p>
	    <p>33333333333333</p>
	    <div>
	      <p>44444444444</p>
	    </div>
	</div>
	
	所有相匹配的P元素都被选择到。

结果:

![](https://images2015.cnblogs.com/blog/743207/201510/743207-20151012215642085-1798651011.png)

## 04. 利用 :first-child 和 :nth-last-child 确定子元素数目

读《css揭秘》时，发现选择器的神奇作用，可以确定子元素数目，比如：

	li:first-child:nth-last-child(2),li:first-child:nth-last-child(2)~li {
		background-color:pink;
	}

这个适用于第一个子元素为`li`且父元素拥有2个子元素，则第一个`li`和后续的`li`都将适用，并且如果有更多或更少的子元素都不会适用。

仔细思考下其中的核心逻辑：

`first-child:nth-last-child(2)`=>即是第1个，又是倒数第2个=>总共有两个子元素

利用选择器还可以继续拓展：

`first-child:nth-last-child(n+2)`=>即是第1个，又是第2,3,4,,,个=>子元素数目>2

`first-child:nth-last-child(-n+4)`=>即是第1个，又是倒数第1,2,3,4个=>子元素数目<=4

`first-child:nth-last-child(-n+4):nth-last-child(n+2)`=>即是第1个，又是第2,3,4,,,个，又是倒数第1,2,3,4个=>子元素数目[2,4]

## 05. CSS中伪类及伪元素用法详解

### 01. 伪类的分类及作用：

![](https://images0.cnblogs.com/i/613712/201406/011913555563267.png)

![](https://images0.cnblogs.com/i/613712/201406/042055205362355.png)

注：该表引自W3School教程

伪元素和伪类的区别从作用也可以看出

伪元素：伪元素是创造关于文档语言能够指定的文档树之外的抽象。例如文档语言不能提供访问元素内容第一字或者第一行的机制。伪元素允许设计师引用它们，否则这是难以办到的。

伪元素还提供样式设计师给在源文档中不存在的内容分配样式（例如：:before和:after能够访问产生的内容）。

伪类：伪类对元素进行分类是基于特征(characteristics)而不是它们的名字、属性或者内容；原则上特征是不可以从文档树上推断得到的。

何为伪类?就是css内植类css内部本身赋予它一些特性和功能，也就是你不用再class=...或id=...你就可以直接拿来使用，当然你也可以改变它的部分属性比如：                        a:link{color:#FF0000;}

#### :active 

大致效果为用鼠标点击时，元素增加特效，鼠标松开时，特效消失。多用在按钮的点击上。

写法:

![](https://images0.cnblogs.com/i/613712/201406/042058501308554.png)

这里id为box的是一div块，在css中首先设置了他的基本样式，下面为加入:active伪类后需要修改的样式。

未点击时:
![](https://images0.cnblogs.com/i/613712/201406/042102098803663.png)
点击之后:
![](https://images0.cnblogs.com/i/613712/201406/042102395993284.png)

:active、:hover、:focus这几种常用伪类写法一致，下面就不再赘述。为了直观贴上几张GIF，方便大家理解。

正如之前所说的:active经常用在按钮的点击上：

![](https://images0.cnblogs.com/i/613712/201406/042106220831449.gif)

大致写法就是：在点击之后让按钮的坐标下移1-2像素并缩小外部阴影，由此给人一种立体的感觉。当然，大家可以发挥想象，充分利用伪类来做出最炫的交互。

#### :hover

当我们需要对某一对象添加当鼠标悬浮之上时改变样式，就可以用到:hover伪类。

这里还是用按钮来做演示：

![](https://images0.cnblogs.com/i/613712/201406/042119028955482.gif)

当光标放在按钮上，按钮的背景色和文字颜色做一反色并加上渐变，这种效果简单但吸引人。当然大家也可以随着不断学习挑战更加炫酷的效果。 

这里多说一句：

![](https://images0.cnblogs.com/i/613712/201406/042124074892027.png)

:hover的好搭档cursor属性，当属性值为pointer时，如上上图，光标覆盖目标时会变成手型。cursor还有url属性，其为设置图片地址。

在之后用javascript或者HTML5做游戏时，系统的光标就显得格格不入了。这里可以通过cursor将光标变成你想要的手型图片，比如这样的：![](https://images0.cnblogs.com/i/613712/201406/042129291929144.png)

此时cursor属性可以放在全局body{}里或者任何你需要的地方。

#### :focus

当我们需要让点击之后的元素一直拥有某些样式，这时用:active就不行了，因为松开鼠标样式会消失。:focus可以用在<input>标签上。

这是之前做过一简单的表单：

![](https://images0.cnblogs.com/i/613712/201406/011937443064776.png)

:focus与之前伪类所产生的来不一样的效果：

![](https://images0.cnblogs.com/i/613712/201406/032216533954644.gif)

#### :first-child

对元素的第一个子元素添加样式，常用在ol,ul下面的li，或者tr下面的td或th上等等。

![](https://images0.cnblogs.com/i/613712/201406/042139395673305.png)

效果：

![](https://images0.cnblogs.com/i/613712/201406/042140085201327.png)

实际中常用到的地方：

![](https://images0.cnblogs.com/i/613712/201406/042141582391174.png)

 在实际编写页面上，经常会有像上图一样的布局。多个图片并排放在一行，对于多个样式相似并排的元素我们通常将其放在列表标签里的`<li></li>`中，这时我们可以先在li的样式中用margin-right来设置`li`之间的间距既每张图间的间距，之后在`li`的:first-child中通过margin-left来设置第一张与左边界的距离，从而调整好整排图片或元素在网页中的布局。

#### 伪元素:before和:after

 二者的作用为在元素之前或之后插入某些内容，注意：这里的“前后”并不是位置上的前后，而是文档流里的前后。

通常情况下用来做这个：

![](https://images0.cnblogs.com/i/613712/201406/042157091454353.png)

这个：

![](https://images0.cnblogs.com/i/613712/201406/042157224118800.png)

以及这个：

![](https://images0.cnblogs.com/i/613712/201406/042157342559547.png)

都是一些指引型的小三角或者小箭头之类的。

代码：

![](https://images0.cnblogs.com/i/613712/201406/042200030364896.png)

通过给一div附上某一小图标，然后设置与该div的相关位置。

content中的内容参见unicode几何图形列表，由于过大就不在这里贴了，只截取一小部分展示下，有兴趣的朋友百度吧。

 ![](https://images0.cnblogs.com/i/613712/201406/042204514277023.png)

当然！！before及after的用法绝不这么简单!

你可以将content属性设置为“”，然后尽情发挥想象：

![](https://images0.cnblogs.com/i/613712/201406/042211265995729.gif)

这里不仅用了:hover，按钮外部的光圈就是通过:before做出来的。

--------------------- 
作者：路修远而求索 

来源：博客园

原文：https://www.cnblogs.com/keyi/p/5943178.html

### 02. 详解::before和::after伪元素的用法

#### 介绍

css3为了区分伪类和伪元素，伪元素采用双冒号写法。

常见伪类——:hover,:link,:active,:target,:not(),:focus。

常见伪元素——::first-letter,::first-line,::before,::after,::selection。

::before和::after下特有的content，用于在css渲染中向元素逻辑上的头部或尾部添加内容。

这些添加不会出现在DOM中，不会改变文档内容，不可复制，仅仅是在css渲染层加入。

所以不要用:before或:after展示有实际意义的内容，尽量使用它们显示修饰性内容，例如图标。

举例：网站有些联系电话，希望在它们前加一个icon☎，就可以使用:before伪元素，如下：

	<!DOCTYPE html>
	<meta charset="utf-8" />
	<style type="text/css">
	    .phoneNumber::before {
	    content:'\260E';
	    font-size: 15px;
	}
	</style>
	<p class="phoneNumber">12345645654</p>

![](https://images0.cnblogs.com/blog2015/315302/201508/101728385358643.png)

Note:这些特殊字符的html，js和css的写法是不同的，具体可查看html特殊字符的html，js，css写法汇总。

#### content属性

::before和::after必须配合content属性来使用，content用来定义插入的内容，content必须有值，至少是空。默认情况下，伪类元素的display是默认值inline，可以通过设置display:block来改变其显示。

content可取以下值。

##### 01. string

使用引号包一段字符串，将会向元素内容中添加字符串。如：a:after{content:""}

举例：

	<!DOCTYPE html>
	<meta charset="utf-8" />
	<style type="text/css">
	p::before{
	    content: "《";
	    color: blue;
	}
	p::after{
	    content: "》";
	    color: blue;
	}
	</style>
	<p>平凡的世界</p>

![](https://images0.cnblogs.com/blog2015/315302/201508/110929133328022.png)

##### 02. attr()

通过attr()调用当前元素的属性，比如将图片alt提示文字或者链接的href地址显示出来。

	<style type="text/css">
	a::after{
	    content: "(" attr(href) ")";
	}
	</style>
	<a href="http://www.cnblogs.com/starof">starof</a>

![](https://images0.cnblogs.com/blog2015/315302/201508/110937215201245.png)

##### 03. url()/uri()

用于引用媒体文件。

举例：“百度”前面给出一张图片，后面给出href属性。

	<style>
	a::before{
	    content: url("https://www.baidu.com/img/baidu_jgylogo3.gif");
	}
	a::after{
	    content:"("attr(href)")";
	}
	a{
	    text-decoration: none;
	}
	</style>
	---------------------------
	<body>
	<a href="http://www.baidu.com">百度</a>
	</body>    

![](https://images0.cnblogs.com/blog2015/315302/201505/041517505323703.png)

##### 04. counter()

调用计数器，可以不使用列表元素实现序号功能。

配合counter-increment和counter-reset属性使用：

h2:before { counter-increment: chapter; content: "Chapter " counter(chapter) ". " }

代码:

	<style>
	body{
	    counter-reset: section;
	}
	h1{
	    counter-reset: subsection;
	}
	h1:before{
	    counter-increment:section;
	    content:counter(section) "、";
	}
	h2:before{
	    counter-increment:subsection;
	    content: counter(section) "." counter(subsection) "、";
	}
	</style>
	------------------------------------------------
	<body>
	<h1>HTML tutorials</h1>
	<h2>HTML Tutorial</h2>
	<h2>XHTML Tutorial</h2>
	<h2>CSS Tutorial</h2>
	
	<h1>Scripting tutorials</h1>
	<h2>JavaScript</h2>
	<h2>VBScript</h2>
	
	<h1>XML tutorials</h1>
	<h2>XML</h2>
	<h2>XSL</h2>
	
	</body>   

效果：

![](https://images0.cnblogs.com/blog2015/315302/201505/041646256106350.png)

了解更多可参考：https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Counters

#### 使用

##### 01. 清除浮动

清除浮动方法有多种，现在最常用的就是下面这种方法，仅需要以下样式即可在元素尾部自动清除浮动

		.cf:before,
	.cf:after {
	    content: " ";
	    display: table; 
	}
	.cf:after {
	    clear: both;
	}
	.cf {
	    *zoom: 1;
	}

##### 02. 模拟float:center的效果

float没有center这个取值，但是可以通过伪类来模拟实现。

这个效果实现很有意思，左右通过::before float各自留出一半图片的位置，再把图片绝对定位上去。

核心css如下：

		#page-wrap { width: 60%; margin: 40px auto; position: relative; }
	#logo { position: absolute; top: 0; left: 50%; margin-left: -125px; }
	#l, #r { width: 49%; }
	#l { float: left; }
	#r { float: right; }
	#l:before, #r:before { content: ""; width: 125px; height: 250px; }
	#l:before { float: right; }
	#r:before { float: left; }

效果图:

![](https://images0.cnblogs.com/blog2015/315302/201508/111029267074149.png)

![](https://images0.cnblogs.com/blog2015/315302/201508/111033227399273.png)

出自：https://css-tricks.com/float-center/

##### 03. 做出各种图形效果

举例：一个六角星

	<style>
	#star-six {
	  width: 0;
	  height: 0;
	  border-left: 50px solid transparent;
	  border-right: 50px solid transparent;
	  border-bottom: 100px solid red;
	  position: relative;
	}
	#star-six::after {
	  width: 0;
	  height: 0;
	  border-left: 50px solid transparent;
	  border-right: 50px solid transparent;
	  border-top: 100px solid red;
	  position: absolute;
	  content: "";
	  top: 30px;
	  left: -50px;
	}
	</style>
	<body>
	<div id="star-six"></div>
	</body>

  #star-six的div是一个正三角行，#star-six::after是一个倒三角形，通过绝对定位，调整其位置即可实现六角星的效果。

![](https://images0.cnblogs.com/blog2015/315302/201508/111044162547286.png)

https://css-tricks.com/the-shapes-of-css/
点我查看更多

##### 04. 不使用图片创建小图标

举例：比如一个电话

很巧妙的应用一个div左border加圆角当机身，::before和::after配合圆角当听筒。

	<style type="text/css">
	    #phone{
			width:50px;
			height:50px;
			border-left:6px solid #EEB422;border-radius:20%;
			transform:rotate(-30deg);
			-webkit-transform:rotate(-30deg);
			margin:20px;
			margin-right:0px;position:relative;
			display: inline-block;top: -5px;
			}
	    #phone:before{
				width:15px;
				height:15px;
				background:#EEB422;
				border-radius: 20%;
				content: "";
				position: absolute;
				left:-2px;top: 1px;
			}
	    #phone:after{width:15px;
					height:15px;
					background:#EEB422;
					border-radius: 20%;
					content: "";
					position: absolute;
					left:-3px;top: 34px;
					}
	</style>
	<div id="wraper">
	    <div id="phone"></div>
	</div>

![](https://images0.cnblogs.com/blog2015/315302/201508/111116453175937.png)

更多图标

![](https://images0.cnblogs.com/blog2015/315302/201508/111126032237893.png)

这个效果来自：http://www.w3cfuns.com/blog-5444604-5402127.html

有大神用伪元素创建了84种小图标，具体可查看http://nicolasgallagher.com/pure-css-gui-icons/

##### 05. 显示打印网页的URL

	<style>
	@media print {
	  a[href]:after {
	    content: " (" attr(href) ") ";
	  }
	}
	</style><body>
	<a href="http://www.baidu.com">百度</a>
	</body> 


![](https://images0.cnblogs.com/blog2015/315302/201505/041721073927186.png)

##### 06. 给blockquote添加引号

经常用到给blockquote 引用段添加巨大的引号作为背景，可以用 ：:before 来代替 background 。好处是即可以给背景留下空间，还可以直接使用文字而非图片：

		<meta charset="utf-8"/>
	<style type="text/css">
	    blockquote::before {
	    content: open-quote;
	    color: #ddd;
	    z-index: -1;
	    font-size:80px;
	}
	</style>
	<blockquote>引用一个段落,双引号用::before伪元素实现</blockquote>

![](https://images0.cnblogs.com/blog2015/315302/201508/111141231299523.png)

##### 07. 超链接特效

	举例：配合 CSS定位实现一个鼠标移上去，超链接出现方括号的效果
	
	<meta charset="utf-8" />
	<style type="text/css">
	body{
	    background-color: #425a6c;
	}
	    a {
	    position: relative;
	    display: inline-block;
	    outline: none;
	    color: #fff;
	    text-decoration: none;
	    font-size: 32px;
	    padding: 5px 20px;
	}
	a:hover::before, a:hover::after { position: absolute; }
	a:hover::before { content: "\5B"; left: -10px; }
	a:hover::after { content: "\5D"; right:  -10px; }
	</style>
	<a>鼠标移上去出现方括号</a>

![](https://images0.cnblogs.com/blog2015/315302/201508/111326598647483.png)

更多创意链接特效可参考： Creative Link Effects 。


##### 08. ::before和::after实现多背景图片

举例：一个标签应用5张背景图

![](https://images0.cnblogs.com/blog2015/315302/201508/111409393792336.png)

原效果来自：Multiple Backgrounds and Borders with CSS 2.1

这个效果看的真的是脑洞大开，虽然多背景图用css3的background-image很容易就能实现。但是这篇文章是10年写的，已经过去5年了，想想也正是他们这样的尝试和努力才加速了css3标准的制定，让今天的开发更easy。今天的我们又能为5年后的开发人员做些什么贡献呢？

--------------------- 
作者：路修远而求索 

来源：博客园

原文：https://www.cnblogs.com/keyi/p/5943133.html