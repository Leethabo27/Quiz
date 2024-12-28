<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Dragon Ball Quiz Game</title>
    <style>
      /* Basic Reset */
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }

      body {
        font-family: Arial, sans-serif;
        overflow: hidden;
        color: #fff;
        background: #000;
        height: 100vh;
      }

      /* Animated Background */
      .background {
        position: absolute;
        width: 100%;
        height: 100%;
        background: url("https://wallpapercave.com/wp/wp5535333.jpg") no-repeat
          center center/cover;
        z-index: -2;
      }

      .dragon-balls {
        position: absolute;
        width: 100%;
        height: 100%;
        z-index: -1;
        overflow: hidden;
      }

      .dragon-ball {
        position: absolute;
        width: 50px;
        height: 50px;
        background: url("https://upload.wikimedia.org/wikipedia/en/6/63/Dragon_Ball_%28ball%29.png")
          no-repeat center center/contain;
        animation: float 5s ease-in-out infinite;
      }

      @keyframes float {
        0%,
        100% {
          transform: translateY(0);
        }
        50% {
          transform: translateY(-30px);
        }
      }

      .dragon-ball:nth-child(1) {
        left: 10%;
        top: 10%;
        animation-delay: 0s;
      }

      .dragon-ball:nth-child(2) {
        left: 80%;
        top: 15%;
        animation-delay: 1s;
      }

      .dragon-ball:nth-child(3) {
        left: 50%;
        top: 70%;
        animation-delay: 2s;
      }

      .dragon-ball:nth-child(4) {
        left: 25%;
        top: 40%;
        animation-delay: 3s;
      }

      .dragon-ball:nth-child(5) {
        left: 75%;
        top: 50%;
        animation-delay: 4s;
      }

      /* Quiz Content */
      .quiz-container {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: rgba(0, 0, 0, 0.8);
        padding: 20px;
        border-radius: 10px;
        width: 80%;
        max-width: 500px;
        text-align: center;
      }

      .quiz-container h1 {
        font-size: 2rem;
        margin-bottom: 20px;
        color: #ffcc00;
        text-shadow: 2px 2px 5px #f00;
      }

      .quiz-container button {
        background: #ff9900;
        color: #fff;
        border: none;
        padding: 10px 20px;
        font-size: 1rem;
        border-radius: 5px;
        cursor: pointer;
        margin: 10px 5px;
      }

      .quiz-container button:hover {
        background: #e68a00;
      }

      /* Footer */
      footer {
        position: absolute;
        bottom: 10px;
        width: 100%;
        text-align: center;
        font-size: 0.9rem;
        color: #fff;
        text-shadow: 1px 1px 3px #000;
      }

      footer a {
        color: #ffcc00;
        text-decoration: none;
      }

      footer a:hover {
        text-decoration: underline;
      }

      /* Dragon Balls */
      .dragon-ball {
        position: absolute;
        width: 40px;
        height: 40px;
        background: radial-gradient(circle, orange, #ff9900);
        border: 2px solid white;
        border-radius: 50%;
        animation: float 5s infinite ease-in-out;
      }

      .dragon-ball:before {
        content: "★";
        font-size: 1.2rem;
        color: red;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        text-shadow: 0 0 5px red;
      }

      @keyframes float {
        0% {
          transform: translateY(0);
        }
        50% {
          transform: translateY(-20px);
        }
        100% {
          transform: translateY(0);
        }
      }

      /* Responsive Breakpoints */
      @media (max-width: 768px) {
        header h1 {
          font-size: 2rem;
        }

        nav a {
          font-size: 0.9rem;
        }

        .subscribe input[type="email"] {
          width: 100%;
          margin: 10px 0;
        }
      }

      @media (max-width: 480px) {
        .links a {
          font-size: 0.9rem;
        }
      }
    </style>
  </head>
  <body>
    <div class="background"></div>
    <div class="dragon-balls">
      <div class="dragon-ball"></div>
      <div class="dragon-ball"></div>
      <div class="dragon-ball"></div>
      <div class="dragon-ball"></div>
      <div class="dragon-ball"></div>
    </div>
    <div class="quiz-container">
      <h1>Dragon Ball Quiz</h1>
      <p id="question"></p>
      <div id="answers"></div>
      <button id="next-btn" style="display: none" onclick="nextQuestion()">
        Next Question
      </button>
      <p id="score" style="margin-top: 20px"></p>
    </div>

    <footer>
      Created by
      <a href="https://lethabosemenya.myportfolio.com" target="_blank"
        >Lethabo Semenya</a
      >
    </footer>

    <script>
      const quizData = [
        {
          question: "What is Goku's Saiyan name?",
          answers: ["Raditz", "Kakarot", "Bardock", "Vegeta"],
          correct: "Kakarot",
        },
        {
          question: "Who was Goku's first trainer?",
          answers: ["Master Roshi", "Kami", "King Kai", "Piccolo"],
          correct: "Master Roshi",
        },
        {
          question: "How many Dragon Balls are there?",
          answers: ["6", "7", "8", "9"],
          correct: "7",
        },
        {
          question: "What is Vegeta's father's name?",
          answers: ["King Cold", "King Vegeta", "Paragus", "Nappa"],
          correct: "King Vegeta",
        },
        {
          question: "Who created the androids?",
          answers: ["Dr. Brief", "Dr. Gero", "Bulma", "Dr. Wheelo"],
          correct: "Dr. Gero",
        },
        {
          question: "Who killed Frieza on Namek?",
          answers: ["Goku", "Vegeta", "Piccolo", "Future Trunks"],
          correct: "Goku",
        },
        {
          question: "What does Gohan mean?",
          answers: ["Rice", "Hero", "Warrior", "Dragon"],
          correct: "Rice",
        },
        {
          question: "Who is Goten's mother?",
          answers: ["Bulma", "Chi-Chi", "Videl", "Android 18"],
          correct: "Chi-Chi",
        },
        {
          question: "What is the name of Goku's Nimbus cloud?",
          answers: [
            "Flying Cloud",
            "Flying Nimbus",
            "Kinto'un",
            "Dragon Cloud",
          ],
          correct: "Flying Nimbus",
        },
        {
          question: "Which Saiyan killed King Cold?",
          answers: ["Vegeta", "Gohan", "Trunks", "Goku"],
          correct: "Trunks",
        },
        {
          question: "What is the name of the Eternal Dragon?",
          answers: ["Shenron", "Porunga", "Omega", "Dragonite"],
          correct: "Shenron",
        },
        {
          question: "What color is Super Saiyan Blue?",
          answers: ["Yellow", "Red", "Blue", "Green"],
          correct: "Blue",
        },
        {
          question: "Who trained Goku on King Kai's planet?",
          answers: ["King Kai", "Bubbles", "Mr. Popo", "Piccolo"],
          correct: "King Kai",
        },
        {
          question: "What is Beerus the God of?",
          answers: ["Creation", "Time", "Destruction", "Life"],
          correct: "Destruction",
        },
        {
          question: "What is Goku's highest form in Dragon Ball Super?",
          answers: ["Super Saiyan 3", "Ultra Instinct", "Kaioken x20", "SSGSS"],
          correct: "Ultra Instinct",
        },
        {
          question: "Who fused to form Vegito?",
          answers: [
            "Goku and Goten",
            "Vegeta and Trunks",
            "Goku and Vegeta",
            "Gotenks",
          ],
          correct: "Goku and Vegeta",
        },
       
      ];

      let currentQuestion = 0;
      let score = 0;

      function loadQuestion() {
        const questionEl = document.getElementById("question");
        const answersEl = document.getElementById("answers");
        const nextBtn = document.getElementById("next-btn");

        // Load the question and answers
        questionEl.textContent = quizData[currentQuestion].question;
        answersEl.innerHTML = "";
        quizData[currentQuestion].answers.forEach((answer) => {
          const button = document.createElement("button");
          button.textContent = answer;
          button.onclick = () => checkAnswer(answer);
          answersEl.appendChild(button);
        });

        nextBtn.style.display = "none"; // Hide the next button until an answer is selected
      }

      function checkAnswer(answer) {
        const nextBtn = document.getElementById("next-btn");
        const scoreEl = document.getElementById("score");

        if (answer === quizData[currentQuestion].correct) {
          alert("Correct! Well done, Saiyan.");
          score++;
        } else {
          alert("Wrong! Better luck next time.");
        }

        scoreEl.textContent = `Score: ${score}/${quizData.length}`;
        nextBtn.style.display = "inline-block";
      }

      function nextQuestion() {
        currentQuestion++;
        if (currentQuestion < quizData.length) {
          loadQuestion();
        } else {
          endQuiz();
        }
      }

      function endQuiz() {
        const questionEl = document.getElementById("question");
        const answersEl = document.getElementById("answers");
        const nextBtn = document.getElementById("next-btn");

        questionEl.textContent = "Quiz Complete!";
        answersEl.innerHTML = `You scored ${score}/${quizData.length}.`;
        nextBtn.style.display = "none";
      }

      // Initialize the quiz
      loadQuestion();
    </script>
    <div
      class="dragon-ball"
      style="top: 10%; left: 15%; animation-duration: 6s"
    ></div>
    <div
      class="dragon-ball"
      style="top: 30%; left: 75%; animation-duration: 7s"
    ></div>
    <div
      class="dragon-ball"
      style="top: 60%; left: 25%; animation-duration: 5s"
    ></div>
    <div
      class="dragon-ball"
      style="top: 80%; left: 50%; animation-duration: 8s"
    ></div>
    <div
      class="dragon-ball"
      style="top: 20%; left: 60%; animation-duration: 6.5s"
    ></div>
  </body>
</html>

