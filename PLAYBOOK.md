# WebMelior — Client Site Playbook

> Knowledge base built from the WebMelior personal site.
> Read this INSTEAD of looking at `clients/home-services-demo/` when building client sites.
> These are reusable patterns — not brand assets.

---

## ⚡ Start of every client project (checklist)

- [ ] Read `PROJECTS.md` — confirm which client folder we're working in
- [ ] Invoke `/ui-ux-pro-max` — loads design intelligence
- [ ] Check `clients/[client-name]/brand_assets/` — use their logo/colors if provided
- [ ] Ask for brand colors if none exist yet (do not invent them)
- [ ] Never run `/frontend-design` — that skill is WebMelior personal brand only

---

## 🎨 Design system tokens (copy and adapt per client)

```css
:root {
  /* Replace these with the client's brand colors */
  --primary:       #004331;   /* darkest brand color */
  --primary-mid:   #0D5C46;   /* main CTA / interactive color */
  --primary-light: #1A9A74;   /* lighter accent */
  --on-primary:    #FDFCF8;   /* text on dark backgrounds */

  --surface:           #FDFCF8;
  --surface-bg:        #faf9f5;
  --surface-container: #efeeea;
  --surface-high:      #e9e8e4;

  --text-dark:   #1b1c1a;
  --text-mid:    #3f4944;
  --text-subtle: #6f7974;

  --accent:      #9FE1CB;   /* highlight / badge dots */
  --mint-light:  #E1F5EE;   /* icon backgrounds */
  --cta-gold:    #D4AF37;   /* high-conversion CTA variant */

  --radius-sm: 2px;
  --radius:    4px;
  --radius-md: 6px;
  --radius-lg: 8px;
  --radius-xl: 12px;

  --shadow-card: 0 1px 4px rgba(45,55,72,0.06), 0 4px 16px rgba(45,55,72,0.06);
  --shadow-btn:  0 1px 3px rgba(0,67,49,0.16), 0 4px 14px rgba(0,67,49,0.14);
  --shadow-lg:   0 4px 24px rgba(45,55,72,0.08), 0 16px 48px rgba(45,55,72,0.06);
}
```

---

## 🔤 Typography

- **Headings:** `Libre Caslon Text` (serif) — `letter-spacing: -0.02em`
- **Body:** `Hanken Grotesk` (sans) — `line-height: 1.7`
- **Google Fonts import:**
```html
<link href="https://fonts.googleapis.com/css2?family=Libre+Caslon+Text:ital,wght@0,400;0,700;1,400&family=Hanken+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet"/>
```
- Section titles: `font-size: clamp(2rem, 4.5vw, 3.25rem)`
- Never use the same font for headings and body

---

## 📐 Grid & layout classes

```css
.grid-2 { display: grid; grid-template-columns: repeat(2,1fr); gap: 20px; }
.grid-3 { display: grid; grid-template-columns: repeat(3,1fr); gap: 20px; }
.grid-4 { display: grid; grid-template-columns: repeat(4,1fr); gap: 20px; }
.container    { max-width: 1280px; margin: 0 auto; }
.container-sm { max-width: 820px;  margin: 0 auto; }
.section      { padding: 80px 24px; }
```

> ⚠️ **Never use inline `grid-template-columns` for responsive grids.**
> Inline styles can't be overridden by media queries.
> Always use a CSS class so breakpoints work.

---

## 📱 Mobile breakpoints

```css
@media (max-width: 1024px) { /* tablet adjustments */ }
@media (max-width: 900px)  { /* hero stacks, hide hero visual */ }
@media (max-width: 768px)  {
  .grid-2, .grid-3, .grid-4 { grid-template-columns: 1fr; }
  .stats-bar                 { grid-template-columns: repeat(2,1fr); }
  .nav-links, .nav-phone     { display: none; }
  .hamburger                 { display: flex; }
  .section                   { padding: 56px 20px; }
}
@media (max-width: 480px) {
  .section-title { font-size: 1.85rem; }
  .stat-num      { font-size: 1.8rem; }
}
```

---

## 🧩 Reusable components

### Sticky nav (hide on scroll down, show on scroll up)
```html
<nav class="site-nav">
  <div class="nav-inner">
    <!-- logo | nav links | CTA button | hamburger -->
  </div>
  <div class="mobile-menu" id="mobileMenu">
    <!-- same links, stacked -->
  </div>
</nav>
```
```js
// Scroll-hide nav
(function(){
  var n=document.querySelector(".site-nav"),l=0;
  window.addEventListener("scroll",function(){
    var y=window.scrollY;
    if(y>l&&y>64) n.classList.add("nav-hidden");
    else n.classList.remove("nav-hidden");
    l=y;
  },{passive:true});
})();
```

