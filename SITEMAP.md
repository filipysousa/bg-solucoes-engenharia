# BG Soluções e Engenharia — Site Reference

> Single-file institutional website. All CSS and JS are inline inside `index.html`.  
> No frameworks, no build step, no dependencies beyond Google Fonts.  
> Last updated: 2026-04-27

---

## Business

| Field | Value |
|---|---|
| Company | BG Soluções e Engenharia |
| Owner | Bruno Evaristo |
| Sector | Mechanical engineering & industrial safety |
| Location | Rua Cônego Braveza, 770 — Fortaleza, CE, Brazil |
| Phone | +55 85 9 9997-1426 |
| WhatsApp | https://wa.me/5585999971426 |
| Email | bgsolucoeseengenharia@gmail.com |
| GitHub | https://github.com/filipysousa/bg-solucoes-engenharia |

---

## File Structure

```
/
├── index.html                        ← entire site (HTML + CSS + JS)
├── .cpanel.yml                       ← Hostgator cPanel auto-deploy config
├── SITEMAP.md                        ← this file
├── img/
│   ├── medicao-espessura-nr13.jpeg   ← technicians inside pressure vessel measuring wall thickness (NR13)
│   ├── trabalho-altura-nr35.jpeg     ← team on scissor lift working at height with harnesses (NR35)
│   ├── end-lp-anel-trinca.jpeg       ← close-up of metal ring with red liquid penetrant revealing crack (END/LP)
│   ├── enfardadeira-nr12.jpeg        ← worker operating hydraulic baling press (NR12)
│   ├── projeto-cad-solidworks.jpeg   ← SolidWorks screen with 3D gearbox assembly model
│   ├── icamento-vaso-guindaste-nr13.jpeg ← pressure vessel being lifted by crane at industrial plant (NR13)
│   ├── motor-protecao-nr12.jpeg      ← industrial motor with orange casing and safety chain (NR12)
│   ├── protecao-coletiva-nr12-a.jpeg ← orange guard installed on machine over metal grating (NR12)
│   ├── protecao-coletiva-nr12-b.jpeg ← orange guard on motor base with mesh screen (NR12)
│   ├── protecao-transmissao-nr12.jpeg ← curved orange guard covering belt/pulley transmission (NR12)
│   ├── inspecao-prensa-nr12.jpeg     ← PPE-equipped operator at large green industrial press (NR12)
│   ├── end-lp-gancho-a.jpeg          ← lifting hook with pink liquid penetrant on work table (END/LP)
│   ├── end-lp-setup-completo.jpeg    ← full END workstation: hooks, chains, LP spray cans (Metal-Chek D70) (END/LP)
│   ├── end-lp-gancho-b.jpeg          ← hook BS05 with LP revealing indications (END/LP)
│   ├── vasos-pressao-nr13.jpeg       ← green fiberglass pressure vessels in industrial installation (NR13)
│   └── manometro-vaso-nr13.jpeg      ← pressure gauge (manometer) between pressure vessels (NR13)
└── video/
    └── medicao-espessura-nr13.mp4    ← footage of ultrasound thickness measurement inside pressure vessel (NR13)
```

---

## Tech Stack

| Item | Detail |
|---|---|
| Structure | Single `index.html` — no separate CSS/JS files |
| Fonts | Google Fonts: `Barlow` (body) + `Barlow Condensed` (headings/display) |
| Favicon | Inline SVG data URI — ⚙ gear emoji |
| Responsive breakpoint | `max-width: 860px` |
| Scroll | Native `scroll-behavior: smooth` |
| Deployment | Git → GitHub → cPanel Git Version Control (Hostgator) → `public_html/` |

---

## Design System

### CSS Variables (`:root`)

| Variable | Value | Usage |
|---|---|---|
| `--green` | `#2a7a2a` | Primary brand green |
| `--green-l` | `#3a9a3a` | Hover state green |
| `--green-d` | `#1a5a1a` | Dark green (stats bar, dif-box bg) |
| `--black` | `#0e0e0e` | Page background |
| `--dark` | `#161616` | Alternate dark sections |
| `--gray` | `#242424` | Medium gray sections |
| `--gray2` | `#2e2e2e` | Card backgrounds |
| `--white` | `#fff` | Text |
| `--acc` | `#4caf50` | Accent green (highlights, tags, links) |
| `--acc2` | `#81c784` | Light accent (badge text) |

### Typography

| Use | Font | Weight | Style |
|---|---|---|---|
| Body text | Barlow | 300, 400, 500, 600 | — |
| Headlines, display | Barlow Condensed | 400, 600, 700, 800 | uppercase |
| Hero h1 | Barlow Condensed | 800 | `clamp(44px, 6.5vw, 82px)` |
| Section titles `.s-title` | Barlow Condensed | 700 | `clamp(30px, 4vw, 50px)` |

