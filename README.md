# BySelect
DIY my select style

## html code
```
<ul class="select">
    <li>
        点击选择
    </li>
    <b></b>
</ul>
<ul class="option">
    <li>选项一</li>
    <li>选项二</li>
    <li>选项三</li>
    <li>选项四</li>
    <li>选项五</li>
</ul>
```
+ select类名可以自定义
+ option类名必须

## css code
```
li {
            list-style: none;
            width: 200px;
            height: 30px;
            border: 1px solid skyblue;
            text-align: center;
            line-height: 30px;
            cursor: pointer;
            user-select: none;
            -webkit-user-select: none;
        }
        .select {
            display: inline-block;
            position: relative;
        }
        .option > li {
            display: none;
        }

        b {
            position: absolute;
            top: 5px;
            right: 10px;
            display: inline-block;
            width: 0;
            height: 0;
            border-width: 10px 10px 10px 10px;
            border-style: solid solid solid solid;
            border-color: transparent transparent transparent #bbb;
        }
        .option .show {
            display: block;
        }
```
+ 样式可以完全自己定义
+ b标签是控制小三角的

## 实现
```
(function (window) {
    $.fn.extend({
        BySelect: function () {
            var that = this;
            $(that).click(function () {

                $(".option > li").toggleClass("show");
                if($(".option > li").hasClass("show")) {
                    $("b").css({
                        "borderColor":"#bbb transparent transparent transparent",
                        "top": "10px"
                    })
                }else {
                    $("b").css({
                        "borderColor": "transparent transparent transparent #bbb",
                        "top": "5px"
                    })
                }
            });
            $(".option > li").click(function () {
                $(that).find("li").html($(this).html());
                $(".option > li").toggleClass("show");
                $("b").css({
                    "borderColor": "transparent transparent transparent #bbb",
                    "top": "5px"
                })
            });
            $(".option > li").mouseover(function () {
                $(this).siblings("li").css("backgroundColor", "white").end().css("backgroundColor", "#f3f3f3")
            });
        }
    })
})(window)
```
+ 鼠标移入样式写死了，自定义可以修改`$(this).siblings("li").css("backgroundColor", "white").end().css("backgroundColor", "#f3f3f3")`该处的颜色
+ 只实现了一些基础的样式，可以和方便的进行二次修改
