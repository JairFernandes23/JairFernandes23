<!DOCTYPE html>
<html lang="pt">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Jair Fernandes · Full Stack Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,400;0,500;0,700;1,400&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --green:   #3fb950;
    --blue:    #58A6FF;
    --orange:  #f78166;
    --yellow:  #e3b341;
    --purple:  #bc8cff;
    --red:     #ff7b7b;
    --bg0:     #0d1117;
    --bg1:     #161b22;
    --bg2:     #21262d;
    --bg3:     #2d333b;
    --border:  #30363d;
    --text:    #c9d1d9;
    --muted:   #8b949e;
    --white:   #f0f6fc;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'JetBrains Mono', monospace;
    background: var(--bg0);
    color: var(--text);
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    width: 12px; height: 12px;
    border: 1.5px solid var(--blue);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.1s, opacity 0.2s;
    transform: translate(-50%, -50%);
  }
  .cursor-dot {
    width: 4px; height: 4px;
    background: var(--blue);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
  }

  /* SCANLINE OVERLAY */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.03) 2px,
      rgba(0,0,0,0.03) 4px
    );
    pointer-events: none;
    z-index: 1000;
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 56px;
    background: rgba(13,17,23,0.85);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 40px;
    z-index: 100;
  }

  .nav-logo {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 18px;
    color: var(--white);
    text-decoration: none;
  }

  .nav-logo span { color: var(--blue); }

  .nav-links {
    display: flex;
    gap: 32px;
    list-style: none;
  }

  .nav-links a {
    font-size: 12px;
    color: var(--muted);
    text-decoration: none;
    transition: color 0.2s;
    position: relative;
  }

  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -4px; left: 0; right: 0;
    height: 1px;
    background: var(--blue);
    transform: scaleX(0);
    transition: transform 0.2s;
  }

  .nav-links a:hover { color: var(--blue); }
  .nav-links a:hover::after { transform: scaleX(1); }

  .nav-status {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 11px;
    color: var(--green);
  }

  .pulse {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--green);
    animation: pulse 2s infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; box-shadow: 0 0 0 0 rgba(63,185,80,0.4); }
    50% { opacity: 0.6; box-shadow: 0 0 0 6px rgba(63,185,80,0); }
  }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    padding: 80px 40px 40px;
    position: relative;
    overflow: hidden;
  }

  .hero-grid {
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(88,166,255,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(88,166,255,0.04) 1px, transparent 1px);
    background-size: 48px 48px;
    animation: gridScroll 20s linear infinite;
  }

  @keyframes gridScroll {
    0% { transform: translateY(0); }
    100% { transform: translateY(48px); }
  }

  .hero-glow {
    position: absolute;
    top: 20%; left: 50%;
    transform: translate(-50%, -50%);
    width: 600px; height: 400px;
    background: radial-gradient(ellipse, rgba(88,166,255,0.07) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-content {
    max-width: 900px;
    margin: 0 auto;
    width: 100%;
    position: relative;
    z-index: 1;
  }

  .hero-tag {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(88,166,255,0.08);
    border: 1px solid rgba(88,166,255,0.2);
    border-radius: 20px;
    padding: 6px 14px;
    font-size: 11px;
    color: var(--blue);
    margin-bottom: 28px;
    animation: fadeUp 0.6s ease forwards;
    opacity: 0;
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(40px, 7vw, 80px);
    font-weight: 800;
    line-height: 1;
    color: var(--white);
    margin-bottom: 8px;
    animation: fadeUp 0.6s 0.1s ease forwards;
    opacity: 0;
  }

  .hero-name .accent { color: var(--blue); }

  .hero-role {
    font-size: clamp(14px, 2vw, 18px);
    color: var(--muted);
    margin-bottom: 32px;
    animation: fadeUp 0.6s 0.2s ease forwards;
    opacity: 0;
  }

  .typing-line {
    font-size: 14px;
    color: var(--green);
    margin-bottom: 40px;
    min-height: 20px;
    animation: fadeUp 0.6s 0.3s ease forwards;
    opacity: 0;
  }

  .typing-cursor-blink {
    display: inline-block;
    width: 9px; height: 16px;
    background: var(--green);
    vertical-align: middle;
    animation: blink 1s steps(1) infinite;
    margin-left: 2px;
  }

  @keyframes blink { 0%,49% { opacity: 1; } 50%,100% { opacity: 0; } }

  .hero-btns {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
    animation: fadeUp 0.6s 0.4s ease forwards;
    opacity: 0;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 12px 24px;
    border-radius: 8px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    font-weight: 500;
    text-decoration: none;
    cursor: pointer;
    transition: all 0.2s;
    border: none;
  }

  .btn-primary {
    background: var(--blue);
    color: #0d1117;
  }
  .btn-primary:hover { background: #79b8ff; transform: translateY(-2px); }

  .btn-secondary {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
  }
  .btn-secondary:hover { border-color: var(--blue); color: var(--blue); transform: translateY(-2px); }

  .hero-scroll {
    position: absolute;
    bottom: 32px; left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    font-size: 10px;
    color: var(--muted);
    animation: bounce 2s ease infinite;
  }

  @keyframes bounce {
    0%,100% { transform: translateX(-50%) translateY(0); }
    50% { transform: translateX(-50%) translateY(6px); }
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* SECTIONS */
  section {
    padding: 80px 40px;
    max-width: 960px;
    margin: 0 auto;
  }

  .section-header {
    display: flex;
    align-items: center;
    gap: 16px;
    margin-bottom: 48px;
  }

  .section-num {
    font-size: 11px;
    color: var(--blue);
    font-weight: 500;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: 28px;
    font-weight: 800;
    color: var(--white);
  }

  .section-line {
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* ABOUT */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 32px;
  }

  .terminal-block {
    background: var(--bg1);
    border: 1px solid var(--border);
    border-radius: 10px;
    overflow: hidden;
  }

  .terminal-header {
    background: var(--bg2);
    padding: 10px 16px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-bottom: 1px solid var(--border);
  }

  .win-btn {
    width: 11px; height: 11px;
    border-radius: 50%;
  }
  .win-red { background: #ff5f57; }
  .win-yellow { background: #febc2e; }
  .win-green { background: #28c840; }

  .terminal-filename {
    flex: 1;
    text-align: center;
    font-size: 11px;
    color: var(--muted);
  }

  .terminal-body {
    padding: 20px;
    font-size: 12.5px;
    line-height: 2;
  }

  .kw { color: var(--purple); }
  .key { color: var(--blue); }
  .str { color: var(--green); }
  .arr-item { color: var(--orange); }
  .bracket { color: var(--yellow); }
  .cm { color: var(--muted); font-style: italic; }
  .prompt-sym { color: var(--green); user-select: none; }

  .about-info {
    display: flex;
    flex-direction: column;
    gap: 16px;
    justify-content: center;
  }

  .info-item {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 14px;
    background: var(--bg1);
    border: 1px solid var(--border);
    border-radius: 8px;
    transition: border-color 0.2s;
  }

  .info-item:hover { border-color: var(--blue); }

  .info-icon {
    font-size: 18px;
    flex-shrink: 0;
    margin-top: 2px;
  }

  .info-label {
    font-size: 10px;
    color: var(--muted);
    margin-bottom: 3px;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  .info-val { font-size: 13px; color: var(--text); }

  /* SKILLS */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }

  .skill-category {
    background: var(--bg1);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 20px;
    transition: border-color 0.2s, transform 0.2s;
  }

  .skill-category:hover {
    border-color: var(--blue);
    transform: translateY(-4px);
  }

  .skill-cat-title {
    font-size: 11px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 1.5px;
    margin-bottom: 16px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--border);
  }

  .skill-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 14px;
  }

  .skill-name-wrap {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .skill-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    flex-shrink: 0;
  }

  .skill-name { font-size: 12px; color: var(--text); }

  .skill-bar-wrap {
    width: 70px;
    height: 3px;
    background: var(--bg2);
    border-radius: 2px;
    overflow: hidden;
  }

  .skill-bar {
    height: 100%;
    border-radius: 2px;
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.8s ease;
  }

  .skill-bar.animated { transform: scaleX(1); }

  /* PROJECTS */
  .projects-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  .project-card {
    background: var(--bg1);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 24px;
    transition: all 0.25s;
    position: relative;
    overflow: hidden;
    cursor: default;
  }

  .project-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--blue), var(--purple));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.3s;
  }

  .project-card:hover {
    border-color: rgba(88,166,255,0.4);
    transform: translateY(-4px);
  }

  .project-card:hover::before { transform: scaleX(1); }

  .project-card.featured {
    grid-column: 1 / -1;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
    align-items: center;
  }

  .project-card.featured::before {
    height: 3px;
  }

  .project-tag {
    display: inline-block;
    padding: 3px 10px;
    border-radius: 20px;
    font-size: 10px;
    margin-bottom: 12px;
    background: rgba(88,166,255,0.1);
    color: var(--blue);
    border: 1px solid rgba(88,166,255,0.2);
  }

  .project-name {
    font-family: 'Syne', sans-serif;
    font-size: 18px;
    font-weight: 700;
    color: var(--white);
    margin-bottom: 8px;
  }

  .project-desc {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.8;
    margin-bottom: 16px;
  }

  .project-tech {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }

  .tech-pill {
    padding: 3px 10px;
    border-radius: 4px;
    font-size: 10px;
    background: var(--bg2);
    color: var(--muted);
    border: 1px solid var(--border);
  }

  .project-visual {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 20px;
    font-size: 11px;
    line-height: 2;
    color: var(--muted);
  }

  /* CONTACT */
  .contact-wrap {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
    align-items: start;
  }

  .contact-text h3 {
    font-family: 'Syne', sans-serif;
    font-size: 22px;
    font-weight: 800;
    color: var(--white);
    margin-bottom: 16px;
  }

  .contact-text p {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.9;
    margin-bottom: 24px;
  }

  .contact-links {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .contact-link {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 14px 16px;
    background: var(--bg1);
    border: 1px solid var(--border);
    border-radius: 8px;
    text-decoration: none;
    color: var(--text);
    font-size: 13px;
    transition: all 0.2s;
  }

  .contact-link:hover {
    border-color: var(--blue);
    color: var(--blue);
    transform: translateX(4px);
  }

  .contact-link-icon {
    width: 32px; height: 32px;
    border-radius: 6px;
    background: var(--bg2);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
    flex-shrink: 0;
  }

  /* contact form */
  .contact-form {
    background: var(--bg1);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 28px;
  }

  .form-group { margin-bottom: 16px; }

  .form-label {
    display: block;
    font-size: 11px;
    color: var(--muted);
    margin-bottom: 6px;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  .form-input, .form-textarea {
    width: 100%;
    background: var(--bg0);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 10px 14px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: var(--text);
    transition: border-color 0.2s;
    outline: none;
  }

  .form-input:focus, .form-textarea:focus {
    border-color: var(--blue);
  }

  .form-textarea { height: 100px; resize: none; }

  .form-btn {
    width: 100%;
    padding: 12px;
    background: var(--blue);
    color: #0d1117;
    border: none;
    border-radius: 6px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.2s;
  }

  .form-btn:hover { background: #79b8ff; transform: translateY(-1px); }

  /* FOOTER */
  footer {
    border-top: 1px solid var(--border);
    padding: 32px 40px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    max-width: 100%;
  }

  .footer-copy {
    font-size: 11px;
    color: var(--muted);
  }

  .footer-copy span { color: var(--blue); }

  .footer-links {
    display: flex;
    gap: 20px;
  }

  .footer-links a {
    font-size: 11px;
    color: var(--muted);
    text-decoration: none;
    transition: color 0.2s;
  }

  .footer-links a:hover { color: var(--blue); }

  /* STATS BAR */
  .stats-bar {
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    background: var(--bg1);
    padding: 0;
    overflow: hidden;
  }

  .stats-inner {
    max-width: 960px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
  }

  .stat-item {
    padding: 28px 32px;
    border-right: 1px solid var(--border);
    text-align: center;
    transition: background 0.2s;
  }

  .stat-item:last-child { border-right: none; }
  .stat-item:hover { background: rgba(88,166,255,0.03); }

  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 36px;
    font-weight: 800;
    color: var(--blue);
    display: block;
  }

  .stat-lbl {
    font-size: 11px;
    color: var(--muted);
    margin-top: 4px;
    display: block;
  }

  /* SCROLL REVEAL */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }

  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* RESPONSIVE */
  @media (max-width: 720px) {
    nav { padding: 0 20px; }
    .nav-links { display: none; }
    section { padding: 60px 20px; }
    .hero { padding: 80px 20px 60px; }
    .about-grid, .skills-grid, .projects-grid,
    .contact-wrap, .stats-inner { grid-template-columns: 1fr; }
    .project-card.featured { grid-column: auto; display: block; }
    .project-visual { display: none; }
    footer { flex-direction: column; gap: 16px; text-align: center; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-dot" id="cursorDot"></div>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">Jair<span>.</span>dev</a>
  <ul class="nav-links">
    <li><a href="#sobre">sobre</a></li>
    <li><a href="#skills">skills</a></li>
    <li><a href="#projetos">projetos</a></li>
    <li><a href="#contato">contato</a></li>
  </ul>
  <div class="nav-status">
    <div class="pulse"></div>
    aberto a oportunidades
  </div>
</nav>

<!-- HERO -->
<div class="hero">
  <div class="hero-grid"></div>
  <div class="hero-glow"></div>
  <div class="hero-content">
    <div class="hero-tag">
      <div style="width:7px;height:7px;border-radius:50%;background:var(--green);"></div>
      Luanda, Angola 🇦🇴 · Full Stack Developer
    </div>
    <h1 class="hero-name">JAIR<br><span class="accent">FERNANDES</span></h1>
    <p class="hero-role">Full Stack Developer &amp; Técnico de Informática</p>
    <div class="typing-line" id="typingLine">
      <span id="typingText"></span><span class="typing-cursor-blink"></span>
    </div>
    <div class="hero-btns">
      <a href="#projetos" class="btn btn-primary">ver projetos →</a>
      <a href="#contato" class="btn btn-secondary">entrar em contato</a>
      <a href="https://github.com/JairFernandes23" target="_blank" class="btn btn-secondary">GitHub ↗</a>
    </div>
  </div>
  <div class="hero-scroll">
    <span>scroll</span>
    <svg width="12" height="20" viewBox="0 0 12 20" fill="none">
      <rect x="1" y="1" width="10" height="18" rx="5" stroke="#8b949e" stroke-width="1.5"/>
      <rect x="4.5" y="4" width="3" height="5" rx="1.5" fill="#8b949e"/>
    </svg>
  </div>
</div>

<!-- STATS BAR -->
<div class="stats-bar reveal">
  <div class="stats-inner">
    <div class="stat-item">
      <span class="stat-num">13</span>
      <span class="stat-lbl">Repositórios</span>
    </div>
    <div class="stat-item">
      <span class="stat-num">5+</span>
      <span class="stat-lbl">Tecnologias</span>
    </div>
    <div class="stat-item">
      <span class="stat-num">2+</span>
      <span class="stat-lbl">Anos de experiência</span>
    </div>
    <div class="stat-item">
      <span class="stat-num">100%</span>
      <span class="stat-lbl">Open to Work</span>
    </div>
  </div>
</div>

<!-- SOBRE -->
<section id="sobre">
  <div class="section-header reveal">
    <span class="section-num">01.</span>
    <h2 class="section-title">sobre mim</h2>
    <div class="section-line"></div>
  </div>
  <div class="about-grid reveal">
    <div class="terminal-block">
      <div class="terminal-header">
        <div class="win-btn win-red"></div>
        <div class="win-btn win-yellow"></div>
        <div class="win-btn win-green"></div>
        <div class="terminal-filename">dev.py</div>
      </div>
      <div class="terminal-body">
        <div><span class="kw">dev</span> <span style="color:var(--muted)">=</span> <span class="bracket">{</span></div>
        <div style="padding-left:20px"><span class="key">"nome"</span><span style="color:var(--muted)">:</span> <span class="str">"Jair Fernandes de Campos"</span><span style="color:var(--muted)">,</span></div>
        <div style="padding-left:20px"><span class="key">"role"</span><span style="color:var(--muted)">:</span> <span class="str">"Full Stack Developer"</span><span style="color:var(--muted)">,</span></div>
        <div style="padding-left:20px"><span class="key">"localização"</span><span style="color:var(--muted)">:</span> <span class="str">"Luanda, Angola 🇦🇴"</span><span style="color:var(--muted)">,</span></div>
        <div style="padding-left:20px"><span class="key">"stack"</span><span style="color:var(--muted)">:</span> <span class="bracket">[</span></div>
        <div style="padding-left:40px"><span class="arr-item">"PHP"</span><span style="color:var(--muted)">,</span> <span class="arr-item">"HTML5"</span><span style="color:var(--muted)">,</span> <span class="arr-item">"CSS3"</span><span style="color:var(--muted)">,</span></div>
        <div style="padding-left:40px"><span class="arr-item">"Python"</span><span style="color:var(--muted)">,</span> <span class="arr-item">"MySQL"</span></div>
        <div style="padding-left:20px"><span class="bracket">]</span><span style="color:var(--muted)">,</span></div>
        <div style="padding-left:20px"><span class="key">"foco"</span><span style="color:var(--muted)">:</span> <span class="str">"Soluções web robustas"</span></div>
        <div><span class="bracket">}</span></div>
        <div style="margin-top:12px"><span class="prompt-sym">$</span> <span style="color:var(--text)">python dev.py<span class="typing-cursor-blink"></span></span></div>
        <div style="color:var(--green);margin-top:4px;">→ Pronto para novos desafios! ✓</div>
      </div>
    </div>

    <div class="about-info">
      <div class="info-item">
        <div class="info-icon">📍</div>
        <div>
          <div class="info-label">Localização</div>
          <div class="info-val">Luanda, Angola</div>
        </div>
      </div>
      <div class="info-item">
        <div class="info-icon">💼</div>
        <div>
          <div class="info-label">Função</div>
          <div class="info-val">Full Stack Developer & Técnico de TI</div>
        </div>
      </div>
      <div class="info-item">
        <div class="info-icon">🛠️</div>
        <div>
          <div class="info-label">Especialidades</div>
          <div class="info-val">Redes LAN/Wi-Fi · Manutenção de hardware · Suporte técnico</div>
        </div>
      </div>
      <div class="info-item">
        <div class="info-icon">🎯</div>
        <div>
          <div class="info-label">Objetivo</div>
          <div class="info-val">Criar soluções web robustas e eficientes</div>
        </div>
      </div>
      <div class="info-item" style="border-color: rgba(63,185,80,0.3); background: rgba(63,185,80,0.04);">
        <div class="info-icon">✅</div>
        <div>
          <div class="info-label" style="color: var(--green);">Disponibilidade</div>
          <div class="info-val" style="color: var(--green);">Aberto a oportunidades</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="section-header reveal">
    <span class="section-num">02.</span>
    <h2 class="section-title">tech stack</h2>
    <div class="section-line"></div>
  </div>
  <div class="skills-grid reveal">
    <div class="skill-category">
      <div class="skill-cat-title">Web & Backend</div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#777BB4;"></div>
          <span class="skill-name">PHP</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#777BB4; width:85%;"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#E34F26;"></div>
          <span class="skill-name">HTML5</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#E34F26; width:92%;"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#264DE4;"></div>
          <span class="skill-name">CSS3</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#264DE4; width:88%;"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#3572A5;"></div>
          <span class="skill-name">Python</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#3572A5; width:78%;"></div></div>
      </div>
    </div>

    <div class="skill-category">
      <div class="skill-cat-title">Base de Dados</div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#4479A1;"></div>
          <span class="skill-name">MySQL</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#4479A1; width:82%;"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#336791;"></div>
          <span class="skill-name">SQL</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#336791; width:80%;"></div></div>
      </div>
      <div class="skill-cat-title" style="margin-top:16px;">Ferramentas</div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#F05032;"></div>
          <span class="skill-name">Git</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#F05032; width:75%;"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#f0f6fc;"></div>
          <span class="skill-name">GitHub</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#f0f6fc; width:78%;"></div></div>
      </div>
    </div>

    <div class="skill-category">
      <div class="skill-cat-title">Infraestrutura & TI</div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#0078D6;"></div>
          <span class="skill-name">Windows</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#0078D6; width:90%;"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#FCC624;"></div>
          <span class="skill-name">Linux</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#FCC624; width:70%;"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#00B4D8;"></div>
          <span class="skill-name">Redes LAN/Wi-Fi</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#00B4D8; width:82%;"></div></div>
      </div>
      <div class="skill-item">
        <div class="skill-name-wrap">
          <div class="skill-dot" style="background:#888;"></div>
          <span class="skill-name">Manutenção HW</span>
        </div>
        <div class="skill-bar-wrap"><div class="skill-bar" style="background:#888; width:85%;"></div></div>
      </div>
    </div>
  </div>
</section>

<!-- PROJETOS -->
<section id="projetos">
  <div class="section-header reveal">
    <span class="section-num">03.</span>
    <h2 class="section-title">projetos</h2>
    <div class="section-line"></div>
  </div>
  <div class="projects-grid reveal">

    <div class="project-card featured">
      <div>
        <div class="project-tag">⭐ Projeto Principal</div>
        <div class="project-name">JFStore Admin</div>
        <div class="project-desc">Painel administrativo completo para gestão de loja online. Sistema de autenticação, gestão de produtos, pedidos e relatórios. Interface responsiva construída com PHP e MySQL com painel intuitivo para gestão do negócio.</div>
        <div class="project-tech">
          <span class="tech-pill">PHP</span>
          <span class="tech-pill">MySQL</span>
          <span class="tech-pill">HTML5</span>
          <span class="tech-pill">CSS3</span>
          <span class="tech-pill">JavaScript</span>
        </div>
      </div>
      <div class="project-visual">
        <div style="color:var(--blue);margin-bottom:8px;"># admin/dashboard.php</div>
        <div><span style="color:var(--purple);">$auth</span> = <span style="color:var(--orange);">new</span> Auth();</div>
        <div><span style="color:var(--purple);">$db</span> = <span style="color:var(--orange);">new</span> Database();</div>
        <div style="margin-top:8px;"><span style="color:var(--purple);">$stats</span> = [</div>
        <div style="padding-left:16px;"><span style="color:var(--green);">"vendas"</span> => <span style="color:var(--blue);">fetchSales</span>(),</div>
        <div style="padding-left:16px;"><span style="color:var(--green);">"stock"</span> => <span style="color:var(--blue);">fetchStock</span>(),</div>
        <div>];</div>
        <div style="margin-top:8px;color:var(--green);">→ Sistema online ✓</div>
      </div>
    </div>

    <div class="project-card">
      <div class="project-tag">Web</div>
      <div class="project-name">Portfólio Web</div>
      <div class="project-desc">Site portfólio pessoal responsivo com design moderno. Apresentação de projetos e competências.</div>
      <div class="project-tech">
        <span class="tech-pill">HTML5</span>
        <span class="tech-pill">CSS3</span>
        <span class="tech-pill">JavaScript</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-tag">Python</div>
      <div class="project-name">Network Tools</div>
      <div class="project-desc">Scripts de diagnóstico de redes LAN/Wi-Fi. Ferramentas para análise e troubleshooting de redes.</div>
      <div class="project-tech">
        <span class="tech-pill">Python</span>
        <span class="tech-pill">Networking</span>
        <span class="tech-pill">CLI</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-tag">PHP + MySQL</div>
      <div class="project-name">CRUD System</div>
      <div class="project-desc">Sistema CRUD genérico com PHP e MySQL, pronto a reutilizar em qualquer projeto web.</div>
      <div class="project-tech">
        <span class="tech-pill">PHP</span>
        <span class="tech-pill">MySQL</span>
        <span class="tech-pill">HTML5</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-tag">TI & Suporte</div>
      <div class="project-name">Suporte Técnico</div>
      <div class="project-desc">Experiência em manutenção de hardware, configuração de redes e suporte ao utilizador em ambiente empresarial.</div>
      <div class="project-tech">
        <span class="tech-pill">Hardware</span>
        <span class="tech-pill">LAN/Wi-Fi</span>
        <span class="tech-pill">Windows</span>
        <span class="tech-pill">Linux</span>
      </div>
    </div>

  </div>
  <div style="text-align:center; margin-top: 32px;">
    <a href="https://github.com/JairFernandes23" target="_blank" class="btn btn-secondary">ver todos os repos no GitHub ↗</a>
  </div>
</section>

<!-- CONTACT -->
<section id="contato">
  <div class="section-header reveal">
    <span class="section-num">04.</span>
    <h2 class="section-title">contato</h2>
    <div class="section-line"></div>
  </div>
  <div class="contact-wrap reveal">
    <div class="contact-text">
      <h3>Vamos trabalhar juntos?</h3>
      <p>Estou sempre aberto a novas oportunidades, projetos freelance ou simplesmente para trocar ideias sobre tecnologia. Se tens um projeto em mente ou uma oportunidade de trabalho, entra em contacto!</p>
      <div class="contact-links">
        <a href="https://github.com/JairFernandes23" target="_blank" class="contact-link">
          <div class="contact-link-icon">GH</div>
          <span>github.com/JairFernandes23</span>
        </a>
        <div class="contact-link">
          <div class="contact-link-icon">📍</div>
          <span>Luanda, Angola 🇦🇴</span>
        </div>
        <div class="contact-link" style="border-color: rgba(63,185,80,0.3); color: var(--green);">
          <div class="contact-link-icon">✅</div>
          <span>Disponível para trabalho</span>
        </div>
      </div>
    </div>

    <div class="contact-form">
      <div class="form-group">
        <label class="form-label">Nome</label>
        <input type="text" class="form-input" placeholder="O teu nome">
      </div>
      <div class="form-group">
        <label class="form-label">Email</label>
        <input type="email" class="form-input" placeholder="email@exemplo.com">
      </div>
      <div class="form-group">
        <label class="form-label">Mensagem</label>
        <textarea class="form-textarea" placeholder="Olá Jair, tenho um projeto..."></textarea>
      </div>
      <button class="form-btn" onclick="sendMsg(this)">enviar mensagem →</button>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-copy">
    © 2025 <span>Jair Fernandes de Campos</span> · Luanda, Angola 🇦🇴
  </div>
  <div class="footer-links">
    <a href="https://github.com/JairFernandes23" target="_blank">GitHub</a>
    <a href="#sobre">Sobre</a>
    <a href="#projetos">Projetos</a>
    <a href="#contato">Contato</a>
  </div>
</footer>

<script>
// Cursor
const cursor = document.getElementById('cursor');
const dot = document.getElementById('cursorDot');
let mx=0,my=0,cx=0,cy=0;
document.addEventListener('mousemove', e => { mx=e.clientX; my=e.clientY; dot.style.left=mx+'px'; dot.style.top=my+'px'; });
function animCursor() {
  cx += (mx-cx)*0.12; cy += (my-cy)*0.12;
  cursor.style.left = cx+'px'; cursor.style.top = cy+'px';
  requestAnimationFrame(animCursor);
}
animCursor();
document.querySelectorAll('a,button,.project-card,.contact-link').forEach(el => {
  el.addEventListener('mouseenter', () => { cursor.style.transform='translate(-50%,-50%) scale(1.8)'; cursor.style.borderColor='var(--green)'; });
  el.addEventListener('mouseleave', () => { cursor.style.transform='translate(-50%,-50%) scale(1)'; cursor.style.borderColor='var(--blue)'; });
});

// Typing hero
const phrases = [
  'Criar soluções web robustas e eficientes...',
  'PHP | HTML5 | CSS3 | Python | MySQL',
  'Suporte técnico · Redes LAN · Hardware',
  'Aberto a novas oportunidades 🚀'
];
let pi=0, ci=0, deleting=false;
const el = document.getElementById('typingText');
function typeLoop() {
  const phrase = phrases[pi];
  if (!deleting) {
    el.textContent = phrase.slice(0, ci++);
    if (ci > phrase.length) { deleting=true; setTimeout(typeLoop, 1800); return; }
  } else {
    el.textContent = phrase.slice(0, ci--);
    if (ci < 0) { deleting=false; pi=(pi+1)%phrases.length; ci=0; }
  }
  setTimeout(typeLoop, deleting ? 40 : 65);
}
setTimeout(typeLoop, 800);

// Scroll reveal
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      // animate skill bars
      e.target.querySelectorAll('.skill-bar').forEach(b => b.classList.add('animated'));
    }
  });
}, { threshold: 0.1 });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

// Form submit
function sendMsg(btn) {
  btn.textContent = 'mensagem enviada! ✓';
  btn.style.background = 'var(--green)';
  setTimeout(() => { btn.textContent = 'enviar mensagem →'; btn.style.background=''; }, 3000);
}
</script>
</body>
</html>
