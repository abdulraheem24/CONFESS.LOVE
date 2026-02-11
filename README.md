# CONFESS.LOVE
Unsaid is an anonymous confession platform that allows users to express hidden emotions safely and privately
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Unsaid — Anonymous Platform</title>

<style>
:root{
  --pink:#ff4fa3;
  --pink-soft:#ff7bbf;
  --bg:#000;
  --card-bg: #111111;
  --text-gray: #aaa;
}

*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family:-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}

body{
  background:#000;
  color:white;
  scroll-behavior: smooth;
  overflow-x: hidden;
}

/* ================= INTRO SCREEN ================= */
.intro{
  position:fixed;
  inset:0;
  background:black;
  display:flex;
  justify-content:center;
  align-items:center;
  z-index:9999;
  animation:fadeOut 1s ease 3.5s forwards;
}

.intro-content{ text-align:center; }
.intro-logo{ font-size:55px; font-weight:500; letter-spacing:8px; opacity:0; animation:logoReveal 1.8s ease forwards; }
.intro-logo span{ color:var(--pink); }
.intro-line{ margin:25px auto 0; width:0; height:2px; background:var(--pink); box-shadow:0 0 20px var(--pink); animation:lineExpand 1.5s ease forwards 1.2s; }

@keyframes logoReveal{ from{ opacity:0; transform:translateY(20px); letter-spacing:15px; } to{ opacity:1; transform:translateY(0); letter-spacing:8px; } }
@keyframes lineExpand{ from{width:0} to{width:140px} }
@keyframes fadeOut{ to{ opacity:0; visibility:hidden; } }

/* ================= LANDING GATE ================= */
.landing-gate {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  text-align: center;
  opacity: 0;
  animation: showMain 1.2s ease forwards 4s;
  position: absolute;
  width: 100%;
  z-index: 500;
}

