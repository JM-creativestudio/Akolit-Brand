<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VØID — Outerwear Collection</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Archivo:wght@300;400;500;600&family=Playfair+Display:ital,wght@1,300&display=swap" rel="stylesheet"/>
<style>
  :root {
    --black: #0a0a0a;
    --white: #f8f6f2;
    --beige: #e8e0d4;
    --grey: #9a9590;
    --gold: #c9a96e;
    --mid: #3a3530;
    --transition: cubic-bezier(0.76, 0, 0.24, 1);
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; font-size: 16px; }

  body {
    font-family: 'Archivo', sans-serif;
    background: var(--black);
    color: var(--white);
    overflow-x: hidden;
    cursor: none;
  }

  /* ── CUSTOM CURSOR ── */
  #cursor {
    position: fixed; z-index: 9999;
    width: 10px; height: 10px;
    background: var(--white);
    border-radius: 50%;
    pointer-events: none;
    transform: translate(-50%, -50%);
    transition: width 0.3s var(--transition), height 0.3s var(--transition), background 0.3s;
    mix-blend-mode: difference;
  }
  #cursor-ring {
    position: fixed; z-index: 9998;
    width: 36px; height: 36px;
    border: 1px solid rgba(248,246,242,0.5);
    border-radius: 50%;
    pointer-events: none;
    transform: translate(-50%, -50%);
    transition: all 0.15s var(--transition);
    mix-blend-mode: difference;
  }
  body:has(a:hover) #cursor,
  body:has(button:hover) #cursor { width: 20px; height: 20px; }

  /* ── LANDING / HERO ── */
  #landing {
    position: fixed; inset: 0; z-index: 100;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    overflow: hidden;
    cursor: none;
    transition: opacity 1.2s var(--transition), transform 1.4s var(--transition);
  }
  #landing.exit {
    opacity: 0;
    transform: scale(1.06);
    pointer-events: none;
  }

  #hero-video {
    position: absolute; inset: 0;
    width: 100%; height: 100%;
    object-fit: cover;
    filter: saturate(0.7) brightness(0.55);
  }

  .hero-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(
      to bottom,
      rgba(10,10,10,0.2) 0%,
      rgba(10,10,10,0.45) 50%,
      rgba(10,10,10,0.72) 100%
    );
  }

  /* Cinematic grain */
  .hero-grain {
    position: absolute; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    opacity: 0.35;
    pointer-events: none;
  }

  .hero-content {
    position: relative; z-index: 2;
    text-align: center;
    animation: heroReveal 1.8s var(--transition) both;
  }
  @keyframes heroReveal {
    from { opacity: 0; transform: translateY(28px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .hero-eyebrow {
    font-family: 'Archivo', sans-serif;
    font-size: 0.68rem;
    font-weight: 500;
    letter-spacing: 0.32em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 1.4rem;
    animation: heroReveal 1.8s 0.2s var(--transition) both;
  }

  .hero-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(5rem, 14vw, 13rem);
    font-weight: 300;
    letter-spacing: -0.02em;
    line-height: 0.88;
    color: var(--white);
    animation: heroReveal 1.8s 0.35s var(--transition) both;
  }
  .hero-title span { font-style: italic; color: var(--beige); }

  .hero-subtitle {
    font-family: 'Archivo', sans-serif;
    font-size: 0.72rem;
    font-weight: 300;
    letter-spacing: 0.28em;
    text-transform: uppercase;
    color: rgba(248,246,242,0.6);
    margin-top: 1.6rem;
    animation: heroReveal 1.8s 0.55s var(--transition) both;
  }

  .hero-cta {
    display: inline-flex; align-items: center; gap: 1.1rem;
    margin-top: 3.5rem;
    padding: 1.1rem 2.8rem;
    border: 1px solid rgba(201,169,110,0.6);
    background: transparent;
    color: var(--white);
    font-family: 'Archivo', sans-serif;
    font-size: 0.68rem;
    font-weight: 500;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    cursor: none;
    position: relative;
    overflow: hidden;
    transition: color 0.5s var(--transition), border-color 0.5s var(--transition);
    animation: heroReveal 1.8s 0.75s var(--transition) both;
  }
  .hero-cta::before {
    content: '';
    position: absolute; inset: 0;
    background: var(--gold);
    transform: translateX(-101%);
    transition: transform 0.55s var(--transition);
  }
  .hero-cta:hover::before { transform: translateX(0); }
  .hero-cta:hover { color: var(--black); border-color: var(--gold); }
  .hero-cta span { position: relative; z-index: 1; }
  .hero-cta .cta-arrow {
    position: relative; z-index: 1;
    width: 18px; height: 1px;
    background: currentColor;
    transition: width 0.3s var(--transition);
  }
  .hero-cta .cta-arrow::after {
    content: '';
    position: absolute; right: 0; top: -3px;
    border: 3px solid transparent;
    border-left-color: currentColor;
  }
  .hero-cta:hover .cta-arrow { width: 28px; }

  .hero-scroll-hint {
    position: absolute; bottom: 2.5rem; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 0.6rem;
    animation: heroReveal 1.8s 1.1s var(--transition) both;
  }
  .hero-scroll-hint span {
    font-size: 0.6rem; letter-spacing: 0.3em;
    text-transform: uppercase; color: rgba(248,246,242,0.4);
  }
  .scroll-line {
    width: 1px; height: 40px;
    background: linear-gradient(to bottom, rgba(201,169,110,0.8), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }
  @keyframes scrollPulse {
    0%, 100% { opacity: 0.4; transform: scaleY(1); }
    50% { opacity: 1; transform: scaleY(1.2); }
  }

  /* ── MAIN STORE (hidden until landing exits) ── */
  #store {
    opacity: 0;
    transition: opacity 0.8s var(--transition) 0.6s;
    min-height: 100dvh;
    background: var(--white);
    color: var(--black);
  }
  #store.visible { opacity: 1; }

  /* ── HEADER ── */
  header {
    position: fixed; top: 0; left: 0; right: 0; z-index: 200;
    padding: 1.4rem 2.4rem;
    display: flex; align-items: center; justify-content: space-between;
    transition: background 0.5s var(--transition), padding 0.5s var(--transition), backdrop-filter 0.5s;
  }
  header.scrolled {
    background: rgba(248,246,242,0.96);
    backdrop-filter: blur(20px);
    padding: 0.9rem 2.4rem;
    border-bottom: 1px solid rgba(10,10,10,0.08);
  }
  header.scrolled .logo { font-size: 1.3rem; }
  header.scrolled .nav-link { color: var(--black); }
  header.scrolled .header-icons svg { stroke: var(--black); }

  .logo {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.7rem;
    font-weight: 300;
    letter-spacing: 0.15em;
    color: var(--white);
    text-decoration: none;
    transition: font-size 0.5s var(--transition), color 0.5s;
    animation: fadeDown 0.8s 0.1s var(--transition) both;
  }
  #store .logo,
  header.scrolled .logo { color: var(--black); }

  nav {
    display: flex; gap: 2.4rem;
    animation: fadeDown 0.8s 0.2s var(--transition) both;
  }
  .nav-link {
    font-size: 0.7rem; font-weight: 500;
    letter-spacing: 0.22em; text-transform: uppercase;
    color: rgba(248,246,242,0.85);
    text-decoration: none;
    position: relative;
    transition: color 0.3s;
  }
  .nav-link::after {
    content: '';
    position: absolute; bottom: -3px; left: 0; right: 100%;
    height: 1px; background: var(--gold);
    transition: right 0.4s var(--transition);
  }
  .nav-link:hover::after { right: 0; }
  .nav-link:hover { color: var(--gold); }

  .header-icons {
    display: flex; gap: 1.4rem; align-items: center;
    animation: fadeDown 0.8s 0.3s var(--transition) both;
  }
  .header-icons svg {
    width: 18px; height: 18px; stroke: rgba(248,246,242,0.85);
    cursor: none; transition: stroke 0.3s, transform 0.3s var(--transition);
    fill: none; stroke-width: 1.4;
  }
  .header-icons svg:hover { stroke: var(--gold); transform: scale(1.15); }

  .cart-badge {
    position: relative; cursor: none;
  }
  .cart-badge::after {
    content: '2';
    position: absolute; top: -5px; right: -7px;
    width: 14px; height: 14px;
    background: var(--gold);
    color: var(--black);
    border-radius: 50%;
    font-size: 0.52rem; font-weight: 600;
    display: flex; align-items: center; justify-content: center;
    line-height: 1;
  }

  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-12px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* Hamburger */
  .hamburger {
    display: none; flex-direction: column; gap: 5px;
    cursor: none; padding: 4px;
  }
  .hamburger span {
    display: block; width: 22px; height: 1px;
    background: var(--white);
    transition: background 0.3s, transform 0.3s;
  }
  header.scrolled .hamburger span { background: var(--black); }

  /* ── STORE CONTENT ── */
  .store-wrapper {
    padding-top: 80px;
  }

  /* ── COLLECTION HERO ── */
  .collection-hero {
    height: 55vh; min-height: 380px;
    display: flex; align-items: flex-end;
    padding: 4rem 3rem;
    position: relative;
    overflow: hidden;
    background: var(--black);
  }
  .collection-hero-bg {
    position: absolute; inset: 0;
    background: linear-gradient(135deg, #1a1510 0%, #0a0a0a 60%, #1c1814 100%);
  }
  .collection-hero-content { position: relative; z-index: 1; }
  .collection-hero-tag {
    font-size: 0.62rem; letter-spacing: 0.35em;
    text-transform: uppercase; color: var(--gold);
    margin-bottom: 0.8rem;
  }
  .collection-hero-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(3rem, 7vw, 6rem);
    font-weight: 300;
    line-height: 0.9;
    color: var(--white);
  }
  .collection-hero-title em {
    font-style: italic; color: var(--beige);
  }
  .collection-hero-count {
    margin-top: 1rem;
    font-size: 0.68rem; letter-spacing: 0.2em;
    color: var(--grey); text-transform: uppercase;
  }

  /* ── FILTER BAR ── */
  .filter-bar {
    background: var(--white);
    border-bottom: 1px solid rgba(10,10,10,0.08);
    padding: 0 2.4rem;
    display: flex; align-items: center; justify-content: space-between;
    gap: 1rem;
    position: sticky; top: 58px; z-index: 190;
  }
  .filter-groups {
    display: flex; align-items: center; gap: 0;
    overflow-x: auto;
  }
  .filter-groups::-webkit-scrollbar { display: none; }

  .filter-btn {
    display: flex; align-items: center; gap: 0.5rem;
    padding: 1rem 1.4rem;
    font-size: 0.68rem; font-weight: 500;
    letter-spacing: 0.18em; text-transform: uppercase;
    color: var(--mid); background: transparent; border: none;
    cursor: none; white-space: nowrap;
    border-bottom: 2px solid transparent;
    transition: color 0.3s, border-color 0.3s;
  }
  .filter-btn:hover, .filter-btn.active {
    color: var(--black);
    border-bottom-color: var(--gold);
  }
  .filter-btn svg { width: 10px; height: 10px; fill: currentColor; }

  .sort-select {
    appearance: none;
    font-family: 'Archivo', sans-serif;
    font-size: 0.68rem; font-weight: 500;
    letter-spacing: 0.18em; text-transform: uppercase;
    color: var(--mid); background: transparent;
    border: none; cursor: none;
    padding: 0.5rem;
    outline: none;
  }
  .sort-select:focus { color: var(--black); }

  /* ── PRODUCT GRID ── */
  .product-grid {
    padding: 3rem 2.4rem 5rem;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1.6rem 1.2rem;
  }

  .product-card {
    position: relative;
    animation: cardReveal 0.7s var(--transition) both;
  }
  @keyframes cardReveal {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  .product-card:nth-child(1) { animation-delay: 0.05s; }
  .product-card:nth-child(2) { animation-delay: 0.12s; }
  .product-card:nth-child(3) { animation-delay: 0.19s; }
  .product-card:nth-child(4) { animation-delay: 0.26s; }
  .product-card:nth-child(5) { animation-delay: 0.1s; }
  .product-card:nth-child(6) { animation-delay: 0.17s; }
  .product-card:nth-child(7) { animation-delay: 0.24s; }
  .product-card:nth-child(8) { animation-delay: 0.31s; }

  .product-image-wrap {
    position: relative;
    overflow: hidden;
    aspect-ratio: 3/4;
    background: var(--beige);
  }
  .product-image-wrap img {
    width: 100%; height: 100%;
    object-fit: cover;
    transition: transform 0.9s var(--transition), opacity 0.5s;
  }
  .product-image-wrap .img-hover {
    position: absolute; inset: 0;
    object-fit: cover;
    opacity: 0;
    transition: opacity 0.6s var(--transition), transform 0.9s var(--transition);
    transform: scale(1.04);
  }
  .product-card:hover .product-image-wrap img { transform: scale(1.06); }
  .product-card:hover .img-hover { opacity: 1; transform: scale(1); }

  .quick-view {
    position: absolute; bottom: 0; left: 0; right: 0;
    padding: 1rem;
    background: rgba(10,10,10,0.92);
    backdrop-filter: blur(10px);
    transform: translateY(100%);
    transition: transform 0.45s var(--transition);
    display: flex; align-items: center; justify-content: center;
  }
  .product-card:hover .quick-view { transform: translateY(0); }
  .quick-view button {
    font-family: 'Archivo', sans-serif;
    font-size: 0.6rem; font-weight: 600;
    letter-spacing: 0.28em; text-transform: uppercase;
    color: var(--white); background: transparent; border: none;
    cursor: none;
    transition: color 0.3s;
  }
  .quick-view button:hover { color: var(--gold); }

  .sale-badge {
    position: absolute; top: 0.8rem; left: 0.8rem;
    padding: 0.25rem 0.65rem;
    background: var(--black);
    font-size: 0.55rem; font-weight: 600;
    letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--gold);
  }

  .wishlist-btn {
    position: absolute; top: 0.8rem; right: 0.8rem;
    width: 30px; height: 30px;
    background: rgba(248,246,242,0.85);
    backdrop-filter: blur(8px);
    border: none; cursor: none;
    display: flex; align-items: center; justify-content: center;
    opacity: 0;
    transform: translateY(-6px);
    transition: opacity 0.35s, transform 0.35s var(--transition);
  }
  .product-card:hover .wishlist-btn { opacity: 1; transform: translateY(0); }
  .wishlist-btn svg { width: 14px; height: 14px; stroke: var(--black); fill: none; stroke-width: 1.4; }
  .wishlist-btn.active svg { fill: var(--black); }

  .product-info { padding: 1rem 0.2rem 0; }
  .product-name {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.05rem; font-weight: 400;
    color: var(--black); letter-spacing: 0.01em;
    margin-bottom: 0.25rem;
  }
  .product-category {
    font-size: 0.6rem; font-weight: 500;
    letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--grey); margin-bottom: 0.55rem;
  }
  .product-price {
    display: flex; align-items: center; gap: 0.7rem;
  }
  .price-current {
    font-size: 0.82rem; font-weight: 500;
    color: var(--black);
  }
  .price-original {
    font-size: 0.75rem; color: var(--grey);
    text-decoration: line-through;
  }
  .price-sale { color: #8b3a3a; }

  /* ── FEATURE STRIP ── */
  .feature-strip {
    background: var(--black);
    padding: 1.2rem 2.4rem;
    display: flex; align-items: center; justify-content: center; gap: 4rem;
    overflow-x: auto;
  }
  .feature-strip::-webkit-scrollbar { display: none; }
  .feature-item {
    display: flex; align-items: center; gap: 0.7rem;
    white-space: nowrap;
  }
  .feature-item svg { width: 16px; height: 16px; stroke: var(--gold); fill: none; stroke-width: 1.4; }
  .feature-item span {
    font-size: 0.62rem; font-weight: 500;
    letter-spacing: 0.2em; text-transform: uppercase;
    color: rgba(248,246,242,0.7);
  }

  /* ── EDITORIAL BANNER ── */
  .editorial-banner {
    display: grid; grid-template-columns: 1fr 1fr;
    height: 72vh; min-height: 480px;
    overflow: hidden;
  }
  .editorial-panel {
    position: relative; overflow: hidden;
  }
  .editorial-panel-img {
    width: 100%; height: 100%; object-fit: cover;
    transition: transform 1.2s var(--transition);
    filter: saturate(0.8);
  }
  .editorial-panel:hover .editorial-panel-img { transform: scale(1.04); }
  .editorial-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(10,10,10,0.75) 0%, transparent 55%);
    display: flex; flex-direction: column;
    justify-content: flex-end;
    padding: 2.5rem;
  }
  .editorial-tag {
    font-size: 0.6rem; letter-spacing: 0.3em;
    text-transform: uppercase; color: var(--gold); margin-bottom: 0.5rem;
  }
  .editorial-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(1.8rem, 3.5vw, 3rem);
    font-weight: 300;
    color: var(--white); line-height: 1;
    margin-bottom: 1.2rem;
  }
  .editorial-title em { font-style: italic; }
  .editorial-link {
    display: inline-flex; align-items: center; gap: 0.8rem;
    font-size: 0.65rem; font-weight: 500;
    letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--white); text-decoration: none;
    transition: color 0.3s;
  }
  .editorial-link::after {
    content: '→';
    transition: transform 0.3s var(--transition);
  }
  .editorial-link:hover { color: var(--gold); }
  .editorial-link:hover::after { transform: translateX(4px); }

  /* ── FOOTER ── */
  footer {
    background: var(--black);
    padding: 5rem 2.4rem 2.5rem;
  }
  .footer-top {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr 1.5fr;
    gap: 3rem;
    padding-bottom: 3rem;
    border-bottom: 1px solid rgba(248,246,242,0.1);
    margin-bottom: 2rem;
  }
  .footer-brand .logo-footer {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2.2rem; font-weight: 300;
    letter-spacing: 0.15em;
    color: var(--white);
    display: block; margin-bottom: 1.2rem;
  }
  .footer-brand p {
    font-size: 0.75rem; line-height: 1.8;
    color: rgba(248,246,242,0.5);
    max-width: 240px;
  }
  .footer-col h5 {
    font-size: 0.6rem; font-weight: 600;
    letter-spacing: 0.28em; text-transform: uppercase;
    color: rgba(248,246,242,0.4); margin-bottom: 1.2rem;
  }
  .footer-col ul { list-style: none; }
  .footer-col ul li { margin-bottom: 0.65rem; }
  .footer-col ul li a {
    font-size: 0.78rem; color: rgba(248,246,242,0.65);
    text-decoration: none;
    transition: color 0.3s;
  }
  .footer-col ul li a:hover { color: var(--white); }

  .newsletter-form {
    display: flex; margin-top: 0.5rem;
    border-bottom: 1px solid rgba(248,246,242,0.3);
    transition: border-color 0.3s;
  }
  .newsletter-form:focus-within { border-color: var(--gold); }
  .newsletter-form input {
    flex: 1; background: transparent; border: none; outline: none;
    font-family: 'Archivo', sans-serif;
    font-size: 0.72rem; color: var(--white);
    padding: 0.6rem 0;
  }
  .newsletter-form input::placeholder { color: rgba(248,246,242,0.35); }
  .newsletter-form button {
    background: transparent; border: none;
    color: var(--gold); font-size: 0.9rem;
    cursor: none; padding: 0 0.3rem;
    transition: transform 0.3s var(--transition);
  }
  .newsletter-form button:hover { transform: translateX(4px); }

  .footer-bottom {
    display: flex; align-items: center; justify-content: space-between;
    flex-wrap: wrap; gap: 1rem;
  }
  .footer-bottom p {
    font-size: 0.65rem; color: rgba(248,246,242,0.3);
    letter-spacing: 0.08em;
  }
  .social-icons {
    display: flex; gap: 1.2rem;
  }
  .social-icons a {
    font-size: 0.62rem; font-weight: 500;
    letter-spacing: 0.2em; text-transform: uppercase;
    color: rgba(248,246,242,0.4);
    text-decoration: none;
    transition: color 0.3s;
  }
  .social-icons a:hover { color: var(--white); }

  /* ── MODAL ── */
  .modal-overlay {
    position: fixed; inset: 0; z-index: 500;
    background: rgba(10,10,10,0.7);
    backdrop-filter: blur(8px);
    display: flex; align-items: center; justify-content: center;
    opacity: 0; pointer-events: none;
    transition: opacity 0.4s var(--transition);
  }
  .modal-overlay.open { opacity: 1; pointer-events: all; }

  .modal {
    background: var(--white);
    max-width: 860px; width: 90%;
    max-height: 90vh; overflow-y: auto;
    display: grid; grid-template-columns: 1fr 1fr;
    transform: translateY(20px) scale(0.98);
    transition: transform 0.5s var(--transition);
  }
  .modal-overlay.open .modal { transform: translateY(0) scale(1); }

  .modal-image {
    width: 100%; aspect-ratio: 3/4;
    object-fit: cover;
  }
  .modal-info { padding: 2.5rem; }
  .modal-category {
    font-size: 0.6rem; letter-spacing: 0.25em;
    text-transform: uppercase; color: var(--grey);
    margin-bottom: 0.6rem;
  }
  .modal-name {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2rem; font-weight: 300;
    color: var(--black); line-height: 1.1;
    margin-bottom: 0.8rem;
  }
  .modal-price {
    font-size: 1.1rem; font-weight: 500;
    color: var(--black); margin-bottom: 1.8rem;
  }
  .modal-desc {
    font-size: 0.78rem; line-height: 1.8;
    color: rgba(10,10,10,0.6); margin-bottom: 1.8rem;
  }
  .size-label {
    font-size: 0.6rem; font-weight: 600;
    letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--mid); margin-bottom: 0.7rem;
    display: block;
  }
  .sizes {
    display: flex; gap: 0.5rem; margin-bottom: 1.8rem; flex-wrap: wrap;
  }
  .size-btn {
    width: 40px; height: 40px;
    border: 1px solid rgba(10,10,10,0.15);
    background: transparent;
    font-size: 0.68rem; font-weight: 500;
    color: var(--mid); cursor: none;
    transition: all 0.2s;
  }
  .size-btn:hover, .size-btn.selected {
    border-color: var(--black);
    background: var(--black); color: var(--white);
  }
  .add-to-cart {
    width: 100%;
    padding: 1.1rem;
    background: var(--black); color: var(--white);
    border: none; cursor: none;
    font-family: 'Archivo', sans-serif;
    font-size: 0.68rem; font-weight: 600;
    letter-spacing: 0.28em; text-transform: uppercase;
    position: relative; overflow: hidden;
    transition: background 0.4s;
  }
  .add-to-cart::before {
    content: '';
    position: absolute; inset: 0;
    background: var(--gold);
    transform: translateX(-101%);
    transition: transform 0.5s var(--transition);
  }
  .add-to-cart:hover::before { transform: translateX(0); }
  .add-to-cart span { position: relative; z-index: 1; }
  .modal-close {
    position: absolute; top: 1.2rem; right: 1.2rem;
    background: rgba(248,246,242,0.9); border: none;
    width: 36px; height: 36px;
    font-size: 1rem; cursor: none;
    transition: background 0.3s, transform 0.3s;
  }
  .modal-close:hover { background: var(--white); transform: rotate(90deg); }

  /* ── MOBILE ── */
  @media (max-width: 1024px) {
    .product-grid { grid-template-columns: repeat(3, 1fr); }
    .footer-top { grid-template-columns: 1fr 1fr; }
    .footer-brand { grid-column: 1 / -1; }
  }
  @media (max-width: 768px) {
    nav, .header-icons .icon-search, .header-icons .icon-account { display: none; }
    .hamburger { display: flex; }
    .product-grid {
      padding: 2rem 1rem 3rem;
      grid-template-columns: repeat(2, 1fr);
      gap: 1rem 0.7rem;
    }
    .filter-bar { padding: 0 1rem; top: 54px; }
    .feature-strip { gap: 2rem; }
    .editorial-banner { grid-template-columns: 1fr; height: auto; }
    .editorial-panel { height: 55vw; min-height: 260px; }
    .footer-top { grid-template-columns: 1fr 1fr; gap: 2rem; }
    .footer-brand { grid-column: 1 / -1; }
    header { padding: 1.1rem 1.2rem; }
    .collection-hero { padding: 2.5rem 1.5rem; }
    .modal { grid-template-columns: 1fr; }
    .modal-image { aspect-ratio: 16/9; }
  }
  @media (max-width: 480px) {
    .hero-title { font-size: clamp(4rem, 18vw, 6rem); }
    .product-grid { grid-template-columns: repeat(2, 1fr); gap: 0.8rem 0.5rem; }
    .editorial-panel { height: 70vw; }
  }

  /* ── MOBILE MENU ── */
  .mobile-menu {
    position: fixed; inset: 0; z-index: 300;
    background: var(--black);
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    gap: 2rem;
    transform: translateX(-100%);
    transition: transform 0.6s var(--transition);
  }
  .mobile-menu.open { transform: translateX(0); }
  .mobile-menu a {
    font-family: 'Cormorant Garamond', serif;
    font-size: 3rem; font-weight: 300;
    color: var(--white); text-decoration: none;
    transition: color 0.3s;
  }
  .mobile-menu a:hover { color: var(--gold); }
  .mobile-close {
    position: absolute; top: 1.5rem; right: 1.5rem;
    background: transparent; border: none;
    color: var(--white); font-size: 1.5rem; cursor: none;
  }

  /* ── SCROLL REVEAL ── */
  .reveal {
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.8s var(--transition), transform 0.8s var(--transition);
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }
</style>
</head>
<body>

