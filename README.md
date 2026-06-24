
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>NALOP · PULSE ON</title>
  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', 'Helvetica Neue', system-ui, -apple-system, sans-serif;
    }

    body {
      background: #f5f3f0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      padding: 1.5rem 1rem;
    }

    /* ----- LOGIN OVERLAY ----- */
    #loginOverlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      backdrop-filter: blur(8px);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 999;
      transition: opacity 0.5s ease;
    }

    #loginOverlay.hidden {
      opacity: 0;
      pointer-events: none;
    }

    .login-box {
      background: white;
      max-width: 380px;
      width: 100%;
      padding: 2.5rem 2rem 2.2rem;
      border-radius: 40px;
      box-shadow: 0 30px 60px rgba(0, 0, 0, 0.3);
      text-align: center;
      animation: loginPop 0.5s ease;
    }

    @keyframes loginPop {
      0% { opacity: 0; transform: scale(0.9) translateY(20px); }
      100% { opacity: 1; transform: scale(1) translateY(0); }
    }

    .login-box .brand {
      font-size: 2.4rem;
      font-weight: 800;
      letter-spacing: -1px;
      color: #111;
      margin-bottom: 0.2rem;
    }
    .login-box .brand span {
      color: #b3002d;
    }
    .login-box .sub {
      color: #555;
      font-size: 0.8rem;
      margin-bottom: 1.8rem;
      font-weight: 500;
      border-bottom: 1px solid #eee;
      padding-bottom: 0.8rem;
    }

    .login-box label {
      display: block;
      text-align: left;
      font-weight: 600;
      font-size: 0.8rem;
      color: #222;
      margin: 1rem 0 0.3rem 0.3rem;
    }

    .login-box input {
      width: 100%;
      padding: 0.8rem 1rem;
      border: 2px solid #e0ddd8;
      border-radius: 50px;
      font-size: 0.95rem;
      background: #fafaf9;
      transition: 0.2s;
      outline: none;
    }

    .login-box input:focus {
      border-color: #b3002d;
      background: white;
      box-shadow: 0 0 0 4px #b3002d22;
    }

    .login-btn {
      width: 100%;
      padding: 0.9rem;
      margin-top: 1.8rem;
      background: #111;
      color: white;
      border: none;
      border-radius: 50px;
      font-weight: 700;
      font-size: 1rem;
      cursor: pointer;
      transition: 0.25s;
      letter-spacing: 0.5px;
    }

    .login-btn:hover {
      background: #b3002d;
      transform: scale(1.01);
      box-shadow: 0 8px 20px #b3002d44;
    }

    .login-error {
      color: #b3002d;
      font-size: 0.8rem;
      margin-top: 0.8rem;
      min-height: 1.4rem;
      font-weight: 500;
    }

    /* ----- MAIN CONTENT (hidden until login) ----- */
    #mainContent {
      width: 100%;
      max-width: 900px;
      display: none;
      flex-direction: column;
      align-items: center;
    }

    #mainContent.show {
      display: flex;
      animation: fadeIn 0.6s ease;
    }

    @keyframes fadeIn {
      0% { opacity: 0; transform: translateY(10px); }
      100% { opacity: 1; transform: translateY(0); }
    }

    .card {
      width: 100%;
      background: white;
      border-radius: 32px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.08), 0 6px 12px rgba(0, 0, 0, 0.05);
      padding: 2rem 1.8rem;
      margin-bottom: 2rem;
      transition: all 0.3s ease;
      animation: cardPop 0.5s ease;
    }

    @keyframes cardPop {
      0% { opacity: 0; transform: scale(0.97); }
      100% { opacity: 1; transform: scale(1); }
    }

    .card:hover {
      box-shadow: 0 24px 48px rgba(0, 0, 0, 0.12);
    }

    /* tour header */
    .tour-header {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      border-bottom: 2px solid #1e1e1e;
      padding-bottom: 0.75rem;
      margin-bottom: 1.5rem;
      flex-wrap: wrap;
      animation: slideFromLeft 0.6s ease;
    }

    @keyframes slideFromLeft {
      0% { opacity: 0; transform: translateX(-20px); }
      100% { opacity: 1; transform: translateX(0); }
    }

    .tour-title {
      font-size: 1.8rem;
      font-weight: 700;
      letter-spacing: -0.02em;
      color: #111;
      display: flex;
      align-items: center;
      gap: 8px;
      flex-wrap: wrap;
    }

    .tour-title span {
      background: #111;
      color: white;
      padding: 0.1rem 0.8rem;
      border-radius: 40px;
      font-size: 0.9rem;
      font-weight: 500;
      letter-spacing: 0.5px;
      animation: pulseBadge 2s infinite;
    }

    @keyframes pulseBadge {
      0% { transform: scale(1); }
      50% { transform: scale(1.03); background: #2a2a2a; }
      100% { transform: scale(1); }
    }

    .tour-year {
      font-weight: 600;
      color: #333;
      font-size: 1rem;
      background: #efedea;
      padding: 0.2rem 1.2rem;
      border-radius: 40px;
      transition: 0.2s;
    }
    .tour-year:hover {
      background: #d6d2cc;
      transform: scale(1.02);
    }

    /* pulse badge */
    .pulse-badge {
      display: flex;
      align-items: center;
      gap: 6px;
      margin: 0.5rem 0 1.2rem 0;
      animation: float 3s ease-in-out infinite;
    }

    @keyframes float {
      0% { transform: translateY(0); }
      50% { transform: translateY(-5px); }
      100% { transform: translateY(0); }
    }

    .pulse-badge i {
      font-size: 1.8rem;
      color: #b3002d;
      animation: heartbeat 1.4s ease-in-out infinite;
    }

    @keyframes heartbeat {
      0% { transform: scale(1); }
      14% { transform: scale(1.2); }
      28% { transform: scale(1); }
      42% { transform: scale(1.15); }
      70% { transform: scale(1); }
      100% { transform: scale(1); }
    }

    .pulse-badge h2 {
      font-weight: 700;
      font-size: 2.2rem;
      letter-spacing: -0.02em;
      color: #0f0f0f;
    }

    .pulse-badge small {
      background: #b3002d;
      color: white;
      font-weight: 600;
      padding: 0.1rem 0.9rem;
      border-radius: 30px;
      font-size: 0.7rem;
      letter-spacing: 0.6px;
      margin-left: 6px;
      animation: pulseBadge 2.2s infinite;
    }

    /* section label */
    .section-label {
      font-weight: 700;
      font-size: 1.1rem;
      border-bottom: 2px solid #d0d0d0;
      padding-bottom: 0.3rem;
      margin: 2rem 0 1.2rem 0;
      letter-spacing: -0.3px;
      color: #1a1a1a;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .section-label i {
      color: #b3002d;
      font-size: 1rem;
      animation: sparkle 2s infinite;
    }

    @keyframes sparkle {
      0% { opacity: 0.7; transform: rotate(0deg); }
      50% { opacity: 1; transform: rotate(8deg); }
      100% { opacity: 0.7; transform: rotate(0deg); }
    }

    /* product grid */
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(170px, 1fr));
      gap: 1.2rem 0.8rem;
    }

    .product-item {
      background: #fafaf9;
      border-radius: 20px;
      padding: 0.8rem 0.6rem 0.8rem 0.6rem;
      border: 1px solid #f0eeeb;
      display: flex;
      flex-direction: column;
      transition: all 0.25s cubic-bezier(0.2, 0.9, 0.3, 1.2);
      animation: itemFade 0.5s ease forwards;
      opacity: 0;
      transform: translateY(10px);
    }

    .product-item:nth-child(1) { animation-delay: 0.05s; }
    .product-item:nth-child(2) { animation-delay: 0.10s; }
    .product-item:nth-child(3) { animation-delay: 0.15s; }
    .product-item:nth-child(4) { animation-delay: 0.20s; }
    .product-item:nth-child(5) { animation-delay: 0.25s; }
    .product-item:nth-child(6) { animation-delay: 0.30s; }

    @keyframes itemFade {
      0% { opacity: 0; transform: translateY(12px); }
      100% { opacity: 1; transform: translateY(0); }
    }

    .product-item:hover {
      background: #f3f0ec;
      border-color: #b3002d;
      transform: scale(1.02) translateY(-4px);
      box-shadow: 0 12px 20px rgba(179, 0, 45, 0.08);
    }

    .product-name {
      font-weight: 700;
      font-size: 0.9rem;
      line-height: 1.2;
      color: #0b0b0b;
      margin-bottom: 0.15rem;
      text-transform: uppercase;
      letter-spacing: -0.2px;
    }

    .product-variant {
      font-size: 0.7rem;
      color: #3f3f3f;
      font-weight: 500;
      text-transform: uppercase;
      background: #ece9e5;
      display: inline-block;
      padding: 0.05rem 0.5rem;
      border-radius: 30px;
      margin: 0.2rem 0 0.3rem;
      width: fit-content;
      letter-spacing: 0.2px;
    }

    .product-price {
      font-weight: 700;
      font-size: 0.95rem;
      color: #111;
      margin-top: 0.2rem;
      transition: 0.2s;
    }
    .product-item:hover .product-price {
      color: #b3002d;
    }

    .product-price small {
      font-weight: 400;
      font-size: 0.6rem;
      color: #4b4b4b;
      margin-left: 2px;
    }

    .badge-recommend {
      background: #b3002d;
      color: white;
      font-size: 0.55rem;
      font-weight: 700;
      padding: 0.1rem 0.5rem;
      border-radius: 30px;
      width: fit-content;
      letter-spacing: 0.4px;
      margin-bottom: 0.3rem;
      animation: recomPulse 2s infinite;
    }

    @keyframes recomPulse {
      0% { background: #b3002d; }
      50% { background: #d40038; box-shadow: 0 0 6px #b3002d77; }
      100% { background: #b3002d; }
    }

    .footer-note {
      font-size: 0.7rem;
      color: #6b6b6b;
      text-align: right;
      margin-top: 0.5rem;
      border-top: 1px solid #e5e2dd;
      padding-top: 0.8rem;
      letter-spacing: 0.2px;
      animation: fadeIn 1s ease;
    }
    .footer-note i {
      animation: spinSlow 6s linear infinite;
      display: inline-block;
    }
    @keyframes spinSlow {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    /* contact card */
    .contact-card-wrapper {
      width: 100%;
      padding: 0.5rem 0.5rem 0.5rem 1.8rem;
      background: #121212;
      border-radius: 60px;
      transition: 0.3s;
      animation: cardPop 0.6s ease;
    }
    .contact-card-wrapper:hover {
      background: #1c1c1c;
      box-shadow: 0 0 0 2px #b3002d44;
    }

    .contact-card {
      background: transparent;
      padding: 0.8rem 0.5rem;
      border-radius: 0;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 0.8rem;
      color: white;
    }

    .brand-name {
      font-size: 2rem;
      font-weight: 800;
      letter-spacing: -1px;
      color: white;
      margin-right: 10px;
      transition: 0.2s;
      display: inline-block;
    }
    .brand-name:hover {
      color: #ffb3b3;
      transform: scale(1.02);
    }

    .ig-handle {
      background: #333;
      padding: 0.2rem 1.2rem;
      border-radius: 40px;
      font-size: 0.8rem;
      font-weight: 600;
      color: #eee;
      transition: 0.2s;
    }
    .ig-handle:hover {
      background: #b3002d;
      color: white;
      transform: scale(1.02);
    }

    .contact-item {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 0.95rem;
      font-weight: 500;
      letter-spacing: -0.2px;
      transition: 0.2s;
    }
    .contact-item i {
      color: #ffb3b3;
      font-size: 1.1rem;
      width: 1.6rem;
      text-align: center;
      transition: 0.2s;
    }
    .contact-item:hover i {
      color: white;
      transform: scale(1.1);
    }
    .contact-item a {
      color: white;
      text-decoration: none;
      border-bottom: 1px dotted rgba(255, 255, 255, 0.2);
    }
    .contact-item a:hover {
      color: #ffb3b3;
      border-bottom: 1px solid #ffb3b3;
    }

    @media (max-width: 600px) {
      .card { padding: 1.5rem 1rem; }
      .tour-title { font-size: 1.2rem; }
      .contact-card { flex-direction: column; align-items: flex-start; gap: 0.8rem; }
      .product-grid { grid-template-columns: repeat(auto-fill, minmax(140px, 1fr)); }
      .contact-card-wrapper { padding: 1rem; border-radius: 32px; }
    }
  </style>
</head>
<body>

  <!-- LOGIN OVERLAY -->
  <div id="loginOverlay">
    <div class="login-box">
      <div class="brand">NALOP <span>·</span></div>
      <div class="sub">PULSE ON · TREASURE TOUR</div>

      <label for="emailInput"><i class="fas fa-envelope" style="margin-right: 6px;"></i> Email</label>
      <input type="email" id="emailInput" placeholder="contoh@email.com" value="nalop@gmail.com">

      <label for="passInput"><i class="fas fa-lock" style="margin-right: 6px;"></i> Password</label>
      <input type="password" id="passInput" placeholder="•••••••" value="12345">

      <button class="login-btn" id="loginBtn"><i class="fas fa-arrow-right-to-bracket" style="margin-right: 8px;"></i> MASUK</button>
      <div class="login-error" id="loginError"></div>
      <div style="margin-top: 0.8rem; font-size: 0.7rem; color: #888;">* password: 12345</div>
    </div>
  </div>

  <!-- MAIN CONTENT (setelah login) -->
  <div id="mainContent">
    <div class="card">
      <!-- tour header -->
      <div class="tour-header">
        <div class="tour-title">
          2025-26 TREASURE TOUR <span>PULSE ON</span>
        </div>
        <div class="tour-year">JAPAN</div>
      </div>

      <!-- PULSE ON big -->
      <div class="pulse-badge">
        <i class="fas fa-heartbeat"></i>
        <h2>PULSE ON</h2>
        <small>RECOMMEND</small>
      </div>

      <!-- RECOMMEND COMBINATION -->
      <div class="section-label">
        <i class="fas fa-star"></i> RECOMMEND COMBINATION
      </div>

      <div class="product-grid">
        <div class="product-item">
          <div class="badge-recommend">★ BEST</div>
          <div class="product-name">ZIP-UP HOODIE</div>
          <div class="product-variant">BLACK, GRAY, KHAKI / M,L</div>
          <div class="product-price">¥8,900 <small>tax in</small></div>
        </div>
        <div class="product-item">
          <div class="badge-recommend">★ BEST</div>
          <div class="product-name">RIDERS JACKET</div>
          <div class="product-variant">WHITE/RED, BLUE, BLACK / M,L</div>
          <div class="product-price">¥29,900 <small>tax in</small></div>
        </div>
        <div class="product-item">
          <div class="badge-recommend">★ BEST</div>
          <div class="product-name">HOODIE</div>
          <div class="product-variant">WHITE/RED, BLUE, BLACK / M,L</div>
          <div class="product-price">¥7,900 <small>tax in</small></div>
        </div>
      </div>

      <!-- RECOMMEND ITEM (first) -->
      <div class="section-label" style="margin-top: 2rem;">
        <i class="fas fa-thumbs-up"></i> RECOMMEND ITEM
      </div>

      <div class="product-grid">
        <div class="product-item"><div class="product-name">HEART CLEAR BAG</div><div class="product-variant">MEMBRIOTYPES</div><div class="product-price">¥2,900 <small>tax in</small></div></div>
        <div class="product-item"><div class="product-name">CLEAR POUCH</div><div class="product-variant">MEMBRIOTYPES</div><div class="product-price">¥1,200 <small>tax in</small></div></div>
        <div class="product-item"><div class="product-name">TOTE BAG</div><div class="product-variant">MEMBRIOTYPES</div><div class="product-price">¥2,900 <small>tax in</small></div></div>
        <div class="product-item"><div class="product-name">MIRRORED COMB</div><div class="product-variant">RED, BLACK</div><div class="product-price">¥1,500 <small>tax in</small></div></div>
        <div class="product-item"><div class="product-name">FRINGE-TRIMMED JACQUARD TOWEL</div><div class="product-variant">RED, BLACK</div><div class="product-price">¥2,500 <small>tax in</small></div></div>
        <div class="product-item"><div class="product-name">HAIR TIE WITH RIBBON</div><div class="product-variant">·</div><div class="product-price">¥800 <small>tax in</small></div></div>
      </div>

      <!-- BEANIE, TRACK JACKET, TOTE BAG -->
      <div class="product-grid" style="margin-top: 0.2rem;">
        <div class="product-item"><div class="product-name">BEANIE</div><div class="product-variant">RED, BLACK</div><div class="product-price">¥3,900 <small>tax in</small></div></div>
        <div class="product-item"><div class="product-name">TRACK JACKET</div><div class="product-variant">RED, BLACK / M,L</div><div class="product-price">¥12,900 <small>tax in</small></div></div>
        <div class="product-item"><div class="product-name">TOTE BAG</div><div class="product-variant">NATURAL, BLACK</div><div class="product-price">¥4,500 <small>tax in</small></div></div>
      </div>

      <!-- RECOMMEND ITEM (second) -->
      <div class="section-label" style="margin-top: 2rem;">
        <i class="fas fa-thumbs-up"></i> RECOMMEND ITEM
      </div>

      <div class="product-grid">
        <div class="product-item"><div class="product-name">SHIRT</div><div class="product-variant">OXFORD WHITE, DENIM BLUE, CHECK RED, CHECK BLACK</div><div class="product-price">¥8,900 <small>tax in</small></div></div>
        <div class="product-item"><div class="product-name">LONG-SLEEVE T-SHIRT</div><div class="product-variant">WHITE/RED, BLUE, BLACK / M,L</div><div class="product-price">¥5,900 <small>tax in</small></div></div>
        <div class="product-item"><div class="product-name">PHOTO CHARM</div><div class="product-variant">MEMBRIOTYPES</div><div class="product-price">¥1,500 <small>tax in</small></div></div>
      </div>

      <!-- PULSEON + fringe + trackpants -->
      <div class="product-grid" style="margin-top: 0.2rem;">
        <div class="product-item">
          <div class="product-name">PULSEON TOUR T-SHIRT</div>
          <div class="product-variant">WHITE/RED, BROWN, NAVY, BLACK</div>
          <div class="product-price">¥4,900 <small>tax in</small></div>
        </div>
        <div class="product-item">
          <div class="product-name">FRINGE-TRIMMED JACQUARD TOWEL</div>
          <div class="product-variant">RED, BLACK / M,L</div>
          <div class="product-price">¥2,500 <small>tax in</small></div>
        </div>
        <div class="product-item">
          <div class="product-name">TRACKPANTS</div>
          <div class="product-variant">RED, BLACK / M,L,XL</div>
          <div class="product-price">¥11,900 <small>tax in</small></div>
        </div>
      </div>

      <!-- date code -->
      <div class="footer-note">
        <i class="fas fa-calendar-alt" style="margin-right: 4px;"></i> 2025.10.25 – 2026.02.11
      </div>
    </div>

    <!-- CONTACT CARD : NALOP, IG, TELP, EMAIL, ALAMAT -->
    <div class="contact-card-wrapper">
      <div class="contact-card">
        <div style="display: flex; align-items: center; gap: 8px; flex-wrap: wrap;">
          <span class="brand-name">NALOP</span>
          <span class="ig-handle"><i class="fab fa-instagram" style="margin-right: 6px;"></i> @nalop</span>
        </div>
        <div style="display: flex; flex-wrap: wrap; gap: 0.8rem 1.5rem;">
          <div class="contact-item"><i class="fas fa-phone-alt"></i> 0891 2345 6789</div>
          <div class="contact-item"><i class="fas fa-envelope"></i> nalop@gmail.com</div>
          <div class="contact-item"><i class="fas fa-map-pin"></i> Jalan Sakaraw 109</div>
        </div>
      </div>
    </div>

    <div style="width:100%; text-align:right; font-size:0.6rem; color:#777; margin-top: 6px; padding-right: 8px;">
      <i class="fas fa-tag"></i> PULSE ON · TREASURE TOUR
    </div>
  </div>

  <script>
    (function() {
      con
