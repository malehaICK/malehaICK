<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GitHub README Generator</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Mono:wght@300;400;500&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #f8f7f4;
    --surface: #ffffff;
    --border: #e8e4dc;
    --border-strong: #d0cac0;
    --text: #1a1814;
    --text-muted: #7a746a;
    --accent: #1a1814;
    --accent-light: #f0ede8;
    --green: #2d6a4f;
    --green-light: #e8f4ee;
    --tag-bg: #f0ede8;
  }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  header {
    padding: 2rem 3rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--border);
    background: var(--surface);
  }

  .logo {
    font-family: 'DM Serif Display', serif;
    font-size: 1.4rem;
    letter-spacing: -0.02em;
  }

  .logo span { font-style: italic; color: var(--text-muted); }

  .badge {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    background: var(--accent-light);
    padding: 0.3rem 0.8rem;
    border-radius: 20px;
    color: var(--text-muted);
    letter-spacing: 0.05em;
  }

  .app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    flex: 1;
    height: calc(100vh - 73px);
  }

  /* ── LEFT PANEL ── */
  .panel-left {
    border-right: 1px solid var(--border);
    overflow-y: auto;
    padding: 2.5rem 3rem;
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }

  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 1rem;
  }

  .field-group { display: flex; flex-direction: column; gap: 1.2rem; }

  .field { display: flex; flex-direction: column; gap: 0.4rem; }

  .field label {
    font-size: 0.78rem;
    font-weight: 500;
    color: var(--text-muted);
  }

  .field input, .field textarea, .field select {
    font-family: 'DM Sans', sans-serif;
    font-size: 0.9rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 0.7rem 1rem;
    color: var(--text);
    outline: none;
    transition: border-color 0.2s;
    resize: none;
  }

  .field input:focus, .field textarea:focus, .field select:focus {
    border-color: var(--accent);
  }

  .field textarea { min-height: 80px; line-height: 1.6; }

  .divider {
    height: 1px;
    background: var(--border);
  }

  /* Skills input */
  .tags-input {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 0.6rem 0.8rem;
    min-height: 46px;
    cursor: text;
    transition: border-color 0.2s;
  }
  .tags-input:focus-within { border-color: var(--accent); }

  .tag {
    display: flex;
    align-items: center;
    gap: 0.3rem;
    background: var(--tag-bg);
    padding: 0.2rem 0.6rem;
    border-radius: 4px;
    font-size: 0.8rem;
    font-family: 'DM Mono', monospace;
  }

  .tag button {
    background: none;
    border: none;
    cursor: pointer;
    color: var(--text-muted);
    font-size: 0.9rem;
    line-height: 1;
    padding: 0;
  }

  .tag-input-field {
    border: none !important;
    outline: none;
    background: transparent;
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    min-width: 80px;
    flex: 1;
    padding: 0.2rem 0 !important;
  }

  /* Toggles */
  .toggles { display: flex; flex-wrap: wrap; gap: 0.5rem; }

  .toggle-btn {
    font-size: 0.78rem;
    font-family: 'DM Sans', sans-serif;
    padding: 0.4rem 0.9rem;
    border-radius: 6px;
    border: 1px solid var(--border);
    background: var(--surface);
    cursor: pointer;
    color: var(--text-muted);
    transition: all 0.15s;
  }

  .toggle-btn.active {
    background: var(--accent);
    color: #fff;
    border-color: var(--accent);
  }

  /* Stats color picker */
  .color-grid { display: flex; gap: 0.6rem; flex-wrap: wrap; }
  .color-swatch {
    width: 28px; height: 28px;
    border-radius: 50%;
    cursor: pointer;
    border: 2px solid transparent;
    transition: transform 0.15s, border-color 0.15s;
  }
  .color-swatch:hover { transform: scale(1.15); }
  .color-swatch.selected { border-color: var(--text); }

  /* Copy button */
  .copy-btn {
    font-family: 'DM Sans', sans-serif;
    font-size: 0.85rem;
    font-weight: 500;
    background: var(--accent);
    color: #fff;
    border: none;
    border-radius: 8px;
    padding: 0.8rem 1.5rem;
    cursor: pointer;
    transition: opacity 0.2s;
    letter-spacing: 0.01em;
  }
  .copy-btn:hover { opacity: 0.85; }
  .copy-btn.copied { background: var(--green); }

  .btn-row { display: flex; gap: 0.8rem; align-items: center; }

  .raw-btn {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    background: transparent;
    color: var(--text-muted);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 0.8rem 1.2rem;
    cursor: pointer;
    transition: all 0.15s;
  }
  .raw-btn:hover { border-color: var(--accent); color: var(--text); }

  /* ── RIGHT PANEL (preview) ── */
  .panel-right {
    overflow-y: auto;
    background: var(--surface);
    display: flex;
    flex-direction: column;
  }

  .preview-header {
    padding: 1.2rem 2.5rem;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: sticky;
    top: 0;
    background: var(--surface);
    z-index: 10;
  }

  .preview-tabs { display: flex; gap: 0; }
  .tab-btn {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.05em;
    padding: 0.4rem 1rem;
    border: 1px solid var(--border);
    background: transparent;
    cursor: pointer;
    color: var(--text-muted);
    transition: all 0.15s;
  }
  .tab-btn:first-child { border-radius: 6px 0 0 6px; }
  .tab-btn:last-child { border-radius: 0 6px 6px 0; border-left: none; }
  .tab-btn.active { background: var(--accent); color: #fff; border-color: var(--accent); }

  .preview-content {
    padding: 2.5rem 3rem;
    flex: 1;
  }

  /* GitHub MD Preview styles */
  .md-preview {
    font-family: 'DM Sans', sans-serif;
    line-height: 1.7;
    color: var(--text);
  }

  .md-preview h1 {
    font-family: 'DM Serif Display', serif;
    font-size: 2rem;
    margin-bottom: 0.5rem;
    letter-spacing: -0.03em;
  }
  .md-preview h2 {
    font-size: 1.1rem;
    font-weight: 600;
    margin: 1.8rem 0 0.8rem;
    padding-bottom: 0.5rem;
    border-bottom: 1px solid var(--border);
  }
  .md-preview h3 { font-size: 0.95rem; font-weight: 600; margin: 1.2rem 0 0.4rem; }
  .md-preview p { margin-bottom: 0.8rem; font-size: 0.92rem; color: #3a3630; }
  .md-preview code {
    font-family: 'DM Mono', monospace;
    font-size: 0.82rem;
    background: var(--tag-bg);
    padding: 0.15rem 0.4rem;
    border-radius: 4px;
  }
  .md-preview pre {
    background: #1a1814;
    color: #f0ede8;
    padding: 1.2rem 1.5rem;
    border-radius: 10px;
    font-family: 'DM Mono', monospace;
    font-size: 0.82rem;
    overflow-x: auto;
    margin: 1rem 0;
    line-height: 1.6;
  }

  .skill-badges { display: flex; flex-wrap: wrap; gap: 0.4rem; margin: 0.5rem 0 1rem; }
  .skill-badge {
    font-family: 'DM Mono', monospace;
    font-size: 0.72rem;
    background: var(--tag-bg);
    border: 1px solid var(--border);
    padding: 0.25rem 0.7rem;
    border-radius: 4px;
    color: var(--text);
  }

  .stats-row { display: flex; gap: 1rem; flex-wrap: wrap; margin: 1rem 0; }
  .stat-card {
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 1rem 1.5rem;
    min-width: 140px;
    flex: 1;
  }
  .stat-card .stat-label { font-size: 0.7rem; color: var(--text-muted); margin-bottom: 0.3rem; font-family: 'DM Mono', monospace; }
  .stat-card .stat-value { font-family: 'DM Serif Display', serif; font-size: 1.6rem; }

  .contact-row { display: flex; gap: 0.8rem; flex-wrap: wrap; margin-top: 0.5rem; }
  .contact-chip {
    font-size: 0.8rem;
    font-family: 'DM Mono', monospace;
    padding: 0.35rem 0.9rem;
    border-radius: 6px;
    border: 1px solid var(--border);
    color: var(--text-muted);
  }

  .wave { display: inline-block; animation: wave 2s infinite; transform-origin: 70% 70%; }
  @keyframes wave {
    0%,60%,100%{transform:rotate(0deg)}
    10%,30%{transform:rotate(14deg)}
    20%{transform:rotate(-8deg)}
    40%{transform:rotate(-4deg)}
    50%{transform:rotate(10deg)}
  }

  .streak-bar { display: flex; gap: 3px; margin: 0.8rem 0; }
  .streak-cell {
    width: 12px; height: 12px;
    border-radius: 2px;
    background: var(--border);
    transition: background 0.2s;
  }

  /* Raw markdown panel */
  .raw-view {
    display: none;
    padding: 2.5rem 3rem;
    flex: 1;
  }
  .raw-view.visible { display: block; }
  .raw-view pre {
    font-family: 'DM Mono', monospace;
    font-size: 0.78rem;
    line-height: 1.8;
    color: var(--text-muted);
    white-space: pre-wrap;
    word-break: break-word;
  }

  .preview-content.hidden { display: none; }

  /* Animations */
  @keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }
  .md-preview > * { animation: fadeIn 0.3s ease forwards; }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--border-strong); border-radius: 2px; }

  @media (max-width: 900px) {
    .app { grid-template-columns: 1fr; height: auto; }
    .panel-right { min-height: 60vh; }
  }
