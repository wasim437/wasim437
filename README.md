<!--
Package: Super-Unique GitHub Profile + GitHub-Pages Dashboard
Files included below (copy each into your GitHub repo):

1) README.md          -> put in repo named exactly as your username (shows on profile)
2) docs/index.html    -> GitHub Pages site (dashboard + animations)
3) docs/assets/style.css
4) docs/assets/script.js
5) docs/game/snake.html -> simple responsive Snake game (playable on Pages)
6) docs/game/snake.js
7) docs/game/style.css

How to use:
- Create a repo named exactly as your GitHub username (example: wasim437)
- Copy README.md to the root of the repo
- Copy the docs/ folder and its files into the repo (this will be the GitHub Pages site)
- In repo Settings -> Pages, select branch `main` (or `gh-pages`) and folder `/docs` then Save
- Fork and enable the Platane snk GitHub Action to generate the snake SVG, or follow their README to create `output/github-contribution-grid-snake.svg`
- Customize your name, links, and skills inside README.md and docs/assets/script.js

Enjoy! Edit anything and push to GitHub — I can help customize colors, emojis, or change game difficulty.
-->

=== README.md ===
# 👋 Hi, I'm **Mohamed Wasim** — Welcome to my ✨Sarcastic + Animated Dashboard✨

> *The only analytics dashboard where the graphs judge you back.* 😏

<p align="center">
  <img src="docs/assets/hero-animated.gif" alt="animated-hero" width="420"/>
</p>

---

## 🧾 Quick Bio
- 🔭 Working on AI / ML / GenAI projects
- 🧠 Passionate about agents, NLP, and creative code experiments
- 💼 Freelance & Open-source contributor
- 📍 Chennai / Remote

---

## 🛠️ Tech Stack (Emoji Overload)
<p align="center">
  <img src="https://img.shields.io/badge/Python-🐍-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/TensorFlow-🧠-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/PyTorch-🔥-red?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Streamlit-📊-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/SQL-🗄️-yellow?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Linux-🐧-black?style=for-the-badge" />
</p>

---

