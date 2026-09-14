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
            src: url('./fonts/DeterminationMonoWebRegular-Z5oq.ttf') format('truetype'); /* 字体文件的相对路径 */
            /* 如果是 .otf 文件，将上面一行改为： format('opentype') */
            /* 如果是 .woff2 文件，将上面一行改为： format('woff2') */
        }
        /* 移除浏览器默认边距，让背景全黑 */
        html, body {
            margin: 0 !important;
            padding: 0 !important;
            background-color: black !important;
            width: 100% !important;
            height: 100vh !important;
            overflow: hidden !important;
            box-sizing: border-box;
        }
                /* 基础文字样式（两行共有） */
        .text-container {
            width: 100%;
            height: 100%;
            display: flex !important;
            flex-direction: column !important; /* 强制上下排列 */
            justify-content: center !important;/* 垂直居中 */
            align-items: center !important;    /* 水平居中 */
        }
        /* 每行文字的独立行容器（强制独占一行） */
        .text-row {
            display: block !important;         /* 块级元素强制换行 */
            width: 100%;                       /* 撑满宽度确保独占一行 */
            text-align: center !important;     /* 文字在行内居中 */
            font-size: 14px !important;
            font-family: 'Determination', sans-serif !important;
            letter-spacing: 1px !important;
            box-sizing: border-box;
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
    <div class="text-container">
        <div class="text-line visible-text">"NICE TRY."</div>
        <div class="text-line hidden-text">熱_の法_は_系の乱_である_増える事_の理かな</div>
    </div>
</body>
</html>
