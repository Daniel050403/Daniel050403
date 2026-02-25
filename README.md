<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Ing. Juan Daniel Alvarado – Dev Profile</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;600;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet" />
<style>
  :root {
    --cyan: #00f7ff;
    --cyan-dim: #00c8d4;
    --bg: #050d12;
    --bg2: #0a1820;
    --bg3: #0f2230;
    --text: #cde8f0;
    --text-dim: #6a9aaa;
    --accent: #ff4f8b;
    --green: #00e676;
    --yellow: #ffe600;
    --purple: #a259ff;
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed; width: 12px; height: 12px;
    background: var(--cyan); border-radius: 50%;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, width 0.2s, height 0.2s;
    box-shadow: 0 0 12px var(--cyan);
  }
  .cursor-ring {
    position: fixed; width: 36px; height: 36px;
    border: 1.5px solid var(--cyan);
    border-radius: 50%; pointer-events: none; z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.12s ease, opacity 0.3s;
    opacity: 0.5;
  }

  /* Grid noise overlay */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image:
      linear-gradient(rgba(0,247,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,247,255,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none; z-index: 0;
  }

  /* Scanline animation */
  body::after {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,247,255,0.015) 2px,
      rgba(0,247,255,0.015) 4px
    );
    pointer-events: none; z-index: 0;
    animation: scanMove 8s linear infinite;
  }
  @keyframes scanMove {
    0% { background-position: 0 0; }
    100% { background-position: 0 100%; }
  }

  section, header, footer { position: relative; z-index: 1; }

  /* ── HEADER ─────────────────────────── */
  header {
    min-height: 100vh;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    text-align: center; padding: 3rem 2rem;
    background: radial-gradient(ellipse 80% 60% at 50% 40%, rgba(0,200,212,0.12) 0%, transparent 70%);
  }

  .avatar-ring {
    width: 120px; height: 120px;
    border-radius: 50%;
    border: 2px solid var(--cyan);
    display: flex; align-items: center; justify-content: center;
    font-size: 2.8rem;
    margin-bottom: 2rem;
    box-shadow: 0 0 30px rgba(0,247,255,0.3), inset 0 0 20px rgba(0,247,255,0.05);
    animation: pulseRing 3s ease-in-out infinite;
  }
  @keyframes pulseRing {
    0%, 100% { box-shadow: 0 0 20px rgba(0,247,255,0.3); }
    50% { box-shadow: 0 0 50px rgba(0,247,255,0.6), 0 0 80px rgba(0,247,255,0.2); }
  }

  .badge-meta {
    display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center;
    margin-bottom: 1.5rem;
    opacity: 0; animation: fadeUp 0.6s 0.4s forwards;
  }
  .badge {
    background: rgba(0,247,255,0.08);
    border: 1px solid rgba(0,247,255,0.2);
    padding: 0.25rem 0.75rem;
    border-radius: 20px;
    font-size: 0.72rem;
    color: var(--cyan-dim);
    letter-spacing: 0.08em;
  }

  .typing-wrapper {
    min-height: 80px;
    display: flex; align-items: center; justify-content: center;
    margin-bottom: 0.75rem;
  }
  #typing-text {
    font-family: 'Syne', sans-serif;
    font-size: clamp(1.6rem, 4vw, 2.6rem);
    font-weight: 800;
    color: var(--cyan);
    text-shadow: 0 0 30px rgba(0,247,255,0.5);
    border-right: 3px solid var(--cyan);
    white-space: nowrap;
    overflow: hidden;
    animation: blink 0.75s step-end infinite;
  }
  @keyframes blink { 0%, 100% { border-color: var(--cyan); } 50% { border-color: transparent; } }

  .subtitle {
    font-size: 0.85rem;
    color: var(--text-dim);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 3rem;
    opacity: 0; animation: fadeUp 0.6s 0.6s forwards;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* Scroll indicator */
  .scroll-hint {
    position: absolute; bottom: 2rem; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 0.5rem;
    color: var(--text-dim); font-size: 0.7rem; letter-spacing: 0.1em;
    opacity: 0; animation: fadeUp 1s 1.5s forwards;
  }
  .scroll-hint .arrow {
    width: 20px; height: 20px;
    border-right: 2px solid var(--cyan-dim);
    border-bottom: 2px solid var(--cyan-dim);
    transform: rotate(45deg);
    animation: bounce 1.5s infinite;
  }
  @keyframes bounce { 0%,100%{transform:rotate(45deg) translateY(0)} 50%{transform:rotate(45deg) translateY(6px)} }

  /* ── SECTIONS ──────────────────────── */
  .section {
    max-width: 900px; margin: 0 auto;
    padding: 4rem 2rem;
    opacity: 0; transform: translateY(40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .section.visible { opacity: 1; transform: translateY(0); }

  .section-label {
    font-size: 0.7rem; letter-spacing: 0.25em;
    color: var(--accent); text-transform: uppercase;
    margin-bottom: 0.5rem;
  }
  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(1.5rem, 3vw, 2rem);
    font-weight: 800;
    color: #fff;
    margin-bottom: 2rem;
    border-bottom: 1px solid rgba(0,247,255,0.15);
    padding-bottom: 0.75rem;
  }

  /* ── TECH GRID ─────────────────────── */
  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 1rem;
  }
  .tech-card {
    background: var(--bg2);
    border: 1px solid rgba(0,247,255,0.1);
    border-radius: 10px;
    padding: 1rem 1.2rem;
    display: flex; align-items: center; gap: 0.75rem;
    transition: border-color 0.3s, transform 0.2s, box-shadow 0.3s;
    cursor: default;
  }
  .tech-card:hover {
    border-color: var(--cyan);
    transform: translateY(-3px);
    box-shadow: 0 8px 24px rgba(0,247,255,0.15);
  }
  .tech-icon { font-size: 1.4rem; }
  .tech-name { font-size: 0.8rem; color: var(--text); font-weight: 600; }

  /* ── SKILL BARS ─────────────────────── */
  .skill-bars { display: flex; flex-direction: column; gap: 1.2rem; }
  .skill-item { }
  .skill-header { display: flex; justify-content: space-between; margin-bottom: 0.4rem; font-size: 0.78rem; }
  .skill-name { color: var(--text); }
  .skill-pct { color: var(--cyan); }
  .bar-bg {
    height: 6px; background: rgba(255,255,255,0.06);
    border-radius: 10px; overflow: hidden;
  }
  .bar-fill {
    height: 100%; border-radius: 10px;
    width: 0;
    transition: width 1.4s cubic-bezier(0.16, 1, 0.3, 1);
    background: linear-gradient(90deg, var(--cyan-dim), var(--cyan));
    box-shadow: 0 0 10px rgba(0,247,255,0.4);
  }

  /* ── INTEGRATIONS ───────────────────── */
  .integration-group { margin-bottom: 2.5rem; }
  .group-label {
    font-size: 0.7rem; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--text-dim); margin-bottom: 1rem;
  }
  .tag-row { display: flex; flex-wrap: wrap; gap: 0.6rem; }
  .tag {
    padding: 0.4rem 1rem;
    border-radius: 6px;
    font-size: 0.78rem;
    font-weight: 600;
    border: 1px solid;
    transition: transform 0.2s, box-shadow 0.2s;
    cursor: default;
  }
  .tag:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(0,0,0,0.3); }
  .tag.cyan   { color: var(--cyan);   border-color: var(--cyan);   background: rgba(0,247,255,0.07); }
  .tag.green  { color: var(--green);  border-color: var(--green);  background: rgba(0,230,118,0.07); }
  .tag.yellow { color: var(--yellow); border-color: var(--yellow); background: rgba(255,230,0,0.07); }
  .tag.purple { color: var(--purple); border-color: var(--purple); background: rgba(162,89,255,0.07); }
  .tag.accent { color: var(--accent); border-color: var(--accent); background: rgba(255,79,139,0.07); }

  /* ── STATS CARDS ────────────────────── */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1.2rem;
  }
  .stat-card {
    background: var(--bg2);
    border: 1px solid rgba(0,247,255,0.1);
    border-radius: 12px;
    padding: 1.5rem;
    text-align: center;
    transition: border-color 0.3s, transform 0.2s;
    position: relative; overflow: hidden;
  }
  .stat-card::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(circle at 50% 0%, rgba(0,247,255,0.06), transparent 70%);
    opacity: 0; transition: opacity 0.3s;
  }
  .stat-card:hover::before { opacity: 1; }
  .stat-card:hover { border-color: var(--cyan); transform: translateY(-4px); }
  .stat-number {
    font-family: 'Syne', sans-serif;
    font-size: 2.2rem; font-weight: 800;
    color: var(--cyan);
    text-shadow: 0 0 20px rgba(0,247,255,0.4);
  }
  .stat-label { font-size: 0.72rem; color: var(--text-dim); margin-top: 0.4rem; letter-spacing: 0.1em; }

  /* ── FOCUS LIST ─────────────────────── */
  .focus-list { display: flex; flex-direction: column; gap: 0.8rem; }
  .focus-item {
    display: flex; align-items: flex-start; gap: 1rem;
    background: var(--bg2);
    border: 1px solid rgba(0,247,255,0.08);
    border-radius: 8px; padding: 1rem 1.2rem;
    transition: border-color 0.3s, transform 0.2s;
  }
  .focus-item:hover { border-color: rgba(0,247,255,0.3); transform: translateX(4px); }
  .focus-check { color: var(--green); font-size: 1rem; flex-shrink: 0; margin-top: 0.1rem; }
  .focus-text { font-size: 0.83rem; line-height: 1.6; color: var(--text); }

  /* ── FOOTER ─────────────────────────── */
  footer {
    text-align: center; padding: 3rem 2rem;
    border-top: 1px solid rgba(0,247,255,0.08);
    color: var(--text-dim); font-size: 0.72rem; letter-spacing: 0.1em;
  }
  footer span { color: var(--cyan); }

  /* ── FLOATING PARTICLES ─────────────── */
  .particles { position: fixed; inset: 0; pointer-events: none; z-index: 0; overflow: hidden; }
  .particle {
    position: absolute;
    width: 2px; height: 2px;
    background: var(--cyan);
    border-radius: 50%;
    opacity: 0;
    animation: floatParticle var(--dur) var(--delay) ease-in infinite;
  }
  @keyframes floatParticle {
    0% { transform: translateY(100vh) scale(0); opacity: 0; }
    10% { opacity: 0.6; }
    90% { opacity: 0.3; }
    100% { transform: translateY(-10vh) scale(1); opacity: 0; }
  }
