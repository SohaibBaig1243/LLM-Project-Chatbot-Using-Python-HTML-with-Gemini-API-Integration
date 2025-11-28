LLM Project: Chatbot Using Python & HTML with Gemini API Integration

1. Introduction
Aaj ke time mein Large Language Models (LLMs) jaise ke Google Gemini, GPT, Claude bohot powerful AI tools hain jo natural language ko samajh kar human-like answers deti hain.
Is project ka purpose hai Python backend + HTML frontend use kar ke ek powerful AI Chatbot banana jo Gemini API se connect ho kar user ke questions ka jawab de.

2. Project Objectives
Simple aur clean frontend (HTML, CSS, JS)
Secure and fast backend (Python Flask)
Gemini API se real-time AI responses
Chat history display
Easy frontend-to-backend communication using AJAX / Fetch API
Fully working LLM-based chatbot project

3. Technology Stack
Frontend
HTML5
CSS3
JavaScript (Fetch API for requests)
Backend
Python 3
Flask Framework
Gemini API Integration (via REST API)

4. System Architecture
User → HTML Chat Interface → Flask Backend → Gemini API → Response → Frontend

5. Project Folder Structure
/llm_chatbot
     ├── app.py
     ├── templates/
     │       └── index.html
     ├── static/
             └── style.css

6. Backend (Python + Gemini API)
app.py (Flask Backend + Gemini Integration)
from flask import Flask, render_template, request, jsonify
import requests
import os

app = Flask(__name__)

GEMINI_API_KEY = "YOUR_GEMINI_API_KEY"
GEMINI_URL = "https://generativelanguage.googleapis.com/v1/models/gemini-pro:generateText?key=" + GEMINI_API_KEY

@app.route("/")
def home():
    return render_template("index.html")

@app.route("/ask", methods=["POST"])
def ask_gemini():
    user_msg = request.json.get("message")

    payload = {
        "prompt": user_msg
    }

    response = requests.post(GEMINI_URL, json=payload)
    data = response.json()

    reply = data.get("candidates", [{}])[0].get("output", "No response")

    return jsonify({"reply": reply})

if __name__ == "__main__":
    app.run(debug=True)

7. Frontend (HTML + CSS + JS)
index.html
<!DOCTYPE html>
<html>
<head>
    <title>AI Chatbot (Gemini LLM)</title>
    <style>
        body { font-family: Arial; background: #f4f4f4; padding: 20px; }
        .chat-box { width: 50%; margin: auto; background: #fff; padding: 20px; border-radius: 10px; }
        .message { margin: 10px 0; padding: 10px; border-radius: 5px; }
        .user { background: #d1ecf1; }
        .bot { background: #d4edda; }
    </style>
</head>
<body>

<div class="chat-box">
    <h2>Gemini AI Chatbot</h2>

    <div id="chat"></div>

    <input type="text" id="user_input" placeholder="Type your message..." style="width:80%">
    <button onclick="sendMessage()">Send</button>

</div>

<script>
function sendMessage() {
    let message = document.getElementById("user_input").value;
    if (!message) return;

    let chat = document.getElementById("chat");
    chat.innerHTML += `<div class="message user"><b>You:</b> ${message}</div>`;

    fetch("/ask", {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: JSON.stringify({"message": message})
    })
    .then(res => res.json())
    .then(data => {
        chat.innerHTML += `<div class="message bot"><b>Bot:</b> ${data.reply}</div>`;
    });

    document.getElementById("user_input").value = "";
}
</script>

</body>
</html>

8. How It Works
User message → HTML input
JavaScript message ko Flask backend ko send karta hai /ask API route per
Flask Gemini API ko prompt send karta hai
Gemini AI response return karta hai
Python response frontend ko return karta hai
Frontend HTML response chat box mein show karta hai

9. Key Features
Real-time AI responses
Clean UI
Easy to modify
Fully expandable codebase
Can be upgraded to speech, authentication, memory, database, etc.

10. Future Enhancements
Chat memory / conversation storage
User login system
Voice-to-text features
Text-to-speech
Advanced UI (Bootstrap / Tailwind)
Gemini Pro Vision (image input)

11. Conclusion
Yeh project beginners aur professionals dono ke liye perfect hai.
Simple structure + powerful Gemini LLM integration = fully functional AI chatbot.
