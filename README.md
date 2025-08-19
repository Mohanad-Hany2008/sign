# sign[html.html](https://github.com/user-attachments/files/21867769/html.html)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Voice to Sign Language</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    button { padding: 10px 20px; margin: 10px 0; }
    #transcript { margin-top: 20px; font-size: 18px; font-weight: bold; }
    #signs { margin-top: 20px; }
    .sign-img { width: 100px; margin: 5px; display: inline-block; }
    #status { margin-top: 10px; color: darkred; font-style: italic; }
  </style>
</head>
<body>

  <h2>🎤 Voice to Sign Language Translator</h2>
  <button id="startBtn">Start Listening</button>
  <button id="stopBtn">Stop Listening</button>

  <p id="status">Status: Not started</p>
  <p id="transcript">Transcript: ...</p>
  <div id="signs"></div>
<button id="startBtn">Start Listening</button>
<p id="status"></p>
<p id="transcript"></p>

<script>
  const statusEl = document.getElementById("status");
  const transcriptEl = document.getElementById("transcript");

  const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
  const recognition = new SpeechRecognition();

  recognition.continuous = true;
  recognition.interimResults = true;
  recognition.lang = "en-US"; // try "ar-EG" if you speak Arabic

  recognition.onstart = () => {
    statusEl.textContent = "✅ Listening... speak now!";
    console.log("Recognition started");
  };

  recognition.onresult = (event) => {
    let text = "";
    for (let i = event.resultIndex; i < event.results.length; i++) {
      text += event.results[i][0].transcript + " ";
    }
    transcriptEl.textContent = "Transcript: " + text;
    console.log("Result:", text);
  };

  recognition.onerror = (event) => {
    console.error("Error:", event.error);
    statusEl.textContent = "❌ Error: " + event.error;
  };

  recognition.onspeechstart = () => console.log("🎤 Speech detected");
  recognition.onsoundstart = () => console.log("🔊 Sound detected");
  recognition.onsoundend = () => console.log("🔇 Sound ended");

  document.getElementById("startBtn").addEventListener("click", () => {
    recognition.start();
  });
</script>


</body>
</html>
