# new1


/* =========================================================
   CHATGPT "TERMINAL HACKER" THEME (Stylus) — CORRECTED
   - Keeps mode picker (Quick/Extended/etc) FUNCTIONAL
   - Edge-to-edge center chat
   - Hacker “code wall” background WITHOUT pseudo-element conflicts
   - Boxy terminal look + CRT scanlines + vignette
   Apply to: https://chatgpt.com/*
   ========================================================= */

/* --------- Core palette & knobs --------- */
:root{
  --t-bg: #020402;
  --t-panel: #040905;
  --t-panel-2: #07110a;

  --t-text: #b7ffd0;
  --t-dim: #73d49a;

  --t-green: #00ff66;
  --t-green-2: #2dff7b;

  --t-border: rgba(0, 255, 102, 0.30);
  --t-border-soft: rgba(0, 255, 102, 0.18);

  --t-code-bg: #03110a;

  --t-radius: 0px;            /* boxy */
  --t-shadow: 0 0 0 1px var(--t-border-soft), 0 14px 40px rgba(0,0,0,0.78);

  --t-font: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono","Courier New", monospace;

  --t-focus: rgba(0, 255, 102, 0.55);
  --t-selection: rgba(0, 255, 102, 0.28);

  /* background effects */
  --codewall-opacity: 0.14;   /* 0.10-0.22 looks good */
  --codewall-blur: 0px;       /* try 0.6px for softer */
}

