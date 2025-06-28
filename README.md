<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>إمارة أولاد عبد الله</title>
  <style>
    /* الأساسيات */
    body {
      margin: 0;
      padding: 0;
      font-family: 'Cairo', sans-serif;
      background: linear-gradient(to bottom, #1b1b1b, #2a2a2a);
      overflow: hidden;
    }

    /* القماش النجمي */
    canvas#نجوم {
      position: fixed;
      top: 0;
      left: 0;
      z-index: -2;
    }

    /* صندوق المحتوى */
    .content {
      position: relative;
      z-index: 1;
      background: rgba(255, 255, 255, 0.07);
      border: 1px solid rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(10px);
      padding: 40px;
      border-radius: 20px;
      max-width: 520px;
      margin: 10% auto;
      text-align: center;
      color: #fdfdfd;
      box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
    }

    h1 {
      font-size: 2.8rem;
      background: linear-gradient(to right, #ffd700, #fff8dc);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
      margin-bottom: 1rem;
    }

    p {
      font-size: 1.4rem;
      line-height: 1.8;
      color: #f0f0f0;
    }

    /* تجاوب للجوال */
    @media (max-width: 600px) {
      .content {
        padding: 25px;
        margin: 20% auto;
      }

      h1 {
        font-size: 2rem;
      }

      p {
        font-size: 1.1rem;
      }
    }
  </style>
</head>
<body>
  <canvas id="نجوم"></canvas>
  <div class="content">
    <h1>إمارة أولاد عبد الله</h1>
    <p>ذاكرة الرمال، وسيف الفخر، وحكاية لا تنطفئ من نور المجد.</p>
  </div>

  <script>
    const canvas = document.getElementById('نجوم');
    const ctx = canvas.getContext('2d');
    let stars = [];

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    for (let i = 0; i < 100; i++) {
