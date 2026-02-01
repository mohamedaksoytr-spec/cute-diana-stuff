<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Falling in Love With Us Again</title>
  <style>
    :root{
      --wine: #4b0f1b;         /* cherry-wine */
      --white: #ffffff;
      --muted: rgba(255,255,255,.75);
      --glass: rgba(255,255,255,.10);
      --glass-2: rgba(255,255,255,.14);
      --border: rgba(255,255,255,.18);
      --shadow: 0 18px 60px rgba(0,0,0,.45);
      --good: #2ecc71;
      --bad: #ff5b5b;
    }

    * { box-sizing: border-box; }
    html, body { height: 100%; }
    body {
      margin: 0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      color: var(--white);
      overflow: hidden; /* prevents scrolling */
      background: radial-gradient(1200px 800px at 20% 10%, #7a1b31 0%, var(--wine) 55%, #24060d 100%);
    }

    /* ========= OPTION A: USE YOUR UPLOADED BACKGROUND IMAGES =========
       Upload these files next to index.html:
       bg-intro.jpg, bg-q1.jpg, bg-q2.jpg, bg-q3.jpg, bg-q4.jpg, bg-done.jpg
    */
    body.bg-intro, body.bg-q1, body.bg-q2, body.bg-q3, body.bg-q4, body.bg-done {
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
    }
    body.bg-intro { background-image: url("bg-intro.jpg"); }
    body.bg-q1    { background-image: url("bg-q1.jpg"); }
    body.bg-q2    { background-image: url("bg-q2.jpg"); }
    body.bg-q3    { background-image: url("bg-q3.jpg"); }
    body.bg-q4    { background-image: url("bg-q4.jpg"); }
    body.bg-done  { background-image: url("bg-done.jpg"); }

    /* Dark overlay so text stays readable on photos */
    .overlay {
      position: fixed;
      inset: 0;
      background: radial-gradient(900px 600px at 20% 10%, rgba(122,27,49,.35) 0%, rgba(75,15,27,.70) 55%, rgba(15,3,6,.78) 100%);
      pointer-events: none;
    }

    .wrap {
      height: 100%;
      display: grid;
      place-items: center;
      padding: 22px;
      position: relative;
      z-index: 1;
    }

    .card {
      width: min(860px, 96vw);
      border-radius: 24px;
      background: linear-gradient(180deg, var(--glass-2), var(--glass));
      border: 1px solid var(--border);
      box-shadow: var(--shadow);
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      overflow: hidden;
      position: relative;
    }

    .card::before{
      content:"";
      position:absolute;
      inset:-2px;
      background: linear-gradient(120deg, rgba(255,255,255,.10), rgba(255,255,255,.02), rgba(255,255,255,.12));
      pointer-events:none;
      mask: linear-gradient(#000, transparent 65%);
      opacity:.85;
    }

    header {
      padding: 26px 26px 0;
    }
    .pill {
      display: inline-flex;
      gap: 10px;
      align-items: center;
      padding: 8px 12px;
      border-radius: 999px;
      background: rgba(255,255,255,.10);
      border: 1px solid rgba(255,255,255,.18);
      font-size: 13px;
      color: var(--muted);
    }
    .dot {
      width: 9px; height: 9px;
      border-radius: 99px;
      background: #ffb3c2;
      box-shadow: 0 0 0 3px rgba(255,179,194,.15);
    }

    h1{
      margin: 14px 0 6px;
      font-size: clamp(26px, 3.2vw, 38px);
      letter-spacing: .2px;
      line-height: 1.12;
    }
    p.sub {
      margin: 0 0 18px;
      color: var(--muted);
      font-size: clamp(14px, 2vw, 16px);
      line-height: 1.5;
    }

    .content {
      padding: 18px 26px 26px;
      display: grid;
      gap: 16px;
    }

    .question-title{
      font-size: clamp(18px, 2.6vw, 24px);
      margin: 0;
    }

    .answers {
      display: grid;
      gap: 12px;
      margin-top: 6px;
    }

    button.choice, button.action {
      appearance: none;
      border: 1px solid rgba(255,255,255,.18);
      background: rgba(255,255,255,.08);
      color: var(--white);
      padding: 14px 14px;
      border-radius: 16px;
      cursor: pointer;
      text-align: left;
      font-size: 16px;
      transition: transform .08s ease, background .2s ease, border-color .2s ease, box-shadow .2s ease;
      box-shadow: 0 10px 28px rgba(0,0,0,.15);
    }

    button.choice:hover, button.action:hover {
      transform: translateY(-1px);
      border-color: rgba(255,255,255,.30);
      background: rgba(255,255,255,.11);
    }

    button.choice:active, button.action:active {
      transform: translateY(0px);
    }

    .row {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
      margin-top: 6px;
    }

    button.action {
      text-align: center;
      font-weight: 700;
      padding: 12px 16px;
      border-radius: 999px;
      background: rgba(255,255,255,.12);
    }
    button.action.primary{
      background: linear-gradient(135deg, #ffffff, #ffd7df);
      color: #3b0b14;
      border: none;
    }

    .feedback {
      min-height: 26px;
      font-size: 15px;
      color: var(--muted);
    }

    .feedback.good { color: rgba(255,255,255,.92); }
    .feedback.bad  { color: rgba(255,220,220,.96); }

    .choice.correct {
      background: rgba(46, 204, 113, .20);
      border-color: rgba(46, 204, 113, .75);
      box-shadow: 0 10px 30px rgba(46, 204, 113, .18);
    }

    .choice.wrong {
      background: rgba(255, 91, 91, .12);
      border-color: rgba(255, 91, 91, .50);
    }

    .footer {
      padding: 0 26px 22px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      color: rgba(255,255,255,.7);
      font-size: 13px;
    }

    .progress {
      display: flex;
      gap: 8px;
      align-items: center;
    }
    .bar {
      width: 10px; height: 10px;
      border-radius: 99px;
      background: rgba(255,255,255,.18);
      border: 1px solid rgba(255,255,255,.20);
    }
    .bar.on { background: rgba(255,255,255,.70); }

    @media (max-width: 520px){
      button.choice { font-size: 15px; }
    }
  </style>
</head>

<body class="bg-intro">
  <div class="overlay"></div>

  <div class="wrap">
    <main class="card" aria-live="polite">
      <header>
        <div class="pill"><span class="dot"></span><span id="topLabel">Quiz of Love</span></div>
        <h1 id="title">Falling in Love With Us Again</h1>
        <p class="sub" id="subtitle">A tiny reminder of how much we fell in love 💌</p>
      </header>

      <section class="content" id="screen"></section>

      <div class="footer">
        <div class="progress" id="progress" aria-label="Progress"></div>
        <div id="hint">Cherry-wine mode: ON 🍒</div>
      </div>
    </main>
  </div>

  <script>
    const BG_CLASSES = {
      intro: "bg-intro",
      q1: "bg-q1",
      q2: "bg-q2",
      q3: "bg-q3",
      q4: "bg-q4",
      done: "bg-done"
    };

    const quiz = [
      {
        key: "q1",
        question: "Question 1: Cutest moment of this relationship?",
        answers: [
          "1- running under rain",
          "2- ship time in bosphour",
          "3- last trip to ukraine",
          "4- this quiz"
        ],
        correctIndex: 3,
        onCorrectText: "Good job 💚 you are doing amazing work love you."
      },
      {
        key: "q2",
        question: "Question 2: How much your boyfriend loves you?",
        answers: [
          "1- soo much",
          "2- you know i love you right?",
          "3- like so much",
          "4- like the universe because it is always expanding"
        ],
        correctIndex: 3,
        onCorrectText: "look your boyfriend never finishes 💚"
      },
      {
        key: "q3",
        question: "Question 3: How happy you are your boyfriend made this?",
        answers: [
          "1- meeh",
          "2- he better to make up for the fight",
          "3- bare minumum",
          "4- like so much"
        ],
        correctIndex: 2,
        onCorrectText: "Bare minimum 😌💚 …and be ready for more of this in our life."
      },
      {
        key: "q4",
        question: "Question 4: What does your boyfriend love most about you?",
        answers: [
          "1- when you try to speak arabic",
          "2- when you try to be funny and can't",
          "3- because you are beautiful and hard to achieve",
          "4- all above except hard to achieve"
        ],
        correctIndex: 3,
        onCorrectText: "Aww you aced exam 💚 good job love you."
      }
    ];

    const screenEl = document.getElementById("screen");
    const progressEl = document.getElementById("progress");
    const topLabelEl = document.getElementById("topLabel");

    function setBodyBg(bgClass){
      document.body.className = "";
      document.body.classList.add(bgClass);
    }

    function renderProgress(completed){
      progressEl.innerHTML = "";
      for(let i=0; i<quiz.length; i++){
        const dot = document.createElement("div");
        dot.className = "bar" + (i < completed ? " on" : "");
        progressEl.appendChild(dot);
      }
    }

    function renderIntro(){
      setBodyBg(BG_CLASSES.intro);
      topLabelEl.textContent = "Quiz of Love";
      renderProgress(0);

      screenEl.innerHTML = `
        <h2 class="question-title">Welcome to Quiz of Love</h2>
        <p class="sub" style="margin:0;">
          Question to make you remember how much we fell in love… are you ready?
        </p>

        <div class="row">
          <button class="action primary" id="yesBtn">Yes 💗</button>
          <button class="action" id="noBtn">Not 😏</button>
        </div>

        <div class="feedback" id="feedback"></div>
      `;

      document.getElementById("yesBtn").addEventListener("click", () => {
        renderQuestion(0);
      });

      document.getElementById("noBtn").addEventListener("click", () => {
        const fb = document.getElementById("feedback");
        fb.className = "feedback bad";
        fb.textContent = "Too late 😌 you’re taking it anyway. Press YES, my love 💗";
      });
    }

    function renderQuestion(index){
      const q = quiz[index];
      setBodyBg(BG_CLASSES[q.key]);
      topLabelEl.textContent = "Falling in Love With Us Again";
      renderProgress(index);

      screenEl.innerHTML = `
        <h2 class="question-title">${q.question}</h2>
        <div class="answers" id="answers"></div>
        <div class="feedback" id="feedback"></div>
        <div class="row">
          <button class="action primary" id="nextBtn" style="display:none;">Next ➜</button>
        </div>
      `;

      const answersWrap = document.getElementById("answers");
      const feedback = document.getElementById("feedback");
      const nextBtn = document.getElementById("nextBtn");
      let solved = false;

      q.answers.forEach((text, i) => {
        const btn = document.createElement("button");
        btn.className = "choice";
        btn.type = "button";
        btn.textContent = text;

        btn.addEventListener("click", () => {
          if (solved) return;

          // remove wrong marks from all choices
          [...answersWrap.querySelectorAll(".choice")].forEach(b => b.classList.remove("wrong"));

          if (i === q.correctIndex) {
            solved = true;
            btn.classList.add("correct");
            feedback.className = "feedback good";
            feedback.textContent = q.onCorrectText;
            nextBtn.style.display = "inline-block";
          } else {
            btn.classList.add("wrong");
            feedback.className = "feedback bad";
            feedback.textContent = "Wrong 😜 choose another answer.";
          }
        });

        answersWrap.appendChild(btn);
      });

      nextBtn.addEventListener("click", () => {
        if (index + 1 < quiz.length) renderQuestion(index + 1);
        else renderDone();
      });
    }

    function renderDone(){
      setBodyBg(BG_CLASSES.done);
      topLabelEl.textContent = "Quiz of Love";
      renderProgress(quiz.length);

      screenEl.innerHTML = `
        <h2 class="question-title">You finished 🥹💗</h2>
        <p class="sub" style="margin:0;">
          I love you. Thanks for playing “Falling in Love With Us Again”.
        </p>

        <div class="row">
          <button class="action primary" id="restartBtn">Play again 🔁</button>
        </div>

        <div class="feedback good" style="margin-top:8px;">
          If you want, I can add more questions, cute animations, music, and a “love score” 😌
        </div>
      `;

      document.getElementById("restartBtn").addEventListener("click", renderIntro);
    }

    renderIntro();
  </script>
</body>
</html>