/* --------- Base --------- */
html, body{
  background: var(--t-bg) !important;
  color: var(--t-text) !important;
  font-family: var(--t-font) !important;
  letter-spacing: 0.2px;
  text-rendering: geometricPrecision;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

::selection{
  background: var(--t-selection) !important;
  color: #001b0a !important;
}

/* Boxy everything */
*{
  border-radius: 0px !important;
  border-color: var(--t-border-soft) !important;
}

/* Links */
a, a:visited{
  color: var(--t-green) !important;
  text-decoration: none !important;
}
a:hover{
  color: var(--t-green-2) !important;
  text-decoration: underline !important;
}

/* Remove soft blur effects */
[class*="shadow"], [class*="backdrop"], [class*="blur"]{
  box-shadow: none !important;
  backdrop-filter: none !important;
}

/* --------- Branding removal (best-effort) --------- */
header,
header *[aria-label*="ChatGPT" i],
header *[title*="ChatGPT" i],
a[href*="openai.com" i],
a[href*="chatgpt" i],
img[alt*="ChatGPT" i],
svg[aria-label*="ChatGPT" i],
svg[title*="ChatGPT" i],
[data-testid*="app-header" i],
[data-testid*="appHeader" i],
nav a[aria-label*="ChatGPT" i],
nav a[title*="ChatGPT" i]{
  display: none !important;
  visibility: hidden !important;
}

/* Do NOT hide things broadly by “model/mode” labels — that breaks mode picker */

/* --------- Layout surfaces --------- */
main, [role="main"]{
  background: transparent !important;
  width: 100% !important;
  max-width: none !important;
}

main > div, [role="main"] > div{
  width: 100% !important;
  max-width: none !important;
}

/* Remove common width caps */
.prose, [class*="prose"]{ max-width: none !important; }
[class*="max-w-"], [class*="maxw"], [class*="container"]{ max-width: none !important; }

/* Sidebars */
aside, nav, [data-testid*="sidebar" i], [class*="sidebar" i], [class*="drawer" i]{
  background: var(--t-panel) !important;
  border-right: 1px solid var(--t-border-soft) !important;
}

/* Dialogs / menus */
[role="dialog"], [role="menu"], [role="listbox"], [data-radix-popper-content-wrapper],
.popover, .menu{
  background: var(--t-panel-2) !important;
  color: var(--t-text) !important;
  border: 1px solid var(--t-border) !important;
  box-shadow: var(--t-shadow) !important;
}

/* Chat column “terminal window” */
main > div, [role="main"] > div{
  background: rgba(4, 9, 5, 0.40) !important;
  border: 1px solid var(--t-border-soft) !important;
  box-shadow: var(--t-shadow) !important;
}

/* Terminal header bar vibe */
main > div::before, [role="main"] > div::before{
  content: "terminal://session";
  display: block;
  padding: 10px 12px;
  color: var(--t-green-2);
  background: rgba(3, 12, 7, 0.95);
  border-bottom: 1px solid var(--t-border-soft);
  font-size: 12px;
  letter-spacing: 0.8px;
  text-transform: lowercase;
}

/* Messages */
article, [data-message-id], [class*="message" i]{
  background: transparent !important;
  border: none !important;
}

[data-message-author-role="user"]{
  border-left: 2px solid rgba(0, 255, 102, 0.45) !important;
  padding-left: 12px !important;
}
[data-message-author-role="assistant"]{
  border-left: 2px solid rgba(0, 255, 102, 0.18) !important;
  padding-left: 12px !important;
}

.prose, [class*="prose"]{
  color: var(--t-text) !important;
  font-family: var(--t-font) !important;
  line-height: 1.55 !important;
}
.prose strong, [class*="prose"] strong{
  color: var(--t-green-2) !important;
  font-weight: 700 !important;
}

hr{
  border: none !important;
  border-top: 1px dashed rgba(0, 255, 102, 0.25) !important;
  opacity: 1 !important;
}

/* --------- Composer / input (keep functional) --------- */
form, [data-testid="composer"], [class*="composer" i], [class*="prompt" i]{
  background: rgba(3, 12, 7, 0.92) !important;
  border: 1px solid var(--t-border) !important;
  box-shadow: var(--t-shadow) !important;
}

/* Visual “>” prompt only (doesn't move buttons) */
form::before, [data-testid="composer"]::before{
  content: ">";
  position: absolute;
  left: 14px;
  top: 14px;
  color: var(--t-green-2);
  font-weight: 800;
  pointer-events: none;
}

/* Ensure relative so the prompt positions correctly */
form, [data-testid="composer"]{
  position: relative !important;
}

textarea, input[type="text"], input[type="search"]{
  background: transparent !important;
  color: var(--t-text) !important;
  border: none !important;
  caret-color: var(--t-green) !important;
  padding-left: 28px !important; /* room for ">" */
  font-family: var(--t-font) !important;
  box-shadow: none !important;
}

textarea::placeholder, input::placeholder{
  color: rgba(115, 212, 154, 0.75) !important;
}

textarea:focus, input:focus, button:focus, [role="button"]:focus{
  outline: 2px solid var(--t-focus) !important;
  outline-offset: 2px !important;
}

/* Buttons (style only; no reordering) */
button, [role="button"]{
  background: rgba(0, 255, 102, 0.06) !important;
  border: 1px solid rgba(0, 255, 102, 0.22) !important;
  color: var(--t-green-2) !important;
  text-transform: lowercase;
  letter-spacing: 0.6px;
}
button:hover, [role="button"]:hover{
  background: rgba(0, 255, 102, 0.10) !important;
  border-color: rgba(0, 255, 102, 0.32) !important;
}
button:disabled, [aria-disabled="true"]{
  opacity: 0.55 !important;
  cursor: not-allowed !important;
}

/* --------- Code blocks --------- */
pre{
  background: var(--t-code-bg) !important;
  color: var(--t-text) !important;
  border: 1px solid rgba(0, 255, 102, 0.22) !important;
  box-shadow: 0 0 0 1px rgba(0, 255, 102, 0.12) !important;
}
code{
  background: rgba(3, 17, 10, 0.9) !important;
  border: 1px solid rgba(0, 255, 102, 0.18) !important;
  padding: 0.15em 0.35em !important;
  color: var(--t-green) !important;
}

/* --------- Tables --------- */
table{
  border-collapse: separate !important;
  border-spacing: 0 !important;
  border: 1px solid rgba(0, 255, 102, 0.22) !important;
}
th, td{
  border-bottom: 1px solid rgba(0, 255, 102, 0.14) !important;
  padding: 10px 12px !important;
}
th{
  background: rgba(3, 12, 7, 0.95) !important;
  color: var(--t-green-2) !important;
}
tr:hover td{
  background: rgba(0, 255, 102, 0.05) !important;
}

/* --------- Scrollbars --------- */
*::-webkit-scrollbar{ width: 10px; height: 10px; }
*::-webkit-scrollbar-track{ background: rgba(3, 10, 6, 0.85); }
*::-webkit-scrollbar-thumb{
  background: rgba(0, 255, 102, 0.18);
  border: 1px solid rgba(0, 255, 102, 0.22);
}
*::-webkit-scrollbar-thumb:hover{ background: rgba(0, 255, 102, 0.28); }

/* Keep toggles/checkboxes visible */
input[type="checkbox"], input[type="radio"]{
  accent-color: var(--t-green-2) !important;
}

/* Tooltips */
[role="tooltip"]{
  background: rgba(7, 17, 10, 0.98) !important;
  color: var(--t-text) !important;
  border: 1px solid rgba(0, 255, 102, 0.22) !important;
  box-shadow: var(--t-shadow) !important;
}

/* =========================================================
   BACKGROUND EFFECTS (NO CONFLICTS)
   - Code wall on html::before (behind everything)
   - Scanlines on body::before (overlay)
   - Vignette on body::after (overlay)
   ========================================================= */

/* Code wall BEHIND the app */
html::before{
  content: "";
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 0;
  opacity: var(--codewall-opacity);
  filter: blur(var(--codewall-blur));

  background-image:
    url("data:image/svg+xml;utf8,\
<svg xmlns='http://www.w3.org/2000/svg' width='900' height='600'>\
<rect width='100%25' height='100%25' fill='%23020402'/>\
<g fill='none' stroke='%2300ff66' stroke-opacity='0.55' stroke-width='1'>\
<path d='M0 40 H900' opacity='0.12'/>\
<path d='M0 120 H900' opacity='0.10'/>\
<path d='M0 200 H900' opacity='0.10'/>\
<path d='M0 280 H900' opacity='0.10'/>\
<path d='M0 360 H900' opacity='0.10'/>\
<path d='M0 440 H900' opacity='0.10'/>\
<path d='M0 520 H900' opacity='0.10'/>\
</g>\
<g font-family='ui-monospace, Menlo, Consolas, monospace' font-size='14' fill='%2300ff66' fill-opacity='0.55'>\
<text x='24' y='60'>if (token &amp;&amp; stage === &quot;prod&quot;) { return; }</text>\
<text x='24' y='90'>const mask = (1 &lt;&lt; i); // bit</text>\
<text x='24' y='150'>for (let k = 0; k &lt; n; k++) sum += a[k];</text>\
<text x='24' y='180'>SELECT city, lat, lng FROM geo WHERE name LIKE ?;</text>\
<text x='24' y='240'>function encrypt(x){ return (x ^ 0x5a) + 13; }</text>\
<text x='24' y='270'>ssh -i key.pem user@10.0.0.12</text>\
<text x='24' y='330'>kubectl get pods -A | grep gateway</text>\
<text x='24' y='360'>curl -s https://api/... | jq '.data[]'</text>\
<text x='24' y='420'>try { await fetch(url) } catch (e) { log(e) }</text>\
<text x='24' y='450'>[OK] authz::verified  [WARN] rate-limit=near</text>\
<text x='24' y='510'>// build: stable | deploy: green | region: yyz</text>\
<text x='24' y='540'>INSERT INTO audit(event, ts) VALUES('login', now());</text>\
</g>\
</svg>");
  background-size: 900px 600px;
  background-repeat: repeat;
}

/* Ensure app stays above code wall */
#root, main, [role="main"], header, aside, nav, [role="dialog"], [role="menu"]{
  position: relative !important;
  z-index: 1 !important;
}

