# 67xw.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Cleaner — Discord Bot</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #2e2e32;
      --bg2: #26262a;
      --bg3: #1e1e21;
      --surface: #35353a;
      --surface2: #3d3d43;
      --accent: #a8a8b0;
      --accent2: #c8c8d4;
      --white: #f0f0f2;
      --muted: #7a7a84;
      --border: rgba(255,255,255,0.08);
      --cmd: #e8e0ff;
      --cmd-bg: rgba(168,160,220,0.12);
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg3);
      color: var(--white);
      font-family: 'DM Sans', sans-serif;
      font-weight: 400;
      line-height: 1.7;
      overflow-x: hidden;
    }

    /* NAV */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 clamp(1.5rem, 5vw, 5rem);
      height: 64px;
      background: rgba(30,30,33,0.85);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
    }
    .nav-logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.6rem;
      letter-spacing: 0.12em;
      color: var(--white);
      display: flex;
      align-items: center;
      gap: 10px;
      text-decoration: none;
    }
    .nav-logo svg { width: 26px; height: 26px; opacity: 0.85; }
    .nav-links { display: flex; gap: 2rem; }
    .nav-links a {
      color: var(--muted);
      text-decoration: none;
      font-size: 0.875rem;
      font-weight: 500;
      letter-spacing: 0.04em;
      transition: color 0.2s;
    }
    .nav-links a:hover { color: var(--white); }

    /* HERO */
    .hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 6rem 2rem 4rem;
      position: relative;
      overflow: hidden;
    }
    .hero::before {
      content: '';
      position: absolute;
      inset: 0;
      background: radial-gradient(ellipse 60% 50% at 50% 40%, rgba(150,145,170,0.07) 0%, transparent 70%);
      pointer-events: none;
    }
    .broom-wrap {
      width: 100px;
      height: 100px;
      margin-bottom: 2rem;
      animation: floatBroom 4s ease-in-out infinite;
    }
    @keyframes floatBroom {
      0%, 100% { transform: translateY(0) rotate(-3deg); }
      50% { transform: translateY(-12px) rotate(3deg); }
    }
    .hero h1 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(4.5rem, 12vw, 9rem);
      letter-spacing: 0.1em;
      color: var(--white);
      line-height: 1;
      margin-bottom: 1rem;
    }
    .hero-sub {
      font-size: clamp(1rem, 2.5vw, 1.25rem);
      color: var(--muted);
      max-width: 480px;
      margin-bottom: 2.5rem;
      font-weight: 300;
    }
    .hero-badge {
      display: inline-block;
      background: var(--cmd-bg);
      border: 1px solid rgba(168,160,220,0.2);
      color: var(--cmd);
      font-size: 0.78rem;
      font-weight: 500;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: 0.4rem 1rem;
      border-radius: 2rem;
      margin-bottom: 2.5rem;
    }
    .scroll-hint {
      position: absolute;
      bottom: 2.5rem;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 6px;
      color: var(--muted);
      font-size: 0.75rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      animation: fadeInUp 1.5s 1s both;
    }
    .scroll-hint span { display: block; width: 1px; height: 40px; background: var(--border); margin: 0 auto; animation: lineGrow 1.5s 1.5s ease both; transform-origin: top; }
    @keyframes lineGrow { from { transform: scaleY(0); } to { transform: scaleY(1); } }
    @keyframes fadeInUp { from { opacity: 0; transform: translate(-50%, 12px); } to { opacity: 1; transform: translate(-50%, 0); } }

    /* SECTIONS */
    section {
      max-width: 860px;
      margin: 0 auto;
      padding: clamp(4rem, 8vw, 7rem) 2rem;
    }
    .section-label {
      display: block;
      font-size: 0.7rem;
      font-weight: 600;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 0.75rem;
    }
    section h2 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(2.4rem, 5vw, 3.5rem);
      letter-spacing: 0.08em;
      color: var(--white);
      margin-bottom: 2rem;
      line-height: 1.1;
    }
    section p {
      color: #9b9ba6;
      font-size: 0.97rem;
      margin-bottom: 1.1rem;
      max-width: 680px;
    }
    section p strong { color: var(--accent2); font-weight: 500; }

    /* DIVIDER */
    .divider {
      max-width: 860px;
      margin: 0 auto;
      height: 1px;
      background: var(--border);
    }

    /* COMMANDS */
    #commands { padding-bottom: clamp(4rem, 8vw, 7rem); }
    .cmd-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1px;
      background: var(--border);
      border: 1px solid var(--border);
      border-radius: 14px;
      overflow: hidden;
      margin-top: 0.5rem;
    }
    .cmd-card {
      background: var(--surface);
      padding: 1.5rem 1.75rem;
      transition: background 0.2s;
      position: relative;
    }
    .cmd-card:hover { background: var(--surface2); }
    .cmd-name {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.5rem;
      letter-spacing: 0.12em;
      color: var(--cmd);
      margin-bottom: 0.5rem;
    }
    .cmd-desc {
      font-size: 0.875rem;
      color: #8888a0;
      line-height: 1.55;
    }
    .cmd-tag {
      display: inline-block;
      background: rgba(168,160,220,0.1);
      border: 1px solid rgba(168,160,220,0.15);
      color: #9090c0;
      font-size: 0.65rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      font-weight: 600;
      padding: 0.2rem 0.55rem;
      border-radius: 2rem;
      margin-bottom: 0.85rem;
    }

    /* FOOTER */
    footer {
      background: var(--bg3);
      border-top: 1px solid var(--border);
      text-align: center;
      padding: 2.5rem 2rem;
      color: var(--muted);
      font-size: 0.8rem;
      letter-spacing: 0.04em;
    }
    footer a { color: var(--muted); text-decoration: none; transition: color 0.2s; }
    footer a:hover { color: var(--white); }

    /* ANIMATIONS */
    .fade-in {
      opacity: 0;
      transform: translateY(20px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }
    .fade-in.visible {
      opacity: 1;
      transform: none;
    }

    @media (max-width: 600px) {
      .nav-links { display: none; }
      .cmd-grid { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>

  <nav>
    <a class="nav-logo" href="#">
      <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M14 2L8 14H4l2 8 6-10h4l-2-10z" fill="currentColor" opacity="0.9"/>
      </svg>
      Cleaner
    </a>
    <div class="nav-links">
      <a href="#commands">Commands</a>
      <a href="#tos">Terms</a>
      <a href="#privacy">Privacy</a>
    </div>
  </nav>

  <!-- HERO -->
  <div class="hero">
    <div class="broom-wrap">
      <svg viewBox="0 0 100 120" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect x="54" y="2" width="10" height="55" rx="5" transform="rotate(20 54 2)" fill="#a0a0b0"/>
        <rect x="42" y="50" width="14" height="6" rx="3" fill="#8888a0"/>
        <path d="M18 65 Q30 58 55 62 Q70 65 80 80 Q60 88 38 86 Q20 82 18 65Z" fill="#b0b0c4"/>
        <line x1="38" y1="86" x2="35" y2="105" stroke="#9090a8" stroke-width="3" stroke-linecap="round"/>
        <line x1="50" y1="88" x2="48" y2="108" stroke="#9090a8" stroke-width="3" stroke-linecap="round"/>
        <line x1="62" y1="86" x2="61" y2="106" stroke="#9090a8" stroke-width="3" stroke-linecap="round"/>
        <line x1="74" y1="82" x2="74" y2="102" stroke="#9090a8" stroke-width="3" stroke-linecap="round"/>
      </svg>
    </div>

    <div class="hero-badge">Discord Bot</div>
    <h1>Cleaner</h1>
    <p class="hero-sub">Keep your server spotless. Purge spam, block scams, and automate message cleanup — all with a single prefix.</p>

    <div class="scroll-hint">
      Scroll
      <span></span>
    </div>
  </div>

  <!-- COMMANDS -->
  <section id="commands" class="fade-in">
    <span class="section-label">What it does</span>
    <h2>Commands &amp; Functions</h2>

    <div class="cmd-grid">

      <div class="cmd-card">
        <div class="cmd-tag">Moderation</div>
        <div class="cmd-name">/banpot</div>
        <p class="cmd-desc">Creates a dedicated channel that detects and blocks MrBeast scam bots and NSFW content — spammers get kicked automatically before they cause damage.</p>
      </div>

      <div class="cmd-card">
        <div class="cmd-tag">Cleanup</div>
        <div class="cmd-name">/purge</div>
        <p class="cmd-desc">Bulk-delete any number of messages in the current channel instantly. Just pass the count and Cleaner takes care of the rest.</p>
      </div>

      <div class="cmd-card">
        <div class="cmd-tag">Automation</div>
        <div class="cmd-name">/clean</div>
        <p class="cmd-desc">Start an automated sweep that continuously removes messages older than a date you choose — keeping channels fresh without any manual effort.</p>
      </div>

      <div class="cmd-card">
        <div class="cmd-tag">Config</div>
        <div class="cmd-name">/prefix</div>
        <p class="cmd-desc">Change the bot's command prefix to whatever fits your server's style. Customize once and every command follows the new prefix.</p>
      </div>

      <div class="cmd-card">
        <div class="cmd-tag">Help</div>
        <div class="cmd-name">/help</div>
        <p class="cmd-desc">Displays all available commands with their descriptions, usage examples, and required permissions — the quick reference you always need.</p>
      </div>

    </div>
  </section>

  <div class="divider"></div>

  <!-- TERMS OF SERVICE -->
  <section id="tos" class="fade-in">
    <span class="section-label">Legal</span>
    <h2>Terms of Service</h2>
    <p><strong>Last updated: 2025</strong></p>
    <p>By adding Cleaner to your Discord server, you agree to these Terms of Service. If you do not agree, please remove the bot from your server immediately.</p>

    <p><strong>1. Acceptable Use</strong><br>
    Cleaner is provided to help moderate Discord servers. You agree not to use the bot for any unlawful purpose, to harass individuals, or to violate Discord's own Terms of Service. Any abuse of the bot's features may result in permanent blacklisting.</p>

    <p><strong>2. Server Owner Responsibility</strong><br>
    The server owner and administrators are solely responsible for how Cleaner is configured and used within their server. We are not liable for moderation actions taken by the bot based on configurations set by your team.</p>

    <p><strong>3. Availability</strong><br>
    We do our best to keep Cleaner online and functional at all times, but we do not guarantee uninterrupted service. The bot may be taken offline for maintenance, updates, or unforeseen issues without prior notice.</p>

    <p><strong>4. Changes to Terms</strong><br>
    These terms may be updated at any time. Continued use of the bot after changes are posted constitutes your acceptance of the revised terms.</p>

    <p><strong>5. Termination</strong><br>
    We reserve the right to terminate or restrict access to Cleaner for any server or user at our sole discretion, particularly in cases of abuse or violation of these terms.</p>
  </section>

  <div class="divider"></div>

  <!-- PRIVACY POLICY -->
  <section id="privacy" class="fade-in">
    <span class="section-label">Your data</span>
    <h2>Privacy Policy</h2>
    <p><strong>Last updated: 2025</strong></p>
    <p>We take your privacy seriously. This policy explains what data Cleaner collects and how it is used.</p>

    <p><strong>1. Data We Collect</strong><br>
    Cleaner collects only what is strictly necessary to function: server IDs, channel IDs, and command configuration preferences (such as custom prefixes and clean schedules). We do not store the content of messages that are deleted.</p>

    <p><strong>2. How Data Is Used</strong><br>
    Collected data is used exclusively to provide and improve the bot's features within your Discord server. We do not sell, share, or monetize any data.</p>

    <p><strong>3. Data Storage</strong><br>
    Configuration data is stored securely and retained only as long as Cleaner is active in your server. When you remove the bot, your server's data is deleted within 30 days.</p>

    <p><strong>4. Third Parties</strong><br>
    Cleaner does not share your data with third-party services. The bot operates solely within the Discord platform and complies with Discord's Developer Terms of Service.</p>

    <p><strong>5. Your Rights</strong><br>
    You may request the deletion of all data associated with your server at any time by contacting us. We will process your request promptly.</p>

    <p><strong>6. Contact</strong><br>
    If you have questions or concerns about this policy, reach out to the bot developer on Discord.</p>
  </section>

  <!-- FOOTER -->
  <footer>
    <p style="margin-bottom: 0.5rem;">
      <a href="#tos">Terms of Service</a> &nbsp;·&nbsp;
      <a href="#privacy">Privacy Policy</a> &nbsp;·&nbsp;
      <a href="#commands">Commands</a>
    </p>
    <p>© 2025 Cleaner Bot — All rights reserved.</p>
  </footer>

  <script>
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
    }, { threshold: 0.1 });
    document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));
  </script>
</body>
</html>