</style>
</head>
<body>

<header>
  <div class="logo">readme<span>.craft</span></div>
  <div class="badge">GitHub README Generator</div>
</header>

<div class="app">

  <!-- LEFT: FORM -->
  <div class="panel-left">

    <div>
      <div class="section-label">Identity</div>
      <div class="field-group">
        <div class="field">
          <label>Name</label>
          <input type="text" id="f-name" placeholder="e.g. Alex Rivera" oninput="render()">
        </div>
        <div class="field">
          <label>GitHub Username</label>
          <input type="text" id="f-username" placeholder="e.g. alexrivera" oninput="render()">
        </div>
        <div class="field">
          <label>Role / Title</label>
          <input type="text" id="f-role" placeholder="e.g. Full-Stack Developer · Open Source Enthusiast" oninput="render()">
        </div>
        <div class="field">
          <label>Bio</label>
          <textarea id="f-bio" placeholder="A short, punchy bio about what you build and care about..." oninput="render()"></textarea>
        </div>
        <div class="field">
          <label>Location</label>
          <input type="text" id="f-location" placeholder="e.g. Toronto, Canada" oninput="render()">
        </div>
      </div>
    </div>

    <div class="divider"></div>

    <div>
      <div class="section-label">Skills & Tech</div>
      <div class="field">
        <label>Add skills (press Enter)</label>
        <div class="tags-input" id="tags-container" onclick="document.getElementById('tag-input').focus()">
          <input class="tag-input-field" id="tag-input" placeholder="e.g. React" onkeydown="handleTagInput(event)">
        </div>
      </div>
    </div>

    <div class="divider"></div>

    <div>
      <div class="section-label">Sections to Include</div>
      <div class="toggles" id="section-toggles">
        <button class="toggle-btn active" data-sec="stats" onclick="toggleSection(this)">GitHub Stats</button>
        <button class="toggle-btn active" data-sec="streak" onclick="toggleSection(this)">Streak</button>
        <button class="toggle-btn active" data-sec="projects" onclick="toggleSection(this)">Projects</button>
        <button class="toggle-btn active" data-sec="contact" onclick="toggleSection(this)">Contact</button>
        <button class="toggle-btn" data-sec="quote" onclick="toggleSection(this)">Quote</button>
        <button class="toggle-btn" data-sec="visitors" onclick="toggleSection(this)">Visitor Count</button>
      </div>
    </div>

    <div class="divider"></div>

    <div>
      <div class="section-label">Projects (up to 3)</div>
      <div class="field-group">
        <div class="field">
          <label>Project 1 — Name</label>
          <input type="text" id="p1-name" placeholder="e.g. devflow" oninput="render()">
        </div>
        <div class="field">
          <label>Project 1 — Description</label>
          <input type="text" id="p1-desc" placeholder="One-liner description" oninput="render()">
        </div>
        <div class="field">
          <label>Project 2 — Name</label>
          <input type="text" id="p2-name" placeholder="e.g. openui" oninput="render()">
        </div>
        <div class="field">
          <label>Project 2 — Description</label>
          <input type="text" id="p2-desc" placeholder="One-liner description" oninput="render()">
        </div>
      </div>
    </div>

    <div class="divider"></div>

    <div>
      <div class="section-label">Contact & Links</div>
      <div class="field-group">
        <div class="field">
          <label>Email</label>
          <input type="text" id="f-email" placeholder="hello@you.dev" oninput="render()">
        </div>
        <div class="field">
          <label>Twitter / X handle</label>
          <input type="text" id="f-twitter" placeholder="@handle" oninput="render()">
        </div>
        <div class="field">
          <label>LinkedIn URL</label>
          <input type="text" id="f-linkedin" placeholder="linkedin.com/in/you" oninput="render()">
        </div>
        <div class="field">
          <label>Portfolio / Website</label>
          <input type="text" id="f-website" placeholder="yourname.dev" oninput="render()">
        </div>
      </div>
    </div>

    <div class="divider"></div>

    <div>
      <div class="section-label">Stats Theme Color</div>
      <div class="color-grid" id="color-grid">
        <div class="color-swatch selected" data-color="1a1814" style="background:#1a1814" onclick="selectColor(this)"></div>
        <div class="color-swatch" data-color="2d6a4f" style="background:#2d6a4f" onclick="selectColor(this)"></div>
        <div class="color-swatch" data-color="1d4ed8" style="background:#1d4ed8" onclick="selectColor(this)"></div>
        <div class="color-swatch" data-color="7c3aed" style="background:#7c3aed" onclick="selectColor(this)"></div>
        <div class="color-swatch" data-color="be185d" style="background:#be185d" onclick="selectColor(this)"></div>
        <div class="color-swatch" data-color="b45309" style="background:#b45309" onclick="selectColor(this)"></div>
        <div class="color-swatch" data-color="0f766e" style="background:#0f766e" onclick="selectColor(this)"></div>
      </div>
    </div>

    <div class="divider"></div>

    <div class="btn-row">
      <button class="copy-btn" id="copy-btn" onclick="copyMarkdown()">Copy Markdown</button>
      <button class="raw-btn" onclick="showRaw()">View Raw</button>
    </div>

  </div>

  <!-- RIGHT: PREVIEW -->
  <div class="panel-right">
    <div class="preview-header">
      <span style="font-size:0.78rem; color:var(--text-muted); font-family:'DM Mono',monospace;">LIVE PREVIEW</span>
      <div class="preview-tabs">
        <button class="tab-btn active" id="tab-preview" onclick="switchTab('preview')">RENDERED</button>
        <button class="tab-btn" id="tab-raw" onclick="switchTab('raw')">MARKDOWN</button>
      </div>
    </div>

    <div class="preview-content" id="preview-content">
      <div class="md-preview" id="md-preview"></div>
    </div>

    <div class="raw-view" id="raw-view">
      <pre id="raw-text"></pre>
    </div>
  </div>

