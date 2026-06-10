<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>宥宥成长日记 · YouYou's Diary</title>
<style>
  /* ============================================================
     MORANDI PALETTE  +  APPLE AESTHETIC
  ============================================================ */
  :root {
    --m-rose:        #d4b5b0;
    --m-sage:        #b5c4b0;
    --m-blue:        #b0c0cc;
    --m-lavender:    #c4b8cc;
    --m-beige:       #e0d5c4;
    --m-cream:       #f4ede1;
    --m-clay:        #c9a896;
    --m-mist:        #e8e4dc;
    --m-ink:         #4a4845;
    --m-text:        #2d2c2a;
    --m-text-soft:   #7a7772;
    --m-glass:       rgba(255, 255, 255, 0.55);
    --m-glass-2:     rgba(255, 255, 255, 0.35);
    --m-glass-bd:    rgba(255, 255, 255, 0.7);
    --shadow-soft:   0 10px 40px rgba(74, 72, 69, 0.08);
    --shadow-hard:   0 20px 60px rgba(74, 72, 69, 0.18);
  }

  * { margin: 0; padding: 0; box-sizing: border-box;
      -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; }

  /* 衬线字体 — 让 hero / 标题更有书卷气 */
  @import url('https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@300;400;500;700&family=Cormorant+Garamond:ital,wght@0,300;0,500;1,300&display=swap');

  :root {
    --serif: "Noto Serif SC", "Songti SC", "STSong", serif;
    --serif-en: "Cormorant Garamond", "Times New Roman", serif;
    --warm: #c9a896;  /* 暖色强调,黄昏金 */
  }

  html, body {
    font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text",
                 "PingFang SC", "Helvetica Neue", "Segoe UI", system-ui, sans-serif;
    color: var(--m-text);
    background: linear-gradient(135deg, #f6efe3 0%, #ece6d9 30%, #ddd6c6 65%, #cdc6b7 100%);
    background-attachment: fixed;
    min-height: 100vh;
    overflow-x: hidden;
    letter-spacing: -0.005em;
  }

  /* 莫兰迪云层 */
  body::before {
    content: ""; position: fixed; inset: 0; pointer-events: none; z-index: 0;
    background:
      radial-gradient(circle at 12% 18%, rgba(212, 181, 176, 0.45), transparent 45%),
      radial-gradient(circle at 88% 78%, rgba(176, 192, 204, 0.40), transparent 45%),
      radial-gradient(circle at 50% 50%, rgba(196, 184, 204, 0.18), transparent 60%);
  }
  /* 噪点纹理 + 暖色暗角 (黄昏时刻) */
  body::after {
    content: ""; position: fixed; inset: 0; pointer-events: none; z-index: 0;
    background-image:
      radial-gradient(ellipse at center, transparent 50%, rgba(74, 50, 30, 0.18) 100%),
      url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='200' height='200'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 0.6  0 0 0 0 0.6  0 0 0 0 0.55  0 0 0 0.04 0'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
    background-blend-mode: normal, overlay;
  }

  /* ===== Bokeh 漂浮粒子层 (黄昏金光) ===== */
  .bokeh {
    position: fixed; inset: 0; pointer-events: none; z-index: 0; overflow: hidden;
  }
  .bokeh span {
    position: absolute; bottom: -120px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(255, 230, 200, 0.7), rgba(201, 168, 150, 0.15) 60%, transparent 75%);
    filter: blur(20px);
    animation: float-up linear infinite;
  }
  @keyframes float-up {
    0%   { transform: translate(0, 0) scale(0.6); opacity: 0; }
    10%  { opacity: 0.9; }
    90%  { opacity: 0.7; }
    100% { transform: translate(var(--dx), -110vh) scale(1.2); opacity: 0; }
  }

  /* ============================================================
     ENTRY GATE
  ============================================================ */
  .gate {
    position: fixed; inset: 0; z-index: 9999;
    background: linear-gradient(135deg, #f4ede1 0%, #e0d5c4 100%);
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; transition: opacity 0.8s ease;
  }
  .gate.hidden { opacity: 0; pointer-events: none; }
  .gate-inner { text-align: center; max-width: 540px; padding: 0 40px; }
  .gate-mark {
    width: 84px; height: 84px; border-radius: 50%;
    background: linear-gradient(135deg, var(--m-rose), var(--m-clay), var(--m-lavender));
    margin: 0 auto 28px; display: flex; align-items: center; justify-content: center;
    color: #fff; font-size: 36px; font-weight: 300;
    box-shadow: 0 12px 40px rgba(201, 168, 150, 0.4);
    animation: float 4s ease-in-out infinite;
  }
  @keyframes float { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
  .gate h2 { font-size: 38px; font-weight: 700; letter-spacing: -0.025em; margin-bottom: 12px; }
  .gate p { color: var(--m-text-soft); font-size: 15px; line-height: 1.7; }
  .gate .enter-hint { margin-top: 28px; font-size: 11px; letter-spacing: 0.25em; text-transform: uppercase; color: var(--m-text-soft); opacity: 0.7; }

  /* ============================================================
     SETUP PANEL (first-run)
  ============================================================ */
  .setup {
    position: relative; z-index: 1;
    max-width: 720px; margin: 100px auto 60px; padding: 0 40px;
  }
  .setup-card {
    background: rgba(255,255,255,0.6);
    backdrop-filter: saturate(180%) blur(30px);
    -webkit-backdrop-filter: saturate(180%) blur(30px);
    border: 1px solid var(--m-glass-bd);
    border-radius: 28px;
    padding: 48px 52px;
    box-shadow: var(--shadow-hard);
  }
  .setup-card h2 {
    font-size: 32px; font-weight: 700; letter-spacing: -0.02em;
    margin-bottom: 8px;
  }
  .setup-card .sub {
    color: var(--m-text-soft); font-size: 14px; line-height: 1.6;
    margin-bottom: 32px;
  }
  .setup-row {
    display: flex; align-items: center; gap: 18px;
    padding: 18px 0;
    border-top: 1px solid rgba(122,119,114,0.12);
  }
  .setup-row:first-of-type { border-top: none; }
  .setup-icon {
    width: 44px; height: 44px; border-radius: 12px;
    background: linear-gradient(135deg, var(--m-rose), var(--m-clay));
    display: flex; align-items: center; justify-content: center;
    color: #fff; font-size: 20px; flex-shrink: 0;
  }
  .setup-icon.music { background: linear-gradient(135deg, var(--m-lavender), var(--m-blue)); }
  .setup-text { flex: 1; min-width: 0; }
  .setup-text strong { display: block; font-size: 15px; font-weight: 600; margin-bottom: 2px; }
  .setup-text span { color: var(--m-text-soft); font-size: 12px; }
  .setup-text .ok { color: #7ba577; font-weight: 500; }
  .setup-btn {
    padding: 9px 18px; border-radius: 20px; border: 1px solid rgba(122,119,114,0.2);
    background: var(--m-text); color: #f4ede1; cursor: pointer; font-size: 12px;
    font-weight: 500; transition: all 0.25s ease;
    font-family: inherit;
  }
  .setup-btn:hover { background: var(--m-ink); transform: translateY(-1px); }
  .setup-btn:disabled { background: rgba(45,44,42,0.3); cursor: not-allowed; transform: none; }
  .setup-foot {
    margin-top: 28px; padding-top: 24px;
    border-top: 1px solid rgba(122,119,114,0.12);
    font-size: 12px; color: var(--m-text-soft); line-height: 1.7;
  }
  .setup-foot code {
    background: rgba(122,119,114,0.08); padding: 2px 7px; border-radius: 4px;
    font-size: 11px;
  }

  /* ============================================================
     NAV
  ============================================================ */
  .nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    padding: 18px 40px; display: flex; justify-content: space-between; align-items: center;
    background: rgba(244, 237, 225, 0.45);
    backdrop-filter: saturate(180%) blur(24px);
    -webkit-backdrop-filter: saturate(180%) blur(24px);
    border-bottom: 1px solid rgba(255,255,255,0.4);
  }
  .brand { display: flex; align-items: center; gap: 12px; font-weight: 600; font-size: 15px; letter-spacing: -0.01em; }
  .brand .dot {
    width: 10px; height: 10px; border-radius: 50%;
    background: linear-gradient(135deg, var(--m-rose), var(--m-clay));
    box-shadow: 0 0 0 3px rgba(212, 181, 176, 0.18);
  }
  .nav-meta { display: flex; gap: 10px; align-items: center; font-size: 12px; color: var(--m-text-soft); }
  .pill {
    padding: 6px 14px; border-radius: 20px;
    background: var(--m-glass-2); backdrop-filter: blur(10px);
    border: 1px solid var(--m-glass-bd); font-weight: 500;
  }
  .pill .src { color: #7ba577; }

  /* ============================================================
     HERO FULL-SCREEN CAROUSEL
  ============================================================ */
  .hero { position: relative; height: 100vh; width: 100%; overflow: hidden; display: none; }
  .hero.has-photos { display: block; }
  .hero-slide {
    position: absolute; inset: 0;
    background-size: cover; background-position: center;
    opacity: 0; transition: opacity 1.6s ease-in-out;
    transform: scale(1.06);
    animation: kenburns 18s ease-in-out infinite;
  }
  .hero-slide.active { opacity: 1; }
  @keyframes kenburns {
    0%   { transform: scale(1.0)  translate(0, 0); }
    50%  { transform: scale(1.14) translate(-1.5%, -1%); }
    100% { transform: scale(1.0)  translate(0, 0); }
  }
  .hero-overlay {
    position: absolute; inset: 0;
    background:
      linear-gradient(120deg, rgba(45,44,42,0.05) 0%, transparent 30%, transparent 70%, rgba(45,30,20,0.4) 100%),
      linear-gradient(to bottom,
      rgba(45,44,42,0.10) 0%, rgba(45,44,42,0.20) 40%,
      rgba(45,44,42,0.55) 80%, rgba(45,44,42,0.78) 100%);
  }
  /* 暖光泄漏 (Hero 角落金色光晕) */
  .hero-leak {
    position: absolute; inset: 0; pointer-events: none; z-index: 2;
    background:
      radial-gradient(ellipse 60% 50% at 100% 0%, rgba(255, 200, 140, 0.45), transparent 60%),
      radial-gradient(ellipse 50% 40% at 0% 100%, rgba(200, 150, 130, 0.35), transparent 60%);
    mix-blend-mode: screen;
  }
  .hero-content {
    position: absolute; left: 60px; bottom: 110px; z-index: 5; color: #f4ede1;
    max-width: 760px;
  }
  .hero-content .tag {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 8px 18px; border-radius: 20px;
    background: rgba(255,255,255,0.15);
    border: 1px solid rgba(255,255,255,0.35);
    backdrop-filter: blur(20px);
    font-size: 11px; letter-spacing: 0.22em; text-transform: uppercase; font-weight: 500;
    margin-bottom: 26px;
  }
  .hero-content .tag::before {
    content: ""; width: 6px; height: 6px; border-radius: 50%;
    background: #ffd9a8; box-shadow: 0 0 8px #ffd9a8;
    animation: dot-pulse 2.4s ease-in-out infinite;
  }
  @keyframes dot-pulse { 0%,100% { opacity: 0.5; } 50% { opacity: 1; } }
  .hero-content h1 {
    font-family: var(--serif);
    font-size: 78px; font-weight: 500; letter-spacing: -0.015em; line-height: 1.08;
    margin-bottom: 22px; text-shadow: 0 4px 30px rgba(0,0,0,0.4);
  }
  .hero-content p {
    font-family: var(--serif);
    font-size: 18px; font-weight: 300; line-height: 1.7; opacity: 0.9;
    text-shadow: 0 2px 12px rgba(0,0,0,0.3);
    max-width: 580px;
  }
  /* 右上角悬浮日期章 */
  .hero-date {
    position: absolute; right: 60px; top: 110px; z-index: 5; color: #f4ede1;
    text-align: right;
    font-family: var(--serif-en);
  }
  .hero-date .day-num {
    font-size: 56px; font-weight: 300; line-height: 1; letter-spacing: -0.02em;
    color: rgba(255, 230, 200, 0.95);
    text-shadow: 0 2px 20px rgba(0,0,0,0.4);
  }
  .hero-date .day-num small { font-size: 18px; opacity: 0.7; margin-left: 4px; font-style: italic; }
  .hero-date .day-label {
    font-size: 11px; letter-spacing: 0.3em; text-transform: uppercase;
    opacity: 0.6; margin-top: 6px; font-family: -apple-system, sans-serif;
  }
  .hero-date .day-line {
    width: 40px; height: 1px; background: rgba(255, 230, 200, 0.4);
    margin: 10px 0 0 auto;
  }
  .hero-controls { position: absolute; right: 60px; bottom: 110px; z-index: 5; display: flex; gap: 12px; }
  .hero-btn {
    width: 50px; height: 50px; border-radius: 50%;
    background: rgba(255,255,255,0.15); border: 1px solid rgba(255,255,255,0.3);
    backdrop-filter: blur(20px);
    color: #fff; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px; transition: all 0.3s ease;
  }
  .hero-btn:hover { background: rgba(255,255,255,0.28); transform: scale(1.06); }
  .hero-dots {
    position: absolute; bottom: 50px; left: 50%; transform: translateX(-50%);
    display: flex; gap: 8px; z-index: 5;
  }
  .hero-dot {
    width: 32px; height: 3px; background: rgba(255,255,255,0.32);
    border-radius: 2px; cursor: pointer; transition: all 0.4s ease;
  }
  .hero-dot.active { background: #fff; width: 52px; }

  /* ============================================================
     SECTION
  ============================================================ */
  .section { position: relative; z-index: 1; padding: 130px 60px 80px; display: none; }
  .section.has-photos { display: block; }

  /* Chapter 印章式分隔 */
  .chapter-mark {
    display: flex; align-items: center; justify-content: center;
    gap: 18px; margin-bottom: 50px; padding-top: 20px;
  }
  .cm-line {
    flex: 1; max-width: 220px; height: 1px;
    background: linear-gradient(90deg, transparent, rgba(122,119,114,0.3), transparent);
  }
  .cm-stamp {
    font-family: var(--serif);
    font-size: 14px; font-weight: 500; letter-spacing: 0.15em;
    color: var(--m-text-soft);
    padding: 6px 18px;
    border: 1px solid rgba(122,119,114,0.2);
    border-radius: 20px;
    background: rgba(255,255,255,0.4);
    backdrop-filter: blur(10px);
  }
  .cm-stamp em {
    font-style: italic; color: var(--warm); font-weight: 500;
  }
  .section-header {
    display: flex; justify-content: space-between; align-items: flex-end;
    margin-bottom: 50px; flex-wrap: wrap; gap: 24px;
  }
  .section-title {
    font-family: var(--serif);
    font-size: 54px; font-weight: 500; letter-spacing: -0.02em; line-height: 1.1;
  }
  .section-title small {
    display: flex; align-items: center; gap: 10px;
    font-size: 11px; font-weight: 500;
    color: var(--m-text-soft); letter-spacing: 0.28em; text-transform: uppercase;
    margin-bottom: 12px;
    font-family: -apple-system, sans-serif;
  }
  .section-title small::before {
    content: "✦"; color: var(--warm); font-size: 12px;
  }
  .section-desc { max-width: 420px; color: var(--m-text-soft); font-size: 15px; line-height: 1.7; }
  .section-actions { display: flex; gap: 10px; align-items: center; }
  .ghost-btn {
    padding: 8px 16px; border-radius: 20px; border: 1px solid rgba(122,119,114,0.2);
    background: rgba(255,255,255,0.5); cursor: pointer; font-size: 12px;
    color: var(--m-text); font-weight: 500; transition: all 0.25s ease;
    font-family: inherit;
  }
  .ghost-btn:hover { background: #fff; border-color: var(--m-clay); }

  /* ============================================================
     GRID
  ============================================================ */
  .grid { columns: 4; column-gap: 22px; }
  .grid-item {
    display: inline-block; width: 100%; margin-bottom: 22px;
    border-radius: 14px; overflow: hidden; position: relative;
    background: #fff; box-shadow: var(--shadow-soft);
    cursor: pointer; transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
    break-inside: avoid; vertical-align: top;
    --item-glow: 201, 168, 150;  /* 默认暖光,JS 会在分析后写入主色 */
  }
  .grid-item::after {
    content: ""; position: absolute; inset: 0; border-radius: inherit;
    box-shadow: inset 0 0 0 1px rgba(255,255,255,0.5),
                inset 0 0 30px rgba(var(--item-glow), 0.08);
    pointer-events: none;
    transition: box-shadow 0.5s ease;
  }
  .grid-item:hover {
    transform: translateY(-8px) scale(1.01);
    box-shadow: 0 20px 50px rgba(var(--item-glow), 0.25),
                0 8px 20px rgba(74, 72, 69, 0.12);
  }
  .grid-item:hover::after {
    box-shadow: inset 0 0 0 1px rgba(255,255,255,0.7),
                inset 0 0 50px rgba(var(--item-glow), 0.15);
  }
  .grid-item img { width: 100%; height: auto; display: block; transition: transform 0.8s ease; }
  .grid-item:hover img { transform: scale(1.04); }
  .grid-item .meta {
    position: absolute; left: 0; right: 0; bottom: 0;
    padding: 70px 18px 16px;
    background: linear-gradient(to top, rgba(0,0,0,0.65), transparent);
    color: #fff; opacity: 0; transition: opacity 0.4s ease;
    font-size: 12px; line-height: 1.5; pointer-events: none;
  }
  .grid-item:hover .meta { opacity: 1; }
  .grid-item .meta strong { font-size: 14px; font-weight: 600; }
  .color-dot {
    display: inline-block; width: 8px; height: 8px; border-radius: 50%;
    margin-right: 7px; vertical-align: middle;
    box-shadow: 0 0 0 2px rgba(255,255,255,0.35), 0 1px 3px rgba(0,0,0,0.2);
    transition: transform 0.3s ease;
  }
  .grid-item:hover .color-dot { transform: scale(1.4); }
  .grid-item .meta .analyzing { opacity: 0.6; font-style: italic; }

  /* ============================================================
     MUSIC PLAYER
  ============================================================ */
  .player {
    position: fixed; right: 26px; bottom: 26px;
    z-index: 200; width: 360px;
    background: rgba(255, 255, 255, 0.6);
    backdrop-filter: saturate(180%) blur(40px);
    -webkit-backdrop-filter: saturate(180%) blur(40px);
    border: 1px solid var(--m-glass-bd);
    border-radius: 24px; padding: 18px;
    box-shadow: var(--shadow-hard);
    transition: all 0.45s cubic-bezier(0.4, 0, 0.2, 1);
  }
  .player.collapsed { width: 64px; height: 64px; padding: 0; overflow: hidden; }
  .player.collapsed .player-body, .player.collapsed .player-meta { display: none; }
  .player.collapsed .player-toggle {
    position: static; width: 100%; height: 100%; border-radius: 24px;
    background: linear-gradient(135deg, var(--m-rose), var(--m-clay));
    color: #fff; font-size: 22px;
    box-shadow: 0 6px 18px rgba(201, 168, 150, 0.4);
  }
  .player.collapsed .player-toggle:hover { transform: scale(1.04); }
  .player-toggle {
    position: absolute; right: 16px; top: 16px;
    width: 28px; height: 28px; border-radius: 50%;
    background: rgba(0,0,0,0.06); border: none; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    color: var(--m-text-soft); font-size: 13px;
    transition: all 0.3s ease;
  }
  .player-toggle:hover { background: rgba(0,0,0,0.1); }
  .player-meta { display: flex; gap: 14px; align-items: center; margin-bottom: 14px; padding-right: 36px; }
  .cover {
    width: 56px; height: 56px; border-radius: 50%;
    background:
      radial-gradient(circle at center, var(--m-clay) 0%, var(--m-clay) 28%, #2a2825 28%, #1a1815 100%);
    display: flex; align-items: center; justify-content: center;
    color: #f4ede1; font-size: 9px; font-weight: 600; flex-shrink: 0;
    position: relative; overflow: hidden;
    box-shadow: 0 4px 14px rgba(0,0,0,0.25), inset 0 0 0 1px rgba(255,255,255,0.08);
  }
  /* 黑胶纹路 */
  .cover::before {
    content: ""; position: absolute; inset: 28%; border-radius: 50%;
    background:
      repeating-radial-gradient(circle, transparent 0px, transparent 1px, rgba(255,255,255,0.04) 1px, rgba(255,255,255,0.04) 2px);
  }
  .cover::after {
    content: ""; position: absolute; left: 50%; top: 50%;
    width: 6px; height: 6px; border-radius: 50%;
    background: var(--m-cream);
    transform: translate(-50%, -50%);
    box-shadow: 0 0 0 2px rgba(0,0,0,0.4);
  }
  .cover .cover-label {
    position: absolute; left: 50%; top: 50%;
    transform: translate(-50%, -50%);
    font-size: 7px; font-weight: 600; letter-spacing: 0.5px;
    color: var(--m-cream); text-transform: uppercase;
    z-index: 2; opacity: 0.7;
  }
  .cover.playing { animation: vinyl-spin 4s linear infinite; }
  @keyframes vinyl-spin { to { transform: rotate(360deg); } }
  .track-info { flex: 1; min-width: 0; }
  .track-name { font-size: 14px; font-weight: 600; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .track-artist { font-size: 12px; color: var(--m-text-soft); margin-top: 2px; }
  .player-body { padding-top: 4px; }
  .progress {
    height: 4px; background: rgba(0,0,0,0.07); border-radius: 2px;
    overflow: hidden; cursor: pointer; margin-bottom: 4px;
  }
  .progress-bar {
    height: 100%; width: 0%;
    background: linear-gradient(90deg, var(--m-rose), var(--m-clay));
    border-radius: 2px; transition: width 0.1s linear;
  }
  .time { display: flex; justify-content: space-between; font-size: 10px; color: var(--m-text-soft); margin-bottom: 14px; font-variant-numeric: tabular-nums; }
  .controls { display: flex; align-items: center; justify-content: center; gap: 22px; }
  .ctrl {
    background: none; border: none; cursor: pointer; color: var(--m-text);
    width: 30px; height: 30px; display: flex; align-items: center; justify-content: center;
    font-size: 14px; transition: all 0.2s ease;
  }
  .ctrl:hover { color: var(--m-clay); transform: scale(1.08); }
  .ctrl.play {
    width: 42px; height: 42px; border-radius: 50%;
    background: linear-gradient(135deg, var(--m-rose), var(--m-clay));
    color: #fff; box-shadow: 0 6px 16px rgba(201, 168, 150, 0.4);
  }
  .ctrl.play:hover { transform: scale(1.06); }
  .ctrl:disabled { opacity: 0.4; cursor: not-allowed; }

  /* ============================================================
     LIGHTBOX
  ============================================================ */
  .lightbox {
    position: fixed; inset: 0; z-index: 1000;
    background: rgba(45, 44, 42, 0.96);
    backdrop-filter: blur(20px);
    display: none; align-items: center; justify-content: center;
    padding: 40px; opacity: 0; transition: opacity 0.4s ease;
  }
  .lightbox.open { display: flex; opacity: 1; }
  .lightbox img { max-width: 90vw; max-height: 88vh; border-radius: 12px; box-shadow: 0 20px 60px rgba(0,0,0,0.4); }
  .lightbox .close {
    position: absolute; top: 30px; right: 30px;
    width: 44px; height: 44px; border-radius: 50%;
    background: rgba(255,255,255,0.15); border: 1px solid rgba(255,255,255,0.3);
    color: #fff; cursor: pointer; font-size: 22px;
    display: flex; align-items: center; justify-content: center; transition: all 0.25s ease;
  }
  .lightbox .close:hover { background: rgba(255,255,255,0.25); transform: scale(1.06); }

  /* ============================================================
     TOAST
  ============================================================ */
  .toast {
    position: fixed; top: 90px; left: 50%; transform: translateX(-50%) translateY(-30px);
    z-index: 500;
    padding: 12px 22px; border-radius: 20px;
    background: rgba(45, 44, 42, 0.85);
    backdrop-filter: blur(20px);
    color: #f4ede1; font-size: 13px;
    opacity: 0; transition: all 0.4s ease;
    pointer-events: none;
    box-shadow: var(--shadow-hard);
  }
  .toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

  /* ============================================================
     FOOTER
  ============================================================ */
  .footer { padding: 50px 60px 100px; text-align: center; color: var(--m-text-soft); font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase; }

  /* ============================================================
     RESPONSIVE
  ============================================================ */
  @media (max-width: 1024px) {
    .grid { columns: 3; }
    .hero-content h1 { font-size: 48px; }
    .section-title { font-size: 38px; }
  }
  @media (max-width: 768px) {
    .grid { columns: 2; column-gap: 14px; }
    .grid-item { margin-bottom: 14px; border-radius: 12px; }
    .section { padding: 80px 20px 60px; }
    .nav { padding: 14px 20px; }
    .nav-meta { display: none; }
    .hero-content { left: 24px; right: 24px; bottom: 90px; }
    .hero-content h1 { font-size: 36px; }
    .hero-content p { font-size: 15px; }
    .hero-controls { right: 24px; bottom: 90px; }
    .section-header { flex-direction: column; align-items: flex-start; }
    .section-title { font-size: 32px; }
    .setup { padding: 0 20px; margin-top: 60px; }
    .setup-card { padding: 32px 24px; border-radius: 22px; }
    .setup-card h2 { font-size: 24px; }
    .player { right: 12px; bottom: 12px; width: calc(100vw - 24px); max-width: 360px; }
  }
</style>
</head>
<body>

  <!-- ============================================================
       ENTRY GATE
  ============================================================ -->
  <!-- Bokeh 漂浮粒子层 -->
  <div class="bokeh" id="bokeh"></div>

  <div class="gate" id="gate">
    <div class="gate-inner">
      <div class="gate-mark">✦</div>
      <h2>宥宥成长日记</h2>
      <p>记录小宥宥的每一步成长<br>轻触进入 · 让音乐与光影一起流淌</p>
      <div class="enter-hint">TAP TO ENTER</div>
    </div>
  </div>

  <!-- ============================================================
       NAV
  ============================================================ -->
  <nav class="nav" style="display:none" id="nav">
    <div class="brand">
      <span class="dot"></span>
      <span>宥宥成长日记</span>
    </div>
    <div class="nav-meta">
      <span class="pill" id="photoCount">0 张照片</span>
      <span class="pill"><span class="src" id="srcLabel">未连接</span></span>
      <span class="pill" id="dateText">2026</span>
    </div>
  </nav>

  <!-- ============================================================
       HERO
  ============================================================ -->
  <section class="hero" id="hero">
    <div class="hero-overlay"></div>
    <div class="hero-leak"></div>
    <div class="hero-date">
      <div class="day-num" id="heroDayNum">∞<small>th</small></div>
      <div class="day-line"></div>
      <div class="day-label" id="heroDateLabel">PHOTO ALBUM</div>
    </div>
    <div class="hero-content">
      <span class="tag">YouYou's Diary · 宥宥的成长</span>
      <h1 id="heroTitle">把世界，一点一点讲给你听</h1>
      <p id="heroSubtitle">每一天都在长大 · 每一刻都值得被温柔地记下</p>
    </div>
    <div class="hero-controls">
      <button class="hero-btn" id="prevSlide" aria-label="上一张">←</button>
      <button class="hero-btn" id="nextSlide" aria-label="下一张">→</button>
    </div>
    <div class="hero-dots" id="heroDots"></div>
  </section>

  <!-- ============================================================
       SETUP PANEL
  ============================================================ -->
  <div class="setup" id="setup">
    <div class="setup-card">
      <h2>连接宥宥的照片</h2>
      <p class="sub">由于浏览器安全限制,网页无法自动读取电脑上的照片。请点击下方按钮,选择装满宥宥照片的文件夹 — 授权后我会自动加载所有图片,并在下次打开时自动恢复。</p>

      <div class="setup-row" id="photoRow">
        <div class="setup-icon">📁</div>
        <div class="setup-text">
          <strong>照片文件夹</strong>
          <span id="photoStatus">未连接</span>
        </div>
        <button class="setup-btn" id="btnPickFolder">选择文件夹</button>
      </div>

      <div class="setup-row" id="musicRow">
        <div class="setup-icon music">♪</div>
        <div class="setup-text">
          <strong>背景音乐</strong>
          <span id="musicStatus">未选择 · 支持 .flac / .mp3 / .wav 等</span>
        </div>
        <button class="setup-btn" id="btnPickMusic">选择音乐</button>
      </div>

      <button class="setup-btn" id="btnEnter" style="display:none;width:100%;margin-top:18px;padding:12px 18px;font-size:13px;border-radius:24px;background:linear-gradient(135deg,var(--m-rose),var(--m-clay));color:#fff;border:none;box-shadow:0 6px 20px rgba(201,168,150,0.35);">
        进入相册 →
      </button>

      <div class="setup-foot">
        ⚠️ <strong>仅在 Chrome / Edge / Opera 浏览器可用此自动连接方式</strong>(基于 File System Access API)。<br>
        若使用 Safari / Firefox,请改用 <code>拖入文件夹</code> 方式 — 在主页"宥宥的足迹"区域直接拖入照片即可。<br><br>
        📌 推荐路径: <code>C:\Users\Alex\Desktop\aiworkshop\photo</code>
      </div>
    </div>
  </div>

  <!-- ============================================================
       GALLERY
  ============================================================ -->
  <section class="section" id="gallery">
    <div class="chapter-mark">
      <span class="cm-line"></span>
      <span class="cm-stamp">Chapter I · <em>成长的形状</em></span>
      <span class="cm-line"></span>
    </div>
    <div class="section-header">
      <div class="section-title">
        <small>Gallery · 宥宥的足迹</small>
        一天一天长大
      </div>
      <p class="section-desc">把装满宥宥照片的文件夹拖到这里,或点击下方区域浏览小宥宥的成长瞬间。若未上传,将以柔和的旅行风景作为占位。</p>
      <div class="section-actions">
        <button class="ghost-btn" id="btnAddMore">＋ 添加更多照片</button>
        <button class="ghost-btn" id="btnChangeFolder">↻ 更换文件夹</button>
      </div>
    </div>

    <div class="dropzone" id="dropzone" style="display:none">
      <div class="setup-row" style="border:none;padding:0">
        <div class="setup-icon">＋</div>
        <div class="setup-text">
          <strong>把宥宥的文件夹拖到这里</strong>
          <span>支持拖入整个文件夹 · 仅在当前浏览器会话内有效</span>
        </div>
        <button class="setup-btn" id="btnPickFolder2">或点击选择</button>
      </div>
    </div>

    <div class="grid" id="grid"></div>
  </section>

  <!-- ============================================================
       LIGHTBOX
  ============================================================ -->
  <div class="lightbox" id="lightbox">
    <button class="close" id="lightboxClose" aria-label="关闭">×</button>
    <img id="lightboxImg" src="" alt="">
  </div>

  <!-- ============================================================
       TOAST
  ============================================================ -->
  <div class="toast" id="toast"></div>

  <!-- ============================================================
       MUSIC PLAYER
  ============================================================ -->
  <div class="player" id="player">
    <button class="player-toggle" id="playerToggle" aria-label="收起/展开">⌃</button>
    <div class="player-meta">
      <div class="cover" id="cover"><span class="cover-label">YOUYOU</span></div>
      <div class="track-info">
        <div class="track-name" id="trackName">未选择音乐</div>
        <div class="track-artist" id="trackArtist">点击选择音乐文件</div>
      </div>
    </div>
    <div class="player-body">
      <div class="progress" id="progress">
        <div class="progress-bar" id="progressBar"></div>
      </div>
      <div class="time">
        <span id="curTime">0:00</span>
        <span id="durTime">0:00</span>
      </div>
      <div class="controls">
        <button class="ctrl" id="rewind" aria-label="后退10秒" disabled>↺</button>
        <button class="ctrl play" id="play" aria-label="播放/暂停" disabled>▶</button>
        <button class="ctrl" id="forward" aria-label="前进10秒" disabled>↻</button>
      </div>
    </div>
    <audio id="audio" preload="auto" loop></audio>
  </div>

  <!-- 隐藏的文件选择器: 照片文件夹 / 音乐文件 -->
  <input type="file" id="musicInput" accept="audio/*,.flac,.mp3,.wav,.m4a,.ogg,.aac,.opus" style="display:none">
  <input type="file" id="folderInput" webkitdirectory directory multiple style="display:none">
  <input type="file" id="imageInput" accept="image/*" multiple style="display:none">

  <footer class="footer">
    宥 宥 成 长 日 记 · EVERY LITTLE STEP COUNTS
  </footer>

<script>
/* ==============================================================
   CONFIG
============================================================== */
const CONFIG = {
  // 期望的默认文件夹名(用于提示)
  preferredFolder: "aiworkshop",
  // 支持的图片扩展
  IMG_EXT: /\.(jpe?g|png|gif|webp|bmp|heic|heif|avif|svg|jfif|tiff?)$/i,
  // 音乐支持类型
  AUDIO_EXT: /\.(mp3|flac|wav|m4a|ogg|aac|opus)$/i,
};

/* ==============================================================
   STATE
============================================================== */
const state = {
  photos: [],
  heroIndex: 0,
  heroTimer: null,
  isPlaying: false,
  dirHandle: null,
  musicUrl: null,
  currentMusicName: "",
};

/* ==============================================================
   INDEXEDDB  (持久化: 句柄 + 音乐 Blob)
============================================================== */
function openDB() {
  return new Promise((resolve, reject) => {
    const req = indexedDB.open("family-album-db", 1);
    req.onupgradeneeded = () => {
      const db = req.result;
      if (!db.objectStoreNames.contains("handles")) db.createObjectStore("handles");
      if (!db.objectStoreNames.contains("music"))   db.createObjectStore("music");
    };
    req.onsuccess = () => resolve(req.result);
    req.onerror = () => reject(req.error);
  });
}
async function saveHandle(key, handle) {
  try {
    const db = await openDB();
    return new Promise((resolve, reject) => {
      const tx = db.transaction("handles", "readwrite");
      tx.objectStore("handles").put(handle, key);
      tx.oncomplete = () => resolve();
      tx.onerror = () => reject(tx.error);
    });
  } catch (e) { console.warn("saveHandle failed:", e); }
}
async function loadHandle(key) {
  try {
    const db = await openDB();
    return new Promise((resolve, reject) => {
      const tx = db.transaction("handles", "readonly");
      const req = tx.objectStore("handles").get(key);
      req.onsuccess = () => resolve(req.result);
      req.onerror = () => reject(req.error);
    });
  } catch (e) { return null; }
}
async function removeHandle(key) {
  try {
    const db = await openDB();
    return new Promise((resolve) => {
      const tx = db.transaction("handles", "readwrite");
      tx.objectStore("handles").delete(key);
      tx.oncomplete = () => resolve();
      tx.onerror = () => resolve();
    });
  } catch (e) {}
}

// 音乐: 以 Blob 形式存到 IndexedDB (任何浏览器通用,不受 FSA API 限制)
async function saveMusicToDB(file) {
  try {
    const db = await openDB();
    return new Promise((resolve, reject) => {
      const tx = db.transaction("music", "readwrite");
      tx.objectStore("music").put({ name: file.name, type: file.type || "audio/flac", blob: file }, "current");
      tx.oncomplete = () => resolve();
      tx.onerror = () => reject(tx.error);
    });
  } catch (e) { console.warn("saveMusicToDB failed:", e); }
}
async function loadMusicFromDB() {
  try {
    const db = await openDB();
    return new Promise((resolve) => {
      const tx = db.transaction("music", "readonly");
      const req = tx.objectStore("music").get("current");
      req.onsuccess = () => resolve(req.result || null);
      req.onerror = () => resolve(null);
    });
  } catch (e) { return null; }
}

/* ==============================================================
   PHOTO NAMING ENGINE
   - 提取每张图的主色调 → 映射到莫兰迪色名
   - 用文件时间生成「X月X日 · 时段 · 颜色」命名
   - 配小色点显示真实取色
============================================================== */
function rgbToHsl(r, g, b) {
  r /= 255; g /= 255; b /= 255;
  const max = Math.max(r, g, b), min = Math.min(r, g, b);
  let h = 0, s = 0, l = (max + min) / 2;
  if (max !== min) {
    const d = max - min;
    s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
    if      (max === r) h = (g - b) / d + (g < b ? 6 : 0);
    else if (max === g) h = (b - r) / d + 2;
    else                h = (r - g) / d + 4;
    h *= 60;
  }
  return [h, s, l];
}

// 莫兰迪色名映射表: [色相min, 色相max, 饱和min, 饱和max, 亮度min, 亮度max, 名字]
const MORANDI_TABLE = [
  // 无彩色系
  [0, 360, 0,    0.12, 0,    0.20, "墨色"],
  [0, 360, 0,    0.12, 0.20, 0.45, "烟灰"],
  [0, 360, 0,    0.12, 0.45, 0.75, "燕麦"],
  [0, 360, 0,    0.12, 0.75, 1.00, "奶白"],
  // 红 / 粉
  [330, 360, 0.12, 0.40, 0,    0.50, "酒红"],
  [330, 360, 0.12, 0.40, 0.50, 1.00, "烟粉"],
  [330, 360, 0.40, 1.00, 0,    0.50, "绛紫"],
  [330, 360, 0.40, 1.00, 0.50, 1.00, "玫粉"],
  [0,   30,  0.12, 0.40, 0,    0.50, "赭石"],
  [0,   30,  0.12, 0.40, 0.50, 1.00, "杏色"],
  // 橙 / 黄
  [0,   30,  0.40, 1.00, 0,    0.50, "焦糖"],
  [0,   30,  0.40, 1.00, 0.50, 1.00, "落日"],
  [30,  60,  0.12, 0.40, 0,    0.50, "橄榄"],
  [30,  60,  0.12, 0.40, 0.50, 1.00, "麦黄"],
  [30,  60,  0.40, 1.00, 0,    0.50, "土黄"],
  [30,  60,  0.40, 1.00, 0.50, 1.00, "金黄"],
  // 绿
  [60, 150,  0.12, 0.40, 0,    0.50, "墨绿"],
  [60, 150,  0.12, 0.40, 0.50, 1.00, "抹茶"],
  [60, 150,  0.40, 1.00, 0,    0.50, "松石"],
  [60, 150,  0.40, 1.00, 0.50, 1.00, "草绿"],
  // 青
  [150,200,  0.12, 0.40, 0,    0.50, "黛青"],
  [150,200,  0.12, 0.40, 0.50, 1.00, "烟青"],
  [150,200,  0.40, 1.00, 0,    1.00, "松绿"],
  // 蓝
  [200,260,  0.12, 0.40, 0,    0.50, "黛蓝"],
  [200,260,  0.12, 0.40, 0.50, 1.00, "雾蓝"],
  [200,260,  0.40, 1.00, 0,    0.50, "靛蓝"],
  [200,260,  0.40, 1.00, 0.50, 1.00, "天蓝"],
  // 紫
  [260,330,  0.12, 0.40, 0,    0.50, "灰紫"],
  [260,330,  0.12, 0.40, 0.50, 1.00, "丁香"],
  [260,330,  0.40, 1.00, 0,    0.50, "紫罗兰"],
  [260,330,  0.40, 1.00, 0.50, 1.00, "藕粉"],
];

function classifyColor(r, g, b) {
  const [h, s, l] = rgbToHsl(r, g, b);
  for (const [hMin, hMax, sMin, sMax, lMin, lMax, name] of MORANDI_TABLE) {
    if (h >= hMin && h < hMax && s >= sMin && s < sMax && l >= lMin && l < lMax) {
      return { name, r: Math.round(r), g: Math.round(g), b: Math.round(b) };
    }
  }
  return { name: "柔光", r: Math.round(r), g: Math.round(g), b: Math.round(b) };
}

function getTimeOfDay(hour) {
  if (hour >= 5  && hour < 8)  return "清晨";
  if (hour >= 8  && hour < 11) return "上午";
  if (hour >= 11 && hour < 13) return "正午";
  if (hour >= 13 && hour < 17) return "午后";
  if (hour >= 17 && hour < 19) return "黄昏";
  if (hour >= 19 && hour < 22) return "夜幕";
  return "深夜";
}

// 从图片 URL 提取主色 (通过 32x32 canvas 采样)
function analyzeImageUrl(url) {
  return new Promise((resolve) => {
    const img = new Image();
    img.onload = () => {
      try {
        const c = document.createElement("canvas");
        c.width = c.height = 32;
        const ctx = c.getContext("2d");
        ctx.drawImage(img, 0, 0, 32, 32);
        const data = ctx.getImageData(0, 0, 32, 32).data;
        let r = 0, g = 0, b = 0, n = 0;
        for (let i = 0; i < data.length; i += 4) {
          if (data[i + 3] < 128) continue;       // 跳过透明像素
          r += data[i]; g += data[i+1]; b += data[i+2]; n++;
        }
        if (!n) return resolve(null);
        r /= n; g /= n; b /= n;
        resolve({ r, g, b, color: classifyColor(r, g, b) });
      } catch (e) { resolve(null); }
    };
    img.onerror = () => resolve(null);
    img.src = url;
  });
}

function buildPhotoTitle(file, analysis) {
  const d = new Date(file.lastModified || Date.now());
  const m = d.getMonth() + 1, day = d.getDate();
  const time = getTimeOfDay(d.getHours());
  const color = analysis?.color?.name || "柔光";
  // 用 "X月X日 · 时段 · 颜色",同组去重加序号
  return { title: `${m}月${day}日 · ${time} · ${color}`, time, color, colorRgb: analysis?.color ? `${analysis.color.r},${analysis.color.g},${analysis.color.b}` : "200,180,160" };
}

// 批量分析所有照片,带进度提示
async function analyzeAndName(photos) {
  if (!photos.length) return;
  const BATCH = 6;
  toast(`正在为照片寻找名字…`);
  for (let i = 0; i < photos.length; i += BATCH) {
    const batch = photos.slice(i, i + BATCH);
    await Promise.all(batch.map(async (p) => {
      const analysis = await analyzeImageUrl(p.src);
      const named = buildPhotoTitle(p.file || p, analysis);
      p.title = named.title;
      p.colorRgb = named.colorRgb;
      p.colorName = named.color;
    }));
    // 每批完成后增量更新 UI
    renderHero();
    renderGrid();
  }
  toast(`✓ 已为 ${photos.length} 张照片命名`);
}

/* ==============================================================
   TOAST
============================================================== */
const toastEl = document.getElementById("toast");
let toastTimer = null;
function toast(msg) {
  toastEl.textContent = msg;
  toastEl.classList.add("show");
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => toastEl.classList.remove("show"), 2800);
}

/* ==============================================================
   FILE SYSTEM ACCESS  (Chrome / Edge / Opera)
============================================================== */
const FSA_SUPPORTED = "showDirectoryPicker" in window && "showOpenFilePicker" in window;

async function pickDirectory() {
  if (!FSA_SUPPORTED) {
    toast("此浏览器不支持,请用 Safari/Firefox 的拖入方式");
    return null;
  }
  try {
    const handle = await window.showDirectoryPicker({ id: "family-album", mode: "read" });
    return handle;
  } catch (e) {
    if (e.name !== "AbortError") console.warn(e);
    return null;
  }
}

// 注: 音乐选择改用普通 <input type="file"> + IndexedDB Blob,兼容性更好
// (File System Access API 在 file:// 协议下经常失效,且 FLAC MIME 类型不统一)

async function readPhotosFromHandle(dirHandle) {
  const photos = [];
  // 递归读取 (async iteration)
  async function walk(handle, prefix) {
    for await (const [name, child] of handle.entries()) {
      if (child.kind === "file") {
        if (CONFIG.IMG_EXT.test(name)) {
          const file = await child.getFile();
          photos.push({
            file,
            src: URL.createObjectURL(file),
            title: name.replace(/\.[^.]+$/, "").slice(0, 40),
            date: file.lastModified ? new Date(file.lastModified).toLocaleDateString("zh-CN") : "未命名",
            source: "local",
          });
        }
      } else if (child.kind === "directory") {
        if (name.startsWith(".") || name === "node_modules" || name === "@eaDir") continue;
        await walk(child, prefix + name + "/");
      }
    }
  }
  await walk(dirHandle, "");
  // 按文件名/修改时间排序
  photos.sort((a, b) => (a.file.lastModified || 0) - (b.file.lastModified || 0));
  return photos;
}

async function ensurePermission(handle, mode = "read") {
  if (!handle.queryPermission) return "granted";
  let p = await handle.queryPermission({ mode });
  if (p === "granted") return "granted";
  p = await handle.requestPermission({ mode });
  return p;
}

/* ==============================================================
   GALLERY / HERO
============================================================== */
// 完成度状态
const ready = { photos: false, music: false };

function updateEnterBtn() {
  const btn = document.getElementById("btnEnter");
  // 至少要选好照片才能进入(音乐可选)
  if (ready.photos) {
    btn.style.display = "block";
    btn.textContent = ready.music ? "进入相册 →" : "不选音乐,直接进入 →";
  } else {
    btn.style.display = "none";
  }
}

function hideSetup() {
  document.getElementById("setup").style.display = "none";
  document.getElementById("nav").style.display = "flex";
}

function showGallery() {
  document.getElementById("hero").classList.add("has-photos");
  document.getElementById("gallery").classList.add("has-photos");
  document.getElementById("dropzone").style.display = "block";
  // 不再隐藏 setup,改由 updateEnterBtn 控制"进入"按钮
}

function renderHero() {
  const hero = document.getElementById("hero");
  hero.querySelectorAll(".hero-slide").forEach(s => s.remove());
  const slides = state.photos.slice(0, Math.min(6, state.photos.length));
  slides.forEach((p, i) => {
    const div = document.createElement("div");
    div.className = "hero-slide" + (i === 0 ? " active" : "");
    div.style.backgroundImage = `url(${p.src})`;
    hero.insertBefore(div, hero.firstChild);
  });
  const dots = document.getElementById("heroDots");
  dots.innerHTML = "";
  slides.forEach((_, i) => {
    const d = document.createElement("div");
    d.className = "hero-dot" + (i === 0 ? " active" : "");
    d.addEventListener("click", () => goToSlide(i));
    dots.appendChild(d);
  });
  if (slides.length && slides[0].title) {
    document.getElementById("heroTitle").textContent = slides[0].title;
  }
  startHeroAutoplay();
}

function goToSlide(i) {
  const slides = document.querySelectorAll(".hero-slide");
  const dots = document.querySelectorAll(".hero-dot");
  if (!slides.length) return;
  slides[state.heroIndex]?.classList.remove("active");
  dots[state.heroIndex]?.classList.remove("active");
  state.heroIndex = (i + slides.length) % slides.length;
  slides[state.heroIndex].classList.add("active");
  dots[state.heroIndex]?.classList.add("active");
  const cur = state.photos[state.heroIndex];
  if (cur?.title) document.getElementById("heroTitle").textContent = cur.title;
}

function startHeroAutoplay() {
  clearInterval(state.heroTimer);
  state.heroTimer = setInterval(() => goToSlide(state.heroIndex + 1), 5500);
}

document.getElementById("prevSlide").addEventListener("click", () => { goToSlide(state.heroIndex - 1); startHeroAutoplay(); });
document.getElementById("nextSlide").addEventListener("click", () => { goToSlide(state.heroIndex + 1); startHeroAutoplay(); });

function renderGrid() {
  const grid = document.getElementById("grid");
  grid.innerHTML = "";
  state.photos.forEach((p, i) => {
    const item = document.createElement("div");
    item.className = "grid-item";
    // 把主色 RGB 注入 CSS 变量,产生"颜色阴影"
    if (p.colorRgb) item.style.setProperty("--item-glow", p.colorRgb);
    const dot = p.colorRgb
      ? `<span class="color-dot" style="background:rgb(${p.colorRgb})"></span>`
      : "";
    const titleHtml = p.title
      ? `<div class="meta"><strong>${dot}${p.title}</strong><br><span style="opacity:.85;font-size:11px">${p.date || ''}</span></div>`
      : (p.title === undefined
          ? `<div class="meta"><strong class="analyzing">正在识别色彩…</strong></div>`
          : "");
    item.innerHTML = `
      <img src="${p.src}" alt="${p.title || ''}" loading="lazy">
      ${titleHtml}
    `;
    item.addEventListener("click", () => openLightbox(p.src));
    grid.appendChild(item);
  });
  updateHeroDateStamp();
}

function openLightbox(src) {
  document.getElementById("lightboxImg").src = src;
  document.getElementById("lightbox").classList.add("open");
}
document.getElementById("lightboxClose").addEventListener("click", () => document.getElementById("lightbox").classList.remove("open"));
document.getElementById("lightbox").addEventListener("click", (e) => { if (e.target.id === "lightbox") document.getElementById("lightbox").classList.remove("open"); });

function updateCount() {
  document.getElementById("photoCount").textContent = `${state.photos.length} 张照片`;
  document.getElementById("dateText").textContent = new Date().getFullYear();
  if (state.dirHandle) {
    document.getElementById("srcLabel").textContent = "📁 " + state.dirHandle.name;
  }
}

/* ==============================================================
   ATMOSPHERIC — bokeh 漂浮粒子 + Hero 日期章
============================================================== */
function spawnBokeh() {
  const box = document.getElementById("bokeh");
  if (!box) return;
  // 莫兰迪色 + 暖金,共 18 颗
  const palette = [
    "rgba(255, 220, 180, 0.55)",  // 暖金
    "rgba(212, 181, 176, 0.45)",  // 雾粉
    "rgba(196, 184, 204, 0.40)",  // 灰紫
    "rgba(176, 192, 204, 0.40)",  // 烟蓝
    "rgba(232, 220, 198, 0.50)",  // 燕麦
  ];
  for (let i = 0; i < 18; i++) {
    const s = document.createElement("span");
    const size = 60 + Math.random() * 160;
    s.style.width = s.style.height = size + "px";
    s.style.left = Math.random() * 100 + "%";
    s.style.background = `radial-gradient(circle, ${palette[i % palette.length]}, transparent 70%)`;
    s.style.setProperty("--dx", (Math.random() * 200 - 100) + "px");
    s.style.animationDuration = (20 + Math.random() * 25) + "s";
    s.style.animationDelay = (Math.random() * -30) + "s";
    s.style.opacity = 0.5 + Math.random() * 0.4;
    box.appendChild(s);
  }
}

function updateHeroDateStamp() {
  // 右侧"第 N 张"计数器 (基于已加载照片数)
  const n = state.photos.length || 0;
  const dayEl = document.getElementById("heroDayNum");
  const labelEl = document.getElementById("heroDateLabel");
  if (dayEl) dayEl.innerHTML = `${n || "∞"}<small>${n ? "frames" : "th"}</small>`;
  if (labelEl) labelEl.textContent = n ? "MEMORIES CAPTURED" : "PHOTO ALBUM";
}

/* ==============================================================
   FOLDER PICK FLOW
============================================================== */
async function onPickFolder() {
  const handle = await pickDirectory();
  if (!handle) return;
  await saveHandle("photoDir", handle);
  state.dirHandle = handle;
  // 行内状态: 绿色 ✓ + 改成"更换"
  const photoStatus = document.getElementById("photoStatus");
  const photoBtn = document.getElementById("btnPickFolder");
  photoStatus.innerHTML = '<span class="ok">✓ ' + handle.name + ' · 已就绪</span>';
  photoBtn.textContent = "更换";
  await loadPhotos();
  if (state.photos.length) {
    ready.photos = true;
    showGallery();
    updateEnterBtn();
    toast(`已加载 ${state.photos.length} 张照片`);
  } else {
    toast("该文件夹中没有找到图片");
  }
}

async function loadPhotos() {
  if (!state.dirHandle) return;
  const perm = await ensurePermission(state.dirHandle, "read");
  if (perm !== "granted") {
    toast("需要读取权限");
    return;
  }
  // 释放旧 URL
  state.photos.forEach(p => p.src?.startsWith("blob:") && URL.revokeObjectURL(p.src));
  state.photos = await readPhotosFromHandle(state.dirHandle);
  // 先用占位标题渲染,再异步分析命名
  state.photos.forEach(p => { if (!p.title) p.title = "正在识别色彩…"; });
  renderHero();
  renderGrid();
  updateCount();
  // 启动色彩分析 (异步,不阻塞)
  analyzeAndName(state.photos);
}

/* ==============================================================
   MUSIC PICK FLOW  (普通 <input type="file"> + IndexedDB Blob)
============================================================== */
const musicInput = document.getElementById("musicInput");

async function onPickMusic() {
  musicInput.click();
}

musicInput.addEventListener("change", async (e) => {
  const file = e.target.files && e.target.files[0];
  if (!file) return;
  // 存到 IndexedDB,下次自动恢复
  await saveMusicToDB(file);
  applyMusicFile(file);
  toast("♪ 已加载音乐 · " + file.name);
});

// 也支持把音频文件直接拖到播放器上
const playerEl = document.getElementById("player");
["dragenter", "dragover"].forEach(ev => {
  playerEl.addEventListener(ev, e => {
    if (e.dataTransfer && Array.from(e.dataTransfer.types).includes("Files")) {
      e.preventDefault();
      playerEl.style.transform = "scale(1.02)";
      playerEl.style.boxShadow = "0 24px 70px rgba(201, 168, 150, 0.35)";
    }
  });
});
["dragleave", "drop"].forEach(ev => {
  playerEl.addEventListener(ev, e => {
    playerEl.style.transform = "";
    playerEl.style.boxShadow = "";
  });
});
playerEl.addEventListener("drop", async (e) => {
  e.preventDefault();
  const file = e.dataTransfer.files && e.dataTransfer.files[0];
  if (!file) return;
  if (!/^audio\//.test(file.type) && !/\.(mp3|flac|wav|m4a|ogg|aac|opus)$/i.test(file.name)) {
    toast("请拖入音频文件");
    return;
  }
  await saveMusicToDB(file);
  applyMusicFile(file);
  toast("♪ 已加载音乐 · " + file.name);
});

function applyMusicFile(file) {
  if (state.musicUrl) URL.revokeObjectURL(state.musicUrl);
  state.musicUrl = URL.createObjectURL(file);
  state.currentMusicName = file.name;
  const audio = document.getElementById("audio");
  audio.src = state.musicUrl;
  audio.volume = 0.55;
  document.getElementById("trackName").textContent = file.name.replace(/\.[^.]+$/, "");
  document.getElementById("trackArtist").textContent = "♪ 等待播放";
  document.getElementById("musicStatus").innerHTML = '<span class="ok">✓ ' + file.name + '</span>';
  document.getElementById("play").disabled = false;
  document.getElementById("rewind").disabled = false;
  document.getElementById("forward").disabled = false;
  // 标记就绪 + 改按钮文案
  ready.music = true;
  document.getElementById("btnPickMusic").textContent = "更换";
  updateEnterBtn();
}

/* ==============================================================
   DRAG & DROP  (Firefox / Safari fallback + 临时添加)
============================================================== */
const dz = document.getElementById("dropzone");
const folderInput = document.getElementById("folderInput") || createHiddenInput("folderInput", { webkitdirectory: "", directory: "", multiple: "" });
const imageInput  = document.getElementById("imageInput")  || createHiddenInput("imageInput",  { accept: "image/*", multiple: "" });

function createHiddenInput(id, attrs) {
  const i = document.createElement("input");
  i.type = "file"; i.id = id; i.style.display = "none";
  for (const k in attrs) i.setAttribute(k, attrs[k]);
  document.body.appendChild(i);
  return i;
}

["dragenter", "dragover"].forEach(ev => {
  dz.addEventListener(ev, e => { e.preventDefault(); dz.style.background = "rgba(255,255,255,0.75)"; });
});
["dragleave", "drop"].forEach(ev => {
  dz.addEventListener(ev, e => { e.preventDefault(); dz.style.background = ""; });
});
dz.addEventListener("drop", e => {
  const items = e.dataTransfer.items;
  if (items && items.length && items[0].webkitGetAsEntry) {
    const files = [];
    let pending = 0;
    for (const it of items) {
      const entry = it.webkitGetAsEntry?.();
      if (entry) {
        pending++;
        walkEntry(entry, files, () => { pending--; if (pending === 0) ingestDroppedFiles(files); });
      }
    }
    if (!pending) ingestDroppedFiles(files);
  } else {
    ingestDroppedFiles(e.dataTransfer.files);
  }
});

folderInput.addEventListener("change", e => ingestDroppedFiles(e.target.files));
imageInput.addEventListener("change", e => ingestDroppedFiles(e.target.files));

document.getElementById("btnPickFolder2").addEventListener("click", e => { e.stopPropagation(); folderInput.click(); });

function walkEntry(entry, files, done) {
  if (entry.isFile) {
    entry.file(f => { files.push(f); done(); });
  } else if (entry.isDirectory) {
    const reader = entry.createReader();
    const readBatch = () => {
      reader.readEntries(entries => {
        if (!entries.length) return done();
        let pending = entries.length;
        entries.forEach(en => walkEntry(en, files, () => { pending--; if (pending === 0) readBatch(); }));
      });
    };
    readBatch();
  } else { done(); }
}

function ingestDroppedFiles(fileList) {
  const files = Array.from(fileList || []);
  const imageFiles = files.filter(f => /^image\//.test(f.type) || CONFIG.IMG_EXT.test(f.name));
  if (!imageFiles.length) { toast("未找到图片文件"); return; }
  toast(`正在读取 ${imageFiles.length} 张照片…`);
  const results = [];
  let pending = imageFiles.length;
  imageFiles.forEach(f => {
    const url = URL.createObjectURL(f);
    results.push({
      file: f,
      src: url,
      title: "正在识别色彩…",  // 先占位,稍后由 analyzeAndName 替换
      originalName: f.name,    // 保留原始文件名备用
      date: f.lastModified ? new Date(f.lastModified).toLocaleDateString("zh-CN") : "未命名",
      source: "dropped"
    });
    pending--;
    if (pending === 0) finalizeIngest(results);
  });
}

function finalizeIngest(newPhotos) {
  if (!newPhotos.length) return;
  state.photos = newPhotos.concat(state.photos);
  // 先用占位标题渲染
  newPhotos.forEach(p => { if (!p.title) p.title = "正在识别色彩…"; });
  showGallery();
  renderHero();
  renderGrid();
  updateCount();
  toast(`已添加 ${newPhotos.length} 张照片`);
  // 异步分析新加入的照片
  analyzeAndName(newPhotos);
  window.scrollTo({ top: 0, behavior: "smooth" });
}

/* ==============================================================
   MUSIC PLAYER CONTROLS
============================================================== */
const audio       = document.getElementById("audio");
const playBtn     = document.getElementById("play");
const progress    = document.getElementById("progress");
const progressBar = document.getElementById("progressBar");
const curTime     = document.getElementById("curTime");
const durTime     = document.getElementById("durTime");
const cover       = document.getElementById("cover");
const player      = document.getElementById("player");

function fmtTime(s) {
  if (!isFinite(s) || s < 0) return "0:00";
  const m = Math.floor(s / 60);
  const r = Math.floor(s % 60).toString().padStart(2, "0");
  return `${m}:${r}`;
}
function setPlaying(p) {
  state.isPlaying = p;
  playBtn.textContent = p ? "❚❚" : "▶";
  cover.classList.toggle("playing", p);
  document.getElementById("trackArtist").textContent = p ? "♪ 正在播放" : "♪ 已暂停";
}

playBtn.addEventListener("click", () => {
  if (!audio.src) { toast("请先选择音乐文件"); return; }
  if (audio.paused) audio.play().then(() => setPlaying(true)).catch(() => toast("播放失败"));
  else { audio.pause(); setPlaying(false); }
});

audio.addEventListener("timeupdate", () => {
  if (!audio.duration) return;
  progressBar.style.width = (audio.currentTime / audio.duration * 100) + "%";
  curTime.textContent = fmtTime(audio.currentTime);
});
audio.addEventListener("loadedmetadata", () => durTime.textContent = fmtTime(audio.duration));
audio.addEventListener("ended", () => setPlaying(false));
audio.addEventListener("error", () => { console.warn("audio error"); toast("音乐播放出错"); });

progress.addEventListener("click", (e) => {
  if (!audio.duration) return;
  const r = progress.getBoundingClientRect();
  audio.currentTime = ((e.clientX - r.left) / r.width) * audio.duration;
});

document.getElementById("rewind").addEventListener("click", () => { audio.currentTime = Math.max(0, audio.currentTime - 10); });
document.getElementById("forward").addEventListener("click", () => { audio.currentTime = Math.min(audio.duration || 0, audio.currentTime + 10); });
document.getElementById("playerToggle").addEventListener("click", () => player.classList.toggle("collapsed"));

/* ==============================================================
   ENTRY GATE
============================================================== */
const gate = document.getElementById("gate");
function dismissGate() {
  gate.classList.add("hidden");
  setTimeout(() => gate.remove(), 800);
  // Try to play music if already loaded
  setTimeout(() => {
    if (audio.src) audio.play().then(() => setPlaying(true)).catch(() => {});
  }, 200);
}
gate.addEventListener("click", dismissGate);
document.addEventListener("keydown", e => {
  if (gate && !gate.classList.contains("hidden") && (e.key === "Enter" || e.key === " ")) {
    e.preventDefault();
    dismissGate();
  }
});

/* ==============================================================
   BUTTONS WIRING
============================================================== */
document.getElementById("btnPickFolder").addEventListener("click", onPickFolder);
document.getElementById("btnPickMusic").addEventListener("click", onPickMusic);
document.getElementById("btnAddMore").addEventListener("click", () => folderInput.click());
document.getElementById("btnChangeFolder").addEventListener("click", onPickFolder);

// "进入相册 →" 按钮: 关闭设置面板并自动开始播放
document.getElementById("btnEnter").addEventListener("click", () => {
  hideSetup();
  if (audio.src && audio.paused) {
    audio.play().then(() => setPlaying(true)).catch(() => {});
  }
  window.scrollTo({ top: 0, behavior: "smooth" });
});

// 二次通路: 点击播放器上的歌名/封面,也能更换音乐
document.getElementById("cover").addEventListener("click", () => musicInput.click());
document.getElementById("trackName").addEventListener("click", () => musicInput.click());
document.getElementById("trackName").style.cursor = "pointer";
document.getElementById("trackName").title = "点击更换音乐";

/* ==============================================================
   AUTO-RESTORE ON LOAD
============================================================== */
(async function boot() {
  // 启动 bokeh 粒子 + 初始日期章
  spawnBokeh();
  updateHeroDateStamp();

  if (!FSA_SUPPORTED) {
    document.querySelector(".setup-foot").innerHTML =
      "⚠️ 当前浏览器 <strong>不支持 File System Access API</strong>。请在主页「宥宥的足迹」区域<strong>直接拖入照片文件夹</strong>即可。<br>推荐使用 Chrome / Edge 获得完整体验。";
  }
  let photosRestored = false, musicRestored = false;
  // Try to restore photo dir
  const dirHandle = await loadHandle("photoDir");
  if (dirHandle) {
    state.dirHandle = dirHandle;
    const perm = await ensurePermission(dirHandle, "read");
    if (perm === "granted") {
      document.getElementById("photoStatus").innerHTML = '<span class="ok">✓ ' + dirHandle.name + ' · 已就绪</span>';
      document.getElementById("btnPickFolder").textContent = "更换";
      await loadPhotos();
      if (state.photos.length) {
        ready.photos = true;
        showGallery();
        photosRestored = true;
        toast(`✓ 已自动恢复 · ${state.photos.length} 张照片`);
      }
    } else {
      document.getElementById("photoStatus").innerHTML = '<span style="color:#a98">需重新授权</span>';
    }
  }
  // Try to restore music
  const stored = await loadMusicFromDB();
  if (stored && stored.blob) {
    const file = new File([stored.blob], stored.name, { type: stored.type || "audio/flac" });
    applyMusicFile(file);
    musicRestored = true;
    console.log("♪ 已自动恢复音乐:", stored.name);
  }
  updateEnterBtn();
  // 两个都已恢复,自动关闭设置面板
  if (photosRestored && musicRestored) {
    setTimeout(() => hideSetup(), 800);
  }
})();
</script>
</body>
</html>