<!-- CURSOR -->
<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- ══════════════════════════════════════
     LANDING / HERO
════════════════════════════════════════ -->
<div id="landing">
  <!-- BACKGROUND VIDEO — using a cinematic Unsplash/Pexels placeholder -->
  <!-- Replace src with your actual video file for production -->
  <video id="hero-video" autoplay muted loop playsinline
    poster="https://images.unsplash.com/photo-1558769132-cb1aea458c5e?w=1600&q=85">
    <source src="https://www.pexels.com/download/video/4772991/" type="video/mp4"/>
    <!-- Fallback: cinematic poster image if video fails -->
  </video>

  <div class="hero-overlay"></div>
  <div class="hero-grain"></div>

  <div class="hero-content">
    <p class="hero-eyebrow">Autumn — Winter 2026</p>
    <h1 class="hero-title">VØ<span>ID</span></h1>
    <p class="hero-subtitle">Outerwear Collection — Silence in Form</p>
    <button class="hero-cta" id="enterBtn">
      <span>Enter Store</span>
      <div class="cta-arrow"></div>
    </button>
  </div>

  <div class="hero-scroll-hint">
    <span>Or tap anywhere</span>
    <div class="scroll-line"></div>
  </div>
</div>

<!-- ══════════════════════════════════════
     MAIN STORE
