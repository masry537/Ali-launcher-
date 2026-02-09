# Ali-launcher- 
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>Ali Super Launcher</title>

<!-- ========================= -->
<!--        GLOBAL CSS         -->
<!-- ========================= -->

<style>

/* =========================
   ROOT VARIABLES
========================= */
:root {
  --bg: #0f0f0f;
  --card: #1a1a1a;
  --text: #FFFFFF;
  --accent: #00ffcc;
  --danger: #ff4444;
  --success: #44ff88;
}

/* =========================
   LIGHT MODE
========================= */
.light {
  --bg: #f5f5f5;
  --card: #ffffff;
  --text: #000000;
  --accent: #0066ff;
  --danger: #cc0000;
  --success: #009944;
}

/* =========================
   BODY
========================= */
body {
  margin: 0;
  padding: 0;
  font-family: Arial, Tahoma, sans-serif;
  background: var(--bg);
  color: var(--text);
  transition: 0.4s;
  overflow-x: hidden;
}

/* =========================
   HEADER
========================= */
header {
  background: linear-gradient(45deg, var(--accent), purple);
  padding: 15px;
  font-size: 22px;
  font-weight: bold;
  position: relative;
}

/* =========================
   MENU BUTTON
========================= */
.menu-btn {
  position: absolute;
  right: 15px;
  top: 10px;
  font-size: 26px;
  cursor: pointer;
}

/* =========================
   SIDE MENU
========================= */
.side-menu {
  position: fixed;
  top: 0;
  right: -300px;
  width: 300px;
  height: 100%;
  background: #ffffff;
  color: #000;
  box-shadow: -5px 0 30px #00000088;
  transition: 0.4s;
  z-index: 999;
  padding-top: 60px;
  overflow-y: auto;
}

.side-menu.show {
  right: 0;
}

/* =========================
   SIDE MENU ITEMS
========================= */
.side-menu .item {
  padding: 15px 20px;
  border-bottom: 1px solid #ddd;
  cursor: pointer;
  font-size: 17px;
  transition: 0.25s;
}

.side-menu .item:hover {
  background: #eee;
}

/* =========================
   SECTIONS
========================= */
.section {
  padding: 20px;
  border-bottom: 1px solid #ffffff22;
}

/* =========================
   SITES GRID
========================= */
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 15px;
  padding: 15px;
}

/* =========================
   SITE CARD
========================= */
.site {
  background: var(--card);
  padding: 20px;
  border-radius: 16px;
  text-align: center;
  cursor: pointer;
  transition: 0.3s;
  box-shadow: 0 0 10px #00000066;
}

.site:hover {
  transform: translateY(-6px) scale(1.05);
  box-shadow: 0 0 20px var(--accent);
}

.site span {
  display: block;
  margin-top: 10px;
  font-size: 18px;
}

/* =========================
   NOTES
========================= */
textarea {
  width: 100%;
  min-height: 120px;
  border-radius: 10px;
  border: none;
  padding: 10px;
  font-size: 16px;
}

/* =========================
   BUTTONS
========================= */
.btn {
  padding: 10px 15px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-weight: bold;
  margin-top: 10px;
}

