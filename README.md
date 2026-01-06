<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Admin View - Secret Messages</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #a18cd1, #fbc2eb);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .container {
      background: white;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
      width: 90%;
      max-width: 500px;
      text-align: center;
    }

    h1 {
      color: #673ab7;
    }

    input[type="password"] {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
    }

    button {
      margin-top: 15px;
      padding: 10px 20px;
      background-color: #673ab7;
      color: white;
      border: none;
      border-radius: 25px;
      cursor: pointer;
    }

    ul {
      margin-top: 20px;
      text-align: left;
      max-height: 250px;
      overflow-y: auto;
      padding-left: 0;
      display: none;
    }

    li {
      background: #f1f1f1;
      margin-bottom: 10px;
      padding: 10px;
      border-left: 4px solid #673ab7;
      border-radius: 6px;
      list-style: none;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Viewer🔐</h1>
    <input type="password" id="password" placeholder="Enter password">
    <button onclick="showMessages()">see Messages</button>

    <ul id="messageList"></ul>
  </div>

  <script>
    const adminPassword = "309"; // Ganti password kamu di sini

    function showMessages() {
      const inputPass = document.getElementById("password").value;
      const list = document.getElementById("messageList");

      if (inputPass !== adminPassword) {
        alert("❌ Wrong password!");
        return;
      }

      const messages = JSON.parse(localStorage.getItem("secretMessages")) || [];

      list.innerHTML = "";

      if (messages.length === 0) {
        list.innerHTML = "<li>No messages found.</li>";
      } else {
        messages.forEach((msg, i) => {
          const item = document.createElement("li");
          item.textContent = `${i + 1}. ${msg.content} (${msg.time})`;
          list.appendChild(item);
        });
      }

      list.style.display = "block";
    }
  </script>
</body>
</html>
