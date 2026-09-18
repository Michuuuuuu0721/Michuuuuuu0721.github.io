---
layout: null
permalink: /entropy/
---
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Entropy</title>
    <style>
        /* 1. 基础全黑背景与防滚动设置 */
        html, body {
            margin: 0 !important;
            padding: 0 !important;
            background-color: black !important;
            width: 100% !important;
            height: 100vh !important;
            overflow: hidden !important;
            font-family: sans-serif;
            box-sizing: border-box;
        }
        /* 2. 居中大容器 */
        .entropy-container {
            width: 100%;
            height: 100%;
            display: flex !important;
            flex-direction: column !important; 
            justify-content: center !important;
            align-items: center !important;
            padding: 20px;
            box-sizing: border-box;
        }
        /* 3. 表单表层包裹 */
        .entropy-form {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 100%;
            max-width: 1200px;
        }
        /* 4. 随机问题文本样式 */
        .question-text {
            color: white;
            font-size: 16px;
            margin-bottom: 30px;
            letter-spacing: 1px;
            text-align: center;
            line-height: 1.6;
            min-height: 50px; /* 防止题目字数不同导致布局跳动 */
            width: 100%;
            max-width: 1000px; 
            box-sizing: border-box;
            padding: 0 20px;
        }
        /* 5. 输入框通用样式（沿用之前的扁平清爽风格） */
        .answer-input {
            background-color: #111;
            border: 1px solid #333;
            color: white;
            padding: 6px 15px;
            font-size: 13px;
            border-radius: 2px;
            outline: none;
            text-align: center;
            width: 80%;
            max-width: 250px;
            margin-bottom: 15px; /* 输入框之间的间距 */
            transition: border-color 0.3s;
        }
        .answer-input:focus {
            border-color: #666;
        }
        /* 6. 提交按钮样式 */
        .submit-btn {
            background-color: #222;
            border: 1px solid #444;
            color: #aaa;
            padding: 6px 20px;
            font-size: 13px;
            border-radius: 2px;
            cursor: pointer;
            margin-top: 10px;
            transition: all 0.3s;
            letter-spacing: 1px;
        }
        .submit-btn:hover {
            background-color: white;
            color: black;
            border-color: white;
        }
    </style>
</head>
<body>
    <div class="entropy-container">
        <!-- 💡 数据收集表单：把下面的 ACTION_URL 替换为你的数据收集链接 -->
        <form class="entropy-form" action="https://formspree.io/f/xwlppkkg" method="POST">            
            <!-- 隐藏的输入框：用于在后台记录用户被抽到的是哪道题 -->
            <input type="hidden" name="Question" id="hidden-question-input">
            <!-- 核心：随机问题显示区域 -->
            <div class="question-text" id="display-question">Loading...</div>
            <!-- 上方输入框：填写姓名 -->
            <input type="text" name="Name" class="answer-input" placeholder="Your Name" required autocomplete="off">
            <!-- 下方输入框：填写答案 -->
            <input type="text" name="Answer" class="answer-input" placeholder="Your Answer" required autocomplete="off">
            <!-- 提交按钮 -->
            <button type="submit" class="submit-btn">SUBMIT</button>
        </form>
    </div>
    <script>
        // 🛠️ 在这里配置你的随机题库（可以无限往下添加新题目）
        const questionPool = [
            "Let's say entropy works on emotional memory. Is forgetting betrayal/hurt a gain or loss?",
            "Let’s say entropy makes you view your own past self like a stranger. Is that sense of distance a good or bad thing?",
            "Let’s say a robot can feel genuine sorrow and joy, yet it cannot physically decay from entropy. Should we regard it as truly alive?<br>Hence, is the ability to decay and die a characteristic of life?",
            "Let’s say an intelligent non‑human species builds meaning completely different from human ideas of purpose. Does their view of life hold equal weight to ours?",
            "Let’s say a machine can perfectly mimics human grief and sorrow. Do we owe it our sympathy?",
            "Let’s say a being’s only purpose is assigned to it by others. Can it create a genuine sense of itself beyond that original mindset?",
            "Let's say that human are, to basic, cells and chemicals that responds conditionally and definitively. What differs us from machines that also responds conditionally and definitively, providing a given input and response? In other words, by what point is there a difference?",
            "Let’s say a creature feels no fear of entropy or ending. Is something missing from its experience of life, or is it simply free?"
        ];
        // 页面加载时运行随机挑选逻辑
        window.addEventListener('DOMContentLoaded', () => {
            // 1. 从题库中随机抽取索引
            const randomIndex = Math.floor(Math.random() * questionPool.length);
            const selectedQuestion = questionPool[randomIndex];
            // 2. 将题目渲染到屏幕正中央
            document.getElementById('display-question').innerHTML = selectedQuestion;
            // 3. 将题目同时写入隐藏的表单项中，这样用户提交时，你能在后台知道他回答的是哪道题
            document.getElementById('hidden-question-input').value = selectedQuestion;
        });
    </script>
</body>
</html>
