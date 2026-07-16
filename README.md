  <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>CHAITANYA EDITS — Cinematic Experience</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --gold: #D4AF37;
      --gold-light: #F4E4BC;
      --gold-dim: rgba(212,175,55,0.15);
      --dark: #0a0a0a;
      --darker: #050505;
      --card-bg: rgba(20,20,20,0.8);
    }
    * { margin: 0; padding: 0; box-sizing: border-box; }
    html { scroll-behavior: smooth; -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; }

    body {
      font-family: 'Inter', sans-serif;
      background: var(--darker);
      color: white;
      overflow-x: hidden;
      line-height: 1.7;
    }

    /* ===== SCENE 1: LOADING ===== */
    .scene-loading {
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100vh;
      background: var(--darker);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 9999;
      transition: opacity 1.5s ease, visibility 1.5s;
    }
    .scene-loading.done { opacity: 0; visibility: hidden; pointer-events: none; }

    .shutter-flash {
      position: absolute; width: 100%; height: 100%;
      background: white; opacity: 0;
      animation: shutterFlash 0.3s ease-out 0.5s forwards;
    }
    @keyframes shutterFlash { 0% { opacity: 0.8; } 100% { opacity: 0; } }

    .loading-particles { position: absolute; width: 100%; height: 100%; overflow: hidden; }
    .particle {
      position: absolute; width: 3px; height: 3px;
      background: var(--gold); border-radius: 50%; opacity: 0;
      animation: particleFloat 3s infinite;
    }
    @keyframes particleFloat {
      0% { transform: translateY(100vh) scale(0); opacity: 0; }
      20% { opacity: 1; } 80% { opacity: 1; }
      100% { transform: translateY(-20vh) scale(1); opacity: 0; }
    }

    .loading-logo {
      font-family: 'Orbitron', sans-serif; font-size: 3rem; font-weight: 900;
      color: var(--gold); letter-spacing: 8px; opacity: 0; transform: scale(0.5);
      animation: logoReveal 1s ease-out 1s forwards;
    }
    @keyframes logoReveal { to { opacity: 1; transform: scale(1); } }

    .loading-text {
      margin-top: 2rem; font-size: 0.9rem; letter-spacing: 4px;
      color: rgba(255,255,255,0.5); animation: loadingPulse 1.5s infinite;
    }
    @keyframes loadingPulse { 0%,100% { opacity: 0.3; } 50% { opacity: 1; } }

    .progress-bar {
      width: 200px; height: 2px; background: rgba(255,255,255,0.1);
      margin-top: 1.5rem; border-radius: 2px; overflow: hidden;
    }
    .progress-fill {
      width: 0%; height: 100%; background: var(--gold);
      animation: progressLoad 2.5s ease-out 0.5s forwards;
    }
    @keyframes progressLoad { to { width: 100%; } }

    /* ===== CREATIVE NAVBAR ===== */
    .creative-nav {
      position: fixed; top: 20px; left: 50%; transform: translateX(-50%);
      z-index: 1000; display: flex; align-items: center; gap: 0;
      padding: 10px 8px;
      background: rgba(10,10,10,0.7);
      backdrop-filter: blur(24px) saturate(180%);
      -webkit-backdrop-filter: blur(24px) saturate(180%);
      border: 1px solid rgba(212,175,55,0.12);
      border-radius: 50px;
      transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
      opacity: 0; translate: 0 -30px;
      max-width: calc(100vw - 2rem);
    }
    .creative-nav.visible { opacity: 1; translate: 0 0; }
    .creative-nav:hover {
      background: rgba(15,15,15,0.9);
      border-color: rgba(212,175,55,0.25);
      box-shadow: 0 8px 32px rgba(212,175,55,0.08);
    }

    .nav-logo-mini {
      font-family: 'Orbitron', sans-serif; font-size: 0.65rem; font-weight: 700;
      color: var(--gold); padding: 8px 14px; letter-spacing: 3px;
      border-right: 1px solid rgba(255,255,255,0.06);
      cursor: pointer; transition: all 0.3s; text-decoration: none;
      white-space: nowrap;
    }
    .nav-logo-mini:hover { color: var(--gold-light); text-shadow: 0 0 20px rgba(212,175,55,0.4); }

    .nav-links { display: flex; gap: 2px; padding: 0 6px; }
    .nav-link {
      position: relative; padding: 8px 14px; font-size: 0.68rem;
      letter-spacing: 1.5px; text-transform: uppercase;
      color: rgba(255,255,255,0.55); text-decoration: none;
      border-radius: 25px; transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
      overflow: hidden; cursor: pointer; border: none; background: none;
      font-family: inherit; white-space: nowrap;
    }
    .nav-link::before {
      content: ''; position: absolute; inset: 0;
      background: radial-gradient(circle at var(--x,50%) var(--y,50%), rgba(212,175,55,0.12), transparent 60%);
      opacity: 0; transition: opacity 0.3s;
    }
    .nav-link:hover::before { opacity: 1; }
    .nav-link:hover { color: var(--gold-light); background: rgba(212,175,55,0.06); }
    .nav-link.active { color: var(--gold); background: rgba(212,175,55,0.08); }

    .nav-cta {
      padding: 8px 18px; background: var(--gold); color: var(--dark);
      font-size: 0.68rem; font-weight: 700; letter-spacing: 1.5px;
      text-transform: uppercase; border-radius: 25px; border: none;
      cursor: pointer; transition: all 0.3s; margin-left: 4px;
      font-family: inherit; white-space: nowrap; min-height: 36px;
    }
    .nav-cta:hover {
      background: var(--gold-light);
      box-shadow: 0 0 30px rgba(212,175,55,0.35);
      transform: scale(1.04);
    }

    /* ===== SCENE 2: HERO ===== */
    .scene-hero {
      position: relative;
      min-height: 100dvh;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      overflow: hidden; background: var(--darker);
      padding: 0 1.5rem;
    }

    .hero-glow {
      position: absolute; width: min(600px, 150vw); height: min(600px, 150vw);
      border-radius: 50%;
      background: radial-gradient(circle, rgba(212,175,55,0.07), transparent 70%);
      pointer-events: none; transition: all 0.15s ease-out; filter: blur(60px);
      will-change: transform;
    }

    .hero-logo-container {
      position: relative; z-index: 2; text-align: center;
      width: 100%; max-width: 100%;
    }

    .hero-logo {
      font-family: 'Orbitron', sans-serif;
      font-size: clamp(1.8rem, 9vw, 5rem);
      font-weight: 900;
      color: var(--gold);
      letter-spacing: clamp(2px, 1.5vw, 10px);
      line-height: 1.1;
      text-shadow:
        0 0 30px rgba(212,175,55,0.25),
        0 0 60px rgba(212,175,55,0.08);
      animation: breathe 4s ease-in-out infinite;
      opacity: 0;
      word-break: normal;
      overflow-wrap: break-word;
      hyphens: none;
    }
    .hero-logo.revealed {
      animation: breathe 4s ease-in-out infinite, fadeInUp 1.2s ease-out forwards;
    }
    @keyframes breathe {
      0%, 100% { transform: scale(1); filter: brightness(1); }
      50% { transform: scale(1.015); filter: brightness(1.08); }
    }
    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(25px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .hero-title {
      margin-top: 1.5rem;
      font-size: clamp(0.7rem, 2.2vw, 1rem);
      letter-spacing: clamp(3px, 0.8vw, 8px);
      text-transform: uppercase;
      color: rgba(255,255,255,0.45);
      opacity: 0; transform: translateY(15px);
      transition: all 1s ease-out 2s;
      font-weight: 400;
    }
    .hero-title.revealed { opacity: 1; transform: translateY(0); }

    .hero-subtitle {
      margin-top: 0.75rem;
      font-size: clamp(0.65rem, 1.8vw, 0.85rem);
      letter-spacing: clamp(2px, 0.5vw, 4px);
      color: rgba(212,175,55,0.5);
      opacity: 0;
      transition: all 1s ease-out 2.6s;
      font-weight: 300;
    }
    .hero-subtitle.revealed { opacity: 1; }

    .scroll-indicator {
      position: absolute; bottom: 5vh; left: 50%; transform: translateX(-50%);
      display: flex; flex-direction: column; align-items: center; gap: 10px;
      opacity: 0; animation: fadeInUp 1s ease-out 3.8s forwards;
    }
    .scroll-line {
      width: 1px; height: 32px;
      background: linear-gradient(to bottom, var(--gold), transparent);
      animation: scrollPulse 2.2s infinite;
    }
    @keyframes scrollPulse {
      0%, 100% { opacity: 0.2; transform: scaleY(0.4); }
      50% { opacity: 0.9; transform: scaleY(1); }
    }
    .scroll-text {
      font-size: 0.55rem; letter-spacing: 3px;
      color: rgba(255,255,255,0.25); text-transform: uppercase;
    }

    /* FIX: Geometric ambient shapes instead of blurry emojis */
    .float-obj {
      position: absolute; pointer-events: none;
      opacity: 0.06; will-change: transform;
    }
    .float-ring {
      top: 12%; right: 5%;
      width: 120px; height: 120px;
      border: 1px solid var(--gold);
      border-radius: 50%;
      animation: floatRotate 35s linear infinite;
    }
    .float-ring::before {
      content: ''; position: absolute; inset: 20px;
      border: 1px solid rgba(212,175,55,0.3); border-radius: 50%;
    }
    .float-diamond {
      bottom: 18%; left: 5%;
      width: 80px; height: 80px;
      border: 1px solid var(--gold);
      transform: rotate(45deg);
      animation: floatRotate 40s linear infinite reverse;
    }
    .float-dot {
      top: 55%; right: 12%;
      width: 6px; height: 6px;
      background: var(--gold); border-radius: 50%;
      animation: floatRotate 30s linear infinite;
      box-shadow: 0 0 20px rgba(212,175,55,0.3);
    }
    @keyframes floatRotate {
      0% { transform: rotate(0deg) translateY(0); }
      33% { transform: rotate(120deg) translateY(-15px); }
      66% { transform: rotate(240deg) translateY(10px); }
      100% { transform: rotate(360deg) translateY(0); }
    }

    /* ===== SCENE 3: FILM STRIP ===== */
    .scene-film {
      position: relative; min-height: 100vh;
      display: flex; align-items: center; justify-content: center;
      overflow: hidden; background: var(--dark); perspective: 1000px;
      padding: 4rem 1.5rem;
    }
    .film-strip-container {
      position: absolute; width: 250%; height: 100%;
      display: flex; gap: 16px;
      transform: rotateY(12deg) rotateX(3deg); opacity: 0.25;
    }
    .film-frame {
      min-width: 260px; height: 170px;
      background: linear-gradient(135deg, rgba(212,175,55,0.08), rgba(0,0,0,0.5));
      border: 1px solid rgba(212,175,55,0.15); border-radius: 6px;
      display: flex; align-items: center; justify-content: center;
      font-size: 2rem; color: rgba(212,175,55,0.2);
      animation: filmScroll 40s linear infinite;
    }
    @keyframes filmScroll { 0% { transform: translateX(0); } 100% { transform: translateX(-50%); } }

    .scene-film-content { position: relative; z-index: 2; text-align: center; max-width: 700px; }

    .scene-label {
      font-size: 0.65rem; letter-spacing: 5px; text-transform: uppercase;
      color: var(--gold); margin-bottom: 1.25rem; opacity: 0; transform: translateY(20px);
      font-weight: 600;
    }
    .scene-label.visible { animation: fadeInUp 0.8s ease-out forwards; }

    .scene-heading {
      font-family: 'Orbitron', sans-serif; font-size: clamp(1.6rem, 4.5vw, 3.2rem);
      font-weight: 700; line-height: 1.15; margin-bottom: 1.25rem;
      opacity: 0; transform: translateY(25px);
    }
    .scene-heading.visible { animation: fadeInUp 1s ease-out 0.2s forwards; }

    .scene-body {
      font-size: clamp(0.9rem, 2vw, 1.05rem); line-height: 1.8;
      color: rgba(255,255,255,0.55); max-width: 560px; margin: 0 auto;
      opacity: 0; transform: translateY(20px);
    }
    .scene-body.visible { animation: fadeInUp 1s ease-out 0.4s forwards; }

    /* ===== SCENE 4: STORY ===== */
    .scene-story {
      position: relative; min-height: 100vh; padding: 100px 1.5rem;
      background: var(--darker); overflow: hidden;
    }
    .story-grid {
      max-width: 1100px; margin: 0 auto;
      display: grid; grid-template-columns: 1fr 1fr; gap: 3rem; align-items: center;
    }
    .story-visual { position: relative; height: 420px; display: flex; align-items: center; justify-content: center; }
    .story-orbit {
      position: absolute; width: 320px; height: 320px;
      border: 1px solid rgba(212,175,55,0.1); border-radius: 50%;
      animation: orbitSpin 30s linear infinite;
    }
    .story-orbit::before {
      content: ''; position: absolute; inset: 40px;
      border: 1px solid rgba(212,175,55,0.06); border-radius: 50%;
      animation: orbitSpin 20s linear infinite reverse;
    }
    @keyframes orbitSpin { to { transform: rotate(360deg); } }
    .story-center {
      width: 120px; height: 120px; border-radius: 50%;
      background: radial-gradient(circle, rgba(212,175,55,0.15), transparent 70%);
      display: flex; align-items: center; justify-content: center; font-size: 3rem;
      animation: pulse 3s ease-in-out infinite;
    }
    @keyframes pulse { 0%,100% { transform: scale(1); } 50% { transform: scale(1.08); } }

    .story-content h2 {
      font-family: 'Orbitron', sans-serif; font-size: clamp(1.5rem, 3.5vw, 2.4rem);
      margin-bottom: 2rem; line-height: 1.2; font-weight: 700;
    }
    .story-content h2 span { color: var(--gold); }

    .story-q {
      margin-bottom: 1.75rem; padding-left: 1.25rem;
      border-left: 2px solid var(--gold);
      opacity: 0; transform: translateX(-25px); transition: all 0.7s ease-out;
    }
    .story-q.visible { opacity: 1; transform: translateX(0); }
    .story-q h4 {
      font-size: 0.85rem; color: var(--gold); margin-bottom: 0.4rem;
      letter-spacing: 2px; text-transform: uppercase; font-weight: 700;
    }
    .story-q p {
      font-size: 0.9rem; color: rgba(255,255,255,0.55); line-height: 1.7;
    }

    /* ===== SCENE 5: SERVICES ===== */
    .scene-services {
      position: relative; min-height: 100vh; padding: 100px 1.5rem;
      background: var(--dark); overflow: hidden;
    }
    .services-header { text-align: center; margin-bottom: 3.5rem; }
    .services-grid {
      max-width: 1100px; margin: 0 auto;
      display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 1.5rem;
    }
    .service-card {
      background: var(--card-bg); border: 1px solid rgba(255,255,255,0.04);
      border-radius: 14px; padding: 2rem; position: relative; overflow: hidden;
      cursor: pointer; opacity: 0;
      transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .service-card:nth-child(1) { transform: translateY(50px) rotate(-1.5deg); }
    .service-card:nth-child(2) { transform: translateX(-35px) scale(0.92); }
    .service-card:nth-child(3) { transform: translateY(-35px) rotate(1.5deg); }
    .service-card:nth-child(4) { transform: translateX(35px) scale(0.92); }
    .service-card:nth-child(5) { transform: translateY(45px) rotate(-1deg); }
    .service-card:nth-child(6) { transform: translateX(-25px) scale(0.95); }
    .service-card.visible { opacity: 1; transform: translate(0) scale(1) rotate(0) !important; }

    .service-card::before {
      content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px;
      background: linear-gradient(90deg, transparent, var(--gold), transparent);
      opacity: 0; transition: opacity 0.3s;
    }
    .service-card:hover::before { opacity: 1; }
    .service-card:hover {
      border-color: rgba(212,175,55,0.15);
      transform: translateY(-6px) !important;
      box-shadow: 0 16px 48px rgba(0,0,0,0.4), 0 0 30px rgba(212,175,55,0.04);
    }
    .service-icon { font-size: 2.2rem; margin-bottom: 1.25rem; display: inline-block; transition: transform 0.3s; }
    .service-card:hover .service-icon { transform: scale(1.15) rotate(8deg); }
    .service-card h3 { font-family: 'Orbitron', sans-serif; font-size: 0.95rem; margin-bottom: 0.6rem; color: var(--gold-light); letter-spacing: 1px; }
    .service-card p { font-size: 0.85rem; color: rgba(255,255,255,0.45); line-height: 1.65; }
    .service-glow {
      position: absolute; width: 140px; height: 140px; border-radius: 50%;
      background: radial-gradient(circle, rgba(212,175,55,0.08), transparent);
      pointer-events: none; opacity: 0; transition: opacity 0.3s;
    }
    .service-card:hover .service-glow { opacity: 1; }

    /* ===== SCENE 6: PORTFOLIO ===== */
    .scene-portfolio {
      position: relative; min-height: 100vh; padding: 100px 1.5rem;
      background: var(--darker); overflow: hidden;
    }
    .portfolio-header { text-align: center; margin-bottom: 3.5rem; }
    .portfolio-grid {
      max-width: 1100px; margin: 0 auto;
      display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 1.5rem;
    }
    .portfolio-card {
      position: relative; height: 240px; border-radius: 14px; overflow: hidden;
      background: linear-gradient(135deg, #12122a, #0f1a30); cursor: pointer; opacity: 0;
      transform: perspective(1000px) rotateY(12deg);
      transition: all 0.6s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .portfolio-card.visible { opacity: 1; transform: perspective(1000px) rotateY(0); }
    .portfolio-card:hover {
      transform: perspective(1000px) rotateY(0) scale(1.02) translateZ(15px);
      box-shadow: 0 24px 48px rgba(0,0,0,0.45);
    }
    .portfolio-card-bg {
      position: absolute; inset: 0;
      background: linear-gradient(135deg, rgba(212,175,55,0.08), rgba(0,0,0,0.75));
      transition: all 0.4s;
    }
    .portfolio-card:hover .portfolio-card-bg {
      background: linear-gradient(135deg, rgba(212,175,55,0.15), rgba(0,0,0,0.6));
    }
    .portfolio-card-content {
      position: absolute; bottom: 0; left: 0; right: 0; padding: 1.75rem;
      background: linear-gradient(to top, rgba(0,0,0,0.92), transparent);
      transform: translateY(15px); transition: all 0.4s;
    }
    .portfolio-card:hover .portfolio-card-content { transform: translateY(0); }
    .portfolio-card h3 { font-family: 'Orbitron', sans-serif; font-size: 1.05rem; margin-bottom: 0.4rem; color: var(--gold-light); }
    .portfolio-card p { font-size: 0.8rem; color: rgba(255,255,255,0.45); }
    .play-btn {
      position: absolute; top: 50%; left: 50%;
      transform: translate(-50%, -50%) scale(0);
      width: 52px; height: 52px; border-radius: 50%; background: var(--gold);
      display: flex; align-items: center; justify-content: center;
      font-size: 1.2rem; color: var(--dark);
      transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
      box-shadow: 0 0 35px rgba(212,175,55,0.35);
    }
    .portfolio-card:hover .play-btn { transform: translate(-50%, -50%) scale(1); }
    .portfolio-glow-orb {
      position: absolute; width: 180px; height: 180px; border-radius: 50%;
      background: radial-gradient(circle, rgba(212,175,55,0.12), transparent);
      pointer-events: none; filter: blur(35px); transition: all 0.3s;
    }

    /* ===== SCENE 7: WORKFLOW ===== */
    .scene-workflow {
      position: relative; min-height: 100vh; padding: 100px 1.5rem;
      background: var(--dark); overflow: hidden;
    }
    .workflow-header { text-align: center; margin-bottom: 4rem; }
    .workflow-container { max-width: 800px; margin: 0 auto; position: relative; }
    .workflow-line {
      position: absolute; left: 50%; top: 0; bottom: 0; width: 2px;
      background: linear-gradient(to bottom, transparent 0%, var(--gold) 10%, var(--gold) 90%, transparent 100%);
      transform: translateX(-50%); opacity: 0.25;
    }
    .workflow-line-fill {
      position: absolute; left: 50%; top: 0; width: 2px; background: var(--gold);
      transform: translateX(-50%); height: 0%; transition: height 1.8s ease-out;
      box-shadow: 0 0 15px rgba(212,175,55,0.4);
    }
    .workflow-step {
      display: flex; align-items: center; margin-bottom: 3.5rem; position: