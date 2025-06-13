#quiz-1
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Quiz Game</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
    }
    .fade {
      transition: all 0.4s ease-in-out;
    }
  </style>
</head>
<body class="bg-gradient-to-br from-indigo-800 to-purple-900 min-h-screen flex items-center justify-center text-white p-4">

  <div id="quizApp" class="bg-white text-gray-800 p-6 rounded-2xl shadow-2xl w-full max-w-md fade">
    <h1 class="text-2xl font-bold text-center mb-4 text-indigo-700">🧠 Quiz Game</h1>
    
    <div id="quizBox">
      <div id="question" class="text-lg font-semibold mb-4"></div>
      <div id="options" class="grid grid-cols-1 gap-3 mb-4"></div>
      <button id="nextBtn" class="w-full py-2 px-4 bg-indigo-600 text-white rounded hover:bg-indigo-700">Next</button>
    </div>

    <div id="resultBox" class="hidden text-center fade">
      <h2 class="text-xl font-bold mb-2">🎉 Quiz Completed!</h2>
      <p id="score" class="text-lg mb-4"></p>
      <button onclick="location.reload()" class="bg-green-600 px-4 py-2 rounded text-white hover:bg-green-700">Play Again</button>
    </div>
  </div>

  <script>
    const questions = [
      {
        question: "What is the capital of France?",
        options: ["Berlin", "Madrid", "Paris", "Lisbon"],
        answer: "Paris"
      },
      {
        question: "Which planet is known as the Red Planet?",
        options: ["Earth", "Saturn", "Mars", "Jupiter"],
        answer: "Mars"
      },
      {
        question: "What is the largest ocean?",
        options: ["Indian Ocean", "Atlantic Ocean", "Arctic Ocean", "Pacific Ocean"],
        answer: "Pacific Ocean"
      },
      {
        question: "Who wrote 'Harry Potter'?",
        options: ["J.R.R. Tolkien", "J.K. Rowling", "George R.R. Martin", "Rick Riordan"],
        answer: "J.K. Rowling"
      },
    ];

    let currentQuestion = 0;
    let score = 0;

    const questionEl = document.getElementById("question");
    const optionsEl = document.getElementById("options");
    const nextBtn = document.getElementById("nextBtn");
    const resultBox = document.getElementById("resultBox");
    const quizBox = document.getElementById("quizBox");
    const scoreEl = document.getElementById("score");

    function showQuestion(index) {
      const q = questions[index];
      questionEl.textContent = q.question;
      optionsEl.innerHTML = "";

      q.options.forEach(option => {
        const btn = document.createElement("button");
        btn.textContent = option;
        btn.className = "bg-indigo-100 hover:bg-indigo-300 text-indigo-800 font-medium py-2 px-4 rounded w-full text-left";
        btn.onclick = () => selectAnswer(btn, q.answer);
        optionsEl.appendChild(btn);
      });
    }

    function selectAnswer(button, correctAnswer) {
      const selected = button.textContent;
      if (selected === correctAnswer) {
        score++;
        button.classList.add("bg-green-300");
      } else {
        button.classList.add("bg-red-300");
      }

      Array.from(optionsEl.children).forEach(btn => {
        btn.disabled = true;
        if (btn.textContent === correctAnswer) {
          btn.classList.add("bg-green-200");
        }
      });

      nextBtn.disabled = false;
    }

    nextBtn.addEventListener("click", () => {
      currentQuestion++;
      if (currentQuestion < questions.length) {
        showQuestion(currentQuestion);
        nextBtn.disabled = true;
      } else {
        quizBox.classList.add("hidden");
        resultBox.classList.remove("hidden");
        scoreEl.textContent = Your score: ${score} out of ${questions.length};
      }
    });

    // Initialize
    showQuestion(currentQuestion);
    nextBtn.disabled = true;
  </script>
</body>
</html>
project 2
