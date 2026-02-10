# hermanmateo-cloud.github.io
<!DOCTYPE html>
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

    /* Allow the No button to move anywhere on the viewport */
    #no {
      position: fixed;
      z-index: 9999;
      transition: left 0.2s ease, top 0.2s ease, transform 0.2s ease;
      will-change: left, top, transform;
    }
  </style>
</head>
<body>

  <img id="valentine-img" src="https://i.postimg.cc/tgWMy7QZ/IMG-9206.jpg" alt="Valentine image">


## Publish with GitHub Pages

- **Automatic deploy:** I added a GitHub Actions workflow at `.github/workflows/deploy.yml` that will publish the repository root to GitHub Pages whenever you push to the `main` branch.
- **To enable:** push your changes to GitHub (if not already pushed):

```bash
git add .
git commit -m "Add GitHub Pages workflow"
git push origin main
```

- **Confirm:** open your repository on GitHub → Settings → Pages. The workflow will create a Pages deployment; ensure the Pages permission and branch settings are correct if you prefer a specific source.

- **URL:** once deployed the site will be available at `https://<your-username>.github.io/Safe_Link1/` (replace `<your-username>` with your GitHub username). For a quick preview you can also use:

```
https://raw.githack.com/<owner>/Safe_Link1/main/index.html
```

If you want, I can also add a branch-based `gh-pages` deployment or push these changes for you (requires repo push access).
  <h1 id="valentine-question">May I be your Valentine? ❤️</h1>

  <div class="button-container">
    <button id="yes" onclick="yes()">Yes</button>
    <button id="no">No</button>
  </div>

  <script>
    const noBtn = document.getElementById("no");
    const yesBtn = document.getElementById("yes");
    const minDistance = 96; // minimum distance in pixels

    // Helper to place No button at least minDistance away from Yes, anywhere in the viewport
    function placeNoButton() {
      const vw = window.innerWidth;
      const vh = window.innerHeight;

      const yesRect = yesBtn.getBoundingClientRect();

      let x, y;
      let attempts = 0;

      do {
        x = Math.random() * (vw - noBtn.offsetWidth);
        y = Math.random() * (vh - noBtn.offsetHeight);

        const noCenterX = x + noBtn.offsetWidth / 2;
        const noCenterY = y + noBtn.offsetHeight / 2;
        const yesCenterX = yesRect.left + yesRect.width / 2;
        const yesCenterY = yesRect.top + yesRect.height / 2;

        const dist = Math.hypot(noCenterX - yesCenterX, noCenterY - yesCenterY);
        if (dist >= minDistance) break;

        attempts++;
      } while (attempts < 100);

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
