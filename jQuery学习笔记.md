##jQUery学习笔记
 * $(document).ready(function(){});
>hide() 隐藏
show(100)  显示
toggle   替换hide()与show()来切换隐藏与显示
fadeIn()  淡入效果
fadeout()  淡出效果
fadeToggle()  切换淡入淡出
fadeTo("slow",0.15);  允许渐变为给定的不透明度（值介于 0 与 1 之间）
slideUp("slow");  向上滑动
slideDown（） 向下滑动
slideToggle()  切换滑动效果

 * 需要事先把div属性设置成为`position:absolute`;
>animate动画
animate({left:'250px'});
 ```javascript
 $("#p10").animate({
				left:'250px',
				 opacity:'0.5',
				 // height:'150px',
				 // width:'150px'  +=增加大小
				height:'+=150px',
      			width:'+=150px'});
			});
animate({height:'toggle'});
队列动画
$(document).ready(function(){
  $("button").click(function(){
    var div=$("div");
    div.animate({height:'300px',opacity:'0.4'},"slow");
    div.animate({width:'300px',opacity:'0.8'},"slow");
    div.animate({height:'100px',opacity:'0.4'},"slow");
    div.animate({width:'100px',opacity:'0.8'},"slow");
  });
});
```

>stop();    按钮会停止当前活动的动画，但允许已排队的动画向前执行。
stop(true); "停止所有" 按钮停止当前活动的动画，并清空动画队列；因此元素上的所有动画都会停止。
stop(true,true);  "停止但要完成" 会立即完成当前活动的动画，然后停下来。

#Callback 函数在当前动画 100% 完成之后执行。
#####错误（没有 callback）

$("p").hide(1000);
alert("The paragraph is now hidden");

#####正确（有 callback）

$("p").hide(1000,function(){
alert("The paragraph is now hidden");
});

####jquery连接技术
 * 多种属性连接到一起
  * $("#p13").css("color","red").slideUp(2000).slideDown(2000);
 * 获取id为test的输入框的值
  * alert("Value: " + $("#test").val());
 * 获取id为test的文本
  * $("#test").text());
 * 获取id为test的文本和html代码
  * $("#test").html());
 * 获取id为w3s的href的值
  * $("#w3s").attr("href")
 * 改变href的值
  * $("#w3s").attr("href","http://www.w3school.com.cn/jquery");

##改变值，相当于innerHTML
>.html()是用来读取元素的html内容（包括html标签），.text()用来读取元素的纯文本内容，包括其后代元素，.val()是用来读取表单元素的"value"值。其中.html()和.text()方法不能使用在表单元素上,而.val()只能使用在表单元素上
>$("#test1").text("Hello world!");
$("#test2").html("<b>Hello world!</b>");
$("#test3").val("Dolly Duck");

##增加，删除内容
>$("#p14").append("<b>后面增加新内容</b>");
>append()前面是要选择的对象，后面是要在对象内插入的元素内容
appendTo()前面是要插入的元素内容，而后面是要选择的对象
```javascript
	$(".content").append('<div class="append">通过append方法添加的元素</div>')
    $('<div class="appendTo">通过appendTo方法添加的元素</div>').appendTo($(".content"))
```
$("#p14").after("<b>后面增加新内容</b>");
prepend()向每个匹配的元素内部前置内容
prependTo()把所有匹配的元素前置到另一个指定的元素集合中
```javascript
 $('<p>prependTo增加的p元素</p>').prependTo($('.aaron2'))
```
通过empty移除了当前div元素下的所有p元素,但是本身的div元素没有被删除,通过empty方法移除里面div的所有元素，它只是清空内部的html代码，但是标记仍然留在DOM中
$("div").empty()
$("#p14").prepend("<b>前面增加新内容</b>");
$("#p14").before("<b>前面增加新内容</b>");
$("#p14").remove();   删除内容
remove会将元素自身移除，同时也会移除元素内部的一切，包括绑定的事件及与该元素相关的jQuery数据。DOM节点不存在了,同事事件也会被销毁
$("p").remove(".p01");//删除class为p01的元素节点
区别：empty不能删除自己本身这个节点  remove该节点与该节点所包含的所有后代节点将同时被删除
#####detach
  这个方法不会把匹配的元素从jQuery对象中删除，因而可以在将来再使用这些匹配的元素。与remove()不同的是，所有绑定的事件、附加的数据等都会保留下来。
$("p").detach()

