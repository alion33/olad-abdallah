<!DOCTYPE html><html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>منصة إمارة أولاد عبد الله الرقمية</title>
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --gold: #ffd700;
      --dark-bg: #1b1b1b;
      --light-glass: rgba(255, 255, 255, 0.07);
      --border-glass: rgba(255, 255, 255, 0.15);
    }* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Cairo', sans-serif;
  background: radial-gradient(circle at top, #222, #111);
  color: #fff;
  overflow-x: hidden;
}

canvas#نجوم {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: -2;
}

.header {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  padding: 30px 10px 10px;
  text-align: center;
}

.header img {
  width: 60px;
  height: 60px;
}

.header h1 {
  font-size: 1.6rem;
  background: linear-gradient(to right, var(--gold), #fff8dc);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.content {
  position: relative;
  z-index: 1;
  background: var(--light-glass);
  border: 1px solid var(--border-glass);
  backdrop-filter: blur(12px);
  padding: 40px;
  border-radius: 20px;
  max-width: 600px;
  margin: 2% auto;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  animation: fadeIn 2s ease-in-out;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-20px); }
  to { opacity: 1; transform: translateY(0); }
}

.content h2 {
  font-size: 2rem;
  background: linear-gradient(to right, var(--gold), #fff8dc);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 2px 2px 6px rgba(0,0,0,0.6);
}

.btn {
  margin-top: 1rem;
  padding: 10px 20px;
  font-size: 1rem;
  background: var(--gold);
  color: #111;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.btn:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 16px rgba(255, 215, 0, 0.3);
}

#authBox, #commentsBox {
  margin-top: 2rem;
  background-color: rgba(255,255,255,0.05);
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.3);
}

.counter {
  margin-top: 20px;
  font-size: 1rem;
  color: #aaa;
}

.comment {
  text-align: right;
  background-color: rgba(255,255,255,0.08);
  margin-top: 10px;
  padding: 10px;
  border-radius: 8px;
}

.comment strong {
  color: var(--gold);
}

@media (max-width: 600px) {
  .header {
    flex-direction: column;
  }
  .header h1 {
    font-size: 1.3rem;
  }
  .content {
    padding: 25px;
    margin: 10% auto;
  }
}

  </style>
</head>
<body>
  <canvas id="نجوم"></canvas>  <div class="header">
    <img src="https://cdn-icons-png.flaticon.com/512/3208/3208722.png" alt="شعار الإمارة">
    <h1>منصة إمارة أولاد عبد الله الرقمية</h1>
  </div>  <div class="content">
    <h2>🏰 أهلاً بك في قلعة المجد... حيث لا يُفتح الباب إلا لأبناء القبيلة.</h2>
    <div id="authBox">
      <p>📢 هل أنت من أبناء قبيلة أولاد عبد الله؟</p>
      <button class="btn" onclick="confirmTribe(true)">نعم</button>
      <button class="btn" onclick="confirmTribe(false)">لا</button>
      <div id="nameInput" style="margin-top: 1rem; display: none;">
        <p>أدخل اسمك لتفعيل العضوية:</p>
        <input type="text" id="username" placeholder="اسمك" style="padding: 8px; border-radius: 6px; border: none; width: 80%; max-width: 250px;">
        <br><br>
        <button class="btn" onclick="activateMember()">تفعيل العضوية</button>
      </div>
      <div id="message" style="margin-top: 1rem; color: #f88; font-weight: bold;"></div>
    </div><div id="commentsBox" style="display: none;">
  <h3>📝 التعليقات</h3>
  <div id="comments"></div>
  <textarea id="commentInput" rows="3" placeholder="اكتب تعليقك هنا..." style="width: 100%; padding: 10px; border-radius: 8px; margin-top: 10px;"></textarea>
  <button class="btn" onclick="addComment()">نشر التعليق</button>
</div>

<div class="counter">عدد الزوار: <span id="visit-count">...</span></div>

  </div>  <script>
    const canvas = document.getElementById('نجوم');
    const ctx = canvas.getContext('2d');
    let stars = [];

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    for (let i = 0; i < 120; i++) {
      stars.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 1.8 + 0.5,
        d: Math.random() * 0.5 + 0.2
      });
    }

    function drawStars() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.fillStyle = "white";
      for (let star of stars) {
        ctx.beginPath();
        ctx.arc(star.x, star.y, star.r, 0, 2 * Math.PI);
        ctx.fill();
      }
    }

    function animateStars() {
      for (let star of stars) {
        star.y += star.d;
        if (star.y > canvas.height) {
          star.y = 0;
          star.x = Math.random() * canvas.width;
        }
      }
      drawStars();
      requestAnimationFrame(animateStars);
    }

    animateStars();

    // auth and comments logic
    const countKey = 'visitCount';
    let visits = localStorage.getItem(countKey);
    if (!visits) visits = 0;
    visits++;
    localStorage.setItem(countKey, visits);
    document.getElementById('visit-count').textContent = visits;

    function confirmTribe(answer) {
      const nameInput = document.getElementById('nameInput');
      const message = document.getElementById('message');
      if (answer) {
        nameInput.style.display = 'block';
        message.textContent = '';
      } else {
        nameInput.style.display = 'none';
        message.textContent = '❌ عذرًا، هذه الصفحة مخصصة حصريًا لأبناء قبيلة أولاد عبد الله.';
      }
    }

    function activateMember() {
      const username = document.getElementById('username').value.trim();
      if (username.length < 2) {
        document.getElementById('message').textContent = '❗ الرجاء إدخال اسم صالح.';
        return;
      }
      localStorage.setItem('tribeMember', username);
      document.getElementById('authBox').innerHTML = `✅ مرحبًا بك يا ${username}! تم تفعيل عضويتك.`;
      showComments(username);
    }

    function showComments(user) {
      const box = document.getElementById('commentsBox');
      box.style.display = 'block';
      loadComments();
    }

    function loadComments() {
      const comments = JSON.parse(localStorage.getItem('commentsList') || '[]');
      const container = document.getElementById('comments');
      container.innerHTML = '';
      comments.forEach(c => {
        container.innerHTML += `<div class="comment"><strong>${c.user}:</strong> ${c.text}</div>`;
      });
    }

    function addComment() {
      const input = document.getElementById('commentInput');
      const text = input.value.trim();
      const user = localStorage.getItem('tribeMember');
      if (text.length === 0 || !user) return;
      const comments = JSON.parse(localStorage.getItem('commentsList') || '[]');
      comments.push({ user, text });
      localStorage.setItem('commentsList', JSON.stringify(comments));
      input.value = '';
      loadComments();
    }

    // إذا كان العضو مفعّل سابقًا
    const currentUser = localStorage.getItem('tribeMember');
    if (currentUser) {
      document.getElementById('authBox').innerHTML = `✅ مرحبًا بك يا ${currentUser}! تم تفعيل عضويتك.`;
      showComments(currentUser);
    }
  </script></body>
</html>