.tagline{ color:#aaa; margin-top:15px; font-size:18px; }
.enter-button{
  margin-top:30px; padding:14px 40px; border-radius:30px; border:1px solid var(--pink);
  background:transparent; color:var(--pink); font-size:15px; cursor:pointer; transition:.3s;
}
.enter-button:hover{ background:var(--pink); color:black; box-shadow:0 0 20px var(--pink); }
@keyframes showMain{ to{opacity:1} }

/* ================= MAIN APP (HIDDEN) ================= */
#mainApp { display: none; opacity: 0; transition: opacity 1s ease; }

.navbar{
  position:fixed; top:0; width:100%; padding:18px 40px; display:flex; justify-content:space-between;
  align-items:center; backdrop-filter:blur(20px); background:linear-gradient(135deg, rgba(0,0,0,0.7), rgba(20,0,15,0.7));
  border-bottom:1px solid rgba(255,255,255,0.05); transition:all .4s ease; z-index:1000;
}
.navbar::after{ content:""; position:absolute; inset:0; border-bottom:2px solid var(--pink); box-shadow:0 0 15px var(--pink); opacity:.6; pointer-events:none; animation:navbarGlow 2s infinite alternate; }
@keyframes navbarGlow{ from{opacity:.4;} to{opacity:.9;} }
.navbar.shrink{ padding:10px 40px; background:rgba(0,0,0,0.9); }

.logo{ font-size:20px; font-weight:500; letter-spacing:1px; cursor:pointer; }
.logo span{ color:var(--pink); }

.nav-links{ display:flex; gap:35px; list-style:none; }
.nav-links a{ text-decoration:none; color:#aaa; font-size:14px; transition:.3s; position:relative; cursor: pointer; }
.nav-links a:hover{ color:white; }
.nav-links a::after{ content:""; position:absolute; bottom:-8px; left:50%; transform:translateX(-50%); width:4px; height:4px; background:var(--pink); border-radius:50%; opacity:0; transition:.3s; }
.nav-links a:hover::after{ opacity:1; }

.profile{ position:relative; }
.profile-btn{ border:1px solid rgba(255,255,255,0.1); background:rgba(255,255,255,0.05); color:white; padding:6px 16px; border-radius:20px; cursor:pointer; transition:.3s; }
.profile-btn:hover{ border-color:var(--pink); }

.dropdown{ position:absolute; top:45px; right:0; width:200px; background:rgba(15,15,15,0.95); border:1px solid rgba(255,255,255,0.08); border-radius:12px; display:none; flex-direction:column; backdrop-filter:blur(20px); }
.dropdown a{ padding:12px 15px; text-decoration:none; color:#ccc; font-size:14px; transition:.3s; }
.dropdown a:hover{ background:rgba(255,79,163,0.1); color:white; }

.app-hero{ margin-top:150px; padding: 0 80px; max-width: 900px; }
.app-hero h1{ font-size:48px; font-weight:500; letter-spacing: -1.5px; }

.container { display: grid; grid-template-columns: 1.2fr 0.8fr; gap: 40px; padding: 60px 80px; }

.card { background: var(--card-bg); border-left: 4px solid var(--pink); border-radius: 12px; padding: 30px; }

textarea { width: 100%; height: 140px; background: #000; border: 1px solid #333; border-radius: 8px; color: white; padding: 15px; box-sizing: border-box; resize: none; margin-bottom: 20px; font-size: 16px; outline: none; }

.submit-btn { width: 100%; background: var(--pink); color: white; border: none; padding: 15px; border-radius: 25px; font-weight: bold; cursor: pointer; transition: 0.3s; }

.confession-item { background: var(--card-bg); border-left: 3px solid var(--pink); padding: 20px; border-radius: 8px; margin-bottom: 15px; font-size: 15px; }

.modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); display: none; justify-content: center; align-items: center; z-index: 2000; }
.modal-box { background: #111; width: 400px; padding: 35px; border-radius: 20px; border: 1px solid #222; }

@keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

@media(max-width:900px){ .nav-links{ display:none; } .container { grid-template-columns: 1fr; padding: 20px; } .app-hero { padding: 40px 20px; margin-top: 100px; } }
</style>
</head>

<body>

<div class="intro">
  <div class="intro-content">
    <h1 class="intro-logo">Unsaid<span>.</span></h1>
    <div class="intro-line"></div>
  </div>
</div>

<div class="landing-gate" id="landingGate">
  <h1>Unsaid. Unseen. Unforgettable.</h1>
  <p class="tagline">Some feelings are too pure to be spoken.</p>
  <button class="enter-button" onclick="enterPlatform()">Enter</button>
</div>

<div id="mainApp">
    <nav class="navbar" id="navbar">
      <div class="logo">Unsaid<span>.</span></div>
      <ul class="nav-links">
        <li><a href="#">Home</a></li>
        <li><a href="#write">Write</a></li>
        <li><a onclick="showInfo('poems')">Poems</a></li>
        <li><a onclick="showInfo('rules')">Rules</a></li>
        <li><a onclick="showInfo('privacy')">Privacy</a></li>
        <li><a onclick="showInfo('agreement')">Agreement</a></li>
      </ul>
      <div class="profile">
        <button class="profile-btn" onclick="toggleProfile()" id="authBtn">Login</button>
        <div class="dropdown" id="dropdown">
          <a href="#">My Confessions</a>
          <a href="#" onclick="logout()">Logout</a>
        </div>
      </div>
    </nav>

    <section class="app-hero">
      <h1>Unsaid. Unseen. Unforgettable.</h1>
      <p style="color:#aaa; margin-top:15px;">Anonymous emotions expressed safely and privately.</p>
    </section>

    <main class="container">
        <section class="card" id="write">
            <h3>💌 Write your confession</h3>
            <textarea id="confInput" placeholder="Write your anonymous confession..."></textarea>
            <button class="submit-btn" onclick="postConfession()">Create Anonymous Link</button>
        </section>

        <section>
            <h3>Recent Confessions</h3>
            <div id="confList">
                <div class="confession-item">Sometimes silence is the loudest goodbye.</div>
            </div>
        </section>
    </main>
</div>

<div class="modal-overlay" id="infoModal">
    <div class="modal-box">
        <h2 id="infoTitle" style="color:var(--pink);"></h2>
        <div id="infoContent" style="color:#aaa; font-size:14px; line-height:1.6; margin-top:15px;"></div>
        <button class="submit-btn" style="margin-top:20px;" onclick="closeModal()">Close</button>
    </div>
</div>

<script>
function enterPlatform() {
    document.getElementById('landingGate').style.display = 'none';
    const app = document.getElementById('mainApp');
    app.style.display = 'block';
    setTimeout(() => { app.style.opacity = '1'; }, 10);
}

window.addEventListener("scroll", ()=>{
  if(window.scrollY > 50) document.getElementById("navbar").classList.add("shrink");
  else document.getElementById("navbar").classList.remove("shrink");
});

function postConfession() {
    const text = document.getElementById('confInput').value.trim();
    if(!text) return alert("Write something first.");

    const uniqueID = Math.random().toString(36).substring(2, 10);
    const generatedLink = "https://unsaid.me/confess/" + uniqueID;

    document.getElementById('confList').insertAdjacentHTML('afterbegin', `<div class="confession-item">${text}</div>`);

    document.getElementById('write').innerHTML = `
        <div style="text-align: center; animation: fadeIn 0.5s ease;">
            <h3 style="color: var(--pink);">Link Created! 🔗</h3>
            <p style="font-size: 13px; color: #aaa; margin: 10px 0;">Click the link to simulate the Receiver View</p>
            <div style="background: #000; padding: 12px; border: 1px dashed var(--pink); border-radius: 8px; margin: 15px 0; cursor:pointer;" onclick="simulateReceiver('${text}')">
                <span style="font-size: 14px; color: var(--pink-soft); text-decoration:underline;">${generatedLink}</span>
            </div>
            <button class="submit-btn" onclick="copyToClipboard('${generatedLink}')" id="copyBtn">Copy Link</button>
            <p onclick="resetWriteCard()" style="font-size: 12px; color: #555; margin-top: 15px; cursor: pointer;">Write another</p>
        </div>
    `;
}

function simulateReceiver(originalText) {
    const modal = document.getElementById('infoModal');
    document.getElementById('infoTitle').innerText = "Reply Anonymously";
    document.getElementById('infoContent').innerHTML = `
        <div style="background:#000; padding:15px; border-radius:10px; margin-bottom:15px; border:1px solid #333;">
            <p style="color:white; font-style:italic;">"${originalText}"</p>
        </div>
        <textarea id="replyIn" placeholder="Write your anonymous reply..." style="height:80px; width:100%; background:#000; border:1px solid #333; color:white; padding:10px; border-radius:10px;"></textarea>
        <button class="submit-btn" onclick="alert('Reply sent!'); closeModal()">Send Reply</button>
    `;
    modal.style.display = 'flex';
}

function copyToClipboard(link) {
    navigator.clipboard.writeText(link).then(() => {
        document.getElementById('copyBtn').innerText = "Copied!";
        setTimeout(() => { document.getElementById('copyBtn').innerText = "Copy Link"; }, 2000);
    });
}

function resetWriteCard() {
    document.getElementById('write').innerHTML = `<h3>💌 Write your confession</h3><textarea id="confInput" placeholder="Write your anonymous confession..."></textarea><button class="submit-btn" onclick="postConfession()">Create Anonymous Link</button>`;
}

function toggleProfile(){
  if(!localStorage.getItem("user")){
    const email = prompt("Enter Email to Signup:");
    if(email) { localStorage.setItem("user", "User_" + Math.floor(Math.random()*999)); updateAuth(); }
  } else {
    const dd = document.getElementById("dropdown");
    dd.style.display = dd.style.display === "flex" ? "none" : "flex";
  }
}

function updateAuth(){ document.getElementById("authBtn").innerText = localStorage.getItem("user") ? "Profile" : "Login"; }
function logout(){ localStorage.removeItem("user"); updateAuth(); document.getElementById("dropdown").style.display="none"; }

function showInfo(type) {
    const modal = document.getElementById('infoModal');
    const title = document.getElementById('infoTitle');
    const content = document.getElementById('infoContent');
    modal.style.display = 'flex';
    if(type === 'rules') {
        title.innerText = "Community Rules";
        content.innerHTML = "• Be respectful.<br>• No hate speech.<br>• Keep anonymity safe.";
    } else if(type === 'privacy') {
        title.innerText = "Privacy Policy";
        content.innerHTML = "We do not track IPs or identities. Your confessions are fully anonymous.";
    } else if(type === 'agreement') {
        title.innerText = "User Agreement";
        content.innerHTML = "• Post responsibly.<br>• Responses are voluntary.<br>• Users are responsible for their content.";
    } else {
        title.innerText = "Poems & Shayari";
        content.innerHTML = "Share your soul through words. We welcome your deepest shayari.";
    }
}

function closeModal() { document.getElementById('infoModal').style.display = 'none'; }
updateAuth();
</script>

</body>
</html>
