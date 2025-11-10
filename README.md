<!-- 🎮 IMAGEN DE BIENVENIDA CYBERPUNK -->
<p align="center">
  <img src="https://raw.githubusercontent.com/AnderMendoza/AnderMendoza/main/assets/banner-header.gif" width="100%" alt="Cyberpunk Banner"/>
</p>

<div align="center">

<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Contador — Cyberpunk 77</title>

<!-- Google Fonts (opcional; si no carga, usa fuentes del sistema) -->
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&display=swap" rel="stylesheet">

<style>
  :root{
    --bg1: #020617;
    --bg2: #07102a;
    --neon-pink: #ff2d95;
    --neon-cyan: #00f0ff;
    --neon-yellow: #ffd166;
    --glass: rgba(255,255,255,0.04);
  }

  html,body{height:100%;margin:0;font-family: "Share Tech Mono", "Courier New", monospace;background: radial-gradient(1200px 600px at 10% 10%, rgba(0,240,255,0.03), transparent), linear-gradient(180deg,var(--bg1) 0%, var(--bg2) 100%); color:#e6f8ff; overflow:hidden; }

  /* Moving grid + noise */
  .grid {
    position:fixed; inset:0;
    background-image:
      linear-gradient(90deg, rgba(0,255,255,0.03) 1px, transparent 1px),
      linear-gradient(0deg, rgba(255,45,149,0.02) 1px, transparent 1px);
    background-size: 40px 40px, 40px 40px;
    pointer-events:none;
    mix-blend-mode: overlay;
    animation: drift 30s linear infinite;
    opacity:0.5;
  }
  @keyframes drift { from{transform:translate(0,0)} to{transform:translate(-120px,-60px)} }

  /* Scanlines */
  .scanlines {
    position:fixed; inset:0; pointer-events:none;
    background: repeating-linear-gradient(
      180deg,
      rgba(0,0,0,0.05) 0px,
      rgba(0,0,0,0.05) 1px,
      transparent 1px,
      transparent 3px
    );
    mix-blend-mode: multiply;
  }

  /* Falling matrix-like chars */
  .matrix {
    position: fixed; inset: 0; pointer-events: none; font-family: monospace; font-weight:700;
    background: transparent;
    mask-image: linear-gradient(180deg, rgba(0,0,0,1), rgba(0,0,0,0.4) 60%, rgba(0,0,0,0));
    opacity: 0.18;
  }
  .matrix span{
    position:absolute; top:-10%;
    left:0; right:0;
    font-size:12px; letter-spacing:6px;
    white-space:nowrap;
    transform:translateX(-10%);
    animation: fall linear infinite;
    color:var(--neon-cyan);
    filter: blur(.2px) saturate(140%);
  }
  @keyframes fall {
    0% { transform: translateY(-120%) translateX(0) scale(0.9); opacity:0 }
    10% { opacity:0.6 }
    100% { transform: translateY(120vh) translateX(6vw) scale(1); opacity:0 }
  }

  /* Main card */
  .card {
    position:relative;
    z-index:5;
    width: min(850px, 92vw);
    margin: 6vh auto;
    padding: 28px;
    border-radius: 14px;
    backdrop-filter: blur(6px) saturate(140%);
    background: linear-gradient(135deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    border: 1px solid rgba(0,255,255,0.06);
    box-shadow: 0 10px 40px rgba(0,0,0,0.6), 0 0 40px rgba(0,240,255,0.03) inset;
    display:flex; align-items:center; gap:20px;
    overflow:visible;
  }

  /* left column with avatar / emblem */
  .emblem {
    width: 140px; height:140px;
    border-radius: 12px;
    background: linear-gradient(135deg, rgba(255,45,149,0.12), rgba(0,240,255,0.08));
    border: 1px solid rgba(255,45,149,0.14);
    display:flex; align-items:center; justify-content:center;
    font-family: "Orbitron", "Segoe UI", sans-serif;
    color: var(--neon-pink);
    font-weight:900;
    letter-spacing:3px;
    text-transform:uppercase;
    font-size:18px;
    text-shadow: 0 0 18px rgba(255,45,149,0.25);
    transform: rotate(-6deg) translateY(-6px);
    box-shadow: 0 8px 30px rgba(0,0,0,0.6), 0 0 30px rgba(255,45,149,0.06) inset;
  }

  /* details */
  .meta {
    flex:1;
    display:flex;
    flex-direction:column;
    gap:6px;
  }
  .meta .title {
    font-family: "Orbitron", sans-serif;
    font-size: 22px;
    color: var(--neon-cyan);
    text-transform:uppercase;
    letter-spacing:2px;
    display:flex; align-items:center; gap:12px;
  }
  .meta .title .badge {
    font-size:12px;
    padding:6px 10px;
    background: linear-gradient(90deg, rgba(255,45,149,0.14), rgba(0,240,255,0.07));
    border-radius:999px;
    border:1px solid rgba(255,255,255,0.04);
    color:var(--neon-pink);
    box-shadow: 0 6px 18px rgba(255,45,149,0.03);
  }

  .meta .desc {
    color: #9dbfcc;
    opacity:0.92;
    font-size:13px;
    line-height:1.2;
    max-width:60ch;
  }

  /* counter bubble */
  .counter {
    width:220px;
    height:116px;
    border-radius:12px;
    background: linear-gradient(180deg, rgba(2,8,23,0.6), rgba(6,10,20,0.3));
    border: 1px solid rgba(0,240,255,0.12);
    display:flex; align-items:center; justify-content:center; flex-direction:column;
    box-shadow: 0 8px 40px rgba(0,0,0,0.6), 0 0 30px rgba(0,240,255,0.04) inset;
  }

  .counter .num {
    font-family: "Orbitron", "Segoe UI", sans-serif;
    font-size:44px;
    font-weight:900;
    letter-spacing:2px;
    color: var(--neon-yellow);
    text-shadow:
      0 0 10px rgba(255,209,102,0.12),
      0 0 36px rgba(255,209,102,0.08);
    display:flex; gap:8px; align-items:baseline;
  }

  .counter .label {
    font-size:11px; text-transform:uppercase; opacity:0.9; color:#cfeff7; margin-top:6px;
    letter-spacing:1.6px;
  }

  /* glitch effect overlay */
  .glitch {
    position:absolute; inset:0; z-index:10; pointer-events:none;
    mix-blend-mode: screen;
  }
  .glitch::before, .glitch::after {
    content:"";
    position:absolute; inset:0; background:linear-gradient(90deg, transparent, rgba(255,45,149,0.06), transparent);
    transform:skewX(-8deg);
    animation: glitchMove 6s linear infinite;
    opacity:0.7;
    filter: blur(6px);
  }
  .glitch::after { animation-duration:9s; background:linear-gradient(90deg, transparent, rgba(0,240,255,0.06), transparent); transform:skewX(8deg); }

  @keyframes glitchMove {
    0% { transform: translateX(-20%) skewX(-8deg) }
    50% { transform: translateX(20%) skewX(-4deg) }
    100% { transform: translateX(-20%) skewX(-8deg) }
  }

  /* footer */
  .footer {
    position:fixed; left:18px; bottom:12px; z-index:6; display:flex; gap:12px; align-items:center; color:#8fcbe9; font-size:12px;
    text-shadow: 0 1px 0 rgba(0,0,0,0.6)
  }
  .sig {
    padding:6px 10px; border-radius:8px; background: linear-gradient(90deg, rgba(0,240,255,0.04), rgba(255,45,149,0.03)); border:1px solid rgba(255,255,255,0.03);
    font-weight:700; color:var(--neon-pink); letter-spacing:1px;
  }

  /* small responsive */
  @media (max-width:720px){
    .card { flex-direction:column; align-items:center; padding:18px; gap:14px; }
    .emblem { transform:none; width:120px;height:120px; }
    .counter { width:92%; max-width:420px; }
  }

  /* flicker animations for number */
  .flicker {
    animation: flicker 6s linear infinite;
  }
  @keyframes flicker {
    0%{opacity:1; text-shadow: 0 0 18px rgba(255,209,102,0.12)}
    2%{opacity:.6}
    3%{opacity:1}
    7%{opacity:.8}
    8%{opacity:1}
    100%{opacity:1}
  }

  /* neon underline effect */
  .underline {
    display:inline-block;
    height:4px;
    width:120px;
    border-radius:999px;
    margin-left:12px;
    background: linear-gradient(90deg, var(--neon-cyan), var(--neon-pink));
    box-shadow: 0 0 18px rgba(0,240,255,0.12), 0 0 30px rgba(255,45,149,0.06);
    transform:translateY(-6px);
  }
</style>
</head>
<body>

<div class="grid" aria-hidden="true"></div>
<div class="scanlines" aria-hidden="true"></div>

<!-- matrix-like several spans to create falling effect -->
<div class="matrix" aria-hidden="true" id="matrix">
  <!-- JS will populate multiple lines -->
</div>

<main class="card" role="main" aria-label="Contador cyberpunk">
  <div class="emblem" aria-hidden="true">CY77</div>

  <div class="meta">
    <div class="title">
      VISITOR PROTOCOL
      <span class="badge">CYBERPUNK 77</span>
      <span class="underline" aria-hidden="true"></span>
    </div>

    <div class="desc">
      Módulo de telemetría local — contador de visitas. Visual retro-futurista con glitchy HUD y scanlines. Cada apertura incrementa el registro local del dispositivo.
    </div>
  </div>

  <div class="counter" aria-live="polite" aria-atomic="true">
    <div class="num flicker" id="countDisplay">0</div>
    <div class="label">VISITS</div>
  </div>

  <div class="glitch" aria-hidden="true"></div>
</main>

<footer class="footer" aria-hidden="false">
  <div class="sig">Creado x The Carlos</div>
  <div style="opacity:.7; font-size:11px;">· localStorage · standalone</div>
</footer>

<script>
  // -----------------------------
  // CONFIG
  // -----------------------------
  const KEY = 'contador_cyberpunk_thecarlos_v1'; // unique key in localStorage
  const START = 1; // starting value if not exists
  // -----------------------------

  // increment logic
  let count = localStorage.getItem(KEY);
  if (!count) {
    count = START;
  } else {
    // parse and increment. If it's NaN, reset
    count = parseInt(count, 10);
    if (Number.isNaN(count)) count = START;
    else count = count + 1;
  }
  localStorage.setItem(KEY, count);

  // format with separators for visual
  function formatNumber(n) {
    return String(n).replace(/\B(?=(\d{3})+(?!\d))/g, "·");
  }

  const display = document.getElementById('countDisplay');
  display.textContent = formatNumber(count);

  // subtle digit-level glitch: randomly offset and color bits
  function glitchOnce(){
    const original = display.textContent;
    const shards = [
      {shift: '-6px', color: 'rgba(255,45,149,0.95)', opacity:0.95},
      {shift: '6px', color: 'rgba(0,240,255,0.9)', opacity:0.9}
    ];
    // create overlays
    shards.forEach((s, i) => {
      const span = document.createElement('span');
      span.textContent = original;
      span.style.position = 'absolute';
      span.style.left = 0;
      span.style.top = 0;
      span.style.pointerEvents = 'none';
      span.style.transform = `translateX(${s.shift})`;
      span.style.mixBlendMode = 'screen';
      span.style.color = s.color;
      span.style.opacity = s.opacity;
      span.style.filter = 'blur(0.6px)';
      span.className = 'tempShard';
      display.parentElement.appendChild(span);
      setTimeout(() => span.remove(), 260 + (i*80));
    });
  }

  // random glitches
  setInterval(() => {
    if (Math.random() < 0.22) glitchOnce();
  }, 900);

  // matrix background generation
  (function makeMatrix(){
    const chars = '0 1 ⌘ ⌥ ∑ Δ ░ ▒ ▓ █ ▌ ▐ ▀ ▄ ☆ ✦ ● ▲ ▼ ► ◄ ▸ ▹ ▪ ▫ ▬'.split(' ');
    const root = document.getElementById('matrix');
    const cols = Math.max(8, Math.floor(window.innerWidth / 60));
    for (let i=0;i<cols;i++){
      const span = document.createElement('span');
      span.style.left = (i * (100/cols)) + '%';
      span.style.fontSize = (8 + Math.random()*12) + 'px';
      span.style.opacity = 0.6 + Math.random()*0.4;
      span.style.animationDuration = (8 + Math.random()*14) + 's';
      // create a long column of chars
      let line = '';
      for (let j=0;j<40;j++){
        line += chars[Math.floor(Math.random()*chars.length)];
      }
      span.textContent = line;
      root.appendChild(span);
    }
  })();

  // Accessibility: update document title with count
  document.title = `Contador — ${count} visitas · The Carlos`;

  // OPTIONAL: double-click the counter to reset (with confirmation)
  document.querySelector('.counter').addEventListener('dblclick', (e) => {
    const ok = confirm('Resetear contador local? Esto solo afecta a este navegador.');
    if (ok){
      localStorage.setItem(KEY, START);
      display.textContent = formatNumber(START);
      document.title = `Contador — ${START} visitas · The Carlos`;
      // small visual feedback
      display.style.transition = 'transform .18s ease';
      display.style.transform = 'scale(1.12)';
      setTimeout(()=> display.style.transform = 'scale(1)', 180);
    }
  });

  // prevent text selection weirdness
  document.onselectstart = () => false;
</script>
</body>
</html>


`[ VISITAS REGISTRADAS EN EL SISTEMA ]`

</div>

---

🧠 **Bot Developer | Hacker Digital**  
💾 *Conectando códigos en un mundo distorsionado por la tecnología*  
🚀 *Desde Night City al universo WhatsApp...*

🎯 *Lenguajes, scripts y comandos hechos con estilo ⚡*  
🔊 *“La red no duerme... y yo tampoco.”*

---

## ⚙️ TECNOLOGÍAS

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-0D0D0D?style=for-the-badge&logo=node.js&logoColor=00FF99" alt="Node.js"/>
  <img src="https://img.shields.io/badge/JavaScript-191919?style=for-the-badge&logo=javascript&logoColor=FCEE09" alt="JavaScript"/>
  <img src="https://img.shields.io/badge/Baileys_MD-000000?style=for-the-badge&logo=whatsapp&logoColor=00FF99" alt="Baileys"/>
  <img src="https://img.shields.io/badge/TypeScript-0D0D0D?style=for-the-badge&logo=typescript&logoColor=3178C6" alt="TypeScript"/>
  <img src="https://img.shields.io/badge/Express-0D0D0D?style=for-the-badge&logo=express&logoColor=FFFFFF" alt="Express"/>
  <img src="https://img.shields.io/badge/MongoDB-0D0D0D?style=for-the-badge&logo=mongodb&logoColor=4DB33D" alt="MongoDB"/>
  <img src="https://img.shields.io/badge/Redis-0D0D0D?style=for-the-badge&logo=redis&logoColor=DC382D" alt="Redis"/>
  <img src="https://img.shields.io/badge/OpenAI-0D0D0D?style=for-the-badge&logo=openai&logoColor=00FFFF" alt="OpenAI"/>
</p>

---

## 📱 CONTACTO Y REDES

<p align="center">
  <a href="https://wa.me/525544876071?text=Hola+Carlos%2C+vengo+de+tu+perfil+de+GitHub+💻">
    <img src="https://files.catbox.moe/kn2z7q.jpg" height="125px" alt="WhatsApp Contact">
  </a>
</p>

<p align="center">
  <a href="https://wa.me/525544876071">
    <img src="https://img.shields.io/badge/WhatsApp-525544876071-00FFFF?style=for-the-badge&logo=whatsapp&logoColor=000" alt="WhatsApp"/>
  </a>
  <a href="https://instagram.com/_carlitos.zx">
    <img src="https://img.shields.io/badge/Instagram-_carlitos.zx-FF0090?style=for-the-badge&logo=instagram&logoColor=fff" alt="Instagram"/>
  </a>
</p>

---

## ⚡ CANAL OFICIAL

<p align="center">
  <a href="https://whatsapp.com/channel/0029VbB36XC8aKvQevh8Bp04?text=.menu">
    <img src="https://img.shields.io/badge/Canal_Oficial-00FFFF?style=for-the-badge&logo=whatsapp&logoColor=FF0000" alt="Canal Oficial"/>
  </a>
</p>

---

## 📊 ESTADÍSTICAS GITHUB

<div align="center">
  <a href="https://github.com/thecarlos19/">
    <img src="https://github-readme-stats.vercel.app/api?username=thecarlos19&include_all_commits=true&count_private=true&show_icons=true&line_height=20&title_color=FF00CC&icon_color=FF66FF&text_color=D3D3D3&bg_color=0,000000,130F40&locale=es" width="450" alt="GitHub Stats"/>
    <img src="https://github-readme-stats.vercel.app/api/top-langs?username=thecarlos19&show_icons=true&locale=es&layout=compact&line_height=20&title_color=FF00CC&icon_color=FF66FF&text_color=D3D3D3&bg_color=0,000000,130F40" width="290" alt="Top Languages"/>
  </a>
</div>

---

## 💻 PROYECTO PRINCIPAL

<p align="center">
  <a href="https://github.com/thecarlos19/black-clover-MD">
    <img src="https://github-readme-stats.vercel.app/api/pin/?username=thecarlos19&repo=black-clover-MD&theme=midnight-purple" alt="Black Clover MD"/>
  </a>
</p>

<p align="center">
  🔗 [⬇️ DESCARGAR BLACK-CLOVER-MD](https://github.com/thecarlos19/black-clover-MD/archive/refs/heads/master.zip)
</p>

---

> **⚙️ Powered By** [The Carlos 👑](https://wa.me/525544876071?text=Hola+vengo+de+tu+perfil+de+GitHub+👑)