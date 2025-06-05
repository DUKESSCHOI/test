<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>쿠팡 울산 2W 근무 시작까지 남은 시간</title>
  <style>
    body {
      font-family: 'Noto Sans KR', sans-serif;
      text-align: center;
      background-color: #000;
      color: #fff;
      margin: 0;
      padding: 20px;
      line-height: 1.6;
    }

    #title {
      margin-top: 7rem;
      margin-bottom: 20px;
    }

    .title-line1 {
      font-size: 2rem;
      font-weight: bold;
    }

    .title-line2 {
      font-size: 1.6rem;
      font-weight: bold;
    }

    .timer-container {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      gap: 0;
    }

    #alarm-icon {
      font-size: 1.5rem;
      animation: blink-visibility 1s step-start infinite;
      color: red;
      margin-bottom: 2px;
      line-height: 1;
      user-select: none;
      display: inline-block;
    }

    #timer {
      font-size: 6rem;
      font-weight: bold;
      color: #fff;
      line-height: 1;
    }

    .blinking {
      color: red !important;
      animation: blink-visibility 1s step-start infinite;
    }

    .blinking-icon {
      animation: blink-visibility 1s step-start infinite;
      color: red;
      font-size: 1.5rem;
      line-height: 1;
      user-select: none;
      display: inline-block;
    }

    @keyframes blink-visibility {
      0%, 49% {
        visibility: visible;
      }
      50%, 100% {
        visibility: hidden;
      }
    }

    .address {
      margin-bottom: 10px;
      font-size: 1.5rem;
      color: #ccc;
    }

    img {
      max-height: 150px;
      border-radius: 12px;
    }

    .work-message {
      margin-top: 10px;
      font-size: 1.6rem;
      color: #fff;
      font-weight: bold;
    }

    .progress-bar-container {
      width: 450px;
      height: 20px;
      background-color: #eee;
      border-radius: 10px;
      overflow: hidden;
      margin-top: 20px;
      position: relative;
    }

    .progress-bar-fill {
      height: 100%;
      width: 0%;
      background-color: #0D3BB3;
      transition: width 0.3s ease, background-color 0.3s ease;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .progress-bar-text {
      position: absolute;
      width: 100%;
      text-align: center;
      pointer-events: none;
      user-select: none;
      font-weight: bold;
      font-size: 0.9rem;
      z-index: 1;
    }

    .progress-bar-danger {
      background-color: red !important;
    }

    @media (max-width: 600px) {
      #title {
        margin-top: 6rem;
      }

      #timer {
        font-size: 4rem;
      }

      .title-line1 {
        font-size: 1.5rem;
      }

      .title-line2 {
        font-size: 1.4rem;
        font-weight: bold;
      }

      .address {
        margin-bottom: 10px;
        font-size: 1.3rem;
      }

      .blinking-icon {
        font-size: 1rem;
      }

      .progress-bar-container {
        width: 90%;
        height: 16px;
      }

      .work-message {
        font-size: 1.5rem;
      }
    }
  </style>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap" rel="stylesheet" />
</head>
<body>
  <h1 id="title">
    <div class="title-line1"></div>
    <div class="address">근무지 주소 : 울산광역시 북구 진장동 1047-4</div>
    <div class="title-line2">
      <span id="work-date"></span> 
      <span> 근무 시작까지 남은 시간</span>
    </div>
  </h1>

  <div class="timer-container">
    <div id="alarm-icon" class="blinking-icon">⏰</div>
    <div id="timer">00시간 00분</div>

    <div class="progress-bar-container">
      <div class="progress-bar-fill" id="progress-bar">
        <span class="progress-bar-text" id="progress-text">00:00:00</span>
      </div>
    </div>

    <img src="후보2.png" class="logo" alt="회사 로고" />
    <div class="work-message">신분증 필참 부탁드립니다!</div>
  </div>

  <script>
    function formatDate(date) {
      const month = date.getMonth()+1;
      const day = date.getDate();
      return `${month}월 ${day}일`;
    }

    function getLuminance(r, g, b) {
      const a = [r, g, b].map((v) => {
        v /= 255;
        return v <= 0.03928
          ? v / 12.92
          : Math.pow((v + 0.055) / 1.055, 2.4);
      });
      return 0.2126 * a[0] + 0.7152 * a[1] + 0.0722 * a[2];
    }

    function getContrastTextColor(backgroundColor) {
      const rgb = backgroundColor.match(/\d+/g).map(Number);
      const luminance = getLuminance(rgb[0], rgb[1], rgb[2]);
      return luminance > 0.5 ? '#000000' : '#ffffff';
    }

    function updateTimer() {
      const now = new Date();

      let todayTarget = new Date();
      todayTarget.setHours(12, 0, 0, 0);
      if (now >= todayTarget) {
        todayTarget.setDate(todayTarget.getDate() + 1);
      }

      const diff = todayTarget - now;

      const hours = Math.floor(diff / (1000 * 60 * 60));
      const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((diff % (1000 * 60)) / 1000);

      const hStr = String(hours).padStart(2, "0");
      const mStr = String(minutes).padStart(2, "0");
      const sStr = String(seconds).padStart(2, "0");

      const timerEl = document.getElementById("timer");
      timerEl.innerHTML = `${hStr}시간 ${mStr}분`;

      if (diff < 3 * 60 * 60 * 1000) {
        timerEl.classList.add("blinking");
      } else {
        timerEl.classList.remove("blinking");
      }

      let displayDate = new Date();
      if (now.getHours() < 1 || (now.getHours() === 1 && now.getMinutes() < 30)) {
        displayDate.setDate(displayDate.getDate());
      } else {
        displayDate.setDate(displayDate.getDate() + 1);
      }

      document.querySelector(".title-line1").textContent = "울산1캠프 소분2(2W)";
      document.getElementById("work-date").textContent = formatDate(displayDate);

      let start = new Date(todayTarget);
      start.setDate(start.getDate() - 1);
      const totalPeriod = todayTarget - start;
      const elapsed = now - start;

      const progressPercent = Math.min(100, Math.max(0, (elapsed / totalPeriod) * 100));
      const progressBar = document.getElementById("progress-bar");
      progressBar.style.width = `${progressPercent}%`;

      if (diff < 3 * 60 * 60 * 1000) {
        progressBar.classList.add("progress-bar-danger");
      } else {
        progressBar.classList.remove("progress-bar-danger");
      }

      const progressText = document.getElementById("progress-text");
      progressText.textContent = `${hStr}:${mStr}:${sStr}`;

      const computedBgColor = window.getComputedStyle(progressBar).backgroundColor;
      progressText.style.color = getContrastTextColor(computedBgColor);
    }

    setInterval(updateTimer, 1000);
    updateTimer();
  </script>
</body>
</html>