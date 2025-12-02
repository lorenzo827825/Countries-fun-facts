<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>World Trivia & Flag Quiz</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    :root {
      --bg: #0f172a;
      --card-bg: #0b1220;
      --card-soft: #020617;
      --accent: #6366f1;
      --accent-soft: rgba(129, 140, 248, 0.2);
      --accent-strong: #4f46e5;
      --text-main: #e5e7eb;
      --text-muted: #9ca3af;
      --border-subtle: rgba(148, 163, 184, 0.4);
      --radius-lg: 18px;
      --radius-md: 12px;
      --radius-pill: 999px;
      --shadow-strong: 0 22px 60px rgba(15, 23, 42, 0.8);
    }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Helvetica, Arial, sans-serif;
      min-height: 100vh;
      background:
        radial-gradient(circle at top left, #1d253b, #020617 55%),
        radial-gradient(circle at bottom right, #0b1220, #020617 70%);
      color: var(--text-main);
      display: flex;
      justify-content: center;
      align-items: flex-start;
      padding: 40px 16px;
    }

    .quiz-wrapper {
      max-width: 960px;
      width: 100%;
      background: radial-gradient(circle at top, #020617, #020617 55%, #020617 100%);
      border-radius: 26px;
      box-shadow: var(--shadow-strong);
      padding: 26px 24px 22px;
      border: 1px solid rgba(148, 163, 184, 0.4);
      position: relative;
      overflow: hidden;
      isolation: isolate;
    }

    .quiz-wrapper::before {
      content: "";
      position: absolute;
      inset: -80px;
      background:
        radial-gradient(circle at 0% 0%, rgba(129, 140, 248, 0.15), transparent 55%),
        radial-gradient(circle at 100% 0%, rgba(45, 212, 191, 0.13), transparent 50%);
      opacity: 0.9;
      pointer-events: none;
      z-index: -1;
    }

    .quiz-header {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: flex-start;
      margin-bottom: 18px;
      gap: 14px;
    }

    .title-block {
      max-width: 580px;
    }

    .title-eyebrow {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-size: 0.78rem;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: #a5b4fc;
      margin-bottom: 6px;
    }

    .title-eyebrow-dot {
      width: 6px;
      height: 6px;
      border-radius: 999px;
      background: linear-gradient(135deg, #22d3ee, #a855f7);
    }

    .title-block h1 {
      font-size: 1.9rem;
      line-height: 1.2;
      letter-spacing: -0.03em;
      margin-bottom: 8px;
      display: inline-flex;
      align-items: center;
      gap: 10px;
    }

    .title-emoji {
      font-size: 1.8rem;
      filter: drop-shadow(0 0 8px rgba(250, 250, 250, 0.3));
    }

    .title-accent-bar {
      width: 82px;
      height: 3px;
      border-radius: 99px;
      background: linear-gradient(90deg, #22c55e, #22d3ee, #a855f7);
      margin-bottom: 7px;
    }

    .title-subline {
      font-size: 0.92rem;
      color: var(--text-muted);
      max-width: 520px;
    }

    .control-panel {
      display: flex;
      flex-direction: column;
      align-items: flex-end;
      gap: 8px;
      min-width: 210px;
    }

    .pill-info {
      font-size: 0.78rem;
      color: #cbd5f5;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: rgba(15, 23, 42, 0.7);
      border: 1px solid rgba(129, 140, 248, 0.4);
      border-radius: 999px;
      padding: 6px 12px;
      backdrop-filter: blur(8px);
    }

    .pill-dot {
      width: 6px;
      height: 6px;
      border-radius: 999px;
      background: #22c55e;
    }

    .btn {
      border: none;
      border-radius: var(--radius-pill);
      padding: 8px 16px;
      font-size: 0.9rem;
      cursor: pointer;
      transition: all 0.2s ease;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-weight: 600;
      user-select: none;
      white-space: nowrap;
    }

    .btn-primary {
      background: linear-gradient(135deg, #6366f1, #22c55e);
      color: #f9fafb;
      box-shadow: 0 12px 30px rgba(79, 70, 229, 0.6);
      border: 1px solid rgba(191, 219, 254, 0.5);
    }

    .btn-primary:hover {
      transform: translateY(-1px);
      filter: brightness(1.05);
    }

    .btn-ghost {
      background: rgba(15, 23, 42, 0.7);
      color: #e5e7eb;
      border: 1px solid rgba(148, 163, 184, 0.6);
      backdrop-filter: blur(8px);
    }

    .quiz-body {
      margin-top: 10px;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .question-card {
      border-radius: var(--radius-md);
      padding: 13px 12px;
      background: #020617;
      border: 1px solid var(--border-subtle);
    }

    .question-top-row {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      margin-bottom: 6px;
    }

    .question-index {
      font-size: 0.78rem;
      font-weight: 600;
      color: #a5b4fc;
      text-transform: uppercase;
      letter-spacing: 0.14em;
    }

    .question-text {
      font-size: 0.97rem;
      margin-bottom: 5px;
      line-height: 1.35;
    }

    .options-list {
      list-style: none;
      margin-top: 4px;
      display: flex;
      flex-direction: column;
      gap: 3px;
    }

    .option-label {
      display: flex;
      align-items: center;
      gap: 7px;
      padding: 6px 7px;
      border-radius: 10px;
      cursor: pointer;
      transition: background 0.16s;
    }

    .option-label:hover {
      background: rgba(15, 23, 42, 0.65);
    }

    .option-letter {
      font-weight: 600;
      font-size: 0.78rem;
      padding: 1px 6px;
      border-radius: 999px;
      background: rgba(148, 163, 184, 0.3);
    }

    .result-box {
      margin-top: 12px;
      padding-top: 10px;
      border-top: 1px dashed rgba(75, 85, 99, 0.9);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .score-pill {
      padding: 3px 9px;
      border-radius: 999px;
      border: 1px solid rgba(148, 163, 184, 0.8);
    }

    .pill-correct {
      padding: 2px 8px;
      border-radius: 999px;
      background: rgba(21, 128, 61, 0.22);
      border: 1px solid rgba(34, 197, 94, 0.85);
    }

    .pill-wrong {
      padding: 2px 8px;
      border-radius: 999px;
      background: rgba(127, 29, 29, 0.42);
      border: 1px solid rgba(248, 113, 113, 0.9);
    }
  </style>
</head>

<body>
  <div class="quiz-wrapper">
    <div class="quiz-header">
      <div class="title-block">
        <div class="title-eyebrow">
          <span class="title-eyebrow-dot"></span>
          <span>World knowledge challenge</span>
        </div>
        <h1><span class="title-emoji">🌍</span>World Trivia & Flag Quiz</h1>
        <div class="title-accent-bar"></div>
        <p class="title-subline">Try 5 random questions each round. Earn 1 point per correct answer!</p>
      </div>
      <div class="control-panel">
        <button class="btn btn-ghost" id="refreshBtn">🔄 New 5 Questions</button>
      </div>
    </div>

    <div class="quiz-body" id="quizContainer"></div>

    <div class="result-box">
      <div id="resultText" class="result-text">
        Score: <span class="score-pill">– / 5</span>
      </div>
      <button class="btn btn-primary" id="submitBtn">Submit</button>
    </div>
  </div>

<script>
    const FACT_QUESTIONS = [
      {
        id: 1,
        type: "fact",
        question: "Which country has the northernmost permanent settlement in the world (Alert)?",
        options: ["Russia", "Canada", "Norway", "Greenland (Denmark)"],
        answer: 1
      },
      {
        id: 2,
        type: "fact",
        question: "Which country is completely surrounded by South Africa?",
        options: ["Botswana", "Eswatini", "Namibia", "Lesotho"],
        answer: 3
      },
      {
        id: 3,
        type: "fact",
        question: "Which country has three official capital cities: Pretoria, Bloemfontein, and Cape Town?",
        options: ["Australia", "South Africa", "Brazil", "India"],
        answer: 1
      },
      {
        id: 4,
        type: "fact",
        question: "Which is the only country that is doubly landlocked in Europe?",
        options: ["Switzerland", "Austria", "Liechtenstein", "Czech Republic"],
        answer: 2
      },
      {
        id: 5,
        type: "fact",
        question: "Which country’s territory includes the remote Easter Island (Rapa Nui)?",
        options: ["Chile", "Peru", "Mexico", "New Zealand"],
        answer: 0
      },
      {
        id: 6,
        type: "fact",
        question: "The enclave of Ceuta on the African coast belongs to which European country?",
        options: ["Portugal", "Spain", "France", "Italy"],
        answer: 1
      },
      {
        id: 7,
        type: "fact",
        question: "Which country has the world’s lowest-lying capital city, below sea level?",
        options: ["Maldives", "Netherlands", "Azerbaijan", "Qatar"],
        answer: 2
      },
      {
        id: 8,
        type: "fact",
        question: "Which Asian country has never been colonised in the modern era?",
        options: ["Thailand", "Vietnam", "Philippines", "Malaysia"],
        answer: 0
      },
      {
        id: 9,
        type: "fact",
        question: "Which country has the highest number of time zones (including overseas territories)?",
        options: ["United States", "France", "Russia", "United Kingdom"],
        answer: 1
      },
      {
        id: 10,
        type: "fact",
        question: "Which country is home to the city of Timbuktu?",
        options: ["Niger", "Mali", "Chad", "Burkina Faso"],
        answer: 1
      },
      {
        id: 11,
        type: "fact",
        question: "Which landlocked country has a navy that operates mainly on Lake Titicaca?",
        options: ["Paraguay", "Bolivia", "Mongolia", "Kazakhstan"],
        answer: 1
      },
      {
        id: 12,
        type: "fact",
        question: "Transnistria is a breakaway region mainly recognised as part of which country?",
        options: ["Romania", "Ukraine", "Moldova", "Russia"],
        answer: 2
      },
      {
        id: 13,
        type: "fact",
        question: "Which country has the shortest coastline in the world (about 20 km)?",
        options: ["Monaco", "Bosnia and Herzegovina", "Slovenia", "Jordan"],
        answer: 1
      },
      {
        id: 14,
        type: "fact",
        question: "Which country completely surrounds the microstate of San Marino?",
        options: ["Switzerland", "France", "Italy", "Austria"],
        answer: 2
      },
      {
        id: 15,
        type: "fact",
        question: "Which country’s official name includes the phrase “Oriental Republic”?",
        options: ["Uruguay", "Paraguay", "Ecuador", "Colombia"],
        answer: 0
      },
      {
        id: 16,
        type: "fact",
        question: "Which country used to be known as Ceylon until 1972?",
        options: ["Myanmar", "Sri Lanka", "Bangladesh", "Laos"],
        answer: 1
      },
      {
        id: 17,
        type: "fact",
        question: "Which two continents does the country of Kazakhstan span?",
        options: ["Asia and Africa", "Asia and Europe", "Europe and Africa", "Europe and South America"],
        answer: 1
      },
      {
        id: 18,
        type: "fact",
        question: "The historic region of Borneo is shared by Indonesia, Brunei and which other country?",
        options: ["Malaysia", "Philippines", "Singapore", "Thailand"],
        answer: 0
      },
      {
        id: 19,
        type: "fact",
        question: "Which country is the only one that is also a continent?",
        options: ["Australia", "Greenland", "Argentina", "South Africa"],
        answer: 0
      },
      {
        id: 20,
        type: "fact",
        question: "Which African country is completely surrounded by Senegal except for its coastline?",
        options: ["Gambia", "Guinea-Bissau", "Guinea", "Sierra Leone"],
        answer: 0
      },
      {
        id: 21,
        type: "fact",
        question: "Which country’s capital is Ulaanbaatar?",
        options: ["Mongolia", "Kyrgyzstan", "Turkmenistan", "Uzbekistan"],
        answer: 0
      },
      {
        id: 22,
        type: "fact",
        question: "Which country has the world’s southernmost city with more than 50,000 people (Ushuaia)?",
        options: ["Chile", "Argentina", "New Zealand", "South Africa"],
        answer: 1
      },
      {
        id: 23,
        type: "fact",
        question: "Which European country has the highest average elevation?",
        options: ["Austria", "Switzerland", "Andorra", "Montenegro"],
        answer: 1
      },
      {
        id: 24,
        type: "fact",
        question: "Which country’s official language is Amharic?",
        options: ["Eritrea", "Kenya", "Ethiopia", "Sudan"],
        answer: 2
      },
      {
        id: 25,
        type: "fact",
        question: "Which country is home to Lake Baikal, the deepest freshwater lake in the world?",
        options: ["Russia", "Canada", "United States", "China"],
        answer: 0
      },
      {
        id: 26,
        type: "fact",
        question: "Which Middle Eastern country has its de facto capital in Tel Aviv for most embassies?",
        options: ["Jordan", "Israel", "Lebanon", "Syria"],
        answer: 1
      },
      {
        id: 27,
        type: "fact",
        question: "Which country has the city of Vladivostok as a major Pacific port?",
        options: ["Japan", "China", "Russia", "South Korea"],
        answer: 2
      },
      {
        id: 28,
        type: "fact",
        question: "Which country’s national currency is the baht?",
        options: ["Thailand", "Laos", "Cambodia", "Vietnam"],
        answer: 0
      },
      {
        id: 29,
        type: "fact",
        question: "Which country controls the island of Greenland?",
        options: ["Iceland", "Norway", "Denmark", "Canada"],
        answer: 2
      },
      {
        id: 30,
        type: "fact",
        question: "Which country has Kigali as its capital city?",
        options: ["Burundi", "Rwanda", "Uganda", "Tanzania"],
        answer: 1
      },
      {
        id: 31,
        type: "fact",
        question: "Which country is famous for the historical region of Transylvania?",
        options: ["Hungary", "Romania", "Serbia", "Bulgaria"],
        answer: 1
      },
      {
        id: 32,
        type: "fact",
        question: "Which country has the largest population in Africa?",
        options: ["Egypt", "Ethiopia", "Nigeria", "South Africa"],
        answer: 2
      },
      {
        id: 33,
        type: "fact",
        question: "Which landlocked Asian country uses the tugrik as its currency?",
        options: ["Laos", "Mongolia", "Nepal", "Bhutan"],
        answer: 1
      },
      {
        id: 34,
        type: "fact",
        question: "Which country has the only national flag that is not rectangular?",
        options: ["Switzerland", "Vatican City", "Nepal", "Bhutan"],
        answer: 2
      },
      {
        id: 35,
        type: "fact",
        question: "Which country is home to the Danakil Depression, one of the hottest places on Earth?",
        options: ["Ethiopia", "Saudi Arabia", "Oman", "Iran"],
        answer: 0
      },
      {
        id: 36,
        type: "fact",
        question: "Which country was formerly known as Burma?",
        options: ["Myanmar", "Bangladesh", "Cambodia", "Sri Lanka"],
        answer: 0
      },
      {
        id: 37,
        type: "fact",
        question: "Which European microstate lies between France and Spain in the Pyrenees?",
        options: ["Andorra", "Monaco", "Liechtenstein", "San Marino"],
        answer: 0
      },
      {
        id: 38,
        type: "fact",
        question: "Which country shares the world’s longest international land border with the United States?",
        options: ["Mexico", "Canada", "Russia", "Cuba"],
        answer: 1
      },
      {
        id: 39,
        type: "fact",
        question: "Which country’s capital was moved from Almaty to Astana (now called Nur-Sultan and again Astana)?",
        options: ["Kazakhstan", "Uzbekistan", "Turkmenistan", "Kyrgyzstan"],
        answer: 0
      },
      {
        id: 40,
        type: "fact",
        question: "Which country’s name literally means “Land of the Afghans”?",
        options: ["Pakistan", "Afghanistan", "Kazakhstan", "Uzbekistan"],
        answer: 1
      },
      {
        id: 41,
        type: "fact",
        question: "Which country has the largest number of Portuguese speakers?",
        options: ["Portugal", "Brazil", "Angola", "Mozambique"],
        answer: 1
      },
      {
        id: 42,
        type: "fact",
        question: "Which country has a city named Tangier that faces the Strait of Gibraltar?",
        options: ["Spain", "Morocco", "Algeria", "Tunisia"],
        answer: 1
      },
      {
        id: 43,
        type: "fact",
        question: "Which country is home to Mount Kilimanjaro?",
        options: ["Kenya", "Tanzania", "Ethiopia", "Uganda"],
        answer: 1
      },
      {
        id: 44,
        type: "fact",
        question: "Which country was created in 2011, becoming the world’s newest widely recognised state?",
        options: ["Eritrea", "Timor-Leste", "South Sudan", "Kosovo"],
        answer: 2
      },
      {
        id: 45,
        type: "fact",
        question: "Which country has Ljubljana as its capital?",
        options: ["Slovakia", "Slovenia", "Croatia", "Serbia"],
        answer: 1
      },
      {
        id: 46,
        type: "fact",
        question: "Which island country in the Indian Ocean is famous for its unique biodiversity and lemurs?",
        options: ["Mauritius", "Madagascar", "Sri Lanka", "Seychelles"],
        answer: 1
      },
      {
        id: 47,
        type: "fact",
        question: "Which European country has the city of Bruges, known for its canals and medieval architecture?",
        options: ["Netherlands", "Belgium", "Germany", "France"],
        answer: 1
      },
      {
        id: 48,
        type: "fact",
        question: "Which country’s capital is Yerevan?",
        options: ["Georgia", "Azerbaijan", "Armenia", "Belarus"],
        answer: 2
      },
      {
        id: 49,
        type: "fact",
        question: "Which country has Suva as its capital city?",
        options: ["Fiji", "Samoa", "Vanuatu", "Tonga"],
        answer: 0
      },
      {
        id: 50,
        type: "fact",
        question: "Which African island nation lies off the coast of Mozambique in the Indian Ocean?",
        options: ["Comoros", "Cape Verde", "São Tomé and Príncipe", "Seychelles"],
        answer: 0
      }
    ];

    const FLAG_QUESTIONS = [
      {
        id: 51,
        type: "flag",
        question: "Which country uses this flag? 🇮🇩",
        options: ["Poland", "Indonesia", "Monaco", "Singapore"],
        answer: 1
      },
      {
        id: 52,
        type: "flag",
        question: "Which country uses this flag? 🇲🇨",
        options: ["Indonesia", "Monaco", "Austria", "Peru"],
        answer: 1
      },
      {
        id: 53,
        type: "flag",
        question: "Which country uses this flag? 🇨🇮",
        options: ["Ireland", "Ivory Coast", "India", "Niger"],
        answer: 1
      },
      {
        id: 54,
        type: "flag",
        question: "Which country uses this flag? 🇮🇪",
        options: ["Ivory Coast", "Italy", "Ireland", "Hungary"],
        answer: 2
      },
      {
        id: 55,
        type: "flag",
        question: "Which country uses this flag? 🇷🇴",
        options: ["Chad", "Moldova", "Romania", "Andorra"],
        answer: 2
      },
      {
        id: 56,
        type: "flag",
        question: "Which country uses this flag? 🇹🇩",
        options: ["Romania", "Chad", "Mali", "Guinea"],
        answer: 1
      },
      {
        id: 57,
        type: "flag",
        question: "Which country uses this flag? 🇲🇱",
        options: ["Senegal", "Mali", "Cameroon", "Guinea"],
        answer: 1
      },
      {
        id: 58,
        type: "flag",
        question: "Which country uses this flag? 🇬🇳",
        options: ["Cameroon", "Mali", "Guinea", "Benin"],
        answer: 2
      },
      {
        id: 59,
        type: "flag",
        question: "Which country uses this flag? 🇳🇪",
        options: ["India", "Niger", "Ireland", "Ivory Coast"],
        answer: 1
      },
      {
        id: 60,
        type: "flag",
        question: "Which country uses this flag? 🇮🇳",
        options: ["Niger", "Ireland", "India", "Mexico"],
        answer: 2
      },
      {
        id: 61,
        type: "flag",
        question: "Which country uses this flag? 🇱🇹",
        options: ["Lithuania", "Bolivia", "Ghana", "Benin"],
        answer: 0
      },
      {
        id: 62,
        type: "flag",
        question: "Which country uses this flag? 🇧🇴",
        options: ["Bolivia", "Ghana", "Lithuania", "Guinea-Bissau"],
        answer: 0
      },
      {
        id: 63,
        type: "flag",
        question: "Which country uses this flag? 🇧🇯",
        options: ["Togo", "Benin", "Cameroon", "Guinea"],
        answer: 1
      },
      {
        id: 64,
        type: "flag",
        question: "Which country uses this flag? 🇬🇭",
        options: ["Guinea", "Ghana", "Bolivia", "Senegal"],
        answer: 1
      },
      {
        id: 65,
        type: "flag",
        question: "Which country uses this flag? 🇱🇻",
        options: ["Austria", "Latvia", "Denmark", "Poland"],
        answer: 1
      },
      {
        id: 66,
        type: "flag",
        question: "Which country uses this flag? 🇦🇹",
        options: ["Austria", "Latvia", "Indonesia", "Denmark"],
        answer: 0
      },
      {
        id: 67,
        type: "flag",
        question: "Which country uses this flag? 🇩🇰",
        options: ["Switzerland", "Denmark", "Norway", "Iceland"],
        answer: 1
      },
      {
        id: 68,
        type: "flag",
        question: "Which country uses this flag? 🇳🇴",
        options: ["Sweden", "Finland", "Norway", "Iceland"],
        answer: 2
      },
      {
        id: 69,
        type: "flag",
        question: "Which country uses this flag? 🇸🇪",
        options: ["Sweden", "Finland", "Ukraine", "Kazakhstan"],
        answer: 0
      },
      {
        id: 70,
        type: "flag",
        question: "Which country uses this flag? 🇺🇦",
        options: ["Sweden", "Ukraine", "Kazakhstan", "Romania"],
        answer: 1
      },
      {
        id: 71,
        type: "flag",
        question: "Which country uses this flag? 🇰🇿",
        options: ["Kazakhstan", "Ukraine", "Uzbekistan", "Mongolia"],
        answer: 0
      },
      {
        id: 72,
        type: "flag",
        question: "Which country uses this flag? 🇺🇿",
        options: ["Kazakhstan", "Uzbekistan", "Turkmenistan", "Kyrgyzstan"],
        answer: 1
      },
      {
        id: 73,
        type: "flag",
        question: "Which country uses this flag? 🇸🇱",
        options: ["Sierra Leone", "Somalia", "Slovenia", "Slovakia"],
        answer: 0
      },
      {
        id: 74,
        type: "flag",
        question: "Which country uses this flag? 🇸🇮",
        options: ["Slovakia", "Slovenia", "Russia", "Serbia"],
        answer: 1
      },
      {
        id: 75,
        type: "flag",
        question: "Which country uses this flag? 🇸🇰",
        options: ["Slovenia", "Slovakia", "Serbia", "Russia"],
        answer: 1
      },
      {
        id: 76,
        type: "flag",
        question: "Which country uses this flag? 🇷🇺",
        options: ["Russia", "Serbia", "Slovakia", "Slovenia"],
        answer: 0
      },
      {
        id: 77,
        type: "flag",
        question: "Which country uses this flag? 🇷🇸",
        options: ["Russia", "Croatia", "Serbia", "Slovenia"],
        answer: 2
      },
      {
        id: 78,
        type: "flag",
        question: "Which country uses this flag? 🇭🇷",
        options: ["Serbia", "Croatia", "Slovakia", "Slovenia"],
        answer: 1
      },
      {
        id: 79,
        type: "flag",
        question: "Which country uses this flag? 🇵🇦",
        options: ["Cuba", "Panama", "Puerto Rico", "Chile"],
        answer: 1
      },
      {
        id: 80,
        type: "flag",
        question: "Which country uses this flag? 🇵🇷",
        options: ["Cuba", "Chile", "Puerto Rico", "Panama"],
        answer: 2
      },
      {
        id: 81,
        type: "flag",
        question: "Which country uses this flag? 🇨🇺",
        options: ["Cuba", "Puerto Rico", "Chile", "Dominican Republic"],
        answer: 0
      },
      {
        id: 82,
        type: "flag",
        question: "Which country uses this flag? 🇩🇴",
        options: ["Cuba", "Dominican Republic", "Haiti", "Panama"],
        answer: 1
      },
      {
        id: 83,
        type: "flag",
        question: "Which country uses this flag? 🇭🇹",
        options: ["Dominican Republic", "Haiti", "Cuba", "Belize"],
        answer: 1
      },
      {
        id: 84,
        type: "flag",
        question: "Which country uses this flag? 🇧🇧",
        options: ["Bahamas", "Barbados", "Belize", "Bermuda"],
        answer: 1
      },
      {
        id: 85,
        type: "flag",
        question: "Which country uses this flag? 🇧🇸",
        options: ["Bahamas", "Barbados", "Belize", "Botswana"],
        answer: 0
      },
      {
        id: 86,
        type: "flag",
        question: "Which country uses this flag? 🇧🇼",
        options: ["Belize", "Botswana", "Bahamas", "Barbados"],
        answer: 1
      },
      {
        id: 87,
        type: "flag",
        question: "Which country uses this flag? 🇳🇦",
        options: ["Namibia", "South Africa", "Botswana", "Kenya"],
        answer: 0
      },
      {
        id: 88,
        type: "flag",
        question: "Which country uses this flag? 🇿🇦",
        options: ["South Africa", "Zimbabwe", "Zambia", "Namibia"],
        answer: 0
      },
      {
        id: 89,
        type: "flag",
        question: "Which country uses this flag? 🇿🇼",
        options: ["Zambia", "Zimbabwe", "Mozambique", "Malawi"],
        answer: 1
      },
      {
        id: 90,
        type: "flag",
        question: "Which country uses this flag? 🇿🇲",
        options: ["Zimbabwe", "Zambia", "Mozambique", "Malawi"],
        answer: 1
      },
      {
        id: 91,
        type: "flag",
        question: "Which country uses this flag? 🇲🇺",
        options: ["Mauritius", "Madagascar", "Maldives", "Malta"],
        answer: 0
      },
      {
        id: 92,
        type: "flag",
        question: "Which country uses this flag? 🇲🇬",
        options: ["Madagascar", "Mauritius", "Maldives", "Mozambique"],
        answer: 0
      },
      {
        id: 93,
        type: "flag",
        question: "Which country uses this flag? 🇲🇻",
        options: ["Malta", "Maldives", "Mauritius", "Micronesia"],
        answer: 1
      },
      {
        id: 94,
        type: "flag",
        question: "Which country uses this flag? 🇲🇹",
        options: ["Malta", "Monaco", "Madagascar", "Maldives"],
        answer: 0
      },
      {
        id: 95,
        type: "flag",
        question: "Which country uses this flag? 🇰🇭",
        options: ["Laos", "Cambodia", "Thailand", "Vietnam"],
        answer: 1
      },
      {
        id: 96,
        type: "flag",
        question: "Which country uses this flag? 🇱🇦",
        options: ["Laos", "Cambodia", "Thailand", "Myanmar"],
        answer: 0
      },
      {
        id: 97,
        type: "flag",
        question: "Which country uses this flag? 🇸🇾",
        options: ["Iraq", "Syria", "Yemen", "Jordan"],
        answer: 1
      },
      {
        id: 98,
        type: "flag",
        question: "Which country uses this flag? 🇾🇪",
        options: ["Iraq", "Syria", "Yemen", "Jordan"],
        answer: 2
      },
      {
        id: 99,
        type: "flag",
        question: "Which country uses this flag? 🇦🇪",
        options: ["Kuwait", "United Arab Emirates", "Jordan", "Oman"],
        answer: 1
      },
      {
        id: 100,
        type: "flag",
        question: "Which country uses this flag? 🇴🇲",
        options: ["Oman", "United Arab Emirates", "Kuwait", "Bahrain"],
        answer: 0
      }
    ];

const QUESTION_BANK = [...FACT_QUESTIONS, ...FLAG_QUESTIONS];
const LETTERS = ["A", "B", "C", "D"];

const quizContainer = document.getElementById("quizContainer");
const submitBtn = document.getElementById("submitBtn");
const refreshBtn = document.getElementById("refreshBtn");
const resultText = document.getElementById("resultText");

let currentQuestions = [];

function shuffle(arr) {
  for (let i = arr.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [arr[i], arr[j]] = [arr[j], arr[i]];
  }
  return arr;
}

function pickNewQuestions() {
  const indices = shuffle([...Array(QUESTION_BANK.length).keys()]);
  currentQuestions = indices.slice(0, 5).map(i => QUESTION_BANK[i]);
  renderQuestions();
  clearOverallResult();
}

function renderQuestions() {
  quizContainer.innerHTML = "";
  currentQuestions.forEach((q, idx) => {
    const card = document.createElement("div");
    card.className = "question-card";
    card.dataset.index = idx;

    const html = `
      <div class="question-top-row">
        <div class="question-index">QUESTION ${idx + 1}</div>
      </div>
      <div class="question-text">${q.question}</div>
      <ul class="options-list">
      ${q.options
        .map((opt, i) => `
        <li>
          <label class="option-label">
            <input type="radio" name="q${idx}" value="${i}" />
            <span class="option-letter">${LETTERS[i]}</span>
            <span>${opt}</span>
          </label>
        </li>
      `)
        .join("")}
      </ul>
    `;
    card.innerHTML = html;
    quizContainer.appendChild(card);
  });
}

function clearPerQuestionPills() {
  document.querySelectorAll(".pill-correct, .pill-wrong").forEach(e => e.remove());
}

function clearOverallResult() {
  resultText.innerHTML = `Score: <span class="score-pill">– / 5</span>`;
}

function gradeQuiz() {
  clearPerQuestionPills();
  let score = 0;

  currentQuestions.forEach((q, idx) => {
    const selected = document.querySelector(`input[name="q${idx}"]:checked`);
    const card = document.querySelector(`.question-card[data-index="${idx}"]`);
    const topRow = card.querySelector(".question-top-row");

    const pill = document.createElement("span");

    if (selected && Number(selected.value) === q.answer) {
      score++;
      pill.className = "pill-correct";
      pill.textContent = "✔ Correct";
    } else {
      pill.className = "pill-wrong";
      pill.textContent = `✖ Wrong (correct: ${LETTERS[q.answer]}. ${q.options[q.answer]})`;
    }

    topRow.appendChild(pill);
  });

  resultText.innerHTML = `
    Score: <span class="score-pill">${score} / ${currentQuestions.length}</span>
  `;
}

submitBtn.addEventListener("click", gradeQuiz);
refreshBtn.addEventListener("click", pickNewQuestions);

pickNewQuestions();
</script>

</body>
</html>
