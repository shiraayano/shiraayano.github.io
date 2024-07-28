一键抄作业，将以下代码复制进alist自定义头部即可

```css
<style>
html, body {
    /* 设置页面背景图片，并使其固定在中心位置，不随滚动条移动 */
    background: url('https://api.adou-web.eu.org/?id=background_mobile') no-repeat center center fixed;
    /* 背景图片覆盖整个视窗 */
    background-size: cover;
    /* 设置全局字体颜色 */
    color: #333;
    /* 设置全局行高 */
    line-height: 1.6;
    /* 设置全局字体 */
    font-family: 'LXGW WenKai', sans-serif;
    /* 设置全局字体加粗 */
    font-weight: bold;
    /* 添加背景过渡效果 */
    transition: background 0.3s ease;
}

/* 响应式设计 - 手机尺寸 */
@media screen and (min-width: 320px) and (max-width: 767px) {
    html, body {
        /* 设置手机尺寸下的背景图片 */
        background: url('https://api.adou-web.eu.org/?id=background_mobile') no-repeat center center fixed;
    }
}

/* 响应式设计 - 平板尺寸 */
@media screen and (min-width: 768px) and (max-width: 1024px) {
    html, body {
        /* 设置平板尺寸下的背景图片 */
        background: url('https://api.adou-web.eu.org/?id=background_tablet') no-repeat center center fixed;
    }
}

/* 响应式设计 - 大屏幕设备尺寸 */
@media screen and (min-width: 1025px) {
    html, body {
        /* 设置大屏幕尺寸下的背景图片 */
        background: url('https://api.adouzi.eu.org/?id=background_pc') no-repeat center center fixed;
    }
}

/* 设置透明度和背景颜色 */
.obj-box, .hope-c-PJLV {
    /* 设置元素背景颜色及透明度 */
    background-color: rgba(0, 0, 0, 0.1) !important;
    /* 设置元素圆角 */
    border-radius: 6px;
    /* 添加背景颜色过渡效果 */
    transition: background-color 0.3s ease;
}

.obj-box:hover, .hope-c-PJLV:hover {
    /* 设置元素悬停时的背景颜色及透明度 */
    background-color: rgba(0, 0, 0, 0.3) !important;
}

/* 白天模式下的样式 */
.hope-ui-light .obj-box, .hope-ui-light .hope-c-PJLV {
    /* 设置白天模式下元素的背景颜色及透明度 */
    background-color: rgba(255, 255, 255, 0.1) !important;
}

.hope-ui-light .obj-box:hover, .hope-ui-light .hope-c-PJLV:hover {
    /* 设置白天模式下元素悬停时的背景颜色及透明度 */
    background-color: rgba(255, 255, 255, 0.3) !important;
}

/* 代码块的样式 */
.hope-ui-light pre, .hope-ui-dark pre {
    /* 设置代码块的背景颜色及透明度 */
    background-color: rgba(255, 255, 255, 0.3) !important;
    /* 设置代码块的圆角 */
    border-radius: 6px;
}

/* 顶部右上角切换按钮及右下角侧边栏按钮的样式 */
.hope-icon-button, .hope-c-PJLV-ijgzmFG-css {
    /* 设置按钮的背景颜色及透明度 */
    background-color: rgba(255, 255, 255, 0.1) !important;
    /* 设置按钮的圆角 */
    border-radius: 6px;
    /* 添加背景颜色过渡效果 */
    transition: background-color 0.3s ease;
}

.hope-icon-button:hover, .hope-c-PJLV-ijgzmFG-css:hover {
    /* 设置按钮悬停时的背景颜色及透明度 */
    background-color: rgba(255, 255, 255, 0.3) !important;
}

/* 评论系统的样式 */
.newValine {
    /* 设置评论区宽度 */
    width: min(96%, 940px);
    /* 设置评论区的方向为纵向 */
    flex-direction: column;
    /* 设置评论区行间距 */
    row-gap: var(--hope-space-2);
    /* 设置评论区圆角 */
    border-radius: var(--hope-radii-xl);
    /* 设置评论区内边距 */
    padding: var(--hope-space-2);
    /* 设置评论区阴影 */
    box-shadow: var(--hope-shadows-lg);
    /* 添加背景颜色过渡效果 */
    transition: background-color 0.3s ease;
}

/* 白天模式下的评论区样式 */
.hope-ui-light .newValine {
    /* 设置白天模式下评论区的背景颜色及透明度 */
    background-color: rgba(255, 255, 255, 0.1) !important;
}

/* 夜间模式下的评论区样式 */
.hope-ui-dark .newValine {
    /* 设置夜间模式下评论区的背景颜色及透明度 */
    background-color: rgba(0, 0, 0, 0.1) !important;
}

/* 输入栏背景图样式 */
.vedit {
    /* 设置输入栏背景图片 */
    background-image: url(https://cdn.jsdelivr.net/gh/anwen-anyi/imgAnwen/images/OuNiJiang.gif);
    /* 设置背景图片的大小 */
    background-size: contain;
    /* 设置背景图片不重复 */
    background-repeat: no-repeat;
    /* 设置背景图片的位置 */
    background-position: right bottom;
    /* 添加过渡效果 */
    transition: all 0.25s ease-in-out 0s;
}

textarea#comment-textarea:focus {
    /* 设置输入框获得焦点时背景图片的位置 */
    background-position-y: 120px;
    /* 添加过渡效果 */
    transition: all 0.25s ease-in-out 0s;
}

/* 底部样式 */
.dibu {
    /* 设置底部边框 */
    border-top: 0;
    /* 设置底部位置 */
    position: absolute;
    bottom: 0;
    /* 设置底部宽度 */
    width: 100%;
    /* 设置底部外边距 */
    margin: 0;
    /* 设置底部内边距 */
    padding: 0;
}

/* App区域样式 */
.App {
    /* 设置App区域最小高度 */
    min-height: 85vh;
}

/* 表格样式 */
.table {
    /* 设置表格居中 */
    margin: auto;
}

/* 渐变背景样式 */
#canvas-basic {
    /* 设置渐变背景的固定位置 */
    position: fixed;
    /* 设置渐变背景的显示属性 */
    display: block;
    /* 设置渐变背景的宽度 */
    width: 100%;
    /* 设置渐变背景的高度 */
    height: 100%;
    /* 设置渐变背景的上下左右位置 */
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    /* 设置渐变背景的层叠顺序 */
    z-index: -999;
}
</style>

```

注释是GPT写的，真方便（