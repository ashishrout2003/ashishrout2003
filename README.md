<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Animated README + Animation Dashboard — Ready to copy</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#7c3aed;--muted:#94a3b8;--glass: rgba(255,255,255,0.03)}
    html,body{height:100%;margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,'Helvetica Neue',Arial}
    body{background:linear-gradient(180deg,#071028 0%,#071226 60%);color:#e6eef8;padding:24px}
    .wrap{display:grid;grid-template-columns:1fr 520px;gap:20px;max-width:1200px;margin:0 auto}
    .card{background:linear-gradient(180deg,var(--card),#061226);border-radius:14px;padding:18px;box-shadow:0 6px 30px rgba(2,6,23,0.6);border:1px solid rgba(255,255,255,0.03)}
    header{display:flex;align-items:center;gap:12px;margin-bottom:12px}
    .logo{width:64px;height:64px;border-radius:12px;display:grid;place-items:center;background:linear-gradient(135deg,var(--accent),#06b6d4);box-shadow:0 6px 30px rgba(124,58,237,0.18);transform:rotate(-10deg);}
    .logo svg{width:44px;height:44px;filter:drop-shadow(0 8px 24px rgba(12,14,26,0.6))}
    h1{margin:0;font-size:20px}
    p.lead{margin:0;color:var(--muted);font-size:13px}

    /* README pane */
    .readme{height:78vh;overflow:auto;padding:18px}
    pre.markdown{background:var(--glass);padding:12px;border-radius:10px;color:#dff3ff;overflow:auto}

    /* Dashboard */
    .dash{height:78vh;display:flex;flex-direction:column;gap:14px}
    .canvas{flex:1;display:grid;grid-template-columns:1fr 1fr;gap:12px}
    .tile{border-radius:12px;padding:12px;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);backdrop-filter:blur(6px)}

    /* Animated snack */
    .snack-wrap{display:flex;align-items:center;justify-content:center;height:100%}
    .burger{width:120px;height:120px;position:relative;transform-origin:center;animation:float 3s ease-in-out infinite}
    @keyframes float{0%{transform:translateY(0)}50%{transform:translateY(-12px) rotate(-3deg)}100%{transform:translateY(0)}}
    .bun{fill:#f6c29c}
    .patty{fill:#4b2e2e}
    .lettuce{fill:#79c267}
    .cheese{fill:#ffcb4c}
    .sesame{fill:#fff3}
    .sprinkle{animation:spin 6s linear infinite}
    @keyframes spin{from{transform:rotate(0)}to{transform:rotate(360deg)}}

    /* stat badges row */
    .badges{display:flex;flex-wrap:wrap;gap:8px}
    .controls{display:flex;gap:8px;margin-top:8px}
    button{background:var(--accent);border:0;padding:8px 12px;border-radius:8px;color:white;font-weight:600;cursor:pointer}
    button.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06)}

    .footer{font-size:12px;color:var(--muted);text-align:center;margin-top:8px}

    /* small responsive */
    @media (max-width:980px){.wrap{grid-template-columns:1fr;}.dash{order:2}}
  </style>
</head>
<body>
  <div class="wrap">
    <div class="card">
      <header>
        <div class="logo" title="Animated README"><svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M3 12a9 9 0 0118 0v1H3v-1z" fill="rgba(255,255,255,0.18)"/><path d="M7 8a1 1 0 011-1h8a1 1 0 011 1v8a3 3 0 01-3 3H10a3 3 0 01-3-3V8z" fill="#fff" opacity="0.06"/></svg></div>
        <div>
          <h1>Animated README & Dashboard</h1>
          <p class="lead">One-file HTML that generates a copyable README.md with GIF/Lottie + a live animation dashboard you can preview.</p>
        </div>
      </header>

      <div class="readme" id="readmePane">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">
          <strong>README preview</strong>
          <div class="controls">
            <button id="copyBtn">Copy README.md</button>
            <button class="ghost" id="downloadBtn">Download README.md</button>
          </div>
        </div>
        <div id="rendered"></div>
        <pre class="markdown" id="raw" style="display:none"></pre>
      </div>

    </div>

    <div class="card dash">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <strong>Animation Dashboard</strong>
        <div class="badges">
          <!-- shields badges (examples) -->
          <img src="https://img.shields.io/badge/animated-yes-7c3aed.svg" alt="animated">
          <img src="https://img.shields.io/badge/lottie-ready-06b6d4.svg" alt="lottie">
          <img src="https://img.shields.io/badge/GIF-supported-brightgreen.svg" alt="gif">
        </div>
      </div>

      <div class="canvas">
        <div class="tile" id="tile1">
          <h4 style="margin-top:4px;margin-bottom:6px">Live Lottie Preview</h4>
          <div id="lottie" style="height:160px;display:grid;place-items:center"></div>
          <small style="color:var(--muted)">Tip: change the Lottie URL in the controls to preview your animation.</small>
          <div style="margin-top:8px;display:flex;gap:8px">
            <input id="lottieUrl" placeholder="Paste lottie JSON URL (cdn)" style="flex:1;padding:8px;border-radius:8px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:inherit">
            <button id="playLottie">Load</button>
          </div>
        </div>

        <div class="tile" id="tile2">
          <h4 style="margin-top:4px;margin-bottom:6px">Animated Snack (CSS + SVG)</h4>
          <div class="snack-wrap">
            <!-- playful animated burger -->
            <svg class="burger" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
              <g transform="translate(100,100)">
                <ellipse class="bun" cx="0" cy="-18" rx="66" ry="26"></ellipse>
                <g class="sesame" transform="translate(-30,-34)"><circle cx="0" cy="0" r="2"/><circle cx="14" cy="-2" r="2"/><circle cx="26" cy="1" r="2"/></g>
                <rect class="lettuce" x="-54" y="0" width="108" height="14" rx="6"></rect>
                <rect class="cheese" x="-50" y="14" width="100" height="12" rx="3"></rect>
                <rect class="patty" x="-54" y="28" width="108" height="16" rx="6"></rect>
                <ellipse class="bun" cx="0" cy="48" rx="66" ry="26"></ellipse>
              </g>
            </svg>
          </div>
        </div>

        <div class="tile" id="tile3">
          <h4 style="margin-top:4px;margin-bottom:6px">Animated SVG Blob</h4>
          <div style="height:160px;display:flex;align-items:center;justify-content:center">
            <svg viewBox="0 0 600 400" width="100%" height="160">
              <defs>
                <linearGradient id="g1" x1="0" x2="1">
                  <stop offset="0" stop-color="#7c3aed" stop-opacity="0.9" />
                  <stop offset="1" stop-color="#06b6d4" stop-opacity="0.9" />
                </linearGradient>
              </defs>
              <path id="blob" fill="url(#g1)"></path>
            </svg>
          </div>
        </div>

        <div class="tile" id="tile4">
          <h4 style="margin-top:4px;margin-bottom:6px">README Helpers</h4>
          <div style="display:flex;flex-direction:column;gap:8px">
            <button id="insertGif">Insert example GIF into README</button>
            <button id="insertBadge">Insert GitHub Stats Badge</button>
            <button id="insertLottie">Insert Lottie Embed</button>
          </div>
        </div>

      </div>

      <div class="footer">Preview created README on the left. Use buttons to copy or download. Open file in VS Code and push to GitHub to show animations on your profile README.</div>
    </div>
  </div>

  <!-- libraries -->
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/bodymovin/5.9.6/lottie.min.js"></script>
  <script>
    // Initial README markdown content
    const readmeMarkdown = `# Hi 👋 I'm Ashish

> 🎛️ Animated GitHub README + Animation Dashboard

![animated header](https://media.giphy.com/media/3oEjI6SIIHBdRxXI40/giphy.gif)

## About
I build things, learn things, and love animations. This README demonstrates:
- Animated GIFs & SVGs
- Lottie animations
- A small "animation dashboard" to preview and copy this README

## Example Animated Badges
![GitHub followers](https://img.shields.io/github/followers/your-username?label=Followers&style=for-the-badge)
![Top language](https://img.shields.io/github/languages/top/your-username/your-repo?style=for-the-badge)

## Lottie (embed)
You can embed a Lottie animation in your README by linking an animated GIF or converting the animation to an HTML snippet inside your project pages. Example link:

\`\`\`html
<!-- Lottie player (use in web pages, not raw README) -->
<script src="https://unpkg.com/@lottiefiles/lottie-player@latest/dist/lottie-player.js"></script>
<lottie-player src="https://assets9.lottiefiles.com/packages/lf20_u4yrau.json" background="transparent" speed="1" style="width:200px; height:200px;" loop autoplay></lottie-player>
\`\`\`

## Animated GIF example
![Coding animation](https://media.giphy.com/media/l0HlSNOxJB956qwfK/giphy.gif)

## How to use
1. Edit this README.md and replace placeholders like \`your-username\`.
2. Commit it to a repository named exactly **\`<your-username>\`** to show on your GitHub profile.
3. Push and enjoy the animations!

---

*Generated with an interactive animation dashboard.*
`;

    // render markdown
    const rendered = document.getElementById('rendered');
    const raw = document.getElementById('raw');
    raw.textContent = readmeMarkdown;
    rendered.innerHTML = marked.parse(readmeMarkdown);

    // copy button
    document.getElementById('copyBtn').addEventListener('click', async ()=>{
      await navigator.clipboard.writeText(readmeMarkdown);
      alert('README.md copied to clipboard — paste into your README.md file.');
    });
    document.getElementById('downloadBtn').addEventListener('click', ()=>{
      const blob = new Blob([readmeMarkdown],{type:'text/markdown'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href = url; a.download = 'README.md'; document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
    });

    // Lottie loader
    const lottieContainer = document.getElementById('lottie');
    let player = null;
    function loadLottie(url){
      lottieContainer.innerHTML = '';
      try{
        player = lottie.loadAnimation({container: lottieContainer,renderer:'svg',loop:true,autoplay:true,path:url});
      }catch(e){ lottieContainer.innerHTML = '<small style="color:#faa">Failed to load Lottie: check URL</small>' }
    }
    document.getElementById('playLottie').addEventListener('click', ()=>{
      const url = document.getElementById('lottieUrl').value.trim();
      if(!url){ alert('Paste a direct lottie JSON URL (cdn). Example: https://assets9.lottiefiles.com/packages/lf20_u4yrau.json'); return }
      loadLottie(url);
    });
    // default lottie
    loadLottie('https://assets9.lottiefiles.com/packages/lf20_u4yrau.json');

    // blob morph animation
    const path = document.getElementById('blob');
    const blobs = [
      'M421.5,286Q378,322,328,338Q278,354,228,340Q178,326,134,296Q90,266,80,209Q70,152,98.5,106Q127,60,185,43Q243,26,293,45Q343,64,387,96Q431,128,443,183Q455,238,421.5,286Z',
      'M421.5,286Q396,332,349,345Q302,358,255,350Q208,342,176,315Q144,288,103.5,254Q63,220,60,170Q57,120,95,88Q133,56,185,48Q237,40,286.5,56Q336,72,371.5,106Q407,140,430,187Q453,234,421.5,286Z',
      'M437,290Q402,340,347,361Q292,382,245,364Q198,346,158,318Q118,290,96,240Q74,190,107,150Q140,110,190,90Q240,70,295,64Q350,58,389.5,95Q429,132,448.5,176Q468,220,437,290Z'
    ];
    let bi = 0;
    function morph(){ path.setAttribute('d',blobs[bi]); bi=(bi+1)%blobs.length; }
    morph(); setInterval(morph,2200);

    // insert helpers into README markdown
    document.getElementById('insertGif').addEventListener('click', ()=>{
      const gifMd = '\n\n![Example GIF](https://media.giphy.com/media/3oEjI6SIIHBdRxXI40/giphy.gif)\n';
      raw.textContent += gifMd; rendered.innerHTML = marked.parse(raw.textContent);
      alert('Inserted example GIF into README preview. Click Copy or Download to save.');
    });
    document.getElementById('insertBadge').addEventListener('click', ()=>{
      const b = '\n\n![GitHub stats](https://github-readme-stats.vercel.app/api?username=your-username&show_icons=true&theme=radical)\n';
      raw.textContent += b; rendered.innerHTML = marked.parse(raw.textContent);
      alert('Inserted example GitHub stats badge. Replace \`your-username\`.');
    });
    document.getElementById('insertLottie').addEventListener('click', ()=>{
      const l = '\n\n<!-- Lottie player (works in web pages, not on raw README) -->\n<script src="https://unpkg.com/@lottiefiles/lottie-player@latest/dist/lottie-player.js"></script>\n<lottie-player src="https://assets9.lottiefiles.com/packages/lf20_u4yrau.json"  background="transparent"  speed="1"  style="width:200px; height:200px;"  loop  autoplay></lottie-player>\n';
      raw.textContent += l; rendered.innerHTML = marked.parse(raw.textContent);
      alert('Inserted a Lottie snippet (for web pages).');
    });
  </script>
</body>
</html>
