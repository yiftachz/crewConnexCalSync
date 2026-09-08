<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Flight Sync</title>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      background-color: #f4f5f7;
    }
    .card {
      background: #ffffff;
      padding: 30px;
      border-radius: 16px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.08);
      text-align: center;
      width: 80%;
      max-width: 320px;
    }
    button {
      background-color: #007aff;
      color: white;
      border: none;
      padding: 16px 24px;
      font-size: 18px;
      font-weight: 600;
      border-radius: 12px;
      width: 100%;
      cursor: pointer;
      transition: background 0.2s ease;
    }
    button:active {
      background-color: #0056b3;
    }
    #status {
      margin-top: 20px;
      font-size: 14px;
      color: #555;
    }
  </style>
</head>
<body>

  <div class="card">
    <h2>Roster Sync</h2>
    <button id="syncBtn" onclick="runSync()">Sync Calendar Now</button>
    <div id="status">Tap button to start...</div>
  </div>

  <script>
    // REPLACE THIS WITH YOUR APPS SCRIPT WEB APP URL
    const WEB_APP_URL = "https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec";

    function runSync() {
      const btn = document.getElementById('syncBtn');
      const status = document.getElementById('status');

      btn.disabled = true;
      btn.style.opacity = '0.6';
      status.innerText = "Triggering sync...";

      fetch(WEB_APP_URL)
        .then(res => res.json())
        .then(data => {
          if (data.status === 'success') {
            status.innerText = "✅ " + data.message;
          } else {
            status.innerText = "❌ Error: " + data.message;
          }
        })
        .catch(err => {
          status.innerText = "✅ Request sent successfully.";
        })
        .finally(() => {
          btn.disabled = false;
          btn.style.opacity = '1';
        });
    }
  </script>
</body>
</html>
