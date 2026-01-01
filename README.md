<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Minna no Nihongo - Night Sky Flashcards</title>
    <style>
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }

      body {
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        min-height: 100vh;
        color: #000;
        overflow-x: hidden;
        background: #000;
        position: relative;
      }

      /* Night Sky Background - Blue + Black Sky View (REMOVED FULL BLACK) */
      .sky-bg {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: -2;
        background:
                /* Multiple blue nebula layers for realistic sky */ radial-gradient(
            ellipse 80% 50% at 20% 30%,
            rgba(0, 50, 150, 0.6) 0%,
            transparent 50%
          ),
          radial-gradient(
            ellipse 60% 40% at 80% 70%,
            rgba(100, 150, 255, 0.4) 0%,
            transparent 50%
          ),
          radial-gradient(
            ellipse 50% 30% at 40% 20%,
            rgba(0, 100, 200, 0.5) 0%,
            transparent 50%
          ),
          /* Deep blue-black gradient instead of pure black */
            linear-gradient(
              135deg,
              #0a0a2e 0%,
              #1a1a4e 30%,
              #0c1445 70%,
              #000428 100%
            );
      }

      /* Animated DOUBLE SIZE GOLDEN Stars - BRIGHTER */
      .stars {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: -1;
      }

      .star {
        position: absolute;
        /* GOLDEN gradient instead of white */
        background: linear-gradient(45deg, #ffd700, #ffed4e, #fff);
        border-radius: 50%;
        animation: fall linear infinite;
        /* MASSIVE golden glow - 3 layers */
        box-shadow: 0 0 20px #ffd700, 0 0 40px #ffed4e,
          0 0 60px rgba(255, 215, 0, 0.5),
          inset 0 0 10px rgba(255, 255, 255, 0.8);
        border: 1px solid rgba(255, 255, 255, 0.9);
      }

      /* DOUBLE SIZE - 8px minimum */
      .star {
        width: 8px !important;
        height: 8px !important;
      }

      .star:nth-child(odd) {
        animation-duration: 18s;
        box-shadow: 0 0 30px #ffd700, 0 0 60px #ffed4e,
          0 0 90px rgba(255, 215, 0, 0.6);
      }

      .star:nth-child(even) {
        animation-duration: 25s;
        box-shadow: 0 0 25px #ffd700, 0 0 50px #ffed4e,
          0 0 80px rgba(255, 215, 0, 0.4);
      }

      @keyframes fall {
        0% {
          transform: translateY(-100vh) rotate(0deg) scale(0.8);
          opacity: 0.8;
        }

        10% {
          opacity: 1;
        }

        90% {
          opacity: 1;
        }

        100% {
          transform: translateY(100vh) rotate(720deg) scale(1.2);
          opacity: 0;
        }
      }

      /* Milky Way Effect */
      .milky-way {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: -1;
        background: radial-gradient(
            ellipse at 10% 20%,
            rgba(255, 215, 0, 0.03) 0%,
            transparent 40%
          ),
          radial-gradient(
            ellipse at 90% 80%,
            rgba(173, 216, 230, 0.02) 0%,
            transparent 40%
          ),
          radial-gradient(
            ellipse at 30% 90%,
            rgba(255, 215, 0, 0.02) 0%,
            transparent 40%
          );
        animation: milkyWayDrift 40s linear infinite;
      }

      @keyframes milkyWayDrift {
        0% {
          transform: translateX(0) rotate(0deg);
        }

        100% {
          transform: translateX(-5%) rotate(1deg);
        }
      }

      /* Main Container - Enhanced glass effect */
      .container {
        max-width: 1000px;
        margin: 2rem auto;
        background: rgba(15, 20, 50, 0.9);
        backdrop-filter: blur(25px);
        border-radius: 25px;
        box-shadow: 0 30px 60px rgba(0, 20, 80, 0.6),
          inset 0 1px 0 rgba(255, 255, 255, 0.15);
        overflow: hidden;
        border: 1px solid rgba(100, 150, 255, 0.3);
        position: relative;
        z-index: 10;
      }

      /* ALL OTHER STYLES REMAIN EXACTLY THE SAME */
      header {
        background: linear-gradient(
          135deg,
          rgba(255, 107, 107, 0.95),
          rgba(254, 202, 87, 0.95)
        );
        color: white;
        padding: 30px;
        text-align: center;
        backdrop-filter: blur(10px);
      }

      h1 {
        font-size: 2.5em;
        margin-bottom: 10px;
        text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
      }

      .subtitle {
        font-size: 1.2em;
        opacity: 0.9;
      }

      .controls {
        padding: 30px;
        background: rgba(248, 249, 250, 0.1);
        backdrop-filter: blur(10px);
        display: flex;
        flex-wrap: wrap;
        gap: 15px;
        justify-content: center;
        align-items: center;
        border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      }

      .mode-selector {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
      }

      select,
      button {
        padding: 12px 20px;
        font-size: 16px;
        border: none;
        border-radius: 25px;
        cursor: pointer;
        transition: all 0.3s ease;
        color: #000;
        font-weight: bold;
        backdrop-filter: blur(10px);
      }

      select {
        background: rgba(255, 255, 255, 0.9);
        border: 2px solid rgba(51, 51, 51, 0.8);
        min-width: 200px;
      }

      button {
        background: linear-gradient(135deg, #4caf50, #45a049);
        color: white;
      }

      button:hover,
      .mode-btn.active {
        transform: translateY(-2px);
        box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
      }

      .mode-btn {
        background: rgba(221, 221, 221, 0.8);
        color: #333;
        min-width: 180px;
      }

      .sound-control {
        display: flex;
        gap: 10px;
        align-items: center;
      }

      .mute-btn {
        background: linear-gradient(135deg, #ff6b6b, #ee5a52);
        padding: 12px 16px;
        min-width: 120px;
      }

      .mute-btn.muted {
        background: linear-gradient(135deg, #666, #444);
      }

      .nav-buttons {
        display: flex;
        gap: 10px;
        margin-top: 20px;
        flex-wrap: wrap;
      }

      .stats {
        background: linear-gradient(
          135deg,
          rgba(102, 126, 234, 0.95),
          rgba(118, 75, 162, 0.95)
        );
        color: white;
        padding: 20px;
        text-align: center;
        backdrop-filter: blur(10px);
      }

      .stat-row {
        display: flex;
        justify-content: space-around;
        margin-bottom: 10px;
        flex-wrap: wrap;
      }

      .stat-item {
        font-size: 1.3em;
        font-weight: bold;
        text-shadow: 0 1px 2px rgba(0, 0, 0, 0.3);
      }

      .progress-container {
        background: rgba(255, 255, 255, 0.2);
        border-radius: 10px;
        height: 12px;
        overflow: hidden;
      }

      .progress-bar {
        height: 100%;
        background: linear-gradient(90deg, #4caf50, #8bc34a);
        width: 0%;
        transition: width 0.5s ease;
        border-radius: 10px;
      }

      .flashcard-container {
        padding: 40px;
        min-height: 450px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 30px;
      }

      .flashcard {
        width: 500px;
        height: 400px;
        position: relative;
        transform-style: preserve-3d;
        transition: transform 0.8s;
        cursor: pointer;
      }

      .flashcard.flipped {
        transform: rotateY(180deg);
      }

      .card-face {
        position: absolute;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
        border-radius: 20px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 40px;
        box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5);
        font-weight: bold;
        text-align: center;
        color: #000 !important;
        backdrop-filter: blur(15px);
        border: 1px solid rgba(255, 255, 255, 0.2);
      }

      .front {
        background: linear-gradient(
          135deg,
          rgba(86, 171, 47, 0.95),
          rgba(168, 230, 207, 0.95),
          rgba(79, 172, 254, 0.95)
        );
      }

      .back {
        background: linear-gradient(
          135deg,
          rgba(255, 154, 158, 0.95),
          rgba(254, 207, 239, 0.95),
          rgba(254, 207, 239, 0.95)
        );
        transform: rotateY(180deg);
      }

      .vocab-text {
        font-size: 2.5em;
        line-height: 1.2;
        margin-bottom: 20px;
        color: #000 !important;
        text-shadow: 0 2px 4px rgba(255, 255, 255, 0.3);
      }

      .english {
        font-size: 1.8em;
        color: #000 !important;
        text-shadow: 0 1px 2px rgba(255, 255, 255, 0.5);
      }

      .auto-audio {
        font-size: 1.1em;
        color: #555;
        margin-top: 10px;
      }

      .card-counter {
        font-size: 1.2em;
        margin-top: 10px;
        color: #ccc;
        text-shadow: 0 1px 2px rgba(0, 0, 0, 0.5);
      }

      .footer {
        background: rgba(51, 51, 51, 0.9);
        color: #ccc;
        text-align: center;
        padding: 20px;
        font-size: 0.9em;
        backdrop-filter: blur(10px);
      }

      @media (max-width: 768px) {
        .flashcard {
          width: 90vw;
          height: 350px;
        }

        .vocab-text {
          font-size: 2em;
        }

        .english {
          font-size: 1.4em;
        }

        .controls {
          flex-direction: column;
        }
      }

      @keyframes twinkle {
        0%,
        100% {
          opacity: 1;
        }

        50% {
          opacity: 0.3;
        }
      }

      .star::before {
        content: "";
        position: absolute;
        top: 50%;
        left: 50%;
        width: 2px;
        height: 2px;
        background: white;
        transform: translate(-50%, -50%);
        animation: twinkle 2s infinite;
      }
    </style>
  </head>

  <body>
    <!-- CHANGED: sky-bg + milky-way + stars -->
    <div class="sky-bg"></div>
    <div class="milky-way"></div>
    <div class="stars" id="stars"></div>

    <!-- ALL HTML CONTENT EXACTLY SAME -->
    <div class="container">
      <header>
        <h1>🌌 Minna no Nihongo - Night Sky Edition</h1>
        <p class="subtitle">Starry Sky Learning • Auto Audio • 25 Lessons</p>
      </header>

      <div class="controls">
        <div class="mode-selector">
          <button class="mode-btn active" onclick="setMode('japanese')">
            Jap → Eng
          </button>
          <button class="mode-btn" onclick="setMode('english')">
            Eng → Jap
          </button>
        </div>
        <div class="sound-control">
          <button class="mute-btn" id="muteBtn" onclick="toggleMute()">
            🔊 Unmute
          </button>
          <span style="color: #fff; font-weight: bold">Auto Audio</span>
        </div>
        <div>
          <label style="color: white">LESSON--</label>
          <select style="text-align: center" id="lessonSelect">
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
            <option value="6">6</option>
            <option value="7">7</option>
            <option value="8">8</option>
            <option value="9">9</option>
            <option value="10">10</option>
            <option value="11">11</option>
            <option value="12">12</option>
            <option value="13">13</option>
            <option value="14">14</option>
            <option value="15">15</option>
            <option value="16">16</option>
            <option value="17">17</option>
            <option value="18">18</option>
            <option value="19">19</option>
            <option value="20">20</option>
            <option value="21">21</option>
            <option value="22">22</option>
            <option value="23">23</option>
            <option value="24">24</option>
            <option value="25">25</option>
            <option value="26">WH-Questions</option>
          </select>
        </div>
        <button onclick="shuffleVocab()">Shuffle</button>
        <button onclick="resetVocab()">Reset</button>
        <button onclick="practiceAll()">All Lessons</button>
      </div>

      <div class="stats">
        <div class="stat-row">
          <div class="stat-item">Score: <span id="score">0</span></div>
          <div class="stat-item">
            Card <span id="currentIndex">1</span>/<span id="totalCards">0</span>
          </div>
          <div class="stat-item">Streak: <span id="streak">0</span></div>
        </div>
        <div class="progress-container">
          <div class="progress-bar" id="progressBar"></div>
        </div>
      </div>

      <div class="flashcard-container">
        <div id="flashcard" class="flashcard" onclick="flipCard()">
          <div class="card-face front" id="frontCard">
            <div class="vocab-text" id="frontText">
              レッスンを選んでください
            </div>
            <div class="auto-audio" id="frontAudioText" style="color: #fff">
              Auto pronunciation enabled ✨
            </div>
          </div>
          <div class="card-face back" id="backCard">
            <div class="vocab-text" id="backText">
              Choose a lesson to start!
            </div>
            <div class="auto-audio" id="backAudioText" style="color: #fff">
              Auto pronunciation enabled ✨
            </div>
          </div>
        </div>
        <div class="nav-buttons">
          <button style="width: 150px; height: 50px" onclick="previousCard()">
            Previous
          </button>
          <button style="width: 150px; height: 50px" onclick="nextCard()">
            Next
          </button>
          <button style="width: 150px; height: 50px" onclick="flipCard()">
            Flip
          </button>
        </div>
        <div id="cardCounter" class="card-counter"></div>
      </div>

      <div class="footer">
        <p>
          🌠 Complete Minna no Nihongo I • Night Sky Learning • Auto Audio
          [web:1][web:2]
        </p>
      </div>
    </div>

    <script>
      // CHANGED: Create DOUBLE SIZE GOLDEN STARS (100 stars)
      function createStars() {
        const starsContainer = document.getElementById("stars");
        for (let i = 0; i < 100; i++) {
          const star = document.createElement("div");
          star.className = "star";
          star.style.left = Math.random() * 100 + "%";
          star.style.width = Math.random() * 6 + 8 + "px"; // 8-14px DOUBLE size
          star.style.height = star.style.width;
          star.style.animationDelay = Math.random() * 25 + "s";
          star.style.animationDuration = Math.random() * 12 + 18 + "s";
          starsContainer.appendChild(star);
        }
      }

      // ALL JAVASCRIPT FUNCTIONS EXACTLY SAME AS ORIGINAL
      const vocabData = {
        1: [
          { japanese: "わたし", romaji: "watashi", english: "I" },
          { japanese: "わたしたち", romaji: "watashitachi", english: "we" },
          { japanese: "あなた", romaji: "anata", english: "you" },
          {
            japanese: "あのひと",
            romaji: "ano hito",
            english: "that person, he, she",
          },
          {
            japanese: "みなさん",
            romaji: "minasan",
            english: "ladies and gentlemen, all of you",
          },

          {
            japanese: "〜さん",
            romaji: "〜san",
            english: "Mr., Ms. (title of respect added to a name)",
          },
          {
            japanese: "〜ちゃん",
            romaji: "〜chan",
            english: "suffix often added to a child’s name",
          },
          {
            japanese: "〜くん",
            romaji: "〜kun",
            english: "suffix often added to a boy’s name",
          },
          {
            japanese: "〜じん",
            romaji: "〜jin",
            english: "suffix meaning “a national of”",
          },

          {
            japanese: "せんせい",
            romaji: "sensei",
            english: "teacher, instructor",
          },
          {
            japanese: "きょうし",
            romaji: "kyoushi",
            english: "teacher, instructor",
          },
          { japanese: "がくせい", romaji: "gakusei", english: "student" },
          {
            japanese: "かいしゃいん",
            romaji: "kaishain",
            english: "company employee",
          },

          {
            japanese: "ぎんこういん",
            romaji: "ginkouin",
            english: "bank employee",
          },
          { japanese: "いしゃ", romaji: "isha", english: "medical doctor" },
          {
            japanese: "けんきゅうしゃ",
            romaji: "kenkyuusha",
            english: "researcher, scholar",
          },
          { japanese: "エンジニア", romaji: "enjiniya", english: "engineer" },

          { japanese: "だいがく", romaji: "daigaku", english: "university" },
          { japanese: "びょういん", romaji: "byouin", english: "hospital" },
          {
            japanese: "でんき",
            romaji: "denki",
            english: "electricity, light",
          },
          { japanese: "だれ", romaji: "dare", english: "who" },

          { japanese: "〜さい", romaji: "〜sai", english: "– years old" },
          { japanese: "なんさい", romaji: "nansai", english: "how old" },
          { japanese: "はい", romaji: "hai", english: "yes" },
          { japanese: "いいえ", romaji: "iie", english: "no" },

          {
            japanese: "しつれいですが",
            romaji: "shitsurei desu ga",
            english: "Excuse me, but",
          },
          {
            japanese: "おなまえは？",
            romaji: "onamae wa?",
            english: "May I have your name?",
          },
          {
            japanese: "はじめまして",
            romaji: "hajimemashite",
            english: "How do you do?",
          },
          {
            japanese: "どうぞ よろしく",
            romaji: "douzo yoroshiku",
            english: "Pleased to meet you",
          },
          {
            japanese: "おねがいします",
            romaji: "onegai shimasu",
            english: "Please (be nice to me)",
          },
          {
            japanese: "こちらは 〜さんです",
            romaji: "kochira wa 〜san desu",
            english: "This is Mr./Ms. 〜",
          },
          {
            japanese: "〜から きました",
            romaji: "〜kara kimashita",
            english: "I came from 〜",
          },

          { japanese: "アメリカ", romaji: "Amerika", english: "U.S.A." },
          { japanese: "イギリス", romaji: "Igirisu", english: "U.K." },
          { japanese: "インド", romaji: "Indo", english: "India" },
          {
            japanese: "インドネシア",
            romaji: "Indoneshia",
            english: "Indonesia",
          },
          { japanese: "かんこく", romaji: "kankoku", english: "South Korea" },
          { japanese: "タイ", romaji: "Tai", english: "Thailand" },
          { japanese: "ちゅうごく", romaji: "chuugoku", english: "China" },
          { japanese: "ドイツ", romaji: "Doitsu", english: "Germany" },
          { japanese: "にほん", romaji: "nihon", english: "Japan" },
          { japanese: "フランス", romaji: "Furansu", english: "France" },
          { japanese: "ブラジル", romaji: "Burajiru", english: "Brazil" },
        ],

        2: [
          { japanese: "これ", romaji: "kore", english: "this (thing here)" },
          {
            japanese: "それ",
            romaji: "sore",
            english: "that (thing near you)",
          },
          {
            japanese: "あれ",
            romaji: "are",
            english: "that (thing over there)",
          },

          { japanese: "この〜", romaji: "kono〜", english: "this 〜 here" },
          { japanese: "その〜", romaji: "sono〜", english: "that 〜 near you" },
          {
            japanese: "あの〜",
            romaji: "ano〜",
            english: "that 〜 over there",
          },

          { japanese: "ほん", romaji: "hon", english: "book" },
          { japanese: "じしょ", romaji: "jisho", english: "dictionary" },
          { japanese: "ざっし", romaji: "zasshi", english: "magazine" },
          { japanese: "しんぶん", romaji: "shinbun", english: "newspaper" },
          { japanese: "ノート", romaji: "nooto", english: "notebook" },
          {
            japanese: "てちょう",
            romaji: "techou",
            english: "pocket notebook",
          },
          { japanese: "めいし", romaji: "meishi", english: "business card" },
          { japanese: "カード", romaji: "kaado", english: "card" },
          {
            japanese: "テレホンカード",
            romaji: "terehonkaado",
            english: "telephone card",
          },
          {
            japanese: "ボールペン",
            romaji: "boorupen",
            english: "ballpoint pen",
          },
          {
            japanese: "シャープペンシル",
            romaji: "shaapupenshiru",
            english: "mechanical pencil",
          },

          { japanese: "かぎ", romaji: "kagi", english: "key" },
          { japanese: "とけい", romaji: "tokei", english: "watch, clock" },
          { japanese: "かさ", romaji: "kasa", english: "umbrella" },
          { japanese: "かばん", romaji: "kaban", english: "bag, briefcase" },

          {
            japanese: "カセットテープ",
            romaji: "kasetto teepu",
            english: "cassette tape",
          },
          {
            japanese: "テープレコーダー",
            romaji: "teepu rekoodaa",
            english: "tape recorder",
          },
          { japanese: "テレビ", romaji: "terebi", english: "television" },
          { japanese: "ラジオ", romaji: "rajio", english: "radio" },
          { japanese: "カメラ", romaji: "kamera", english: "camera" },
          {
            japanese: "コンピューター",
            romaji: "konpyuutaa",
            english: "computer",
          },
          {
            japanese: "じどうしゃ",
            romaji: "jidousha",
            english: "automobile, car",
          },

          { japanese: "つくえ", romaji: "tsukue", english: "desk" },
          { japanese: "いす", romaji: "isu", english: "chair" },

          {
            japanese: "チョコレート",
            romaji: "chokoreeto",
            english: "chocolate",
          },
          { japanese: "コーヒー", romaji: "koohii", english: "coffee" },

          {
            japanese: "えいご",
            romaji: "eigo",
            english: "the English language",
          },
          {
            japanese: "にほんご",
            romaji: "nihongo",
            english: "the Japanese language",
          },
          { japanese: "〜ご", romaji: "〜go", english: "〜 language" },

          { japanese: "なん", romaji: "nan", english: "what" },
          { japanese: "そう", romaji: "sou", english: "so" },

          {
            japanese: "ちがいます",
            romaji: "chigaimasu",
            english: "No, it isn’t / You are wrong",
          },
          {
            japanese: "そうですか",
            romaji: "sou desu ka",
            english: "I see / Is that so?",
          },
          {
            japanese: "あのう",
            romaji: "anou",
            english: "well (used to show hesitation)",
          },
          {
            japanese: "あのう",
            romaji: "anou",
            english: "well (used to show hesitation)",
          },
          {
            japanese: "ほんの きもちです",
            romaji: "hon no kimochi desu",
            english: "It's nothing / It's a token of my gratitude",
          },
          {
            japanese: "どうぞ",
            romaji: "douzo",
            english: "Please / Here you are",
          },
          { japanese: "どうも", romaji: "doumo", english: "Well / Thanks" },
          { japanese: "ありがとう", romaji: "arigatou", english: "Thank you" },
          {
            japanese: "ございます",
            romaji: "gozaimasu",
            english: "very much (polite suffix)",
          },
          {
            japanese: "どうもありがとうございます",
            romaji: "doumo arigatou gozaimasu",
            english: "Thank you very much",
          },

          {
            japanese: "これから",
            romaji: "kore kara",
            english: "from now on / hereafter",
          },
          {
            japanese: "おせわになります",
            romaji: "osewa ni narimasu",
            english: "I hope for your kind assistance",
          },
          {
            japanese: "こちらこそ",
            romaji: "kochira koso",
            english: "Likewise / I am pleased to meet you",
          },
          {
            japanese: "よろしく",
            romaji: "yoroshiku",
            english: "Nice to meet you / Please treat me well",
          },
        ],

        3: [
          { japanese: "ここ", romaji: "koko", english: "here, this place" },
          {
            japanese: "そこ",
            romaji: "soko",
            english: "there, that place near you",
          },
          {
            japanese: "あそこ",
            romaji: "asoko",
            english: "that place over there",
          },
          { japanese: "どこ", romaji: "doko", english: "where, what place" },

          {
            japanese: "こちら",
            romaji: "kochira",
            english: "this way, this place (polite)",
          },
          {
            japanese: "そちら",
            romaji: "sochira",
            english: "that way, that place near you (polite)",
          },
          {
            japanese: "あちら",
            romaji: "achira",
            english: "that way, that place over there (polite)",
          },
          {
            japanese: "どちら",
            romaji: "dochira",
            english: "which way, where (polite)",
          },

          {
            japanese: "きょうしつ",
            romaji: "kyoushitsu",
            english: "classroom",
          },
          {
            japanese: "しょくどう",
            romaji: "shokudou",
            english: "dining hall, canteen",
          },
          { japanese: "じむしょ", romaji: "jimusho", english: "office" },
          {
            japanese: "かいぎしつ",
            romaji: "kaigishitsu",
            english: "conference room, assembly room",
          },
          {
            japanese: "うけつけ",
            romaji: "uketsuke",
            english: "reception desk",
          },
          { japanese: "ロビー", romaji: "robii", english: "lobby" },
          { japanese: "へや", romaji: "heya", english: "room" },
          { japanese: "トイレ", romaji: "toire", english: "toilet, rest room" },
          {
            japanese: "おてあらい",
            romaji: "otearai",
            english: "toilet, rest room",
          },
          { japanese: "かいだん", romaji: "kaidan", english: "staircase" },
          {
            japanese: "エレベーター",
            romaji: "erebeetaa",
            english: "elevator, lift",
          },
          {
            japanese: "エスカレーター",
            romaji: "esukareetaa",
            english: "escalator",
          },

          { japanese: "おくに", romaji: "okuni", english: "country" },
          { japanese: "かいしゃ", romaji: "kaisha", english: "company" },
          { japanese: "うち", romaji: "uchi", english: "house, home" },

          {
            japanese: "でんわ",
            romaji: "denwa",
            english: "telephone, telephone call",
          },
          { japanese: "くつ", romaji: "kutsu", english: "shoes" },
          { japanese: "ネクタイ", romaji: "nekutai", english: "necktie" },
          { japanese: "ワイン", romaji: "wain", english: "wine" },
          {
            japanese: "たばこ",
            romaji: "tabako",
            english: "tobacco, cigarette",
          },

          {
            japanese: "うりば",
            romaji: "uriba",
            english: "department, counter (in a department store)",
          },
          { japanese: "ちか", romaji: "chika", english: "basement" },
          { japanese: "〜かい", romaji: "〜kai", english: "〜th floor" },
          { japanese: "〜がい", romaji: "〜gai", english: "〜th floor" },
          { japanese: "なんがい", romaji: "nangai", english: "what floor" },

          { japanese: "〜えん", romaji: "〜en", english: "〜 yen" },
          { japanese: "いくら", romaji: "ikura", english: "how much" },

          { japanese: "ひゃく", romaji: "hyaku", english: "hundred" },
          { japanese: "せん", romaji: "sen", english: "thousand" },
          { japanese: "まん", romaji: "man", english: "ten thousand" },

          { japanese: "すみません", romaji: "sumimasen", english: "Excuse me" },
          {
            japanese: "〜でございます",
            romaji: "〜de gozaimasu",
            english: "polite equivalent of です",
          },
          {
            japanese: "〜をみせてください",
            romaji: "〜o misete kudasai",
            english: "Please show me 〜",
          },
          {
            japanese: "じゃ",
            romaji: "ja",
            english: "well, then, in that case",
          },
          {
            japanese: "〜をください",
            romaji: "〜o kudasai",
            english: "Give me 〜, please",
          },
          {
            japanese: "しんおおさか",
            romaji: "Shin-Ōsaka",
            english: "name of a station in Osaka",
          },
          { japanese: "イタリア", romaji: "Itaria", english: "Italy" },
          { japanese: "スイス", romaji: "Suisu", english: "Switzerland" },
          {
            japanese: "エムティー",
            romaji: "Emutii",
            english: "fictitious company (MT)",
          },
          {
            japanese: "ヨーネン",
            romaji: "Yoonen",
            english: "fictitious company (Yonen)",
          },
          {
            japanese: "アキックス",
            romaji: "Akikkusu",
            english: "fictitious company (Akix)",
          },
        ],

        4: [
          {
            japanese: "おきます",
            romaji: "okimasu",
            english: "get up, wake up",
          },
          { japanese: "ねます", romaji: "nemasu", english: "sleep, go to bed" },
          { japanese: "はたらきます", romaji: "hatarakimasu", english: "work" },
          {
            japanese: "やすみます",
            romaji: "yasumimasu",
            english: "take a rest, take a holiday",
          },
          {
            japanese: "べんきょうします",
            romaji: "benkyou shimasu",
            english: "study",
          },
          { japanese: "おわります", romaji: "owarimasu", english: "finish" },

          {
            japanese: "デパート",
            romaji: "depaato",
            english: "department store",
          },
          { japanese: "ぎんこう", romaji: "ginkou", english: "bank" },
          {
            japanese: "ゆうびんきょく",
            romaji: "yuubinkyoku",
            english: "post office",
          },
          { japanese: "としょかん", romaji: "toshokan", english: "library" },
          {
            japanese: "びじゅつかん",
            romaji: "bijutsukan",
            english: "art museum",
          },

          { japanese: "いま", romaji: "ima", english: "now" },
          { japanese: "〜じ", romaji: "〜ji", english: "〜 o’clock" },
          { japanese: "〜ふん", romaji: "〜fun", english: "〜 minute" },
          { japanese: "〜ぷん", romaji: "〜pun", english: "〜 minute" },
          { japanese: "はん", romaji: "han", english: "half" },
          { japanese: "なんじ", romaji: "nanji", english: "what time" },
          { japanese: "なんぷん", romaji: "nanpun", english: "what minute" },
          { japanese: "ごぜん", romaji: "gozen", english: "a.m., morning" },
          { japanese: "ごご", romaji: "gogo", english: "p.m., afternoon" },

          { japanese: "あさ", romaji: "asa", english: "morning" },
          { japanese: "ひる", romaji: "hiru", english: "daytime, noon" },
          { japanese: "ばん", romaji: "ban", english: "night, evening" },
          { japanese: "よる", romaji: "yoru", english: "night, evening" },

          {
            japanese: "おととい",
            romaji: "ototoi",
            english: "the day before yesterday",
          },
          { japanese: "きのう", romaji: "kinou", english: "yesterday" },
          { japanese: "きょう", romaji: "kyou", english: "today" },
          { japanese: "あした", romaji: "ashita", english: "tomorrow" },
          {
            japanese: "あさって",
            romaji: "asatte",
            english: "the day after tomorrow",
          },

          { japanese: "けさ", romaji: "kesa", english: "this morning" },
          {
            japanese: "こんばん",
            romaji: "konban",
            english: "this evening, tonight",
          },

          {
            japanese: "やすみ",
            romaji: "yasumi",
            english: "rest, a holiday, a day off",
          },
          {
            japanese: "ひるやすみ",
            romaji: "hiruyasumi",
            english: "lunchtime",
          },
          { japanese: "まいあさ", romaji: "maiasa", english: "every morning" },
          { japanese: "まいばん", romaji: "maiban", english: "every night" },
          { japanese: "まいにち", romaji: "mainichi", english: "every day" },

          { japanese: "げつようび", romaji: "getsuyoubi", english: "Monday" },
          { japanese: "かようび", romaji: "kayoubi", english: "Tuesday" },
          { japanese: "すいようび", romaji: "suiyoubi", english: "Wednesday" },
          { japanese: "もくようび", romaji: "mokuyoubi", english: "Thursday" },
          { japanese: "きんようび", romaji: "kinyoubi", english: "Friday" },
          { japanese: "どようび", romaji: "doyoubi", english: "Saturday" },
          { japanese: "にちようび", romaji: "nichiyoubi", english: "Sunday" },
          {
            japanese: "なんようび",
            romaji: "nanyoubi",
            english: "what day of the week",
          },

          { japanese: "ばんごう", romaji: "bangou", english: "number" },
          { japanese: "なんばん", romaji: "nanban", english: "what number" },

          { japanese: "〜から", romaji: "〜kara", english: "from 〜" },
          {
            japanese: "〜まで",
            romaji: "〜made",
            english: "up to 〜 / until 〜",
          },
          {
            japanese: "〜と〜",
            romaji: "〜to〜",
            english: "and (used to connect nouns)",
          },
          { japanese: "そちら", romaji: "sochira", english: "your place" },
          {
            japanese: "たいへんですね",
            romaji: "taihen desu ne",
            english: "That's tough, isn't it?",
          },
          { japanese: "えーと", romaji: "eeto", english: "well, let me see" },

          {
            japanese: "いちぜろよん",
            romaji: "ichi zero yon",
            english: "directory assistance",
          },
          {
            japanese: "おねがいします",
            romaji: "onegai shimasu",
            english: "Please (ask for a favor)",
          },
          {
            japanese: "かしこまりました",
            romaji: "kashikomarimashita",
            english: "Certainly (sir, madam)",
          },
          {
            japanese: "おといあわせのばんごう",
            romaji: "otoiawase no bangou",
            english: "the number being inquired about",
          },
          {
            japanese: "どうもありがとうございました",
            romaji: "doumo arigatou gozaimashita",
            english: "Thank you very much",
          },

          {
            japanese: "ニューヨーク",
            romaji: "Nyuu Yooku",
            english: "New York",
          },
          { japanese: "ペキン", romaji: "Pekin", english: "Beijing" },
          { japanese: "ロンドン", romaji: "Rondon", english: "London" },
          { japanese: "バンコク", romaji: "Bankoku", english: "Bangkok" },
          {
            japanese: "ロサンゼルス",
            romaji: "Rosanzerusu",
            english: "Los Angeles",
          },
        ],

        5: [
          { japanese: "いきます", romaji: "ikimasu", english: "go" },
          { japanese: "きます", romaji: "kimasu", english: "come" },
          {
            japanese: "かえります",
            romaji: "kaerimasu",
            english: "go home, return",
          },

          { japanese: "がっこう", romaji: "gakkou", english: "school" },
          { japanese: "スーパー", romaji: "suupaa", english: "supermarket" },
          { japanese: "えき", romaji: "eki", english: "station" },

          { japanese: "ひこうき", romaji: "hikouki", english: "airplane" },
          { japanese: "ふね", romaji: "fune", english: "ship" },
          { japanese: "でんしゃ", romaji: "densha", english: "electric train" },
          {
            japanese: "ちかてつ",
            romaji: "chikatetsu",
            english: "subway, underground",
          },
          {
            japanese: "しんかんせん",
            romaji: "shinkansen",
            english: "the Shinkansen, the bullet train",
          },
          { japanese: "バス", romaji: "basu", english: "bus" },
          { japanese: "タクシー", romaji: "takushii", english: "taxi" },
          { japanese: "じてんしゃ", romaji: "jitensha", english: "bicycle" },
          { japanese: "あるいて", romaji: "aruite", english: "on foot" },

          { japanese: "ひと", romaji: "hito", english: "person, people" },
          { japanese: "ともだち", romaji: "tomodachi", english: "friend" },
          { japanese: "かれ", romaji: "kare", english: "he, boyfriend, lover" },
          {
            japanese: "かのじょ",
            romaji: "kanojo",
            english: "she, girlfriend, lover",
          },
          { japanese: "かぞく", romaji: "kazoku", english: "family" },
          {
            japanese: "ひとりで",
            romaji: "hitoride",
            english: "alone, by oneself",
          },

          { japanese: "せんしゅう", romaji: "senshuu", english: "last week" },
          { japanese: "こんしゅう", romaji: "konshuu", english: "this week" },
          { japanese: "らいしゅう", romaji: "raishuu", english: "next week" },
          { japanese: "せんげつ", romaji: "sengetsu", english: "last month" },
          { japanese: "こんげつ", romaji: "kongetsu", english: "this month" },
          { japanese: "らいげつ", romaji: "raigetsu", english: "next month" },
          { japanese: "きょねん", romaji: "kyonen", english: "last year" },
          { japanese: "ことし", romaji: "kotoshi", english: "this year" },
          { japanese: "らいねん", romaji: "rainen", english: "next year" },
          {
            japanese: "〜がつ",
            romaji: "〜gatsu",
            english: "〜th month of the year",
          },
          { japanese: "なんがつ", romaji: "nan gatsu", english: "what month" },

          {
            japanese: "ついたち",
            romaji: "tsuitachi",
            english: "first day of the month",
          },
          {
            japanese: "ふつか",
            romaji: "futsuka",
            english: "second, two days",
          },
          { japanese: "みっか", romaji: "mikka", english: "third, three days" },
          { japanese: "よっか", romaji: "yokka", english: "fourth, four days" },
          { japanese: "いつか", romaji: "itsuka", english: "fifth, five days" },
          { japanese: "むいか", romaji: "muika", english: "sixth, six days" },
          {
            japanese: "なのか",
            romaji: "nanoka",
            english: "seventh, seven days",
          },
          {
            japanese: "ようか",
            romaji: "youka",
            english: "eighth, eight days",
          },
          {
            japanese: "ここのか",
            romaji: "kokonoka",
            english: "ninth, nine days",
          },
          { japanese: "とおか", romaji: "tooka", english: "tenth, ten days" },
          {
            japanese: "じゅうよっか",
            romaji: "juuyokka",
            english: "fourteenth, fourteen days",
          },
          {
            japanese: "はつか",
            romaji: "hatsuka",
            english: "twentieth, twenty days",
          },
          {
            japanese: "にじゅうよっか",
            romaji: "nijuu yokka",
            english: "twenty fourth, twenty four days",
          },
          {
            japanese: "〜にち",
            romaji: "〜nichi",
            english: "〜th day of the month / 〜 days",
          },
          {
            japanese: "なんにち",
            romaji: "nan nichi",
            english: "which day of the month / how many days",
          },
          { japanese: "いつ", romaji: "itsu", english: "when" },
          { japanese: "たんじょうび", romaji: "tanjoubi", english: "birthday" },

          { japanese: "ふつう", romaji: "futsuu", english: "local (train)" },
          { japanese: "きゅうこう", romaji: "kyuukou", english: "rapid" },
          { japanese: "とっきゅう", romaji: "tokkyuu", english: "express" },
          { japanese: "つぎの", romaji: "tsugi no", english: "next" },

          {
            japanese: "どういたしまして",
            romaji: "dou itashimashite",
            english: "You're welcome / Don't mention it",
          },
          {
            japanese: "〜ばんせん",
            romaji: "〜bansen",
            english: "platform 〜 / 〜th platform",
          },
        ],

        6: [
          { japanese: "たべます", romaji: "tabemasu", english: "eat" },
          { japanese: "のみます", romaji: "nomimasu", english: "drink" },
          {
            japanese: "すいます",
            romaji: "suimasu",
            english: "smoke [a cigarette]",
          },
          {
            japanese: "たばこをすいます",
            romaji: "tabako o suimasu",
            english: "smoke a cigarette",
          },

          {
            japanese: "みます",
            romaji: "mimasu",
            english: "see, look at, watch",
          },
          { japanese: "ききます", romaji: "kikimasu", english: "hear, listen" },
          { japanese: "よみます", romaji: "yomimasu", english: "read" },
          {
            japanese: "かきます",
            romaji: "kakimasu",
            english: "write, draw, paint",
          },
          { japanese: "かいます", romaji: "kaimasu", english: "buy" },
          {
            japanese: "とります",
            romaji: "torimasu",
            english: "take [a photograph]",
          },
          {
            japanese: "しゃしんをとります",
            romaji: "shashin o torimasu",
            english: "take a photograph",
          },

          { japanese: "します", romaji: "shimasu", english: "do" },
          {
            japanese: "あいます",
            romaji: "aimasu",
            english: "meet [a friend]",
          },
          {
            japanese: "ともだちにあいます",
            romaji: "tomodachi ni aimasu",
            english: "meet a friend",
          },

          {
            japanese: "ごはん",
            romaji: "gohan",
            english: "a meal, cooked rice",
          },
          { japanese: "あさごはん", romaji: "asagohan", english: "breakfast" },
          { japanese: "ひるごはん", romaji: "hirugohan", english: "lunch" },
          { japanese: "ばんごはん", romaji: "bangohan", english: "supper" },

          { japanese: "パン", romaji: "pan", english: "bread" },
          { japanese: "たまご", romaji: "tamago", english: "egg" },
          { japanese: "にく", romaji: "niku", english: "meat" },
          { japanese: "さかな", romaji: "sakana", english: "fish" },
          { japanese: "やさい", romaji: "yasai", english: "vegetable" },
          { japanese: "くだもの", romaji: "kudamono", english: "fruit" },

          { japanese: "みず", romaji: "mizu", english: "water" },
          { japanese: "おちゃ", romaji: "ocha", english: "tea, green tea" },
          { japanese: "こうちゃ", romaji: "koucha", english: "black tea" },
          { japanese: "ぎゅうにゅう", romaji: "gyuunyuu", english: "milk" },
          { japanese: "ミルク", romaji: "miruku", english: "milk" },
          { japanese: "ジュース", romaji: "juusu", english: "juice" },
          { japanese: "ビール", romaji: "biiru", english: "beer" },
          {
            japanese: "おさけ",
            romaji: "osake",
            english: "alcohol, Japanese rice wine",
          },
          {
            japanese: "ビデオ",
            romaji: "bideo",
            english: "video tape, video deck",
          },
          { japanese: "えいが", romaji: "eiga", english: "movie" },
          { japanese: "CD", romaji: "shii dii", english: "CD, compact disc" },
          { japanese: "てがみ", romaji: "tegami", english: "letter" },
          { japanese: "レポート", romaji: "repooto", english: "report" },
          { japanese: "しゃしん", romaji: "shashin", english: "photograph" },
          { japanese: "みせ", romaji: "mise", english: "store, shop" },
          {
            japanese: "レストラン",
            romaji: "resutoran",
            english: "restaurant",
          },
          { japanese: "にわ", romaji: "niwa", english: "garden" },

          { japanese: "しゅくだい", romaji: "shukudai", english: "homework" },
          {
            japanese: "しゅくだいをします",
            romaji: "shukudai o shimasu",
            english: "do homework",
          },
          { japanese: "テニス", romaji: "tenisu", english: "tennis" },
          {
            japanese: "テニスをします",
            romaji: "tenisu o shimasu",
            english: "play tennis",
          },
          {
            japanese: "サッカー",
            romaji: "sakkaa",
            english: "soccer, football",
          },
          {
            japanese: "サッカーをします",
            romaji: "sakkaa o shimasu",
            english: "play soccer",
          },

          {
            japanese: "おはなみ",
            romaji: "ohanami",
            english: "cherry-blossom viewing",
          },
          { japanese: "なに", romaji: "nani", english: "what" },
          { japanese: "いっしょに", romaji: "issho ni", english: "together" },
          {
            japanese: "ちょっと",
            romaji: "chotto",
            english: "a little while, a little bit",
          },
          { japanese: "いつも", romaji: "itsumo", english: "always, usually" },
          { japanese: "ときどき", romaji: "tokidoki", english: "sometimes" },
          {
            japanese: "それから",
            romaji: "sorekara",
            english: "after that, and then",
          },
          { japanese: "ええ", romaji: "ee", english: "yes" },
          {
            japanese: "いいですね",
            romaji: "ii desu ne",
            english: "That's good",
          },
          {
            japanese: "わかりました",
            romaji: "wakarimashita",
            english: "I see",
          },

          {
            japanese: "なんですか",
            romaji: "nan desu ka",
            english: "Yes? / What is it?",
          },
          {
            japanese: "じゃ、またあした",
            romaji: "ja, mata ashita",
            english: "See you tomorrow",
          },

          { japanese: "メキシコ", romaji: "Mekishiko", english: "Mexico" },
          {
            japanese: "おおさかじょうこうえん",
            romaji: "Oosakajou Kouen",
            english: "Osaka Castle Park",
          },
        ],

        7: [
          { japanese: "きります", romaji: "kirimasu", english: "cut, slice" },
          { japanese: "おくります", romaji: "okurimasu", english: "send" },
          { japanese: "あげます", romaji: "agemasu", english: "give" },
          { japanese: "もらいます", romaji: "moraimasu", english: "receive" },
          { japanese: "かします", romaji: "kashimasu", english: "lend" },
          { japanese: "かります", romaji: "karimasu", english: "borrow" },
          { japanese: "おしえます", romaji: "oshiemasu", english: "teach" },
          { japanese: "ならいます", romaji: "naraimasu", english: "learn" },
          {
            japanese: "かけます",
            romaji: "kakemasu",
            english: "make [a telephone call]",
          },
          {
            japanese: "でんわをかけます",
            romaji: "denwa o kakemasu",
            english: "make a telephone call",
          },

          { japanese: "て", romaji: "te", english: "hand, arm" },
          { japanese: "はし", romaji: "hashi", english: "chopsticks" },
          { japanese: "スプーン", romaji: "supuun", english: "spoon" },
          { japanese: "ナイフ", romaji: "naifu", english: "knife" },
          { japanese: "フォーク", romaji: "fooku", english: "fork" },
          { japanese: "はさみ", romaji: "hasami", english: "scissors" },
          { japanese: "ファクス", romaji: "fakusu", english: "fax" },
          {
            japanese: "ワープロ",
            romaji: "waapuro",
            english: "word processor",
          },
          {
            japanese: "パソコン",
            romaji: "pasokon",
            english: "personal computer",
          },
          { japanese: "パンチ", romaji: "panchi", english: "punch" },
          { japanese: "ホッチキス", romaji: "hotchikisu", english: "stapler" },
          {
            japanese: "セロテープ",
            romaji: "seroteepu",
            english: "Scotch tape / clear adhesive tape",
          },
          { japanese: "けしゴム", romaji: "keshigomu", english: "eraser" },
          { japanese: "かみ", romaji: "kami", english: "paper" },

          { japanese: "はな", romaji: "hana", english: "flower / blossom" },
          { japanese: "シャツ", romaji: "shatsu", english: "shirt" },
          {
            japanese: "プレゼント",
            romaji: "purezento",
            english: "present / gift",
          },
          {
            japanese: "にもつ",
            romaji: "nimotsu",
            english: "baggage / parcel",
          },
          { japanese: "おかね", romaji: "okane", english: "money" },
          { japanese: "きっぷ", romaji: "kippu", english: "ticket" },

          {
            japanese: "クリスマス",
            romaji: "kurisumasu",
            english: "Christmas",
          },
          { japanese: "ちち", romaji: "chichi", english: "(my) father" },
          { japanese: "はは", romaji: "haha", english: "(my) mother" },
          {
            japanese: "おとうさん",
            romaji: "otousan",
            english: "(someone else's) father",
          },
          {
            japanese: "おかあさん",
            romaji: "okaasan",
            english: "(someone else's) mother",
          },

          { japanese: "もう", romaji: "mou", english: "already" },
          { japanese: "まだ", romaji: "mada", english: "not yet" },
          {
            japanese: "これから",
            romaji: "kore kara",
            english: "from now on / soon",
          },

          {
            japanese: "〜すてきですね",
            romaji: "〜suteki desu ne",
            english: "What a nice 〜!",
          },

          {
            japanese: "ごめんください",
            romaji: "gomen kudasai",
            english: "Excuse me / May I come in?",
          },
          {
            japanese: "いらっしゃい",
            romaji: "irasshai",
            english: "Welcome / How nice of you to come",
          },
          {
            japanese: "どうぞおあがりください",
            romaji: "douzo oagari kudasai",
            english: "Do come in",
          },
          {
            japanese: "しつれいします",
            romaji: "shitsurei shimasu",
            english: "Thank you / May I?",
          },
          {
            japanese: "〜はいかがですか",
            romaji: "〜wa ikaga desu ka",
            english: "Would you like 〜?",
          },
          {
            japanese: "いただきます",
            romaji: "itadakimasu",
            english: "Thank you / I accept (before eating)",
          },
          { japanese: "りょこう", romaji: "ryokou", english: "trip, tour" },
          {
            japanese: "りょこうをします",
            romaji: "ryokou o shimasu",
            english: "travel / make a trip",
          },
          {
            japanese: "おみやげ",
            romaji: "omiyage",
            english: "souvenir / present",
          },

          { japanese: "ヨーロッパ", romaji: "Yooroppa", english: "Europe" },
          { japanese: "スペイン", romaji: "Supein", english: "Spain" },
        ],
        8: [
          { japanese: "ハンサム", romaji: "hansamu", english: "handsome" },
          { japanese: "きれい", romaji: "kirei", english: "beautiful, clean" },
          { japanese: "しずか", romaji: "shizuka", english: "quiet" },
          { japanese: "にぎやか", romaji: "nigiyaka", english: "lively" },
          { japanese: "ゆうめい", romaji: "yuumei", english: "famous" },
          { japanese: "しんせつ", romaji: "shinsetsu", english: "kind" },
          {
            japanese: "げんき",
            romaji: "genki",
            english: "healthy, sound, cheerful",
          },
          { japanese: "ひま", romaji: "hima", english: "free (time)" },
          { japanese: "べんり", romaji: "benri", english: "convenient" },
          {
            japanese: "すてき",
            romaji: "suteki",
            english: "fine, nice, wonderful",
          },

          { japanese: "おおきい", romaji: "ookii", english: "big, large" },
          { japanese: "ちいさい", romaji: "chiisai", english: "small, little" },
          { japanese: "あたらしい", romaji: "atarashii", english: "new" },
          { japanese: "ふるい", romaji: "furui", english: "old (not of age)" },
          { japanese: "いい", romaji: "ii", english: "good" },
          { japanese: "よい", romaji: "yoi", english: "good (formal/variant)" },
          { japanese: "わるい", romaji: "warui", english: "bad" },
          { japanese: "あつい", romaji: "atsui", english: "hot" },
          {
            japanese: "さむい",
            romaji: "samui",
            english: "cold (temperature)",
          },
          { japanese: "つめたい", romaji: "tsumetai", english: "cold (touch)" },
          {
            japanese: "むずかしい",
            romaji: "muzukashii",
            english: "difficult",
          },
          { japanese: "やさしい", romaji: "yasashii", english: "easy" },
          {
            japanese: "たかい",
            romaji: "takai",
            english: "expensive / tall / high",
          },
          { japanese: "やすい", romaji: "yasui", english: "inexpensive" },
          { japanese: "ひくい", romaji: "hikui", english: "low" },
          {
            japanese: "おもしろい",
            romaji: "omoshiroi",
            english: "interesting",
          },
          {
            japanese: "おいしい",
            romaji: "oishii",
            english: "delicious / tasty",
          },
          { japanese: "いそがしい", romaji: "isogashii", english: "busy" },
          { japanese: "たのしい", romaji: "tanoshii", english: "enjoyable" },

          { japanese: "しろい", romaji: "shiroi", english: "white" },
          { japanese: "くろい", romaji: "kuroi", english: "black" },
          { japanese: "あかい", romaji: "akai", english: "red" },
          { japanese: "あおい", romaji: "aoi", english: "blue" },

          { japanese: "さくら", romaji: "sakura", english: "cherry blossom" },
          { japanese: "やま", romaji: "yama", english: "mountain" },
          { japanese: "まち", romaji: "machi", english: "town / city" },
          { japanese: "たべもの", romaji: "tabemono", english: "food" },
          { japanese: "くるま", romaji: "kuruma", english: "car / vehicle" },

          { japanese: "ところ", romaji: "tokoro", english: "place" },
          { japanese: "りょう", romaji: "ryou", english: "dormitory" },

          { japanese: "べんきょう", romaji: "benkyou", english: "study" },
          { japanese: "せいかつ", romaji: "seikatsu", english: "life" },
          {
            japanese: "おしごと",
            romaji: "oshigoto",
            english: "work / business",
          },
          {
            japanese: "しごとをします",
            romaji: "shigoto o shimasu",
            english: "do one’s job / work",
          },

          { japanese: "どう", romaji: "dou", english: "how" },
          { japanese: "どんな", romaji: "donna", english: "what kind of" },
          {
            japanese: "どれ",
            romaji: "dore",
            english: "which one (of three or more)",
          },

          { japanese: "とても", romaji: "totemo", english: "very" },
          {
            japanese: "あまり",
            romaji: "amari",
            english: "not so (used with negatives)",
          },

          {
            japanese: "そして",
            romaji: "soshite",
            english: "and (used to connect sentences)",
          },
          { japanese: "〜が、〜", romaji: "〜ga, 〜", english: "〜, but 〜" },
          {
            japanese: "おげんきですか",
            romaji: "ogenki desu ka",
            english: "How are you?",
          },
          {
            japanese: "そうですね",
            romaji: "sou desu ne",
            english: "Well, let me see",
          },

          {
            japanese: "にほんのせいかつになれましたか",
            romaji: "Nihon no seikatsu ni naremashita ka",
            english: "Have you got used to the life in Japan?",
          },
          {
            japanese: "もういっぱいいかがですか",
            romaji: "mou ippai ikaga desu ka",
            english: "Won’t you have another cup of 〜?",
          },
          {
            japanese: "いいえ、けっこうです",
            romaji: "iie, kekkou desu",
            english: "No, thank you",
          },
          {
            japanese: "もう〜ですね",
            romaji: "mou 〜 desu ne",
            english: "It’s already 〜, isn’t it?",
          },
          {
            japanese: "そろそろしつれいします",
            romaji: "sorosoro shitsurei shimasu",
            english: "It’s almost time to leave now",
          },
          {
            japanese: "またいらっしゃってください",
            romaji: "mata irasshatte kudasai",
            english: "Please come again",
          },

          {
            japanese: "ふじさん",
            romaji: "Fujisan",
            english: "Mt. Fuji, the highest mountain in Japan",
          },
          {
            japanese: "びわこ",
            romaji: "Biwako",
            english: "Lake Biwa, the biggest lake in Japan",
          },
          { japanese: "シャンハイ", romaji: "Shanhai", english: "Shanghai" },
          {
            japanese: "しちにんのさむらい",
            romaji: "Shichinin no Samurai",
            english: "The Seven Samurai (classic movie)",
          },
          {
            japanese: "きんかくじ",
            romaji: "Kinkakuji",
            english: "Kinkakuji Temple (Golden Pavilion)",
          },
        ],

        9: [
          {
            japanese: "わかります",
            romaji: "wakarimasu",
            english: "understand",
          },
          {
            japanese: "あります",
            romaji: "arimasu",
            english: "have / exist (inanimate)",
          },

          { japanese: "すき", romaji: "suki", english: "like" },
          { japanese: "きらい", romaji: "kirai", english: "dislike" },
          { japanese: "じょうず", romaji: "jouzu", english: "good at" },
          { japanese: "へた", romaji: "heta", english: "poor at" },

          { japanese: "りょうり", romaji: "ryouri", english: "dish / cooking" },
          { japanese: "のみもの", romaji: "nomimono", english: "drinks" },
          { japanese: "スポーツ", romaji: "supootsu", english: "sport" },
          { japanese: "やきゅう", romaji: "yakyuu", english: "baseball" },
          { japanese: "ダンス", romaji: "dansu", english: "dance" },
          { japanese: "おんがく", romaji: "ongaku", english: "music" },
          { japanese: "うた", romaji: "uta", english: "song" },
          {
            japanese: "クラシック",
            romaji: "kurashikku",
            english: "classical music",
          },
          { japanese: "ジャズ", romaji: "jazu", english: "jazz" },
          { japanese: "コンサート", romaji: "konsaato", english: "concert" },
          { japanese: "カラオケ", romaji: "karaoke", english: "karaoke" },
          {
            japanese: "かぶき",
            romaji: "kabuki",
            english: "Kabuki (traditional Japanese musical drama)",
          },
          { japanese: "え", romaji: "e", english: "picture / drawing" },
          { japanese: "じ", romaji: "ji", english: "letter / character" },
          {
            japanese: "かんじ",
            romaji: "kanji",
            english: "Chinese characters",
          },
          {
            japanese: "ひらがな",
            romaji: "hiragana",
            english: "Hiragana script",
          },
          {
            japanese: "かたかな",
            romaji: "katakana",
            english: "Katakana script",
          },
          {
            japanese: "ローマじ",
            romaji: "rooma ji",
            english: "Roman alphabet",
          },
          {
            japanese: "こまかいおかね",
            romaji: "komakai okane",
            english: "small change",
          },
          { japanese: "チケット", romaji: "chiketto", english: "ticket" },
          { japanese: "じかん", romaji: "jikan", english: "time" },
          {
            japanese: "ようじ",
            romaji: "youji",
            english: "something to do / errand",
          },
          {
            japanese: "やくそく",
            romaji: "yakusoku",
            english: "appointment / promise",
          },
          {
            japanese: "ごしゅじん",
            romaji: "goshujin",
            english: "(someone else's) husband",
          },
          { japanese: "おっと", romaji: "otto", english: "(my) husband" },
          { japanese: "しゅじん", romaji: "shujin", english: "(my) husband" },
          {
            japanese: "おくさん",
            romaji: "okusan",
            english: "(someone else's) wife",
          },
          { japanese: "つま", romaji: "tsuma", english: "(my) wife" },
          { japanese: "かない", romaji: "kanai", english: "(my) wife" },
          { japanese: "こども", romaji: "kodomo", english: "child" },

          { japanese: "よく", romaji: "yoku", english: "well / much" },
          {
            japanese: "だいたい",
            romaji: "daitai",
            english: "mostly / roughly",
          },
          { japanese: "たくさん", romaji: "takusan", english: "many / much" },
          {
            japanese: "すこし",
            romaji: "sukoshi",
            english: "a little / a few",
          },
          {
            japanese: "ぜんぜん",
            romaji: "zenzen",
            english: "not at all (used with negatives)",
          },
          {
            japanese: "はやく",
            romaji: "hayaku",
            english: "early / quickly / fast",
          },

          { japanese: "〜から", romaji: "〜kara", english: "because 〜" },
          { japanese: "どうして", romaji: "doushite", english: "why" },
          {
            japanese: "ざんねんです",
            romaji: "zannen desu",
            english: "I'm sorry to hear that / That's a pity",
          },
          { japanese: "すみません", romaji: "sumimasen", english: "I'm sorry" },
          {
            japanese: "もしもし",
            romaji: "moshi moshi",
            english: "hello (used on the phone)",
          },
          { japanese: "ああ", romaji: "aa", english: "oh" },
          {
            japanese: "いっしょにいかがですか",
            romaji: "issho ni ikaga desu ka",
            english: "Won’t you join me (us)?",
          },
          {
            japanese: "〜はちょっと",
            romaji: "〜wa chotto",
            english: "〜 is a bit difficult (used to decline politely)",
          },
          {
            japanese: "だめですか",
            romaji: "dame desu ka",
            english: "So you cannot (come)?",
          },
          {
            japanese: "またこんどおねがいします",
            romaji: "mata kondo onegai shimasu",
            english: "Please ask me again some other time",
          },

          {
            japanese: "おざわせいじ",
            romaji: "Ozawa Seiji",
            english: "Seiji Ozawa (famous Japanese conductor)",
          },
        ],

        10: [
          {
            japanese: "います",
            romaji: "imasu",
            english: "exist / be (animate)",
          },
          {
            japanese: "あります",
            romaji: "arimasu",
            english: "exist / be (inanimate)",
          },

          { japanese: "いろいろ", romaji: "iroiro", english: "various" },

          { japanese: "おとこのひと", romaji: "otoko no hito", english: "man" },
          {
            japanese: "おんなのひと",
            romaji: "onna no hito",
            english: "woman",
          },
          { japanese: "おとこのこ", romaji: "otoko no ko", english: "boy" },
          { japanese: "おんなのこ", romaji: "onna no ko", english: "girl" },

          { japanese: "いぬ", romaji: "inu", english: "dog" },
          { japanese: "ねこ", romaji: "neko", english: "cat" },
          { japanese: "き", romaji: "ki", english: "tree / wood" },

          { japanese: "もの", romaji: "mono", english: "thing" },
          { japanese: "フィルム", romaji: "firumu", english: "film" },
          { japanese: "でんち", romaji: "denchi", english: "battery" },
          { japanese: "はこ", romaji: "hako", english: "box" },

          { japanese: "スイッチ", romaji: "suicchi", english: "switch" },
          {
            japanese: "れいぞうこ",
            romaji: "reizouko",
            english: "refrigerator",
          },
          { japanese: "テーブル", romaji: "teeburu", english: "table" },
          { japanese: "ベッド", romaji: "beddo", english: "bed" },
          { japanese: "たな", romaji: "tana", english: "shelf" },
          { japanese: "ドア", romaji: "doa", english: "door" },
          { japanese: "まど", romaji: "mado", english: "window" },

          {
            japanese: "ポスト",
            romaji: "posuto",
            english: "mailbox / postbox",
          },
          { japanese: "ビル", romaji: "biru", english: "building" },
          { japanese: "こうえん", romaji: "kouen", english: "park" },
          {
            japanese: "きっさてん",
            romaji: "kissaten",
            english: "coffee shop",
          },
          { japanese: "ほんや", romaji: "honya", english: "bookstore" },
          { japanese: "〜や", romaji: "〜ya", english: "~ store" },
          {
            japanese: "のりば",
            romaji: "noriba",
            english: "boarding area / platform",
          },
          { japanese: "けん", romaji: "ken", english: "prefecture" },

          { japanese: "うえ", romaji: "ue", english: "on / above / over" },
          {
            japanese: "した",
            romaji: "shita",
            english: "under / below / beneath",
          },
          { japanese: "まえ", romaji: "mae", english: "front / before" },
          { japanese: "うしろ", romaji: "ushiro", english: "back / behind" },
          { japanese: "みぎ", romaji: "migi", english: "right (side)" },
          { japanese: "ひだり", romaji: "hidari", english: "left (side)" },
          { japanese: "なか", romaji: "naka", english: "in / inside" },
          { japanese: "そと", romaji: "soto", english: "outside" },
          { japanese: "となり", romaji: "tonari", english: "next to / beside" },
          { japanese: "ちかく", romaji: "chikaku", english: "near / vicinity" },
          { japanese: "あいだ", romaji: "aida", english: "between / among" },

          {
            japanese: "〜や〜など",
            romaji: "〜ya 〜nado",
            english: "〜, 〜, and so on",
          },
          {
            japanese: "いちばん〜",
            romaji: "ichiban 〜",
            english: "the most 〜",
          },
          {
            japanese: "だんめ",
            romaji: "danme",
            english: "the -th shelf (counter for shelves)",
          },

          {
            japanese: "どうもすみません",
            romaji: "doumo sumimasen",
            english: "Thank you",
          },
          {
            japanese: "チリソース",
            romaji: "chiri soosu",
            english: "chili sauce",
          },
          { japanese: "おく", romaji: "oku", english: "the back" },
          {
            japanese: "スパイス・コーナー",
            romaji: "supaisu koonaa",
            english: "spice corner",
          },

          {
            japanese: "とうきょうディズニーランド",
            romaji: "Toukyou Dizuniirando",
            english: "Tokyo Disneyland",
          },
        ],

        11: [
          { japanese: "います", romaji: "imasu", english: "have (a child)" },
          {
            japanese: "います",
            romaji: "imasu",
            english: "stay / be (in Japan)",
          },
          {
            japanese: "かかります",
            romaji: "kakarimasu",
            english: "take (time or money)",
          },
          {
            japanese: "やすみます",
            romaji: "yasumimasu",
            english: "take a day off (work)",
          },

          { japanese: "ひとつ", romaji: "hitotsu", english: "one (thing)" },
          { japanese: "ふたつ", romaji: "futatsu", english: "two" },
          { japanese: "みっつ", romaji: "mittsu", english: "three" },
          { japanese: "よっつ", romaji: "yottsu", english: "four" },
          { japanese: "いつつ", romaji: "itsutsu", english: "five" },
          { japanese: "むっつ", romaji: "muttsu", english: "six" },
          { japanese: "ななつ", romaji: "nanatsu", english: "seven" },
          { japanese: "やっつ", romaji: "yattsu", english: "eight" },
          { japanese: "ここのつ", romaji: "kokonotsu", english: "nine" },
          { japanese: "とお", romaji: "too", english: "ten" },
          { japanese: "いくつ", romaji: "ikutsu", english: "how many" },
          { japanese: "ひとり", romaji: "hitori", english: "one person" },
          { japanese: "ふたり", romaji: "futari", english: "two persons" },
          { japanese: "ひとり", romaji: "hitori", english: "one person" },
          { japanese: "〜にん", romaji: "〜nin", english: "〜 people" },

          {
            japanese: "〜だい",
            romaji: "〜dai",
            english: "counter for machines / cars",
          },
          {
            japanese: "〜まい",
            romaji: "〜mai",
            english: "counter for paper / stamps",
          },
          { japanese: "〜かい", romaji: "〜kai", english: "〜 times" },

          { japanese: "りんご", romaji: "ringo", english: "apple" },
          { japanese: "みかん", romaji: "mikan", english: "mandarin orange" },
          {
            japanese: "サンドイッチ",
            romaji: "sandoicchi",
            english: "sandwich",
          },
          {
            japanese: "カレーライス",
            romaji: "karee raisu",
            english: "curry and rice",
          },
          {
            japanese: "アイスクリーム",
            romaji: "aisukuriimu",
            english: "ice cream",
          },

          { japanese: "きって", romaji: "kitte", english: "postage stamp" },
          { japanese: "はがき", romaji: "hagaki", english: "post card" },
          { japanese: "ふうとう", romaji: "fuutou", english: "envelope" },
          {
            japanese: "そくたつ",
            romaji: "sokutatsu",
            english: "special delivery",
          },
          {
            japanese: "かきとめ",
            romaji: "kakitome",
            english: "registered mail",
          },
          { japanese: "エアメール", romaji: "eamēru", english: "airmail" },
          { japanese: "こうくうびん", romaji: "koukuubin", english: "airmail" },
          { japanese: "ふなびん", romaji: "funabin", english: "sea mail" },
          { japanese: "りょうしん", romaji: "ryoushin", english: "parents" },
          {
            japanese: "きょうだい",
            romaji: "kyoudai",
            english: "brothers and sisters",
          },
          { japanese: "あに", romaji: "ani", english: "(my) elder brother" },
          {
            japanese: "おにいさん",
            romaji: "oniisan",
            english: "(someone else's) elder brother",
          },
          { japanese: "あね", romaji: "ane", english: "(my) elder sister" },
          {
            japanese: "おねえさん",
            romaji: "oneesan",
            english: "(someone else's) elder sister",
          },
          {
            japanese: "おとうと",
            romaji: "otouto",
            english: "(my) younger brother",
          },
          {
            japanese: "おとうとさん",
            romaji: "otouto san",
            english: "(someone else's) younger brother",
          },
          {
            japanese: "いもうと",
            romaji: "imouto",
            english: "(my) younger sister",
          },
          {
            japanese: "いもうとさん",
            romaji: "imouto san",
            english: "(someone else's) younger sister",
          },

          {
            japanese: "がいこく",
            romaji: "gaikoku",
            english: "foreign country",
          },

          { japanese: "〜じかん", romaji: "〜jikan", english: "〜 hours" },
          {
            japanese: "〜しゅうかん",
            romaji: "〜shuukan",
            english: "〜 weeks",
          },
          { japanese: "〜かげつ", romaji: "〜kagetsu", english: "〜 months" },
          { japanese: "〜ねん", romaji: "〜nen", english: "〜 years" },
          { japanese: "〜ぐらい", romaji: "〜gurai", english: "about 〜" },
          { japanese: "どのくらい", romaji: "dono kurai", english: "how long" },

          { japanese: "ぜんぶで", romaji: "zenbu de", english: "in total" },
          { japanese: "みんな", romaji: "minna", english: "all / everything" },
          { japanese: "〜だけ", romaji: "〜dake", english: "only 〜" },
          {
            japanese: "いらっしゃいませ",
            romaji: "irasshaimase",
            english: "Welcome / May I help you?",
          },
          {
            japanese: "いいおてんきですね",
            romaji: "ii otenki desu ne",
            english: "Nice weather, isn’t it?",
          },
          {
            japanese: "おでかけですか",
            romaji: "odekake desu ka",
            english: "Are you going out?",
          },
          {
            japanese: "ちょっと〜まで",
            romaji: "chotto 〜 made",
            english: "I’m just going to 〜",
          },
          {
            japanese: "いっていらっしゃい",
            romaji: "itte irasshai",
            english: "So long (Go and come back)",
          },
          {
            japanese: "いってまいります",
            romaji: "itte mairimasu",
            english: "So long (I’m going and coming back)",
          },
          {
            japanese: "それから",
            romaji: "sorekara",
            english: "and / furthermore",
          },
          {
            japanese: "オーストラリア",
            romaji: "Oosutoraria",
            english: "Australia",
          },
        ],

        12: [
          { japanese: "かんたん", romaji: "kantan", english: "easy / simple" },
          { japanese: "ちかい", romaji: "chikai", english: "near" },
          { japanese: "とおい", romaji: "tooi", english: "far" },
          { japanese: "はやい", romaji: "hayai", english: "fast / early" },
          { japanese: "おそい", romaji: "osoi", english: "slow / late" },
          {
            japanese: "おおい",
            romaji: "ooi",
            english: "many / much (people)",
          },
          {
            japanese: "すくない",
            romaji: "sukunai",
            english: "few / a little (people)",
          },
          { japanese: "あたたかい", romaji: "atatakai", english: "warm" },
          { japanese: "すずしい", romaji: "suzushii", english: "cool" },
          { japanese: "あまい", romaji: "amai", english: "sweet" },
          { japanese: "からい", romaji: "karai", english: "hot / spicy" },
          { japanese: "おもい", romaji: "omoi", english: "heavy" },
          { japanese: "かるい", romaji: "karui", english: "light" },
          { japanese: "いい", romaji: "ii", english: "prefer / good" },
          { japanese: "きせつ", romaji: "kisetsu", english: "season" },
          { japanese: "はる", romaji: "haru", english: "spring" },
          { japanese: "なつ", romaji: "natsu", english: "summer" },
          { japanese: "あき", romaji: "aki", english: "autumn / fall" },
          { japanese: "ふゆ", romaji: "fuyu", english: "winter" },

          { japanese: "てんき", romaji: "tenki", english: "weather" },
          { japanese: "あめ", romaji: "ame", english: "rain / rainy" },
          { japanese: "ゆき", romaji: "yuki", english: "snow / snowy" },
          { japanese: "くもり", romaji: "kumori", english: "cloudy" },

          { japanese: "ホテル", romaji: "hoteru", english: "hotel" },
          { japanese: "くうこう", romaji: "kuukou", english: "airport" },
          { japanese: "うみ", romaji: "umi", english: "sea / ocean" },
          { japanese: "せかい", romaji: "sekai", english: "world" },

          { japanese: "パーティー", romaji: "paatii", english: "party" },
          { japanese: "おまつり", romaji: "omatsuri", english: "festival" },
          { japanese: "しけん", romaji: "shiken", english: "examination" },
          {
            japanese: "すきやき",
            romaji: "sukiyaki",
            english: "sukiyaki (beef and vegetable hot pot)",
          },
          {
            japanese: "さしみ",
            romaji: "sashimi",
            english: "sashimi (sliced raw fish)",
          },
          {
            japanese: "おすし",
            romaji: "osushi",
            english: "sushi (vinegared rice topped with raw fish)",
          },
          {
            japanese: "てんぷら",
            romaji: "tenpura",
            english: "tempura (deep-fried seafood and vegetables)",
          },

          {
            japanese: "いけばな",
            romaji: "ikebana",
            english: "flower arrangement",
          },
          {
            japanese: "もみじ",
            romaji: "momiji",
            english: "maple / red leaves of autumn",
          },

          {
            japanese: "どちら",
            romaji: "dochira",
            english: "which one (between two)",
          },
          { japanese: "どちらも", romaji: "dochiramo", english: "both" },

          { japanese: "ずっと", romaji: "zutto", english: "by far" },
          {
            japanese: "はじめて",
            romaji: "hajimete",
            english: "for the first time",
          },

          { japanese: "ただいま", romaji: "tadaima", english: "I'm home" },
          {
            japanese: "おかえりなさい",
            romaji: "okaerinasai",
            english: "Welcome home",
          },
          {
            japanese: "すごいですね",
            romaji: "sugoi desu ne",
            english: "That's amazing",
          },
          { japanese: "でも", romaji: "demo", english: "but" },
          {
            japanese: "つかれました",
            romaji: "tsukaremashita",
            english: "I'm tired",
          },
          {
            japanese: "ぎおんまつり",
            romaji: "Gion Matsuri",
            english: "the Gion Festival (Kyoto’s most famous festival)",
          },
          { japanese: "ホンコン", romaji: "Honkon", english: "Hong Kong" },
          {
            japanese: "シンガポール",
            romaji: "Shingapooru",
            english: "Singapore",
          },
          {
            japanese: "まいにちや",
            romaji: "Mainichi ya",
            english: "fictitious supermarket",
          },
          {
            japanese: "ABCストア",
            romaji: "ABC sutoa",
            english: "fictitious supermarket",
          },
          {
            japanese: "ジャパン",
            romaji: "Japan",
            english: "fictitious supermarket",
          },
        ],
        13: [
          {
            japanese: "あそびます",
            romaji: "asobimasu",
            english: "enjoy oneself / play",
          },
          { japanese: "およぎます", romaji: "oyogimasu", english: "swim" },
          {
            japanese: "むかえます",
            romaji: "mukaemasu",
            english: "go to meet / welcome",
          },
          {
            japanese: "つかれます",
            romaji: "tsukaremasu",
            english: "get tired",
          },
          {
            japanese: "だします",
            romaji: "dashimasu",
            english: "send (a letter)",
          },
          {
            japanese: "はいります",
            romaji: "hairimasu",
            english: "enter (a coffee shop)",
          },
          {
            japanese: "でます",
            romaji: "demasu",
            english: "go out (of a coffee shop)",
          },
          {
            japanese: "けっこんします",
            romaji: "kekkon shimasu",
            english: "marry / get married",
          },
          {
            japanese: "かいものします",
            romaji: "kaimono shimasu",
            english: "do shopping",
          },
          {
            japanese: "しょくじします",
            romaji: "shokuji shimasu",
            english: "have a meal / dine",
          },
          {
            japanese: "さんぽします",
            romaji: "sanpo shimasu",
            english: "take a walk (in a park)",
          },

          {
            japanese: "たいへん",
            romaji: "taihen",
            english: "hard / tough / severe / awful",
          },
          { japanese: "ほしい", romaji: "hoshii", english: "want (something)" },
          { japanese: "さびしい", romaji: "sabishii", english: "lonely" },
          { japanese: "ひろい", romaji: "hiroi", english: "wide / spacious" },
          {
            japanese: "せまい",
            romaji: "semai",
            english: "narrow / small (room)",
          },

          {
            japanese: "しやくしょ",
            romaji: "shiyakusho",
            english: "municipal office / city hall",
          },
          { japanese: "プール", romaji: "puuru", english: "swimming pool" },
          { japanese: "かわ", romaji: "kawa", english: "river" },

          { japanese: "けいざい", romaji: "keizai", english: "economy" },
          { japanese: "びじゅつ", romaji: "bijutsu", english: "fine arts" },
          { japanese: "つり", romaji: "tsuri", english: "fishing" },
          { japanese: "スキー", romaji: "sukii", english: "skiing" },
          {
            japanese: "かいぎ",
            romaji: "kaigi",
            english: "meeting / conference",
          },
          { japanese: "とうろく", romaji: "touroku", english: "registration" },

          { japanese: "しゅうまつ", romaji: "shuumatsu", english: "weekend" },
          { japanese: "〜ごろ", romaji: "〜goro", english: "about (time)" },
          { japanese: "なにか", romaji: "nanika", english: "something" },
          {
            japanese: "どこか",
            romaji: "dokoka",
            english: "somewhere / some place",
          },
          {
            japanese: "おなかが すきました",
            romaji: "onaka ga sukimashita",
            english: "(I'm) hungry",
          },
          {
            japanese: "おなかが いっぱいです",
            romaji: "onaka ga ippai desu",
            english: "(I'm) full",
          },
          {
            japanese: "のどが かわきました",
            romaji: "nodo ga kawakimashita",
            english: "(I'm) thirsty",
          },
          {
            japanese: "そうですね",
            romaji: "sou desu ne",
            english: "I agree with you",
          },
          {
            japanese: "そうしましょう",
            romaji: "sou shimashou",
            english: "Let's do that",
          },
          {
            japanese: "ごちゅうもんは？",
            romaji: "gochuumon wa?",
            english: "May I take your order?",
          },
          { japanese: "ていしょく", romaji: "teishoku", english: "set meal" },
          {
            japanese: "ぎゅうどん",
            romaji: "gyuudon",
            english: "bowl of rice topped with beef",
          },
          {
            japanese: "しょうしょう おまちください",
            romaji: "shou shou omachi kudasai",
            english: "Please wait a moment",
          },
          {
            japanese: "べつべつに",
            romaji: "betsu betsu ni",
            english: "separately",
          },
          { japanese: "ロシア", romaji: "Roshia", english: "Russia" },
          {
            japanese: "つるや",
            romaji: "Tsuruya",
            english: "fictitious Japanese restaurant",
          },
          {
            japanese: "おはようテレビ",
            romaji: "Ohayou Terebi",
            english: "fictitious TV program",
          },
        ],

        14: [
          { japanese: "つけます", romaji: "tsukemasu", english: "turn on" },
          { japanese: "けします", romaji: "keshimasu", english: "turn off" },
          { japanese: "あけます", romaji: "akemasu", english: "open" },
          {
            japanese: "しめます",
            romaji: "shimemasu",
            english: "close / shut",
          },
          { japanese: "いそぎます", romaji: "isogimasu", english: "hurry" },
          { japanese: "まちます", romaji: "machimasu", english: "wait" },
          { japanese: "とめます", romaji: "tomemasu", english: "stop / park" },
          { japanese: "まがります", romaji: "magarimasu", english: "turn" },
          { japanese: "みぎへ", romaji: "migi e", english: "to the right" },
          { japanese: "もちます", romaji: "mochimasu", english: "hold" },
          { japanese: "とります", romaji: "torimasu", english: "take / pass" },
          {
            japanese: "てつだいます",
            romaji: "tetsudaimasu",
            english: "help (with a task)",
          },
          { japanese: "よびます", romaji: "yobimasu", english: "call" },
          {
            japanese: "はなします",
            romaji: "hanashimasu",
            english: "speak / talk",
          },
          { japanese: "みせます", romaji: "misemasu", english: "show" },
          {
            japanese: "おしえます",
            romaji: "oshiemasu",
            english: "tell (information/address)",
          },
          {
            japanese: "じゅうしょを",
            romaji: "juusho o",
            english: "an address",
          },
          {
            japanese: "はじめます",
            romaji: "hajimemasu",
            english: "start / begin",
          },
          { japanese: "ふります", romaji: "furimasu", english: "rain" },
          {
            japanese: "あめが",
            romaji: "ame ga",
            english: "rain (subject marker)",
          },
          {
            japanese: "コピーします",
            romaji: "kopii shimasu",
            english: "copy",
          },

          { japanese: "エアコン", romaji: "eakon", english: "air conditioner" },
          { japanese: "パスポート", romaji: "pasupooto", english: "passport" },
          { japanese: "なまえ", romaji: "namae", english: "name" },
          { japanese: "じゅうしょ", romaji: "juusho", english: "address" },
          { japanese: "ちず", romaji: "chizu", english: "map" },
          { japanese: "しお", romaji: "shio", english: "salt" },
          { japanese: "さとう", romaji: "satou", english: "sugar" },
          {
            japanese: "よみかた",
            romaji: "yomikata",
            english: "how to read / way of reading",
          },
          {
            japanese: "〜かた",
            romaji: "~kata",
            english: "how to ~ / way of ~ ing",
          },

          {
            japanese: "ゆっくり",
            romaji: "yukkuri",
            english: "slowly / leisurely",
          },
          { japanese: "すぐ", romaji: "sugu", english: "immediately" },
          { japanese: "また", romaji: "mata", english: "again" },
          { japanese: "あとで", romaji: "atode", english: "later" },
          {
            japanese: "もうすこし",
            romaji: "mou sukoshi",
            english: "a little more",
          },
          {
            japanese: "もう〜",
            romaji: "mou ~",
            english: "~ more / another ~",
          },

          {
            japanese: "しんごうを みぎへ まがって ください",
            romaji: "shingou o migi e magatte kudasai",
            english: "Turn to the right at the signal",
          },
          { japanese: "まっすぐ", romaji: "massugu", english: "straight" },
          {
            japanese: "これで おねがいします",
            romaji: "kore de onegaishimasu",
            english: "I'd like to pay with this",
          },
          { japanese: "おつり", romaji: "otsuri", english: "change" },

          {
            japanese: "うめだ",
            romaji: "Umeda",
            english: "name of a town in Osaka",
          },
        ],
        15: [
          { japanese: "たちます", romaji: "tachimasu", english: "stand up" },
          { japanese: "すわります", romaji: "suwarimasu", english: "sit down" },
          { japanese: "つかいます", romaji: "tsukaimasu", english: "use" },
          { japanese: "おきます", romaji: "okimasu", english: "put" },
          {
            japanese: "つくります",
            romaji: "tsukurimasu",
            english: "make / produce",
          },
          { japanese: "うります", romaji: "urimasu", english: "sell" },
          { japanese: "しります", romaji: "shirimasu", english: "get to know" },
          {
            japanese: "すみます",
            romaji: "sumimasu",
            english: "be going to live",
          },
          {
            japanese: "けんきゅうします",
            romaji: "kenkyuu shimasu",
            english: "do research",
          },
          { japanese: "しっています", romaji: "shitte imasu", english: "know" },
          { japanese: "すんでいます", romaji: "sunde imasu", english: "live" },
          { japanese: "おおさかに", romaji: "oosaka ni", english: "in Osaka" },

          {
            japanese: "しりょう",
            romaji: "shiryou",
            english: "materials / data",
          },
          { japanese: "カタログ", romaji: "katarogu", english: "catalog" },
          {
            japanese: "じこくひょう",
            romaji: "jikokuhyou",
            english: "timetable",
          },
          { japanese: "ふく", romaji: "fuku", english: "clothes" },
          { japanese: "せいひん", romaji: "seihin", english: "products" },
          { japanese: "ソフト", romaji: "sofuto", english: "software" },

          {
            japanese: "せんもん",
            romaji: "senmon",
            english: "speciality / field of study",
          },
          {
            japanese: "はいしゃ",
            romaji: "haisha",
            english: "dentist / dentist’s",
          },
          {
            japanese: "とこや",
            romaji: "tokoya",
            english: "barber / barber’s",
          },
          {
            japanese: "プレイガイド",
            romaji: "pureigaido",
            english: "(theater) ticket agency",
          },
          {
            japanese: "どくしん",
            romaji: "dokushin",
            english: "single / unmarried",
          },

          { japanese: "とくに", romaji: "tokuni", english: "especially" },
          {
            japanese: "おもいだします",
            romaji: "omoidasemasu",
            english: "remember / recollect",
          },

          { japanese: "ごかぞく", romaji: "gokazoku", english: "your family" },
          {
            japanese: "いらっしゃいます",
            romaji: "irasshaimasu",
            english: "be (honorific equivalent of います)",
          },
          {
            japanese: "こうこう",
            romaji: "koukou",
            english: "senior high school",
          },

          {
            japanese: "にっぽんばし",
            romaji: "Nipponbashi",
            english: "name of a shopping district in Osaka",
          },
        ],
        16: [
          { japanese: "のります", romaji: "norimasu", english: "ride, get on" },
          {
            japanese: "でんしゃに",
            romaji: "densha ni",
            english: "onto a train",
          },

          { japanese: "おります", romaji: "orimasu", english: "get off" },
          {
            japanese: "でんしゃを",
            romaji: "densha o",
            english: "from a train",
          },

          {
            japanese: "のりかえます",
            romaji: "norikaemasu",
            english: "change (trains, etc.)",
          },

          { japanese: "あびます", romaji: "abimasu", english: "take a shower" },
          { japanese: "シャワーを", romaji: "shawaa o", english: "shower" },

          {
            japanese: "いれます",
            romaji: "iremasu",
            english: "put in, insert",
          },
          {
            japanese: "だします",
            romaji: "dashimasu",
            english: "take out, withdraw",
          },

          { japanese: "はいります", romaji: "hairimasu", english: "enter" },
          {
            japanese: "だいがくに",
            romaji: "daigaku ni",
            english: "into university",
          },

          { japanese: "でます", romaji: "demasu", english: "graduate from" },
          {
            japanese: "だいがくを",
            romaji: "daigaku o",
            english: "from university",
          },

          {
            japanese: "やめます",
            romaji: "yamemasu",
            english: "quit, retire, stop, give up",
          },
          { japanese: "かいしゃを", romaji: "kaisha o", english: "company" },

          { japanese: "おします", romaji: "oshimasu", english: "push, press" },

          { japanese: "わかい", romaji: "wakai", english: "young" },
          { japanese: "ながい", romaji: "nagai", english: "long" },
          { japanese: "みじかい", romaji: "mijikai", english: "short" },
          { japanese: "あかるい", romaji: "akarui", english: "bright, light" },
          { japanese: "くらい", romaji: "kurai", english: "dark" },
          { japanese: "おてら", romaji: "otera", english: "Buddhist temple" },
          { japanese: "じんじゃ", romaji: "jinja", english: "Shinto shrine" },
          {
            japanese: "りゅうがくせい",
            romaji: "ryuugakusei",
            english: "foreign student",
          },
          { japanese: "いちばん", romaji: "ichiban", english: "number one" },
          {
            japanese: "どうやって",
            romaji: "douyatte",
            english: "in what way, how",
          },
          {
            japanese: "どの",
            romaji: "dono",
            english: "which (used for three or more)",
          },
          {
            japanese: "いいえ、まだまだです。",
            romaji: "iie, madamada desu.",
            english: "[No,] I still have a long way to go.",
          },
          { japanese: "かいわ", romaji: "kaiwa", english: "conversation" },
          {
            japanese: "おひきだしですか。",
            romaji: "ohikidashi desu ka.",
            english: "Are you making a withdrawal?",
          },
          { japanese: "まず", romaji: "mazu", english: "first of all" },
          {
            japanese: "キャッシュカード",
            romaji: "kyasshu kaado",
            english: "cash dispensing card",
          },
          {
            japanese: "あんしょうばんごう",
            romaji: "anshou bangou",
            english: "personal identification number, PIN",
          },
          {
            japanese: "つぎに",
            romaji: "tsugi ni",
            english: "next, as a next step",
          },
          {
            japanese: "きんがく",
            romaji: "kingaku",
            english: "amount of money",
          },
          {
            japanese: "かくにん",
            romaji: "kakunin",
            english: "confirmation (~ shimasu: confirm)",
          },
          { japanese: "ボタン", romaji: "botan", english: "button" },
          {
            japanese: "ジェイアール",
            romaji: "jēaru",
            english: "Japan Railway",
          },
          { japanese: "アジア", romaji: "ajia", english: "Asia" },
          {
            japanese: "バンドン",
            romaji: "bandon",
            english: "Bandung (in Indonesia)",
          },
          {
            japanese: "ベラクルス",
            romaji: "berakurusu",
            english: "Veracruz (in Mexico)",
          },
          {
            japanese: "フランケン",
            romaji: "furanken",
            english: "Franken (in Germany)",
          },
          { japanese: "ベトナム", romaji: "betonamu", english: "Vietnam" },
          { japanese: "フエ", romaji: "fue", english: "Hue (in Vietnam)" },
          {
            japanese: "だいがくまえ",
            romaji: "daigakumae",
            english: "fictitious bus stop",
          },
        ],

        17: [
          { japanese: "おぼえます", romaji: "oboemasu", english: "memorize" },
          { japanese: "わすれます", romaji: "wasuremasu", english: "forget" },
          { japanese: "なくします", romaji: "nakushimasu", english: "lose" },
          {
            japanese: "だします",
            romaji: "dashimasu",
            english: "hand in (a report)",
          },
          { japanese: "はらいます", romaji: "haraimasu", english: "pay" },
          {
            japanese: "かえします",
            romaji: "kaeshimasu",
            english: "give back, return",
          },
          { japanese: "でかけます", romaji: "dekakemasu", english: "go out" },
          {
            japanese: "ぬぎます",
            romaji: "nugimasu",
            english: "take off (clothes, shoes)",
          },
          {
            japanese: "もっていきます",
            romaji: "motte ikimasu",
            english: "take (something)",
          },
          {
            japanese: "もってきます",
            romaji: "motte kimasu",
            english: "bring (something)",
          },
          {
            japanese: "しんぱいします",
            romaji: "shinpai shimasu",
            english: "worry",
          },
          {
            japanese: "ざんぎょうします",
            romaji: "zangyou shimasu",
            english: "work overtime",
          },
          {
            japanese: "しゅっちょうします",
            romaji: "shucchou shimasu",
            english: "go on a business trip",
          },
          {
            japanese: "のみます",
            romaji: "nomimasu",
            english: "take (medicine)",
          },
          {
            japanese: "はいります",
            romaji: "hairimasu",
            english: "take (a bath)",
          },

          {
            japanese: "たいせつ",
            romaji: "taisetsu",
            english: "important, precious",
          },
          {
            japanese: "だいじょうぶ",
            romaji: "daijoubu",
            english: "all right",
          },
          { japanese: "あぶない", romaji: "abunai", english: "dangerous" },

          {
            japanese: "もんだい",
            romaji: "mondai",
            english: "question, problem, trouble",
          },
          { japanese: "こたえ", romaji: "kotae", english: "answer" },

          { japanese: "きんえん", romaji: "kinen", english: "no smoking" },
          {
            japanese: "けんこうほけんしょう",
            romaji: "kenkou hokenshou",
            english: "health insurance card",
          },

          { japanese: "かぜ", romaji: "kaze", english: "cold, flu" },
          { japanese: "ねつ", romaji: "netsu", english: "fever" },
          {
            japanese: "びょうき",
            romaji: "byouki",
            english: "illness, disease",
          },
          { japanese: "くすり", romaji: "kusuri", english: "medicine" },

          { japanese: "おふろ", romaji: "ofuro", english: "bath" },
          { japanese: "うわぎ", romaji: "uwagi", english: "jacket, outerwear" },
          { japanese: "したぎ", romaji: "shitagi", english: "underwear" },
          {
            japanese: "せんせい",
            romaji: "sensei",
            english: "doctor (used when addressing a medical doctor)",
          },

          {
            japanese: "にさんにち",
            romaji: "ni san nichi",
            english: "a few days",
          },
          { japanese: "にさん", romaji: "ni san", english: "a few (counter)" },
          {
            japanese: "までに",
            romaji: "made ni",
            english: "before, by (time limit)",
          },
          {
            japanese: "ですから",
            romaji: "desu kara",
            english: "therefore, so",
          },

          {
            japanese: "どうしましたか",
            romaji: "dou shimashita ka",
            english: "what’s the matter?",
          },
          {
            japanese: "いたいです",
            romaji: "itai desu",
            english: "I have a pain",
          },
          { japanese: "のど", romaji: "nodo", english: "throat" },
          {
            japanese: "おだいじに",
            romaji: "odaiji ni",
            english: "take care of yourself",
          },
        ],

        18: [
          {
            japanese: "できます",
            romaji: "dekimasu",
            english: "be able to, can",
          },
          { japanese: "あらいます", romaji: "araimasu", english: "wash" },
          {
            japanese: "ひきます",
            romaji: "hikimasu",
            english: "play (stringed instrument or piano)",
          },
          { japanese: "うたいます", romaji: "utaimasu", english: "sing" },
          {
            japanese: "あつめます",
            romaji: "atsumemasu",
            english: "collect, gather",
          },
          { japanese: "すてます", romaji: "sutemasu", english: "throw away" },
          {
            japanese: "かえます",
            romaji: "kaemasu",
            english: "exchange, change",
          },
          {
            japanese: "うんてんします",
            romaji: "untenshimasu",
            english: "drive",
          },
          {
            japanese: "よやくします",
            romaji: "yoyakushimasu",
            english: "reserve, book",
          },
          {
            japanese: "けんがくします",
            romaji: "kengakushimasu",
            english: "visit some place for study",
          },

          { japanese: "ピアノ", romaji: "piano", english: "piano" },
          { japanese: "メートル", romaji: "meetoru", english: "meter" },
          { japanese: "こくさい", romaji: "kokusai", english: "international" },
          { japanese: "げんきん", romaji: "genkin", english: "cash" },

          { japanese: "しゅみ", romaji: "shumi", english: "hobby" },
          { japanese: "にっき", romaji: "nikki", english: "diary" },
          { japanese: "おいのり", romaji: "oinori", english: "prayer" },

          { japanese: "かちょう", romaji: "kachou", english: "section chief" },
          {
            japanese: "ぶちょう",
            romaji: "buchou",
            english: "department chief",
          },
          {
            japanese: "しゃちょう",
            romaji: "shachou",
            english: "president of a company",
          },

          { japanese: "どうぶつ", romaji: "doubutsu", english: "animal" },
          { japanese: "うま", romaji: "uma", english: "horse" },
          {
            japanese: "へえ",
            romaji: "hee",
            english: "really! (used when expressing surprise)",
          },
          {
            japanese: "それはおもしろいですね",
            romaji: "sore wa omoshiroi desu ne",
            english: "that must be interesting",
          },
          {
            japanese: "なかなか",
            romaji: "nakanaka",
            english: "not easily (used with negatives)",
          },
          {
            japanese: "ぼくじょう",
            romaji: "bokujou",
            english: "ranch, stock farm",
          },
          {
            japanese: "ほんとうですか",
            romaji: "hontou desu ka",
            english: "really?",
          },
          { japanese: "ぜひ", romaji: "zehi", english: "by all means" },

          {
            japanese: "ビートルズ",
            romaji: "biitoruzu",
            english: "the Beatles",
          },
        ],

        19: [
          {
            japanese: "のぼります",
            romaji: "noborimasu",
            english: "climb (a mountain)",
          },
          {
            japanese: "とまります",
            romaji: "tomarimasu",
            english: "stay (at a hotel)",
          },
          {
            japanese: "そうじします",
            romaji: "souji shimasu",
            english: "clean (a room)",
          },
          {
            japanese: "せんたくします",
            romaji: "sentaku shimasu",
            english: "wash (clothes)",
          },
          {
            japanese: "れんしゅうします",
            romaji: "renshuu shimasu",
            english: "practice",
          },
          { japanese: "なります", romaji: "narimasu", english: "become" },

          { japanese: "ねむい", romaji: "nemui", english: "sleepy" },
          { japanese: "つよい", romaji: "tsuyoi", english: "strong" },
          { japanese: "よわい", romaji: "yowai", english: "weak" },
          {
            japanese: "ちょうしがいい",
            romaji: "choushi ga ii",
            english: "be in good condition",
          },
          {
            japanese: "ちょうしがわるい",
            romaji: "choushi ga warui",
            english: "be in bad condition",
          },

          { japanese: "ちょうし", romaji: "choushi", english: "condition" },

          { japanese: "ゴルフ", romaji: "gorufu", english: "golf" },
          { japanese: "すもう", romaji: "sumou", english: "sumo wrestling" },
          { japanese: "パチンコ", romaji: "pachinko", english: "pinball game" },

          { japanese: "おちゃ", romaji: "ocha", english: "tea ceremony" },
          { japanese: "ひ", romaji: "hi", english: "day, date" },

          { japanese: "いちど", romaji: "ichido", english: "once" },
          {
            japanese: "いちども",
            romaji: "ichido mo",
            english: "not once, never",
          },
          { japanese: "だんだん", romaji: "dandan", english: "gradually" },
          { japanese: "もうすぐ", romaji: "mou sugu", english: "soon" },

          {
            japanese: "おかげさまで",
            romaji: "okage sama de",
            english: "thank you (for help received)",
          },
          {
            japanese: "かんぱい",
            romaji: "kanpai",
            english: "Bottoms up / Cheers",
          },
          {
            japanese: "じつは",
            romaji: "jitsu wa",
            english: "actually / to tell the truth",
          },
          { japanese: "ダイエット", romaji: "daietto", english: "diet" },
          {
            japanese: "なんかいも",
            romaji: "nankai mo",
            english: "many times",
          },
          { japanese: "しかし", romaji: "shikashi", english: "but / however" },
          {
            japanese: "むり",
            romaji: "muri",
            english: "excessive / impossible",
          },
          {
            japanese: "からだにいい",
            romaji: "karada ni ii",
            english: "good for one’s health",
          },
          { japanese: "ケーキ", romaji: "keeki", english: "cake" },

          {
            japanese: "かつしかほくさい",
            romaji: "Katsushika Hokusai",
            english:
              "famous Edo period woodblock artist and painter (1760–1849)",
          },
        ],

        20: [
          {
            japanese: "いります",
            romaji: "irimasu",
            english: "need / require (a visa)",
          },
          {
            japanese: "しらべます",
            romaji: "shirabemasu",
            english: "check / investigate",
          },
          {
            japanese: "なおします",
            romaji: "naoshimasu",
            english: "repair / correct",
          },
          {
            japanese: "しゅうりします",
            romaji: "shuuri shimasu",
            english: "repair",
          },
          {
            japanese: "でんわします",
            romaji: "denwa shimasu",
            english: "phone",
          },

          {
            japanese: "ぼく",
            romaji: "boku",
            english: "I (informal, used by men)",
          },
          {
            japanese: "きみ",
            romaji: "kimi",
            english: "you (informal, used by men)",
          },
          {
            japanese: "〜くん",
            romaji: "〜kun",
            english: "Mr. (informal, used by men)",
          },

          { japanese: "うん", romaji: "un", english: "yes (informal)" },
          { japanese: "ううん", romaji: "uun", english: "no (informal)" },

          {
            japanese: "サラリーマン",
            romaji: "sarariiman",
            english: "salaried worker / office worker",
          },
          { japanese: "ことば", romaji: "kotoba", english: "word / language" },
          { japanese: "ぶっか", romaji: "bukka", english: "commodity prices" },
          {
            japanese: "きもの",
            romaji: "kimono",
            english: "kimono (traditional Japanese attire)",
          },

          { japanese: "ビザ", romaji: "biza", english: "visa" },

          { japanese: "はじめ", romaji: "hajime", english: "the beginning" },
          { japanese: "おわり", romaji: "owari", english: "the end" },

          {
            japanese: "こっち",
            romaji: "kocchi",
            english: "this way / this place (informal)",
          },
          {
            japanese: "そっち",
            romaji: "socchi",
            english: "that way / that place (informal)",
          },
          {
            japanese: "あっち",
            romaji: "acchi",
            english: "that way / that place over there (informal)",
          },
          {
            japanese: "どっち",
            romaji: "docchi",
            english: "which one / which way / where (informal)",
          },
          {
            japanese: "このあいだ",
            romaji: "kono aida",
            english: "the other day",
          },
          { japanese: "みんなで", romaji: "minna de", english: "all together" },
          {
            japanese: "〜けど",
            romaji: "〜kedo",
            english: "〜, but (informal)",
          },

          {
            japanese: "くにへかえるの",
            romaji: "kuni e kaeru no",
            english: "Are you going back to your country?",
          },
          {
            japanese: "どうするの",
            romaji: "dou suru no",
            english: "What will you do?",
          },
          {
            japanese: "どうしようかな",
            romaji: "dou shiyou kana",
            english: "What shall I do?",
          },
          {
            japanese: "よかったら",
            romaji: "yokattara",
            english: "if you like",
          },
          { japanese: "いろいろ", romaji: "iroiro", english: "various" },
        ],

        21: [
          { japanese: "おもいます", romaji: "omoimasu", english: "think" },
          { japanese: "いいます", romaji: "iimasu", english: "say" },
          {
            japanese: "たります",
            romaji: "tarimasu",
            english: "be enough, be sufficient",
          },
          { japanese: "かちます", romaji: "kachimasu", english: "win" },
          {
            japanese: "まけます",
            romaji: "makemasu",
            english: "lose, be beaten",
          },
          {
            japanese: "あります",
            romaji: "arimasu",
            english: "be held, take place (festival)",
          },
          {
            japanese: "やくにたちます",
            romaji: "yaku ni tachimasu",
            english: "be useful",
          },

          { japanese: "むだ", romaji: "muda", english: "wasteful" },
          { japanese: "ふべん", romaji: "fuben", english: "inconvenient" },
          { japanese: "おなじ", romaji: "onaji", english: "the same" },
          { japanese: "すごい", romaji: "sugoi", english: "awful, great" },

          {
            japanese: "しゅしょう",
            romaji: "shushou",
            english: "prime minister",
          },
          {
            japanese: "だいとうりょう",
            romaji: "daitouryou",
            english: "president",
          },

          { japanese: "せいじ", romaji: "seiji", english: "politics" },
          { japanese: "ニュース", romaji: "nyuusu", english: "news" },
          { japanese: "スピーチ", romaji: "supiichi", english: "speech" },
          { japanese: "しあい", romaji: "shiai", english: "game, match" },
          {
            japanese: "アルバイト",
            romaji: "arubaito",
            english: "part-time job",
          },
          { japanese: "いけん", romaji: "iken", english: "opinion" },
          { japanese: "おはなし", romaji: "ohanashi", english: "talk, story" },
          { japanese: "ユーモア", romaji: "yuumoa", english: "humor" },
          { japanese: "むだ", romaji: "muda", english: "waste" },
          { japanese: "デザイン", romaji: "dezain", english: "design" },

          {
            japanese: "こうつう",
            romaji: "koutsuu",
            english: "transportation, traffic",
          },
          { japanese: "ラッシュ", romaji: "rasshu", english: "rush hour" },

          {
            japanese: "さいきん",
            romaji: "saikin",
            english: "recently, these days",
          },
          { japanese: "たぶん", romaji: "tabun", english: "probably, perhaps" },
          { japanese: "きっと", romaji: "kitto", english: "surely" },
          { japanese: "ほんとうに", romaji: "hontou ni", english: "really" },
          { japanese: "そんなに", romaji: "sonna ni", english: "not so much" },
          {
            japanese: "について",
            romaji: "ni tsuite",
            english: "about, concerning",
          },

          {
            japanese: "しかたがありません",
            romaji: "shikata ga arimasen",
            english: "there is no other choice",
          },

          {
            japanese: "しばらくですね",
            romaji: "shibaraku desu ne",
            english: "long time no see",
          },
          {
            japanese: "でものみませんか",
            romaji: "demo nomimasen ka",
            english: "how about drinking or something?",
          },
          {
            japanese: "みないと",
            romaji: "minai to",
            english: "I’ve got to watch it",
          },
          { japanese: "もちろん", romaji: "mochiron", english: "of course" },

          { japanese: "カンガルー", romaji: "kangaruu", english: "kangaroo" },
          {
            japanese: "キャプテン・クック",
            romaji: "kyaputen kukku",
            english: "Captain James Cook",
          },
        ],

        22: [
          {
            japanese: "きます",
            romaji: "kimasu",
            english: "put on (a shirt, etc.)",
          },
          {
            japanese: "はきます",
            romaji: "hakimasu",
            english: "put on (shoes, trousers, etc.)",
          },
          {
            japanese: "かぶります",
            romaji: "kaburimasu",
            english: "put on (a hat, etc.)",
          },
          {
            japanese: "かけます",
            romaji: "kakemasu",
            english: "put on (glasses)",
          },
          { japanese: "うまれます", romaji: "umaremasu", english: "be born" },

          { japanese: "コート", romaji: "kooto", english: "coat" },
          { japanese: "スーツ", romaji: "suutsu", english: "suit" },
          { japanese: "セーター", romaji: "seetaa", english: "sweater" },

          { japanese: "ぼうし", romaji: "boushi", english: "hat, cap" },
          { japanese: "めがね", romaji: "megane", english: "glasses" },

          { japanese: "よく", romaji: "yoku", english: "often" },
          {
            japanese: "おめでとうございます",
            romaji: "omedetou gozaimasu",
            english: "congratulations",
          },

          { japanese: "こちら", romaji: "kochira", english: "this (polite)" },
          { japanese: "やちん", romaji: "yachin", english: "house rent" },
          { japanese: "うーん", romaji: "uun", english: "let me see" },
          {
            japanese: "ダイニングキッチン",
            romaji: "dainingu kicchin",
            english: "kitchen with dining area",
          },
          {
            japanese: "わしつ",
            romaji: "washitsu",
            english: "Japanese-style room",
          },
          {
            japanese: "おしいれ",
            romaji: "oshiire",
            english: "Japanese-style closet",
          },
          {
            japanese: "ふとん",
            romaji: "futon",
            english: "Japanese-style mattress and quilt",
          },
          { japanese: "アパート", romaji: "apaato", english: "apartment" },

          { japanese: "パリ", romaji: "pari", english: "Paris" },
          {
            japanese: "ばんりのちょうじょう",
            romaji: "banri no choujou",
            english: "the Great Wall of China",
          },
          {
            japanese: "よかきゅうかいはつセンター",
            romaji: "yoka kyuukaihatsu sentaa",
            english: "Center for Developing Leisure Activities",
          },
          {
            japanese: "レジャーはくしょ",
            romaji: "rejaa hakusho",
            english: "white paper on leisure",
          },
        ],
        23: [
          {
            japanese: "ききます",
            romaji: "kikimasu",
            english: "ask (the teacher)",
          },
          { japanese: "まわします", romaji: "mawashimasu", english: "turn" },
          { japanese: "ひきます", romaji: "hikimasu", english: "pull" },
          { japanese: "かえます", romaji: "kaemasu", english: "change" },
          {
            japanese: "さわります",
            romaji: "sawarimasu",
            english: "touch (a door)",
          },
          {
            japanese: "でます",
            romaji: "demasu",
            english: "come out (change)",
          },
          {
            japanese: "うごきます",
            romaji: "ugokimasu",
            english: "move, work (a watch)",
          },
          {
            japanese: "あるきます",
            romaji: "arukimasu",
            english: "walk (along a road)",
          },
          {
            japanese: "わたります",
            romaji: "watarimasu",
            english: "cross (a bridge)",
          },
          {
            japanese: "きをつけます",
            romaji: "ki o tsukemasu",
            english: "pay attention, take care",
          },
          {
            japanese: "ひっこしします",
            romaji: "hikkoshi shimasu",
            english: "move (house)",
          },

          { japanese: "でんきや", romaji: "denkiya", english: "electrician" },
          { japanese: "や", romaji: "ya", english: "shop / person of ~" },

          { japanese: "サイズ", romaji: "saizu", english: "size" },
          { japanese: "おと", romaji: "oto", english: "sound" },
          { japanese: "きかい", romaji: "kikai", english: "machine" },
          { japanese: "つまみ", romaji: "tsumami", english: "knob" },
          { japanese: "こしょう", romaji: "koshou", english: "breakdown" },

          { japanese: "みち", romaji: "michi", english: "road, way" },
          { japanese: "こうさてん", romaji: "kousaten", english: "crossroad" },
          { japanese: "しんごう", romaji: "shingou", english: "traffic light" },
          { japanese: "かど", romaji: "kado", english: "corner" },
          { japanese: "はし", romaji: "hashi", english: "bridge" },
          {
            japanese: "ちゅうしゃじょう",
            romaji: "chuushajou",
            english: "parking lot",
          },

          { japanese: "め", romaji: "me", english: "ordinal marker (-th)" },

          {
            japanese: "おしょうがつ",
            romaji: "oshougatsu",
            english: "New Year’s Day",
          },
          {
            japanese: "ごちそうさまでした",
            romaji: "gochisousama deshita",
            english: "that was delicious",
          },

          { japanese: "たてもの", romaji: "tatemono", english: "building" },
          {
            japanese: "がいこくじんとうろくしょう",
            romaji: "gaikokujin touroku shou",
            english: "alien registration card",
          },

          {
            japanese: "しょうとくたいし",
            romaji: "shoutoku taishi",
            english: "Prince Shotoku",
          },
          {
            japanese: "ほうりゅうじ",
            romaji: "houryuuji",
            english: "Horyuji Temple",
          },

          {
            japanese: "げんきちゃ",
            romaji: "genki cha",
            english: "fictitious tea",
          },
          {
            japanese: "ほんだえき",
            romaji: "honda eki",
            english: "fictitious station",
          },
          {
            japanese: "としょかんまえ",
            romaji: "toshokan mae",
            english: "fictitious bus stop",
          },
        ],
        24: [
          { japanese: "くれます", romaji: "kuremasu", english: "give (me)" },
          {
            japanese: "つれていきます",
            romaji: "tsurete ikimasu",
            english: "take (someone)",
          },
          {
            japanese: "つれてきます",
            romaji: "tsurete kimasu",
            english: "bring (someone)",
          },
          {
            japanese: "おくります",
            romaji: "okurimasu",
            english: "escort / go with (someone)",
          },
          {
            japanese: "しょうかいします",
            romaji: "shoukai shimasu",
            english: "introduce",
          },
          {
            japanese: "あんないします",
            romaji: "annai shimasu",
            english: "show around / show the way",
          },
          {
            japanese: "せつめいします",
            romaji: "setsumei shimasu",
            english: "explain",
          },
          { japanese: "いれます", romaji: "iremasu", english: "make (coffee)" },

          {
            japanese: "おじいさん",
            romaji: "ojiisan",
            english: "grandfather / old man",
          },
          {
            japanese: "おじいちゃん",
            romaji: "ojiichan",
            english: "grandfather / old man",
          },
          {
            japanese: "おばあさん",
            romaji: "obaasan",
            english: "grandmother / old woman",
          },
          {
            japanese: "おばあちゃん",
            romaji: "obaachan",
            english: "grandmother / old woman",
          },

          { japanese: "じゅんび", romaji: "junbi", english: "preparation" },
          { japanese: "いみ", romaji: "imi", english: "meaning" },
          { japanese: "おかし", romaji: "okashi", english: "sweets / snacks" },
          { japanese: "ぜんぶ", romaji: "zenbu", english: "all" },
          { japanese: "じぶんで", romaji: "jibun de", english: "by oneself" },
          { japanese: "ほかに", romaji: "hoka ni", english: "besides" },
          {
            japanese: "ワゴンしゃ",
            romaji: "wagonsha",
            english: "station wagon",
          },
          { japanese: "おべんとう", romaji: "obentou", english: "box lunch" },
          {
            japanese: "ははのひ",
            romaji: "Haha no Hi",
            english: "Mother’s Day",
          },
        ],

        25: [
          {
            japanese: "かんがえます",
            romaji: "kangaemasu",
            english: "think, consider",
          },
          {
            japanese: "つきます",
            romaji: "tsukimasu",
            english: "arrive (at the station)",
          },
          {
            japanese: "りゅうがくします",
            romaji: "ryuugaku shimasu",
            english: "study abroad",
          },
          {
            japanese: "とります",
            romaji: "torimasu",
            english: "grow old (take years)",
          },

          {
            japanese: "いなか",
            romaji: "inaka",
            english: "countryside, hometown",
          },
          { japanese: "たいしかん", romaji: "taishikan", english: "embassy" },
          { japanese: "ぐるーぷ", romaji: "guruupu", english: "group" },
          { japanese: "ちゃんす", romaji: "chansu", english: "chance" },

          { japanese: "おく", romaji: "oku", english: "hundred million" },

          { japanese: "もし", romaji: "moshi", english: "if (conditional)" },
          { japanese: "いくら", romaji: "ikura", english: "however / even if" },
          {
            japanese: "てんきん",
            romaji: "tenkin",
            english: "transfer (be transferred to another office)",
          },

          {
            japanese: "こと",
            romaji: "koto",
            english: "thing, matter (about ~)",
          },

          {
            japanese: "いっぱいのみましょう",
            romaji: "ippai nomimashou",
            english: "let’s have a drink together",
          },

          {
            japanese: "いろいろおせわになりました",
            romaji: "iroiro osewa ni narimashita",
            english: "thank you for everything you have done for me",
          },

          {
            japanese: "がんばります",
            romaji: "ganbarimasu",
            english: "do one’s best",
          },

          {
            japanese: "どうぞおげんきで",
            romaji: "douzo ogenki de",
            english: "best of luck (said when expecting a long separation)",
          },
        ],

        26: [
          { japanese: "だれ", romaji: "dare", english: "who" },
          { japanese: "だれの", romaji: "dare no", english: "whose" },

          { japanese: "なに", romaji: "nani", english: "what" },
          {
            japanese: "なん",
            romaji: "nan",
            english: "what (used before certain sounds)",
          },

          { japanese: "どれ", romaji: "dore", english: "which (one)" },
          { japanese: "どの", romaji: "dono", english: "which (+ noun)" },

          { japanese: "どこ", romaji: "doko", english: "where" },
          {
            japanese: "どちら",
            romaji: "dochira",
            english: "which place (polite)",
          },

          { japanese: "いつ", romaji: "itsu", english: "when" },

          { japanese: "どうして", romaji: "doushite", english: "why" },
          { japanese: "なぜ", romaji: "naze", english: "why (formal)" },

          { japanese: "どう", romaji: "dou", english: "how" },

          { japanese: "いくら", romaji: "ikura", english: "how much (price)" },
          {
            japanese: "いくつ",
            romaji: "ikutsu",
            english: "how many / how much",
          },

          {
            japanese: "なんこ",
            romaji: "nanko",
            english: "how many (small objects)",
          },
          {
            japanese: "なんにん",
            romaji: "nannin",
            english: "how many people",
          },
          {
            japanese: "なんまい",
            romaji: "nanmai",
            english: "how many (flat objects)",
          },

          {
            japanese: "どのくらい",
            romaji: "dono kurai",
            english: "how long / how much (degree)",
          },
          {
            japanese: "どれくらい",
            romaji: "dore kurai",
            english: "how long / how much (degree)",
          },

          { japanese: "どんな", romaji: "donna", english: "what kind of" },

          {
            japanese: "どっち",
            romaji: "docchi",
            english: "which direction (casual)",
          },
          {
            japanese: "どちら",
            romaji: "dochira",
            english: "which direction (polite)",
          },
        ],
      };

      let currentVocab = [];
      let currentIndex = 0;
      let score = 0;
      let total = 0;
      let streak = 0;
      let isFlipped = false;
      let allLessonsMode = false;
      let currentMode = "japanese";
      let isMuted = false;

      function speakText(text, lang) {
        if (isMuted) return;
        speechSynthesis.cancel();
        const utterance = new SpeechSynthesisUtterance(text);
        utterance.lang = lang;
        utterance.rate = 0.9;
        utterance.pitch = 1;
        utterance.volume = 0.8;
        speechSynthesis.speak(utterance);
      }

      function toggleMute() {
        isMuted = !isMuted;
        const btn = document.getElementById("muteBtn");
        if (isMuted) {
          btn.textContent = "🔇 Muted";
          btn.classList.add("muted");
        } else {
          btn.textContent = "🔊 Unmute";
          btn.classList.remove("muted");
        }
      }

      function autoSpeakFront() {
        if (currentIndex >= currentVocab.length || isMuted) return;
        const vocab = currentVocab[currentIndex];
        const textToSpeak =
          currentMode === "japanese" ? vocab.japanese : vocab.english;
        const lang = currentMode === "japanese" ? "ja-JP" : "en-US";
        speakText(textToSpeak, lang);
      }

      function setMode(mode) {
        currentMode = mode;
        document
          .querySelectorAll(".mode-btn")
          .forEach((btn) => btn.classList.remove("active"));
        event.target.classList.add("active");
        showCard();
      }

      function initLesson(lessonNum) {
        currentVocab = [...vocabData[lessonNum]];
        shuffleVocab();
        allLessonsMode = false;
        updateStats();
        showCard();
      }

      function practiceAll() {
        currentVocab = [];
        for (let lesson in vocabData) {
          currentVocab.push(...vocabData[lesson]);
        }
        shuffleVocab();
        allLessonsMode = true;
        updateStats();
        showCard();
      }

      function shuffleVocab() {
        for (let i = currentVocab.length - 1; i > 0; i--) {
          const j = Math.floor(Math.random() * (i + 1));
          [currentVocab[i], currentVocab[j]] = [
            currentVocab[j],
            currentVocab[i],
          ];
        }
        currentIndex = 0;
        streak = 0;
        showCard();
      }

      function resetVocab() {
        score = 0;
        total = 0;
        streak = 0;
        currentIndex = 0;
        initLesson(document.getElementById("lessonSelect").value || 1);
      }

      function flipCard() {
        const card = document.getElementById("flashcard");
        card.classList.toggle("flipped");
        isFlipped = !isFlipped;
      }

      function showCard(autoSpeak = true) {
        if (currentIndex >= currentVocab.length || currentIndex < 0) {
          currentIndex = Math.max(
            0,
            Math.min(currentVocab.length - 1, currentIndex)
          );
        }

        const vocab = currentVocab[currentIndex];

        if (currentMode === "japanese") {
          document.getElementById("frontText").textContent = vocab.japanese;
          document.getElementById(
            "frontAudioText"
          ).textContent = `Pronouncing: ${vocab.romaji}`;
        } else {
          document.getElementById("frontText").textContent = vocab.english;
          document.getElementById(
            "frontAudioText"
          ).textContent = `Pronouncing: ${vocab.japanese}`;
        }

        if (currentMode === "japanese") {
          document.getElementById("backText").textContent = vocab.english;
          document.getElementById(
            "backAudioText"
          ).textContent = `Answer: ${vocab.english}`;
        } else {
          document.getElementById("backText").textContent = vocab.japanese;
          document.getElementById(
            "backAudioText"
          ).textContent = `Answer: ${vocab.japanese} (${vocab.romaji})`;
        }

        document.getElementById("cardCounter").textContent = `Card ${
          currentIndex + 1
        } of ${currentVocab.length} (${
          currentMode === "japanese" ? "JP→EN" : "EN→JP"
        })`;

        isFlipped = false;
        document.getElementById("flashcard").classList.remove("flipped");

        if (autoSpeak) {
          setTimeout(autoSpeakFront, 300);
        }
        updateStats();
      }

      function nextCard() {
        if (currentIndex < currentVocab.length - 1) {
          currentIndex++;
        }
        total++;
        score++;
        streak++;
        showCard(true);
      }

      function previousCard() {
        if (currentIndex > 0) {
          currentIndex--;
        }
        showCard(true);
      }

      function updateStats() {
        document.getElementById("score").textContent = score;
        document.getElementById("totalCards").textContent = currentVocab.length;
        document.getElementById("currentIndex").textContent = currentIndex + 1;
        document.getElementById("streak").textContent = streak;
        const progress = total > 0 ? Math.min((score / total) * 100, 100) : 0;
        document.getElementById("progressBar").style.width = progress + "%";
      }

      document
        .getElementById("lessonSelect")
        .addEventListener("change", function () {
          initLesson(parseInt(this.value));
        });

      // Initialize
      createStars();
      initLesson(1);
    </script>
  </body>
</html>
