---
title: 我的vontis站点魔改总结
categories:
  - volantis
  - 魔改
  - 教程
tags: 
  - volantis
  - themes
  - 魔改
cover: 
mathjax: true
katex: true
type: post
description: 我的vontis站点魔改总结
abbrlink: 13229
date: 2023-06-28 20:05:10
swiper_index: 8 #置顶轮播图顺序，需填非负整数，数字越大越靠前
---
## 前言
{% note red 'fas fa-fan' flat%}温馨提示：在修改源码时注意做好备份处理{% endnote %}

### 魔改前需加入的文件
#### 1.如果报错 $ is not defined,或其他有关 $ 的错误,很可能是因为你没有jQuery或者jQuery异常,需要自行引用.注意jQuery必须在目标代码之前,最好是第一个引用
```
<script src="https://unpkg.com/jquery@3.6.0/dist/jquery.min.js"></script>
```

### 一.暗黑模式动画
#### 1.添加DarkMode.js
```DarkMode.js
function BackTOP() {
    $("#btn").hide();
    $(function () {
        $(window).scroll(function () {
            if ($(window).scrollTop() > 50) {
                $("#btn").fadeIn(200);
            } else {
                $("#btn").fadeOut(200);
            }
        });
        $("#btn").click(function () {
            $('body,html').animate({
                    scrollTop: 0
                },
                500);
            return false;
        });
    });
    $(function () {
        $("#say").click(function () {
            $('body,html').animate({
                    scrollTop: $('html, body').get(0).scrollHeight
                },
                500);
            return false;
        });
    })
}

$('#readmode').click(function () {
        $('body').toggleClass('read-mode')
    })
    
function SiderMenu() {
    $('#main-container').toggleClass('open');
    $('.iconflat').css('width', '50px').css('height', '50px');
    $('.openNav').css('height', '50px');
    $('#main-container,#mo-nav,.openNav').toggleClass('open')
}

function switchNightMode() {
    $('<div class="Cuteen_DarkSky"><div class="Cuteen_DarkPlanet"></div></div>').appendTo($("body")), setTimeout(
        function () {
            (volantis.dark.mode == "dark") 
            ? 
            ($("html").addClass("DarkMode"),
            $('#modeicon').attr("xlink:href", "#icon-sun")) 
            : 
            ($("html").removeClass("DarkMode"),
            $('#modeicon').attr("xlink:href", "#icon-_moon")), 
            setTimeout(function () {
                $(".Cuteen_DarkSky").fadeOut(1e3, function () {
                    $(this).remove()
                })
            }, 2e3)
        }), 50
}

function checkNightMode() {
    if ($("html").hasClass("n-f")) {
        $("html").removeClass("day");
        $("html").addClass("DarkMode");
        $('#modeicon').attr("xlink:href", "#icon-sun")
        return;
    }
    if ($("html").hasClass("d-f")) {
        $("html").removeClass("DarkMode");
        $("html").addClass("day");
        $('#modeicon').attr("xlink:href", "#icon-_moon")
        return;
    }
    if (volantis.dark.mode == "dark") {
        $("html").addClass("DarkMode");
        $('#modeicon').attr("xlink:href", "#icon-sun")
    } else {
        $("html").removeClass("DarkMode");
        $('#modeicon').attr("xlink:href", "#icon-_moon")
    }
}
BackTOP();
volantis.dark.push(switchNightMode);
```
#### 2.添加DarkMode.css
```
#RightDownBtn {
    position: fixed;
    left: 1.875rem;
    bottom: 1.875rem;
    padding: 0.3125rem 0.625rem;
    background: #fff;
    border-radius: 0.1875rem;
    transition: 0.3s ease all;
    z-index: 1;
    align-items: flex-end;
    flex-direction: column;
    display: -moz-flex;
    display: flex;
    float: right;
}

#RightDownBtn>a,
#RightDownBtn>label {
    width: 1.5em;
    height: 1.5em;
    margin: 0.3125rem 0;
    transition: .2s cubic-bezier(.25, .46, .45, .94);
}

/* font color */
.DarkMode #page,
.DarkMode #colophon,
.DarkMode #vcomments .vbtn,
.DarkMode .art-content #archives .al_mon_list .al_mon,
.DarkMode .art-content #archives .al_mon_list span,
.DarkMode body,
.DarkMode .art-content #archives .al_mon_list .al_mon,
.DarkMode .art-content #archives .al_mon_list span,
.DarkMode button,
.DarkMode .art .art-content #archives a,
.DarkMode textarea,
.DarkMode strong,
.DarkMode a,
.DarkMode p,
.DarkMode li,
.DarkMode .label {
    color: rgba(255, 255, 255, .6);
}


.DarkMode #page,
.DarkMode body,
.DarkMode #colophon,
.DarkMode #main-container,
.DarkMode #page .yya,
.DarkMode #content,
.DarkMode #contentss,
.DarkMode #footer {
    background-color: #292a2d;
}
.DarkMode strong,
.DarkMode img {
    filter: brightness(.7);
}

/* sun and noon */
.Cuteen_DarkSky,
.Cuteen_DarkSky:before {
    content: "";
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: 88888888
}

.Cuteen_DarkSky {
    background: linear-gradient(#feb8b0, #fef9db)
}

.Cuteen_DarkSky:before {
    transition: 2s ease all;
    opacity: 0;
    background: linear-gradient(#4c3f6d, #6c62bb, #93b1ed)
}

.DarkMode .Cuteen_DarkSky:before {
    opacity: 1
}

.Cuteen_DarkPlanet {
    z-index: 99999999;
    position: fixed;
    left: -50%;
    top: -50%;
    width: 200%;
    height: 200%;
    -webkit-animation: CuteenPlanetMove 2s cubic-bezier(.7, 0, 0, 1);
    animation: CuteenPlanetMove 2s cubic-bezier(.7, 0, 0, 1);
    transform-origin: center bottom
}

@-webkit-keyframes CuteenPlanetMove {
    0% {
        transform: rotate(0)
    }

    to {
        transform: rotate(360deg)
    }
}

@keyframes CuteenPlanetMove {
    0% {
        transform: rotate(0)
    }

    to {
        transform: rotate(360deg)
    }
}

.Cuteen_DarkPlanet:after {
    position: absolute;
    left: 35%;
    top: 40%;
    width: 9.375rem;
    height: 9.375rem;
    border-radius: 50%;
    content: "";
    background: linear-gradient(#fefefe, #fffbe8)
}
```