════════════════════════════════════════ -->
<div id="store">

  <!-- HEADER -->
  <header id="header">
    <a href="#" class="logo">VØID</a>
    <nav>
      <a href="#" class="nav-link">Home</a>
      <a href="#" class="nav-link">Shop</a>
      <a href="#" class="nav-link">Collections</a>
      <a href="#" class="nav-link">About</a>
    </nav>
    <div class="header-icons">
      <svg class="icon-search" viewBox="0 0 24 24"><circle cx="11" cy="11" r="7"/><line x1="16.5" y1="16.5" x2="22" y2="22"/></svg>
      <svg class="icon-account" viewBox="0 0 24 24"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
      <div class="cart-badge">
        <svg viewBox="0 0 24 24"><path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/><line x1="3" y1="6" x2="21" y2="6"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>
      </div>
      <button class="hamburger" id="hamburgerBtn" aria-label="Menu">
        <span></span><span></span><span></span>
      </button>
    </div>
  </header>

  <!-- MOBILE MENU -->
  <div class="mobile-menu" id="mobileMenu">
    <button class="mobile-close" id="mobileClose">✕</button>
    <a href="#">Home</a>
    <a href="#">Shop</a>
    <a href="#">Collections</a>
    <a href="#">About</a>
  </div>

  <div class="store-wrapper">

    <!-- COLLECTION HERO -->
    <section class="collection-hero">
      <div class="collection-hero-bg"></div>
      <div class="collection-hero-content">
        <p class="collection-hero-tag">New Arrivals — AW 2026</p>
        <h2 class="collection-hero-title">Outerwear<br/><em>Collection</em></h2>
        <p class="collection-hero-count">24 pieces</p>
      </div>
    </section>

    <!-- FEATURE STRIP -->
    <div class="feature-strip">
      <div class="feature-item">
        <svg viewBox="0 0 24 24"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
        <span>Free shipping over $250</span>
      </div>
      <div class="feature-item">
        <svg viewBox="0 0 24 24"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/></svg>
        <span>Returns within 30 days</span>
      </div>
      <div class="feature-item">
        <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
        <span>Sustainably crafted</span>
      </div>
      <div class="feature-item">
        <svg viewBox="0 0 24 24"><rect x="1" y="4" width="22" height="16" rx="2" ry="2"/><line x1="1" y1="10" x2="23" y2="10"/></svg>
        <span>Secure checkout</span>
      </div>
    </div>

    <!-- FILTER BAR -->
    <div class="filter-bar">
      <div class="filter-groups">
        <button class="filter-btn active">All</button>
        <button class="filter-btn">Coats</button>
        <button class="filter-btn">Jackets</button>
        <button class="filter-btn">Vests</button>
        <button class="filter-btn">Knitwear</button>
        <button class="filter-btn">
          Size
          <svg viewBox="0 0 10 6"><path d="M1 1l4 4 4-4" stroke="currentColor" fill="none" stroke-width="1.2"/></svg>
        </button>
        <button class="filter-btn">
          Colour
          <svg viewBox="0 0 10 6"><path d="M1 1l4 4 4-4" stroke="currentColor" fill="none" stroke-width="1.2"/></svg>
        </button>
      </div>
      <select class="sort-select">
        <option>Sort: Featured</option>
        <option>Price: Low–High</option>
        <option>Price: High–Low</option>
        <option>Newest</option>
      </select>
    </div>

    <!-- PRODUCT GRID -->
    <section class="product-grid" id="productGrid">

      <!-- Product 1 -->
      <article class="product-card" data-id="1">
        <div class="product-image-wrap">
          <img src="https://images.unsplash.com/photo-1539109136881-3be0616acf4b?w=600&q=80" alt="Onyx Overcoat"/>
          <img class="img-hover" src="https://images.unsplash.com/photo-1594938298603-c8148c4b4d51?w=600&q=80" alt="Onyx Overcoat alt"/>
          <div class="quick-view"><button>Quick View</button></div>
          <button class="wishlist-btn">
            <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
          </button>
        </div>
        <div class="product-info">
          <p class="product-category">Coat</p>
          <h3 class="product-name">Onyx Overcoat</h3>
          <div class="product-price"><span class="price-current">$895</span></div>
        </div>
      </article>

      <!-- Product 2 -->
      <article class="product-card" data-id="2">
        <div class="product-image-wrap">
          <img src="https://images.unsplash.com/photo-1551488831-00ddcb6c6bd3?w=600&q=80" alt="Tundra Parka"/>
          <img class="img-hover" src="https://images.unsplash.com/photo-1520975916090-3105956dac38?w=600&q=80" alt="Tundra Parka alt"/>
          <div class="quick-view"><button>Quick View</button></div>
          <button class="wishlist-btn">
            <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
          </button>
          <span class="sale-badge">Sale</span>
        </div>
        <div class="product-info">
          <p class="product-category">Jacket</p>
          <h3 class="product-name">Tundra Parka</h3>
          <div class="product-price">
            <span class="price-current price-sale">$620</span>
            <span class="price-original">$890</span>
          </div>
        </div>
      </article>

      <!-- Product 3 -->
      <article class="product-card" data-id="3">
        <div class="product-image-wrap">
          <img src="https://images.unsplash.com/photo-1576566588028-4147f3842f27?w=600&q=80" alt="Void Blazer"/>
          <img class="img-hover" src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=600&q=80" alt="Void Blazer alt"/>
          <div class="quick-view"><button>Quick View</button></div>
          <button class="wishlist-btn">
            <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
          </button>
        </div>
        <div class="product-info">
          <p class="product-category">Blazer</p>
          <h3 class="product-name">Void Blazer</h3>
          <div class="product-price"><span class="price-current">$545</span></div>
        </div>
      </article>

      <!-- Product 4 -->
      <article class="product-card" data-id="4">
        <div class="product-image-wrap">
          <img src="https://images.unsplash.com/photo-1515886657613-9f3515b0c78f?w=600&q=80" alt="Ash Trench"/>
          <img class="img-hover" src="https://images.unsplash.com/photo-1487222477894-8943e31ef7b2?w=600&q=80" alt="Ash Trench alt"/>
          <div class="quick-view"><button>Quick View</button></div>
          <button class="wishlist-btn">
            <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
          </button>
          <span class="sale-badge">New</span>
        </div>
        <div class="product-info">
          <p class="product-category">Trench</p>
          <h3 class="product-name">Ash Trench</h3>
          <div class="product-price"><span class="price-current">$1,120</span></div>
        </div>
      </article>

      <!-- Product 5 -->
      <article class="product-card" data-id="5">
        <div class="product-image-wrap">
          <img src="https://images.unsplash.com/photo-1499971856191-1a420a42b498?w=600&q=80" alt="Dusk Vest"/>
          <img class="img-hover" src="https://images.unsplash.com/photo-1509631179647-0177331693ae?w=600&q=80" alt="Dusk Vest alt"/>
          <div class="quick-view"><button>Quick View</button></div>
          <button class="wishlist-btn">
            <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
          </button>
        </div>
        <div class="product-info">
          <p class="product-category">Vest</p>
          <h3 class="product-name">Dusk Vest</h3>
          <div class="product-price"><span class="price-current">$340</span></div>
        </div>
      </article>

      <!-- Product 6 -->
      <article class="product-card" data-id="6">
        <div class="product-image-wrap">
          <img src="https://images.unsplash.com/photo-1525507119028-ed4c629a60a3?w=600&q=80" alt="Fog Bomber"/>
          <img class="img-hover" src="https://images.unsplash.com/photo-1593030761757-71fae45fa0e7?w=600&q=80" alt="Fog Bomber alt"/>
          <div class="quick-view"><button>Quick View</button></div>
          <button class="wishlist-btn">
            <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
          </button>
          <span class="sale-badge">Sale</span>
        </div>
        <div class="product-info">
          <p class="product-category">Jacket</p>
          <h3 class="product-name">Fog Bomber</h3>
          <div class="product-price">
            <span class="price-current price-sale">$480</span>
            <span class="price-original">$660</span>
          </div>
        </div>
      </article>

      <!-- Product 7 -->
      <article class="product-card" data-id="7">
        <div class="product-image-wrap">
          <img src="https://images.unsplash.com/photo-1554412933-514a83d2f3c8?w=600&q=80" alt="Slate Caban"/>
          <img class="img-hover" src="https://images.unsplash.com/photo-1544022613-e87ca75a784a?w=600&q=80" alt="Slate Caban alt"/>
          <div class="quick-view"><button>Quick View</button></div>
          <button class="wishlist-btn">
            <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
          </button>
          <span class="sale-badge">New</span>
        </div>
        <div class="product-info">
          <p class="product-category">Coat</p>
          <h3 class="product-name">Slate Caban</h3>
          <div class="product-price"><span class="price-current">$780</span></div>
        </div>
      </article>

      <!-- Product 8 -->
      <article class="product-card" data-id="8">
        <div class="product-image-wrap">
          <img src="https://images.unsplash.com/photo-1508214751196-bcfd4ca60f91?w=600&q=80" alt="Ember Knit"/>
          <img class="img-hover" src="https://images.unsplash.com/photo-1519931552651-5bbdd4dc0b22?w=600&q=80" alt="Ember Knit alt"/>
          <div class="quick-view"><button>Quick View</button></div>
          <button class="wishlist-btn">
            <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
          </button>
        </div>
        <div class="product-info">
          <p class="product-category">Knitwear</p>
          <h3 class="product-name">Ember Knit</h3>
          <div class="product-price"><span class="price-current">$295</span></div>
        </div>
      </article>

    </section>

    <!-- EDITORIAL BANNER -->
    <section class="editorial-banner reveal">
      <div class="editorial-panel">
        <img class="editorial-panel-img"
          src="https://images.unsplash.com/photo-1490481651871-ab68de25d43d?w=900&q=80"
          alt="The Weight of Silence"/>
        <div class="editorial-overlay">
          <p class="editorial-tag">Editorial</p>
          <h3 class="editorial-title">The Weight<br/>of <em>Silence</em></h3>
          <a href="#" class="editorial-link">View Lookbook</a>
        </div>
      </div>
      <div class="editorial-panel">
        <img class="editorial-panel-img"
          src="https://images.unsplash.com/photo-1469334031218-e382a71b716b?w=900&q=80"
          alt="Crafted in Milan"/>
        <div class="editorial-overlay">
          <p class="editorial-tag">Craftsmanship</p>
          <h3 class="editorial-title"><em>Crafted</em><br/>in Milan</h3>
          <a href="#" class="editorial-link">Our Process</a>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="reveal">
      <div class="footer-top">
        <div class="footer-brand">
          <span class="logo-footer">VØID</span>
          <p>Outerwear made for those who move between worlds. Designed in silence, crafted with intention. AW 2026.</p>
        </div>
        <div class="footer-col">
          <h5>Shop</h5>
          <ul>
            <li><a href="#">New Arrivals</a></li>
            <li><a href="#">Outerwear</a></li>
            <li><a href="#">Knitwear</a></li>
            <li><a href="#">Accessories</a></li>
            <li><a href="#">Sale</a></li>
          </ul>
        </div>
        <div class="footer-col">
          <h5>Company</h5>
          <ul>
            <li><a href="#">About VØID</a></li>
            <li><a href="#">Sustainability</a></li>
            <li><a href="#">Press</a></li>
            <li><a href="#">Careers</a></li>
          </ul>
        </div>
        <div class="footer-col">
          <h5>Support</h5>
          <ul>
            <li><a href="#">Contact Us</a></li>
            <li><a href="#">Shipping & Returns</a></li>
            <li><a href="#">Size Guide</a></li>
            <li><a href="#">Privacy Policy</a></li>
            <li><a href="#">Terms of Service</a></li>
          </ul>
        </div>
        <div class="footer-col">
          <h5>The Inner Circle</h5>
          <p style="font-size:0.72rem;color:rgba(248,246,242,0.45);line-height:1.7;margin-bottom:1rem;">Early access, editorial drops, and nothing else.</p>
          <form class="newsletter-form" onsubmit="return false">
            <input type="email" placeholder="Your email"/>
            <button type="submit">→</button>
          </form>
        </div>
      </div>
      <div class="footer-bottom">
        <p>© 2026 VØID Studio. All rights reserved.</p>
        <div class="social-icons">
          <a href="#">Instagram</a>
          <a href="#">Pinterest</a>
          <a href="#">Twitter</a>
          <a href="#">Substack</a>
        </div>
      </div>
    </footer>

  </div>
