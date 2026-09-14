---
layout: null
permalink: /guide000/
---
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guide000</title>
    <style>
        /* 1. 基础全黑背景与全屏设置 */
        html, body {
            margin: 0 !important;
            padding: 0 !important;
            background-color: black !important;
            width: 100% !important;
            height: 100vh !important;
            overflow: hidden !important;
            font-family: sans-serif;
        }
        /* 2. 横向三等分大容器 */
        .quiz-container {
            display: flex !important;
            width: 100%;
            height: 100%;
            box-sizing: border-box;
        }
        /* 3. 每一个问题列的样式（核心：横向三等分） */
        .quiz-column {
            flex: 1; /* 关键：平分空间，三列刚好 1:1:1 */
            display: flex;
            flex-direction: column;
            justify-content: center; /* 垂直居中 */
            align-items: center;     /* 水平居中 */
            padding: 40px;
            box-sizing: border-box;
            border-right: 1px solid #111; /* 微弱的深灰色分界线，可删除 */
            transition: all 0.5s ease;    /* 出现时的平滑过渡动画 */
            opacity: 1;
        }        
        /* 移除最后一列的分界线 */
        .quiz-column:last-child {
            border-right: none;
        }
        /* 4. 关键：还未解锁的题目样式 —— 完全隐藏 */
        .quiz-column.locked {
            opacity: 0;
            pointer-events: none; /* 锁定时无法点击或聚焦输入框 */
        }
        /* 5. 文字与输入框样式 */
        .question-text {
            color: white;
            font-size: 14px;
            margin-bottom: 20px;
            letter-spacing: 1px;
            text-align: center;
        }
        /* 💡 新增：用于将提示文字和输入框横向并排的容器 */
        .input-group {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
        }
        /* 💡 新增：输入框前缀文字的样式 */
        .input-prefix {
            color: #666; /* 使用低调的暗灰色 */
            font-size: 14px;
            margin-right: 8px; /* 和输入框保持一点间距 */
            font-family: monospace; /* 使用等宽字体，更符合网页后缀的科技感 */
            user-select: none; /* 防止用户误选这段文字 */
        }
        .answer-input {
            background-color: #111;
            border: 1px solid #333;
            color: white;
            padding: 5px 15px;
            font-size: 12px;
            border-radius: 4px;
            outline: none;
            text-align: center;
            width: 80%;
            max-width: 200px;
            transition: border-color 0.3s;
        }
        /* 输入框聚焦时变亮 */
        .answer-input:focus {
            border-color: #666;
        }
        /* 答对时输入框的特殊样式 */
        .answer-input.correct {
            border-color: #28a745 !important; /* 绿色边框 */
            background-color: #0b2e13;
            pointer-events: none; /* 答对后锁定输入框 */
        }
    </style>
</head>
<body>
    <div class="quiz-container">       
        <!-- 问题 1 (默认可见) -->
        <div class="quiz-column" id="col-1">
            <div class="question-text">Step 1: By using LSB, find the message hidden in the image. (hexadecimal values XX XX XX etc.)</div>
            <div class="input-group">
                <input type="text" class="answer-input" id="input-1" placeholder="Enter..." autocomplete="off">
            </div>
        </div>
        <!-- 问题 2 (默认锁定) -->
        <div class="quiz-column locked" id="col-2">
            <div class="question-text">Step 2: Find the designated key by analysing the image source and the length of ciphertext.</div>
            <div class="input-group">
                <input type="text" class="answer-input" id="input-2" placeholder="Enter..." autocomplete="off">
            </div>
        </div>
        <!-- 问题 3 (默认锁定) -->
        <div class="quiz-column locked" id="col-3">
            <div class="question-text">Step 3: Hence, by using the designated key, deduce the cleartext using XOR.</div>
            <div class="input-group">
                <span class="input-prefix">/</span>
                <input type="text" class="answer-input" id="input-3" placeholder="Enter..." autocomplete="off">
            </div>
        </div>
    </div>
    <!-- JavaScript 逻辑：判断对错与解锁下一关 -->
    <script>
        // 🛠️ 在这里配置你的正确答案（支持大小写模糊匹配）
        const config = {
            q1: { answer: "00 2f 36 2e 3d 36 35 33 3a 2c", nextCol: "col-2" },
            q2: { answer: "EARTH", nextCol: "col-3" },
            q3: { answer: "ENDZUSTAND", nextCol: null } // 最后一题，没有下一关
        };
        // 监听第一个输入框
        document.getElementById('input-1').addEventListener('input', function() {
            checkAnswer(this, config.q1.answer, config.q1.nextCol);
        });
        // 监听第二个输入框
        document.getElementById('input-2').addEventListener('input', function() {
            checkAnswer(this, config.q2.answer, config.q2.nextCol);
        });
        // 监听第三个输入框
        document.getElementById('input-3').addEventListener('input', function() {
             // 检查第三题答案（确保 config.q3.answer 依然匹配你的标准答案）
            if (this.value.trim().toLowerCase() === config.q3.answer.toLowerCase()) {
                // 1. 标记第三个输入框为正确（变绿）
                this.classList.add('correct');        
                // 2. 稍微延迟 0.8 秒（800毫秒），让用户看到输入框变绿的成功反馈，然后丝滑跳转
                setTimeout(() => {
                    // 使用绝对路径跳转到你的 endzustand 页面
                    window.location.href = '/endzustand/';
                }, 800);     
            }
        });
        // 通用的答案检查函数
        function checkAnswer(inputElement, correctAnswer, nextColumnId) {
            // 获取用户输入并去除空格、转为小写（防止大小写导致判错）
            const userAnswer = inputElement.value.trim().toLowerCase();            
            if (userAnswer === correctAnswer.toLowerCase()) {
                // 1. 标记当前输入框为正确
                inputElement.classList.add('correct');                
                // 2. 解锁下一个问题列
                if (nextColumnId) {
                    const nextCol = document.getElementById(nextColumnId);
                    nextCol.classList.remove('locked');                    
                    // 3. 自动让下一个输入框获得焦点，提升体验
                    setTimeout(() => {
                        nextCol.querySelector('.answer-input').focus();
                    }, 500);
                }
            }
        }
    </script>
</body>
</html>