>$("#addcss").addClass("fontclass");   增加CSS
$("#addcss").rmoveClass("fontclass");  删除css
$("#addcss").toggleClass("fontclass");  切换css

$(this).clone().css   复制所有匹配的元素集合，包括所有匹配元素、匹配元素的下级元素、文字节点。
#####替换并删除节点
```javascript
 $(".right > div:first p:eq(1)").replaceWith('<a style="color:red">replaceWith替换第二段的内容</a>')
 $('<a style="color:red">replaceAll替换第六段的内容</a>').replaceAll('.right > div:last p:last');
```
###DOM包裹wrap()方法（创建父级元素）
```javascript
创建父级元素（对于单个创建）
一个p元素增加一个div包裹
$('p').wrap('<div></div>')
删除父级元素
$('p').unwrap('<div></div>')
所有p元素外部增加一个div包裹
$('p').wrapAll('<div></div>');
wrapInner方法给所有P元素增加内部父容器div
$('p').wrapInner('<div></div>');
```

###更改CSS样式
```javascript
$("#color").css({"background":"red","font-size":"30px"}); 
 $("#color").css("font-weight","bold");
  $("#div3").width(320).height(320);    更改宽度高度
  .css({
            'font-size'        :"15px",
            "background-color" :"#40E0D0",
            "border"           :"1px solid red"
        })
add()将元素追加到匹配元素集合中
        $('#demo1").add('#demo2");
```
 
 ##返回高度宽度
 ```javascript
  $(document).ready(function(){
  $("#btn09").click(function(){
    var txt="";
    txt+="Width of div: " + $("#div1").width() + "</br>";
    txt+="Height of div: " + $("#div1").height() + "</br>";
    txt+="Inner width of div: " + $("#div1").innerWidth() + "</br>";
    txt+="Inner height of div: " + $("#div1").innerHeight();
    
    txt+="Outer width of div: " + $("#div1").outerWidth() + "</br>";
    txt+="Outer height of div: " + $("#div1").outerHeight();
    
    $("#div1").html(txt);
  });
});
 ```
>innerWidth() - 返回元素的宽度（包括内边距）。
>innerHeight() - 返回元素的高度（包括内边距）。
>outerWidth() - 返回元素的宽度（包括内边距和边框）。
outerHeight() - 返回元素的高度（包括内边距和边框）。