</style>
</head>
<body>

<!-- Cursor -->
<div class="cursor" id="cur"></div>
<div class="cursor-ring" id="curRing"></div>

<!-- Particles -->
<div class="particles" id="particles"></div>

<!-- ─── HEADER ─── -->
<header>
  <div class="avatar-ring" style="opacity:0;animation:fadeUp 0.5s 0.1s forwards">🚀</div>

  <div class="badge-meta">
    <span class="badge">📍 Ciudad de México</span>
    <span class="badge">🎓 UPT Tecámac</span>
    <span class="badge">💼 2022 – Presente</span>
    <span class="badge">🏢 Consorcio Internacional IMOVS</span>
  </div>

  <div class="typing-wrapper">
    <span id="typing-text"></span>
  </div>

  <p class="subtitle">Gerente de Desarrollo · Especialista en Integración de APIs</p>

  <div class="scroll-hint">
    SCROLL<div class="arrow"></div>
  </div>
</header>

<!-- ─── TECNOLOGÍAS ─── -->
<div class="section" id="s1">
  <p class="section-label">// stack principal</p>
  <h2 class="section-title">🧠 Tecnologías y Arquitectura</h2>
  <div class="tech-grid">
    <div class="tech-card"><span class="tech-icon">⚡</span><span class="tech-name">C# / .NET 8</span></div>
    <div class="tech-card"><span class="tech-icon">🌐</span><span class="tech-name">ASP.NET Core</span></div>
    <div class="tech-card"><span class="tech-icon">🗄️</span><span class="tech-name">SQL Server</span></div>
    <div class="tech-card"><span class="tech-icon">🔗</span><span class="tech-name">Entity Framework</span></div>
    <div class="tech-card"><span class="tech-icon">🤖</span><span class="tech-name">Selenium</span></div>
    <div class="tech-card"><span class="tech-icon">🏗️</span><span class="tech-name">APIs REST</span></div>
    <div class="tech-card"><span class="tech-icon">📐</span><span class="tech-name">Arq. en Capas</span></div>
    <div class="tech-card"><span class="tech-icon">⚙️</span><span class="tech-name">Automatización</span></div>
  </div>

  <div style="margin-top:2.5rem">
    <div class="skill-bars" id="skillBars">
      <div class="skill-item">
        <div class="skill-header"><span class="skill-name">C# / .NET</span><span class="skill-pct">95%</span></div>
        <div class="bar-bg"><div class="bar-fill" data-width="95"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-header"><span class="skill-name">API REST Design</span><span class="skill-pct">92%</span></div>
        <div class="bar-bg"><div class="bar-fill" data-width="92"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-header"><span class="skill-name">SQL Server / EF Core</span><span class="skill-pct">88%</span></div>
        <div class="bar-bg"><div class="bar-fill" data-width="88"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-header"><span class="skill-name">Selenium / Automatización</span><span class="skill-pct">85%</span></div>
        <div class="bar-bg"><div class="bar-fill" data-width="85"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-header"><span class="skill-name">E-commerce / Marketplaces</span><span class="skill-pct">90%</span></div>
        <div class="bar-bg"><div class="bar-fill" data-width="90"></div></div>
      </div>
    </div>
  </div>
