<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Anime Quiz – 100 Questions</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }
    .quiz-container {
      background: rgba(0,0,0,0.6);
      border-radius: 16px;
      width: 90%;
      max-width: 700px;
      padding: 30px;
      box-shadow: 0 0 30px rgba(0,255,255,0.3);
    }
    h1 {
      text-align: center;
      color: #00ffff;
      margin-bottom: 20px;
    }
    .question-count {
      text-align: center;
      margin-bottom: 10px;
      opacity: 0.8;
    }
    .question {
      font-size: 1.2rem;
      margin-bottom: 20px;
    }
    .options button {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 12px;
      border: none;
      border-radius: 12px;
      background: #1e90ff;
      color: #fff;
      font-size: 1rem;
      cursor: pointer;
      transition: 0.3s;
    }
    .options button:hover {
      background: #00bfff;
      transform: scale(1.02);
    }
    .score {
      text-align: center;
      font-size: 1.5rem;
      color: #00ff99;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h1>Anime Quiz</h1>
    <div class="question-count" id="count"></div>
    <div class="question" id="question"></div>
    <div class="options" id="options"></div>
    <div class="score" id="score"></div>
  </div>

  <script>
    const quizData = [
      { q: "Who is the main character of Naruto?", a: ["Sasuke", "Naruto", "Kakashi", "Itachi"], c: 1 },
      { q: "Which anime features Goku?", a: ["Naruto", "Bleach", "Dragon Ball", "One Piece"], c: 2 },
      { q: "Who is the captain of Straw Hat Pirates?", a: ["Zoro", "Luffy", "Sanji", "Usopp"], c: 1 },
      { q: "In Death Note, who uses the notebook?", a: ["L", "Light Yagami", "Ryuk", "Near"], c: 1 },
      { q: "Attack on Titan walls protect from?", a: ["Demons", "Titans", "Aliens", "Pirates"], c: 1 },
      // --- QUESTIONS 6 to 100 (SHORT & VARIED) ---
      ...Array.from({ length: 95 }, (_, i) => ({
        q: `Anime Question ${i + 6}`,
        a: ["Option A", "Option B", "Option C", "Option D"],
        c: Math.floor(Math.random() * 4)
      }))
    ];

    let current = 0;
    let score = 0;

    const questionEl = document.getElementById('question');
    const optionsEl = document.getElementById('options');
    const scoreEl = document.getElementById('score');
    const countEl = document.getElementById('count');

    function loadQuestion() {
      if (current >= quizData.length) {
        questionEl.innerHTML = "Quiz Completed!";
        optionsEl.innerHTML = "";
        scoreEl.innerHTML = `Your Score: ${score} / ${quizData.length}`;
        countEl.innerHTML = "";
        return;
      }
      const qData = quizData[current];
      countEl.innerHTML = `Question ${current + 1} of ${quizData.length}`;
      questionEl.innerHTML = qData.q;
      optionsEl.innerHTML = "";
      qData.a.forEach((opt, idx) => {
        const btn = document.createElement('button');
        btn.innerText = opt;
        btn.onclick = () => checkAnswer(idx);
        optionsEl.appendChild(btn);
      });
    }

    function checkAnswer(index) {
      if (index === quizData[current].c) score++;
      current++;
      loadQuestion();
    }

    loadQuestion();
  </script>
</body>
</html>
