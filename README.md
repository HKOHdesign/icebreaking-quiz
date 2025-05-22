<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>생기부 작성 퀴즈</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap');

    body {
      font-family: 'Noto Sans KR', sans-serif;
      background: linear-gradient(to bottom right, #7F7FD5, #86A8E7, #91EAE4);
      margin: 0;
      padding: 0;
      color: #333;
    }
    header {
      text-align: center;
      padding: 30px 20px 20px;
    }
    header h1 {
      font-size: 2.2rem;
      color: #fff;
      text-shadow: 1px 1px 4px rgba(0,0,0,0.3);
    }
    .quiz-container {
      max-width: 800px;
      margin: 20px auto;
      background: #ffffffcc;
      border-radius: 20px;
      padding: 30px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.15);
    }
    .question-page {
      display: none;
    }
    .question-page.active {
      display: block;
    }
    .question h3 {
      color: #3f51b5;
    }
    .options button {
      display: block;
      width: 100%;
      margin: 8px 0;
      padding: 14px;
      border: none;
      border-radius: 8px;
      background: #7f7fd5;
      color: #fff;
      font-size: 1rem;
      cursor: pointer;
      transition: 0.2s;
    }
    .options button.correct {
      background: #4caf50;
    }
    .options button.incorrect {
      background: #f44336;
    }
    .answer {
      margin-top: 16px;
      padding: 14px;
      background: #e0e7ff;
      border-left: 4px solid #3f51b5;
      border-radius: 8px;
      display: none;
      color: #1a237e;
      font-weight: bold;
    }
    .nav-btns {
      margin-top: 30px;
      text-align: center;
    }
    .nav-btns button {
      margin: 5px;
      padding: 14px 28px;
      border: none;
      border-radius: 30px;
      background: #5a55ae;
      color: #fff;
      cursor: pointer;
      font-size: 1rem;
      transition: 0.2s;
    }
    .nav-btns button:hover {
      background: #3f3c91;
    }
    .summary-container {
      text-align: center;
      display: none;
      color: #3e3c91;
    }
    .summary-container h3 {
      margin-top: 0;
      color: #3f51b5;
    }
    .summary-container ul {
      list-style: none;
      padding: 0;
    }
    .summary-container li {
      margin: 8px 0;
      padding: 8px;
      background: #ffffff;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.05);
    }
  </style>
</head>
<body>

  <header>
    <h1>생기부 작성 퀴즈</h1>
  </header>

  <div class="quiz-container" id="quiz-container"></div>

  <script>
    const quizData = [
      {
        question: "1️⃣ 다음 중 생기부 기재 시 가장 중요하게 고려해야 할 학생의 역량은?",
        options: [
          "① 시험 점수를 꾸준히 90점 이상 받는 역량",
          "② 교사의 지시를 묵묵히 따르는 역량",
          "③ 주어진 과제를 주도적으로 탐구하고 해결하는 역량",
          "④ 친구들과 싸우지 않고 사이좋게 지내는 역량"
        ],
        correct: 2
      },
      {
        question: "2️⃣ 세특 작성 시 지양해야 할 표현은?",
        options: [
          "① 수업 시간 내내 집중하며 발표에 적극 참여함",
          "② AI 보고서 작성하며 심화 탐구 능력을 보여줌",
          "③ 리더십 발휘해 우수한 결과를 도출함",
          "④ 수학 경시대회 수상으로 재능이 뛰어남"
        ],
        correct: 3
      },
      {
        question: "3️⃣ 생기부 내용이 학생과 다를 때 가장 먼저 할 일은?",
        options: [
          "① 학생에게 '이게 너라고?' 묻는다",
          "② 동료 교사에게 보여준다",
          "③ 학생의 태도와 활동을 유심히 관찰한다",
          "④ 학생 의견만 전적으로 반영한다"
        ],
        correct: 2
      },
      {
        question: "4️⃣ 독서활동상황 도서 선정 시 적절한 방법은?",
        options: [
          "① 독후감 강요",
          "② 협박",
          "③ 진로와 연결해 설득, 활동 연계",
          "④ 몰래 책 바꾸기"
        ],
        correct: 2
      },
      {
        question: "5️⃣ 창의적 체험활동 특기사항에 적절한 내용은?",
        options: [
          "① 급식실 줄서기",
          "② 싸우지 않고 행사 마침",
          "③ 동아리에서 갈등 중재, 아이디어 제시",
          "④ 쉬는 시간마다 잠"
        ],
        correct: 2
      },
      {
        question: "6️⃣ 학생이 '게으르다'고 말할 때 교사의 적절한 반응은?",
        options: [
          "① 단호하게 '아니다'",
          "② '다음엔 사실대로 쓸게'",
          "③ '왜 그렇게 느끼는지' 대화하며 이해 돕기",
          "④ 부모님께 전화"
        ],
        correct: 2
      },
      {
        question: "7️⃣ 생기부 작성 시 가장 중요하게 생각할 점은?",
        options: [
          "① 글자 수 채우기",
          "② 긍정적인 내용만 기재",
          "③ 성장과 변화, 특성을 구체적으로 기록",
          "④ 민원 안 들을 무난한 내용"
        ],
        correct: 2
      }
    ];

    let currentPage = 0;
    let score = 0;
    const quizContainer = document.getElementById('quiz-container');

    function renderPage() {
      if (currentPage >= quizData.length) {
        showSummary();
        return;
      }
      const q = quizData[currentPage];
      quizContainer.innerHTML = `
        <div class="question-page active">
          <div class="question">
            <h3>${q.question}</h3>
            <div class="options">
              ${q.options.map((opt, i) => `<button onclick="selectAnswer(this, ${i})">${opt}</button>`).join('')}
            </div>
            <div class="answer">정답: ${q.options[q.correct]}</div>
          </div>
          <div class="nav-btns">
            ${currentPage > 0 ? '<button onclick="prevPage()">이전</button>' : ''}
            <button onclick="showAnswer()">정답 보기</button>
            ${currentPage < quizData.length-1 ? '<button onclick="nextPage()">다음</button>' : '<button onclick="showSummary()">결과 보기</button>'}
          </div>
        </div>
      `;
    }

    function selectAnswer(btn, idx) {
      const q = quizData[currentPage];
      const buttons = document.querySelectorAll('.options button');
      buttons.forEach(b => b.disabled = true);
      if (idx === q.correct) {
        btn.classList.add('correct');
        score++;
      } else {
        btn.classList.add('incorrect');
        buttons[q.correct].classList.add('correct');
      }
    }

    function showAnswer() {
      document.querySelector('.answer').style.display = 'block';
    }

    function nextPage() {
      currentPage++;
      renderPage();
    }

    function prevPage() {
      currentPage--;
      renderPage();
    }

    function showSummary() {
      quizContainer.innerHTML = `
        <div class="summary-container" style="display:block">
          <h3>📖 정답 요약 & 점수</h3>
          <ul>
            ${quizData.map((q, i) => `<li>${q.question.slice(0,3)} ${q.options[q.correct]}</li>`).join('')}
          </ul>
          <h3>🎉 당신의 점수: ${score} / ${quizData.length}</h3>
          <div class="nav-btns">
            <button onclick="restartQuiz()">처음으로</button>
          </div>
        </div>
      `;
    }

    function restartQuiz() {
      currentPage = 0;
      score = 0;
      renderPage();
    }

    renderPage();
  </script>

</body>
</html>
