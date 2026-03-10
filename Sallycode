<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Invest1 — Demo</title>
  <style>
    :root{--bg:#f6f8fa;--card:#fff;--accent:#0b5cff;--muted:#666;}
    body{font-family:Inter,system-ui,Segoe UI,Arial; background:var(--bg); margin:0; padding:36px; display:flex; justify-content:center}
    .card{background:var(--card); padding:28px; border-radius:12px; width:720px; box-shadow:0 6px 20px rgba(20,30,60,0.08)}
    h1{margin:0 0 6px; font-size:24px}
    .profit{font-weight:700; font-size:40px; color:#111; margin:8px 0 18px}
    .muted{color:var(--muted)}
    .controls{display:flex; gap:8px; align-items:center; margin-bottom:14px}
    input[type="text"]{padding:10px 12px; border-radius:8px; border:1px solid #e3e7ee; flex:1; font-size:15px}
    button{background:var(--accent); color:white; border:0; padding:10px 14px; border-radius:8px; cursor:pointer; font-weight:600}
    button.secondary{background:#e9eefc; color:var(--accent); font-weight:600}
    .status{margin-top:8px; font-size:15px}
    .small{font-size:13px; color:var(--muted)}
    .share{margin-top:12px; display:flex; gap:8px; align-items:center}
    .linkbox{background:#f3f6fb; padding:8px 10px; border-radius:8px; font-size:13px; color:#0b5cff; overflow:auto}
    form{width:100%; display:flex; gap:8px; align-items:center}
  </style>
</head>
<body>
  <div class="card" role="main" aria-labelledby="title">
    <h1 id="title">Invest1 — Demo</h1>
    <div class="muted small">Showing the profit and a simple public sign-in (no password)</div>

    <div style="margin-top:18px">
      <div class="profit" id="profit">Profit: 431,000k pesos</div>
      <div class="small">This number is shown exactly as requested.</div>
    </div>

    <div style="margin-top:18px">
      <label class="small" for="nameInput">Enter your name and press Sign in (anyone can sign in)</label>

      <!-- Sign-in form: pressing Enter will submit -->
      <form id="signForm" aria-label="Sign in form" onsubmit="return false;">
        <input type="text" id="nameInput" name="name" placeholder="Type your name..." aria-label="Name" autocomplete="name" />
        <button id="signBtn" type="submit">Sign in</button>
        <button id="clearBtn" type="button" class="secondary">Sign out</button>
      </form>

      <div class="status" id="status">Not signed in</div>

      <div class="share">
        <button id="copyBtn" class="secondary" type="button">Copy share link</button>
        <div class="linkbox" id="linkBox">Share link will appear here</div>
      </div>

      <div style="margin-top:12px" class="small">Tip: The share link will include the name as a URL parameter so others can open the page and see the same signed-in name.</div>
    </div>
  </div>

  <script>
    // Elements
    const signForm = document.getElementById('signForm');
    const nameInput = document.getElementById('nameInput');
    const signBtn = document.getElementById('signBtn');
    const status = document.getElementById('status');
    const linkBox = document.getElementById('linkBox');
    const copyBtn = document.getElementById('copyBtn');
    const clearBtn = document.getElementById('clearBtn');

    // Update UI based on name
    function updateUI(name) {
      if (name) {
        status.textContent = 'Signed in as ' + name;
        nameInput.value = name;
      } else {
        status.textContent = 'Not signed in';
        nameInput.value = '';
      }
      const base = location.origin + location.pathname;
      const share = name ? base + '?name=' + encodeURIComponent(name) : base;
      linkBox.textContent = share;
    }

    // Sign-in action
    function signIn() {
      const name = nameInput.value.trim();
      if (!name) {
        alert('Type your name first');
        nameInput.focus();
        return;
      }
      localStorage.setItem('invest1_name', name);
      updateUI(name);
      // Update the URL param without reloading
      const url = new URL(location.href);
      url.searchParams.set('name', name);
      history.replaceState(null, '', url.toString());
      // Small UX feedback
      signBtn.textContent = 'Signed';
      setTimeout(() => { signBtn.textContent = 'Sign in'; }, 1200);
    }

    // Sign-out action
    function signOut() {
      localStorage.removeItem('invest1_name');
      const url = new URL(location.href);
      url.searchParams.delete('name');
      history.replaceState(null, '', url.toString());
      updateUI('');
    }

    // Load stored name or from URL on init
    function loadName() {
      const urlParams = new URLSearchParams(location.search);
      const urlName = urlParams.get('name');
      const stored = localStorage.getItem('invest1_name');
      const name = urlName || stored || '';
      if (name) localStorage.setItem('invest1_name', name);
      updateUI(name);
    }

    // Copy share link
    copyBtn.addEventListener('click', async () => {
      try {
        await navigator.clipboard.writeText(linkBox.textContent);
        copyBtn.textContent = 'Copied!';
        setTimeout(() => { copyBtn.textContent = 'Copy share link'; }, 1400);
      } catch (e) {
        alert('Copy failed — select and copy the link manually.');
      }
    });

    // Wire form submit and buttons
    signForm.addEventListener('submit', (e) => {
      e.preventDefault();
      signIn();
    });

    signBtn.addEventListener('click', (e) => {
      // in case button click triggers separately
      e.preventDefault();
      signIn();
    });

    clearBtn.addEventListener('click', () => {
      signOut();
    });

    // Initialize
    loadName();
  </script>
</body>
</html>
