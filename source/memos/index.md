---
title: memos
top_img: false
comments: true
aside: false
type: page
date: 2021-03-14 20:00:00
---
<div class="page-top-card" style="background-image: url(https://memos.wyblog1.tk/o/r/5/zongbg.webp);">    
    <div class="content-item-tips">动态</div>
    <span class="content-item-title">空间说说</span>
    <div class="content-bottom">
        <div class="tips">我的生活、吐槽、闲话...</div>
        <a class="banner-button" onclick="pjax.loadUrl('/photos/')" data-pjax-state="">
            <i class="fa-solid fa-image"></i><span>生活相册</span>
        </a>
    </div>
</div>

<style>
@media screen and (max-width: 900px)
a.banner-button {
    width: 50px;
    height: 35px;
    display: flex;
    align-items: center;
    justify-content: center;
}
a.banner-button {
    cursor: pointer;
    color: #fff!important;
    backdrop-filter: saturate(180%) blur(20px);
    background: rgb(120 120 120 / 30%);
    padding: 5px 15px;
    border-radius: 100px;
    text-decoration: none!important;
}
a:hover {
    color: #4976f5;
}
@media screen and (max-width: 900px)
.page-top-card {
    padding: 10px 1rem;
    height: 12rem;
}
div#page {
    background: #39c5bb;
}
.page-title{
    display: none;
}
[data-theme=dark] #twikoo .tk-content,
#twikoo .tk-content {
    padding: 0;
    background: transparent;
}

.talk_item,
.tk-expand,
.tk-comments-container>.tk-comment,
.tk-submit:nth-child(1){
    background: var(--card-bg);
    border: var(--leonus-border);
    transition: all .3s ease-in-out;
    border-radius: 12px;
}
.talk_item:hover,
.tk-comments-container>.tk-comment:hover,
.tk-submit:nth-child(1):hover {
    border-color: var(--leonus-purple);
}

.tk-submit {
    padding: 20px 10px 0;
}

.tk-comments-container>.tk-comment {
    padding: 15px;
}

.page-top-card {
    background-color: #666;
    margin-bottom:  12px
}
/* 页面初始化结束 */

#talk .loading {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

#talk .loading img {
    width: 200px;
}

.talk_item {
    display: inline-block;
    width: 32%;
    margin-right: 1%;
    padding: 15px 1rem 12px;
    margin-bottom: 15px;
}

.avatar {
    margin: 0 !important;
    width: 50px;
    height: 50px;
    border-radius: 10px;
}

.talk_meta {
    display: flex;
    align-items: center;
    width: 100%;
    line-height: 1.5;
}

.talk_meta .info {
    display: flex;
    flex-direction: column;
    margin-left: 10px;
}

span.talk_nick {
    color: #6dbdc3;
    font-size: 1.2rem;
}

span.talk_date {
    font-size: 14px;
    opacity: .6;
}

.talk_content {
    line-height: 1.5;
    margin-top: 10px;
}

.zone_imgbox {
    display: flex;
    flex-wrap: wrap;
    --w: 177px;
    gap: 10px;
    margin-top: 5px;
}

.zone_imgbox a {
    display: block;
    width: var(--w);
    max-height: var(--w);
    position: relative;
}

.zone_imgbox img {
    border-radius: 5px !important;
    width: 100%;
    height: 100%;
    margin: 0 !important;
    object-fit: cover;
}

/* 提醒 */

.limit {
    transition: all .3s ease-in-out;
    color: rgba(76, 73, 72, 0.6);
}

[data-theme=dark] .limit {
    color: rgba(255, 255, 255, 0.5);
}

.limit {
    display: none;
    text-align: center;
    margin-top: 20px;
    color: var(--font-color);
}

@media screen and (max-width: 1250px) {
    .zone_imgbox {
        --w: 120px;
    }
}


@media screen and (max-width: 1100px) {
    .talk_item {
        width: 100%;
        margin-right: 1.4%;
    }

    .zone_imgbox {
        --w: 150px;
        gap: 6px;
    }
}

@media screen and (max-width: 768px) {
    .talk_item {
        width: 100%;
        margin-right: 0;
    }

    span.talk_date {
        font-size: 14px;
    }
}


@media screen and (max-width: 900px)
.page-top-card {
    padding: 10px 1rem;
    height: 12rem;
}
.page-top-card {
    background-size: cover;
    background-position: center;
    height: 20rem;
    padding: 10px 2.7rem;
    border-radius: 20px;
    color: #fff;
    position: relative;
}
span.content-item-title {
    font-size: 2.3em;
    font-weight: 700;
    line-height: 1.2;
}
.content-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: absolute;
    width: calc(100% - 5.4rem);
    bottom: 1rem;
}
</style>


<div id="talk">
<div class='loading'><img src="/img/loading.svg" alt="加载中..."></div>
</div>

