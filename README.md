# A-Simple-Chat-Bot
A Simple Chat Bot using  HTML CSS &amp; JS

#HTML CODE

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Smart AI ChatBot</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <div class="chat-container">
    <div class="chat-header">🤖 ChatBot Pro</div>
    <div class="chat-box" id="chat-box"></div>
    <div class="input-area">
      <input type="text" id="user-input" placeholder="Type a message..." autofocus />
      <button onclick="sendMessage()">Send</button>
    </div>
  </div>

  <script src="index.js"></script>
</body>
</html>



#CSS CODE

body {
  margin: 0;
  font-family: "Segoe UI", sans-serif;
  background: linear-gradient(to right, #74ebd5, #ACB6E5);
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.chat-container {
  background: #fff;
  width: 100%;
  max-width: 500px;
  border-radius: 15px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.chat-header {
  background: #4a90e2;
  color: white;
  padding: 15px;
  text-align: center;
  font-weight: bold;
}

.chat-box {
  height: 450px;
  overflow-y: auto;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  background-color: #f5f7fa;
}

.message {
  max-width: 80%;
  padding: 10px 14px;
  border-radius: 18px;
  font-size: 15px;
  position: relative;
  animation: fadeIn 0.3s ease-in-out;
}

.user {
  align-self: flex-end;
  background-color: #daf5dc;
}

.bot {
  align-self: flex-start;
  background-color: #e4e4e4;
}

.typing {
  font-style: italic;
  font-size: 13px;
  opacity: 0.7;
}

.timestamp {
  font-size: 11px;
  color: #888;
  margin-top: 3px;
}

.input-area {
  display: flex;
  border-top: 1px solid #ccc;
  padding: 10px;
  gap: 10px;
  background: #fff;
}

input[type="text"] {
  flex: 1;
  padding: 10px 15px;
  border-radius: 20px;
  border: 1px solid #ccc;
  outline: none;
}

button {
  background-color: #4a90e2;
  color: white;
  padding: 10px 18px;
  border: none;
  border-radius: 20px;
  cursor: pointer;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(5px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 600px) {
  .chat-container {
    margin: 10px;
    height: 95vh;
  }
}






#JS CODE

const input = document.getElementById("user-input");
const chatBox = document.getElementById("chat-box");

input.addEventListener("keydown", (e) => {
  if (e.key === "Enter") sendMessage();
});

function sendMessage() {
  const msg = input.value.trim();
  if (!msg) return;

  appendMessage("user", msg);
  input.value = "";
  showTyping();
  setTimeout(() => generateResponse(msg), 800);
}

function appendMessage(sender, text) {
  const msgDiv = document.createElement("div");
  msgDiv.className = `message ${sender}`;
  msgDiv.innerHTML = `${text}<div class="timestamp">${getTime()}</div>`;
  chatBox.appendChild(msgDiv);
  chatBox.scrollTop = chatBox.scrollHeight;
}

function showTyping() {
  const typing = document.createElement("div");
  typing.id = "typing";
  typing.className = "message bot typing";
  typing.innerHTML = "Typing...";
  chatBox.appendChild(typing);
  chatBox.scrollTop = chatBox.scrollHeight;
}

function removeTyping() {
  const typing = document.getElementById("typing");
  if (typing) chatBox.removeChild(typing);
}

function getTime() {
  const now = new Date();
  return now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
}

function generateResponse(input) {
  removeTyping();
  const msg = input.toLowerCase();
  let reply = "🤔 I didn’t get that. Try something else.";

  if (msg.includes("hello") || msg.includes("hi")) {
    reply = "👋 Hello there! How can I help?";
  } else if (msg.includes("how are you")) {
    reply = "I'm doing great! Thanks for asking 😊";
  } else if (msg.includes("your name")) {
    reply = "I’m SmartBot, your friendly assistant!";
  } else if (msg.includes("time")) {
    reply = `⏰ It's ${getTime()}`;
  } else if (msg.includes("date")) {
    reply = `📅 Today is ${new Date().toDateString()}`;
  } else if (msg.includes("bye")) {
    reply = "Goodbye! 👋 Have a great day!";
  } else if (msg.includes("help")) {
    reply = "🛠️ I can answer greetings, time/date, and small talk!";
  }

  appendMessage("bot", reply);
}
