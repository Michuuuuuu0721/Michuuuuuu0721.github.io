---
layout: null
permalink: /guide000
---
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>解密游戏</title>
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
            font-size: 16px;
            margin-bottom: 20px;
            letter-spacing: 1px;
            text-align: center;
        }
        .answer-input {
            background-color: #111;
            border: 1px solid #333;
            color: white;
            padding: 10px 15px;
            font-size: 14px;
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
            <div class="question-text">问题一：世界上第一台计算机叫什么？</div>
            <input type="text" class="answer-input" id="input-1" placeholder="请输入答案..." autocomplete="off">
        </div>
        <!-- 问题 2 (默认锁定) -->
        <div class="quiz-column locked" id="col-2">
            <div class="question-text">问题二：1加1等于几？</div>
            <input type="text" class="answer-input" id="input-2" placeholder="请输入答案..." autocomplete="off">
        </div>
        <!-- 问题 3 (默认锁定) -->
        <div class="quiz-column locked" id="col-3">
            <div class="question-text">问题三：最终关卡：本网站的博主是谁？</div>
            <input type="text" class="answer-input" id="input-3" placeholder="请输入答案..." autocomplete="off">
        </div>
    </div>
    <!-- JavaScript 逻辑：判断对错与解锁下一关 -->
    <script>
        // 🛠️ 在这里配置你的正确答案（支持大小写模糊匹配）
        const config = {
            q1: { answer: "ENIAC", nextCol: "col-2" },
            q2: { answer: "2", nextCol: "col-3" },
            q3: { answer: "michu", nextCol: null } // 最后一题，没有下一关
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
            // 最后一题正确后的特殊处理
            if (this.value.trim().toLowerCase() === config.q3.answer.toLowerCase()) {
                this.classList.add('correct');
                alert('恭喜你，全部通关！'); // 这里可以改成跳转或显示通关彩蛋
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
