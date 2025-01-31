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
        .options button {
            display: block;
            width: 100%;
            padding: 15px;
            margin: 10px 0;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 20px;
            font-weight: bold;
            background-color: #004d99;
            color: white;
            transition: all 0.3s;
        }
        .options button:hover {
            background-color: gold;
            color: black;
        }
        .correct {
            background-color: green !important;
            color: white;
        }
        .wrong {
            background-color: red !important;
            color: white;
        }
        #progress {
            font-size: 20px;
            margin-bottom: 15px;
            font-weight: bold;
        }
        #result {
            font-size: 24px;
            font-weight: bold;
            margin-top: 20px;
            padding: 15px;
            border-radius: 10px;
            color: white;
        }
        #restart {
            display: none;
            margin-top: 20px;
            padding: 15px 30px;
            font-size: 22px;
            font-weight: bold;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            background-color: gold;
            color: black;
            transition: 0.3s;
        }
        #restart:hover {
            background-color: #ffcc00;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div id="progress"></div>
        <div class="question-box">
            <div id="question-container"></div>
        </div>
        <div id="options-container"></div>
        <div id="result"></div>
        <button id="restart">Play Again</button>
    </div>
    <script>
        let questions = [
            { question: "The body's capacity to function effectively, allowing you to be healthy and perform daily activities.", options: ["Wellness", "Physical fitness", "Flexibility", "Muscular endurance"], answer: "Physical fitness" },
            { question: "The act of consistently practicing healthy habits to achieve better physical and mental well-being.", options: ["Wellness", "Physical fitness", "Training principle", "Coordination"], answer: "Wellness" }
        ]; // Ensure there are 45 questions in the array

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        let selectedQuestions = [];
        function selectRandomQuestions() {
            shuffleArray(questions);
            selectedQuestions = questions.slice(0, 45); // Ensures 45 questions per quiz
        }

        let currentQuestionIndex = 0;
        let score = 0;
        selectRandomQuestions();

        function displayQuestion() {
            if (currentQuestionIndex >= selectedQuestions.length) {
                showResults();
                return;
            }

            let questionData = selectedQuestions[currentQuestionIndex];
            document.getElementById("progress").innerText = `Question ${currentQuestionIndex + 1} of ${selectedQuestions.length}`;
            document.getElementById("question-container").innerText = questionData.question;

            let optionsContainer = document.getElementById("options-container");
            optionsContainer.innerHTML = "";
            questionData.options.forEach(option => {
                let button = document.createElement("button");
                button.innerText = option;
                button.addEventListener("click", () => checkAnswer(option, button));
                optionsContainer.appendChild(button);
            });
        }

        function checkAnswer(selected, button) {
            let correctAnswer = selectedQuestions[currentQuestionIndex].answer;
            if (selected === correctAnswer) {
                button.classList.add("correct");
                score++;
            } else {
                button.classList.add("wrong");
            }
            setTimeout(() => {
                currentQuestionIndex++;
                displayQuestion();
            }, 1000);
        }

        function showResults() {
            let percentage = (score / selectedQuestions.length) * 100;
            let resultText = `You scored ${score} out of ${selectedQuestions.length} (${percentage.toFixed(2)}%)`;
            let resultContainer = document.getElementById("result");
            resultContainer.innerText = resultText;
            resultContainer.style.backgroundColor = percentage >= 75 ? "green" : "red";
            resultContainer.innerHTML += `<br>${percentage >= 75 ? "Congratulations! You passed!" : "Try again! You failed."}`;
            document.getElementById("restart").style.display = "block";
        }

        document.getElementById("restart").addEventListener("click", () => {
            currentQuestionIndex = 0;
            score = 0;
            selectRandomQuestions();
            document.getElementById("result").innerHTML = "";
            document.getElementById("restart").style.display = "none";
            displayQuestion();
        });

        displayQuestion();
    </script>
</body>
</html>