### 二.首页动态诗词
#### 1.在volantis的配置文件里修改 subtitle 为"<div id="binft"></div>"
```
############################### Cover ############################### > start
cover:
  ...
  subtitle: <div id="binft"></div>
  ...
```
#### 2.以defer方式引入以下js,注意把里面的诗词改成自己的
```
var binft = function (r) {
    var isTransparent = true;
    function getRandomColor() {
        if(isTransparent){
            isTransparent = false;
            //此处修改字体颜色,最后的 0 和 1 不要改
            return "rgba(255,255,255,0)"
        }else{
            isTransparent = true;
            return "rgba(255,255,255,1)"
        }
    }  
    function n(r) {
        for (var n = document.createDocumentFragment(), i = 0; r > i; i++) {
            var oneword = document.createElement("span");
            oneword.textContent = "_"; // 此处是末尾字符,如果想用光标样式可以改为"|"
            oneword.style.color = getRandomColor();
            n.appendChild(oneword);
        }
        return n
    }
    function i() {
        var t = wordList[c.skillI];
        c.step ? c.step-- : (c.step = refreshDelayTime, c.prefixP < l.length ? (c.prefixP >= 0 && (c.text += l[c.prefixP]), c.prefixP++) : "forward" === c.direction ? c.skillP < t.length ? (c.text += t[c.skillP], c.skillP++) : c.delay ? c.delay-- : (c.direction = "backward", c.delay = showTotalWordDelayTime) : c.skillP > 0 ? (c.text = c.text.slice(0, -1), c.skillP--) : (c.skillI = (c.skillI + 1) % wordList.length, c.direction = "forward")), r.textContent = c.text, r.appendChild(n(c.prefixP < l.length ? Math.min(maxLength, maxLength + c.prefixP) : Math.min(maxLength, t.length - c.skillP))), setTimeout(i, d)
    }
    var l = "",
    //此处改成你自己的诗词
    wordList = [ 
            "有花堪折直需折,莫待无花空折枝.",
            "闲居少邻并,草径入荒园.鸟宿池边树,僧敲月下门.",
            "侯门一入深如海,从此萧郎是路人.",
            "才见岭头云似盖,已惊岩下雪如尘.",
            "人间万事消磨尽,只有清香似旧时.",
            "日暮酒醒人已远,满天风雨下西楼.",
            "落灯花,棋未收,叹新丰逆旅淹留.",
            "软风吹过窗纱,心期便隔天涯.",
            "迷惑失故路,薄暮无宿栖.",
            "不见白头相携老,只许与君共天明.",
            "晓迎秋露一枝新,不占园中最上春.",
            "荷尽已无擎雨盖,菊残犹有傲霜枝.",
            "春未绿,鬓先丝.人间别久不成悲.",
            "江东子弟多才俊,卷土重来未可知.",
            "莫听穿林打叶声,何妨吟啸且徐行.",
            "在天愿作比翼鸟,在地愿为连理枝.",
        ].map(function (r) {
    return r + ""
    }),
    showTotalWordDelayTime = 2,
    refreshDelayTime = 1,
    maxLength = 1,
    d = 75,
    c = {
        text: "",
        prefixP: -maxLength,
        skillI: 0,
        skillP: 0,
        direction: "forward",
        delay: showTotalWordDelayTime,
        step: refreshDelayTime
    };
    i()
};
binft(document.getElementById('binft'));
```

### 三."Hello World"特效
#### 1.修改主题配置文件里的标题
```
############################### Cover ############################### > start
cover:
  ...
  title: '<font><span>Hello</span> <span>World</span></font>'
  ...
```
#### 2.引入以下css样式,推荐添加到 hexo/source/_volantis/style.styl 里
```
/* 此处调节字体大小
.top .title font{
    font-size: 1em;
}
*/
.top .title span{
    transition: 0.5s;
}
.top .title:hover span:nth-child(1){
    margin-right: 10px;
}
.top .title:hover span:nth-child(2){
    margin-left: 10px;
}
.top .title:hover span{
    color: #fff;
    text-shadow: 0 0 10px #fff,
                 0 0 20px #fff,
                 0 0 40px #fff,
                 0 0 80px #fff,
                 0 0 120px #fff,
                 0 0 160px #fff;
}
```