## 🕹️ Play With My Stuff
- 🎮 **Mini game (Dino / Snake)** — [Play now on my Pages](https://USERNAME.github.io/game/snake.html)
- 🐍 **Contribution Snake** (auto-generated with GitHub Action) — shown in docs site and README when available

---

## 📊 Sarcastic Dashboard Snapshot
> (A fancy snapshot of live widgets is below — for the real live stuff, open my GitHub Pages)

![GitHub stats](https://github-readme-stats.vercel.app/api?username=USERNAME&show_icons=true&theme=radical)


---

## 📡 Live Dashboard (Hosted on GitHub Pages)
> Click the "Open Dashboard" button to view an animated, reactive dashboard with sarcastic comments and interactive widgets.

<p align="center">
  <a href="https://USERNAME.github.io/index.html">
    <img src="https://img.shields.io/badge/Open%20Dashboard-▶️-blue?style=for-the-badge" alt="Open Dashboard" />
  </a>
</p>

---

## 🔧 How to Customize
1. Replace `USERNAME` in README.md and docs/assets/script.js with your GitHub username.
2. Change the hero gif `docs/assets/hero-animated.gif` to your own (keep similar dimensions).
3. Edit `docs/index.html` to add/remove cards, data, or change the sarcastic text.
4. To get the contribution-snake: fork Platane/snk and follow their actions to generate `output/github-contribution-grid-snake.svg` in your repo root, then update image path in README.

---

## 📬 Contact
- LinkedIn: https://linkedin.com/in/mohamed-wasim-227171260
- Email: wasimmisaw437@gmail.com

---

<p align="center">Made with ☕, 🧠, and a little sarcasm. ✨</p>

=== docs/index.html ===
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Wasim's Animated Dashboard</title>
  <link rel="stylesheet" href="assets/style.css">
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;500;700&display=swap" rel="stylesheet">
  <!-- Lottie for vector animations -->
  <script src="https://unpkg.com/@lottiefiles/lottie-player@latest/dist/lottie-player.js"></script>
</head>
<body>
  <header class="topbar">
    <div class="left">
      <h1>👋 Wasim's <span class="muted">Sarcastic</span> Dashboard</h1>
      <p class="subtitle">Analytics that roast you — with style.</p>
    </div>
    <div class="right">
      <a class="btn" href="https://github.com/USERNAME"><img src="https://img.shields.io/badge/GitHub-Profile-black?style=flat-square&logo=github" /></a>
      <a class="btn" href="/game/snake.html"><img src="https://img.shields.io/badge/Play-Game-FF69B4?style=flat-square&logo=unity" /></a>
    </div>
  </header>

  <main class="grid">
    <section class="card big">
      <div class="card-head">Live Mood Meter <span class="sarcastic">(Probably lies)</span></div>
      <div class="meter" id="moodMeter">
        <!-- animated SVG will be injected by JS -->
      </div>
      <div class="comment" id="moodComment">Loading sarcastic verdict...</div>
    </section>

    <section class="card small">
      <div class="card-head">GitHub Snapshot</div>
      <img src="https://github-readme-stats.vercel.app/api?username=USERNAME&show_icons=true&theme=radical" alt="stats"/>
    </section>

    <section class="card small">
      <div class="card-head">Contribution Snake</div>
      <img src="output/github-contribution-grid-snake.svg" alt="snake" onerror="this.src='assets/fallback-snake.svg'"/>
    </section>

    <section class="card small">
      <div class="card-head">Skill-o-Meter</div>
      <div class="skills" id="skills">
        <!-- js fills this -->
      </div>
    </section>

    <section class="card wide">
      <div class="card-head">Live Console (Sarcastic)</div>
      <pre class="console" id="console">Ready. Waiting for your glorious commits.</pre>
      <button class="btn ghost" id="fakeCommit">Simulate Commit</button>
    </section>
  </main>

  <footer class="footer">
    <div>Made with ☕ and a suspicious amount of JavaScript.</div>
  </footer>

  <script src="assets/script.js"></script>
</body>
</html>

=== docs/assets/style.css ===
:root{
  --bg:#0f1724; --card:#0b1220; --accent:#ff7ab6; --muted:#9aa4b2; --glass: rgba(255,255,255,0.03);
  --glass-2: rgba(255,255,255,0.02);
}
*{box-sizing:border-box;font-family:Montserrat,system-ui,Segoe UI,Roboto,'Helvetica Neue',Arial}
body{margin:0;background:linear-gradient(180deg,#071020,var(--bg));color:#e6eef8}
.topbar{display:flex;justify-content:space-between;align-items:center;padding:18px 32px}
.topbar h1{margin:0;font-size:20px}
.topbar .muted{color:var(--accent)}
.topbar .subtitle{margin:4px 0 0;font-size:13px;color:var(--muted)}
.btn{display:inline-block;margin-left:8px}
.grid{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;padding:24px}
.card{background:linear-gradient(180deg,var(--glass),var(--glass-2));padding:16px;border-radius:14px;box-shadow:0 6px 20px rgba(0,0,0,0.6)}
.card.big{grid-column:span 2;min-height:260px}
.card.wide{grid-column:span 3}
.card-head{font-weight:700;margin-bottom:8px}
.meter{height:150px;display:flex;align-items:center;justify-content:center}
.comment{margin-top:12px;color:var(--muted)}
.skills{display:flex;gap:8px;flex-wrap:wrap}
.skill{padding:8px 12px;border-radius:999px;background:rgba(255,255,255,0.03);font-weight:600}
.console{background:#061020;padding:12px;border-radius:8px;height:110px;overflow:auto}
.btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px 12px;border-radius:8px;margin-top:8px;color:#fff}
.footer{padding:12px 24px;text-align:center;color:var(--muted)}
@media(max-width:900px){.grid{grid-template-columns:1fr}.card.big{grid-column:span 1}.card.wide{grid-column:span 1}}

=== docs/assets/script.js ===
// Replace USERNAME when you copy
const USERNAME = 'USERNAME';

// Mood meter animation (SVG circle runner)
const moodMeter = document.getElementById('moodMeter');
const moodComment = document.getElementById('moodComment');

function rand(min,max){return Math.floor(Math.random()*(max-min+1))+min}

function renderMood(){
  const mood = rand(0,100);
  const svg = `
  <svg width="300" height="120" viewBox="0 0 300 120" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <linearGradient id="g1" x1="0" x2="1"><stop offset="0" stop-color="#00d4ff" /><stop offset="1" stop-color="#ff7ab6" /></linearGradient>
    </defs>
    <rect x="10" y="30" width="280" height="40" rx="20" fill="#031018" stroke="#08242f" />
    <rect x="12" y="32" width="${(mood/100)*256}" height="36" rx="18" fill="url(#g1)">
      <animate attributeName="width" from="0" to="${(mood/100)*256}" dur="1s" fill="freeze" />
    </rect>
    <text x="150" y="24" font-size="14" text-anchor="middle" fill="#cde9ff">Mood: ${mood}%</text>
  </svg>
  `;
  moodMeter.innerHTML = svg;
  // sarcastic comment
  const jokes = [
    "Coding energy: suspiciously caffeinated ☕",
    "Confidence: 63% — Compiler: 0% 😬",
    "GPU temperature: Proudly melting 🔥",
    "Will this deploy? Probably. Will it work? Nope. 🤡",
  ];
  moodComment.textContent = jokes[rand(0,jokes.length-1)];
}

// Skill-o-meter
const skills = [
  {name:'Python 🐍', level:98, emoji:'🤓'},
  {name:'ML/AI 🤖', level:92, emoji:'🤯'},
  {name:'DL 🧠', level:85, emoji:'🔥'},
  {name:'Streamlit 📊', level:76, emoji:'🎭'},
  {name:'SQL 🗄️', level:70, emoji:'😅'},
  {name:'Linux 🐧', level:88, emoji:'🛠️'},
];

function renderSkills(){
  const container = document.getElementById('skills');
  container.innerHTML = '';
  skills.forEach(s=>{
    const el = document.createElement('div');
    el.className = 'skill';
    el.innerHTML = `${s.emoji} ${s.name} <strong style="margin-left:8px;color:var(--muted);font-weight:700">${s.level}%</strong>`;
    container.appendChild(el);
  })
}

// Fake console log spam
const consoleEl = document.getElementById('console');
function fakeLog(msg){
  consoleEl.textContent = `${new Date().toLocaleTimeString()} - ${msg}\n` + consoleEl.textContent;
}

document.getElementById('fakeCommit').addEventListener('click',()=>{
  const outcomes = [
    'Unit tests passed (but we both know they are fake)',
    'Merge conflict: you vs. yourself',
    'Deploy succeeded. No errors logged. Lies detected later.',
    'Refactor complete. Code now 50% prettier, 100% slower.'
  ];
  fakeLog(outcomes[rand(0,outcomes.length-1)]);
});

// Initial render
renderMood();
renderSkills();
fakeLog('Dashboard initialized. Awaiting your inevitable brilliance.');

// Periodically change mood
setInterval(renderMood, 8000);

=== docs/assets/fallback-snake.svg ===
<!-- simple static fallback snake svg (tiny) -->
<svg xmlns="http://www.w3.org/2000/svg" width="300" height="70" viewBox="0 0 300 70">
  <rect width="300" height="70" fill="#071020" rx="8"/>
  <text x="150" y="40" fill="#7fffd4" text-anchor="middle" font-family="Arial" font-size="14">🐍 Snake will appear here (enable Actions)</text>
</svg>

=== docs/game/snake.html ===
<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Snake — Wasim</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="game-wrap">
    <h2>🐍 Wasim's Tiny Snake</h2>
    <canvas id="game" width="360" height="360"></canvas>
    <div class="controls">Use arrow keys or swipe to move • <button id="restart">Restart</button></div>
  </div>
  <script src="snake.js"></script>
</body>
</html>

=== docs/game/style.css ===
body{margin:0;font-family:Montserrat,Arial;background:linear-gradient(180deg,#071020,#041021);color:#fff;display:flex;align-items:center;justify-content:center;height:100vh}
.game-wrap{background:rgba(255,255,255,0.03);padding:18px;border-radius:12px;box-shadow:0 8px 30px rgba(0,0,0,0.6);text-align:center}
canvas{background:#031517;border-radius:8px;display:block;margin:10px auto}
.controls{margin-top:8px}

=== docs/game/snake.js ===
const canvas = document.getElementById('game');
const ctx = canvas.getContext('2d');
const size = 20; const cols = canvas.width/size; const rows = canvas.height/size;
let snake = [{x:5,y:5}]; let dir={x:1,y:0}; let food={x:10,y:10}; let score=0; let speed=6; let tick=0;

function spawnFood(){ food={x:Math.floor(Math.random()*cols), y:Math.floor(Math.random()*rows)};
  // avoid spawning on snake
  if(snake.some(s=>s.x===food.x && s.y===food.y)) spawnFood();
}

function draw(){
  ctx.fillStyle='#031517'; ctx.fillRect(0,0,canvas.width,canvas.height);
  // draw snake
  for(let i=0;i<snake.length;i++){
    ctx.fillStyle = i===0 ? '#ff7ab6' : '#00d4ff';
    ctx.fillRect(snake[i].x*size, snake[i].y*size, size-1, size-1);
  }
  // draw food
  ctx.fillStyle='#ffd166'; ctx.fillRect(food.x*size, food.y*size, size-1, size-1);
  // score
  ctx.fillStyle='#bcd'; ctx.font='14px Arial'; ctx.fillText('Score: '+score,10,18);
}

function update(){
  tick++;
  if(tick % Math.floor(12/speed) !==0) return;
  const head = {x:snake[0].x+dir.x, y:snake[0].y+dir.y};
  // wall wrap
  if(head.x<0) head.x = cols-1; if(head.x>=cols) head.x=0; if(head.y<0) head.y=rows-1; if(head.y>=rows) head.y=0;
  // hit self
  if(snake.some(s=>s.x===head.x && s.y===head.y)){ score=0; snake=[{x:5,y:5}]; dir={x:1,y:0}; spawnFood(); return; }
  snake.unshift(head);
  if(head.x===food.x && head.y===food.y){ score++; spawnFood(); if(score%3===0) speed+=0.5; }
  else snake.pop();
}

function loop(){ update(); draw(); requestAnimationFrame(loop); }

window.addEventListener('keydown',e=>{
  if(e.key==='ArrowUp' && dir.y!==1) dir={x:0,y:-1};
  if(e.key==='ArrowDown' && dir.y!==-1) dir={x:0,y:1};
  if(e.key==='ArrowLeft' && dir.x!==1) dir={x:-1,y:0};
  if(e.key==='ArrowRight' && dir.x!==-1) dir={x:1,y:0};
});

// basic touch controls
let startX=0, startY=0;
canvas.addEventListener('touchstart',e=>{ const t=e.touches[0]; startX=t.clientX; startY=t.clientY; });
canvas.addEventListener('touchend',e=>{ const t=e.changedTouches[0]; const dx=t.clientX-startX, dy=t.clientY-startY; if(Math.abs(dx)>Math.abs(dy)){ if(dx>0 && dir.x!==-1) dir={x:1,y:0}; else if(dx<0 && dir.x!==1) dir={x:-1,y:0}; } else { if(dy>0 && dir.y!==-1) dir={x:0,y:1}; else if(dy<0 && dir.y!==1) dir={x:0,y:-1}; } });

spawnFood(); loop();

=== docs/assets/hero-animated.gif ===
(Binary placeholder) -- Replace with your animated GIF. Recommended: 420px width, transparent BG, looped. Use your own or get a free one from giphy.com or create via Lottie + convert to GIF.