</div>

<!-- ─── INTEGRACIONES ─── -->
<div class="section" id="s2">
  <p class="section-label">// servicios externos</p>
  <h2 class="section-title">🔌 Integraciones</h2>

  <div class="integration-group">
    <p class="group-label">🚚 Paqueterías</p>
    <div class="tag-row">
      <span class="tag yellow">DHL</span>
      <span class="tag purple">FedEx</span>
      <span class="tag accent">UPS</span>
    </div>
  </div>

  <div class="integration-group">
    <p class="group-label">💳 Métodos de Pago</p>
    <div class="tag-row">
      <span class="tag cyan">Mercado Pago</span>
      <span class="tag cyan">PayPal</span>
      <span class="tag purple">Stripe</span>
      <span class="tag green">Transferencias Bancarias</span>
    </div>
  </div>

  <div class="integration-group">
    <p class="group-label">🛒 Marketplaces y E-commerce</p>
    <div class="tag-row">
      <span class="tag green">Shopify</span>
      <span class="tag yellow">Mercado Libre</span>
      <span class="tag accent">Amazon</span>
      <span class="tag purple">VTEX</span>
      <span class="tag cyan">Liverpool</span>
      <span class="tag green">CFDI 4.0</span>
    </div>
  </div>
</div>

<!-- ─── STATS ─── -->
<div class="section" id="s3">
  <p class="section-label">// métricas profesionales</p>
  <h2 class="section-title">📊 Estadísticas</h2>
  <div class="stats-grid">
    <div class="stat-card">
      <div class="stat-number" data-count="3">0</div>
      <div class="stat-label">AÑOS DE EXPERIENCIA</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" data-count="5">0</div>
      <div class="stat-label">MARKETPLACES INTEGRADOS</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" data-count="3">0</div>
      <div class="stat-label">PAQUETERÍAS INTEGRADAS</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" data-count="3">0</div>
      <div class="stat-label">PASARELAS DE PAGO</div>
    </div>
  </div>
</div>

<!-- ─── ENFOQUE ─── -->
<div class="section" id="s4">
  <p class="section-label">// filosofía de trabajo</p>
  <h2 class="section-title">⚙️ Enfoque Profesional</h2>
  <div class="focus-list">
    <div class="focus-item"><span class="focus-check">✔</span><span class="focus-text">Liderazgo técnico y gestión de equipos de desarrollo</span></div>
    <div class="focus-item"><span class="focus-check">✔</span><span class="focus-text">Integración de APIs empresariales y servicios externos</span></div>
    <div class="focus-item"><span class="focus-check">✔</span><span class="focus-text">Sistemas de logística y comercio electrónico omnicanal</span></div>
    <div class="focus-item"><span class="focus-check">✔</span><span class="focus-text">Automatización avanzada de procesos con Selenium</span></div>
    <div class="focus-item"><span class="focus-check">✔</span><span class="focus-text">Desarrollo backend robusto, escalable y mantenible</span></div>
    <div class="focus-item"><span class="focus-check">✔</span><span class="focus-text">Arquitectura orientada a integración y microservicios</span></div>
    <div class="focus-item"><span class="focus-check">✔</span><span class="focus-text">Facturación electrónica CFDI 4.0 y conciliación automática</span></div>
  </div>
</div>