<div class="limit">- 只展示最近100条说说 -</div>
<script>
pageTalk();
// 页面说说
function pageTalk() {
    fetch('https://memos.wyblog1.tk/api/memo?creatorId=1&tag=说说&limit=100').then(res => res.json()).then(data => { // 注意修改域名和用户id
        let items = [],
            html = '',
            icon = '<svg viewBox="0 0 512 512"xmlns="http://www.w3.org/2000/svg"class="is-badge icon"><path d="m512 268c0 17.9-4.3 34.5-12.9 49.7s-20.1 27.1-34.6 35.4c.4 2.7.6 6.9.6 12.6 0 27.1-9.1 50.1-27.1 69.1-18.1 19.1-39.9 28.6-65.4 28.6-11.4 0-22.3-2.1-32.6-6.3-8 16.4-19.5 29.6-34.6 39.7-15 10.2-31.5 15.2-49.4 15.2-18.3 0-34.9-4.9-49.7-14.9-14.9-9.9-26.3-23.2-34.3-40-10.3 4.2-21.1 6.3-32.6 6.3-25.5 0-47.4-9.5-65.7-28.6-18.3-19-27.4-42.1-27.4-69.1 0-3 .4-7.2 1.1-12.6-14.5-8.4-26-20.2-34.6-35.4-8.5-15.2-12.8-31.8-12.8-49.7 0-19 4.8-36.5 14.3-52.3s22.3-27.5 38.3-35.1c-4.2-11.4-6.3-22.9-6.3-34.3 0-27 9.1-50.1 27.4-69.1s40.2-28.6 65.7-28.6c11.4 0 22.3 2.1 32.6 6.3 8-16.4 19.5-29.6 34.6-39.7 15-10.1 31.5-15.2 49.4-15.2s34.4 5.1 49.4 15.1c15 10.1 26.6 23.3 34.6 39.7 10.3-4.2 21.1-6.3 32.6-6.3 25.5 0 47.3 9.5 65.4 28.6s27.1 42.1 27.1 69.1c0 12.6-1.9 24-5.7 34.3 16 7.6 28.8 19.3 38.3 35.1 9.5 15.9 14.3 33.4 14.3 52.4zm-266.9 77.1 105.7-158.3c2.7-4.2 3.5-8.8 2.6-13.7-1-4.9-3.5-8.8-7.7-11.4-4.2-2.7-8.8-3.6-13.7-2.9-5 .8-9 3.2-12 7.4l-93.1 140-42.9-42.8c-3.8-3.8-8.2-5.6-13.1-5.4-5 .2-9.3 2-13.1 5.4-3.4 3.4-5.1 7.7-5.1 12.9 0 5.1 1.7 9.4 5.1 12.9l58.9 58.9 2.9 2.3c3.4 2.3 6.9 3.4 10.3 3.4 6.7-.1 11.8-2.9 15.2-8.7z"fill="#1da1f2"></path></svg>';
        data.data.forEach(item => { items.push(Format(item)) });
        if (items.length == 30) document.querySelector('.limit').style.display = 'block';
        items.forEach(item => {
            html += `<div class="talk_item"><div class="talk_meta"><img class="no-lightbox avatar" src="https://q1.qlogo.cn/g?b=qq&nk=990320751&s=5"><div class="info"><span class="talk_nick">Leonus${icon}</span><span class="talk_date">${item.date}</span></div></div><div class="talk_content">${item.content}</div><div class="talk_bottom"><div><span class="talk_tag"></span></div><a href="javascript:;"onclick="goComment('${item.text}')"><span class="icon"><i class="fa-solid fa-message fa-fw"></i></span></a></div></div>` // 注意修改头像链接和名称
        })
        document.getElementById('talk').innerHTML = html
    })
}
// 页面评论
function goComment(e) {
    var n = document.querySelector(".el-textarea__inner")
    n.value = `> ${e}\n\n`;
    n.focus();
    btf.snackbarShow("无需删除空行，直接输入评论即可", !1, 2e3);
}
// 页面内容格式化
function Format(item) {
    let date = getTime(new Date(item.createdTs * 1000).toString()),
        content = item.content,
        tag = item.content.match(/\{(.*?)\}/g),
        imgls = content.match(/!\[.*\]\(.*?\)/g), // 2023-02-06更新
        text = ''
    text = content.replace(/#(.*?)\s/g, '').replace(/\!\[(.*?)\]\((.*?)\)/g, '').replace(/\{(.*?)\}/g, '')
    content = text.replace(/\[(.*?)\]\((.*?)\)/g, `<a href="$2">@$1</a>`);
    if (imgls) {
        content += `<div class="zone_imgbox">`
        imgls.map(item => { return item.replace(/!\[.*\]\((.*?)\)/, '$1') }).forEach(e => content += `<a href="${e}" data-fancybox="gallery" class="fancybox" data-thumb="${e}"><img src="${e}"></a>` // 2023-02-06更新
        )
        content += '</div>'
    }
    return {
        content: content,
        tag: tag ? tag[0].replace(/\{(.*?)\}/,'$1') : '无标签',
        date: date,
        text: text.replace(/\[(.*?)\]\((.*?)\)/g, '[链接]' + `${imgls?'[图片]':''}`)
    }
}
// 页面时间格式化
function getTime(time) {
    let d = new Date(time),
        ls = [d.getFullYear(), d.getMonth() + 1, d.getDate(), d.getHours(), d.getMinutes(), d.getSeconds()];
    for (let i = 0; i < ls.length; i++) {
        ls[i] = ls[i] <= 9 ? '0' + ls[i] : ls[i] + ''
    }
    if (new Date().getFullYear() == ls[0]) return ls[1] + '月' + ls[2] + '日 ' + ls[3] +':'+ ls[4]
    else return ls[0] + '年' + ls[1] + '月' + ls[2] + '日 ' + ls[3] +':'+ ls[4]
}
</script>