</div>

<!-- QUICK VIEW MODAL -->
<div class="modal-overlay" id="modal">
  <div class="modal" id="modalBox" style="position:relative">
    <button class="modal-close" id="modalClose">✕</button>
    <img id="modalImg" class="modal-image" src="" alt=""/>
    <div class="modal-info">
      <p class="modal-category" id="modalCat"></p>
      <h2 class="modal-name" id="modalName"></h2>
      <p class="modal-price" id="modalPrice"></p>
      <p class="modal-desc" id="modalDesc"></p>
      <span class="size-label">Select Size</span>
      <div class="sizes">
        <button class="size-btn">XS</button>
        <button class="size-btn">S</button>
        <button class="size-btn selected">M</button>
        <button class="size-btn">L</button>
        <button class="size-btn">XL</button>
      </div>
      <button class="add-to-cart" id="addCartBtn"><span>Add to Cart</span></button>
    </div>
  </div>
</div>

<script>
/* ── CURSOR ── */
const cursor = document.getElementById('cursor');
const ring   = document.getElementById('cursor-ring');
let mx = 0, my = 0, rx = 0, ry = 0;

document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.left = mx + 'px';
  cursor.style.top  = my + 'px';
});

(function animRing() {
  rx += (mx - rx) * 0.12;
  ry += (my - ry) * 0.12;
  ring.style.left = rx + 'px';
  ring.style.top  = ry + 'px';
  requestAnimationFrame(animRing);
})();

