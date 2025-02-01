<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PE Terminology Quiz - Game Show Style</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Bungee+Shade&family=Poppins:wght@300;400;700&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #1a1a1a;
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            text-align: center;
        }
        .quiz-container {
            width: 60%;
            background: linear-gradient(45deg, #004d99, #001f3f);
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
            text-align: center;
            border: 5px solid gold;
            position: relative;
        }
        .question-box {
            background: #003366;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 8px rgba(255, 215, 0, 0.8);
            font-size: 22px;
            font-weight: bold;
            color: white;
            display: none;
        }
        .options-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 15px;
            display: none;
        }
        .option-button {
            width: 80%;
            padding: 15px;
            margin: 10px 0;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
            background-color: #004d99;
            color: white;
            transition: all 0.3s;
        }
        .option-button:hover {
            background-color: gold;
            color: black;
        }
        .correct {
            background-color: green !important;
        }
        .wrong {
            background-color: red !important;
        }
        #next-btn, #start-btn {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 18px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            background-color: gold;
            color: black;
        }
        .question-list {
            position: absolute;
            right: -180px;
            top: 10px;
            background: #003366;
            padding: 15px;
            border-radius: 10px;
            color: white;
            font-size: 14px;
            width: 150px;
            display: none;
        }
        .current {
            color: gold;
            font-weight: bold;
        }
        #username-container {
            margin-bottom: 15px;
        }
        #username {
            padding: 10px;
            font-size: 16px;
            border-radius: 10px;
            border: none;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div id="username-container">
            <input type="text" id="username" placeholder="Enter your username" required>
            <button id="start-btn">Start Quiz</button>
        </div>
        <div id="progress"></div>
        <div class="question-box" id="question-container"></div>
        <div class="options-container" id="options-container"></div>
        <button id="next-btn" style="display: none;">Next</button>
        <div id="result"></div>
        <button id="restart" style="display: none;">Play Again</button>
        <div class="question-list" id="question-list"></div>
    </div>
    <script>
        let questions = [];
        for (let i = 1; i <= 45; i++) {
            questions.push({ question: `Question ${i}?`, options: ["A", "B", "C", "D"], answer: "A" });
        }
        let currentQuestionIndex = 0;
        let score = 0;
        let username = "";
        
        document.getElementById("start-btn").addEventListener("click", () => {
            username = document.getElementById("username").value;
            if (!username.trim()) {
                alert("Please enter your username.");
                return;
            }
            document.getElementById("username-container").style.display = "none";
            document.getElementById("question-container").style.display = "block";
            document.getElementById("options-container").style.display = "flex";
            document.getElementById("question-list").style.display = "block";
            displayQuestion();
        });
        
        document.getElementById("next-btn").addEventListener("click", () => {
            currentQuestionIndex++;
            if (currentQuestionIndex < questions.length) {
                displayQuestion();
            } else {
                showResults();
            }
        });
        
        function displayQuestion() {
            let questionData = questions[currentQuestionIndex];
            document.getElementById("question-container").innerText = questionData.question;
            
            let optionsContainer = document.getElementById("options-container");
            optionsContainer.innerHTML = "";
            questionData.options.forEach(option => {
                let button = document.createElement("button");
                button.classList.add("option-button");
                button.innerText = option;
                button.addEventListener("click", () => checkAnswer(option, button));
                optionsContainer.appendChild(button);
            });
            document.getElementById("next-btn").style.display = "none";
            updateQuestionList();
        }
        
        function checkAnswer(selected, button) {
            let correctAnswer = questions[currentQuestionIndex].answer;
            button.classList.add(selected === correctAnswer ? "correct" : "wrong");
            document.getElementById("next-btn").style.display = "block";
            if (selected === correctAnswer) score++;
        }
        
        function showResults() {
            let percentage = (score / questions.length) * 100;
            let resultText = `${username}'s Score: ${score}/45 (${percentage.toFixed(2)}%)`;
            document.getElementById("result").innerText = resultText;
        }
        
        function updateQuestionList() {
            let list = "";
            for (let i = 0; i < questions.length; i++) {
                list += `<div class="${i === currentQuestionIndex ? "current" : ""}">Question ${i+1}</div>`;
            }
            document.getElementById("question-list").innerHTML = list;
        }
    </script>
</body>
</html>
