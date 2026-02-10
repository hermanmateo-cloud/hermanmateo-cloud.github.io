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
      min-height: 60px; /* space for No button */
      width: 100%;
      max-width: 400px;
    }

    button {
      font-size: 18px;
      padding: 10px 20px;
      cursor: pointer;
      z-index: 1;
    }

    #no {
      position: absolute;
      top: 0;
      z-index: 2;
      transition: left 0.2s ease, top 0.2s ease;
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
    const minDistance = 96; // 1 inch away

    // Helper to place No button at least minDistance away from Yes
    function placeNoButton() {
      const containerWidth = container.clientWidth;
      const containerHeight = container.clientHeight;

      const yesLeft = yesBtn.offsetLeft;
      const yesRight = yesLeft + yesBtn.offsetWidth;

      let x, y;

      do {
        x = Math.random() * (containerWidth - noBtn.offsetWidth);
        y = Math.random() * (containerHeight - noBtn.offsetHeight);
      } while (
        x + noBtn.offsetWidth > yesLeft - minDistance &&
        x < yesRight + minDistance
      );

      noBtn.style.left = x + "px";
      noBtn.style.top = y + "px";
    }

    // Place No button at start
    placeNoButton();

    // Move No button every time it's clicked
    noBtn.addEventListener("click", placeNoButton);

    function yes() {
      document.body.style.background = "darkcyan";

      const question = document.getElementById("valentine-question");
      const img = document.getElementById("valentine-img");
      question.textContent = "Yay! Happy Valentine’s Day! 💖";
      img.src = "https://media.giphy.com/media/l0MYt5jPR6QX5pnqM/giphy.gif";
      img.alt = "Celebration";

      yesBtn.style.display = "none";
      noBtn.style.display = "none";
    }
  </script>

</body>
</html>
