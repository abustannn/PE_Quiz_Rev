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
        }
        .options-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 15px;
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
        #next-btn {
            display: none;
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 18px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            background-color: gold;
            color: black;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div id="question-container" class="question-box"></div>
        <div id="options-container" class="options-container"></div>
        <button id="next-btn">Next</button>
        <div id="result"></div>
    </div>
    <script>
        let questions = [
            { question: "The body's capacity to function effectively, allowing you to be healthy and perform daily activities.", options: ["Physical fitness", "Wellness", "Flexibility", "Muscular endurance"], answer: "Physical fitness" },
            { question: "The act of consistently practicing healthy habits to achieve better physical and mental well-being.", options: ["Wellness", "Physical fitness", "Training principle", "Coordination"], answer: "Wellness" },
            { question: "The ability to perform exercises at moderate-to-vigorous intensity for a prolonged time.", options: ["Power", "Muscular strength", "Cardiovascular endurance", "Reaction time"], answer: "Cardiovascular endurance" },
            { question: "The ability of muscles to exert force or lift heavy weights.", options: ["Agility", "Muscular strength", "Speed", "Balance"], answer: "Muscular strength" },
            { question: "The ability of muscles to sustain exercise for an extended period.", options: ["Body composition", "Flexibility", "Muscular endurance", "Coordination"], answer: "Muscular endurance" }
        ];
        
        let currentQuestionIndex = 0;
        let score = 0;
        
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
        }
        
        function checkAnswer(selected, button) {
            let correctAnswer = questions[currentQuestionIndex].answer;
            button.classList.add(selected === correctAnswer ? "correct" : "wrong");
            document.getElementById("next-btn").style.display = "block";
            if (selected === correctAnswer) score++;
        }
        
        document.getElementById("next-btn").addEventListener("click", () => {
            currentQuestionIndex++;
            if (currentQuestionIndex < questions.length) {
                displayQuestion();
            } else {
                document.getElementById("question-container").innerText = "Quiz Complete!";
                document.getElementById("options-container").innerHTML = "";
                document.getElementById("result").innerText = `You scored ${score}/${questions.length} (${((score / questions.length) * 100).toFixed(2)}%)`;
                document.getElementById("next-btn").style.display = "none";
            }
        });
        
        displayQuestion();
    </script>
</body>
</html>
