<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Lumina</title>
  <style>
    body {
      margin: 0;
      background: black;
      overflow: hidden;
      color: white;
      font-family: 'Orbitron', sans-serif;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .stars {
      position: fixed;
      width: 100%;
      height: 100%;
      background: black;
      z-index: 0;
    }
    .star {
      position: absolute;
      background: white;
      border-radius: 50%;
      opacity: 0.8;
      animation: twinkle 2s infinite ease-in-out alternate;
    }
    @keyframes twinkle {
      from { opacity: 0.2; transform: scale(1); }
      to { opacity: 1; transform: scale(1.3); }
    }
    .title {
      z-index: 1;
      font-family: 'Old English Text MT', serif;
      font-size: 3em;
      margin-bottom: 20px;
    }
    .credit {
      z-index: 1;
      font-family: 'Old English Text MT', serif;
      margin-bottom: 30px;
      font-size: 1.2em;
    }
    .countdown {
      z-index: 1;
      font-size: 4em;
      text-align: center;
      letter-spacing: 0.1em;
    }
  </style>
</head>
<body>
  <div class="stars" id="stars"></div>
  <div class="title">Lumina</div>
  <div class="credit">created by lumina</div>
  <div class="countdown" id="timer"></div>

  <script>
    // Star animation generator
    const starContainer = document.getElementById('stars');
    const numStars = 150;

    for (let i = 0; i < numStars; i++) {
      const star = document.createElement('div');
      star.classList.add('star');
      const size = Math.random() * 2 + 1;
      star.style.width = `${size}px`;
      star.style.height = `${size}px`;
      star.style.top = `${Math.random() * 100}%`;
      star.style.left = `${Math.random() * 100}%`;
      star.style.animationDuration = `${1 + Math.random() * 3}s`;
      starContainer.appendChild(star);
    }

    const targetDate = new Date('August 3, 2025 00:00:00').getTime();

    const updateCountdown = () => {
      const now = new Date().getTime();
      const distance = targetDate - now;

      const days = Math.floor(distance / (1000 * 60 * 60 * 24));
      const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((distance % (1000 * 60)) / 1000);

      document.getElementById('timer').innerHTML =
        `${String(days).padStart(2, '0')} : ` +
        `${String(hours).padStart(2, '0')} : ` +
        `${String(minutes).padStart(2, '0')} : ` +
        `${String(seconds).padStart(2, '0')}`;

      if (distance < 0) {
        document.getElementById('timer').innerHTML = '00 : 00 : 00 : 00';
      }
    };

    updateCountdown();
    setInterval(updateCountdown, 1000);
  </script>
</body>
</html>
