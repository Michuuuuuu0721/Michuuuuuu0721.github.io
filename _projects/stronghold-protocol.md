---
title: "卫戍协议：盟约"
date: 2026-10-11
layout: null
permalink: /stronghold-protocol/
---
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>卫戍协议：盟约 · 神经连接中</title>
    <style>
        /* 1. 锁死纯黑美学背景，防止任何溢出滚动条 */
        html, body {
            margin: 0 !important;
            padding: 0 !important;
            background-color: black !important;
            color: #c3cbc7 !important;
            width: 100% !important;
            height: 100vh !important;
            overflow: hidden !important;
            font-family: sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            box-sizing: border-box;
        }

        /* 2. 居中容器 */
        .terminal-box {
            text-align: center;
            max-width: 90%;
        }

        /* 3. 小字排版 */
        .status-text {
            font-size: 14px;
            letter-spacing: 2px;
            text-transform: uppercase;
            margin-bottom: 8px;
            font-weight: 300;
        }

        .countdown-text {
            font-size: 12px;
            color: #555;
            letter-spacing: 1px;
        }

        /* 4. 加载微光动效 */
        .loading-bar {
            width: 120px;
            height: 1px;
            background-color: #222;
            margin: 20px auto 0 auto;
            position: relative;
            overflow: hidden;
        }
        .loading-bar::after {
            content: '';
            position: absolute;
            left: -50%;
            width: 50%;
            height: 100%;
            background-color: #666;
            animation: loading-slide 1.5s infinite linear;
        }
        @keyframes loading-slide {
            0% { left: -50%; }
            100% { left: 100%; }
        }
    </style>
</head>
<body>

    <div class="terminal-box">
        <!-- 小字 -->
        <div class="status-text">CONNECTING TO STRONGHOLD PROTOCOL SERVER...</div>
        <div class="countdown-text" id="timer">NEURAL LINK WILL BE ESTABLISHED IN 1.5S</div>
        
        <!-- 进度条 -->
        <div class="loading-bar"></div>
    </div>

    <!-- 重定向状态机 -->
    <script>
        window.addEventListener('DOMContentLoaded', () => {
            //  Railway 主站链接
            const targetUrl = "https://stronghold-protocol-michu.up.railway.app/";
            
            // 延迟跳转
            setTimeout(() => {
                window.location.replace(targetUrl);
            }, 1500);
        });
    </script>

</body>
</html>