##遍历
>$("span").parent().css({"color":"red","border":"2px solid red"});   定义直接直接父级元素的css样式
>$("span").parents().css({"color":"red","border":"2px solid red"});   所有span元素的所有祖先
$("div").closet("li')首先从本身开始向上匹配，若匹配到符合要求的第一个，即停止匹配。
$("span").parentsUntil("div").css   定义两个元素之间的祖先
$("div").children().css({"color":"red","border":"2px solid red"});   定义div的孩子的css样式
 $("div").children("p.1").css;   定义div中孩子p为class为1的样式
 $("div").find("span").css  定义属于div后代的所有span元素：
 $("div").find("*");  定义div的所有后代
 $("h2").siblings().css  定义同胞（同级）元素
  $("h2").siblings("p")  同胞元素的所有p元素，前后相邻的兄弟节点：
  $("h2").next();   下一个同胞元素
  nextAll() 方法返回被选元素的所有跟随的同胞元素（就是他之下的元素）
 $("h2").nextUntil("h6");返回介于h2与h6元素之间的所有同胞元素：
 $('.item-3').prev()  通过prev是匹配合集中每一个元素的上一个兄弟元素
 $("div p").first().css 选取首个 div元素内部的第一个 p 元素
 $("div p").last().css  选择最后一个div元素中的最后一个p元素：
 $("p").eq(1).css("background-color","yellow");索引号从 0 开始，因此首个元素的索引号是 0 而不是 1。下面的例子选取第二个p元素（索引号 1）：
 $("p").filter(".intro").css  不匹配这个标准的元素会被从集合中删除，匹配的元素会被返回
 $("p").not(".intro");返回不带有类名 "intro" 的所有p元素
 
 ```javascript
 each  遍历
  $("button:first").click(function() {
        //遍历所有的li
        //修改每个li内的字体颜色
        $("li").each(function(index, element) {
            $(this).css('color','red')
        })

    })
    $("button:last").click(function() {
        //遍历所有的li
        //修改偶数li内的字体颜色
        $("li").each(function(index, element) {
            if (index % 2) {
                $(this).css('color','blue')
            }
        })
    })
  ```
 
 ##JQuery  AJAX
 >$("#div1").load("demo_test.txt");  把文件 "demo_test.txt" 的内容加载到指定的 <div> 元素中：
 > $("#div1").load("/example/jquery/demo_test.txt #p1");     把 "demo_test.txt" 文件中 id="p1" 的元素的内容，加载到指定的 <div> 元素中：

jQuery get() 和 post() 方法用于通过 HTTP GET 或 POST 请求从服务器请求数据。

    GET - 从指定的资源请求数据
    POST - 向指定的资源提交要处理的数据

GET 基本上用于从服务器获得（取回）数据。注释：GET 方法可能返回缓存数据。
POST 也可用于从服务器获取数据。不过，POST 方法不会缓存数据，并且常用于连同请求一起发送数据。

GET语法：

$.get(URL,callback);

必需的 URL 参数规定您希望请求的 URL。

可选的 callback 参数是请求成功后所执行的函数名。

$.get() 方法从服务器上的一个文件中取回数据：
 ```javascript
$(document).ready(function(){
  $("button").click(function(){
    $.get("/example/jquery/demo_test.asp",function(data,status){
      alert("数据：" + data + "\n状态：" + status);
    });
  });
});
```
>这段代码是向页面发送 HTTP GET 请求，然后获得返回的结果

POST语法：

$.post(URL,data,callback);

必需的 URL 参数规定您希望请求的 URL。

可选的 data 参数规定连同请求发送的数据。

可选的 callback 参数是请求成功后所执行的函数名。
```javascript
$(document).ready(function(){
  $("button").click(function(){
    $.post("/example/jquery/demo_test_post.asp",
    {
      name:"Donald Duck",
      city:"Duckburg"
    },
    function(data,status){
      alert("数据：" + data + "\n状态：" + status);
    });
  });
});
```
>向页面发送 HTTP POST 请求，并获得返回的结果
```javascript
$.noConflict();
jQuery(document).ready(function(){
  jQuery("button").click(function(){
    jQuery("p").text("jQuery 仍在运行！");
  });
});
```
>noConflict() 方法会释放会 $ 标识符的控制，这样其他脚本就可以使用它了
##选择器
$(".div:first") 找到第一个div
$(".div:last")  找到最后一个div
$(".div:even")  :even 选择所引值为偶数的元素，从 0 开始计数
$(".div:odd"):odd 选择所引值为奇数的元素，从 0 开始计数
$(".aaron:eq(2)")  选择单个
$(".aaron:gt(3)")  :gt 选择匹配集合中所有索引值大于给定index参数的元素
$(".aaron:lt(2)") :lt 选择匹配集合中所有索引值小于给定index参数的元素  与:gt相反
 $("input:not(:checked) + p")   选中所有紧接着没有checked属性的input元素后的p元素，赋予颜色
 #内容筛选选择器
 ![img](../jQuery/images/4.jpg)
 :contains与:has都有查找的意思，但是contains查找包含“指定文本”的元素，has查找包含“指定元素”的元素

 		查找所有class='div'中DOM元素中包含"contains"的元素节点
        //并且设置颜色
        $(".div:contains(':contains')").css("color", "#CD00CD");

        //查找所有class='div'中DOM元素中包含"span"的元素节点
        //并且设置颜色
        $(".div:has(span)").css("color", "blue");

       //选择所有包含子元素或者文本的a元素
       //增加一个蓝色的边框
       $("a:parent").css("border", "3px groove blue");



       //找到a元素下面的所有空节点(没有子元素)
       //增加一段文本与边框
       $("a:empty").text(":empty").css("border", "3px groove red"); 

![](../jQuery/images/5.jpg)
![](../jQuery/images/1.jpg)
###子元素筛选选择器
![](../jQuery/images/2.jpg)
###表单元素选择器
![](../jQuery/images/3.jpg)

###this加工成jQuery对象
>this，表示当前的上下文对象是一个html对象，可以调用html对象所拥有的属性和方法。
>$(this),代表的上下文对象是一个jquery的上下文对象，可以调用jQuery的方法和属性值。
```javascript
$('#test2').click(function(){
            //通过包装成jQuery对象改变颜色
            $(this).css('color','blue')
})；
```
##元素的数据存储
```javascript  
$('.left').click(function() {
        var ele = $(this);
        //通过$.data方式设置数据
        $.data(ele, "a", "data test")
        $.data(ele, "b", {
            name : "慕课网"
        })
        //通过$.data方式取出数据
        var reset = $.data(ele, "a") + "</br>" + $.data(ele, "b").name;
        ele.find('span').append(reset);
    })
```
