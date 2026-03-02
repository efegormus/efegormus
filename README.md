<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>efegormus / efegormus</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300;0,400;0,600;1,300&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0d1117;
    --canvas: #161b22;
    --border: #30363d;
    --border-light: #21262d;
    --text: #c9d1d9;
    --muted: #8b949e;
    --bright: #f0f6fc;
    --green: #3fb950;
    --blue: #58a6ff;
    --orange: #d29922;
    --pink: #f47067;
    --purple: #bc8cff;
    --teal: #39d353;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    min-height: 100vh;
    padding: 0;
  }

  /* ── REPO HEADER BAR ── */
  .repo-bar {
    background: var(--canvas);
    border-bottom: 1px solid var(--border);
    padding: 12px 24px;
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 13px;
    color: var(--muted);
    position: sticky;
    top: 0;
    z-index: 10;
  }

  .repo-bar .breadcrumb {
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .repo-bar .breadcrumb a {
    color: var(--blue);
    text-decoration: none;
    font-weight: 600;
  }
  .repo-bar .breadcrumb a:hover { text-decoration: underline; }
  .repo-bar .breadcrumb .sep { color: var(--border); }

  .repo-badge {
    font-size: 11px;
    padding: 1px 8px;
    border: 1px solid var(--border);
    border-radius: 999px;
    color: var(--muted);
    margin-left: 6px;
  }

  .repo-bar-right {
    margin-left: auto;
    display: flex;
    gap: 8px;
  }

  .gh-btn {
    font-size: 11px;
    padding: 4px 12px;
    border: 1px solid var(--border);
    border-radius: 6px;
    background: var(--canvas);
    color: var(--text);
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 5px;
    transition: background 0.15s, border-color 0.15s;
  }
  .gh-btn:hover { background: #1c2128; border-color: #8b949e; }

  /* ── LAYOUT ── */
  .layout {
    display: grid;
    grid-template-columns: 1fr 296px;
    gap: 0;
    max-width: 1280px;
    margin: 0 auto;
    padding: 24px 24px;
    align-items: start;
  }

  /* ── README PANEL ── */
  .readme-panel {
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
  }

  .readme-header {
    background: var(--canvas);
    border-bottom: 1px solid var(--border);
    padding: 10px 16px;
    font-size: 12px;
    color: var(--muted);
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .readme-header svg { width: 14px; height: 14px; fill: var(--muted); }

  .readme-body {
    padding: 32px 40px 40px;
    background: var(--bg);
    animation: fadeIn 0.5s ease both;
  }

  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

  /* ── MARKDOWN ELEMENTS ── */
  .md-wave {
    font-size: 48px;
    margin-bottom: 4px;
    display: block;
    animation: wave 2s ease-in-out infinite;
    transform-origin: 70% 70%;
    display: inline-block;
  }
  @keyframes wave {
    0%, 100% { transform: rotate(0deg); }
    20% { transform: rotate(14deg); }
    40% { transform: rotate(-8deg); }
    60% { transform: rotate(14deg); }
    80% { transform: rotate(-4deg); }
  }

  .md-h1 {
    font-family: 'Instrument Serif', serif;
    font-size: 36px;
    color: var(--bright);
    font-weight: 400;
    margin-bottom: 6px;
    line-height: 1.2;
  }

  .md-h1 em { font-style: italic; color: var(--blue); }

  .md-subtitle {
    font-size: 13px;
    color: var(--muted);
    margin-bottom: 28px;
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    align-items: center;
  }

  .md-badge {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    font-size: 11px;
    padding: 3px 10px;
    border-radius: 4px;
    font-weight: 600;
    letter-spacing: 0.02em;
  }

  .badge-green  { background: rgba(63,185,80,0.15);  color: var(--green);  border: 1px solid rgba(63,185,80,0.3); }
  .badge-blue   { background: rgba(88,166,255,0.12); color: var(--blue);   border: 1px solid rgba(88,166,255,0.25); }
  .badge-purple { background: rgba(188,140,255,0.12); color: var(--purple); border: 1px solid rgba(188,140,255,0.25); }
  .badge-orange { background: rgba(210,153,34,0.15); color: var(--orange); border: 1px solid rgba(210,153,34,0.3); }

  .md-divider {
    border: none;
    border-top: 1px solid var(--border-light);
    margin: 28px 0;
  }

  .md-h2 {
    font-size: 20px;
    color: var(--bright);
    font-weight: 600;
    margin-bottom: 16px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--border-light);
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .md-h3 {
    font-size: 15px;
    color: var(--bright);
    font-weight: 600;
    margin-bottom: 10px;
    margin-top: 20px;
  }

  .md-p {
    font-size: 13px;
    line-height: 1.85;
    color: var(--text);
    margin-bottom: 14px;
  }

  .md-p code, .inline-code {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    background: rgba(110,118,129,0.15);
    padding: 2px 6px;
    border-radius: 4px;
    color: var(--pink);
    border: 1px solid rgba(110,118,129,0.2);
  }

  /* ── TYPING ANIMATION ── */
  .typing-wrap {
    font-size: 13px;
    color: var(--muted);
    margin-bottom: 28px;
  }

  .typing-cursor::after {
    content: '|';
    color: var(--green);
    animation: blink 1s step-end infinite;
  }
  @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

  /* ── SKILL ICONS ROW ── */
  .skills-row {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 8px;
  }

  .skill-chip {
    font-size: 12px;
    padding: 5px 14px;
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--text);
    background: var(--canvas);
    display: flex;
    align-items: center;
    gap: 6px;
    transition: all 0.15s;
    cursor: default;
  }

  .skill-chip:hover { border-color: var(--blue); color: var(--blue); background: rgba(88,166,255,0.05); }

  .skill-chip .dot {
    width: 6px; height: 6px; border-radius: 50%; flex-shrink: 0;
  }
  .dot-cpp    { background: #f34b7d; }
  .dot-py     { background: #3572A5; }
  .dot-html   { background: #e34c26; }
  .dot-ml     { background: var(--purple); }
  .dot-ds     { background: var(--teal); }
  .dot-sys    { background: var(--orange); }
  .dot-algo   { background: var(--blue); }

  /* ── PROJECT CARDS ── */
  .project-card {
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 18px 20px;
    margin-bottom: 12px;
    background: var(--canvas);
    transition: border-color 0.2s, background 0.2s;
    cursor: default;
  }
  .project-card:hover { border-color: #58a6ff55; background: #1c2128; }

  .project-top {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 8px;
    gap: 12px;
  }

  .project-name-row {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .project-icon { font-size: 16px; }

  .project-title {
    font-size: 14px;
    font-weight: 600;
    color: var(--blue);
  }

  .project-desc {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.7;
    margin-bottom: 12px;
  }

  .project-footer {
    display: flex;
    align-items: center;
    gap: 14px;
    font-size: 11px;
    color: var(--muted);
  }

  .project-lang {
    display: flex;
    align-items: center;
    gap: 5px;
  }

  .project-star { color: var(--orange); }

  /* ── CONTRIBUTION GRAPH ── */
  .contrib-section { margin-top: 6px; }

  .contrib-grid {
    display: grid;
    grid-template-columns: repeat(52, 1fr);
    gap: 3px;
    overflow: hidden;
  }

  .contrib-cell {
    aspect-ratio: 1;
    border-radius: 2px;
    background: #161b22;
    border: 1px solid rgba(0,0,0,0.3);
    transition: transform 0.1s;
    cursor: default;
  }

  .contrib-cell:hover { transform: scale(1.4); z-index: 1; }

  .c0 { background: #161b22; }
  .c1 { background: #0e4429; }
  .c2 { background: #006d32; }
  .c3 { background: #26a641; }
  .c4 { background: #39d353; }

  .contrib-label {
    display: flex;
    justify-content: space-between;
    font-size: 10px;
    color: var(--muted);
    margin-bottom: 6px;
  }

  /* ── SIDEBAR ── */
  .sidebar {
    padding-left: 16px;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .side-card {
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 16px;
    background: var(--canvas);
    animation: fadeIn 0.6s ease both;
  }

  .side-card-title {
    font-size: 12px;
    font-weight: 600;
    color: var(--bright);
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .side-stat-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .side-stat {
    text-align: center;
    padding: 10px;
    background: var(--bg);
    border-radius: 4px;
    border: 1px solid var(--border-light);
  }

  .side-stat-n {
    font-family: 'Instrument Serif', serif;
    font-size: 24px;
    color: var(--bright);
    display: block;
  }

  .side-stat-l {
    font-size: 10px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.08em;
  }

  .side-link {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12px;
    color: var(--muted);
    text-decoration: none;
    padding: 6px 0;
    border-bottom: 1px solid var(--border-light);
    transition: color 0.15s;
  }
  .side-link:last-child { border-bottom: none; }
  .side-link:hover { color: var(--blue); }

  .side-link-icon { font-size: 13px; min-width: 18px; }

  .location-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12px;
    color: var(--muted);
    padding: 4px 0;
  }

  .avail-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    background: var(--green);
    animation: pulse 2s ease infinite;
    flex-shrink: 0;
  }
  @keyframes pulse { 0%,100%{box-shadow:0 0 0 0 rgba(63,185,80,0.4)} 50%{box-shadow:0 0 0 5px rgba(63,185,80,0)} }

  .trophy-row {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .trophy-item {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 12px;
    padding: 8px 10px;
    background: var(--bg);
    border-radius: 4px;
    border: 1px solid var(--border-light);
    color: var(--text);
    transition: border-color 0.15s;
  }
  .trophy-item:hover { border-color: var(--orange); }
  .trophy-item .trophy-icon { font-size: 16px; }
  .trophy-item .trophy-sub { font-size: 10px; color: var(--muted); margin-top: 1px; }
  .trophy-meta { display: flex; flex-direction: column; }

  /* ── FOOTER ── */
  .readme-footer {
    padding: 14px 40px 20px;
    background: var(--bg);
    border-top: 1px solid var(--border-light);
    font-size: 11px;
    color: var(--muted);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .readme-footer em {
    font-family: 'Instrument Serif', serif;
    font-style: italic;
    font-size: 13px;
    color: var(--text);
  }

  @media (max-width: 900px) {
    .layout { grid-template-columns: 1fr; padding: 16px; }
    .sidebar { padding-left: 0; }
    .contrib-grid { grid-template-columns: repeat(26, 1fr); }
    .readme-body { padding: 24px 20px; }
    .readme-footer { padding: 12px 20px; flex-direction: column; gap: 6px; }
  }
</style>
</head>
<body>

<!-- REPO BAR -->
<div class="repo-bar">
  <div class="breadcrumb">
    <a href="#">efegormus</a>
    <span class="sep">/</span>
    <a href="#"><strong>efegormus</strong></a>
    <span class="repo-badge">Public</span>
  </div>
  <div class="repo-bar-right">
    <button class="gh-btn">⭐ Star</button>
    <button class="gh-btn">🍴 Fork</button>
    <button class="gh-btn">👁 Watch</button>
  </div>
</div>

<div class="layout">

  <!-- README -->
  <div>
    <div class="readme-panel">
      <div class="readme-header">
        <svg viewBox="0 0 16 16"><path d="M0 3.75C0 2.784.784 2 1.75 2h12.5c.966 0 1.75.784 1.75 1.75v8.5A1.75 1.75 0 0 1 14.25 14H1.75A1.75 1.75 0 0 1 0 12.25Zm1.75-.25a.25.25 0 0 0-.25.25v8.5c0 .138.112.25.25.25h12.5a.25.25 0 0 0 .25-.25v-8.5a.25.25 0 0 0-.25-.25Z"></path></svg>
        README.md
      </div>

      <div class="readme-body">

        <!-- INTRO -->
        <span class="md-wave">👋</span>
        <h1 class="md-h1">Hi, I'm <em>Efe Görmüş</em></h1>

        <div class="md-subtitle">
          <span class="md-badge badge-blue">🎓 CS @ Sabancı University</span>
          <span class="md-badge badge-purple">✈️ Exchange @ TU Berlin 2026</span>
          <span class="md-badge badge-green">🟢 Open to Opportunities</span>
        </div>

        <div class="typing-wrap">
          <span class="typing-cursor">$ I build systems that go from idea → working product</span>
        </div>

        <hr class="md-divider">

        <!-- ABOUT -->
        <h2 class="md-h2">🧑‍💻 About Me</h2>
        <p class="md-p">
          I'm a Computer Science student passionate about writing <code>clean</code>,
          <code>structured</code>, and <code>efficient</code> code. My approach is simple:
          ship working systems and relentlessly improve them through iteration.
          I thrive at the intersection of algorithmic thinking and real-world engineering.
        </p>

        <hr class="md-divider">

        <!-- STACK -->
        <h2 class="md-h2">🛠️ Tech Stack</h2>

        <h3 class="md-h3">Languages</h3>
        <div class="skills-row">
          <div class="skill-chip"><span class="dot dot-cpp"></span>C++</div>
          <div class="skill-chip"><span class="dot dot-py"></span>Python</div>
          <div class="skill-chip"><span class="dot dot-html"></span>HTML</div>
        </div>

        <h3 class="md-h3">Core Areas</h3>
        <div class="skills-row">
          <div class="skill-chip"><span class="dot dot-algo"></span>Algorithms & Data Structures</div>
          <div class="skill-chip"><span class="dot dot-ml"></span>Machine Learning</div>
          <div class="skill-chip"><span class="dot dot-sys"></span>System Design</div>
          <div class="skill-chip"><span class="dot dot-ds"></span>Data Science</div>
        </div>

        <hr class="md-divider">

        <!-- PROJECTS -->
        <h2 class="md-h2">🚀 Projects</h2>

        <div class="project-card">
          <div class="project-top">
            <div class="project-name-row">
              <span class="project-icon">📊</span>
              <span class="project-title">startup-success-prediction</span>
            </div>
            <span class="md-badge badge-purple">ML</span>
          </div>
          <div class="project-desc">
            Machine learning model analyzing early-stage startup data to predict success probability.
            Designed with structured preprocessing and evaluation pipelines for clean, reproducible results.
          </div>
          <div class="project-footer">
            <div class="project-lang"><span class="dot dot-py"></span>Python</div>
            <span><span class="project-star">⭐</span> ML · Data Science</span>
          </div>
        </div>

        <div class="project-card">
          <div class="project-top">
            <div class="project-name-row">
              <span class="project-icon">🤖</span>
              <span class="project-title">vex-robotics-software</span>
            </div>
            <span class="md-badge badge-orange">Captain</span>
          </div>
          <div class="project-desc">
            Led software architecture and system integration for a competitive robotics team.
            Coordinated hardware-software interaction across subsystems — achieved
            <strong style="color:#d29922">Top National Rankings in Turkey for 3 consecutive years</strong>.
          </div>
          <div class="project-footer">
            <div class="project-lang"><span class="dot dot-cpp"></span>C++</div>
            <span><span class="project-star">🏆</span> National Champion · 3× Years</span>
          </div>
        </div>


      </div><!-- /readme-body -->

      <div class="readme-footer">
        <em>"Build. Ship. Improve. Repeat."</em>
        <span>Last updated: March 2026</span>
      </div>
    </div>
  </div>

  <!-- SIDEBAR -->
  <div class="sidebar">

    <div class="side-card" style="animation-delay:0.1s">
      <div class="side-card-title">📍 Info</div>
      <div class="location-item"><span>🏫</span> Sabancı University</div>
      <div class="location-item"><span>✈️</span> TU Berlin Exchange</div>
      <div class="location-item"><span>📍</span> Turkey · Germany</div>
      <div class="location-item" style="margin-top:8px">
        <div class="avail-dot"></div>
        <span style="color: #3fb950; font-size:11px;">Available for opportunities</span>
      </div>
    </div>

    <div class="side-card" style="animation-delay:0.15s">
      <div class="side-card-title">🔗 Connect</div>

      <a class="side-link" href="mailto:efe.gormus@sabanciuniv.edu">
        <span class="side-link-icon">📧</span>Email
      </a>
      <a class="side-link" href="https://linkedin.com/in/efegormus" target="_blank">
        <span class="side-link-icon">💼</span>LinkedIn
      </a>
      <a class="side-link" href="https://github.com/efegormus" target="_blank">
        <span class="side-link-icon">🐙</span>GitHub
      </a>
    </div>

  </div>
</div>



</body>
</html>