/* Slightly darken panels for readability */
main > div, [role="main"] > div,
aside, nav, [data-testid*="sidebar" i]{
  background: rgba(2, 4, 2, 0.72) !important;
}

/* Scanlines overlay */
body::before{
  content:"";
  position: fixed;
  inset: 0;
  pointer-events: none;
  background:
    repeating-linear-gradient(
      to bottom,
      rgba(0, 255, 102, 0.025),
      rgba(0, 255, 102, 0.025) 1px,
      rgba(0,0,0,0) 3px,
      rgba(0,0,0,0) 6px
    );
  mix-blend-mode: overlay;
  opacity: 0.16;
  z-index: 999999;
}

/* Vignette overlay */
body::after{
  content:"";
  position: fixed;
  inset: -20%;
  pointer-events: none;
  background: radial-gradient(ellipse at center,
    rgba(0,0,0,0) 0%,
    rgba(0,0,0,0.35) 55%,
    rgba(0,0,0,0.75) 100%);
  opacity: 0.9;
  z-index: 999998;
}





/* =========================
   FIX: bring back model selector (GPT-4o / o1 / etc)
   Paste at VERY BOTTOM
   ========================= */

/* 1) Your theme hides a lot of links/icons broadly.
      This restores the top-left header / model switcher area. */
header,
[data-testid*="app-header" i],
[data-testid*="appHeader" i]{
  display: flex !important;
  visibility: visible !important;
}

/* 2) Restore anything that might be hidden because it contains "chatgpt/openai" */
header a,
header button,
header svg,
header img,
header [role="button"]{
  display: inline-flex !important;
  visibility: visible !important;
  pointer-events: auto !important;
}

/* 3) Specifically UNHIDE these (your old rules hid them) */
header *[aria-label*="ChatGPT" i],
header *[title*="ChatGPT" i],
nav a[aria-label*="ChatGPT" i],
nav a[title*="ChatGPT" i],
a[href*="openai.com" i],
a[href*="chatgpt" i],
img[alt*="ChatGPT" i],
svg[aria-label*="ChatGPT" i],
svg[title*="ChatGPT" i]{
  display: inline-flex !important;
  visibility: visible !important;
  pointer-events: auto !important;
}

/* 4) Make sure it sits top-left and above overlays */
header{
  position: sticky !important;
  top: 0 !important;
  left: 0 !important;
  z-index: 1000000 !important;
  background: rgba(2, 4, 2, 0.85) !important;
  border-bottom: 1px solid rgba(0, 255, 102, 0.22) !important;
}

/* 5) Ensure the model selector dropdown isn't clipped */
header *{
  overflow: visible !important;
}