/* ── LANDING → STORE TRANSITION ── */
const landing  = document.getElementById('landing');
const store    = document.getElementById('store');
const enterBtn = document.getElementById('enterBtn');

function enterStore() {
  landing.classList.add('exit');
  store.classList.add('visible');
  document.body.style.overflowY = 'auto';
  setTimeout(() => { landing.style.display = 'none'; }, 1500);
}

enterBtn.addEventListener('click', e => { e.stopPropagation(); enterStore(); });
landing.addEventListener('click', enterStore);

document.body.style.overflowY = 'hidden';

/* ── HEADER SCROLL ── */
const header = document.getElementById('header');
window.addEventListener('scroll', () => {
  header.classList.toggle('scrolled', window.scrollY > 60);
}, { passive: true });

/* ── FILTER TABS ── */
document.querySelectorAll('.filter-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
  });
});

/* ── WISHLIST TOGGLE ── */
document.querySelectorAll('.wishlist-btn').forEach(btn => {
  btn.addEventListener('click', e => {
    e.stopPropagation();
    btn.classList.toggle('active');
  });
});

/* ── QUICK VIEW MODAL ── */
const products = {
  1: { name: 'Onyx Overcoat', cat: 'Coat', price: '$895',
       img: 'https://images.unsplash.com/photo-1539109136881-3be0616acf4b?w=700&q=85',
       desc: 'A sculptural long-line overcoat in Japanese boiled wool. Clean lapel, single-button closure, unlined. The definitive layer.' },
  2: { name: 'Tundra Parka', cat: 'Jacket', price: '$620',
       img: 'https://images.unsplash.com/photo-1551488831-00ddcb6c6bd3?w=700&q=85',
       desc: 'Technical outer shell with reclaimed down fill. Storm hood, mag-clip closures, interior security zip. Ready for everything.' },
  3: { name: 'Void Blazer',  cat: 'Blazer', price: '$545',
       img: 'https://images.unsplash.com/photo-1576566588028-4147f3842f27?w=700&q=85',
       desc: 'A deconstructed single-breast blazer in Belgian linen. Minimal canvas, unpadded shoulder. Weightless authority.' },
  4: { name: 'Ash Trench',   cat: 'Trench', price: '$1,120',
       img: 'https://images.unsplash.com/photo-1515886657613-9f3515b0c78f?w=700&q=85',
       desc: 'Double-breasted trench in deadstock gabardine. Storm patch, D-ring belt, extended rear vent. Timeless construction.' },
  5: { name: 'Dusk Vest',    cat: 'Vest',   price: '$340',
       img: 'https://images.unsplash.com/photo-1499971856191-1a420a42b498?w=700&q=85',
       desc: 'Cropped vest with oversized zip-thru in brushed nylon. Lightweight structure. Layer or wear alone.' },
  6: { name: 'Fog Bomber',   cat: 'Jacket', price: '$480',
       img: 'https://images.unsplash.com/photo-1525507119028-ed4c629a60a3?w=700&q=85',
       desc: 'Oversized MA-1 silhouette in pearl-dyed ripstop. Ribbed cuffs, internal storage, tonal hardware.' },
  7: { name: 'Slate Caban',  cat: 'Coat',   price: '$780',
       img: 'https://images.unsplash.com/photo-1554412933-514a83d2f3c8?w=700&q=85',
       desc: 'Maritime pea coat updated with a modern dropped shoulder. Double-button front, notched lapel, patch pockets.' },
  8: { name: 'Ember Knit',   cat: 'Knitwear', price: '$295',
       img: 'https://images.unsplash.com/photo-1508214751196-bcfd4ca60f91?w=700&q=85',
       desc: 'Heavyweight boucle roll-neck in Mongolian cashmere blend. Dropped shoulder, ribbed body. The warmest silence.' }
};

