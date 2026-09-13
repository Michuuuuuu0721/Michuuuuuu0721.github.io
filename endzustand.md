---
layout: null
permalink: /endzustand/
---
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Endzustand</title>
    <style>
        @font-face {
            font-family: 'Determination';     /* 给你的字体起个名字 */
            src: url('./f   onts/DeterminationMonoWebRegular-Z5oq.ttf') format('truetype'); /* 字体文件的相对路径 */
            /* 如果是 .otf 文件，将上面一行改为： format('opentype') */
            /* 如果是 .woff2 文件，将上面一行改为： format('woff2') */
        }
        /* 移除浏览器默认边距，让背景全黑 */
        body {
            margin: 0;
            background-color: black;
            height: 100vh;
            display: flex;
            justify-content: center; /* 水平居中 */
            align-items: center;     /* 垂直居中 */
            overflow: hidden;        /* 禁止滚动条 */
        }
                /* 基础文字样式（两行共有） */
        .text-line {
            font-size: 14px;
            font-family: 'Determination', sans-serif;
            letter-spacing: 1px;
            line-height: 1.8;        /* 调整两行字之间的行高间距 */
            text-align: center;
        }
        /* 第一行：显示的白色小字 */
        .visible-text {
            color: white;
        }
        /* 第二行：隐藏的黑色小字 */
        .hidden-text {
            color: black;
            user-select: text;       /* 确保用户可以正常划选这段字 */
        }
        /* 可选：如果你希望用户鼠标划选时，高亮颜色也更特别（比如黑底白字反过来），可以保留以下代码 */
        .hidden-text::selection {
            background: white;       /* 划选时的背景色变为白色 */
            color: black;            /* 划选时的文字颜色变为黑色 */
        }
    </style>
</head>
<body>
    <!-- 第一行：正常可见的字 -->
    <div class="text-line visible-text">"NICE TRY."</div>
    <!-- 第二行：藏起来的黑色字（鼠标刮开涂白可见） -->
    <div class="text-line hidden-text">熱_の法_は_系の乱_である_増える事_の理かな</div>

</body>
</html>
