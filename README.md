<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PE Terminology Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            padding: 20px;
            text-align: center;
        }
        .quiz-container {
            max-width: 600px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .question {
            font-weight: bold;
            margin-bottom: 10px;
        }
        .options button {
            display: block;
            width: 100%;
            padding: 10px;
            margin: 5px 0;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s;
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
            margin: 10px 0;
        }
        #result {
            font-size: 20px;
            font-weight: bold;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div id="progress"></div>
        <div id="question-container"></div>
        <div id="options-container"></div>
        <div id="result"></div>
        <button id="restart" style="display: none;">Take Another Quiz</button>
    </div>
    <script>
        let questions = [
            { question: "The body's capacity to function effectively, allowing you to be healthy and perform daily activities.", options: ["Wellness", "Physical fitness", "Flexibility", "Muscular endurance"], answer: "Physical fitness" },
            { question: "The act of consistently practicing healthy habits to achieve better physical and mental well-being.", options: ["Wellness", "Physical fitness", "Training principle", "Coordination"], answer: "Wellness" },
            { question: "The ability to perform exercises at moderate-to-vigorous intensity for a prolonged time.", options: ["Power", "Muscular strength", "Cardiovascular endurance", "Reaction time"], answer: "Cardiovascular endurance" }
        ]; // Add all 45 questions here

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        let currentQuestionIndex = 0;
        let score = 0;
        shuffleArray(questions);

        function displayQuestion() {
            if (currentQuestionIndex >= questions.length) {
                showResults();
                return;
            }

            let questionData = questions[currentQuestionIndex];
            document.getElementById("progress").innerText = `Question ${currentQuestionIndex + 1} of ${questions.length}`;
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
            let correctAnswer = questions[currentQuestionIndex].answer;
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
            let percentage = (score / questions.length) * 100;
            let resultText = `You scored ${score} out of ${questions.length} (${percentage.toFixed(2)}%)`;
            let resultContainer = document.getElementById("result");
            resultContainer.innerText = resultText;
            resultContainer.style.color = percentage >= 75 ? "green" : "red";
            resultContainer.innerHTML += `<br>${percentage >= 75 ? "Congratulations! You passed!" : "Try again! You failed."}`;
            document.getElementById("restart").style.display = "block";
        }

        document.getElementById("restart").addEventListener("click", () => {
            currentQuestionIndex = 0;
            score = 0;
            shuffleArray(questions);
            document.getElementById("result").innerHTML = "";
            document.getElementById("restart").style.display = "none";
            displayQuestion();
        });

        displayQuestion();
    </script>
</body>
</html>
