<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tài Xỉu - Long Tranh Hổ Đấu (Cửa Bão x33)</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Montserrat', 'Segoe UI', Tahoma, sans-serif;
      user-select: none;
    }

    body {
      min-height: 100vh;
      background-color: #030206;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 14px;
      color: #fff;
      overflow-x: hidden;
      position: relative;
    }

    /* --- NỀN ĐỘNG LONG TRANH HỔ ĐẤU --- */
    .bg-battle {
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 0;
      overflow: hidden;
    }

    .fire-aura {
      position: absolute;
      top: -10%;
      left: -15%;
      width: 65vw;
      height: 120vh;
      background: radial-gradient(circle at 30% 45%, rgba(255, 69, 0, 0.45) 0%, rgba(255, 140, 0, 0.25) 45%, transparent 75%);
      filter: blur(40px);
      animation: flamePulse 4s ease-in-out infinite alternate;
    }

    @keyframes flamePulse {
      0% { transform: scale(1) translate(0, 0); opacity: 0.7; }
      50% { transform: scale(1.1) translate(20px, -15px); opacity: 0.95; }
      100% { transform: scale(1.05) translate(-10px, 10px); opacity: 0.8; }
    }

    .water-aura {
      position: absolute;
      top: -10%;
      right: -15%;
      width: 65vw;
      height: 120vh;
      background: radial-gradient(circle at 70% 55%, rgba(0, 195, 255, 0.45) 0%, rgba(0, 102, 255, 0.25) 45%, transparent 75%);
      filter: blur(40px);
      animation: waterWave 5s ease-in-out infinite alternate;
    }

    @keyframes waterWave {
      0% { transform: scale(1) translate(0, 0); opacity: 0.75; }
      50% { transform: scale(1.08) translate(-25px, 15px); opacity: 1; }
      100% { transform: scale(1.02) translate(10px, -10px); opacity: 0.8; }
    }

    .clash-core {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 250px;
      height: 250px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(255, 255, 255, 0.8) 0%, rgba(255, 215, 0, 0.3) 35%, rgba(0, 229, 255, 0.2) 60%, transparent 80%);
      filter: blur(25px);
      animation: coreFlicker 1.8s ease-in-out infinite alternate;
    }

    @keyframes coreFlicker {
      0% { transform: translate(-50%, -50%) scale(0.85); opacity: 0.5; }
      50% { transform: translate(-50%, -50%) scale(1.25); opacity: 0.95; }
      100% { transform: translate(-50%, -50%) scale(1); opacity: 0.7; }
    }

    #embers-canvas, #fireworks-canvas {
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 1;
    }

    #fireworks-canvas { z-index: 999; }

    /* MENU ADMIN CAN THIỆP */
    .admin-toggle-btn {
      position: fixed;
      top: 14px;
      right: 14px;
      background: rgba(20, 15, 35, 0.85);
      border: 1px solid #ffe600;
      color: #ffe600;
      padding: 6px 12px;
      border-radius: 20px;
      font-size: 11px;
      font-weight: 800;
      cursor: pointer;
      z-index: 1000;
      box-shadow: 0 0 10px rgba(255, 230, 0, 0.3);
    }

    .admin-panel {
      position: fixed;
      top: 50px;
      right: 14px;
      background: rgba(10, 5, 25, 0.95);
      border: 1.5px solid #00f0ff;
      border-radius: 14px;
      padding: 12px 16px;
      z-index: 1000;
      display: none;
      flex-direction: column;
      gap: 8px;
      box-shadow: 0 0 20px rgba(0, 240, 255, 0.4);
      min-width: 220px;
    }

    .admin-panel.open { display: flex; }
    .admin-title { font-size: 12px; font-weight: 900; color: #00f0ff; text-transform: uppercase; }

    .admin-row {
      display: flex;
      gap: 6px;
      align-items: center;
      font-size: 12px;
    }

    .admin-select {
      background: #181230;
      color: #ffe600;
      border: 1px solid #48cae4;
      border-radius: 6px;
      padding: 4px;
      font-size: 11px;
      font-weight: bold;
    }

    /* TIÊU ĐỀ & TOP BAR */
    .brand-title {
      font-size: 24px;
      font-weight: 900;
      letter-spacing: 4px;
      text-transform: uppercase;
      margin-bottom: 6px;
      background: linear-gradient(90deg, #ff4500, #ffd700, #00f0ff, #ff4500);
      background-size: 250% auto;
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      animation: shineText 3.5s linear infinite;
      filter: drop-shadow(0 0 16px rgba(255, 140, 0, 0.7));
      z-index: 2;
    }

    @keyframes shineText { to { background-position: 250% center; } }

    .top-bar {
      display: flex;
      gap: 16px;
      align-items: center;
      margin-bottom: 10px;
      background: rgba(10, 8, 20, 0.82);
      backdrop-filter: blur(12px);
      padding: 6px 20px;
      border-radius: 40px;
      border: 1px solid rgba(255, 255, 255, 0.2);
      z-index: 2;
    }

    .chip-balance {
      font-size: 18px;
      color: #ffe600;
      font-weight: 900;
      text-shadow: 0 0 10px rgba(255, 230, 0, 0.8);
    }

    .btn-reset-coin {
      background: linear-gradient(90deg, #ff8c00, #ffd700);
      color: #000;
      border: none;
      border-radius: 20px;
      padding: 4px 10px;
      font-weight: 800;
      font-size: 11px;
      cursor: pointer;
    }

    /* BÀN CƯỢC */
    .table-layout {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 16px;
      width: 100%;
      max-width: 960px;
      position: relative;
      z-index: 2;
    }

    .bet-box {
      flex: 1;
      height: 270px;
      background: rgba(12, 10, 24, 0.78);
      backdrop-filter: blur(14px);
      border-radius: 24px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      position: relative;
      transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }

    #bet-xiu {
      border: 2px solid rgba(0, 210, 255, 0.5);
      box-shadow: inset 0 0 30px rgba(0, 150, 255, 0.2);
    }
    #bet-xiu .bet-title { color: #00f0ff; text-shadow: 0 0 25px rgba(0, 240, 255, 0.9); }

    #bet-tai {
      border: 2px solid rgba(255, 80, 0, 0.5);
      box-shadow: inset 0 0 30px rgba(255, 60, 0, 0.2);
    }
    #bet-tai .bet-title { color: #ff5500; text-shadow: 0 0 25px rgba(255, 85, 0, 0.9); }

    .bet-box:hover { transform: translateY(-4px) scale(1.02); }

    .bet-box.selected {
      border-color: #ffd700 !important;
      box-shadow: 0 0 35px rgba(255, 215, 0, 0.7) !important;
    }

    .bet-box.confirmed {
      border-color: #00ff88 !important;
      box-shadow: 0 0 35px rgba(0, 255, 136, 0.8) !important;
    }

    .bet-box.win {
      animation: neonRainbow 0.6s infinite alternate !important;
    }

    @keyframes neonRainbow {
      0% { box-shadow: 0 0 30px #ff3b00; border-color: #ff3b00; }
      50% { box-shadow: 0 0 40px #ffd700; border-color: #ffd700; }
      100% { box-shadow: 0 0 50px #00f0ff; border-color: #00f0ff; }
    }

    .bet-title {
      font-size: 48px;
      font-weight: 900;
      letter-spacing: 6px;
    }

    .bet-sub {
      font-size: 13px;
      color: #c9d1d9;
      font-weight: 600;
      letter-spacing: 1px;
      margin-top: 4px;
    }

    .bet-rate {
      font-size: 12px;
      color: #ffd700;
      font-weight: 800;
      margin-top: 2px;
    }

    .bet-amount {
      margin-top: 12px;
      font-size: 14px;
      color: #ffe600;
      font-weight: 800;
      background: rgba(0, 0, 0, 0.65);
      padding: 5px 14px;
      border-radius: 30px;
      border: 1px solid rgba(255, 230, 0, 0.4);
    }

    /* KHU VỰC GIỮA: MÂM XÓC VÀ CỬA BÃO X33 */
    .center-col {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 12px;
      z-index: 2;
    }

    .arena {
      position: relative;
      width: 270px;
      height: 270px;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-shrink: 0;
    }

    .plate {
      position: absolute;
      width: 260px;
      height: 260px;
      background: radial-gradient(circle, #241432 0%, #12091c 65%, #05020a 100%);
      border-radius: 50%;
      border: 7px solid #ffd700;
      box-shadow: 0 0 35px rgba(255, 215, 0, 0.5), 0 20px 40px rgba(0,0,0,0.9);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 1;
    }

    .bowl {
      position: absolute;
      width: 215px;
      height: 215px;
      background: radial-gradient(circle at 35% 35%, #ff4500 0%, #8b0000 55%, #1a0005 100%);
      border-radius: 50%;
      border: 5px solid #ffd700;
      box-shadow: 0 0 35px rgba(255, 69, 0, 0.7), 0 20px 40px rgba(0, 0, 0, 0.95);
      z-index: 10;
      cursor: pointer;
      transform: translateY(-230px) scale(0.85);
      opacity: 0;
      pointer-events: none;
      transition: transform 0.45s cubic-bezier(0.175, 0.885, 0.32, 1.3), opacity 0.3s ease;
    }

    .bowl.covered {
      transform: translateY(0) scale(1);
      opacity: 1;
      pointer-events: auto;
    }

    .bowl-knob {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 42px;
      height: 42px;
      border-radius: 50%;
      background: radial-gradient(circle, #fff3a8 0%, #ffd700 70%, #996515 100%);
      box-shadow: 0 0 15px rgba(255, 215, 0, 0.9);
      border: 2px solid #fff;
    }

    .dice-group {
      position: relative;
      width: 130px;
      height: 130px;
      z-index: 2;
    }

    .die {
      position: absolute;
      width: 42px;
      height: 42px;
      background: linear-gradient(145deg, #ffffff, #e6e6e6);
      border-radius: 10px;
      box-shadow: 0 5px 12px rgba(0, 0, 0, 0.6);
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-template-rows: repeat(3, 1fr);
      padding: 4px;
      transition: transform 0.2s ease;
    }

    #die1 { top: 10px; left: 44px; }
    #die2 { bottom: 16px; left: 14px; transform: rotate(-22deg); }
    #die3 { bottom: 16px; right: 14px; transform: rotate(38deg); }

    .dot {
      width: 8px;
      height: 8px;
      background: #111;
      border-radius: 50%;
      margin: auto;
      visibility: hidden;
    }

    .shaking { animation: superShake 0.08s infinite alternate; }

    @keyframes superShake {
      0% { transform: translate(-8px, -5px) rotate(-3deg); }
      100% { transform: translate(8px, 6px) rotate(3deg); }
    }

    /* CỬA CƯỢC BÃO (X33) NẰM TRUNG TÂM */
    .bao-bet-box {
      width: 260px;
      background: rgba(25, 10, 45, 0.85);
      border: 2px solid #a855f7;
      border-radius: 18px;
      padding: 10px 14px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      box-shadow: inset 0 0 20px rgba(168, 85, 247, 0.25), 0 6px 15px rgba(0,0,0,0.5);
      transition: all 0.25s ease;
    }

    .bao-bet-box:hover {
      transform: translateY(-2px) scale(1.03);
    }

    .bao-bet-box.selected {
      border-color: #ffd700 !important;
      box-shadow: 0 0 25px rgba(255, 215, 0, 0.8) !important;
    }

    .bao-bet-box.confirmed {
      border-color: #00ff88 !important;
      box-shadow: 0 0 25px rgba(0, 255, 136, 0.8) !important;
    }

    .bao-bet-box.win {
      animation: baoGlowWin 0.6s infinite alternate !important;
    }

    @keyframes baoGlowWin {
      from { box-shadow: 0 0 20px #ff007f; border-color: #ff007f; }
      to { box-shadow: 0 0 45px #ffe600; border-color: #ffe600; }
    }

    .bao-title {
      font-size: 24px;
      font-weight: 900;
      letter-spacing: 2px;
      color: #d8b4fe;
      text-shadow: 0 0 15px rgba(168, 85, 247, 0.8);
    }

    .bao-desc {
      font-size: 11px;
      color: #e9d5ff;
      font-weight: 600;
    }

    .bao-rate {
      font-size: 13px;
      font-weight: 900;
      color: #ffe600;
      text-shadow: 0 0 8px rgba(255, 230, 0, 0.7);
    }

    .bao-amount {
      font-size: 13px;
      color: #ffe600;
      font-weight: 800;
      margin-top: 4px;
    }

    /* BANNER HIỂN THỊ KẾT QUẢ */
    .result-banner {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) scale(0);
      z-index: 25;
      pointer-events: none;
      text-align: center;
      opacity: 0;
      transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.35);
    }

    .result-banner.active {
      transform: translate(-50%, -50%) scale(1);
      opacity: 1;
    }

    .result-badge {
      font-size: 50px;
      font-weight: 900;
      letter-spacing: 4px;
      padding: 8px 40px;
      border-radius: 50px;
      color: #fff;
      text-transform: uppercase;
      display: inline-block;
      box-shadow: 0 15px 50px rgba(0, 0, 0, 0.9);
      animation: pulseGlow 0.8s infinite alternate;
    }

    @keyframes pulseGlow {
      from { transform: scale(1); }
      to { transform: scale(1.08); }
    }

    .result-badge.tai {
      background: linear-gradient(135deg, #ff3b00, #b7094c);
      border: 4px solid #fff;
      box-shadow: 0 0 50px #ff3b00;
    }

    .result-badge.xiu {
      background: linear-gradient(135deg, #00c3ff, #00509d);
      border: 4px solid #fff;
      box-shadow: 0 0 50px #00c3ff;
    }

    .result-badge.bao {
      background: linear-gradient(135deg, #7b2cbf, #ff007f);
      border: 4px solid #ffe600;
      box-shadow: 0 0 60px #ff007f, 0 0 30px #7b2cbf;
      color: #ffe600;
    }

    .win-alert-text {
      font-size: 17px;
      font-weight: 900;
      margin-top: 10px;
      text-shadow: 0 2px 10px rgba(0,0,0,0.9);
      background: rgba(8, 4, 16, 0.9);
      padding: 6px 18px;
      border-radius: 30px;
      border: 1px solid rgba(255,255,255,0.2);
    }

    /* BẢNG ĐIỀU KHIỂN CƯỢC */
    .bet-control-panel {
      margin-top: 14px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
      background: rgba(12, 10, 24, 0.85);
      backdrop-filter: blur(14px);
      padding: 12px 24px;
      border-radius: 20px;
      border: 1px solid rgba(255, 255, 255, 0.15);
      z-index: 2;
    }

    .chip-selector {
      display: flex;
      gap: 10px;
      align-items: center;
    }

    .chip-btn {
      background: #1e153b;
      color: #ffe600;
      border: 1px solid #ffe600;
      border-radius: 20px;
      padding: 6px 14px;
      font-size: 13px;
      font-weight: 800;
      cursor: pointer;
      transition: all 0.2s;
    }

    .chip-btn:hover { background: #ffe600; color: #000; transform: translateY(-2px); }

    .input-box {
      width: 100px;
      padding: 6px 10px;
      border-radius: 8px;
      border: 2px solid #ffe600;
      background: #0b071a;
      color: #ffe600;
      font-weight: 800;
      text-align: center;
      font-size: 14px;
      outline: none;
    }

    .btn-group { display: flex; gap: 12px; }

    .action-btn {
      padding: 10px 22px;
      font-size: 13px;
      font-weight: 900;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      text-transform: uppercase;
      letter-spacing: 1px;
      transition: all 0.2s ease;
    }

    .btn-confirm { background: linear-gradient(135deg, #ffe600, #ff9900); color: #000; }
    .btn-shake { background: linear-gradient(135deg, #ff4500, #c00); color: #fff; }
    .btn-open { background: linear-gradient(135deg, #00f0ff, #0077b6); color: #000; }

    .action-btn:hover:not(:disabled) { transform: translateY(-2px); }
    .action-btn:disabled {
      background: #231c36 !important;
      color: #635b7e !important;
      cursor: not-allowed;
      transform: none !important;
    }

    .guide-text { font-size: 13px; color: #a5f3fc; font-weight: 600; }

    /* BẢNG SOI CẦU */
    .history-board {
      margin-top: 12px;
      background: rgba(8, 6, 18, 0.88);
      backdrop-filter: blur(14px);
      border: 1px solid rgba(255, 255, 255, 0.15);
      border-radius: 18px;
      padding: 10px 20px;
      width: 100%;
      max-width: 960px;
      display: flex;
      flex-direction: column;
      gap: 8px;
      z-index: 2;
    }

    .history-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 13px;
      font-weight: 700;
    }

    .history-legend { display: flex; gap: 14px; font-size: 12px; }
    .legend-item { display: flex; align-items: center; gap: 6px; }

    .history-dots {
      display: flex;
      gap: 10px;
      align-items: center;
      overflow-x: auto;
      padding: 6px 2px;
      min-height: 42px;
    }

    .history-dots::-webkit-scrollbar { height: 4px; }
    .history-dots::-webkit-scrollbar-thumb {
      background: rgba(255, 255, 255, 0.2);
      border-radius: 4px;
    }

    .dot-result {
      width: 26px;
      height: 26px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 11px;
      font-weight: 900;
      color: #fff;
      flex-shrink: 0;
      box-shadow: 0 0 10px currentColor;
    }

    .dot-result.tai-dot {
      background: radial-gradient(circle at 35% 35%, #ff5500, #b7094c);
      color: #ff3b00;
      border: 1.5px solid #ff884d;
    }

    .dot-result.xiu-dot {
      background: radial-gradient(circle at 35% 35%, #00f0ff, #00509d);
      color: #00f0ff;
      border: 1.5px solid #90e0ef;
    }

    .dot-result.bao-dot {
      background: radial-gradient(circle at 35% 35%, #ff007f, #7b2cbf);
      color: #ffd700;
      border: 1.5px solid #ffe600;
    }
  </style>
</head>
<body>

  <!-- ADMIN CHỈNH KẾT QUẢ -->
  <button class="admin-toggle-btn" onclick="toggleAdminPanel()">⚙ Bảng Chỉnh Kết Quả</button>
  <div class="admin-panel" id="admin-panel">
    <div class="admin-title">⚡ Can thiệp xúc xắc</div>
    
    <div class="admin-row">
      <span>Chế độ:</span>
      <select class="admin-select" id="cheat-mode" onchange="onCheatModeChange()">
        <option value="random">Ngẫu nhiên tự nhiên</option>
        <option value="force-tai">Ép ra TÀI (11-18)</option>
        <option value="force-xiu">Ép ra XỈU (3-10)</option>
        <option value="force-bao">Ép ra BÃO (Bộ 3 x33)</option>
        <option value="custom">Chỉ định cụ thể</option>
      </select>
    </div>

    <div class="admin-row" id="custom-dice-row" style="display: none;">
      <span>Mặt:</span>
      <select class="admin-select" id="c-d1">
        <option value="1">1</option><option value="2">2</option><option value="3">3</option>
        <option value="4">4</option><option value="5">5</option><option value="6">6</option>
      </select>
      <select class="admin-select" id="c-d2">
        <option value="1">1</option><option value="2">2</option><option value="3">3</option>
        <option value="4">4</option><option value="5">5</option><option value="6">6</option>
      </select>
      <select class="admin-select" id="c-d3">
        <option value="1">1</option><option value="2">2</option><option value="3">3</option>
        <option value="4">4</option><option value="5">5</option><option value="6">6</option>
      </select>
    </div>
  </div>

  <div class="bg-battle">
    <div class="fire-aura"></div>
    <div class="water-aura"></div>
    <div class="clash-core"></div>
  </div>

  <canvas id="embers-canvas"></canvas>
  <canvas id="fireworks-canvas"></canvas>

  <div class="brand-title">★ LONG HỔ TRANH HÙNG ★</div>

  <div class="top-bar">
    <div>Số dư: <span class="chip-balance" id="balance">1000</span> xu</div>
    <button class="btn-reset-coin" onclick="resetCoins()">+1000 XU</button>
    <div>Cửa đã chốt: <strong id="locked-choice" style="color: #00ff88;">Chưa có</strong></div>
  </div>

  <div class="table-layout">
    <!-- CỬA XỈU (3 - 10) -->
    <div class="bet-box" id="bet-xiu" onclick="selectGate('XIU')">
      <div class="bet-title">XỈU</div>
      <div class="bet-sub">BĂNG HỔ &bull; 3 - 10</div>
      <div class="bet-rate">TỈ LỆ: 1 ĂN 2</div>
      <div class="bet-amount" id="amt-xiu">0 xu</div>
    </div>

    <!-- KHU VỰC TRUNG TÂM: MÂM XÓC + CỬA BÃO -->
    <div class="center-col">
      <div class="arena" id="arena">
        <div class="plate">
          <div class="dice-group">
            <div class="die" id="die1"></div>
            <div class="die" id="die2"></div>
            <div class="die" id="die3"></div>
          </div>
        </div>

        <div class="bowl" id="bowl" onclick="openBowl()">
          <div class="bowl-knob"></div>
        </div>

        <div class="result-banner" id="banner">
          <div class="result-badge" id="banner-tag">TÀI</div>
          <div class="win-alert-text" id="banner-detail">12 ĐIỂM</div>
        </div>
      </div>

      <!-- CỬA CƯỢC BÃO (X33) -->
      <div class="bao-bet-box" id="bet-bao" onclick="selectGate('BAO')">
        <div class="bao-title">⚡ CỬA BÃO ⚡</div>
        <div class="bao-desc">3 MẶT XÚC XẮC ĐỒNG NHẤT</div>
        <div class="bao-rate">TỈ LỆ: 1 ĂN 33 (x33)</div>
        <div class="bao-amount" id="amt-bao">0 xu</div>
      </div>
    </div>

    <!-- CỬA TÀI (11 - 18) -->
    <div class="bet-box" id="bet-tai" onclick="selectGate('TAI')">
      <div class="bet-title">TÀI</div>
      <div class="bet-sub">HỎA LONG &bull; 11 - 18</div>
      <div class="bet-rate">TỈ LỆ: 1 ĂN 2</div>
      <div class="bet-amount" id="amt-tai">0 xu</div>
    </div>
  </div>

  <div class="bet-control-panel">
    <div class="chip-selector">
      <span style="font-weight: 700; color: #ffe600;">Mức cược:</span>
      <input type="number" class="input-box" id="bet-input" value="100" min="10" step="10">
      <button class="chip-btn" onclick="setQuickBet(50)">50</button>
      <button class="chip-btn" onclick="setQuickBet(100)">100</button>
      <button class="chip-btn" onclick="setQuickBet(200)">200</button>
      <button class="chip-btn" onclick="setQuickBet('all')">TẤT TAY</button>
    </div>

    <div class="btn-group">
      <button class="action-btn btn-confirm" id="btn-confirm" onclick="confirmBet()">Xác Nhận Cược</button>
      <button class="action-btn btn-shake" id="btn-shake" onclick="shakeBowl()" disabled>Đậy Bát & Xóc</button>
      <button class="action-btn btn-open" id="btn-open" onclick="openBowl()" disabled>Mở Bát</button>
    </div>

    <div class="guide-text" id="guide">Chọn cửa TÀI, XỈU hoặc BÃO (x33) rồi bấm "Xác Nhận Cược"!</div>
  </div>

  <div class="history-board">
    <div class="history-header">
      <span style="color: #ffd700; text-transform: uppercase;">📊 Lịch Sử Các Phiên</span>
      <div class="history-legend">
        <div class="legend-item">
          <div class="dot-result tai-dot" style="width: 14px; height: 14px; font-size: 0;"></div>
          <span>Tài (11-18)</span>
        </div>
        <div class="legend-item">
          <div class="dot-result xiu-dot" style="width: 14px; height: 14px; font-size: 0;"></div>
          <span>Xỉu (3-10)</span>
        </div>
        <div class="legend-item">
          <div class="dot-result bao-dot" style="width: 14px; height: 14px; font-size: 0;"></div>
          <span>Bão (Bộ 3 x33)</span>
        </div>
      </div>
    </div>

    <div class="history-dots" id="history-dots"></div>
  </div>

  <script>
    const dotPatterns = {
      1: [4],
      2: [2, 6],
      3: [2, 4, 6],
      4: [0, 2, 6, 8],
      5: [0, 2, 4, 6, 8],
      6: [0, 2, 3, 5, 6, 8]
    };

    function initDie(dieEl) {
      dieEl.innerHTML = '';
      for (let i = 0; i < 9; i++) {
        const dot = document.createElement('div');
        dot.className = 'dot';
        dieEl.appendChild(dot);
      }
    }

    function renderDie(dieEl, val) {
      const dots = dieEl.getElementsByClassName('dot');
      for (let i = 0; i < 9; i++) dots[i].style.visibility = 'hidden';
      dotPatterns[val].forEach(idx => {
        dots[idx].style.visibility = 'visible';
        dots[idx].style.background = (val === 1 || val === 4) ? '#ff2200' : '#111827';
      });
    }

    const d1 = document.getElementById('die1');
    const d2 = document.getElementById('die2');
    const d3 = document.getElementById('die3');
    const bowl = document.getElementById('bowl');
    const arena = document.getElementById('arena');
    const banner = document.getElementById('banner');
    const bannerTag = document.getElementById('banner-tag');
    const bannerDetail = document.getElementById('banner-detail');
    const guide = document.getElementById('guide');
    const balanceEl = document.getElementById('balance');
    const lockedChoiceEl = document.getElementById('locked-choice');
    const betInput = document.getElementById('bet-input');
    const historyDotsContainer = document.getElementById('history-dots');

    const boxXiu = document.getElementById('bet-xiu');
    const boxTai = document.getElementById('bet-tai');
    const boxBao = document.getElementById('bet-bao');
    const amtXiu = document.getElementById('amt-xiu');
    const amtTai = document.getElementById('amt-tai');
    const amtBao = document.getElementById('amt-bao');

    const btnConfirm = document.getElementById('btn-confirm');
    const btnShake = document.getElementById('btn-shake');
    const btnOpen = document.getElementById('btn-open');

    // Admin Controls
    const adminPanel = document.getElementById('admin-panel');
    const cheatModeSelect = document.getElementById('cheat-mode');
    const customDiceRow = document.getElementById('custom-dice-row');
    const customD1 = document.getElementById('c-d1');
    const customD2 = document.getElementById('c-d2');
    const customD3 = document.getElementById('c-d3');

    let balance = 1000;
    let selectedGate = null;
    let activeBetGate = null;
    let activeBetAmount = 0;
    let diceValues = [1, 2, 3];
    let isLocked = false;
    let sessionCount = 0;

    [d1, d2, d3].forEach(d => initDie(d));
    renderDie(d1, 1);
    renderDie(d2, 2);
    renderDie(d3, 3);

    function toggleAdminPanel() { adminPanel.classList.toggle('open'); }
    function onCheatModeChange() {
      customDiceRow.style.display = (cheatModeSelect.value === 'custom') ? 'flex' : 'none';
    }

    function resetCoins() {
      balance += 1000;
      balanceEl.innerText = balance;
    }

    function setQuickBet(amt) {
      if (isLocked) return;
      if (amt === 'all') betInput.value = balance;
      else betInput.value = amt;
    }

    function selectGate(gate) {
      if (isLocked) return;
      selectedGate = gate;
      boxXiu.classList.toggle('selected', gate === 'XIU');
      boxTai.classList.toggle('selected', gate === 'TAI');
      boxBao.classList.toggle('selected', gate === 'BAO');
      guide.innerText = `Đã chọn: ${gate === 'BAO' ? 'BÃO (x33)' : gate}. Bấm "Xác Nhận Cược" để chốt!`;
    }

    function confirmBet() {
      if (!selectedGate) {
        alert("Vui lòng click chọn cửa TÀI, XỈU hoặc BÃO trước!");
        return;
      }
      const amt = parseInt(betInput.value, 10);
      if (isNaN(amt) || amt <= 0) {
        alert("Số tiền cược không hợp lệ!");
        return;
      }
      if (amt > balance) {
        alert("Số dư xu không đủ!");
        return;
      }

      balance -= amt;
      activeBetGate = selectedGate;
      activeBetAmount = amt;
      isLocked = true;

      balanceEl.innerText = balance;
      lockedChoiceEl.innerText = `${activeBetGate === 'BAO' ? 'BÃO (x33)' : activeBetGate} (${activeBetAmount} xu)`;

      if (activeBetGate === 'XIU') amtXiu.innerText = `${activeBetAmount} xu`;
      else if (activeBetGate === 'TAI') amtTai.innerText = `${activeBetAmount} xu`;
      else amtBao.innerText = `${activeBetAmount} xu`;

      boxXiu.classList.toggle('confirmed', activeBetGate === 'XIU');
      boxTai.classList.toggle('confirmed', activeBetGate === 'TAI');
      boxBao.classList.toggle('confirmed', activeBetGate === 'BAO');

      btnConfirm.disabled = true;
      btnShake.disabled = false;
      guide.innerText = "Cược thành công! Bấm 'Đậy Bát & Xóc'.";
    }

    // TÍNH TOÁN KẾT QUẢ THEO THIẾT LẬP ADMIN
    function determineNextDice() {
      const mode = cheatModeSelect.value;
      if (mode === 'custom') {
        return [
          parseInt(customD1.value, 10),
          parseInt(customD2.value, 10),
          parseInt(customD3.value, 10)
        ];
      }

      if (mode === 'force-bao') {
        const val = Math.floor(Math.random() * 6) + 1;
        return [val, val, val];
      }

      if (mode === 'force-tai') {
        while (true) {
          const a = Math.floor(Math.random() * 6) + 1;
          const b = Math.floor(Math.random() * 6) + 1;
          const c = Math.floor(Math.random() * 6) + 1;
          const sum = a + b + c;
          if (sum >= 11 && sum <= 18 && !(a === b && b === c)) {
            return [a, b, c];
          }
        }
      }

      if (mode === 'force-xiu') {
        while (true) {
          const a = Math.floor(Math.random() * 6) + 1;
          const b = Math.floor(Math.random() * 6) + 1;
          const c = Math.floor(Math.random() * 6) + 1;
          const sum = a + b + c;
          if (sum >= 3 && sum <= 10 && !(a === b && b === c)) {
            return [a, b, c];
          }
        }
      }

      return [
        Math.floor(Math.random() * 6) + 1,
        Math.floor(Math.random() * 6) + 1,
        Math.floor(Math.random() * 6) + 1
      ];
    }

    function shakeBowl() {
      btnShake.disabled = true;
      banner.classList.remove('active');
      boxXiu.classList.remove('win');
      boxTai.classList.remove('win');
      boxBao.classList.remove('win');

      bowl.classList.add('covered');

      setTimeout(() => {
        arena.classList.add('shaking');
        guide.innerText = "Đang xóc bí mật...";

        const bounceInterval = setInterval(() => {
          [d1, d2, d3].forEach(die => {
            const rx = Math.floor(Math.random() * 34 - 17);
            const ry = Math.floor(Math.random() * 34 - 17);
            const rdeg = Math.floor(Math.random() * 360);
            die.style.transform = `translate(${rx}px, ${ry}px) rotate(${rdeg}deg)`;
          });
        }, 70);

        setTimeout(() => {
          clearInterval(bounceInterval);
          arena.classList.remove('shaking');

          diceValues = determineNextDice();

          renderDie(d1, diceValues[0]);
          renderDie(d2, diceValues[1]);
          renderDie(d3, diceValues[2]);

          guide.innerText = "Đã xóc xong! Bấm 'Mở Bát'.";
          btnOpen.disabled = false;
        }, 1200);
      }, 350);
    }

    function addHistoryRecord(resultType, sumScore) {
      sessionCount++;
      const dot = document.createElement('div');
      
      let dotClass = 'xiu-dot';
      let symbol = 'X';
      if (resultType === 'BAO') {
        dotClass = 'bao-dot';
        symbol = 'B';
      } else if (resultType === 'TAI') {
        dotClass = 'tai-dot';
        symbol = 'T';
      }

      dot.className = `dot-result ${dotClass}`;
      dot.innerText = symbol;
      dot.title = `Phiên #${sessionCount}: ${resultType} (${sumScore} điểm)`;

      historyDotsContainer.appendChild(dot);
      historyDotsContainer.scrollLeft = historyDotsContainer.scrollWidth;
    }

    function openBowl() {
      if (btnOpen.disabled) return;

      bowl.classList.remove('covered');
      btnOpen.disabled = true;

      const [v1, v2, v3] = diceValues;
      const sum = v1 + v2 + v3;
      const isBao = (v1 === v2 && v2 === v3);

      let resultText = "";
      if (isBao) {
        resultText = "BAO";
        bannerTag.innerText = "BÃO!";
        bannerTag.className = "result-badge bao";
      } else if (sum >= 11 && sum <= 18) {
        resultText = "TAI";
        bannerTag.innerText = "TÀI";
        bannerTag.className = "result-badge tai";
      } else {
        resultText = "XIU";
        bannerTag.innerText = "XỈU";
        bannerTag.className = "result-badge xiu";
      }

      addHistoryRecord(resultText, sum);

      // XỬ LÝ TRẢ THƯỞNG
      if (isBao) {
        if (activeBetGate === 'BAO') {
          // THẮNG CƯỢC BÃO: 1 ăn 33 (nhận thưởng gấp 33 lần)
          const winReward = activeBetAmount * 33;
          balance += winReward;
          bannerDetail.innerText = `💥 TRÚNG BÃO (x33)! +${winReward} XU (${v1}-${v2}-${v3})`;
          bannerDetail.style.color = "#ffe600";
          boxBao.classList.add('win');
          launchMegaFireworks();
        } else {
          // Ra bão mà cược Tài hoặc Xỉu thì bị xử thua
          bannerDetail.innerText = `⚡ XUẤT HIỆN BÃO (${v1}-${v2}-${v3})! TÀI & XỈU ĐỀU THUA!`;
          bannerDetail.style.color = "#ff4d6d";
        }
      } else if (activeBetGate === resultText) {
        // THẮNG CƯỢC TÀI HOẶC XỈU (1 ăn 2)
        const winReward = activeBetAmount * 2;
        balance += winReward;
        bannerDetail.innerText = `🎉 THẮNG LỚN +${winReward} XU! (${v1}+${v2}+${v3}=${sum})`;
        bannerDetail.style.color = "#ffe600";
        (resultText === 'TAI' ? boxTai : boxXiu).classList.add('win');
        launchFireworksSeries();
      } else {
        // THUA CƯỢC
        bannerDetail.innerText = `😢 THUA RỒI! (${v1}+${v2}+${v3}=${sum})`;
        bannerDetail.style.color = "#ff4d6d";
      }

      balanceEl.innerText = balance;
      banner.classList.add('active');

      // Tự động dọn bàn cược sau 2.5s
      setTimeout(() => {
        amtXiu.innerText = "0 xu";
        amtTai.innerText = "0 xu";
        amtBao.innerText = "0 xu";
        lockedChoiceEl.innerText = "Chưa có";

        boxXiu.classList.remove('confirmed', 'selected', 'win');
        boxTai.classList.remove('confirmed', 'selected', 'win');
        boxBao.classList.remove('confirmed', 'selected', 'win');

        selectedGate = null;
        activeBetGate = null;
        activeBetAmount = 0;
        isLocked = false;

        btnConfirm.disabled = false;
        guide.innerText = "Ván mới: Hãy chọn lại cửa và bấm 'Xác Nhận Cược'.";
      }, 2500);
    }

    // --- HIỆU ỨNG TÀN LỬA BAY NỀN ---
    const embersCanvas = document.getElementById('embers-canvas');
    const embersCtx = embersCanvas.getContext('2d');
    let embers = [];

    function resizeCanvas() {
      embersCanvas.width = window.innerWidth;
      embersCanvas.height = window.innerHeight;
      fireworksCanvas.width = window.innerWidth;
      fireworksCanvas.height = window.innerHeight;
    }

    const fireworksCanvas = document.getElementById('fireworks-canvas');
    const fireworksCtx = fireworksCanvas.getContext('2d');
    let particles = [];
    let isAnimating = false;

    window.addEventListener('resize', resizeCanvas);

    function initEmbers() {
      embers = [];
      for (let i = 0; i < 65; i++) {
        embers.push({
          x: Math.random() * window.innerWidth,
          y: Math.random() * window.innerHeight,
          vx: (Math.random() - 0.5) * 1.5,
          vy: -(Math.random() * 1.6 + 0.6),
          size: Math.random() * 3 + 1,
          color: Math.random() > 0.4 ? '#ff5500' : '#00c3ff',
          alpha: Math.random() * 0.7 + 0.3
        });
      }
    }

    function renderEmbers() {
      embersCtx.clearRect(0, 0, embersCanvas.width, embersCanvas.height);
      embers.forEach(e => {
        e.x += e.vx;
        e.y += e.vy;
        if (e.y < 0) {
          e.y = embersCanvas.height;
          e.x = Math.random() * embersCanvas.width;
        }
        embersCtx.beginPath();
        embersCtx.arc(e.x, e.y, e.size, 0, Math.PI * 2);
        embersCtx.fillStyle = e.color;
        embersCtx.globalAlpha = e.alpha;
        embersCtx.shadowColor = e.color;
        embersCtx.shadowBlur = 8;
        embersCtx.fill();
      });
      requestAnimationFrame(renderEmbers);
    }

    // Pháo hoa thường (thắng Tài/Xỉu)
    function launchFireworksSeries() {
      triggerConfetti(fireworksCanvas.width / 2, fireworksCanvas.height / 2);
      setTimeout(() => triggerConfetti(fireworksCanvas.width * 0.25, fireworksCanvas.height * 0.4), 250);
      setTimeout(() => triggerConfetti(fireworksCanvas.width * 0.75, fireworksCanvas.height * 0.4), 500);
    }

    // Đại tiệc pháo hoa cực đại khi trúng BÃO x33
    function launchMegaFireworks() {
      for (let i = 0; i < 5; i++) {
        setTimeout(() => {
          triggerConfetti(
            Math.random() * fireworksCanvas.width,
            Math.random() * fireworksCanvas.height * 0.6 + 100
          );
        }, i * 200);
      }
    }

    function triggerConfetti(originX, originY) {
      const colors = ['#ff3b00', '#00f0ff', '#ffd700', '#ff007f', '#a855f7', '#ffffff'];
      for (let i = 0; i < 140; i++) {
        const angle = Math.random() * Math.PI * 2;
        const speed = Math.random() * 18 + 5;
        particles.push({
          x: originX,
          y: originY,
          vx: Math.cos(angle) * speed,
          vy: Math.sin(angle) * speed - 2,
          size: Math.random() * 8 + 4,
          color: colors[Math.floor(Math.random() * colors.length)],
          rotation: Math.random() * 360,
          rotationSpeed: (Math.random() - 0.5) * 14,
          life: 1
        });
      }
      if (!isAnimating) {
        isAnimating = true;
        requestAnimationFrame(renderParticles);
      }
    }

    function renderParticles() {
      fireworksCtx.clearRect(0, 0, fireworksCanvas.width, fireworksCanvas.height);
      for (let i = particles.length - 1; i >= 0; i--) {
        const p = particles[i];
        p.x += p.vx;
        p.y += p.vy;
        p.vy += 0.38;
        p.rotation += p.rotationSpeed;
        p.life -= 0.012;

        fireworksCtx.save();
        fireworksCtx.translate(p.x, p.y);
        fireworksCtx.rotate((p.rotation * Math.PI) / 180);
        fireworksCtx.globalAlpha = Math.max(p.life, 0);
        fireworksCtx.fillStyle = p.color;
        fireworksCtx.shadowColor = p.color;
        fireworksCtx.shadowBlur = 10;
        fireworksCtx.fillRect(-p.size / 2, -p.size / 2, p.size, p.size);
        fireworksCtx.restore();

        if (p.life <= 0) particles.splice(i, 1);
      }

      if (particles.length > 0) requestAnimationFrame(renderParticles);
      else isAnimating = false;
    }

    resizeCanvas();
    initEmbers();
    renderEmbers();
  </script>

</body>
</html>
