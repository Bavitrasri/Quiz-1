<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Present Simple & Continuous Quiz</title>
    <style>
         body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            width: 80%;
            max-width: 600px;
            text-align: center;
        }

        h1 {
            color: #333;
        }

        #name-input-container {
            margin-bottom: 20px;
        }

        #name-input {
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            width: 70%;
            font-size: 16px;
        }

        .question {
            margin-bottom: 20px;
            font-size: 18px;
        }

        .options {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            margin-bottom: 15px;
        }

        .options label {
            margin-bottom: 8px;
            cursor: pointer;
            display: block;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            width: 100%;
            text-align: left;
            box-sizing: border-box; /* Important for padding */
            transition: background-color 0.2s ease; /* Smooth hover effect */
        }

        .options label:hover {
            background-color: #f5f5f5;
        }

        .options input[type="radio"] {
            margin-right: 10px;
        }

        button {
            background-color: #4CAF50;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }

        button:hover {
            background-color: #3e8e41;
        }

        #result {
            margin-top: 20px;
            font-size: 20px;
            font-weight: bold;
        }

        /* Contrast Colors */
        .correct {
            background-color: #aaffaa !important; /* Light green */
        }

        .incorrect {
            background-color: #ffaaaa !important; /* Light red */
        }

        .feedback {
            margin-top: 10px;
            font-style: italic;
        }

        #timer {
            font-size: 20px;
            font-weight: bold;
            margin-bottom: 10px;
        }
        #all-scores {
            margin-top: 30px;
            text-align: left;
        }

        #all-scores h2 {
            font-size: 22px;
            margin-bottom: 10px;
        }

        #all-scores ul {
            padding-left: 20px;
        }

        #all-scores li {
            font-size: 18px;
            margin-bottom: 5px;
        }
        /* Responsive Design */
        @media (max-width: 768px) {
            .container {
                width: 95%;
            }
        }

        @media (max-width: 480px) {
            h1 {
                font-size: 24px;
            }

            .question {
                font-size: 16px;
            }

            button {
                font-size: 14px;
                padding: 10px 15px;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Present Simple & Continuous Quiz</h1>

        <div id="name-input-container">
            <label for="name-input">Enter Your Name:</label>
            <input type="text" id="name-input" placeholder="Your Name">
            <button onclick="startQuiz()">Start Quiz</button> <!-- Start Quiz Button -->
        </div>
         <div id="timer">Time Left: <span id="time">10:00</span></div>

        <form id="quiz-form" style="display:none;">
        </form>

        <div id="feedback" class="feedback"></div>
        <button onclick="submitAnswer()">Submit Answer</button>
        <button onclick="nextQuestion()" disabled id="next-button">Next Question</button>

        <div id="result" style="display:none;"></div>

         <div id="all-scores" style="display: none;">
            <h2>All Scores</h2>
            <ul id="all-scores-list"></ul>
        </div>
    </div>

    <script>
         const questions = [
           {
                question: "What _____ you _____ (do) tonight?",
                options: ["do/do", "are/doing", "does/doing", "is/do"],
                answer: "are/doing"
            },
            {
                question: "She usually _____ (walk) to school, but today she _____ (take) the bus.",
                options: ["walks/takes", "is walking/is taking", "walk/take", "walking/taking"],
                answer: "walks/takes"
            },
            {
                question: "They _____ (not/like) spicy food. They prefer mild dishes.",
                options: ["don't like", "aren't liking", "doesn't like", "not like"],
                answer: "don't like"
            },
             {
                question: "Right now, the chef _____ (prepare) a delicious meal in the kitchen.",
                options: ["prepares", "is preparing", "prepare", "preparing"],
                answer: "is preparing"
            },
             {
                question: "My dad always _____ (read) the newspaper in the morning.",
                options: ["is reading", "read", "reads", "reading"],
                answer: "reads"
            },
             {
                question: "Listen! Someone _____ (play) the piano.",
                options: ["plays", "is playing", "play", "playing"],
                answer: "is playing"
            },
            {
                question: "Water _____ (boil) at 100 degrees Celsius.",
                options: ["boils", "is boiling", "boil", "boiling"],
                answer: "boils"
            },
            {
                question: "She _____ (not/study) French at the moment because she's on holiday.",
                options: ["don't study", "isn't studying", "doesn't study", "not studying"],
                answer: "isn't studying"
            },
            {
                question: "_____ (you/understand) the question?",
                options: ["Are you understand", "Do you understand", "You are understanding", "You understand"],
                answer: "Do you understand"
            },
            {
                question: "He _____ (work) at the bank. He's a cashier.",
                options: ["is working", "work", "works", "working"],
                answer: "works"
            },
             {
                question: "I _____ (think) about buying a new phone.",
                options: ["am thinking", "think", "thinking", "thinks"],
                answer: "am thinking"
            },
            {
                question: "The sun _____ (rise) in the east.",
                options: ["is rising", "rises", "rise", "rising"],
                answer: "rises"
            },
            {
                question: "They _____ (live) in London.",
                options: ["is living", "live", "lives", "living"],
                answer: "live"
            },
            {
                question: "She _____ (not/like) to cook.",
                options: ["don't like", "isn't liking", "doesn't like", "not liking"],
                answer: "doesn't like"
            },
            {
                question: "He _____ (study) for his exams right now.",
                options: ["studies", "is studying", "study", "studying"],
                answer: "is studying"
            },
             {
                question: "Birds _____ (fly).",
                options: ["is flying", "fly", "flies", "flying"],
                answer: "fly"
            },
            {
                question: "Right now I _____ (learn) to code.",
                options: ["am learning", "learn", "is learning", "learning"],
                answer: "am learning"
            },
            {
                question: "We _____ (enjoy) the party. ",
                options: ["enjoys", "is enjoying", "enjoy", "am enjoying"],
                answer: "enjoy"
            },
             {
                question: "The baby _____ (sleep) now. ",
                options: ["sleeps", "is sleeping", "sleep", "are sleeping"],
                answer: "is sleeping"
            },
             {
                question: "I _____ (go) to bed at 9pm every night. ",
                options: ["am going", "go", "goes", "is going"],
                answer: "go"
            }
        ];

        const quizForm = document.getElementById("quiz-form");
        const resultDiv = document.getElementById("result");
        const feedbackDiv = document.getElementById("feedback");
        const nextButton = document.getElementById("next-button");
        const allScoresDiv = document.getElementById("all-scores");
        const allScoresList = document.getElementById("all-scores-list");
        const timerDisplay = document.getElementById("time");
        let currentQuestion = 0;
        let score = 0;
        let playerName = "";
        let timeLeft = 600; // 10 minutes in seconds
        let timerInterval;

        // Load scores from local storage
        let allScores = JSON.parse(localStorage.getItem('allQuizScores')) || [];

        function loadQuestion() {
            nextButton.disabled = true;
            feedbackDiv.textContent = ""; // Clear previous feedback

            const questionData = questions[currentQuestion];
            const questionElement = document.createElement("div");
            questionElement.classList.add("question");
            questionElement.textContent = questionData.question;

            const optionsElement = document.createElement("div");
            optionsElement.classList.add("options");

            questionData.options.forEach((option, index) => {
                const label = document.createElement("label");
                const input = document.createElement("input");
                input.type = "radio";
                input.name = "question" + currentQuestion;
                input.value = option;
                input.id = "option" + index;

                label.appendChild(input);
                label.appendChild(document.createTextNode(option));
                optionsElement.appendChild(label);
            });

            quizForm.innerHTML = "";
            quizForm.appendChild(questionElement);
            quizForm.appendChild(optionsElement);
        }

        function submitAnswer() {
             nextButton.disabled = false;
            const selectedOption = document.querySelector(`input[name="question${currentQuestion}"]:checked`);
            if (!selectedOption) {
                alert("Please select an answer.");
                return;
            }

            const answer = selectedOption.value;
            const isCorrect = answer === questions[currentQuestion].answer;

            const labels = document.querySelectorAll('.options label');
            labels.forEach(label => {
                if (label.querySelector('input').value === questions[currentQuestion].answer) {
                    label.classList.add("correct");
                }
                if (label.querySelector('input:checked') === label.querySelector('input') && !isCorrect) {
                    label.classList.add("incorrect");
                }
            });
            if (isCorrect) {
                score++;
                feedbackDiv.textContent = "Correct!";
                feedbackDiv.style.color = "green";
            } else {
                feedbackDiv.textContent = "Incorrect. The correct answer was: " + questions[currentQuestion].answer;
                feedbackDiv.style.color = "red";
            }
             document.querySelector('[onclick="submitAnswer()"]').disabled = true;
        }

        function nextQuestion() {
            currentQuestion++;
            document.querySelector('[onclick="submitAnswer()"]').disabled = false;
            if (currentQuestion < questions.length) {
                loadQuestion();
            } else {
                endQuiz();
            }
        }

        function startTimer() {
            timerInterval = setInterval(function () {
                timeLeft--;
                const minutes = Math.floor(timeLeft / 60);
                const seconds = timeLeft % 60;
                timerDisplay.textContent = `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;

                if (timeLeft <= 0) {
                    endQuiz();
                }
            }, 1000);
        }

        function endQuiz() {
            clearInterval(timerInterval); // Stop the timer
             playerName = document.getElementById("name-input").value.trim();
            if (playerName === "") {
                playerName = "Anonymous";
            }
            quizForm.style.display = "none";
            feedbackDiv.style.display = "none";
            document.querySelector('[onclick="submitAnswer()"]').style.display = "none";
            document.querySelector('[onclick="nextQuestion()"]').style.display = "none";
            document.getElementById("timer").style.display = "none";

            resultDiv.textContent = `Time's up, ${playerName}! You scored ${score} out of ${questions.length}!`;
            resultDiv.style.display = "block";

            // Save score
            allScores.push({ name: playerName, score: score });

            // Save to local storage
            localStorage.setItem('allQuizScores', JSON.stringify(allScores));

            displayAllScores();
            allScoresDiv.style.display = "block";
        }
         function displayAllScores() {
            allScoresList.innerHTML = "";
            allScores.forEach((entry) => {
                const listItem = document.createElement("li");
                listItem.textContent = `${entry.name}: ${entry.score}`;
                allScoresList.appendChild(listItem);
            });
        }
         // Function to start the quiz
        function startQuiz() {
            playerName = document.getElementById("name-input").value.trim();
            if (playerName === "") {
                alert("Please enter your name to start the quiz.");
                return;
            }

            // Hide the name input container
            document.getElementById("name-input-container").style.display = "none";
            document.getElementById("quiz-form").style.display = "block";
            // Load the first question
            loadQuestion();

            //Start Timer
            startTimer(); // CRITICAL: This was missing!
        }

         displayAllScores();
    </script>

</body>
</html>
