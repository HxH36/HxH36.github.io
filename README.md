# HxH36.github.io

<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <title>Mercedes Style Robot View + PS5 Controller</title>
  <link rel="icon" type="image/png" href="Mercedes-Logo.png">
  <meta name="viewport" content="width=device-width, initial-scale=1" />

  <!-- QR-Code Bibliothek (CDN) -->
  <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.1/build/qrcode.min.js"></script>

  <style>
    :root {
      --bg-main: #05070a;
      --bg-card: #0c1016;
      --bg-card-soft: #10151d;
      --accent: #00d0ff;
      --accent-soft: rgba(0, 208, 255, 0.2);
      --accent-strong: rgba(0, 208, 255, 0.4);
      --text-main: #f5f7fb;
      --text-soft: #a7b0c3;
      --danger: #ff3b5b;
      --success: #23d18b;
      --border-subtle: #171c25;
      --shadow-soft: 0 24px 60px rgba(0, 0, 0, 0.8);
      --radius-xl: 22px;
      --radius-lg: 16px;
      --radius-pill: 999px;
      --transition-fast: 0.2s ease-out;

      --btn-ps-cross: #4fd1ff;
      --btn-ps-circle: #ff6b81;
      --btn-ps-square: #b388ff;
      --btn-ps-triangle: #7ae582;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    html {
      scroll-behavior: smooth;
    }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: radial-gradient(circle at top left, #141b2a 0, #05070a 40%, #000 100%);
      background-size: 200% 200%;
      animation: bgShift 30s ease-in-out infinite alternate;
      color: var(--text-main);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: stretch;
      padding: 18px;
    }

    @keyframes bgShift {
      0%   { background-position: 0% 0%; }
      50%  { background-position: 50% 100%; }
      100% { background-position: 100% 0%; }
    }

    .app-shell {
      width: 100%;
      max-width: 1280px;
      border-radius: 28px;
      background: linear-gradient(145deg, rgba(17, 24, 39, 0.9), rgba(3, 7, 14, 0.98));
      border: 1px solid rgba(148, 163, 184, 0.06);
      box-shadow: var(--shadow-soft);
      display: flex;
      flex-direction: column;
      overflow: hidden;
      backdrop-filter: blur(14px);
    }

    /* simple entry animation */
    .animate-in {
      opacity: 0;
      transform: translateY(10px);
      animation: floatIn 0.7s var(--transition-fast) forwards;
    }

    .animate-delay-1 {
      animation-delay: 0.12s;
    }

    .animate-delay-2 {
      animation-delay: 0.24s;
    }

    .animate-delay-3 {
      animation-delay: 0.36s;
    }

    @keyframes floatIn {
      0% {
        opacity: 0;
        transform: translateY(12px) scale(0.99);
      }
      100% {
        opacity: 1;
        transform: translateY(0) scale(1);
      }
    }

    /* Top bar */
    .top-bar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 14px 22px;
      border-bottom: 1px solid var(--border-subtle);
      background:
        radial-gradient(circle at top left, rgba(0, 208, 255, 0.18), transparent 55%),
        radial-gradient(circle at bottom right, rgba(15, 23, 42, 0.9), transparent 60%);
    }

    .brand-group { display: flex; align-items: center; gap: 12px; }

    .brand-ring {
      width: 32px; height: 32px;
      border-radius: 999px;
      border: 1px solid var(--accent);
      display: flex; align-items: center; justify-content: center;
      position: relative;
      box-shadow: 0 0 18px rgba(0, 208, 255, 0.5);
      overflow: hidden;
    }

    .brand-ring::before,
    .brand-ring::after {
      content: "";
      position: absolute;
      border-radius: inherit;
      border: 1px solid rgba(0, 208, 255, 0.35);
      inset: 3px;
    }
    .brand-ring::after { inset: 6px; }

    .brand-ring span {
      position: absolute; inset: 0;
      background:
        linear-gradient(120deg, transparent 40%, rgba(0, 208, 255, 0.3) 60%, transparent 80%);
      mix-blend-mode: screen;
      animation: sweep 2.4s linear infinite;
      opacity: 0.7;
    }

    .brand-dot {
      width: 5px; height: 5px;
      border-radius: 50%;
      background: var(--accent);
      position: relative;
      z-index: 1;
    }

    @keyframes sweep {
      0% { transform: translateX(-100%); }
      100% { transform: translateX(100%); }
    }

    .brand-text-main {
      font-size: 0.95rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--text-soft);
    }

    .brand-text-sub {
      font-size: 0.78rem;
      color: var(--accent);
      letter-spacing: 0.18em;
      text-transform: uppercase;
      opacity: 0.85;
    }

    .status-group {
      display: flex;
      align-items: center;
      gap: 12px;
      font-size: 0.78rem;
      color: var(--text-soft);
    }

    .status-pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 4px 10px;
      border-radius: var(--radius-pill);
      background: rgba(15, 23, 42, 0.8);
      border: 1px solid rgba(148, 163, 184, 0.2);
      box-shadow: 0 0 10px rgba(0, 208, 255, 0.5);
    }

    .status-dot {
      width: 8px; height: 8px;
      border-radius: 50%;
      background: #22c55e;
      box-shadow: 0 0 12px rgba(34, 197, 94, 0.9);
      animation: statusPulse 1.6s ease-in-out infinite;
    }

    @keyframes statusPulse {
      0%, 100% { transform: scale(1); }
      50%      { transform: scale(1.2); }
    }

    .status-label {
      text-transform: uppercase;
      letter-spacing: 0.16em;
      font-size: 0.72rem;
    }

    .battery-badge {
      padding: 4px 10px;
      border-radius: var(--radius-pill);
      border: 1px solid rgba(148, 163, 184, 0.2);
      background: rgba(15, 23, 42, 0.9);
      display: inline-flex;
      align-items: center;
      gap: 6px;
      position: relative;
      overflow: hidden;
    }

    .battery-badge::after {
      content: "";
      position: absolute; inset: 0;
      background: linear-gradient(120deg, transparent 40%, rgba(148, 163, 184, 0.25) 50%, transparent 60%);
      opacity: 0.6;
      pointer-events: none;
      animation: batteryShine 5s linear infinite;
    }

    @keyframes batteryShine {
      0%   { transform: translateX(-120%); }
      40%  { transform: translateX(120%); }
      100% { transform: translateX(120%); }
    }

    .battery-bar {
      width: 40px; height: 8px;
      border-radius: 999px;
      border: 1px solid rgba(148, 163, 184, 0.5);
      padding: 1px;
      overflow: hidden;
    }

    .battery-fill {
      height: 100%;
      width: 78%;
      border-radius: 999px;
      background: linear-gradient(90deg, #22c55e, #bef264);
      transition: width 0.4s ease-out;
    }

    /* Layout main area */
    .main {
      display: grid;
      grid-template-columns: minmax(0, 3fr) minmax(0, 1.5fr);
      gap: 18px;
      padding: 18px 22px 22px;
    }

    /* linke Spalte = Kamera + Systemlog */
    .left-column {
      display: flex;
      flex-direction: column;
      gap: 14px;
    }

    @media (max-width: 900px) {
      .main {
        grid-template-columns: minmax(0, 1fr);
      }

      .left-column {
        order: 1;
      }

      .side-column {
        order: 2;
      }
    }

    /* Cards */
    .card {
      background: radial-gradient(circle at top, rgba(15, 23, 42, 0.9), #020617 70%);
      border-radius: var(--radius-xl);
      border: 1px solid var(--border-subtle);
      padding: 14px 14px 16px;
      display: flex;
      flex-direction: column;
      gap: 12px;
      position: relative;
      overflow: hidden;
    }

    .card::before {
      content: "";
      position: absolute;
      inset: -30%;
      background: radial-gradient(circle at 10% 0%, rgba(0, 208, 255, 0.18), transparent 55%);
      opacity: 0.7;
      pointer-events: none;
    }

    .card-header {
      display: flex;
      align-items: baseline;
      justify-content: space-between;
      gap: 12px;
      position: relative;
      z-index: 1;
    }

    .card-title {
      font-size: 0.88rem;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-soft);
    }

    .card-subtitle {
      font-size: 0.7rem;
      color: var(--accent);
      text-transform: uppercase;
      letter-spacing: 0.18em;
    }

    .chips {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
    }

    .chip {
      font-size: 0.7rem;
      text-transform: uppercase;
      letter-spacing: 0.12em;
      padding: 4px 9px;
      border-radius: var(--radius-pill);
      border: 1px solid rgba(148, 163, 184, 0.2);
      background: rgba(15, 23, 42, 0.95);
      color: var(--text-soft);
      display: inline-flex;
      align-items: center;
      gap: 6px;
      position: relative;
      overflow: hidden;
    }

    .chip::after {
      content: "";
      position: absolute;
      inset: 0;
      background: linear-gradient(120deg, transparent 0%, rgba(148, 163, 184, 0.25) 50%, transparent 100%);
      opacity: 0;
      transform: translateX(-40%);
      transition: opacity 0.4s ease, transform 0.4s ease;
    }

    .chip:hover::after {
      opacity: 1;
      transform: translateX(40%);
    }

    .chip-dot {
      width: 6px; height: 6px;
      border-radius: 50%;
      background: var(--accent);
      box-shadow: 0 0 10px rgba(0, 208, 255, 0.9);
    }

    /* Camera viewport */
    .camera-shell {
      position: relative;
      border-radius: 20px;
      background: radial-gradient(circle at center, #020617, #000);
      border: 1px solid #020617;
      overflow: hidden;
      width: 100%;
      aspect-ratio: 16 / 9;
      display: flex;
      animation: cameraGlow 8s ease-in-out infinite;
    }

    @keyframes cameraGlow {
      0%,100% {
        box-shadow:
          0 0 0 0 rgba(0, 208, 255, 0.0),
          0 24px 40px rgba(0, 0, 0, 0.9);
      }
      50% {
        box-shadow:
          0 0 25px 0 rgba(0, 208, 255, 0.45),
          0 24px 50px rgba(0, 0, 0, 0.95);
      }
    }

    .camera-shell::before {
      content: "";
      position: absolute;
      inset: 0;
      border-radius: inherit;
      border: 1px solid rgba(148, 163, 184, 0.18);
      pointer-events: none;
    }

    .camera-shell::after {
      content: "";
      position: absolute;
      inset: 10px;
      border-radius: 16px;
      --corner: 18px;
      background:
        linear-gradient(to right, var(--accent-soft), transparent) 0 0 / var(--corner) 2px no-repeat,
        linear-gradient(to right, var(--accent-soft), transparent) 0 100% / var(--corner) 2px no-repeat,
        linear-gradient(to left, var(--accent-soft), transparent) 100% 0 / var(--corner) 2px no-repeat,
        linear-gradient(to left, var(--accent-soft), transparent) 100% 100% / var(--corner) 2px no-repeat,
        linear-gradient(to bottom, var(--accent-soft), transparent) 0 0 / 2px var(--corner) no-repeat,
        linear-gradient(to bottom, var(--accent-soft), transparent) 100% 0 / 2px var(--corner) no-repeat,
        linear-gradient(to top, var(--accent-soft), transparent) 0 100% / 2px var(--corner) no-repeat,
        linear-gradient(to top, var(--accent-soft), transparent) 100% 100% / 2px var(--corner) no-repeat;
      opacity: 0.8;
      pointer-events: none;
      box-shadow: 0 0 20px rgba(0, 208, 255, 0.4);
    }

    .camera-hud {
      position: absolute;
      inset: 0;
      background-image:
        linear-gradient(to right, rgba(148, 163, 184, 0.13) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(148, 163, 184, 0.12) 1px, transparent 1px);
      background-size: 60px 60px;
      mix-blend-mode: soft-light;
      opacity: 0.35;
      pointer-events: none;
      z-index: 2;
    }

    .camera-inner-glow {
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at center, rgba(15, 23, 42, 0.9), transparent 60%);
      mix-blend-mode: screen;
      opacity: 0.85;
      pointer-events: none;
      z-index: 1;
    }

    .camera-video-wrapper {
      position: relative;
      z-index: 2;
      width: 100%;
      display: flex;
    }

    img.stream {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      background: radial-gradient(circle at center, #020617, #000);
    }

    .camera-overlay {
      position: absolute;
      inset: 0;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      padding: 10px 12px;
      pointer-events: none;
      z-index: 3;
    }

    .camera-overlay-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 8px;
    }

    .glass-pill {
      pointer-events: auto;
      background: linear-gradient(
        135deg,
        rgba(15, 23, 42, 0.96),
        rgba(15, 23, 42, 0.5)
      );
      border-radius: var(--radius-pill);
      border: 1px solid rgba(148, 163, 184, 0.55);
      padding: 4px 10px;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      backdrop-filter: blur(12px);
      font-size: 0.68rem;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-soft);
      box-shadow: 0 0 16px rgba(0, 0, 0, 0.7);
    }

    .rec-dot {
      width: 9px; height: 9px;
      border-radius: 50%;
      background: var(--danger);
      box-shadow: 0 0 14px rgba(248, 113, 113, 0.9);
      animation: pulse 1s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); opacity: 0.7; }
      50% { transform: scale(1.35); opacity: 1; }
    }

    .glass-pill strong {
      color: var(--text-main);
      font-weight: 600;
    }

    .glass-tag {
      pointer-events: none;
      font-size: 0.65rem;
      padding: 4px 8px;
      border-radius: var(--radius-pill);
      border: 1px solid rgba(148, 163, 184, 0.3);
      background: radial-gradient(circle at top, rgba(15, 23, 42, 0.96), rgba(15, 23, 42, 0.6));
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--text-soft);
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .glass-tag::before {
      content: "";
      width: 7px; height: 7px;
      border-radius: 999px;
      border: 2px solid var(--accent);
      box-shadow: 0 0 10px rgba(0, 208, 255, 0.7);
    }

    .controls {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      pointer-events: auto;
    }

    .btn {
      border: 1px solid rgba(148, 163, 184, 0.5);
      border-radius: var(--radius-pill);
      background: radial-gradient(circle at top left, rgba(0, 208, 255, 0.16), rgba(15, 23, 42, 0.96));
      padding: 7px 14px;
      font-size: 0.74rem;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--text-main);
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      outline: none;
      transition: transform var(--transition-fast), box-shadow var(--transition-fast), border-color var(--transition-fast), background 0.2s;
      box-shadow: 0 0 14px rgba(15, 23, 42, 0.9);
    }

    .btn-icon {
      width: 9px; height: 9px;
      border-radius: 2px;
      border: 1px solid var(--accent);
      box-shadow: 0 0 10px rgba(0, 208, 255, 0.8);
    }

    .btn:hover {
      transform: translateY(-1px) scale(1.01);
      box-shadow: 0 0 20px rgba(0, 208, 255, 0.6);
      border-color: var(--accent);
      background: radial-gradient(circle at top left, rgba(0, 208, 255, 0.23), rgba(15, 23, 42, 0.96));
    }

    .btn:active {
      transform: translateY(0) scale(0.99);
      box-shadow: 0 0 12px rgba(0, 208, 255, 0.5);
    }

    .btn.secondary {
      background: radial-gradient(circle at top right, rgba(15, 23, 42, 0.96), rgba(15, 23, 42, 1));
      border-color: rgba(148, 163, 184, 0.45);
      color: var(--text-soft);
    }

    .btn.secondary .btn-icon {
      border-color: rgba(148, 163, 184, 0.7);
      box-shadow: 0 0 8px rgba(148, 163, 184, 0.8);
    }

    .timer {
      font-size: 0.76rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--text-soft);
      opacity: 0.9;
    }

    .timer span { color: var(--accent); }

    .camera-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
      position: relative;
      z-index: 2;
    }

    .side-column { display: flex; flex-direction: column; gap: 14px; }

    .side-card {
      background: linear-gradient(150deg, rgba(15, 23, 42, 0.96), #020617);
      border-radius: var(--radius-lg);
      border: 1px solid var(--border-subtle);
      padding: 12px 14px;
      position: relative;
      overflow: hidden;
    }

    .side-card::before {
      content: "";
      position: absolute;
      inset: -30%;
      background: radial-gradient(circle at 110% -10%, rgba(0, 208, 255, 0.22), transparent 55%);
      opacity: 0.6;
      pointer-events: none;
    }

    .side-title {
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 0.18em;
      color: var(--text-soft);
      margin-bottom: 8px;
    }

    .telemetry-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 8px;
      font-size: 0.78rem;
      position: relative;
      z-index: 1;
    }

    .telemetry-item {
      background: radial-gradient(circle at top, #020617, #020617);
      border-radius: 12px;
      border: 1px solid rgba(30, 64, 175, 0.7);
      padding: 8px 9px;
      display: flex;
      flex-direction: column;
      gap: 3px;
      box-shadow: 0 0 18px rgba(15, 23, 42, 0.9);
      position: relative;
      overflow: hidden;
      transition: transform 0.18s ease-out, box-shadow 0.18s ease-out, border-color 0.18s ease-out;
    }

    .telemetry-item::after {
      content: "";
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at top right, rgba(0, 208, 255, 0.16), transparent 60%);
      opacity: 0.9;
      pointer-events: none;
    }

    .telemetry-item:hover {
      transform: translateY(-2px);
      border-color: rgba(56, 189, 248, 0.9);
      box-shadow: 0 0 22px rgba(56, 189, 248, 0.4);
    }

    .telemetry-label {
      font-size: 0.68rem;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      color: var(--text-soft);
      position: relative;
      z-index: 1;
    }

    .telemetry-value {
      font-size: 0.92rem;
      font-weight: 500;
      color: var(--text-main);
      position: relative;
      z-index: 1;
      display: flex;
      align-items: baseline;
      gap: 4px;
    }

    .telemetry-unit { font-size: 0.7rem; color: var(--text-soft); }

    .telemetry-sub {
      font-size: 0.7rem;
      color: var(--accent);
      opacity: 0.9;
      position: relative;
      z-index: 1;
    }

    .hint-text {
      margin-top: 6px;
      font-size: 0.75rem;
      color: var(--text-soft);
      position: relative;
      z-index: 1;
    }

    .hint-text code {
      font-size: 0.72rem;
      padding: 2px 5px;
      border-radius: 6px;
      background: rgba(15, 23, 42, 0.9);
      border: 1px solid rgba(148, 163, 184, 0.25);
      color: var(--accent);
    }

    .log-list {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 4px;
      font-size: 0.76rem;
      position: relative;
      z-index: 1;
      max-height: 130px;
      overflow-y: auto;
    }

    .log-item {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      padding: 4px 0;
      border-bottom: 1px dashed rgba(30, 64, 175, 0.6);
      animation: logIn 0.25s ease-out;
      transform-origin: left;
    }

    @keyframes logIn {
      0% {
        opacity: 0;
        transform: translateY(4px);
      }
      100% {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .log-label { color: var(--text-soft); }
    .log-value { color: var(--accent); text-align: right; }

    .bottom-fade {
      height: 10px;
      margin-top: 4px;
      background: linear-gradient(90deg, transparent, var(--accent-soft), transparent);
      opacity: 0.6;
      border-radius: 999px;
    }

    /* ========= PS5 CONTROLLER CARD ========= */

    .controller-shell {
      margin-top: 6px;
      background: radial-gradient(circle at top, #020617, #020617 60%, #000 100%);
      border-radius: 20px;
      border: 1px solid rgba(15, 23, 42, 0.9);
      padding: 14px 12px 10px;
      position: relative;
      box-shadow: 0 18px 40px rgba(0, 0, 0, 0.7);
      overflow: hidden;
    }

    .controller-shell::before {
      content: "";
      position: absolute;
      inset: 0;
      border-radius: inherit;
      background: radial-gradient(circle at 50% -20%, rgba(0, 208, 255, 0.25), transparent 60%);
      opacity: 0.9;
      pointer-events: none;
    }

    .controller-top-row {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      margin-bottom: 10px;
      position: relative;
      z-index: 1;
    }

    .controller-status {
      font-size: 0.7rem;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      color: var(--text-soft);
    }

    .controller-status span { color: var(--accent); }

    .controller-last-btn {
      font-size: 0.72rem;
      color: var(--text-soft);
      text-align: right;
    }

    .controller-last-btn strong { color: var(--text-main); }

    .controller-body {
      position: relative;
      width: 100%;
      aspect-ratio: 5 / 2;
      margin: 0 auto;
    }

    .controller-base-center {
      position: absolute;
      left: 10%; right: 10%;
      top: 24%; bottom: 32%;
      border-radius: 60px;
      background: radial-gradient(circle at top, #ffffff, #e5e7eb);
      box-shadow:
        0 0 0 1px rgba(15, 23, 42, 0.6),
        0 18px 35px rgba(0, 0, 0, 0.9);
    }

    .controller-base-center::after {
      content: "";
      position: absolute;
      left: 25%; right: 25%;
      top: 40%; bottom: -25%;
      border-radius: 40px 40px 70px 70px;
      background: radial-gradient(circle at top, #111827, #020617);
      box-shadow:
        0 0 0 1px rgba(15, 23, 42, 0.8),
        0 12px 24px rgba(0, 0, 0, 0.9);
    }

    .controller-grip {
      position: absolute;
      top: 36%;
      width: 30%; height: 60%;
      border-radius: 80% 40% 80% 40%;
      background: radial-gradient(circle at 20% 10%, #ffffff, #e5e7eb);
      box-shadow:
        0 0 0 1px rgba(15, 23, 42, 0.5),
        0 18px 35px rgba(0, 0, 0, 0.9);
      overflow: hidden;
    }

    .controller-grip.left  { left: 0%;  transform: rotate(-8deg); }
    .controller-grip.right { right: 0%; transform: scaleX(-1) rotate(-8deg); }

    .controller-grip::after {
      content: "";
      position: absolute;
      left: 5%; right: -10%;
      bottom: -5%;
      height: 55%;
      border-radius: 70% 40% 80% 60%;
      background: radial-gradient(circle at 30% 0, #111827, #020617);
    }

    .controller-touchpad {
      position: absolute;
      left: 32%; right: 32%;
      top: 20%; height: 26%;
      border-radius: 18px;
      background: radial-gradient(circle at top, #111827, #020617);
      box-shadow:
        0 0 0 1px rgba(30, 64, 175, 0.8),
        inset 0 0 10px rgba(0, 0, 0, 0.9);
      overflow: hidden;
      pointer-events: none;
    }

    .controller-touchpad::before {
      content: "";
      position: absolute; inset: 0;
      background-image:
        radial-gradient(circle at 0 0, rgba(148, 163, 184, 0.2) 1px, transparent 0);
      background-size: 6px 6px;
      opacity: 0.5;
    }

    .controller-touchpad::after {
      content: "";
      position: absolute;
      left: 10%; right: 10%;
      top: -16%; height: 10px;
      border-radius: 999px;
      background: linear-gradient(90deg, rgba(59, 130, 246, 0.8), rgba(56, 189, 248, 0.8));
      box-shadow:
        0 0 10px rgba(56, 189, 248, 0.9),
        0 0 20px rgba(37, 99, 235, 0.9);
    }

    .controller-touchpad.active {
      box-shadow:
        0 0 0 1px rgba(0, 208, 255, 0.9),
        0 0 25px rgba(0, 208, 255, 0.9),
        inset 0 0 14px rgba(15, 23, 42, 0.9);
    }

    .controller-button {
      position: absolute;
      border-radius: 999px;
      background: radial-gradient(circle at 30% 20%, #1f2937, #020617);
      border: 1px solid rgba(15, 23, 42, 0.9);
      box-shadow:
        0 6px 10px rgba(0, 0, 0, 0.8),
        inset 0 0 0 1px rgba(148, 163, 184, 0.15);
      display: flex; align-items: center; justify-content: center;
      font-size: 0.7rem;
      color: var(--text-soft);
      transition: box-shadow 0.08s ease-out, background 0.08s, color 0.08s, transform 0.08s;
      z-index: 3;
    }

    .controller-button.small { font-size: 0.62rem; }
    .controller-button.face  { width: 14%; height: 22%; }

    .controller-button.stick {
      width: 16%; height: 28%;
      border-radius: 50%;
      box-shadow:
        0 10px 16px rgba(0, 0, 0, 0.85),
        inset 0 0 0 1px rgba(148, 163, 184, 0.15);
      position: absolute;
      overflow: visible;
      z-index: 10;
    }

    .stick-nub {
      position: absolute;
      inset: 30%;
      border-radius: 50%;
      background: radial-gradient(circle at 30% 20%, #111827, #020617);
      box-shadow:
        0 0 0 1px rgba(148, 163, 184, 0.6),
        0 4px 8px rgba(0, 0, 0, 0.8);
      transform: translate(var(--dx, 0%), var(--dy, 0%));
      transition: transform 0.03s linear;
    }

    .controller-button.trigger { width: 18%; height: 14%; }
    .controller-button.dpad    { width: 12%; height: 18%; }
    .controller-button.center  { width: 8%; height: 14%; font-size: 0.6rem; }

    .controller-button.active {
      background: radial-gradient(circle at 30% 20%, rgba(0, 208, 255, 0.3), #020617);
      box-shadow:
        0 0 0 1px rgba(0, 208, 255, 0.6),
        0 0 16px rgba(0, 208, 255, 0.9),
        inset 0 0 0 1px rgba(15, 23, 42, 0.9);
      color: #e5faff;
    }

    .controller-button.active:not(.btn-ps):not(.btn-triangle) {
      transform: translateY(1px) scale(0.99);
      animation: btnPulse 0.22s ease-out;
    }

    @keyframes btnPulse {
      0%   { transform: scale(1); }
      40%  { transform: scale(0.96); }
      100% { transform: scale(0.99); }
    }

    .controller-button .label { position: relative; z-index: 1; }

    .btn-cross .label   { color: var(--btn-ps-cross);   font-size: 1rem; }
    .btn-circle .label  { color: var(--btn-ps-circle);  font-size: 1rem; }
    .btn-square .label  { color: var(--btn-ps-square);  font-size: 1rem; }
    .btn-triangle .label{ color: var(--btn-ps-triangle);font-size: 1rem; }

    .controller-button.active.btn-cross .label,
    .controller-button.active.btn-circle .label,
    .controller-button.active.btn-square .label,
    .controller-button.active.btn-triangle .label {
      color: #e5faff;
    }

    .btn-cross    { right: 10%; top: 60%; }
    .btn-circle   { right:  4%; top: 46%; }
    .btn-square   { right: 16%; top: 46%; }
    .btn-triangle { right: 10%; top: 32%; }

    .btn-l3 { left: 23%; top: 63%; }
    .btn-r3 { right: 23%; top: 63%; }

    .btn-du { left: 11%; top: 32%; }
    .btn-dd { left: 11%; top: 58%; }
    .btn-dl { left:  3%; top: 45%; }
    .btn-dr { left: 19%; top: 45%; }

    .btn-l1 { left: 22%; top: 10%; }
    .btn-r1 { right: 22%; top: 10%; }
    .btn-l2 { left: 10%; top: 4%; }
    .btn-r2 { right: 10%; top: 4%; }

    .btn-share   { left: 37%; top: 30%; }
    .btn-options { right: 37%; top: 30%; }

    .btn-ps      { left: 50%; top: 46%; transform: translateX(-50%); }
    .btn-ps .label { font-size: 0.75rem; }

    .btn-ps.controller-button.active {
      transform: translateX(-50%) !important;
      animation: none !important;
    }

    .controller-footer-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
      font-size: 0.68rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--text-soft);
      position: relative;
      z-index: 1;
    }

    .controller-footer-row span { color: var(--accent); }

    .controller-active {
      margin-top: 6px;
      font-size: 0.7rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--text-soft);
    }

    .controller-active span { color: var(--accent); }

    /* ==== QR MODAL ==== */

    .qr-modal {
      position: fixed;
      inset: 0;
      background: rgba(3, 7, 18, 0.86);
      backdrop-filter: blur(10px);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 999;
    }

    .qr-modal-inner {
      background: radial-gradient(circle at top, #020617, #020617 60%, #000 100%);
      border-radius: 24px;
      border: 1px solid rgba(148, 163, 184, 0.4);
      padding: 20px 22px 16px;
      max-width: 360px;
      width: 90%;
      box-shadow: 0 30px 80px rgba(0, 0, 0, 0.85);
      text-align: center;
      position: relative;
    }

    .qr-modal-title {
      font-size: 0.9rem;
      text-transform: uppercase;
      letter-spacing: 0.18em;
      color: var(--text-soft);
      margin-bottom: 10px;
    }

    .qr-modal-sub {
      font-size: 0.8rem;
      color: var(--text-soft);
      margin-bottom: 12px;
    }

    .qr-canvas-wrap {
      display: inline-flex;
      padding: 10px;
      border-radius: 20px;
      background: radial-gradient(circle at top, rgba(15, 23, 42, 0.96), rgba(15, 23, 42, 0.8));
      border: 1px solid rgba(148, 163, 184, 0.6);
      margin-bottom: 10px;
    }

    #qr-canvas {
      width: 220px;
      height: 220px;
    }

    .qr-close {
      margin-top: 8px;
      font-size: 0.75rem;
      cursor: pointer;
      color: var(--accent);
      text-transform: uppercase;
      letter-spacing: 0.16em;
    }

    .qr-close:hover {
      text-decoration: underline;
    }

    /* ========= MOBILE-SHELL (nur Kamera + Push-To-Talk) ========= */

    .mobile-shell {
      display: none;
      width: 100%;
      max-width: 600px;
      margin: 0 auto;
      flex-direction: column;
      align-items: stretch;
      justify-content: flex-start;
    }

    .mobile-shell-inner {
      display: flex;
      flex-direction: column;
      height: 100vh;
      background: #020617;
    }

    .mobile-header {
      padding: 10px 14px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom: 1px solid rgba(15, 23, 42, 0.9);
    }

    .mobile-header-title {
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 0.18em;
      color: var(--text-soft);
    }

    .mobile-main {
      flex: 1;
      display: flex;
      flex-direction: column;
    }

    .mobile-video {
      flex: 1;
      position: relative;
      background: #000;
    }

    .mobile-video img {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .mobile-footer {
      padding: 10px 14px 14px;
      border-top: 1px solid rgba(15, 23, 42, 0.9);
      background: radial-gradient(circle at top, #020617, #020617 60%, #000 100%);
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .ptt-btn {
      border-radius: 999px;
      padding: 12px 16px;
      border: 1px solid rgba(248, 113, 113, 0.8);
      background: radial-gradient(circle at top, rgba(248, 113, 113, 0.3), #020617);
      color: #fecaca;
      font-size: 0.9rem;
      text-transform: uppercase;
      letter-spacing: 0.18em;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      cursor: pointer;
    }

    .ptt-btn.active {
      background: radial-gradient(circle at top, rgba(34, 197, 94, 0.35), #022c22);
      border-color: rgba(34, 197, 94, 0.9);
      color: #bbf7d0;
    }

    .ptt-dot {
      width: 12px;
      height: 12px;
      border-radius: 999px;
      background: #f87171;
      box-shadow: 0 0 16px rgba(248, 113, 113, 0.9);
    }

    .ptt-btn.active .ptt-dot {
      background: #22c55e;
      box-shadow: 0 0 16px rgba(34, 197, 94, 0.9);
    }

    .ptt-info {
      font-size: 0.75rem;
      color: var(--text-soft);
    }

    .ptt-text {
      font-size: 0.8rem;
      color: var(--accent);
      min-height: 1.3em;
    }
  </style>
</head>
<body>
  <div class="app-shell">
    <header class="top-bar animate-in">
      <div class="brand-group">
        <div class="brand-ring">
          <span></span>
          <div class="brand-dot"></div>
        </div>
        <div>
          <div class="brand-text-main">GIBI VISION</div>
          <div class="brand-text-sub">Mercedes-Benz Cockpit</div>
        </div>
      </div>

      <div class="status-group">
        <div class="status-pill">
          <span class="status-dot"></span>
          <span class="status-label">Live Connected</span>
        </div>

        <div class="battery-badge">
          <span style="font-size:0.72rem;letter-spacing:0.14em;text-transform:uppercase;">Battery</span>
          <div class="battery-bar"><div class="battery-fill" id="battery-fill"></div></div>
          <span style="font-size:0.8rem;" id="battery-text">78%</span>
        </div>

        <!-- NEUER BUTTON: QR-Code für Handy -->
        <button class="btn secondary" id="open-qr-btn">
          <span class="btn-icon"></span>
          <span>Auf Handy öffnen</span>
        </button>
      </div>
    </header>

    <main class="main">
      <!-- Linke Spalte: Kamera + System Log -->
      <div class="left-column">
        <!-- Kamera -->
        <section class="card animate-in animate-delay-1">
          <div class="card-header">
            <div>
              <div class="card-title">Exterior Vision</div>
              <div class="card-subtitle">live camera feed</div>
            </div>
            <div class="chips">
              <div class="chip"><span class="chip-dot"></span> 640 × 480</div>
              <div class="chip">Faces + Gestures</div>
            </div>
          </div>

          <div class="camera-shell">
            <div class="camera-inner-glow"></div>
            <div class="camera-hud"></div>

            <div class="camera-video-wrapper">
              <!-- Desktop -->
<img class="stream" src="http://localhost:8000/video" alt="Robot Live Stream" />

            </div>

            <div class="camera-overlay">
              <div class="camera-overlay-top">
                <div class="glass-pill">
                  <span class="rec-dot"></span>
                  <span>Recording</span>
                  <strong>Live</strong>
                </div>
                <div class="glass-tag">Hand Gesture Control</div>
              </div>
            </div>
          </div>

          <div class="camera-footer">
            <div class="controls">
              <button class="btn" onclick="location.reload()">
                <span class="btn-icon"></span>
                <span>Refresh</span>
              </button>
              <button class="btn secondary" onclick="document.querySelector('.camera-shell').requestFullscreen?.()">
                <span class="btn-icon"></span>
                <span>Full Screen</span>
              </button>
            </div>
            <div class="timer">
              Uptime <span id="uptime-text">00:00:00</span>
            </div>
          </div>
        </section>

        <!-- System log unter der Kamera -->
        <section class="side-card animate-in animate-delay-2">
          <div class="side-title">System log</div>
          <ul class="log-list" id="log-list">
            <li class="log-item">
              <span class="log-label">00:00:00</span>
              <span class="log-value">Dashboard geladen</span>
            </li>
          </ul>
          <div class="bottom-fade"></div>
        </section>
      </div>

      <!-- Rechte Seite: Vehicle status + Controller -->
      <aside class="side-column">
        <section class="side-card animate-in animate-delay-1">
          <div class="side-title">Vehicle status</div>
          <div class="telemetry-grid">
            <div class="telemetry-item">
              <div class="telemetry-label">Speed</div>
              <div class="telemetry-value">
                <span id="telemetry-speed">0.0</span>
                <span class="telemetry-unit">m/s</span>
              </div>
              <div class="telemetry-sub" id="telemetry-speed-mode">Comfort Mode</div>
            </div>
            <div class="telemetry-item">
              <div class="telemetry-label">Temperature</div>
              <div class="telemetry-value">
                <span id="telemetry-temp">32.4</span>
                <span class="telemetry-unit">°C</span>
              </div>
              <div class="telemetry-sub">Body</div>
            </div>
            <div class="telemetry-item">
              <div class="telemetry-label">Network</div>
              <div class="telemetry-value">
                <span id="telemetry-network">-52</span>
                <span class="telemetry-unit">dBm</span>
              </div>
              <div class="telemetry-sub" id="telemetry-network-sub">Wi-Fi Link</div>
            </div>
            <div class="telemetry-item">
              <div class="telemetry-label">Mode</div>
              <div class="telemetry-value">
                <span id="telemetry-mode">Remote</span>
              </div>
              <div class="telemetry-sub" id="telemetry-mode-sub">Operator control</div>
            </div>
          </div>
          <p class="hint-text">
            Stream-Quelle:
            <code>http://localhost:8000/video</code>
          </p>
          <div class="bottom-fade"></div>
        </section>

        <!-- PS5 CONTROLLER -->
        <section class="side-card animate-in animate-delay-2">
          <div class="side-title">PS Controller Input</div>

          <div class="controller-shell">
            <div class="controller-top-row">
              <div class="controller-status" id="controller-status">
                Controller: <span>nicht verbunden</span>
              </div>
              <div class="controller-last-btn" id="controller-last-btn">
                Letzte Taste: <strong>-</strong>
              </div>
            </div>

            <div class="controller-body">
              <div class="controller-base-center"></div>
              <div class="controller-grip left"></div>
              <div class="controller-grip right"></div>

              <div class="controller-touchpad" data-btn-id="btn-touchpad"></div>

              <!-- Face Buttons -->
              <div class="controller-button face btn-cross" data-btn-id="btn-cross">
                <span class="label">✕</span>
              </div>
              <div class="controller-button face btn-circle" data-btn-id="btn-circle">
                <span class="label">○</span>
              </div>
              <div class="controller-button face btn-square" data-btn-id="btn-square">
                <span class="label">□</span>
              </div>
              <div class="controller-button face btn-triangle" data-btn-id="btn-triangle">
                <span class="label">△</span>
              </div>

              <!-- Sticks -->
              <div class="controller-button stick btn-l3" data-btn-id="btn-l3">
                <div class="stick-nub" id="stick-l"></div>
              </div>
              <div class="controller-button stick btn-r3" data-btn-id="btn-r3">
                <div class="stick-nub" id="stick-r"></div>
              </div>

              <!-- D-Pad -->
              <div class="controller-button dpad btn-du small" data-btn-id="btn-du">
                <span class="label">▲</span>
              </div>
              <div class="controller-button dpad btn-dd small" data-btn-id="btn-dd">
                <span class="label">▼</span>
              </div>
              <div class="controller-button dpad btn-dl small" data-btn-id="btn-dl">
                <span class="label">◀</span>
              </div>
              <div class="controller-button dpad btn-dr small" data-btn-id="btn-dr">
                <span class="label">▶</span>
              </div>

              <!-- L1 / R1 -->
              <div class="controller-button trigger btn-l1 small" data-btn-id="btn-l1">
                <span class="label">L1</span>
              </div>
              <div class="controller-button trigger btn-r1 small" data-btn-id="btn-r1">
                <span class="label">R1</span>
              </div>

              <!-- L2 / R2 -->
              <div class="controller-button trigger btn-l2 small" data-btn-id="btn-l2">
                <span class="label">L2</span>
              </div>
              <div class="controller-button trigger btn-r2 small" data-btn-id="btn-r2">
                <span class="label">R2</span>
              </div>

              <!-- Share / Options / PS -->
              <div class="controller-button center btn-share small" data-btn-id="btn-share">
                <span class="label">SHARE</span>
              </div>
              <div class="controller-button center btn-options small" data-btn-id="btn-options">
                <span class="label">OPTIONS</span>
              </div>
              <div class="controller-button center btn-ps small" data-btn-id="btn-ps">
                <span class="label">PS</span>
              </div>
            </div>

            <div class="controller-footer-row">
              <div>Gamepad-API: <span id="controller-api-state">bereit</span></div>
              <div>Mapping: <span>PlayStation (Standard)</span></div>
            </div>
            <div class="controller-active" id="controller-active">
              Aktive Tasten: <span>–</span>
            </div>
          </div>
        </section>
      </aside>
    </main>
  </div>

  <!-- MOBILE SHELL: wird genutzt, wenn ?mobile=1 in der URL steht -->
  <div id="mobile-shell" class="mobile-shell">
    <div class="mobile-shell-inner">
      <div class="mobile-header">
        <div class="mobile-header-title">GIBI VISION · Mobile</div>
        <div style="font-size:0.7rem;color:#9ca3af;">Push-to-Talk</div>
      </div>
      <div class="mobile-main">
        <div class="mobile-video">
          <!-- Desktop -->
<img class="stream" src="http://localhost:8000/video" alt="Robot Live Stream" />


        </div>
      </div>
      <div class="mobile-footer">
        <button id="ptt-btn" class="ptt-btn">
          <span class="ptt-dot"></span>
          <span id="ptt-label">Gedrückt halten & sprechen</span>
        </button>
        <div class="ptt-info">
          Halte den Button gedrückt (oder lange antippen), sprich ins Handy-Mikrofon.  
          Der Text wird unten angezeigt und kann von der Web-App weiterverarbeitet werden.
        </div>
        <div class="ptt-text" id="ptt-text"></div>
      </div>
    </div>
  </div>

  <!-- QR MODAL -->
  <div id="qr-modal" class="qr-modal">
    <div class="qr-modal-inner">
      <div class="qr-modal-title">Auf Handy öffnen</div>
      <div class="qr-modal-sub">
        Scanne diesen QR-Code mit der Handy-Kamera, um die mobile Ansicht
        (nur Kamera + Push-to-Talk) zu öffnen.
      </div>
      <div class="qr-canvas-wrap">
        <canvas id="qr-canvas"></canvas>
      </div>
      <div class="qr-modal-sub" style="font-size:0.7rem;">
        Link kodiert: <span id="qr-url" style="color:var(--accent);word-break:break-all;"></span>
      </div>
      <div class="qr-close" id="qr-close">Schließen</div>
    </div>
  </div>

  <script>
    const startTime = Date.now();

    function formatTime(seconds) {
      const h = String(Math.floor(seconds / 3600)).padStart(2, "0");
      const m = String(Math.floor((seconds % 3600) / 60)).padStart(2, "0");
      const s = String(Math.floor(seconds % 60)).padStart(2, "0");
      return `${h}:${m}:${s}`;
    }

    function updateUptime() {
      const diffSec = (Date.now() - startTime) / 1000;
      const uptimeEl = document.getElementById("uptime-text");
      if (uptimeEl) uptimeEl.textContent = formatTime(diffSec);
    }

    function updateTelemetryFake() {
      const speedEl = document.getElementById("telemetry-speed");
      const speedModeEl = document.getElementById("telemetry-speed-mode");
      const tempEl = document.getElementById("telemetry-temp");
      const netEl = document.getElementById("telemetry-network");
      const netSubEl = document.getElementById("telemetry-network-sub");
      const modeEl = document.getElementById("telemetry-mode");
      const modeSubEl = document.getElementById("telemetry-mode-sub");
      const batteryFill = document.getElementById("battery-fill");
      const batteryText = document.getElementById("battery-text");
      const logList = document.getElementById("log-list");

      if (!speedEl || !speedModeEl || !tempEl || !netEl || !netSubEl || !modeEl || !modeSubEl || !batteryFill || !batteryText || !logList) {
        return;
      }

      const speed = (Math.random() * 1.6).toFixed(2);
      speedEl.textContent = speed;
      speedModeEl.textContent = speed > 1.0 ? "Sport Mode" : speed > 0.2 ? "Comfort Mode" : "Idle";

      const temp = (30 + Math.random() * 10).toFixed(1);
      tempEl.textContent = temp;

      const network = -40 - Math.random() * 35;
      netEl.textContent = network.toFixed(0);
      netSubEl.textContent = network > -55 ? "Wi-Fi Link · Excellent" :
                             network > -65 ? "Wi-Fi Link · Good" :
                                             "Wi-Fi Link · Weak";

      const modes = [
        ["Remote", "Operator control"],
        ["Autonomous", "Path following"],
        ["Assist", "Shared control"]
      ];
      const chosen = modes[Math.floor(Math.random() * modes.length)];
      modeEl.textContent = chosen[0];
      modeSubEl.textContent = chosen[1];

      const base = 78;
      const offset = (Math.sin(Date.now() / 40000) * 3);
      const battery = Math.max(0, Math.min(100, base + offset));
      batteryFill.style.width = battery.toFixed(0) + "%";
      batteryText.textContent = battery.toFixed(0) + "%";

      if (Math.random() < 0.3) {
        const nowSeconds = (Date.now() - startTime) / 1000;
        const timeLabel = formatTime(nowSeconds);
        const messages = [
          "Gesture frame verarbeitet",
          "Face detection aktualisiert",
          "Telemetrie aktualisiert",
          "Netzwerk-Check OK",
          "Mode state synchronisiert"
        ];
        const msg = messages[Math.floor(Math.random() * messages.length)];

        const li = document.createElement("li");
        li.className = "log-item";
        li.innerHTML = `<span class="log-label">${timeLabel}</span><span class="log-value">${msg}</span>`;
        logList.insertBefore(li, logList.firstChild);

        while (logList.children.length > 20) {
          logList.removeChild(logList.lastChild);
        }
      }
    }

    setInterval(updateUptime, 1000);
    setInterval(updateTelemetryFake, 2000);
    updateUptime();
    updateTelemetryFake();

    const controllerStatusEl = document.getElementById("controller-status");
    const lastBtnStrong = document.getElementById("controller-last-btn")?.querySelector("strong");
    const apiStateEl = document.getElementById("controller-api-state");
    const controllerActiveSpan = document.getElementById("controller-active")?.querySelector("span");

    const stickLeftNub = document.getElementById("stick-l");
    const stickRightNub = document.getElementById("stick-r");

    const buttonMap = {
      0:  "btn-cross",
      1:  "btn-circle",
      2:  "btn-square",
      3:  "btn-triangle",
      4:  "btn-l1",
      5:  "btn-r1",
      6:  "btn-l2",
      7:  "btn-r2",
      8:  "btn-share",
      9:  "btn-options",
      10: "btn-l3",
      11: "btn-r3",
      12: "btn-du",
      13: "btn-dd",
      14: "btn-dl",
      15: "btn-dr",
      16: "btn-ps",
      17: "btn-touchpad"
    };

    const buttonNames = {
      "btn-cross":    "✕",
      "btn-circle":   "○",
      "btn-square":   "□",
      "btn-triangle": "△",
      "btn-l1":       "L1",
      "btn-r1":       "R1",
      "btn-l2":       "L2",
      "btn-r2":       "R2",
      "btn-share":    "SHARE",
      "btn-options":  "OPTIONS",
      "btn-l3":       "L3",
      "btn-r3":       "R3",
      "btn-du":       "D-Up",
      "btn-dd":       "D-Down",
      "btn-dl":       "D-Left",
      "btn-dr":       "D-Right",
      "btn-ps":       "PS",
      "btn-touchpad": "Touchpad"
    };

    const buttonElements = {};
    document.querySelectorAll("[data-btn-id]").forEach(el => {
      const id = el.getAttribute("data-btn-id");
      buttonElements[id] = el;
    });

    let activeGamepadIndex = null;

    function setControllerStatus(connected, gamepad) {
      if (!controllerStatusEl) return;
      if (connected && gamepad) {
        controllerStatusEl.innerHTML = `Controller: <span>${gamepad.id}</span>`;
      } else {
        controllerStatusEl.innerHTML = `Controller: <span>nicht verbunden</span>`;
      }
    }

    function addControllerLog(message) {
      const logList = document.getElementById("log-list");
      if (!logList) return;
      const nowSeconds = (Date.now() - startTime) / 1000;
      const timeLabel = formatTime(nowSeconds);
      const li = document.createElement("li");
      li.className = "log-item";
      li.innerHTML = `<span class="log-label">${timeLabel}</span><span class="log-value">${message}</span>`;
      logList.insertBefore(li, logList.firstChild);
      while (logList.children.length > 20) {
        logList.removeChild(logList.lastChild);
      }
    }

    function clearAllButtons() {
      Object.values(buttonElements).forEach(el => el.classList.remove("active"));
      if (controllerActiveSpan) controllerActiveSpan.textContent = "–";
    }

    function resetSticks() {
      if (stickLeftNub) {
        stickLeftNub.style.setProperty("--dx", "0%");
        stickLeftNub.style.setProperty("--dy", "0%");
      }
      if (stickRightNub) {
        stickRightNub.style.setProperty("--dx", "0%");
        stickRightNub.style.setProperty("--dy", "0%");
      }
    }

    function updateStickNubs(gp) {
      const ax0 = gp.axes[0] || 0;
      const ax1 = gp.axes[1] || 0;
      const ax2 = gp.axes[2] || 0;
      const ax3 = gp.axes[3] || 0;

      const maxOffset = 35;

      if (stickLeftNub) {
        stickLeftNub.style.setProperty("--dx", `${ax0 * maxOffset}%`);
        stickLeftNub.style.setProperty("--dy", `${ax1 * maxOffset}%`);
      }
      if (stickRightNub) {
        stickRightNub.style.setProperty("--dx", `${ax2 * maxOffset}%`);
        stickRightNub.style.setProperty("--dy", `${ax3 * maxOffset}%`);
      }
    }

    function updateGamepad() {
      const gamepads = navigator.getGamepads ? navigator.getGamepads() : [];
      let gp = null;

      if (activeGamepadIndex !== null && gamepads[activeGamepadIndex]) {
        gp = gamepads[activeGamepadIndex];
      } else {
        for (let i = 0; i < gamepads.length; i++) {
          if (gamepads[i]) {
            gp = gamepads[i];
            activeGamepadIndex = i;
            setControllerStatus(true, gp);
            break;
          }
        }
      }

      if (!gp) {
        clearAllButtons();
        resetSticks();
        requestAnimationFrame(updateGamepad);
        return;
      }

      const activeNames = [];

      gp.buttons.forEach((btn, index) => {
        const id = buttonMap[index];
        if (!id) return;
        const el = buttonElements[id];
        if (!el) return;

        if (btn.pressed) {
          if (!el.classList.contains("active")) {
            el.classList.add("active");
            const pretty = buttonNames[id] || id;
            if (lastBtnStrong) lastBtnStrong.textContent = pretty;
          }
          const pretty = buttonNames[id] || id;
          if (!activeNames.includes(pretty)) activeNames.push(pretty);
        } else {
          el.classList.remove("active");
        }
      });

      if (controllerActiveSpan) {
        controllerActiveSpan.textContent = activeNames.length ? activeNames.join(" · ") : "–";
      }

      updateStickNubs(gp);
      requestAnimationFrame(updateGamepad);
    }

    if (!("getGamepads" in navigator)) {
      if (apiStateEl) apiStateEl.textContent = "nicht verfügbar";
      if (controllerStatusEl) controllerStatusEl.innerHTML = `Controller: <span>nicht unterstützt</span>`;
    } else {
      if (apiStateEl) apiStateEl.textContent = "bereit";
      requestAnimationFrame(updateGamepad);
    }

    window.addEventListener("gamepadconnected", (e) => {
      activeGamepadIndex = e.gamepad.index;
      setControllerStatus(true, e.gamepad);
      if (apiStateEl) apiStateEl.textContent = "aktiv";
      addControllerLog(`Gamepad verbunden: ${e.gamepad.id}`);
    });

    window.addEventListener("gamepaddisconnected", (e) => {
      addControllerLog(`Gamepad getrennt: ${e.gamepad.id}`);
      activeGamepadIndex = null;
      setControllerStatus(false, null);
      if (apiStateEl) apiStateEl.textContent = "bereit";
      clearAllButtons();
      resetSticks();
    });

    /* ==== QR CODE + MOBILE VIEW LOGIK ==== */

    (function setupQrAndMobile() {
      const params = new URLSearchParams(window.location.search);
      const isMobile = params.get("mobile") === "1";

      const appShell = document.querySelector(".app-shell");
      const mobileShell = document.getElementById("mobile-shell");

      if (isMobile) {
        if (appShell) appShell.style.display = "none";
        if (mobileShell) mobileShell.style.display = "flex";
        document.body.style.padding = "0";
        document.body.style.justifyContent = "center";
      } else {
        if (mobileShell) mobileShell.style.display = "none";
      }

      const openQrBtn = document.getElementById("open-qr-btn");
      const qrModal = document.getElementById("qr-modal");
      const qrCanvas = document.getElementById("qr-canvas");
      const qrClose = document.getElementById("qr-close");
      const qrUrlLabel = document.getElementById("qr-url");

      if (openQrBtn && qrModal && qrCanvas) {
        let baseUrl;

        // Wenn als file:// geöffnet, origin ist leer oder file:// -> LAN-URL hart setzen
        if (!window.location.origin || window.location.origin.startsWith("file")) {
  // ⚠️ HIER deine echte IP + PORT 8080
  baseUrl = "http://localhost:8080/GIBI_Website.html";
} else {
  baseUrl = window.location.origin + window.location.pathname;
}


        const mobileUrl = baseUrl + (baseUrl.includes("?") ? "&mobile=1" : "?mobile=1");

        if (qrUrlLabel) {
          qrUrlLabel.textContent = mobileUrl;
        }

        function openModal() {
          qrModal.style.display = "flex";
          if (window.QRCode && qrCanvas) {
            QRCode.toCanvas(qrCanvas, mobileUrl, {
              width: 220,
              margin: 2
            }, function (err) {
              if (err) console.error(err);
            });
          }
        }

        function closeModal() {
          qrModal.style.display = "none";
        }

        openQrBtn.addEventListener("click", openModal);
        if (qrClose) qrClose.addEventListener("click", closeModal);
        qrModal.addEventListener("click", (e) => {
          if (e.target === qrModal) {
            closeModal();
          }
        });
      }
    })();

    /* ==== PUSH TO TALK (Mobile) ==== */

    (function setupPushToTalk() {
      const pttBtn = document.getElementById("ptt-btn");
      const pttText = document.getElementById("ptt-text");
      const pttLabel = document.getElementById("ptt-label");
      if (!pttBtn) return;

      let recognition = null;
      let listening = false;

      const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
      if (!SpeechRecognition) {
        if (pttLabel) {
          pttLabel.textContent = "Browser unterstützt kein Speech-To-Text";
        }
        return;
      }

      recognition = new SpeechRecognition();
      recognition.lang = "de-DE";
      recognition.continuous = false;
      recognition.interimResults = true;

      recognition.onstart = () => {
        listening = true;
        pttBtn.classList.add("active");
        if (pttLabel) pttLabel.textContent = "Sprich jetzt …";
      };

      recognition.onend = () => {
        listening = false;
        pttBtn.classList.remove("active");
        if (pttLabel) pttLabel.textContent = "Gedrückt halten & sprechen";
      };

      recognition.onerror = (event) => {
        console.error("SpeechRecognition error", event);
        if (pttLabel) pttLabel.textContent = "Fehler bei Spracherkennung";
      };

      recognition.onresult = (event) => {
        let finalTranscript = "";
        let interimTranscript = "";

        for (let i = event.resultIndex; i < event.results.length; ++i) {
          if (event.results[i].isFinal) {
            finalTranscript += event.results[i][0].transcript;
          } else {
            interimTranscript += event.results[i][0].transcript;
          }
        }

        const textToShow = (finalTranscript || interimTranscript).trim();
        if (pttText) {
          pttText.textContent = textToShow;
        }

        // Hier könntest du den Text an dein Backend schicken:
        // fetch("/api/speech", {
        //   method: "POST",
        //   headers: { "Content-Type": "application/json" },
        //   body: JSON.stringify({ text: textToShow })
        // });
      };

      function startListening() {
        if (!recognition || listening) return;
        try {
          recognition.start();
        } catch (err) {
          console.error(err);
        }
      }

      function stopListening() {
        if (!recognition || !listening) return;
        recognition.stop();
      }

      pttBtn.addEventListener("mousedown", startListening);
      pttBtn.addEventListener("mouseup", stopListening);
      pttBtn.addEventListener("mouseleave", stopListening);

      pttBtn.addEventListener("touchstart", (e) => {
        e.preventDefault();
        startListening();
      }, { passive: false });

      pttBtn.addEventListener("touchend", (e) => {
        e.preventDefault();
        stopListening();
      }, { passive: false });
    })();
  </script>
</body>
</html>
