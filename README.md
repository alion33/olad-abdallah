<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>إمارة أولاد عبد الله</title>
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <canvas id="stars"></canvas> <!-- النجوم المتحركة -->
  <div class="container">
    <h1>إمارة أولاد عبد الله</h1>
    <p>ذاكرة الرمال، وسيف الفخر، وحكاية لا تنطفئ من ضوء المجد.</p>
  </div>

  <!-- سكريبت النجوم -->
  <script>
    const canvas = document.getElementById('stars');
    const ctx = canvas.getContext('2d');
    let stars = [];

    function resize() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    window.addEventListener('resize', resize);
    resize();

    for (let i = 0; i < 100; i++) {
      stars.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 1.5,
        o: Math.random(),
        speed: Math.random() * 0.2
      });
    }

    function drawStars() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      stars.forEach(s => {
        ctx.beginPath();
        ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(255,255,200,${s.o})`;
        ctx.fill();
        s.y += s.speed;
        if (s.y > canvas.height) s.y = 0;
      });
      requestAnimationFrame(drawStars);
    }

    drawStars();
  </script>
</body>
</html>
