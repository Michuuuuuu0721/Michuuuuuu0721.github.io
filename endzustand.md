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
            font-family: 'Determination';
            src: url('./fonts/DeterminationMonoWebRegular-Z5oq.ttf') format('truetype'); 
        }
        html, body {
            margin: 0 !important;
            padding: 0 !important;
            background-color: black !important;
            width: 100% !important;
            height: 100vh !important;
            overflow: hidden !important;
            box-sizing: border-box;
        }
        .text-container {
            width: 100%;
            height: 100%;
            display: flex !important;
            flex-direction: column !important; 
            justify-content: center !important;
            align-items: center !important;
        }
        .text-row {
            display: block !important;
            width: 100%;
            text-align: center !important;
            font-size: 14px !important;
            font-family: 'Determination', sans-serif !important;
            letter-spacing: 1px !important;
            box-sizing: border-box;
        }
        .visible-text {
            color: white;
        }
        .hidden-text {
            color: black;
            user-select: text;
        }
        .hidden-text::selection {
            background: white;
            color: black;
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