.btn-accent { background: var(--accent); }
.btn-danger { background: var(--danger); color:#fff; }
.btn-success { background: var(--success); }

.footer {
  padding: 15px;
  text-align: center;
  opacity: 0.6;
  font-size: 14px;
}

/* =========================
   FAKE CONSOLE
========================= */
.console {
  background: #000;
  color: #0f0;
  padding: 10px;
  border-radius: 10px;
  font-family: monospace;
  height: 150px;
  overflow-y: auto;
  font-size: 13px;
}

</style>
</head>

<body>

<!-- =========================
   HEADER
========================= -->
<header>
  🚀 Ali Super Launcher
  <div class="menu-btn" onclick="toggleMenu()">☰</div>
</header>

<!-- =========================
   SIDE MENU
========================= -->
<div class="side-menu" id="sideMenu">

  <div class="item" onclick="refreshPage()">🔄 Refresh</div>
  <div class="item" onclick="toggleMode()">🌙 / ☀️ Dark - Light</div>
  <div class="item" onclick="addSite()">➕ Add Site</div>
  <div class="item" onclick="clearSites()">🧹 Clear Sites</div>
  <div class="item" onclick="openConsole()">🖥️ Open Console</div>
  <div class="item" onclick="showAbout()">ℹ️ About</div>
  <div class="item" onclick="toggleMenu()">❌ Exit</div>

</div>

<!-- =========================
   SITES
========================= -->
<div class="container" id="sites">

  <div class="site" onclick="openSite('https://google.com')">🌍<span>Google</span></div>
  <div class="site" onclick="openSite('https://youtube.com')">▶️<span>YouTube</span></div>
  <div class="site" onclick="openSite('https://github.com')">💻<span>GitHub</span></div>
  <div class="site" onclick="openSite('https://chat.openai.com')">🤖<span>ChatGPT</span></div>

</div>

<!-- =========================
   NOTES SECTION
========================= -->
<div class="section">
  <h2>📝 Notes</h2>
  <textarea id="notes" placeholder="اكتب ملاحظاتك هنا..."></textarea>
  <button class="btn btn-success" onclick="saveNotes()">💾 Save Notes</button>
</div>

<!-- =========================
   FAKE CONSOLE
========================= -->
<div class="section" id="consoleSection" style="display:none;">
  <h2>🖥️ Fake Console</h2>
  <div class="console" id="consoleBox">
    > System Booting...<br>
    > Loading Modules...<br>
    > Ready ✔️<br>
  </div>
</div>

<!-- =========================
   ABOUT
========================= -->
<div class="section" id="aboutSection" style="display:none;">
  <h2>ℹ️ About</h2>
  <p>
    This launcher was created by Ali 😎<br>
    Version: 1.0.0<br>
    Purpose: Learn HTML, CSS, JS and have fun!<br>
  </p>
</div>

<div class="footer">
  © 2026 Ali Launcher - Just For Fun 😈
</div>

<!-- =========================
   JAVASCRIPT
========================= -->
<script>

// =========================
// MENU
// =========================
function toggleMenu(){
  document.getElementById("sideMenu").classList.toggle("show");
}

// =========================
// REFRESH
// =========================
function refreshPage(){
  logConsole("Refreshing page...");
  location.reload();
}

// =========================
// DARK / LIGHT
// =========================
function toggleMode(){
  document.body.classList.toggle("light");
  logConsole("Theme toggled.");
}

// =========================
// OPEN SITE
// =========================
function openSite(url){
  logConsole("Opening: " + url);
  window.open(url,"_blank");
}

// =========================
// ADD SITE
// =========================
function addSite(){
  let name = prompt("اسم الموقع:");
  let link = prompt("رابط الموقع:");
  let icon = prompt("إيموجي:", "🔗");

  if(!name || !link) return;

  let div = document.createElement("div");
  div.className = "site";
  div.innerHTML = `${icon}<span>${name}</span>`;
  div.onclick = function(){
    openSite(link);
  };

  document.getElementById("sites").appendChild(div);
  logConsole("Site added: " + name);
}

// =========================
// CLEAR SITES
// =========================
function clearSites(){
  if(confirm("مسح كل المواقع؟")){
    document.getElementById("sites").innerHTML = "";
    logConsole("All sites cleared.");
  }
}

// =========================
// NOTES
// =========================
function saveNotes(){
  let text = document.getElementById("notes").value;
  localStorage.setItem("ali_notes", text);
  logConsole("Notes saved.");
  alert("تم حفظ الملاحظات ✅");
}

// Load notes
document.getElementById("notes").value = localStorage.getItem("ali_notes") || "";

// =========================
// CONSOLE
// =========================
function openConsole(){
  document.getElementById("consoleSection").style.display = "block";
  logConsole("Console opened.");
}

function logConsole(msg){
  let box = document.getElementById("consoleBox");
  box.innerHTML += "> " + msg + "<br>";
  box.scrollTop = box.scrollHeight;
}

// =========================
// ABOUT
// =========================
function showAbout(){
  document.getElementById("aboutSection").style.display = "block";
  logConsole("About section opened.");
}

// =========================
// AUTO LOGS (FAKE SYSTEM)
// =========================
setInterval(()=>{
  logConsole("System check OK...");
},15000);

</script>

</body>
</html>
