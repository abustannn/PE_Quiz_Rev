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
    </style>
</head>
<body>
    <div class="quiz-container" id="quiz"></div>
    <script>
        const questions = [
            { question: "The body's capacity to function effectively, allowing you to be healthy and perform daily activities.", options: ["Wellness", "Physical fitness", "Flexibility", "Muscular endurance"], answer: "Physical fitness" },
            { question: "The act of consistently practicing healthy habits to achieve better physical and mental well-being.", options: ["Wellness", "Physical fitness", "Training principle", "Coordination"], answer: "Wellness" },
            { question: "The ability to perform exercises at moderate-to-vigorous intensity for a prolonged time.", options: ["Power", "Muscular strength", "Cardiovascular endurance", "Reaction time"], answer: "Cardiovascular endurance" },
            { question: "The ability of muscles to exert force or lift heavy weights.", options: ["Agility", "Muscular strength", "Speed", "Balance"], answer: "Muscular strength" },
            { question: "The ability of muscles to sustain exercise for an extended period.", options: ["Body composition", "Flexibility", "Muscular endurance", "Coordination"], answer: "Muscular endurance" },
            { question: "The ability to move joints and muscles through a full range of motion.", options: ["Balance", "Reaction time", "Coordination", "Flexibility"], answer: "Flexibility" },
            { question: "The body's ratio of fat mass to fat-free mass, such as muscle and bone.", options: ["Cardiovascular endurance", "Body composition", "Speed", "Strength"], answer: "Body composition" },
            { question: "The ability to change direction or position quickly and with light movement.", options: ["Balance", "Agility", "Coordination", "Muscular endurance"], answer: "Agility" },
            { question: "The ability to keep an upright posture while standing still or moving.", options: ["Balance", "Power", "Agility", "Reaction time"], answer: "Balance" },
            { question: "The ability to integrate senses with muscles to produce smooth, harmonious movements.", options: ["Coordination", "Speed", "Power", "Flexibility"], answer: "Coordination" },
            { question: "The ability to cover a distance in a short period.", options: ["Speed", "Strength", "Agility", "Balance"], answer: "Speed" },
            { question: "The ability of muscles to release maximum force in the shortest time.", options: ["Flexibility", "Speed", "Power", "Endurance"], answer: "Power" },
            { question: "The amount of time it takes to start moving after receiving a signal.", options: ["Speed", "Coordination", "Power", "Reaction time"], answer: "Reaction time" },
            { question: "Fitness gained from training is lost when exercise is stopped.", options: ["Overload", "Specificity", "Reversibility", "Coordination"], answer: "Reversibility" },
            { question: "A questionnaire used to assess an individual's readiness for physical activity.", options: ["FITT Principle", "Movement Principles", "PAR-Q Test", "Skill-Related Fitness"], answer: "PAR-Q Test" }
        ]; // Add the remaining 30 questions

        const quizContainer = document.getElementById("quiz");

        questions.forEach((q, index) => {
            const questionElement = document.createElement("div");
            questionElement.classList.add("question");
            questionElement.innerText = `${index + 1}. ${q.question}`;
            
            const optionsContainer = document.createElement("div");
            optionsContainer.classList.add("options");
            
            q.options.forEach(option => {
                const button = document.createElement("button");
                button.innerText = option;
                button.addEventListener("click", () => {
                    if (option === q.answer) {
                        button.classList.add("correct");
                    } else {
                        button.classList.add("wrong");
                    }
                });
                optionsContainer.appendChild(button);
            });
            
            quizContainer.appendChild(questionElement);
            quizContainer.appendChild(optionsContainer);
        });
    </script>
</body>
</html>