const modal     = document.getElementById('modal');
const modalClose = document.getElementById('modalClose');
const addCart   = document.getElementById('addCartBtn');

document.querySelectorAll('.quick-view button').forEach(btn => {
  btn.addEventListener('click', e => {
    e.stopPropagation();
    const card = btn.closest('.product-card');
    const id   = card.dataset.id;
    const p    = products[id];
    document.getElementById('modalImg').src    = p.img;
    document.getElementById('modalCat').textContent  = p.cat;
    document.getElementById('modalName').textContent = p.name;
    document.getElementById('modalPrice').textContent = p.price;
    document.getElementById('modalDesc').textContent  = p.desc;
    modal.classList.add('open');
    document.body.style.overflow = 'hidden';
  });
});

function closeModal() {
  modal.classList.remove('open');
  document.body.style.overflow = '';
}
modalClose.addEventListener('click', closeModal);
modal.addEventListener('click', e => { if (e.target === modal) closeModal(); });

/* Size selector */
document.querySelectorAll('.size-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.size-btn').forEach(b => b.classList.remove('selected'));
    btn.classList.add('selected');
  });
});

/* Add to cart feedback */
addCart.addEventListener('click', () => {
  const s = addCart.querySelector('span');
  s.textContent = 'Added ✓';
  addCart.style.background = '#2a4a2a';
  setTimeout(() => { s.textContent = 'Add to Cart'; addCart.style.background = ''; }, 2000);
});

/* ── MOBILE MENU ── */
const hamburger   = document.getElementById('hamburgerBtn');
const mobileMenu  = document.getElementById('mobileMenu');
const mobileClose = document.getElementById('mobileClose');

hamburger.addEventListener('click', () => { mobileMenu.classList.add('open'); });
mobileClose.addEventListener('click', () => { mobileMenu.classList.remove('open'); });

/* ── SCROLL REVEAL ── */
const revealEls = document.querySelectorAll('.reveal');
const io = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); io.unobserve(e.target); } });
}, { threshold: 0.12 });
revealEls.forEach(el => io.observe(el));

/* ── KEYBOARD: ESC closes modal ── */
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeModal(); });
</script>
</body>
</html>
