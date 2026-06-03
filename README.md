<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Harmony Tea Collection – Sip the Serenity</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com"/>
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400&family=Jost:wght@300;400;500;600&display=swap" rel="stylesheet"/>

  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            matcha:    { DEFAULT: '#4a7c59', dark: '#2d5a3d', light: '#7aab8a', pale: '#d4e8db' },
            earth:     { DEFAULT: '#7a5c42', dark: '#5c4230', light: '#a8846a' },
            cream:     { DEFAULT: '#f5f0e8', warm: '#ede5d5', deep: '#d9cdb8' },
            gold:      { DEFAULT: '#c9a96e', light: '#e0c898' },
            ink:       { DEFAULT: '#1e1a14', soft: '#3d3628' },
          },
          fontFamily: {
            display: ['"Cormorant Garamond"', 'serif'],
            body:    ['"Jost"', 'sans-serif'],
          },
        }
      }
    }
  </script>

  <style>
    *, *::before, *::after { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body { font-family: 'Jost', sans-serif; background-color: #f5f0e8; color: #1e1a14; overflow-x: hidden; }

    /* ─── Grain overlay ─── */
    body::before {
      content: '';
      position: fixed; inset: 0; z-index: 0; pointer-events: none;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
      opacity: 0.6;
    }

    /* ─── Navbar ─── */
    #navbar { transition: background 0.4s, box-shadow 0.4s; }
    #navbar.scrolled { background: rgba(245,240,232,0.97) !important; box-shadow: 0 2px 20px rgba(0,0,0,0.08); }

    /* ─── Hero ─── */
    #hero {
      position: relative; min-height: 100vh; display: flex; align-items: center;
      background: url('https://images.unsplash.com/photo-1556679343-c7306c1976bc?w=1600&q=80') center center / cover no-repeat;
    }
    #hero::after {
      content: ''; position: absolute; inset: 0;
      background: linear-gradient(135deg, rgba(30,26,20,0.72) 0%, rgba(45,90,61,0.55) 60%, rgba(30,26,20,0.30) 100%);
    }
    #hero > * { position: relative; z-index: 1; }

    /* vertical text decoration */
    .vert-text {
      writing-mode: vertical-rl; text-orientation: mixed; letter-spacing: 0.3em;
      font-family: 'Cormorant Garamond', serif; font-size: 0.7rem; color: rgba(255,255,255,0.5);
      user-select: none;
    }

    /* ─── Section divider ─── */
    .divider {
      width: 60px; height: 2px; background: #c9a96e; margin: 0 auto 2rem;
    }
    .divider-left { margin-left: 0; }

    /* ─── Product card ─── */
    .product-card {
      background: white; border: 1px solid #e8e0d0;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    .product-card:hover { transform: translateY(-6px); box-shadow: 0 20px 50px rgba(0,0,0,0.12); }
    .product-card img { transition: transform 0.5s ease; }
    .product-card:hover img { transform: scale(1.05); }

    /* ─── Flag card ─── */
    .flag-card {
      background: white; border: 1px solid #e8e0d0;
      transition: transform 0.25s, box-shadow 0.25s;
    }
    .flag-card:hover { transform: translateY(-4px); box-shadow: 0 12px 30px rgba(0,0,0,0.10); }

    /* ─── Form input ─── */
    .form-input {
      width: 100%; border: 1px solid #d9cdb8; background: #faf7f2;
      padding: 0.75rem 1rem; font-family: 'Jost', sans-serif; font-size: 0.9rem;
      color: #1e1a14; outline: none; transition: border-color 0.25s;
    }
    .form-input:focus { border-color: #4a7c59; }

    /* ─── Animations ─── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(30px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
    @keyframes scaleIn {
      from { opacity: 0; transform: scale(0.93); }
      to   { opacity: 1; transform: scale(1); }
    }
    .anim-fade-up  { animation: fadeUp  0.8s ease both; }
    .anim-fade-in  { animation: fadeIn  1s  ease both; }
    .anim-scale-in { animation: scaleIn 0.7s ease both; }
    .delay-1 { animation-delay: 0.15s; }
    .delay-2 { animation-delay: 0.30s; }
    .delay-3 { animation-delay: 0.45s; }
    .delay-4 { animation-delay: 0.60s; }
    .delay-5 { animation-delay: 0.80s; }

    /* ─── Scroll reveal (JS-driven) ─── */
    .reveal { opacity: 0; transform: translateY(28px); transition: opacity 0.7s ease, transform 0.7s ease; }
    .reveal.visible { opacity: 1; transform: translateY(0); }

    /* ─── Toast ─── */
    #toast {
      position: fixed; bottom: 2rem; left: 50%; transform: translateX(-50%) translateY(80px);
      background: #2d5a3d; color: #f5f0e8; padding: 0.9rem 2rem; font-family: 'Jost', sans-serif;
      font-size: 0.9rem; letter-spacing: 0.05em; z-index: 9999;
      transition: transform 0.4s ease, opacity 0.4s ease; opacity: 0;
    }
    #toast.show { transform: translateX(-50%) translateY(0); opacity: 1; }

    /* ─── Spec table ─── */
    .spec-row { border-bottom: 1px solid #e8e0d0; }
    .spec-row:last-child { border-bottom: none; }

    /* ─── Mobile nav ─── */
    #mobile-menu { transition: max-height 0.35s ease, opacity 0.35s ease; max-height: 0; opacity: 0; overflow: hidden; }
    #mobile-menu.open { max-height: 400px; opacity: 1; }

    /* Horizontal rule style */
    .ornament { color: #c9a96e; font-size: 1.2rem; letter-spacing: 0.5rem; user-select: none; }

    /* USP badge */
    .usp-badge {
      display: inline-flex; align-items: center; gap: 0.3rem;
      background: #d4e8db; color: #2d5a3d; font-size: 0.68rem;
      font-weight: 600; letter-spacing: 0.07em; padding: 0.25rem 0.6rem;
      text-transform: uppercase;
    }

    /* Category chip */
    .cat-chip {
      display: inline-block; font-size: 0.65rem; font-weight: 600; letter-spacing: 0.12em;
      text-transform: uppercase; padding: 0.2rem 0.7rem;
      background: #f5f0e8; border: 1px solid #c9a96e; color: #7a5c42;
    }

    /* Scrollbar */
    ::-webkit-scrollbar { width: 6px; }
    ::-webkit-scrollbar-track { background: #f5f0e8; }
    ::-webkit-scrollbar-thumb { background: #4a7c59; border-radius: 3px; }
  </style>
</head>
<body class="relative z-0">

<!-- ══════════════════ NAVBAR ══════════════════ -->
<nav id="navbar" class="fixed top-0 left-0 right-0 z-50 transition-all duration-300">
  <div class="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
    <!-- Logo -->
    <a href="#hero" class="flex items-center gap-3">
      <div class="w-8 h-8 flex items-center justify-center border border-gold" style="background:rgba(74,124,89,0.9)">
        <svg viewBox="0 0 24 24" class="w-4 h-4 fill-none stroke-cream" stroke-width="1.5"><path d="M3 12c0-4.97 4.03-9 9-9s9 4.03 9 9M7 15c.5-2 2.5-3.5 5-3.5s4.5 1.5 5 3.5M9 18c.8-1.2 1.8-1.8 3-1.8s2.2.6 3 1.8"/></svg>
      </div>
      <span class="font-display text-lg font-semibold tracking-wide text-cream">Harmony Tea</span>
    </a>

    <!-- Desktop links -->
    <ul class="hidden md:flex items-center gap-8 text-sm font-body font-400 tracking-wider text-cream" style="text-shadow:0 1px 3px rgba(0,0,0,0.5)">
      <li><a href="#markets" class="hover:text-gold-light transition-colors">Markets</a></li>
      <li><a href="#catalog" class="hover:text-gold-light transition-colors">Catalog</a></li>
      <li><a href="#b2b" class="hover:text-gold-light transition-colors">B2B Info</a></li>
      <li><a href="#contact" class="hover:text-gold-light transition-colors">Contact</a></li>
    </ul>

    <!-- CTA -->
    <a href="#contact" class="hidden md:inline-block text-xs font-body font-600 tracking-widest uppercase px-5 py-2.5 bg-matcha text-cream border border-matcha-light hover:bg-matcha-dark transition-colors">
      Send Inquiry
    </a>

    <!-- Hamburger -->
    <button id="hamburger" class="md:hidden flex flex-col gap-1.5 p-1" aria-label="Open menu">
      <span class="block w-6 h-px bg-cream"></span>
      <span class="block w-6 h-px bg-cream"></span>
      <span class="block w-4 h-px bg-cream"></span>
    </button>
  </div>

  <!-- Mobile menu -->
  <div id="mobile-menu" class="md:hidden bg-cream">
    <ul class="flex flex-col font-body text-sm tracking-wider text-ink px-6 py-4 gap-4">
      <li><a href="#markets" class="hover:text-matcha transition-colors">Markets</a></li>
      <li><a href="#catalog" class="hover:text-matcha transition-colors">Catalog</a></li>
      <li><a href="#b2b" class="hover:text-matcha transition-colors">B2B Info</a></li>
      <li><a href="#contact" class="hover:text-matcha transition-colors">Contact</a></li>
      <li>
        <a href="#contact" class="inline-block text-xs font-600 tracking-widest uppercase px-5 py-2.5 bg-matcha text-cream">
          Send Inquiry
        </a>
      </li>
    </ul>
  </div>
</nav>

<!-- ══════════════════ HERO ══════════════════ -->
<section id="hero" class="relative">
  <!-- Vertical text ornaments -->
  <div class="absolute left-6 bottom-20 hidden lg:flex flex-col items-center gap-4 z-10">
    <div class="w-px h-16 bg-gold opacity-50"></div>
    <span class="vert-text">HARMONY TEA · EST. 2025</span>
  </div>
  <div class="absolute right-6 top-1/2 -translate-y-1/2 hidden lg:flex flex-col items-center gap-4 z-10">
    <span class="vert-text">INDONESIA · PURE · HALAL</span>
    <div class="w-px h-16 bg-gold opacity-50"></div>
  </div>

  <div class="max-w-7xl mx-auto px-6 py-32 md:py-40 flex flex-col items-center text-center">
    <!-- Eyebrow -->
    <p class="anim-fade-up text-gold font-body font-300 text-xs tracking-[0.35em] uppercase mb-5">
      ✦ Premium Indonesian Green Tea ✦
    </p>

    <!-- Main headline -->
    <h1 class="anim-fade-up delay-1 font-display font-300 text-cream leading-none mb-4"
        style="font-size: clamp(3rem, 8vw, 6.5rem); text-shadow: 0 4px 30px rgba(0,0,0,0.4);">
      Harmony Tea<br/>
      <span class="italic font-semibold text-gold-light" style="font-size:0.9em;">Collection</span>
    </h1>

    <!-- Tag line -->
    <p class="anim-fade-up delay-2 font-display italic text-cream text-xl md:text-3xl font-light mb-6 opacity-90"
       style="text-shadow:0 2px 12px rgba(0,0,0,0.4);">
      "Sip the Serenity"
    </p>

    <!-- Divider ornament -->
    <div class="anim-fade-up delay-2 ornament mb-6">— ⋅ ◈ ⋅ —</div>

    <!-- Sub-headline -->
    <p class="anim-fade-up delay-3 font-body font-300 text-cream text-base md:text-lg max-w-2xl leading-relaxed opacity-85 mb-10"
       style="text-shadow:0 1px 8px rgba(0,0,0,0.5);">
      The Authentic Indonesian Green Tea.<br/>
      Pure mountain origin &nbsp;·&nbsp; Halal certified &nbsp;·&nbsp; Sustainably farmed.
    </p>

    <!-- CTA buttons -->
    <div class="anim-fade-up delay-4 flex flex-col sm:flex-row gap-4 items-center">
      <a href="#contact"
         class="inline-flex items-center gap-2 px-8 py-4 bg-matcha text-cream font-body text-sm font-600 tracking-widest uppercase hover:bg-matcha-dark transition-colors duration-300 group">
        <span>Kirim Inquiry Sekarang</span>
        <svg class="w-4 h-4 group-hover:translate-x-1 transition-transform" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
      </a>
      <a href="#catalog"
         class="inline-flex items-center gap-2 px-8 py-4 border border-cream text-cream font-body text-sm font-400 tracking-widest uppercase hover:bg-cream hover:text-ink transition-colors duration-300">
        View Catalog
      </a>
    </div>

    <!-- Stats bar -->
    <div class="anim-fade-up delay-5 mt-16 flex flex-wrap justify-center gap-x-10 gap-y-4">
      <div class="text-center">
        <p class="font-display text-2xl font-semibold text-gold">100%</p>
        <p class="font-body text-xs tracking-widest text-cream opacity-70 uppercase">Natural</p>
      </div>
      <div class="w-px h-10 bg-cream opacity-20 self-center hidden sm:block"></div>
      <div class="text-center">
        <p class="font-display text-2xl font-semibold text-gold">120mg</p>
        <p class="font-body text-xs tracking-widest text-cream opacity-70 uppercase">Catechins</p>
      </div>
      <div class="w-px h-10 bg-cream opacity-20 self-center hidden sm:block"></div>
      <div class="text-center">
        <p class="font-display text-2xl font-semibold text-gold">40mg</p>
        <p class="font-body text-xs tracking-widest text-cream opacity-70 uppercase">L-Theanine</p>
      </div>
      <div class="w-px h-10 bg-cream opacity-20 self-center hidden sm:block"></div>
      <div class="text-center">
        <p class="font-display text-2xl font-semibold text-gold">5+</p>
        <p class="font-body text-xs tracking-widest text-cream opacity-70 uppercase">Export Markets</p>
      </div>
    </div>
  </div>

  <!-- Scroll indicator -->
  <div class="absolute bottom-8 left-1/2 -translate-x-1/2 z-10 flex flex-col items-center gap-2 animate-bounce opacity-60">
    <p class="font-body text-xs tracking-widest text-cream uppercase">Scroll</p>
    <svg class="w-4 h-4 text-cream" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M12 5v14M5 12l7 7 7-7"/></svg>
  </div>
</section>


<!-- ══════════════════ ABOUT STRIP ══════════════════ -->
<section class="bg-matcha-dark py-12 relative overflow-hidden">
  <div class="absolute inset-0 opacity-10" style="background:repeating-linear-gradient(45deg,#fff 0px,#fff 1px,transparent 1px,transparent 30px)"></div>
  <div class="max-w-7xl mx-auto px-6 relative">
    <div class="flex flex-wrap justify-center gap-8 md:gap-16 text-center">
      <div class="flex flex-col items-center gap-2">
        <svg class="w-7 h-7 text-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 013.138-3.138z"/></svg>
        <p class="font-body text-xs tracking-widest text-cream uppercase font-600">BPOM RI Certified</p>
      </div>
      <div class="flex flex-col items-center gap-2">
        <svg class="w-7 h-7 text-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M12 3l1.8 5.4H20l-4.9 3.5 1.8 5.4L12 14 7.1 17.3l1.8-5.4L4 8.4h6.2z"/></svg>
        <p class="font-body text-xs tracking-widest text-cream uppercase font-600">Halal Indonesia</p>
      </div>
      <div class="flex flex-col items-center gap-2">
        <svg class="w-7 h-7 text-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M3 7l9-4 9 4M3 7v10l9 4 9-4V7M3 7l9 4m0 0v10m0-10l9-4"/></svg>
        <p class="font-body text-xs tracking-widest text-cream uppercase font-600">Mountain Origin</p>
      </div>
      <div class="flex flex-col items-center gap-2">
        <svg class="w-7 h-7 text-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M4.5 12.75l6 6 9-13.5"/></svg>
        <p class="font-body text-xs tracking-widest text-cream uppercase font-600">No Preservatives</p>
      </div>
      <div class="flex flex-col items-center gap-2">
        <svg class="w-7 h-7 text-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M12 21a9 9 0 100-18 9 9 0 000 18zm0 0V3m0 9h9"/></svg>
        <p class="font-body text-xs tracking-widest text-cream uppercase font-600">Global Export Ready</p>
      </div>
    </div>
  </div>
</section>


<!-- ══════════════════ TARGET MARKETS ══════════════════ -->
<section id="markets" class="py-24 md:py-32 bg-cream-warm">
  <div class="max-w-7xl mx-auto px-6">

    <!-- Section heading -->
    <div class="text-center mb-16 reveal">
      <p class="font-body text-xs tracking-[0.35em] text-matcha uppercase mb-3">B2B Global Reach</p>
      <h2 class="font-display text-4xl md:text-5xl font-light text-ink mb-4">Target Market &amp; <em>Export Destinations</em></h2>
      <div class="divider"></div>
    </div>

    <!-- Consumer Segments -->
    <div class="mb-20">
      <h3 class="font-display text-2xl md:text-3xl font-light text-ink text-center mb-10 reveal">Consumer Segments</h3>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">

        <!-- Segment 1 -->
        <div class="reveal bg-white border border-cream-deep p-8 text-center group hover:border-matcha transition-colors duration-300">
          <div class="w-16 h-16 mx-auto mb-5 flex items-center justify-center bg-matcha-pale group-hover:bg-matcha-light transition-colors rounded-full">
            <svg class="w-7 h-7 text-matcha-dark" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M4.5 12.75l6 6 9-13.5M9 12l2 2 4-4"/></svg>
          </div>
          <h4 class="font-display text-xl font-semibold text-ink mb-3">Health Conscious</h4>
          <p class="font-body text-sm text-earth font-300 leading-relaxed">Urban professionals and wellness-first consumers seeking antioxidant-rich, clean-label beverages with verified nutritional benefits.</p>
        </div>

        <!-- Segment 2 -->
        <div class="reveal delay-1 bg-white border border-cream-deep p-8 text-center group hover:border-matcha transition-colors duration-300">
          <div class="w-16 h-16 mx-auto mb-5 flex items-center justify-center bg-matcha-pale group-hover:bg-matcha-light transition-colors rounded-full">
            <svg class="w-7 h-7 text-matcha-dark" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M3 12c0-4.97 4.03-9 9-9s9 4.03 9 9M7 15c.5-2 2.5-3.5 5-3.5s4.5 1.5 5 3.5M9 18c.8-1.2 1.8-1.8 3-1.8s2.2.6 3 1.8"/></svg>
          </div>
          <h4 class="font-display text-xl font-semibold text-ink mb-3">Tea Enthusiasts</h4>
          <p class="font-body text-sm text-earth font-300 leading-relaxed">Discerning connoisseurs who appreciate single-origin terroir, artisanal craftsmanship, and the rich heritage of Southeast Asian tea culture.</p>
        </div>

        <!-- Segment 3 -->
        <div class="reveal delay-2 bg-white border border-cream-deep p-8 text-center group hover:border-matcha transition-colors duration-300">
          <div class="w-16 h-16 mx-auto mb-5 flex items-center justify-center bg-matcha-pale group-hover:bg-matcha-light transition-colors rounded-full">
            <svg class="w-7 h-7 text-matcha-dark" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M12 6v6l4 2M12 22c5.52 0 10-4.48 10-10S17.52 2 12 2 2 6.48 2 12s4.48 10 10 10z"/></svg>
          </div>
          <h4 class="font-display text-xl font-semibold text-ink mb-3">Busy Professionals</h4>
          <p class="font-body text-sm text-earth font-300 leading-relaxed">High-earning urban middle class seeking premium, convenient, and meaningful beverage rituals that blend performance with mindful living.</p>
        </div>
      </div>
    </div>

    <!-- Export Destinations -->
    <h3 class="font-display text-2xl md:text-3xl font-light text-ink text-center mb-10 reveal">Export Destinations</h3>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-5">

      <!-- China -->
      <div class="flag-card p-6 text-center reveal">
        <div class="text-5xl mb-3">🇨🇳</div>
        <h4 class="font-display text-lg font-semibold text-ink mb-1">China</h4>
        <p class="cat-chip mb-3">Premium Tier</p>
        <p class="font-body text-xs text-earth leading-relaxed">High-demand premium tea segment; rising appetite for Southeast Asian terroir experiences.</p>
      </div>

      <!-- Germany -->
      <div class="flag-card p-6 text-center reveal delay-1">
        <div class="text-5xl mb-3">🇩🇪</div>
        <h4 class="font-display text-lg font-semibold text-ink mb-1">Germany</h4>
        <p class="cat-chip mb-3">Organic Specialist</p>
        <p class="font-body text-xs text-earth leading-relaxed">Europe's top organic tea market; strong demand for sustainable, certified-clean supply chains.</p>
      </div>

      <!-- Poland -->
      <div class="flag-card p-6 text-center reveal delay-2">
        <div class="text-5xl mb-3">🇵🇱</div>
        <h4 class="font-display text-lg font-semibold text-ink mb-1">Poland</h4>
        <p class="cat-chip mb-3">Sustainable Market</p>
        <p class="font-body text-xs text-earth leading-relaxed">Rapidly growing organic tea consumers; eco-label preference driving import demand.</p>
      </div>

      <!-- Malaysia -->
      <div class="flag-card p-6 text-center reveal delay-3">
        <div class="text-5xl mb-3">🇲🇾</div>
        <h4 class="font-display text-lg font-semibold text-ink mb-1">Malaysia</h4>
        <p class="cat-chip mb-3">Halal Hub</p>
        <p class="font-body text-xs text-earth leading-relaxed">ASEAN's leading Halal trade hub; ideal gateway for Muslim-majority market distribution.</p>
      </div>

      <!-- Vietnam -->
      <div class="flag-card p-6 text-center reveal delay-4">
        <div class="text-5xl mb-3">🇻🇳</div>
        <h4 class="font-display text-lg font-semibold text-ink mb-1">Vietnam</h4>
        <p class="cat-chip mb-3">Regional Gateway</p>
        <p class="font-body text-xs text-earth leading-relaxed">Booming specialty tea culture; growing premium segment receptive to Indonesian origin teas.</p>
      </div>
    </div>
  </div>
</section>


<!-- ══════════════════ CATALOG ══════════════════ -->
<section id="catalog" class="py-24 md:py-32" style="background:#f5f0e8;">
  <div class="max-w-7xl mx-auto px-6">

    <div class="text-center mb-4 reveal">
      <p class="font-body text-xs tracking-[0.35em] text-matcha uppercase mb-3">Our Products</p>
      <h2 class="font-display text-4xl md:text-5xl font-light text-ink mb-4">Product <em>Catalog</em></h2>
      <div class="divider"></div>
    </div>

    <!-- USP bar -->
    <div class="reveal flex flex-wrap justify-center gap-3 mb-14">
      <span class="usp-badge">✓ No Preservatives</span>
      <span class="usp-badge">✓ 120mg Catechins</span>
      <span class="usp-badge">✓ 40mg L-Theanine</span>
      <span class="usp-badge">✓ Pure Mountain Origin</span>
      <span class="usp-badge">✓ Halal Certified</span>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-7">

      <!-- Product 1 -->
      <div class="product-card reveal flex flex-col">
        <div class="overflow-hidden relative">
          <img src="https://images.unsplash.com/photo-1536256263959-770b48d82b0a?w=600&q=80"
               alt="Pure Matcha Powder" class="w-full h-52 object-cover"/>
          <span class="absolute top-3 left-3 bg-matcha-dark text-cream text-xs font-body font-600 tracking-widest px-3 py-1 uppercase">Super Premium</span>
        </div>
        <div class="p-6 flex flex-col flex-1">
          <p class="font-body text-xs tracking-widest text-earth uppercase mb-1">100g</p>
          <h3 class="font-display text-xl font-semibold text-ink mb-2">Pure Matcha Powder</h3>
          <p class="font-body text-xs text-earth font-300 leading-relaxed flex-1 mb-4">
            Stone-milled ceremonial-grade matcha sourced from highland tea gardens. Brilliant green, umami-rich, zero additives.
          </p>
          <div class="flex flex-wrap gap-2 mb-4">
            <span class="usp-badge">No Preservatives</span>
            <span class="usp-badge">120mg Catechins</span>
          </div>
          <div class="flex items-end justify-between pt-4 border-t border-cream-deep">
            <div>
              <p class="font-body text-xs text-earth uppercase tracking-wider mb-0.5">FOB Price</p>
              <p class="font-display text-2xl font-semibold text-matcha-dark">$28.50</p>
            </div>
            <a href="#contact" class="text-xs font-body font-600 tracking-widest uppercase px-4 py-2.5 bg-ink text-cream hover:bg-matcha-dark transition-colors">Order</a>
          </div>
        </div>
      </div>

      <!-- Product 2 -->
      <div class="product-card reveal delay-1 flex flex-col">
        <div class="overflow-hidden relative">
          <img src="https://images.unsplash.com/photo-1556679343-c7306c1976bc?w=600&q=80"
               alt="Sencha Green Tea Leaf" class="w-full h-52 object-cover"/>
          <span class="absolute top-3 left-3 bg-matcha text-cream text-xs font-body font-600 tracking-widest px-3 py-1 uppercase">Premium Artisan</span>
        </div>
        <div class="p-6 flex flex-col flex-1">
          <p class="font-body text-xs tracking-widest text-earth uppercase mb-1">250g</p>
          <h3 class="font-display text-xl font-semibold text-ink mb-2">Sencha Green Tea Leaf</h3>
          <p class="font-body text-xs text-earth font-300 leading-relaxed flex-1 mb-4">
            First-flush sencha leaves hand-picked at peak season. Crisp, grassy notes with a clean, refreshing finish.
          </p>
          <div class="flex flex-wrap gap-2 mb-4">
            <span class="usp-badge">No Preservatives</span>
            <span class="usp-badge">40mg L-Theanine</span>
          </div>
          <div class="flex items-end justify-between pt-4 border-t border-cream-deep">
            <div>
              <p class="font-body text-xs text-earth uppercase tracking-wider mb-0.5">FOB Price</p>
              <p class="font-display text-2xl font-semibold text-matcha-dark">$18.25</p>
            </div>
            <a href="#contact" class="text-xs font-body font-600 tracking-widest uppercase px-4 py-2.5 bg-ink text-cream hover:bg-matcha-dark transition-colors">Order</a>
          </div>
        </div>
      </div>

      <!-- Product 3 -->
      <div class="product-card reveal delay-2 flex flex-col">
        <div class="overflow-hidden relative">
          <img src="https://images.unsplash.com/photo-1544787219-7f47ccb76574?w=600&q=80"
               alt="Genmaicha Blend" class="w-full h-52 object-cover"/>
          <span class="absolute top-3 left-3 bg-earth text-cream text-xs font-body font-600 tracking-widest px-3 py-1 uppercase">Signature Blend</span>
        </div>
        <div class="p-6 flex flex-col flex-1">
          <p class="font-body text-xs tracking-widest text-earth uppercase mb-1">200g</p>
          <h3 class="font-display text-xl font-semibold text-ink mb-2">Genmaicha Blend</h3>
          <p class="font-body text-xs text-earth font-300 leading-relaxed flex-1 mb-4">
            Classic sencha blended with toasted brown rice. Warm, nutty aroma with a smooth, comforting finish for everyday sipping.
          </p>
          <div class="flex flex-wrap gap-2 mb-4">
            <span class="usp-badge">No Preservatives</span>
            <span class="usp-badge">120mg Catechins</span>
          </div>
          <div class="flex items-end justify-between pt-4 border-t border-cream-deep">
            <div>
              <p class="font-body text-xs text-earth uppercase tracking-wider mb-0.5">FOB Price</p>
              <p class="font-display text-2xl font-semibold text-matcha-dark">$15.80</p>
            </div>
            <a href="#contact" class="text-xs font-body font-600 tracking-widest uppercase px-4 py-2.5 bg-ink text-cream hover:bg-matcha-dark transition-colors">Order</a>
          </div>
        </div>
      </div>

      <!-- Product 4 -->
      <div class="product-card reveal delay-3 flex flex-col">
        <div class="overflow-hidden relative">
          <img src="https://images.unsplash.com/photo-1571934811356-5cc061b6821f?w=600&q=80"
               alt="Artisanal Tea Gift Set" class="w-full h-52 object-cover"/>
          <span class="absolute top-3 left-3 bg-gold text-ink text-xs font-body font-600 tracking-widest px-3 py-1 uppercase">Special Collection</span>
        </div>
        <div class="p-6 flex flex-col flex-1">
          <p class="font-body text-xs tracking-widest text-earth uppercase mb-1">Gift Set</p>
          <h3 class="font-display text-xl font-semibold text-ink mb-2">Artisanal Tea Gift Set</h3>
          <p class="font-body text-xs text-earth font-300 leading-relaxed flex-1 mb-4">
            Curated collection featuring our three signature teas in premium packaging. Perfect for retail gifting, corporate hampers, and hotel amenities.
          </p>
          <div class="flex flex-wrap gap-2 mb-4">
            <span class="usp-badge">No Preservatives</span>
            <span class="usp-badge">Full Spectrum</span>
          </div>
          <div class="flex items-end justify-between pt-4 border-t border-cream-deep">
            <div>
              <p class="font-body text-xs text-earth uppercase tracking-wider mb-0.5">FOB Price</p>
              <p class="font-display text-2xl font-semibold text-matcha-dark">$55.00</p>
            </div>
            <a href="#contact" class="text-xs font-body font-600 tracking-widest uppercase px-4 py-2.5 bg-ink text-cream hover:bg-matcha-dark transition-colors">Order</a>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>


<!-- ══════════════════ B2B SPECIFICATIONS ══════════════════ -->
<section id="b2b" class="py-24 md:py-32 bg-ink relative overflow-hidden">
  <!-- Background texture -->
  <div class="absolute inset-0 opacity-5"
       style="background: url('https://images.unsplash.com/photo-1556679343-c7306c1976bc?w=800&q=50') center/cover no-repeat;"></div>

  <div class="max-w-7xl mx-auto px-6 relative z-10">
    <div class="text-center mb-14 reveal">
      <p class="font-body text-xs tracking-[0.35em] text-gold uppercase mb-3">For Global Buyers</p>
      <h2 class="font-display text-4xl md:text-5xl font-light text-cream mb-4">Business <em>Specifications</em></h2>
      <div class="divider"></div>
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-2 gap-10 items-start">

      <!-- Spec Table -->
      <div class="reveal">
        <h3 class="font-body text-xs tracking-[0.3em] text-gold uppercase mb-6">Trade &amp; Compliance Details</h3>
        <div class="border border-gray-700">
          <div class="spec-row flex" style="border-color: rgba(255,255,255,0.1);">
            <div class="w-40 flex-shrink-0 px-5 py-4 bg-matcha-dark bg-opacity-30">
              <p class="font-body text-xs tracking-widest text-gold uppercase">HS Code</p>
            </div>
            <div class="px-5 py-4">
              <p class="font-display text-lg text-cream font-light">0902.20</p>
              <p class="font-body text-xs text-gray-400 mt-0.5">Green Tea — not fermented / flavoured</p>
            </div>
          </div>
          <div class="spec-row flex" style="border-color: rgba(255,255,255,0.1);">
            <div class="w-40 flex-shrink-0 px-5 py-4 bg-matcha-dark bg-opacity-30">
              <p class="font-body text-xs tracking-widest text-gold uppercase">Certifications</p>
            </div>
            <div class="px-5 py-4">
              <p class="font-display text-lg text-cream font-light">BPOM RI &amp; Halal Indonesia</p>
              <p class="font-body text-xs text-gray-400 mt-0.5">Full regulatory compliance for Muslim-majority &amp; global markets</p>
            </div>
          </div>
          <div class="spec-row flex" style="border-color: rgba(255,255,255,0.1);">
            <div class="w-40 flex-shrink-0 px-5 py-4 bg-matcha-dark bg-opacity-30">
              <p class="font-body text-xs tracking-widest text-gold uppercase">MOQ</p>
            </div>
            <div class="px-5 py-4">
              <p class="font-display text-lg text-cream font-light">50 kg / 200 Units per SKU</p>
              <p class="font-body text-xs text-gray-400 mt-0.5">Flexible trial orders available — contact us for custom MOQ discussions</p>
            </div>
          </div>
          <div class="spec-row flex" style="border-color: rgba(255,255,255,0.1);">
            <div class="w-40 flex-shrink-0 px-5 py-4 bg-matcha-dark bg-opacity-30">
              <p class="font-body text-xs tracking-widest text-gold uppercase">Lead Time</p>
            </div>
            <div class="px-5 py-4">
              <p class="font-display text-lg text-cream font-light">14–21 Business Days</p>
              <p class="font-body text-xs text-gray-400 mt-0.5">Est. 7–14 days production + 7–10 days international freight (varies by destination)</p>
            </div>
          </div>
          <div class="spec-row flex" style="border-color: rgba(255,255,255,0.1);">
            <div class="w-40 flex-shrink-0 px-5 py-4 bg-matcha-dark bg-opacity-30">
              <p class="font-body text-xs tracking-widest text-gold uppercase">Incoterms</p>
            </div>
            <div class="px-5 py-4">
              <p class="font-display text-lg text-cream font-light">FOB Tanjung Priok, Indonesia</p>
              <p class="font-body text-xs text-gray-400 mt-0.5">CIF &amp; other terms available on request</p>
            </div>
          </div>
          <div class="flex" style="border-color: rgba(255,255,255,0.1);">
            <div class="w-40 flex-shrink-0 px-5 py-4 bg-matcha-dark bg-opacity-30">
              <p class="font-body text-xs tracking-widest text-gold uppercase">Packaging</p>
            </div>
            <div class="px-5 py-4">
              <p class="font-display text-lg text-cream font-light">Private Label Available</p>
              <p class="font-body text-xs text-gray-400 mt-0.5">Custom branding &amp; OEM packaging supported for qualified buyers</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Why Choose Us -->
      <div class="reveal delay-2">
        <h3 class="font-body text-xs tracking-[0.3em] text-gold uppercase mb-6">Why Partner With Us</h3>
        <div class="space-y-5">
          <div class="flex gap-4 items-start p-5 border border-gray-700 hover:border-matcha-light transition-colors">
            <div class="w-10 h-10 flex-shrink-0 flex items-center justify-center bg-matcha-dark rounded-full mt-0.5">
              <svg class="w-5 h-5 text-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M12 3c-4.97 0-9 4.03-9 9s4.03 9 9 9 9-4.03 9-9M15 12a3 3 0 11-6 0 3 3 0 016 0z"/></svg>
            </div>
            <div>
              <h4 class="font-body text-sm font-600 text-cream tracking-wide mb-1">Traceable Single-Origin Supply</h4>
              <p class="font-body text-xs text-gray-400 leading-relaxed">Every batch traceable from mountain garden to your warehouse. Full transparency documentation provided.</p>
            </div>
          </div>
          <div class="flex gap-4 items-start p-5 border border-gray-700 hover:border-matcha-light transition-colors">
            <div class="w-10 h-10 flex-shrink-0 flex items-center justify-center bg-matcha-dark rounded-full mt-0.5">
              <svg class="w-5 h-5 text-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"/></svg>
            </div>
            <div>
              <h4 class="font-body text-sm font-600 text-cream tracking-wide mb-1">Dual Certification Assurance</h4>
              <p class="font-body text-xs text-gray-400 leading-relaxed">BPOM RI food safety and Halal Indonesia certification — two of the most recognized credentials in global tea trade.</p>
            </div>
          </div>
          <div class="flex gap-4 items-start p-5 border border-gray-700 hover:border-matcha-light transition-colors">
            <div class="w-10 h-10 flex-shrink-0 flex items-center justify-center bg-matcha-dark rounded-full mt-0.5">
              <svg class="w-5 h-5 text-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"/></svg>
            </div>
            <div>
              <h4 class="font-body text-sm font-600 text-cream tracking-wide mb-1">Flexible OEM &amp; Private Label</h4>
              <p class="font-body text-xs text-gray-400 leading-relaxed">Custom packaging, brand integration, and reformulation services available for established distributors.</p>
            </div>
          </div>
          <div class="flex gap-4 items-start p-5 border border-gray-700 hover:border-matcha-light transition-colors">
            <div class="w-10 h-10 flex-shrink-0 flex items-center justify-center bg-matcha-dark rounded-full mt-0.5">
              <svg class="w-5 h-5 text-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
            </div>
            <div>
              <h4 class="font-body text-sm font-600 text-cream tracking-wide mb-1">Dedicated Export Support</h4>
              <p class="font-body text-xs text-gray-400 leading-relaxed">Experienced export team handles documentation, logistics coordination, and regulatory compliance for your country.</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>


<!-- ══════════════════ QUOTE BANNER ══════════════════ -->
<section class="py-16 bg-matcha relative overflow-hidden">
  <div class="absolute inset-0 opacity-10" style="background: repeating-linear-gradient(-45deg, #fff 0px, #fff 1px, transparent 1px, transparent 40px);"></div>
  <div class="max-w-3xl mx-auto px-6 text-center relative z-10 reveal">
    <p class="ornament text-gold mb-6">— ◈ —</p>
    <blockquote class="font-display text-2xl md:text-4xl font-light italic text-cream leading-snug mb-6">
      "From Indonesia's highlands to the world's finest tables — <em>every leaf tells a story of care.</em>"
    </blockquote>
    <p class="font-body text-xs tracking-widest text-cream opacity-70 uppercase">Harmony Tea Collection · Indonesia</p>
  </div>
</section>


<!-- ══════════════════ CONTACT ══════════════════ -->
<section id="contact" class="py-24 md:py-32 bg-cream-warm">
  <div class="max-w-7xl mx-auto px-6">
    <div class="text-center mb-14 reveal">
      <p class="font-body text-xs tracking-[0.35em] text-matcha uppercase mb-3">Get In Touch</p>
      <h2 class="font-display text-4xl md:text-5xl font-light text-ink mb-4">Send Us an <em>Inquiry</em></h2>
      <div class="divider"></div>
      <p class="font-body text-sm text-earth font-300 max-w-lg mx-auto mt-4">
        Ready to source premium Indonesian green tea? Fill in the form below and our export team will respond within 24 hours.
      </p>
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-5 gap-10 items-start">

      <!-- ── Inquiry Form ── -->
      <div class="lg:col-span-3 reveal">
        <form id="inquiry-form" class="space-y-0" novalidate>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-0">
            <div class="relative">
              <label class="block font-body text-xs tracking-widest text-earth uppercase mb-1.5 mt-5">Full Name *</label>
              <input id="f-name" type="text" placeholder="John Smith" required
                     class="form-input"/>
            </div>
            <div class="relative sm:ml-0.5">
              <label class="block font-body text-xs tracking-widest text-earth uppercase mb-1.5 mt-5">Company Name *</label>
              <input id="f-company" type="text" placeholder="Acme Distributors Ltd." required
                     class="form-input"/>
            </div>
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-0">
            <div class="relative">
              <label class="block font-body text-xs tracking-widest text-earth uppercase mb-1.5 mt-5">Country of Origin *</label>
              <input id="f-country" type="text" placeholder="Germany" required
                     class="form-input"/>
            </div>
            <div class="relative sm:ml-0.5">
              <label class="block font-body text-xs tracking-widest text-earth uppercase mb-1.5 mt-5">Email Address *</label>
              <input id="f-email" type="email" placeholder="john@company.com" required
                     class="form-input"/>
            </div>
          </div>
          <div class="relative">
            <label class="block font-body text-xs tracking-widest text-earth uppercase mb-1.5 mt-5">Products of Interest</label>
            <select id="f-product" class="form-input appearance-none" style="background-image:url('data:image/svg+xml,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 width=%2212%22 height=%228%22 viewBox=%220 0 12 8%22%3E%3Cpath d=%22M1 1l5 5 5-5%22 stroke=%22%237a5c42%22 stroke-width=%221.5%22 fill=%22none%22/%3E%3C/svg%3E'); background-repeat:no-repeat; background-position: right 1rem center; padding-right:2.5rem;">
              <option value="">— Select a product —</option>
              <option>Pure Matcha Powder (100g) — Super Premium</option>
              <option>Sencha Green Tea Leaf (250g) — Premium Artisan</option>
              <option>Genmaicha Blend (200g) — Signature Blend</option>
              <option>Artisanal Tea Gift Set — Special Collection</option>
              <option>Multiple Products / Custom Order</option>
            </select>
          </div>
          <div class="relative">
            <label class="block font-body text-xs tracking-widest text-earth uppercase mb-1.5 mt-5">Message / Inquiry *</label>
            <textarea id="f-message" rows="5" required placeholder="Please describe your requirements — estimated quantities, destination port, any special certifications needed, etc."
                      class="form-input resize-none"></textarea>
          </div>

          <!-- Privacy note -->
          <p class="font-body text-xs text-gray-400 mt-3">
            Your information will only be used to respond to your inquiry. We do not share or sell your data.
          </p>

          <button type="submit"
                  class="mt-6 w-full flex items-center justify-center gap-2 px-8 py-4 bg-matcha text-cream font-body text-sm font-600 tracking-widest uppercase hover:bg-matcha-dark transition-colors duration-300 group">
            <span id="btn-text">Submit Inquiry</span>
            <svg id="btn-arrow" class="w-4 h-4 group-hover:translate-x-1 transition-transform" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M22 2L11 13M22 2l-7 20-4-9-9-4 20-7z"/></svg>
            <svg id="btn-spin" class="w-5 h-5 animate-spin hidden" fill="none" viewBox="0 0 24 24"><circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"/><path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4z"/></svg>
          </button>
        </form>
      </div>

      <!-- ── Contact Info ── -->
      <div class="lg:col-span-2 space-y-6 reveal delay-2">

        <!-- Primary contact -->
        <div class="bg-white border border-cream-deep p-7">
          <p class="font-body text-xs tracking-[0.3em] text-matcha uppercase mb-4">Primary Contact</p>
          <div class="flex items-center gap-4 mb-4">
            <div class="w-12 h-12 flex-shrink-0 flex items-center justify-center bg-matcha-pale rounded-full">
              <svg class="w-5 h-5 text-matcha-dark" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24"><path d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"/></svg>
            </div>
            <div>
              <p class="font-body font-600 text-ink text-sm">Akbar</p>
              <p class="font-body text-xs text-earth">Export Manager</p>
            </div>
          </div>
          <a href="tel:+6281282064814"
             class="flex items-center gap-3 font-body text-sm text-matcha hover:text-matcha-dark transition-colors mb-3">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/></svg>
            +62 812 8206 4814
          </a>
          <a href="https://wa.me/6281282064814" target="_blank"
             class="inline-flex items-center gap-2 text-xs font-body font-600 tracking-widest uppercase px-4 py-2.5 bg-[#25D366] text-white hover:bg-green-700 transition-colors w-full justify-center">
            <svg class="w-4 h-4" viewBox="0 0 24 24" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/><path d="M12 0C5.373 0 0 5.373 0 12c0 2.115.548 4.1 1.508 5.831L0 24l6.335-1.662A11.945 11.945 0 0012 24c6.627 0 12-5.373 12-12S18.627 0 12 0zm0 21.882c-1.848 0-3.58-.498-5.073-1.368l-.362-.215-3.762.987.997-3.655-.237-.376C2.597 15.488 2.118 13.789 2.118 12 2.118 6.539 6.539 2.118 12 2.118 17.461 2.118 21.882 6.539 21.882 12S17.461 21.882 12 21.882z"/></svg>
            Chat on WhatsApp
          </a>
        </div>

        <!-- Founders -->
        <div class="bg-white border border-cream-deep p-7">
          <p class="font-body text-xs tracking-[0.3em] text-matcha uppercase mb-4">Founding Team</p>
          <ul class="space-y-3">
            <li class="flex items-center gap-3">
              <div class="w-8 h-8 flex-shrink-0 flex items-center justify-center bg-matcha-pale rounded-full text-matcha-dark font-display font-semibold text-sm">A</div>
              <div>
                <p class="font-body text-sm font-500 text-ink">Akbar Maulana Ginting</p>
                <p class="font-body text-xs text-earth">Co-Founder</p>
              </div>
            </li>
            <li class="flex items-center gap-3">
              <div class="w-8 h-8 flex-shrink-0 flex items-center justify-center bg-matcha-pale rounded-full text-matcha-dark font-display font-semibold text-sm">B</div>
              <div>
                <p class="font-body text-sm font-500 text-ink">Bayu Rahma Dani</p>
                <p class="font-body text-xs text-earth">Co-Founder</p>
              </div>
            </li>
            <li class="flex items-center gap-3">
              <div class="w-8 h-8 flex-shrink-0 flex items-center justify-center bg-matcha-pale rounded-full text-matcha-dark font-display font-semibold text-sm">R</div>
              <div>
                <p class="font-body text-sm font-500 text-ink">Reyner Sava Tristan</p>
                <p class="font-body text-xs text-earth">Co-Founder</p>
              </div>
            </li>
          </ul>
        </div>

        <!-- Address -->
        <div class="bg-white border border-cream-deep p-7">
          <p class="font-body text-xs tracking-[0.3em] text-matcha uppercase mb-3">Address</p>
          <div class="flex gap-3">
            <svg class="w-4 h-4 text-matcha mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/><path d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/></svg>
            <div>
              <p class="font-body text-sm text-ink font-500">Politeknik APP Jakarta</p>
              <p class="font-body text-xs text-earth leading-relaxed mt-1">Kementerian Perindustrian<br/>Jakarta, Indonesia</p>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</section>


<!-- ══════════════════ FOOTER ══════════════════ -->
<footer class="bg-ink-soft py-12 border-t border-gray-800">
  <div class="max-w-7xl mx-auto px-6">
    <div class="flex flex-col md:flex-row items-center justify-between gap-6">
      <div class="flex items-center gap-3">
        <div class="w-8 h-8 flex items-center justify-center bg-matcha">
          <svg viewBox="0 0 24 24" class="w-4 h-4 fill-none stroke-cream" stroke-width="1.5"><path d="M3 12c0-4.97 4.03-9 9-9s9 4.03 9 9M7 15c.5-2 2.5-3.5 5-3.5s4.5 1.5 5 3.5M9 18c.8-1.2 1.8-1.8 3-1.8s2.2.6 3 1.8"/></svg>
        </div>
        <div>
          <p class="font-display text-cream font-semibold text-sm tracking-wide">Harmony Tea Collection</p>
          <p class="font-body text-xs text-gray-500">Indonesia · Pure · Halal</p>
        </div>
      </div>
      <nav class="flex flex-wrap justify-center gap-6 text-xs font-body tracking-widest text-gray-400 uppercase">
        <a href="#markets" class="hover:text-gold transition-colors">Markets</a>
        <a href="#catalog" class="hover:text-gold transition-colors">Catalog</a>
        <a href="#b2b" class="hover:text-gold transition-colors">B2B Info</a>
        <a href="#contact" class="hover:text-gold transition-colors">Contact</a>
      </nav>
      <p class="font-body text-xs text-gray-600 text-center">
        HS Code 0902.20 · BPOM RI · Halal Indonesia<br/>
        © 2025 Harmony Tea Collection. All rights reserved.
      </p>
    </div>
    <div class="mt-8 pt-8 border-t border-gray-800 text-center">
      <p class="font-display italic text-gray-600 text-sm">
        "Pure mountain origin · Sustainably farmed · Globally certified"
      </p>
    </div>
  </div>
</footer>

<!-- ══════════════════ TOAST ══════════════════ -->
<div id="toast">
  ✓ Inquiry submitted! We'll be in touch within 24 hours.
</div>


<!-- ══════════════════ JAVASCRIPT ══════════════════ -->
<script>
  // ── Navbar scroll effect ──
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    if (window.scrollY > 60) {
      navbar.classList.add('scrolled');
    } else {
      navbar.classList.remove('scrolled');
    }
  });

  // ── Mobile hamburger ──
  const hamburger = document.getElementById('hamburger');
  const mobileMenu = document.getElementById('mobile-menu');
  hamburger.addEventListener('click', () => {
    mobileMenu.classList.toggle('open');
  });
  // Close menu when a link is clicked
  mobileMenu.querySelectorAll('a').forEach(a => {
    a.addEventListener('click', () => mobileMenu.classList.remove('open'));
  });

  // ── Scroll reveal ──
  const revealEls = document.querySelectorAll('.reveal');
  const revealObserver = new IntersectionObserver((entries) => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        // stagger within parent
        const siblings = Array.from(entry.target.parentElement.querySelectorAll('.reveal'));
        const idx = siblings.indexOf(entry.target);
        entry.target.style.transitionDelay = `${idx * 0.07}s`;
        entry.target.classList.add('visible');
        revealObserver.unobserve(entry.target);
      }
    });
  }, { threshold: 0.12, rootMargin: '0px 0px -40px 0px' });

  revealEls.forEach(el => revealObserver.observe(el));

  // ── Toast helper ──
  function showToast(msg, type = 'success') {
    const toast = document.getElementById('toast');
    toast.textContent = msg;
    toast.style.background = type === 'error' ? '#7a2020' : '#2d5a3d';
    toast.classList.add('show');
    setTimeout(() => toast.classList.remove('show'), 4000);
  }

  // ── Form submission ──
  const form = document.getElementById('inquiry-form');
  const btnText = document.getElementById('btn-text');
  const btnArrow = document.getElementById('btn-arrow');
  const btnSpin = document.getElementById('btn-spin');

  form.addEventListener('submit', async (e) => {
    e.preventDefault();

    const name    = document.getElementById('f-name').value.trim();
    const company = document.getElementById('f-company').value.trim();
    const country = document.getElementById('f-country').value.trim();
    const email   = document.getElementById('f-email').value.trim();
    const message = document.getElementById('f-message').value.trim();

    // Basic validation
    if (!name || !company || !country || !email || !message) {
      showToast('⚠ Please fill in all required fields.', 'error');
      return;
    }
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(email)) {
      showToast('⚠ Please enter a valid email address.', 'error');
      return;
    }

    // Loading state
    btnText.textContent = 'Sending…';
    btnArrow.classList.add('hidden');
    btnSpin.classList.remove('hidden');

    // Simulate async send (replace with real endpoint as needed)
    await new Promise(resolve => setTimeout(resolve, 1800));

    // Reset
    btnText.textContent = 'Submit Inquiry';
    btnArrow.classList.remove('hidden');
    btnSpin.classList.add('hidden');
    form.reset();

    showToast('✓ Inquiry submitted! We\'ll be in touch within 24 hours.');
  });

  // ── Smooth active nav highlight ──
  const sections = document.querySelectorAll('section[id]');
  const navLinks = document.querySelectorAll('nav a[href^="#"]');

  const sectionObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const id = entry.target.id;
        navLinks.forEach(link => {
          if (link.getAttribute('href') === `#${id}`) {
            link.style.color = '#c9a96e';
          } else {
            link.style.color = '';
          }
        });
      }
    });
  }, { threshold: 0.4 });

  sections.forEach(s => sectionObserver.observe(s));
</script>

</body>
</html>
