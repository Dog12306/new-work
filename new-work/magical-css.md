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