### Section badge
```html
<div class="section-badge"><span class="dot"></span>Label text</div>
```

### Stats bar (4-col → 2-col on mobile)
```html
<div class="stats-bar">
  <div class="stat-cell">
    <div class="stat-num">30+</div>
    <div class="stat-label">Label</div>
  </div>
  <!-- repeat × 4 -->
</div>
```

### FAQ accordion
```html
<div class="faq-item">
  <button class="faq-q" aria-expanded="false">
    Question text
    <svg><!-- chevron --></svg>
  </button>
  <div class="faq-a">Answer text</div>
</div>
```
```js
document.querySelectorAll('.faq-q').forEach(btn => {
  btn.addEventListener('click', () => {
    const item = btn.closest('.faq-item');
    const open = item.classList.contains('open');
    document.querySelectorAll('.faq-item').forEach(i => {
      i.classList.remove('open');
      i.querySelector('.faq-q').setAttribute('aria-expanded','false');
    });
    if(!open){ item.classList.add('open'); btn.setAttribute('aria-expanded','true'); }
  });
});
```

### Scroll reveal animation
```html
<div class="reveal"><!-- content --></div>
```
```js
const obs = new IntersectionObserver(e => e.forEach(x => {
  if(x.isIntersecting){ x.target.classList.add('revealed'); obs.unobserve(x.target); }
}), {threshold:.08});
document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
```

---

## 📅 Cal.com booking embed

```html
<!-- In <head> or before </body> -->
<script type="text/javascript">
  (function (C, A, L) { let p = function (a, ar) { a.q.push(ar); }; let d = C.document; C.Cal = C.Cal || function () { let cal = C.Cal; let ar = arguments; if (!cal.loaded) { cal.ns = {}; cal.q = cal.q || []; d.head.appendChild(d.createElement("script")).src = A; cal.loaded = true; } if (ar[0] === L) { const api = function () { p(api, arguments); }; const namespace = ar[1]; api.q = api.q || []; if(typeof namespace === "string"){cal.ns[namespace] = cal.ns[namespace] || api;p(cal.ns[namespace], ar);p(cal, ["initNamespace", namespace]);} else p(cal, ar); return;} p(cal, ar); }; })(window, "https://app.cal.com/embed/embed.js", "init");
  Cal("init", "book-a-free-call", {origin:"https://app.cal.com"});
  Cal.ns["book-a-free-call"]("ui", {"hideEventTypeDetails":false,"layout":"month_view","styles":{"branding":{"brandColor":"CLIENT_BRAND_COLOR"}}});
</script>

<!-- On any booking button -->
<a data-cal-link="CAL_USERNAME/book-a-free-call"
   data-cal-namespace="book-a-free-call"
   data-cal-config='{"layout":"month_view","useSlotsViewOnSmallScreen":"true"}'
   href="#"
   class="btn btn-primary">
  Book a Free Call
</a>
```
> Replace `CAL_USERNAME` and `CLIENT_BRAND_COLOR` per client.

---

## 📬 Contact form → Google Sheets

- Use Google Apps Script as a Web App endpoint
- Form submits via `fetch()` POST to the script URL
- Script appends a row to a Google Sheet
- Always wrap in `try/catch` and show success/error state to user
- Store the Apps Script URL in the HTML — it's not a secret but document it clearly

---

## 🚀 Vercel + GitHub deployment setup

1. Create GitHub repo for the client (`gh repo create [name] --public`)
2. Push initial files
3. Go to vercel.com → **Add New Project** → import from GitHub
4. Set **Output Directory** to `clients/[client-name]/site` (or root if standalone repo)
5. Deploy — Vercel auto-deploys on every push to `main` from that point

> Always use a **standalone GitHub repo per client** — never push client files to the WebMelior personal repo.

---

## ❌ Hard rules (never do these)

- Never use `transition-all`
- Never use default Tailwind blue/indigo as a primary color
- Never use inline `display:grid` with `grid-template-columns` for responsive layouts
- Never commit `.env` files or API keys
- Never copy content or brand assets from `clients/home-services-demo/` into a client project
- Never run `/frontend-design` for a client — it loads WebMelior's personal brand
- Never use `file:///` URLs for screenshots — always use `localhost` via `node serve.mjs`

---

## 📸 Screenshot workflow

```powershell
# Terminal 1 — start server (from the client's site folder)
node ../../../serve.mjs

# Terminal 2 — take screenshot
node ../../../screenshot.mjs http://localhost:3000
node ../../../screenshot.mjs http://localhost:3000 label
```
Screenshots save to `./temporary screenshots/screenshot-N.png`
Minimum 2 comparison rounds before calling a UI task done.

---

*Last updated: 2026-07-09 · Add new patterns here as they're built*
