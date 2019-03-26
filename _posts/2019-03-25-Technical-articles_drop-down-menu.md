---
layout: post_layout
title: 技术篇-二级菜单
time: 2019年03月25日 星期一
location: 广州
---
最近研究二级菜单，发现有三种实现方法

第一种：纯html+css

{% highlight html linenos %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    *{margin:0;padding: 0;list-style: none;text-decoration: none;}
    #nav{width: 500px;height: 40px;background: #ccc;margin: 0 auto;display: flex;justify-content: center;}
    ul{background: #aaa}
    ul li{float:left; display:block; height: 40px; line-height: 40px; padding: 0 20px; position: relative;}
    ul li:hover{background: #cea;}
    ul li ul li{float: none;}
    /*关键一：将二级菜单设置为display：none;*/
    ul li ul{position: absolute;top:40px;left: 0; display: none;}
    ul li ul li:hover{background: red;}
    /*关键二：在划过二级菜单从属的一级菜单时，设置为display:block;*/
    ul li:hover ul{display: block;}
    </style>
</head>
<body>
    <div id="nav">
        <ul>
            <li><a href="">首页</a></li>
            <li><a href="">汽车</a>
                <ul>
                    <li><a href="#">奥迪</a> </li>
                    <li><a href="#">道奇</a> </li>
                </ul>
            </li>
            <li><a href="">手机</a>
                <ul>
                    <li><a href="#">小米</a> </li>
                    <li><a href="#">华为</a> </li>
                </ul>
            </li>
            <li><a href="">联系我们</a></li>
        </ul>
    </div>   
</body>
</html>
{% endhighlight %}

第二种：JavaScript

{% highlight html linenos %}
<!DOCTYPE html>
<html lang="en">
<head>
    <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Document</title>
<style>
*{margin:0;padding: 0;list-style: none;text-decoration: none;}
#nav{width: 500px;height: 40px;background: #ccc;margin: 0 auto;display: flex;justify-content: center;}
ul{background: #aaa}
ul li{float:left; display:block; height: 40px; line-height: 40px; padding: 0 20px; position: relative;}
ul li:hover{background: #cea;}
ul li ul li{float: none;}
ul li ul{position: absolute;top:40px;left: 0; display:none;}
ul li ul li:hover{background: red;}
</style>
</head>
<body>
<div id="nav">
<ul>
<li><a href="#">首页</a></li>
<li onmouseover="show(this)" onmouseout="hide(this)"><a href="#">汽车</a>
<!-- 关键一：在二级标题从属的一级标题标签内设置时间执行程序，this代表的时这个li元素 -->
<ul>
<li><a href="#">奥迪</a> </li>
<li><a href="#">道奇</a> </li>
</ul>
</li>
<li onmouseover="show(this)" onmouseout="hide(this)"><a href="#">手机</a>
<ul>
<li><a href="#">小米</a> </li>
<li><a href="#">华为</a> </li>
</ul>
</li>
<li><a href="#">联系我们</a></li>
</ul>
</div>	
<script>
function show(li){
var ul=li.getElementsByTagName("ul")[0];
// 关建二：在li这个对象内查询标签名为ul的标签，由于二级标签只有一个，所以索引为0即可。
ul.style.display="block";
// 关键三：当鼠标划过li时，其子元素ul标签的display为block
}
function hide(li){
var ul=li.getElementsByTagName("ul")[0];
ul.style.display="none";
// 关键四：当鼠标划出li时，其子元素ul的display为none
}
</script>
</body>
</html>
{% endhighlight %}

第三种：jQuery

{% highlight html linenos %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
<style>
    *{margin:0;padding: 0;list-style: none;text-decoration: none;}
    #nav{width: 500px;height: 40px;background: #ccc;margin: 0 auto;display: flex;justify-content: center;}
    ul{background: #aaa}
    ul li{float:left; display:block; height: 40px; line-height: 40px; padding: 0 20px; position: relative;}
    ul li:hover{background: #cea;}
    ul li ul li{float: none;}
    ul li ul{position: absolute;top:40px;left: 0; display: none;}
    ul li ul li:hover{background: red;}
</style>
</head>
<body>
    <div id="nav">
    <ul>
        <li><a href="">首页</a></li>
        <li class="navmenu"><a href="">汽车</a>
          <ul>
               <li><a href="#">奥迪</a> </li>
               <li><a href="#">道奇</a> </li>
         </ul>
        </li>
        <li class="navmenu"><a href="">手机</a>
          <ul>
              <li><a href="#">小米</a> </li>
              <li><a href="#">华为</a> </li>
         </ul>
        </li>
        <li><a href="">联系我们</a></li>
   </ul>
</div>	
<script src="jquery-3.1.1.js"></script>
<!-- 关键一：引入jQuery库文件 -->
<script type="text/javascript">
$(function(){
   $(".navmenu").mouseover(function(){
              $(this).children("ul").show();
})

})
// 关键二：正确使用jQuey的语法完成行为。
$(function(){
   $(".navmenu") .mouseout(function(){
             $(this).children("ul").hide();
})

})
</script>
</body>
</html>
{% endhighlight %}

总结：第一种方法可以完美的把结构完全分类，第二种方法我个人不太推荐的，因为太乱了........，第三种方法个人很喜欢，简单明了，还是jquery方便，不过那种方法都好适合自己的就行。