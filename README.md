<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Valentine?</title>
  <style>
    body {
      height: 100vh;
      margin: 0;
      font-family: Arial, sans-serif;
      background: darkslategray;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      overflow: hidden;
      transition: background 0.5s ease;
    }

    img {
      max-width: 300px;
      border-radius: 12px;
      margin-bottom: 20px;
    }

    h1 {
      color: white;
      margin-bottom: 20px;
    }

    .button-container {
      position: relative;
      display: flex;
      justify-content: center;
      gap: 20px;
      margin-top: 20px;
      width: 100%;
      height: 300px;
      max-width: 600px;
    }

    button {
      font-size: 18px;
      padding: 10px 20px;
      cursor: pointer;
      border: 2px solid transparent;
      border-radius: 5px;
      background-color: #ff69b4;
      color: white;
      font-weight: bold;
      transition: background-color 0.2s ease;
      box-sizing: border-box;
    }

    button:hover {
      background-color: #ff1493;
    }

    button:active {
      background-color: #c71585;
    }

    #yes {
      position: relative;
      z-index: 1;
    }

    #no {
      position: absolute;
      z-index: 2;
      transition: left 0.3s ease, top 0.3s ease;
    }
  </style>
</head>
<body>

  <img id="valentine-img" src="https://i.postimg.cc/tgWMy7QZ/IMG-9206.jpg" alt="Valentine image">

  <h1 id="valentine-question">May I Be Your Valentine? ❤️</h1>

  <div class="button-container">
    <button id="yes" onclick="yes()">Yes</button>
    <button id="no">No</button>
  </div>

  <script>
    const noBtn = document.getElementById("no");
    const yesBtn = document.getElementById("yes");
    const container = document.querySelector(".button-container");
    const minDistance = 100;

    // Helper to place No button at least minDistance away from Yes
    function placeNoButton() {
      const containerRect = container.getBoundingClientRect();
      const containerWidth = containerRect.width;
      const containerHeight = containerRect.height;

      const yesBtnRect = yesBtn.getBoundingClientRect();
      const noBtnWidth = noBtn.offsetWidth;
      const noBtnHeight = noBtn.offsetHeight;

      // Calculate Yes button position relative to container
      const yesRelativeLeft = yesBtnRect.left - containerRect.left;
      const yesRelativeTop = yesBtnRect.top - containerRect.top;
      const yesRight = yesRelativeLeft + yesBtnRect.width;
      const yesBottom = yesRelativeTop + yesBtnRect.height;

      let x, y;
      let attempts = 0;
      const maxAttempts = 100;

      do {
        x = Math.random() * (containerWidth - noBtnWidth);
        y = Math.random() * (containerHeight - noBtnHeight);
        attempts++;

        // Check if position is far enough from Yes button
        const noLeft = x;
        const noRight = x + noBtnWidth;
        const noTop = y;
        const noBottom = y + noBtnHeight;

        const tooClose =
          noRight > yesRelativeLeft - minDistance &&
          noLeft < yesRight + minDistance &&
          noBottom > yesRelativeTop - minDistance &&
          noTop < yesBottom + minDistance;

        if (!tooClose) break;
      } while (attempts < maxAttempts);

      // Clamp position to stay within container
      x = Math.max(0, Math.min(x, containerWidth - noBtnWidth));
      y = Math.max(0, Math.min(y, containerHeight - noBtnHeight));

      noBtn.style.left = x + "px";
      noBtn.style.top = y + "px";
    }

    // Place No button at start
    window.addEventListener("load", placeNoButton);

    // Move No button every time it's clicked
    noBtn.addEventListener("click", placeNoButton);

    // Also reposition on window resize
    window.addEventListener("resize", placeNoButton);

    function yes() {
      document.body.style.background = "darkcyan";

      const question = document.getElementById("valentine-question");
      const img = document.getElementById("valentine-img");
      question.textContent = "Yay! Happy Valentine's Day! 💖";
      img.src = "https://media.giphy.com/media/l0MYt5jPR6QX5pnqM/giphy.gif";
      img.alt = "Celebration";

      yesBtn.style.display = "none";
      noBtn.style.display = "none";
    }
  </script>

</body>
</html>
