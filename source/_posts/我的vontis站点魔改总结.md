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
cover: https://images.boysec.cn/cover1.webp
mathjax: true
katex: true
type: post
description: 我的vontis站点魔改总结
abbrlink: 13229
date: 2023-06-28 20:05:10
swiper_index: 8 #置顶轮播图顺序，需填非负整数，数字越大越靠前
top_group_index: 8 #右侧磁帖顺序，需填非负整数，数字越大越靠前
---
## 前言
{% note red 'fas fa-fan' flat%}温馨提示：在修改源码时注意做好备份处理{% endnote %}

### 暗黑模式动画(通用)
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
```DarkMode.css
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