---

## Page Sections (top to bottom)

### 1. `<nav>` — Fixed Navigation
- Height: 68px, `z-index: 200`, backdrop blur
- Logo: `BG Soluções e Engenharia` (`.nav-brand`)
- Links: Serviços · Diferenciais · Sobre · Contato
- CTA button: "Solicitar Orçamento" → WhatsApp
- Mobile: hamburger button (`.ham`) shows/hides vertical menu
- JS: menu closes on outside click and on anchor link click; navbar darkens on scroll > 60px

### 2. `.hero` — Hero Section
- Full viewport height (`min-height: 100vh`)
- **Left** (`.hero-content`): badge + h1 + subtitle + 2 CTA buttons
  - Primary CTA: WhatsApp (`.btn-wa`)
  - Secondary CTA: "Ver Serviços ↓" → `#servicos` (`.btn-ghost`)
- **Right** (`.hero-deck-outer`): photo deck slideshow (hidden on mobile)
- Background: `--black` + subtle green grid pattern (`::before`) + green radial glow (`.hero-glow`)

#### Hero Deck (Photo Slideshow)
- Container: `#heroDeck` (`480px × 600px`)
- 16 cards stacked with CSS transforms (`.deck-card`)
- Positions: `pos-0` (front) → `pos-1` → `pos-2` → `pos-back` (hidden)
- Auto-advances every **3.8 seconds**
- Navigation: `#deckPrev` / `#deckNext` buttons + counter `#deckCounter`
- Interactions: click `pos-1` card advances; mouse drag (threshold 60px); touch swipe (threshold 55px)
- During drag: front card follows cursor (rotate + translateX, no transition)
- Images: all 16 from `img/` (first 3 `loading="eager"`, rest `loading="lazy"`)

### 3. `.stats-bar` — NR Highlights Bar
- 4-column grid, green-dark background
- Displays: NR 11, NR 12, NR 13, NR 35

### 4. `#servicos` — Services Section
- Background: `--dark`
- Grid: `repeat(auto-fill, minmax(290px, 1fr))`, gap 2px
- **8 service cards** (`.srv`), each with: image or blank placeholder → icon → NR tag → h3 → description → bullet list

| Card | Image | NR tag |
|---|---|---|
| Laudos e Relatórios de Engenharia | `medicao-espessura-nr13.jpeg` | NR 11/12/13 |
| Linhas de Vida e Ancoragem | placeholder 🪜 | NR 35 |
| Ensaios Não Destrutivos | `end-lp-anel-trinca.jpeg` | END |
| Planos de Manutenção | `enfardadeira-nr12.jpeg` | Gestão/Manutenção |
| Projetos Mecânicos e Industriais | placeholder ⚙️ | Projetos Mecânicos |
| Segurança Operacional e Análise de Risco | placeholder ⚠️ | Segurança |
| Eficiência Energética e Termodinâmica | placeholder 💡 | Eficiência Energética |
| Treinamentos Técnicos | placeholder 🎓 | Treinamentos |

- Cards with image use `.srv-img` (180px tall, bleeds to card edges with negative margins)
- Cards without image use `.srv-img-blank` (same dimensions, dark gradient + emoji, 25% opacity)

### 5. `#campo` — Field Projects Section
- Background: `--gray`
- Centered layout, max-width 860px (`.campo-wrap`)
- **Video** (`.campo-video`): `video/medicao-espessura-nr13.mp4`, poster `img/medicao-espessura-nr13.jpeg`, `preload="none"`, with legend bar
- **Photo grid** (`.campo-fotos`): 4 columns (2 on mobile), square aspect-ratio, hover zoom
  - Photos: `medicao-espessura-nr13.jpeg`, `end-lp-anel-trinca.jpeg`, `trabalho-altura-nr35.jpeg`, `enfardadeira-nr12.jpeg`

### 6. `#diferencial` — Differentials Section
- Background: `--black`
- 2-column grid (`.dif-grid`), 1 column on mobile
- Left: dark green box (`.dif-box`) with quote + text; "BG" watermark via `::after`
- Right: tag + title + sector tags (`.setor`): Cimenteiras, Têxteis, Geração de Energia, Construção Civil, Movimentação de Cargas

### 7. `#sobre` — About Section
- Background: `--gray`
- 2-column grid (`.sobre-grid`), 1 column on mobile
- Left: tag + title + 5 checkmark items (`.sobre-checks`)
- Right: `img/trabalho-altura-nr35.jpeg` (`.sobre-img`, aspect-ratio 4/3, `object-fit: cover`)