<footer>
  <p>Ing. Juan Daniel Alvarado · <span>Daniel050403</span> · Consorcio Internacional IMOVS · <span>Ciudad de México, MX</span></p>
  <p style="margin-top:0.5rem">Built with 💻 · 2025</p>
</footer>

<script>
// ── CURSOR ──
const cur = document.getElementById('cur');
const curRing = document.getElementById('curRing');
let mx = 0, my = 0, rx = 0, ry = 0;
document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
function animCursor() {
  cur.style.left = mx + 'px'; cur.style.top = my + 'px';
  rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12;
  curRing.style.left = rx + 'px'; curRing.style.top = ry + 'px';
  requestAnimationFrame(animCursor);
}
animCursor();

// ── PARTICLES ──
const pContainer = document.getElementById('particles');
for (let i = 0; i < 30; i++) {
  const p = document.createElement('div');
  p.className = 'particle';
  p.style.left = Math.random() * 100 + 'vw';
  p.style.setProperty('--dur', (6 + Math.random() * 10) + 's');
  p.style.setProperty('--delay', (Math.random() * 10) + 's');
  p.style.width = p.style.height = (1 + Math.random() * 2) + 'px';
  pContainer.appendChild(p);
}

// ── TYPING ──
const lines = [
  'Ing. Juan Daniel Alvarado',
  'Gerente de Desarrollo',
  'Especialista en APIs',
  'Sistemas Empresariales',
  'E-commerce & Logística'
];
let li = 0, ci = 0, deleting = false;
const el = document.getElementById('typing-text');
function type() {
  const word = lines[li];
  if (!deleting) {
    el.textContent = word.slice(0, ++ci);
    if (ci === word.length) { deleting = true; setTimeout(type, 2200); return; }
  } else {
    el.textContent = word.slice(0, --ci);
    if (ci === 0) { deleting = false; li = (li + 1) % lines.length; }
  }
  setTimeout(type, deleting ? 45 : 75);
}
setTimeout(type, 600);

// ── SCROLL REVEAL ──
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      // skill bars
      e.target.querySelectorAll('.bar-fill').forEach(b => {
        b.style.width = b.dataset.width + '%';
      });
      // counters
      e.target.querySelectorAll('[data-count]').forEach(el => {
        const target = parseInt(el.dataset.count);
        let cur2 = 0;
        const step = Math.ceil(target / 40);
        const iv = setInterval(() => {
          cur2 = Math.min(cur2 + step, target);
          el.textContent = cur2 + '+';
          if (cur2 >= target) clearInterval(iv);
        }, 40);
      });
    }
  });
}, { threshold: 0.15 });

document.querySelectorAll('.section').forEach(s => observer.observe(s));
</script>
</body>
</html>