</div>

<script>
  let skills = [];
  let activeSections = { stats: true, streak: true, projects: true, contact: true, quote: false, visitors: false };
  let statsColor = '1a1814';

  function v(id) { return document.getElementById(id)?.value?.trim() || ''; }

  function handleTagInput(e) {
    if (e.key === 'Enter' || e.key === ',') {
      e.preventDefault();
      const val = e.target.value.trim().replace(',','');
      if (val && !skills.includes(val)) {
        skills.push(val);
        renderTags();
        render();
      }
      e.target.value = '';
    }
    if (e.key === 'Backspace' && !e.target.value && skills.length) {
      skills.pop();
      renderTags();
      render();
    }
  }

  function renderTags() {
    const container = document.getElementById('tags-container');
    const input = document.getElementById('tag-input');
    container.innerHTML = '';
    skills.forEach((s, i) => {
      const tag = document.createElement('div');
      tag.className = 'tag';
      tag.innerHTML = `${s}<button onclick="removeTag(${i})">×</button>`;
      container.appendChild(tag);
    });
    container.appendChild(input);
  }

  function removeTag(i) {
    skills.splice(i, 1);
    renderTags();
    render();
  }

  function toggleSection(btn) {
    const sec = btn.dataset.sec;
    activeSections[sec] = !activeSections[sec];
    btn.classList.toggle('active', activeSections[sec]);
    render();
  }

  function selectColor(el) {
    document.querySelectorAll('.color-swatch').forEach(s => s.classList.remove('selected'));
    el.classList.add('selected');
    statsColor = el.dataset.color;
    render();
  }

  function switchTab(tab) {
    document.getElementById('preview-content').classList.toggle('hidden', tab === 'raw');
    document.getElementById('raw-view').classList.toggle('visible', tab === 'raw');
    document.getElementById('tab-preview').classList.toggle('active', tab === 'preview');
    document.getElementById('tab-raw').classList.toggle('active', tab === 'raw');
    if (tab === 'raw') document.getElementById('raw-text').textContent = generateMarkdown();
  }

  function showRaw() { switchTab('raw'); }

  // ── PREVIEW RENDER ──
  function render() {
    const name = v('f-name') || 'Your Name';
    const username = v('f-username') || 'yourusername';
    const role = v('f-role') || 'Developer · Open Source Enthusiast';
    const bio = v('f-bio') || 'I build things for the web. Passionate about clean code and great UX.';
    const location = v('f-location');
    const email = v('f-email');
    const twitter = v('f-twitter');
    const linkedin = v('f-linkedin');
    const website = v('f-website');
    const p1name = v('p1-name'); const p1desc = v('p1-desc');
    const p2name = v('p2-name'); const p2desc = v('p2-desc');

    // Streak cells
    const streakHTML = Array.from({length: 52}, (_,i) => {
      const intensity = Math.random();
      const alpha = intensity < 0.4 ? '10' : intensity < 0.65 ? '30' : intensity < 0.85 ? '60' : 'ff';
      return `<div class="streak-cell" style="background:#${statsColor}${alpha}"></div>`;
    }).join('');

    let html = `
      <h1><span class="wave">👋</span> Hey, I'm ${name}</h1>
      <p style="color:var(--text-muted); font-family:'DM Mono',monospace; font-size:0.8rem; margin-bottom:0.3rem">${role}</p>
      ${location ? `<p style="font-size:0.8rem;color:var(--text-muted)">📍 ${location}</p>` : ''}
      <p style="margin-top:1rem">${bio}</p>
    `;

    if (skills.length) {
      html += `<h2>🛠 Tech Stack</h2><div class="skill-badges">${skills.map(s=>`<span class="skill-badge">${s}</span>`).join('')}</div>`;
    }

    if (activeSections.stats) {
      html += `
        <h2>📊 GitHub Stats</h2>
        <div class="stats-row">
          <div class="stat-card"><div class="stat-label">COMMITS THIS YEAR</div><div class="stat-value" style="color:#${statsColor}">847</div></div>
          <div class="stat-card"><div class="stat-label">REPOSITORIES</div><div class="stat-value" style="color:#${statsColor}">42</div></div>
          <div class="stat-card"><div class="stat-label">PULL REQUESTS</div><div class="stat-value" style="color:#${statsColor}">203</div></div>
        </div>
        <p style="font-size:0.72rem; color:var(--text-muted); font-family:'DM Mono',monospace">
          ↑ Replace with real GitHub stats badges (github-readme-stats)
        </p>
      `;
    }

    if (activeSections.streak) {
      html += `<h2>🔥 Contribution Streak</h2><div class="streak-bar">${streakHTML}</div>`;
    }

    if (activeSections.projects && (p1name || p2name)) {
      html += `<h2>🚀 Featured Projects</h2>`;
      if (p1name) html += `<h3>→ <code>${p1name}</code></h3><p>${p1desc || 'No description yet.'}</p>`;
      if (p2name) html += `<h3>→ <code>${p2name}</code></h3><p>${p2desc || 'No description yet.'}</p>`;
    }

    if (activeSections.quote) {
      html += `
        <h2>💭 Quote</h2>
        <pre>"First, solve the problem. Then, write the code."
— John Johnson</pre>
      `;
    }

    if (activeSections.visitors) {
      html += `<p style="font-family:'DM Mono',monospace; font-size:0.78rem; color:var(--text-muted)">👁 <strong>Visitors:</strong> <code>![Visitor Count](https://profile-counter.glitch.me/${username}/count.svg)</code></p>`;
    }

    if (activeSections.contact && (email || twitter || linkedin || website)) {
      html += `<h2>📬 Get in Touch</h2><div class="contact-row">`;
      if (email)    html += `<span class="contact-chip">✉ ${email}</span>`;
      if (twitter)  html += `<span class="contact-chip">𝕏 ${twitter}</span>`;
      if (linkedin) html += `<span class="contact-chip">in ${linkedin}</span>`;
      if (website)  html += `<span class="contact-chip">🌐 ${website}</span>`;
      html += `</div>`;
    }

    html += `<p style="margin-top:2rem; font-size:0.75rem; color:var(--text-muted); font-family:'DM Mono',monospace">⭐ Star a repo if you find it useful!</p>`;

    document.getElementById('md-preview').innerHTML = html;
    if (!document.getElementById('raw-view').classList.contains('visible')) return;
    document.getElementById('raw-text').textContent = generateMarkdown();
  }

  // ── MARKDOWN GENERATOR ──
  function generateMarkdown() {
    const name = v('f-name') || 'Your Name';
    const username = v('f-username') || 'yourusername';
    const role = v('f-role') || 'Developer · Open Source Enthusiast';
    const bio = v('f-bio') || 'I build things for the web.';
    const location = v('f-location');
    const email = v('f-email');
    const twitter = v('f-twitter');
    const linkedin = v('f-linkedin');
    const website = v('f-website');
    const p1n = v('p1-name'); const p1d = v('p1-desc');
    const p2n = v('p2-name'); const p2d = v('p2-desc');

    let md = `# 👋 Hey, I'm ${name}\n\n`;
    md += `**${role}**\n\n`;
    if (location) md += `📍 ${location}\n\n`;
    md += `${bio}\n\n`;
    md += `---\n\n`;

    if (skills.length) {
      md += `## 🛠 Tech Stack\n\n`;
      md += skills.map(s => `\`${s}\``).join(' · ') + '\n\n';
    }

    if (activeSections.stats) {
      md += `## 📊 GitHub Stats\n\n`;
      md += `![${name}'s GitHub Stats](https://github-readme-stats.vercel.app/api?username=${username}&show_icons=true&theme=default&title_color=${statsColor}&icon_color=${statsColor}&hide_border=true)\n\n`;
      md += `![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=${username}&layout=compact&hide_border=true&title_color=${statsColor})\n\n`;
    }

    if (activeSections.streak) {
      md += `## 🔥 Streak\n\n`;
      md += `![GitHub Streak](https://streak-stats.demolab.com?user=${username}&hide_border=true&ring=${statsColor}&fire=${statsColor}&currStreakLabel=${statsColor})\n\n`;
    }

    if (activeSections.projects && (p1n || p2n)) {
      md += `## 🚀 Featured Projects\n\n`;
      if (p1n) { md += `### → \`${p1n}\`\n${p1d || ''}\n\n`; }
      if (p2n) { md += `### → \`${p2n}\`\n${p2d || ''}\n\n`; }
    }

    if (activeSections.quote) {
      md += `## 💭 Quote\n\n`;
      md += `> "First, solve the problem. Then, write the code." — John Johnson\n\n`;
    }

    if (activeSections.visitors) {
      md += `![Visitor Count](https://profile-counter.glitch.me/${username}/count.svg)\n\n`;
    }

    if (activeSections.contact && (email || twitter || linkedin || website)) {
      md += `## 📬 Get in Touch\n\n`;
      if (email)    md += `- ✉ [${email}](mailto:${email})\n`;
      if (twitter)  md += `- 𝕏 [${twitter}](https://twitter.com/${twitter.replace('@','')})\n`;
      if (linkedin) md += `- 💼 [LinkedIn](https://${linkedin})\n`;
      if (website)  md += `- 🌐 [${website}](https://${website})\n`;
      md += '\n';
    }

    md += `---\n\n⭐ *Star a repo if you find it useful!*\n`;
    return md;
  }

  function copyMarkdown() {
    const md = generateMarkdown();
    navigator.clipboard.writeText(md).then(() => {
      const btn = document.getElementById('copy-btn');
      btn.textContent = '✓ Copied!';
      btn.classList.add('copied');
      setTimeout(() => { btn.textContent = 'Copy Markdown'; btn.classList.remove('copied'); }, 2000);
    });
  }

  // Init
  render();
</script>
</body>
</html>
