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
        html, body {
            margin: 0 !important;
            padding: 0 !important;
            background-color: black !important;
            width: 100% !important;
            height: 100vh !important;
            overflow: hidden !important;
            font-family: sans-serif;
        }
        .quiz-container {
            display: flex !important;
            flex-direction: row; /* PC 端横向并排 */
            width: 100%;
            height: 100%;
            box-sizing: border-box;
        }
        .quiz-column {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 40px;
            box-sizing: border-box;
            border-right: 1px solid #111;
            transition: all 0.5s ease;    /* 平滑过渡动画 */
            opacity: 1;
        }        
        .quiz-column:last-child {
            border-right: none;
            border-bottom: none;
        }
        /* 移动端样式 */
        @media (max-width: 1024px) {
             /* 纵向滚动 */
            html, body {
                overflow-x: hidden !important;
                overflow-y: auto !important; 
            }
            .quiz-container {
                flex-direction: column !important; /* 垂直排列 */
                height: auto !important;
                width: 100% !important;
            }
            .quiz-column {
                flex: none !important;
                width: 100% !important;
                height: 100vh !important;
                border-right: none !important;     /* 移除左右分界线 */
                border-bottom: 1px solid #111;     /* 上下分界线 */
            }
        }
        .quiz-column.locked {
            opacity: 0;
            pointer-events: none;
        }
        .question-text {
            color: white;
            font-size: 16px;
            margin-bottom: 20px;
            letter-spacing: 1px;
            text-align: center;
        }
        /* 遮罩提示 */
        .hint-spoiler {
            background-color: #111;      
            color: #111;                 
            padding: 2px 6px;         
            border-radius: 4px;  
            cursor: help;  
            transition: all 0.3s ease; 
            user-select: none;
        }
        .hint-spoiler:hover {
            background-color: #222;     
            color: white;  
            user-select: text; 
        }
        .input-group {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
        }
        .input-prefix {
            color: #666;
            font-size: 14px;
            margin-right: 8px;
            font-family: monospace;
            user-select: none;
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
        .answer-input:focus {
            border-color: #666;
        }
        .answer-input.correct {
            border-color: #28a745 !important;
            background-color: #0b2e13;
            pointer-events: none;
        }
    </style>
</head>
<body>
    <div class="quiz-container">       
        <!-- 问题 1 -->
        <div class="quiz-column" id="col-1">
            <div class="question-text">Step 1: By <span class="hint-spoiler">LSB steganography</span>, find the message hidden in the image.<br>(hexadecimal values XX XX XX etc.)</div>
            <div class="input-group">
                <input type="text" class="answer-input" id="input-1" placeholder="Enter..." autocomplete="off">
            </div>
        </div>
        <!-- 问题 2 -->
        <div class="quiz-column locked" id="col-2">
            <div class="question-text">Step 2: Find the designated key by analysing the image source and the length of ciphertext.</div>
            <div class="input-group">
                <input type="text" class="answer-input" id="input-2" placeholder="Enter..." autocomplete="off">
            </div>
        </div>
        <!-- 问题 3 -->
        <div class="quiz-column locked" id="col-3">
            <div class="question-text">Step 3: Hence, by using the designated key, deduce the plaintext using <span class="hint-spoiler">XOR</span>.</div>
            <div class="input-group">
                <span class="input-prefix">./</span>
                <input type="text" class="answer-input" id="input-3" placeholder="Enter..." autocomplete="off">
            </div>
        </div>
    </div>
    <!-- JavaScript 判断对错 & 解锁下一关 -->
    <script>
        const config = {
            q1: { answer: "00 2f 36 2e 3d 36 35 33 3a 2c", nextCol: "col-2" },
            q2: { answer: "EARTH", nextCol: "col-3" },
            q3: { answer: "ENDZUSTAND", nextCol: null } 
        };
        document.getElementById('input-1').addEventListener('input', function() {
            checkAnswer(this, config.q1.answer, config.q1.nextCol);
        });
        document.getElementById('input-2').addEventListener('input', function() {
            checkAnswer(this, config.q2.answer, config.q2.nextCol);
        });
        document.getElementById('input-3').addEventListener('input', function() {
            if (this.value.trim().toLowerCase() === config.q3.answer.toLowerCase()) {
                this.classList.add('correct');        
                setTimeout(() => {
                    window.location.href = '/endzustand/';
                }, 800);     
            }
        });
        function checkAnswer(inputElement, correctAnswer, nextColumnId) {
            const userAnswer = inputElement.value.trim().toLowerCase();            
            if (userAnswer === correctAnswer.toLowerCase()) {
                inputElement.classList.add('correct');                
                if (nextColumnId) {
                    const nextCol = document.getElementById(nextColumnId);
                    nextCol.classList.remove('locked');                    
                    setTimeout(() => {
                        nextCol.querySelector('.answer-input').focus();
                    }, 500);
                }
            }
        }
    </script>
</body>
<!-- 居然看到这里了吗（（ -->
</html>