### 8. `#tipos` — Solution Types Section
- Background: `--dark`
- Centered heading, 6-card grid (`repeat(auto-fit, minmax(210px, 1fr))`)
- Cards (`.tipo`): Inspeções, Projetos, Ensaios END, Consultoria, Laudos Técnicos, Treinamentos
- Hover: border green + translateY(-4px)

### 9. `#contato` — Contact Section
- Background: `--black`, centered
- 3 info cards (`.c-card`): WhatsApp, Email, Address
- Large WhatsApp CTA button (`.wa-big`)

### 10. `<footer>`
- Logo + address line + copyright
- Mobile: column layout, centered

### Fixed Elements
- `.float-wa`: WhatsApp floating button, bottom-right, `z-index: 300`

---

## JavaScript

All JS is in a single `<script>` tag at end of `<body>`. Three main blocks:

### 1. Mobile Menu
```
ham click → toggle nav-menu display (flex column, absolute, full-width)
anchor click → smooth scroll + close menu
document click → close menu if open and click is outside menu/ham
```

### 2. Hero Deck (IIFE)
```
SLIDES array (16 objects: {src, alt})
cards = DOM elements created from SLIDES, appended to #heroDeck
getPos(i) → class based on (i - cur) % n: pos-0, pos-1, pos-2, pos-back
update() → apply classes + update counter text
go(dir) → locked guard → cur += dir → update() → reset auto timer → unlock after 350ms
Auto: setInterval(go(1), 3800)
Drag: mousedown/mousemove/mouseup on wrap; touchstart/touchend
  mousemove: clamps dx to ±100, applies inline transform to front card (no transition)
  mouseup/touchend: if |dx| > threshold → go(direction)
```

### 3. Navbar Scroll
```
scroll → navbar background darkens when scrollY > 60px
```

---

## Key CSS Classes Reference

| Class | Element | Purpose |
|---|---|---|
| `.s-tag` | `<span>` | Small uppercase colored label above section titles |
| `.s-title` | `<h2>` | Section main heading (Barlow Condensed, responsive size) |
| `.s-sub` | `<p>` | Section subtitle (muted, max-width 520px) |
| `.s-head` | `<div>` | Wrapper for tag+title+sub, margin-bottom 56px |
| `.section` | `<section>` | Standard section padding (96px 5%) |
| `.srv` | `<div>` | Service card (gray2 bg, left border accent on hover) |
| `.srv-img` | `<img>` | Card photo, 180px, bleeds to edges |
| `.srv-img-blank` | `<div>` | Placeholder for cards without photo, same size as srv-img |
| `.srv-icon` | `<div>` | 46×46px green-tinted icon box |
| `.srv-nr` | `<div>` | NR tag text (green, uppercase, small) |
| `.deck-card` | `<div>` | Individual photo card in hero slideshow |
| `.deck-card.pos-0` | — | Front card: rotate(-1deg), scale(1), z-index 10 |
| `.deck-card.pos-1` | — | Second card: rotate(5deg) translate(22,16) scale(.94) |
| `.deck-card.pos-2` | — | Third card: rotate(10deg) translate(44,32) scale(.88) |
| `.deck-card.pos-back` | — | Hidden cards: opacity 0, pointer-events none |
| `.deck-card.is-dragging` | — | Disables transition during mouse drag |
| `.btn-wa` | `<a>` | Green WhatsApp CTA button |
| `.btn-ghost` | `<a>` | Transparent outlined button |
| `.wa-big` | `<a>` | Large green WhatsApp button in contact section |
| `.float-wa` | `<a>` | Fixed WhatsApp bubble (bottom-right) |
| `.setor` | `<span>` | Industry sector tag pill |
| `.ck` | `<div>` | Circular checkmark in about section |
| `.campo-foto` | `<div>` | Square photo in campo grid, hover zoom |
| `.tipo` | `<div>` | Solution type card, hover lift effect |
| `.c-card` | `<div>` | Contact info card |

---

## Deployment

```yaml
# .cpanel.yml — copies files to Hostgator public_html on deploy
deployment:
  tasks:
    - export DEPLOYPATH=/home1/brunoe85/public_html/
    - /bin/cp -Rf index.html $DEPLOYPATH
    - /bin/cp -Rf img $DEPLOYPATH
    - /bin/cp -Rf video $DEPLOYPATH
```

**Deploy flow:** push to GitHub → cPanel Git Version Control → "Update from Remote" → "Deploy HEAD Commit"

**Git identity configured locally:**
- `user.name`: Bruno Evaristo
- `user.email`: amanda.filipy@gmail.com
