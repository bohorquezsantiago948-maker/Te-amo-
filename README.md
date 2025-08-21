<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Palabras de amor cayendo</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background: linear-gradient(#1a0033, #330066);
      height: 100vh;
      color: white;
      font-family: Arial, sans-serif;
    }
    .fall {
      position: absolute;
      top: -50px;
      animation: fall linear forwards;
      white-space: nowrap;
      text-shadow: 0 0 10px rgba(255,255,255,0.3);
    }
    @keyframes fall {
      0% { transform: translateY(-50px); opacity: 1; }
      100% { transform: translateY(110vh); opacity: 0.8; }
    }
    .music-control {
      position: fixed;
      bottom: 10px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(255,255,255,0.2);
      padding: 10px 20px;
      border-radius: 20px;
      font-size: 14px;
      color: white;
      cursor: pointer;
    }
    .music-iframe {
      display: block;
      margin: 20px auto 0 auto;
      border: none;
      border-radius: 15px;
      box-shadow: 0 0 10px #222;
    }
  </style>
</head>
<body>
  <!-- Música de fondo con YouTube -->
  <iframe class="music-iframe" width="320" height="180" src="https://www.youtube.com/embed/D94triePAJE?autoplay=1&loop=1&playlist=D94triePAJE" allow="autoplay; encrypted-media" allowfullscreen></iframe>

  <div class="music-control" onclick="toggleMusic()">🎶 Mostrar/Ocultar Música</div>

  <script>
    const words = [
      "achis", "te amo", "labubu", "uwu", "linda muchachita",
      "Mariana", "ghunther", "chofri", "mi vida", "corazón",
      "eres mi todo", "preciosa", "amor eterno", "te extraño",
      "mi cielo", "mi reina", "eres única"
    ];
    const symbols = ["❤","★","💕","✨","💖"];

    function random(min, max) {
      return Math.random() * (max - min) + min;
    }

    function createFallingItem(text, isWord = true) {
      const el = document.createElement("div");
      el.className = "fall";
      el.textContent = text;

      el.style.left = random(0, window.innerWidth - 50) + "px";
      el.style.fontSize = isWord ? random(18, 40) + "px" : random(14, 28) + "px";
      el.style.color = isWord ? "#ff99cc" : (text.includes("❤") || text.includes("💕") || text.includes("💖") ? "red" : "yellow");

      const duration = random(4, 10);
      el.style.animationDuration = duration + "s";

      document.body.appendChild(el);
      setTimeout(() => el.remove(), duration * 1000);
    }

    setInterval(() => {
      for (let i = 0; i < 3; i++) {
        if (Math.random() < 0.6) {
          createFallingItem(words[Math.floor(Math.random() * words.length)], true);
        } else {
          createFallingItem(symbols[Math.floor(Math.random() * symbols.length)], false);
        }
      }
    }, 400);

    // Mostrar/Ocultar reproductor de música
    const musicIframe = document.querySelector('.music-iframe');
    let musicVisible = true;
    function toggleMusic() {
      musicVisible = !musicVisible;
      musicIframe.style.display = musicVisible ? 'block' : 'none';
    }
  </script>
</body>
</html>
