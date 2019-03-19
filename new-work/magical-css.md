#css部分奇特用法总结

##01 css选择器中:first-child与:first-of-type的区别
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




