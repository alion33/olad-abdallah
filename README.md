<!DOCTYPE html><html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>منصة إمارة أولاد عبد الله</title>
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --gold: #ffd700;
      --dark: #121212;
    }* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Cairo', sans-serif;
}

body {
  background: url('background.jpg') no-repeat center center fixed;
  background-size: cover;
  color: #fff;
  overflow-x: hidden;
}

.container {
  max-width: 700px;
  margin: 5% auto;
  padding: 30px;
  background: rgba(0, 0, 0, 0.6);
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.6);
  text-align: center;
}

h1 {
  font-size: 2.5rem;
  background: linear-gradient(to right, var(--gold), #fff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 20px;
}

p.description {
  font-size: 1.2rem;
  margin-bottom: 30px;
  color: #eee;
}

button {
  background: var(--gold);
  color: #000;
  padding: 10px 25px;
  border: none;
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s;
}

button:hover {
  background: #e6c200;
}

#authBox, #commentsBox {
  margin-top: 25px;
}

#nameInput {
  margin-top: 15px;
}

input {
  padding: 10px;
  border-radius: 6px;
  border: none;
  margin-top: 10px;
  width: 80%;
}

.comment {
  background: rgba(255, 255, 255, 0.1);
  padding: 10px;
  border-radius: 10px;
  text-align: right;
  margin-top: 10px;
}

.comment strong {
  color: var(--gold);
}

.counter {
  margin-top: 20px;
  font-size: 0.9rem;
  color: #ddd;
}

  </style>
</head>
<body>
  <div class="container">
    <h1>منصة إمارة أولاد عبد الله</h1>
    <p class="description">مرحبًا بك في قلعة المجد، حيث لا يُفتح الباب إلا لأبناء القبيلة.</p><div id="authBox">
  <p>📌 هل أنت من أبناء قبيلة أولاد عبد الله؟</p>
  <button onclick="confirmTribe(true)">نعم</button>
  <button onclick="confirmTribe(false)">لا</button>

  <div id="nameInput" style="display: none;">
    <p>أدخل اسمك لتفعيل العضوية:</p>
    <input type="text" id="username" placeholder="اسمك القبلي">
    <br><br>
    <button onclick="activateMember()">تفعيل</button>
  </div>

  <div id="message" style="margin-top: 15px; font-weight: bold;"></div>
</div>

<div id="commentsBox" style="display: none;">
  <h3>📝 التعليقات</h3>
  <div id="comments"></div>
  <textarea id="commentInput" rows="3" placeholder="اكتب تعليقك..." style="width: 100%; margin-top: 10px; padding: 10px; border-radius: 8px;"></textarea>
  <br>
  <button onclick="addComment()">نشر التعليق</button>
</div>

<div class="counter">👁️ عدد الزوار: <span id="visit-count"></span></div>

  </div>  <script>
    let visits = localStorage.getItem('visitCount');
    if (!visits) visits = 0;
    visits++;
    localStorage.setItem('visitCount', visits);
    document.getElementById('visit-count').textContent = visits;

    function confirmTribe(answer) {
      if (answer) {
        document.getElementById('nameInput').style.display = 'block';
        document.getElementById('message').textContent = '';
      } else {
        document.getElementById('nameInput').style.display = 'none';
        document.getElementById('message').textContent = '❌ نعتذر، هذه الصفحة مخصصة فقط لأبناء قبيلة أولاد عبد الله.';
      }
    }

    function activateMember() {
      const name = document.getElementById('username').value.trim();
      if (name.length < 2) {
        document.getElementById('message').textContent = '⚠️ الرجاء إدخال اسم صالح';
        return;
      }
      localStorage.setItem('tribeMember', name);
      document.getElementById('authBox').innerHTML = `✅ أهلًا بك يا <strong>${name}</strong>! تم تفعيل عضويتك.`;
      showComments();
    }

    function showComments() {
      document.getElementById('commentsBox').style.display = 'block';
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
      const text = document.getElementById('commentInput').value.trim();
      const user = localStorage.getItem('tribeMember');
      if (!text || !user) return;
      const comments = JSON.parse(localStorage.getItem('commentsList') || '[]');
      comments.push({ user, text });
      localStorage.setItem('commentsList', JSON.stringify(comments));
      document.getElementById('commentInput').value = '';
      loadComments();
    }

    const member = localStorage.getItem('tribeMember');
    if (member) {
      document.getElementById('authBox').innerHTML = `✅ أهلًا بك يا <strong>${member}</strong>! تم تفعيل عضويتك.`;
      showComments();
    }
  </script></body>
</html>
