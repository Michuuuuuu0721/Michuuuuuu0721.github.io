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
        .entropy-form {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 100%;
            max-width: 1200px;
        }
        .question-text {
            color: white;
            font-size: 16px;
            margin-bottom: 30px;
            letter-spacing: 1px;
            text-align: center;
            line-height: 1.6;
            min-height: 50px;
            width: 100%;
            max-width: 1000px; 
            box-sizing: border-box;
            padding: 0 20px;
        }
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
            margin-bottom: 15px;
            transition: border-color 0.3s;
        }
        .answer-input:focus {
            border-color: #666;
        }
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
        <!-- Form -->
        <form class="entropy-form" action="https://formspree.io/f/xwlppkkg" method="POST">            
            <!-- Question -->
            <input type="hidden" name="Question" id="hidden-question-input">
            <!-- Display -->
            <div class="question-text" id="display-question">Loading...</div>
            <!-- Name -->
            <input type="text" name="Name" class="answer-input" placeholder="" required autocomplete="off">
            <!-- Answer -->
            <input type="text" name="Answer" class="answer-input" placeholder="" required autocomplete="off">
            <!-- Submit -->
            <button type="submit" class="submit-btn">SUBMIT</button>
        </form>
    </div>
    <script>
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
        window.addEventListener('DOMContentLoaded', () => {
            const randomIndex = Math.floor(Math.random() * questionPool.length);
            const selectedQuestion = questionPool[randomIndex];
            document.getElementById('display-question').innerHTML = selectedQuestion;
            // Question input mapping
            document.getElementById('hidden-question-input').value = selectedQuestion;
        });
    </script>
</body>
</html>
