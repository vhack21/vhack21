
<!DOCTYPE html>
<html>
<head>
<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Share+Tech+Mono&display=swap');

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: #000;
    color: #c0c0c0;
    font-family: 'JetBrains Mono', monospace;
    min-height: 100vh;
    overflow-x: hidden;
  }

  #rain-canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
    z-index: 0;
    opacity: 0.18;
  }

  .page {
    position: relative;
    z-index: 1;
    max-width: 680px;
    margin: 0 auto;
    padding: 40px 24px 60px;
  }

  /* ── BAT SIGNAL ── */
  .bat-signal-wrap {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 12px;
    animation: pulse-glow 3s ease-in-out infinite;
  }

  @keyframes pulse-glow {
    0%,100% { filter: drop-shadow(0 0 8px #8B000088); }
    50%      { filter: drop-shadow(0 0 24px #8B000088) drop-shadow(0 0 48px #3b000044); }
  }

  /* ── HERO NAME ── */
  .hero-name {
    text-align: center;
    font-size: 28px;
    font-weight: 700;
    letter-spacing: 6px;
    color: #fff;
    text-shadow: 0 0 20px #8B0000, 0 0 40px #3b0000;
    margin-bottom: 4px;
    animation: flicker 6s infinite;
  }

  @keyframes flicker {
    0%,94%,100% { opacity: 1; }
    95% { opacity: 0.7; }
    97% { opacity: 1; }
    98% { opacity: 0.85; }
  }

  .hero-sub {
    text-align: center;
    font-size: 11px;
    color: #8B0000;
    letter-spacing: 4px;
    margin-bottom: 32px;
  }

  /* ── TYPING LINE ── */
  .typing-wrap {
    text-align: center;
    height: 22px;
    margin-bottom: 28px;
  }
  #typed {
    font-size: 13px;
    color: #cc3333;
    border-right: 2px solid #8B0000;
    display: inline-block;
    animation: blink-cursor 0.9s step-end infinite;
  }
  @keyframes blink-cursor { 0%,100%{border-color:#8B0000;} 50%{border-color:transparent;} }

  /* ── DIVIDER ── */
  .divider {
    border: none;
    border-top: 0.5px solid #2a0000;
    margin: 0 0 28px;
  }
  .divider-red {
    border-top-color: #8B0000;
    margin: 20px 0;
  }

  /* ── SECTION LABEL ── */
  .section-label {
    font-size: 10px;
    letter-spacing: 3px;
    color: #8B0000;
    margin-bottom: 14px;
    text-transform: uppercase;
  }

  /* ── IDENTITY CARD ── */
  .identity-grid {
    display: grid;
    grid-template-columns: 120px 1fr;
    gap: 6px 0;
    background: #0a0000;
    border: 0.5px solid #2a0000;
    border-radius: 6px;
    padding: 18px 20px;
    margin-bottom: 28px;
  }
  .id-key {
    font-size: 11px;
    color: #555;
    padding: 3px 0;
  }
  .id-val {
    font-size: 11px;
    color: #c0c0c0;
    padding: 3px 0;
  }
  .id-val span.red { color: #cc3333; }
  .id-val span.green { color: #1a6644; }
  .id-status {
    display: flex;
    align-items: center;
    gap: 6px;
  }
  .status-dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: #cc3333;
    animation: status-pulse 2s ease-in-out infinite;
  }
  @keyframes status-pulse {
    0%,100%{ box-shadow: 0 0 4px #cc3333; opacity:1; }
    50%{ box-shadow: 0 0 12px #cc3333; opacity:0.7; }
  }

  /* ── TECH PILLS ── */
  .tech-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 28px;
  }
  .tech-pill {
    font-size: 10px;
    letter-spacing: 1px;
    background: #0a0000;
    border: 0.5px solid #3a0000;
    color: #cc3333;
    padding: 5px 12px;
    border-radius: 3px;
    cursor: default;
    transition: background 0.2s, border-color 0.2s, color 0.2s;
  }
  .tech-pill:hover {
    background: #1a0000;
    border-color: #8B0000;
    color: #fff;
  }

  /* ── CODE BLOCK ── */
  .code-block {
    background: #060606;
    border: 0.5px solid #1a0000;
    border-left: 2px solid #8B0000;
    border-radius: 4px;
    padding: 18px 20px;
    margin-bottom: 28px;
    font-size: 11px;
    line-height: 1.8;
    overflow-x: auto;
  }
  .code-kw { color: #8B0000; }
  .code-type { color: #cc3333; }
  .code-str { color: #4a7a4a; }
  .code-field { color: #888; }
  .code-val { color: #c0c0c0; }
  .code-comment { color: #333; }

  /* ── STATS GRID ── */
  .stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    margin-bottom: 28px;
  }
  .stat-card {
    background: #0a0000;
    border: 0.5px solid #2a0000;
    border-radius: 6px;
    padding: 14px 16px;
    transition: border-color 0.2s;
    cursor: default;
  }
  .stat-card:hover { border-color: #8B0000; }
  .stat-label { font-size: 9px; color: #555; letter-spacing: 2px; margin-bottom: 6px; text-transform: uppercase; }
  .stat-value { font-size: 22px; font-weight: 700; color: #cc3333; }
  .stat-sub { font-size: 9px; color: #3a1a1a; margin-top: 4px; }

  /* ── ACTIVITY BARS ── */
  .activity-wrap { margin-bottom: 28px; }
  .activity-row {
    display: grid;
    grid-template-columns: 80px 1fr 36px;
    align-items: center;
    gap: 10px;
    margin-bottom: 8px;
  }
  .act-lang { font-size: 10px; color: #666; letter-spacing: 1px; }
  .act-bar-bg {
    background: #0d0d0d;
    border-radius: 2px;
    height: 4px;
    overflow: hidden;
  }
  .act-bar {
    height: 100%;
    background: linear-gradient(90deg, #8B0000, #cc3333);
    border-radius: 2px;
    width: 0;
    transition: width 1.2s cubic-bezier(.4,0,.2,1);
  }
  .act-pct { font-size: 9px; color: #555; text-align: right; }

  /* ── WHILE LOOP ── */
  .loop-block {
    background: #060606;
    border: 0.5px solid #1a0000;
    border-radius: 4px;
    padding: 16px 20px;
    text-align: center;
    font-size: 12px;
    line-height: 2;
    margin-bottom: 28px;
    position: relative;
    overflow: hidden;
  }
  .loop-running {
    font-size: 9px;
    color: #3a3a3a;
    letter-spacing: 3px;
    margin-top: 8px;
    animation: running-fade 2s ease-in-out infinite;
  }
  @keyframes running-fade { 0%,100%{opacity:0.3;} 50%{opacity:1;} }

  /* ── CONNECT ROW ── */
  .connect-row {
    display: flex;
    gap: 12px;
    justify-content: center;
    margin-bottom: 8px;
  }
  .connect-btn {
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    color: #555;
    background: #0a0000;
    border: 0.5px solid #2a0000;
    border-radius: 3px;
    padding: 8px 16px;
    cursor: pointer;
    text-decoration: none;
    transition: color 0.2s, border-color 0.2s;
    text-transform: uppercase;
  }
  .connect-btn:hover { color: #cc3333; border-color: #8B0000; }

  /* ── FOOTER QUOTE ── */
  .footer-quote {
    text-align: center;
    font-size: 12px;
    color: #2a0000;
    letter-spacing: 2px;
    margin-top: 8px;
    font-style: italic;
  }
  .footer-quote em { color: #4a1a1a; font-style: normal; }

  /* ── ANIMATED TICKER ── */
  .ticker-wrap {
    overflow: hidden;
    white-space: nowrap;
    border-top: 0.5px solid #1a0000;
    border-bottom: 0.5px solid #1a0000;
    padding: 6px 0;
    margin-bottom: 28px;
  }
  .ticker-inner {
    display: inline-block;
    animation: ticker 20s linear infinite;
    font-size: 9px;
    color: #3a0000;
    letter-spacing: 3px;
  }
  @keyframes ticker { from { transform: translateX(100%); } to { transform: translateX(-100%); } }

  /* ── SCROLLING STREAK ── */
  .streak-row {
    display: flex;
    gap: 3px;
    margin-bottom: 28px;
    flex-wrap: wrap;
  }
  .streak-day {
    width: 10px; height: 10px;
    border-radius: 2px;
    background: #0d0d0d;
    border: 0.5px solid #111;
    transition: background 0.3s;
  }
  .streak-day.active { background: #8B0000; border-color: #cc3333; }
  .streak-day.hot    { background: #cc3333; border-color: #ff4444; }
</style>
</head>
<body>

<canvas id="rain-canvas"></canvas>

<div class="page">

  <!-- BAT SIGNAL SVG -->
  <div class="bat-signal-wrap">
    <svg width="90" height="90" viewBox="0 0 90 90" xmlns="http://www.w3.org/2000/svg">
      <circle cx="45" cy="45" r="40" fill="#0a0000" stroke="#8B0000" stroke-width="1"/>
      <!-- bat silhouette -->
      <path d="M45 52
        C38 52 33 47 28 46
        C22 45 17 47 15 50
        C18 45 20 38 26 36
        C22 33 20 28 22 24
        C25 28 29 30 33 29
        C35 26 38 24 42 24
        C40 27 40 30 42 32
        L45 30 L48 32
        C50 30 50 27 48 24
        C52 24 55 26 57 29
        C61 30 65 28 68 24
        C70 28 68 33 64 36
        C70 38 72 45 75 50
        C73 47 68 45 62 46
        C57 47 52 52 45 52Z"
        fill="#8B0000"/>
      <!-- body -->
      <ellipse cx="45" cy="55" rx="5" ry="7" fill="#8B0000"/>
    </svg>
  </div>

  <!-- NAME -->
  <div class="hero-name">VEDANT SAGAR</div>
  <div class="hero-sub">SOFTWARE ENGINEER · THE DARK KNIGHT OF BACKEND</div>

  <!-- TYPING -->
  <div class="typing-wrap">
    <span id="typed"></span>
  </div>

  <!-- TICKER -->
  <div class="ticker-wrap">
    <span class="ticker-inner">
      ◈ JAVA &nbsp;&nbsp; ◈ SPRING BOOT &nbsp;&nbsp; ◈ KAFKA &nbsp;&nbsp; ◈ REDIS &nbsp;&nbsp; ◈ POSTGRESQL &nbsp;&nbsp; ◈ MICROSERVICES &nbsp;&nbsp; ◈ KUBERNETES &nbsp;&nbsp; ◈ DOCKER &nbsp;&nbsp; ◈ DISTRIBUTED SYSTEMS &nbsp;&nbsp; ◈ SYSTEM DESIGN &nbsp;&nbsp; ◈ JAVA &nbsp;&nbsp; ◈ SPRING BOOT &nbsp;&nbsp; ◈ KAFKA &nbsp;&nbsp; ◈ REDIS &nbsp;&nbsp;
    </span>
  </div>

  <hr class="divider">

  <!-- IDENTITY -->
  <div class="section-label">▸ IDENTITY MATRIX</div>
  <div class="identity-grid">
    <div class="id-key">&gt; Name</div>       <div class="id-val">Vedant Sagar</div>
    <div class="id-key">&gt; Role</div>       <div class="id-val"><span class="red">Software Engineer</span></div>
    <div class="id-key">&gt; Language</div>   <div class="id-val">Java</div>
    <div class="id-key">&gt; Stack</div>      <div class="id-val">Spring Boot · Kafka · Redis</div>
    <div class="id-key">&gt; Database</div>   <div class="id-val">PostgreSQL · MySQL · MongoDB</div>
    <div class="id-key">&gt; Arch</div>       <div class="id-val">Microservices</div>
    <div class="id-key">&gt; Mode</div>       <div class="id-val">Learning. Building. Shipping.</div>
    <div class="id-key">&gt; Status</div>
    <div class="id-val">
      <div class="id-status">
        <div class="status-dot"></div>
        <span class="red">ACTIVE</span>
      </div>
    </div>
  </div>

  <!-- TECH PILLS -->
  <div class="section-label">▸ TECH ARSENAL</div>
  <div class="tech-grid" id="tech-grid"></div>

  <hr class="divider">

  <!-- BATMAN CODE -->
  <div class="section-label">▸ BATMAN.JAVA</div>
  <div class="code-block">
    <div><span class="code-kw">public final class</span> <span class="code-type">Batman</span> {</div>
    <div>&nbsp;</div>
    <div>&nbsp; <span class="code-kw">private final</span> <span class="code-type">String</span> <span class="code-field">coffee</span> = <span class="code-str">"Black"</span>;</div>
    <div>&nbsp; <span class="code-kw">private final</span> <span class="code-type">String</span> <span class="code-field">codeStyle</span> = <span class="code-str">"Clean"</span>;</div>
    <div>&nbsp; <span class="code-kw">private final</span> <span class="code-type">String</span> <span class="code-field">architecture</span> = <span class="code-str">"Microservices"</span>;</div>
    <div>&nbsp; <span class="code-kw">private final</span> <span class="code-type">String</span> <span class="code-field">cache</span> = <span class="code-str">"Redis"</span>;</div>
    <div>&nbsp; <span class="code-kw">private final</span> <span class="code-type">String</span> <span class="code-field">broker</span> = <span class="code-str">"Kafka"</span>;</div>
    <div>&nbsp; <span class="code-kw">private final</span> <span class="code-type">String</span> <span class="code-field">database</span> = <span class="code-str">"PostgreSQL"</span>;</div>
    <div>&nbsp; <span class="code-kw">private final</span> <span class="code-type">String</span> <span class="code-field">motto</span> =</div>
    <div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="code-str">"Build systems that survive production."</span>;</div>
    <div>&nbsp;</div>
    <div>}</div>
  </div>

  <!-- STATS -->
  <div class="section-label">▸ SIGNAL STRENGTH</div>
  <div class="stats-grid">
    <div class="stat-card">
      <div class="stat-label">Commits</div>
      <div class="stat-value" id="stat-commits">0</div>
      <div class="stat-sub">lines in the dark</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Stars</div>
      <div class="stat-value" id="stat-stars">0</div>
      <div class="stat-sub">signals received</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Streak</div>
      <div class="stat-value" id="stat-streak">0</div>
      <div class="stat-sub">nights consecutive</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Repos</div>
      <div class="stat-value" id="stat-repos">0</div>
      <div class="stat-sub">missions deployed</div>
    </div>
  </div>

  <!-- LANGUAGE ACTIVITY -->
  <div class="section-label">▸ CODE BREAKDOWN</div>
  <div class="activity-wrap" id="activity-wrap"></div>

  <!-- STREAK GRID -->
  <div class="section-label">▸ CONTRIBUTION GRID</div>
  <div class="streak-row" id="streak-row"></div>

  <hr class="divider divider-red">

  <!-- WHILE LOOP -->
  <div class="loop-block">
    <div><span class="code-kw">while</span> (<span class="code-val">alive</span>) {</div>
    <div id="loop-line" style="color:#8B0000;">&nbsp; &nbsp; learn();</div>
    <div><span style="color:#8B0000;">&nbsp; &nbsp; build();</span></div>
    <div><span style="color:#8B0000;">&nbsp; &nbsp; optimize();</span></div>
    <div><span style="color:#8B0000;">&nbsp; &nbsp; deploy();</span></div>
    <div>}</div>
    <div class="loop-running">// RUNNING IN PRODUCTION</div>
  </div>

  <!-- CONNECT -->
  <div class="section-label" style="text-align:center;">▸ BROADCAST CHANNEL</div>
  <div class="connect-row">
    <a class="connect-btn" href="https://www.linkedin.com/in/vedant-sagar-4775531a5/" target="_blank">LinkedIn</a>
    <a class="connect-btn" href="https://leetcode.com/vedant21" target="_blank">LeetCode</a>
    <a class="connect-btn" href="https://twitter.com/vedantsagar14" target="_blank">Twitter</a>
  </div>

  <hr class="divider" style="margin-top:28px;">

  <div class="footer-quote">"The city needs hope." &nbsp;<em>— build it.</em></div>

</div>

<script>
/* ── RAIN ── */
const canvas = document.getElementById('rain-canvas');
const ctx = canvas.getContext('2d');
let drops = [];

function initRain() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  drops = Array.from({length: 80}, () => ({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    len: 10 + Math.random() * 20,
    speed: 2 + Math.random() * 4,
    opacity: 0.05 + Math.random() * 0.15
  }));
}

function animateRain() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  drops.forEach(d => {
    ctx.strokeStyle = `rgba(139,0,0,${d.opacity})`;
    ctx.lineWidth = 0.5;
    ctx.beginPath();
    ctx.moveTo(d.x, d.y);
    ctx.lineTo(d.x - 1, d.y + d.len);
    ctx.stroke();
    d.y += d.speed;
    if (d.y > canvas.height) { d.y = -d.len; d.x = Math.random() * canvas.width; }
  });
  requestAnimationFrame(animateRain);
}

initRain();
animateRain();
window.addEventListener('resize', initRain);

/* ── TYPING EFFECT ── */
const lines = [
  'Software Engineer',
  'Java | Spring Boot',
  'Building Scalable Backend Systems',
  'Distributed Systems Architect',
  'The Night is Dark and Full of Production Bugs'
];
let li = 0, ci = 0, deleting = false;
const typedEl = document.getElementById('typed');

function typeLoop() {
  const cur = lines[li];
  if (!deleting) {
    typedEl.textContent = cur.slice(0, ++ci);
    if (ci === cur.length) { deleting = true; setTimeout(typeLoop, 2200); return; }
    setTimeout(typeLoop, 60);
  } else {
    typedEl.textContent = cur.slice(0, --ci);
    if (ci === 0) { deleting = false; li = (li + 1) % lines.length; setTimeout(typeLoop, 400); return; }
    setTimeout(typeLoop, 30);
  }
}
setTimeout(typeLoop, 800);

/* ── TECH PILLS ── */
const techs = ['Java','Spring Boot','Kafka','Redis','PostgreSQL','MySQL','MongoDB','Docker','Kubernetes','Maven','Gradle','Git','Linux','Microservices','System Design','REST APIs'];
const tg = document.getElementById('tech-grid');
techs.forEach((t, i) => {
  const p = document.createElement('div');
  p.className = 'tech-pill';
  p.textContent = t;
  p.style.opacity = '0';
  p.style.transform = 'translateY(8px)';
  p.style.transition = `opacity 0.4s ${i*0.05}s, transform 0.4s ${i*0.05}s, background 0.2s, border-color 0.2s, color 0.2s`;
  tg.appendChild(p);
  setTimeout(() => { p.style.opacity = '1'; p.style.transform = 'translateY(0)'; }, 300 + i * 50);
});

/* ── COUNTER ANIMATION ── */
function animCount(id, target, duration) {
  const el = document.getElementById(id);
  let start = 0, step = target / (duration / 16);
  const t = setInterval(() => {
    start = Math.min(start + step, target);
    el.textContent = Math.round(start);
    if (start >= target) clearInterval(t);
  }, 16);
}
setTimeout(() => {
  animCount('stat-commits', 247, 1400);
  animCount('stat-stars', 38, 1000);
  animCount('stat-streak', 21, 900);
  animCount('stat-repos', 14, 700);
}, 600);

/* ── LANGUAGE BARS ── */
const langs = [
  { name: 'Java', pct: 78 },
  { name: 'SQL', pct: 12 },
  { name: 'YAML', pct: 5 },
  { name: 'Shell', pct: 3 },
  { name: 'Other', pct: 2 },
];
const aw = document.getElementById('activity-wrap');
langs.forEach((l, i) => {
  const row = document.createElement('div');
  row.className = 'activity-row';
  row.innerHTML = `<div class="act-lang">${l.name}</div>
    <div class="act-bar-bg"><div class="act-bar" id="bar-${i}"></div></div>
    <div class="act-pct">${l.pct}%</div>`;
  aw.appendChild(row);
  setTimeout(() => {
    document.getElementById(`bar-${i}`).style.width = l.pct + '%';
  }, 400 + i * 100);
});

/* ── STREAK GRID ── */
const sr = document.getElementById('streak-row');
const totalDays = 105;
const pattern = [1,1,0,1,1,1,0,1,1,1,1,0,1,0,1,1,1,1,0,0,1,1,1,0,1,1,1,1,1,0,1,1,0,1,1,0,1,1,1,1,0,1,1,1,1,0,0,1,1,1,1,1,1,0,1,1,0,1,1,1,1,1,0,1,1,1,0,1,0,1,1,1,1,0,1,1,1,1,0,1,1,1,0,0,1,1,1,1,0,1,1,0,1,1,1,0,1,1,1,1,1,0,1,1,1];
for (let i = 0; i < totalDays; i++) {
  const d = document.createElement('div');
  d.className = 'streak-day';
  const v = pattern[i % pattern.length];
  const isHot = v && i > 90;
  setTimeout(() => {
    if (isHot) d.classList.add('hot');
    else if (v) d.classList.add('active');
  }, 800 + i * 8);
  sr.appendChild(d);
}

/* ── LOOP LINE CYCLING ── */
const loopLines = ['&nbsp; &nbsp; learn();','&nbsp; &nbsp; build();','&nbsp; &nbsp; optimize();','&nbsp; &nbsp; deploy();'];
let ll = 0;
const loopEl = document.getElementById('loop-line');
setInterval(() => {
  ll = (ll + 1) % loopLines.length;
  loopEl.style.opacity = '0';
  setTimeout(() => {
    loopEl.innerHTML = loopLines[ll];
    loopEl.style.opacity = '1';
  }, 200);
}, 900);
</script>
</body>
</html>
