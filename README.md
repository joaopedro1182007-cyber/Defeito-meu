# Defeito-meu
Um aplicativo para se declarar e mostrar para a pessoa que você ama o quanto ela é importante para você!
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Defeito Meu 💖</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400;1,700&family=EB+Garamond:ital,wght@0,300;0,400;1,300;1,400&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --wine:   #5c1120;
    --rose:   #b8364d;
    --blush:  #f0909f;
    --cream:  #fdf0ee;
    --gold:   #c9963a;
    --gold2:  #e8c87a;
    --dark:   #110508;
    --border: rgba(201,150,58,0.18);
  }

  body {
    background: var(--dark);
    color: var(--cream);
    font-family: 'EB Garamond', serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  .bg {
    position: fixed; inset: 0; z-index: 0;
    background:
      radial-gradient(ellipse 70% 60% at 15% 55%, #40091a 0%, transparent 65%),
      radial-gradient(ellipse 50% 50% at 85% 15%, #1f0820 0%, transparent 55%),
      radial-gradient(ellipse 60% 50% at 60% 90%, #280712 0%, transparent 55%),
      #0e0408;
  }

  .petals-container {
    position: fixed; inset: 0; z-index: 1; pointer-events: none; overflow: hidden;
  }
  .petal {
    position: absolute; top: -30px; opacity: 0;
    animation: fall linear infinite; user-select: none;
  }
  @keyframes fall {
    0%   { transform: translateX(0) rotate(0deg); opacity: 0.75; top: -30px; }
    50%  { transform: translateX(40px) rotate(180deg); }
    100% { transform: translateX(-20px) rotate(360deg); opacity: 0; top: 108vh; }
  }

  header {
    position: relative; z-index: 10;
    text-align: center;
    padding: 3.5rem 1rem 1.5rem;
  }

  .eyebrow {
    font-size: 0.72rem; letter-spacing: 0.45em; text-transform: uppercase;
    color: var(--gold); margin-bottom: 0.7rem;
    opacity: 0; animation: fadeUp 1s 0.2s forwards;
  }

  h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(3rem, 9vw, 6rem);
    font-style: italic; font-weight: 700;
    background: linear-gradient(150deg, var(--blush) 0%, var(--gold2) 50%, var(--rose) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    line-height: 1.05; opacity: 0; animation: fadeUp 1s 0.4s forwards;
  }

  .divider {
    display: flex; align-items: center; justify-content: center; gap: 0.9rem;
    margin: 1.2rem auto 0; opacity: 0; animation: fadeUp 1s 0.6s forwards; max-width: 300px;
  }
  .divider-line { flex: 1; height: 1px; background: linear-gradient(to right, transparent, var(--gold)); }
  .divider-line.r { background: linear-gradient(to left, transparent, var(--gold)); }
  .heart-icon { color: var(--rose); font-size: 1.05rem; animation: pulse 2s ease-in-out infinite; display: inline-block; }
  @keyframes pulse { 0%,100%{transform:scale(1);} 50%{transform:scale(1.35);} }

  main {
    position: relative; z-index: 10;
    max-width: 760px; margin: 0 auto; padding: 1.5rem 1.5rem 6rem;
  }

  .message-card {
    background: linear-gradient(145deg, rgba(92,17,32,0.28), rgba(20,6,12,0.65));
    border: 1px solid var(--border); border-radius: 3px;
    padding: 2.8rem 2.5rem 2rem; margin-bottom: 1.8rem;
    backdrop-filter: blur(16px); position: relative; overflow: hidden;
    opacity: 0; animation: fadeUp 1s 0.8s forwards;
    box-shadow: 0 30px 80px rgba(0,0,0,0.5), inset 0 1px 0 rgba(255,255,255,0.04);
  }
  .message-card::before {
    content: '\275D'; position: absolute; top: -0.3rem; left: 1.2rem;
    font-size: 7rem; color: var(--rose); opacity: 0.1;
    font-family: 'Playfair Display', serif; line-height: 1; pointer-events: none;
  }
  .message-card::after {
    content: ''; position: absolute; bottom: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, transparent, var(--rose), transparent); opacity: 0.4;
  }

  #displayed-message {
    font-size: clamp(1.15rem, 2.8vw, 1.5rem); font-style: italic; line-height: 1.85;
    color: var(--cream); min-height: 3rem; transition: opacity 0.35s ease;
    text-align: center; position: relative; z-index: 1;
  }
  .message-author {
    text-align: right; margin-top: 1.5rem;
    color: var(--gold); font-size: 0.88rem; letter-spacing: 0.12em; opacity: 0.9;
  }

  .actions {
    display: flex; flex-wrap: wrap; gap: 0.9rem; justify-content: center;
    margin-bottom: 2.5rem; opacity: 0; animation: fadeUp 1s 1s forwards;
  }

  .btn {
    padding: 0.7rem 1.7rem; border: none; cursor: pointer;
    font-family: 'EB Garamond', serif; font-size: 1.05rem;
    letter-spacing: 0.04em; border-radius: 2px;
    transition: all 0.28s cubic-bezier(0.34,1.4,0.64,1);
    position: relative; overflow: hidden; white-space: nowrap;
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--wine), var(--rose));
    color: var(--cream); border: 1px solid rgba(184,54,77,0.6);
    box-shadow: 0 4px 20px rgba(184,54,77,0.25);
  }
  .btn-primary:hover { transform: translateY(-3px) scale(1.02); box-shadow: 0 10px 30px rgba(184,54,77,0.45); }
  .btn-secondary {
    background: rgba(255,255,255,0.04); color: var(--gold);
    border: 1px solid rgba(201,150,58,0.35);
  }
  .btn-secondary:hover { background: rgba(201,150,58,0.1); transform: translateY(-3px) scale(1.02); }

  .panel {
    background: rgba(255,255,255,0.025); border: 1px solid var(--border); border-radius: 3px;
    padding: 2rem 2rem 1.8rem; margin-bottom: 2rem; backdrop-filter: blur(8px);
    animation: fadeUp 1s 1.1s both;
  }

  .panel h2 {
    font-family: 'Playfair Display', serif; font-size: 1.25rem; color: var(--gold);
    margin-bottom: 1.3rem; font-style: italic;
    display: flex; align-items: center; gap: 0.5rem;
    border-bottom: 1px solid var(--border); padding-bottom: 0.8rem;
  }
  .panel h2.sub {
    margin-top: 1.4rem; border-top: 1px solid var(--border); padding-top: 1.2rem;
  }

  textarea, input[type="text"] {
    width: 100%; background: rgba(255,255,255,0.04);
    border: 1px solid rgba(201,150,58,0.18); border-radius: 2px;
    color: var(--cream); font-family: 'EB Garamond', serif;
    font-size: 1.05rem; padding: 0.85rem 1rem; outline: none;
    transition: border-color 0.3s, box-shadow 0.3s;
  }
  textarea { resize: vertical; min-height: 110px; margin-bottom: 0.7rem; }
  input[type="text"] { margin-bottom: 1rem; }
  textarea:focus, input[type="text"]:focus {
    border-color: rgba(184,54,77,0.6); box-shadow: 0 0 0 3px rgba(184,54,77,0.1);
  }
  textarea::placeholder, input[type="text"]::placeholder { color: rgba(240,144,159,0.35); font-style: italic; }

  .row { display: flex; gap: 0.8rem; flex-wrap: wrap; }

  .saved-list { display: flex; flex-direction: column; gap: 0.75rem; margin-bottom: 1.5rem; }
  .saved-empty { color: rgba(240,144,159,0.38); font-style: italic; font-size: 0.95rem; text-align: center; padding: 1rem 0; }
  .saved-item {
    background: rgba(255,255,255,0.025); border: 1px solid rgba(255,255,255,0.06);
    border-left: 3px solid var(--rose); padding: 1rem 1.2rem; border-radius: 0 3px 3px 0;
    cursor: pointer; transition: all 0.25s;
    display: flex; justify-content: space-between; align-items: flex-start; gap: 1rem;
  }
  .saved-item:hover { background: rgba(184,54,77,0.1); transform: translateX(5px); }
  .saved-item p { font-style: italic; font-size: 0.95rem; color: var(--cream); opacity: 0.85; flex: 1; line-height: 1.5; }
  .saved-meta { display: flex; align-items: center; gap: 0.5rem; flex-shrink: 0; }
  .saved-meta span { font-size: 0.75rem; color: var(--gold); white-space: nowrap; }
  .delete-btn {
    background: none; border: none; cursor: pointer;
    color: rgba(255,255,255,0.25); font-size: 0.9rem; padding: 0 0.2rem; transition: color 0.2s;
  }
  .delete-btn:hover { color: var(--rose); }

  #music-btn {
    position: fixed; bottom: 1.8rem; right: 1.8rem; z-index: 50;
    width: 52px; height: 52px; border-radius: 50%;
    border: 1px solid rgba(201,150,58,0.4);
    background: linear-gradient(135deg, rgba(92,17,32,0.9), rgba(184,54,77,0.9));
    color: white; font-size: 1.4rem; cursor: pointer;
    backdrop-filter: blur(10px); box-shadow: 0 4px 20px rgba(0,0,0,0.5);
    transition: all 0.3s; display: flex; align-items: center; justify-content: center;
  }
  #music-btn:hover { transform: scale(1.1); box-shadow: 0 6px 25px rgba(184,54,77,0.5); }
  #music-btn.muted { opacity: 0.5; }

  .toast {
    position: fixed; bottom: 2rem; left: 50%;
    transform: translateX(-50%) translateY(120px);
    background: linear-gradient(135deg, #3d0e1a, #7a2035);
    color: var(--cream); padding: 0.75rem 2rem; border-radius: 2px;
    font-size: 0.95rem; z-index: 200;
    transition: transform 0.4s cubic-bezier(0.34,1.56,0.64,1);
    border: 1px solid rgba(184,54,77,0.5); box-shadow: 0 10px 40px rgba(0,0,0,0.6); white-space: nowrap;
  }
  .toast.show { transform: translateX(-50%) translateY(0); }

  .share-overlay {
    display: none; position: fixed; inset: 0; z-index: 100;
    background: rgba(8,2,5,0.94); backdrop-filter: blur(10px);
    align-items: center; justify-content: center; padding: 1.5rem;
  }
  .share-overlay.open { display: flex; }
  .share-card {
    background: linear-gradient(145deg, #1e090f, #2d0c18);
    border: 1px solid rgba(201,150,58,0.3); border-radius: 4px;
    padding: 3rem 2.5rem; max-width: 460px; width: 100%;
    text-align: center; position: relative;
    box-shadow: 0 40px 100px rgba(0,0,0,0.8);
    animation: scaleIn 0.35s cubic-bezier(0.34,1.56,0.64,1);
  }
  @keyframes scaleIn { from{transform:scale(0.85);opacity:0;} to{transform:scale(1);opacity:1;} }
  .share-card h3 {
    font-family: 'Playfair Display', serif; font-style: italic; font-size: 2rem;
    background: linear-gradient(135deg, var(--blush), var(--gold2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    margin-bottom: 1.6rem;
  }
  .share-msg { font-style: italic; font-size: 1.15rem; line-height: 1.75; color: var(--cream); margin-bottom: 0.6rem; }
  .share-from { color: var(--gold); font-size: 0.88rem; letter-spacing: 0.1em; margin-bottom: 2rem; }
  .close-btn {
    position: absolute; top: 1rem; right: 1.2rem;
    background: none; border: none; color: rgba(201,150,58,0.5); font-size: 1.4rem; cursor: pointer; transition: color 0.2s;
  }
  .close-btn:hover { color: var(--gold); }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(22px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ── GALERIA ── */
  .gallery-panel {
    background: rgba(255,255,255,0.025); border: 1px solid var(--border); border-radius: 3px;
    padding: 2rem 2rem 1.8rem; margin-bottom: 2rem; backdrop-filter: blur(8px);
    animation: fadeUp 1s 1.2s both;
  }
  .gallery-panel h2 {
    font-family: 'Playfair Display', serif; font-size: 1.25rem; color: var(--gold);
    margin-bottom: 1.3rem; font-style: italic;
    display: flex; align-items: center; gap: 0.5rem;
    border-bottom: 1px solid var(--border); padding-bottom: 0.8rem;
  }

  .upload-zone {
    border: 2px dashed rgba(201,150,58,0.3); border-radius: 4px;
    padding: 2rem 1rem; text-align: center; cursor: pointer;
    transition: all 0.3s; margin-bottom: 1.2rem; position: relative;
    background: rgba(255,255,255,0.02);
  }
  .upload-zone:hover, .upload-zone.drag-over {
    border-color: rgba(184,54,77,0.6);
    background: rgba(184,54,77,0.06);
  }
  .upload-zone input[type="file"] {
    position: absolute; inset: 0; opacity: 0; cursor: pointer; width: 100%; height: 100%;
  }
  .upload-zone .upload-icon { font-size: 2.2rem; margin-bottom: 0.5rem; display: block; }
  .upload-zone p { color: rgba(240,144,159,0.6); font-style: italic; font-size: 0.95rem; }
  .upload-zone span { color: var(--gold); font-size: 0.82rem; display: block; margin-top: 0.3rem; opacity: 0.7; }

  .media-grid {
    display: grid; grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
    gap: 0.75rem; margin-bottom: 1.2rem;
  }
  .media-thumb {
    position: relative; border-radius: 3px; overflow: hidden;
    aspect-ratio: 1; background: rgba(0,0,0,0.3);
    border: 1px solid rgba(201,150,58,0.15);
    cursor: pointer; transition: all 0.25s;
    group: true;
  }
  .media-thumb:hover { border-color: rgba(184,54,77,0.5); transform: scale(1.03); }
  .media-thumb img, .media-thumb video {
    width: 100%; height: 100%; object-fit: cover; display: block;
  }
  .media-thumb .thumb-overlay {
    position: absolute; inset: 0; background: rgba(92,17,32,0.0);
    display: flex; align-items: center; justify-content: center; gap: 0.4rem;
    transition: background 0.25s;
  }
  .media-thumb:hover .thumb-overlay { background: rgba(92,17,32,0.7); }
  .thumb-btn {
    background: none; border: none; color: white; font-size: 1.1rem;
    cursor: pointer; opacity: 0; transition: opacity 0.2s; padding: 0.3rem;
  }
  .media-thumb:hover .thumb-btn { opacity: 1; }
  .video-badge {
    position: absolute; top: 0.4rem; left: 0.4rem;
    background: rgba(0,0,0,0.65); border-radius: 2px;
    font-size: 0.65rem; padding: 0.1rem 0.35rem; color: var(--gold2);
    letter-spacing: 0.05em;
  }
  .media-empty {
    grid-column: 1/-1; text-align: center;
    color: rgba(240,144,159,0.35); font-style: italic; font-size: 0.95rem; padding: 1.5rem 0;
  }

  /* ── LIGHTBOX ── */
  .lightbox {
    display: none; position: fixed; inset: 0; z-index: 150;
    background: rgba(5,1,3,0.96); backdrop-filter: blur(12px);
    align-items: center; justify-content: center; padding: 1rem;
  }
  .lightbox.open { display: flex; }
  .lightbox-inner {
    position: relative; max-width: 90vw; max-height: 90vh;
    display: flex; flex-direction: column; align-items: center; gap: 1rem;
  }
  .lightbox-inner img, .lightbox-inner video {
    max-width: 90vw; max-height: 80vh; border-radius: 3px;
    border: 1px solid rgba(201,150,58,0.2);
    box-shadow: 0 40px 100px rgba(0,0,0,0.9);
    object-fit: contain;
  }
  .lightbox-close {
    position: absolute; top: -2.5rem; right: 0;
    background: none; border: none; color: rgba(201,150,58,0.6);
    font-size: 1.6rem; cursor: pointer; transition: color 0.2s;
  }
  .lightbox-close:hover { color: var(--gold); }
  .lightbox-nav {
    display: flex; gap: 0.8rem; align-items: center;
  }
  .lightbox-nav button {
    background: rgba(255,255,255,0.06); border: 1px solid rgba(201,150,58,0.25);
    color: var(--gold); font-size: 1rem; padding: 0.5rem 1.2rem;
    border-radius: 2px; cursor: pointer; transition: all 0.2s;
    font-family: 'EB Garamond', serif;
  }
  .lightbox-nav button:hover { background: rgba(201,150,58,0.12); }
  .lightbox-counter { color: rgba(240,144,159,0.5); font-size: 0.85rem; font-style: italic; }
</style>
</head>
<body>

<div class="bg"></div>
<div class="petals-container" id="petals"></div>

<!-- Player YouTube invisível -->
<div style="position:fixed;top:-9999px;left:-9999px;width:1px;height:1px;overflow:hidden;">
  <div id="yt-player"></div>
</div>

<header>
  <p class="eyebrow">✦ Uma mensagem do coração ✦</p>
  <h1>Defeito Meu</h1>
  <div class="divider">
    <span class="divider-line"></span>
    <span class="heart-icon">♥</span>
    <span class="divider-line r"></span>
  </div>
</header>

<main>
  <div class="message-card">
    <p id="displayed-message">Te amar é o meu defeito mais bonito... 💖</p>
    <p class="message-author" id="displayed-author">— Com amor ✦</p>
  </div>

  <div class="actions">
    <button class="btn btn-primary" onclick="randomMessage()">💌 Nova Mensagem</button>
    <button class="btn btn-secondary" onclick="openShare()">💝 Compartilhar</button>
    <button class="btn btn-secondary" onclick="copyMessage()">📋 Copiar</button>
    <button class="btn btn-secondary" onclick="document.getElementById('gallery-panel').scrollIntoView({behavior:'smooth'})">📸 Nossa Galeria</button>
  </div>

  <div class="gallery-panel" id="gallery-panel">
    <h2>📸 Nossa Galeria</h2>
    <div class="upload-zone" id="upload-zone">
      <input type="file" id="media-input" accept="image/*,video/*" multiple onchange="handleFiles(this.files)" />
      <span class="upload-icon">🌹</span>
      <p>Clique ou arraste fotos e vídeos aqui</p>
      <span>Suporte: JPG, PNG, GIF, MP4, MOV e mais</span>
    </div>
    <div class="media-grid" id="media-grid">
      <p class="media-empty">Nenhuma foto ou vídeo adicionado ainda... 💫</p>
    </div>
  </div>

  <div class="lightbox" id="lightbox">
    <div class="lightbox-inner">
      <button class="lightbox-close" onclick="closeLightbox()">✕</button>
      <div id="lightbox-media"></div>
      <div class="lightbox-nav">
        <button onclick="lightboxPrev()">← Anterior</button>
        <span class="lightbox-counter" id="lightbox-counter"></span>
        <button onclick="lightboxNext()">Próximo →</button>
      </div>
    </div>
  </div>

  <div class="panel">
    <h2>✍️ Escreva sua mensagem</h2>
    <textarea id="custom-msg" placeholder="Escreva aqui o que sente no coração..."></textarea>

    <h2 class="sub">🖊️ Assinatura</h2>
    <input type="text" id="custom-author" placeholder="Assinado: (seu nome ou apelido)" />

    <h2 class="sub">💌 Minhas mensagens salvas</h2>
    <div class="saved-list" id="saved-list">
      <p class="saved-empty">Nenhuma mensagem salva ainda...</p>
    </div>

    <div class="row">
      <button class="btn btn-primary" onclick="showCustom()">💖 Exibir mensagem</button>
      <button class="btn btn-secondary" onclick="saveMessage()">💾 Salvar mensagem</button>
    </div>
  </div>
</main>

<div class="share-overlay" id="share-modal">
  <div class="share-card">
    <button class="close-btn" onclick="closeShare()">✕</button>
    <h3>Defeito Meu 💖</h3>
    <p class="share-msg" id="share-text">—</p>
    <p class="share-from" id="share-author">—</p>
    <div class="row" style="justify-content:center;">
      <button class="btn btn-primary" onclick="copyShare()">📋 Copiar</button>
      <button class="btn btn-secondary" onclick="shareWhatsApp()">💬 WhatsApp</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>
<button id="music-btn" class="muted" onclick="toggleMusic()" title="Tocar música">🔇</button>

<script src="https://www.youtube.com/iframe_api"></script>
<script>
  // ── MENSAGENS ──
  const defaultMessages = [
    { text: "Te amar é o meu defeito mais bonito, e nunca vou querer me curar disso.", author: "Do fundo do coração" },
    { text: "Você chegou e bagunçou tudo de um jeito que eu precisava ser bagunçado.", author: "Com amor" },
    { text: "Eu me perco em você de um jeito que nem o mapa-múndi me salvaria.", author: "Apaixonado(a)" },
    { text: "Se te amar é loucura, então eu não quero a razão.", author: "Para sempre seu(sua)" },
    { text: "Você é o motivo pelo qual eu acredito que o amor de verdade existe.", author: "Com todo meu amor" },
    { text: "Até os meus defeitos ficam bonitos quando estão perto de você.", author: "Seu(Sua) maior fã" },
    { text: "Eu não sei viver sem você — e nem quero tentar descobrir.", author: "Infinitamente seu(sua)" },
    { text: "O meu coração bate diferente quando você está por perto.", author: "Com saudade e amor" },
    { text: "Você é a parte mais bonita de qualquer dia que eu vivo.", author: "Do coração" },
    { text: "Se amor fosse música, o que eu sinto por você seria a nossa canção favorita.", author: "Sempre seu(sua)" },
    { text: "Com você aprendi que amar é a única coisa que vale a pena perder o controle.", author: "De coração aberto" },
    { text: "Às vezes fico te olhando e penso: como fui tão sorteiro de te encontrar?", author: "Com gratidão e amor" },
  ];

  let currentMessage = defaultMessages[0];
  let savedMessages = [];

  // ── YOUTUBE ──
  let ytPlayer = null;
  let ytReady = false;
  let musicOn = false;

  window.onYouTubeIframeAPIReady = function() {
    ytPlayer = new YT.Player('yt-player', {
      height: '1', width: '1',
      videoId: '9HkwZBjZ6-w',
      playerVars: { autoplay: 0, loop: 1, playlist: '9HkwZBjZ6-w', controls: 0, rel: 0, modestbranding: 1 },
      events: {
        onReady: function(e) {
          ytReady = true;
          e.target.setVolume(50);
          showToast('🎵 Clique em 🔇 para tocar a música!');
        }
      }
    });
  };

  function toggleMusic() {
    const btn = document.getElementById('music-btn');
    if (!ytReady) { showToast('⏳ Aguarde, carregando...'); return; }
    if (musicOn) {
      ytPlayer.pauseVideo();
      btn.textContent = '🔇';
      btn.classList.add('muted');
      musicOn = false;
    } else {
      ytPlayer.playVideo();
      btn.textContent = '🎵';
      btn.classList.remove('muted');
      musicOn = true;
    }
  }

  // ── PÉTALAS ──
  function createPetals() {
    const container = document.getElementById('petals');
    const emojis = ['🌹','🌸','💗','✨','💫','🌺','🪷'];
    for (let i = 0; i < 20; i++) {
      const p = document.createElement('span');
      p.className = 'petal';
      p.textContent = emojis[Math.floor(Math.random() * emojis.length)];
      p.style.left = (Math.random() * 100) + 'vw';
      p.style.animationDuration = (7 + Math.random() * 9) + 's';
      p.style.animationDelay = (Math.random() * 10) + 's';
      p.style.fontSize = (0.75 + Math.random() * 0.75) + 'rem';
      container.appendChild(p);
    }
  }

  // ── MENSAGENS ──
  function displayMessage(msg, author) {
    const el = document.getElementById('displayed-message');
    const au = document.getElementById('displayed-author');
    el.style.opacity = '0'; au.style.opacity = '0';
    setTimeout(() => {
      el.textContent = msg; au.textContent = '— ' + author + ' ✦';
      el.style.transition = 'opacity 0.4s'; au.style.transition = 'opacity 0.4s';
      el.style.opacity = '1'; au.style.opacity = '1';
    }, 320);
    currentMessage = { text: msg, author };
  }

  function randomMessage() {
    const all = [...defaultMessages, ...savedMessages];
    displayMessage(...Object.values(all[Math.floor(Math.random() * all.length)]));
  }

  function showCustom() {
    const msg = document.getElementById('custom-msg').value.trim();
    const author = document.getElementById('custom-author').value.trim() || 'Com amor';
    if (!msg) { showToast('✍️ Escreva uma mensagem primeiro!'); return; }
    displayMessage(msg, author);
  }

  function saveMessage() {
    const msg = document.getElementById('custom-msg').value.trim();
    const author = document.getElementById('custom-author').value.trim() || 'Com amor';
    if (!msg) { showToast('✍️ Escreva uma mensagem para salvar!'); return; }
    savedMessages.push({ text: msg, author });
    document.getElementById('custom-msg').value = '';
    document.getElementById('custom-author').value = '';
    renderSaved();
    showToast('💖 Mensagem salva!');
  }

  function renderSaved() {
    const list = document.getElementById('saved-list');
    if (!savedMessages.length) {
      list.innerHTML = '<p class="saved-empty">Nenhuma mensagem salva ainda...</p>';
      return;
    }
    list.innerHTML = savedMessages.map((m, i) => `
      <div class="saved-item" onclick="displayMessage(${JSON.stringify(m.text)}, ${JSON.stringify(m.author)})">
        <p>"${m.text}"</p>
        <div class="saved-meta">
          <span>${m.author}</span>
          <button class="delete-btn" onclick="event.stopPropagation();deleteMsg(${i})">✕</button>
        </div>
      </div>
    `).join('');
  }

  function deleteMsg(i) { savedMessages.splice(i, 1); renderSaved(); showToast('🗑️ Removida'); }

  function copyMessage() {
    navigator.clipboard.writeText(`"${currentMessage.text}"\n\n— ${currentMessage.author} 💖\n\n✨ Defeito Meu`)
      .then(() => showToast('📋 Mensagem copiada!'));
  }

  function openShare() {
    document.getElementById('share-text').textContent = `"${currentMessage.text}"`;
    document.getElementById('share-author').textContent = `— ${currentMessage.author} 💖`;
    document.getElementById('share-modal').classList.add('open');
  }
  function closeShare() { document.getElementById('share-modal').classList.remove('open'); }
  function copyShare() {
    navigator.clipboard.writeText(`"${currentMessage.text}"\n— ${currentMessage.author} 💖\n\n✨ Defeito Meu`)
      .then(() => showToast('📋 Copiado!'));
  }
  function shareWhatsApp() {
    window.open(`https://wa.me/?text=${encodeURIComponent(`💖 *Defeito Meu*\n\n"${currentMessage.text}"\n\n— ${currentMessage.author} ✦`)}`, '_blank');
  }

  function showToast(msg) {
    const t = document.getElementById('toast');
    t.textContent = msg; t.classList.add('show');
    setTimeout(() => t.classList.remove('show'), 3000);
  }

  document.getElementById('share-modal').addEventListener('click', function(e) {
    if (e.target === this) closeShare();
  });

  // ── GALERIA ──
  let mediaItems = [];
  let lightboxIndex = 0;

  const uploadZone = document.getElementById('upload-zone');
  uploadZone.addEventListener('dragover', e => { e.preventDefault(); uploadZone.classList.add('drag-over'); });
  uploadZone.addEventListener('dragleave', () => uploadZone.classList.remove('drag-over'));
  uploadZone.addEventListener('drop', e => {
    e.preventDefault(); uploadZone.classList.remove('drag-over');
    handleFiles(e.dataTransfer.files);
  });

  function handleFiles(files) {
    Array.from(files).forEach(file => {
      if (!file.type.startsWith('image/') && !file.type.startsWith('video/')) return;
      const url = URL.createObjectURL(file);
      mediaItems.push({ url, type: file.type.startsWith('video/') ? 'video' : 'image', name: file.name });
    });
    renderGallery();
    showToast('📸 ' + files.length + ' arquivo(s) adicionado(s)!');
  }

  function renderGallery() {
    const grid = document.getElementById('media-grid');
    if (!mediaItems.length) {
      grid.innerHTML = '<p class="media-empty">Nenhuma foto ou vídeo adicionado ainda... 💫</p>';
      return;
    }
    grid.innerHTML = mediaItems.map((item, i) => `
      <div class="media-thumb" onclick="openLightbox(${i})">
        ${item.type === 'video'
          ? `<video src="${item.url}" muted preload="metadata"></video><span class="video-badge">▶ vídeo</span>`
          : `<img src="${item.url}" alt="foto ${i+1}" loading="lazy" />`
        }
        <div class="thumb-overlay">
          <button class="thumb-btn" onclick="event.stopPropagation();openLightbox(${i})">🔍</button>
          <button class="thumb-btn" onclick="event.stopPropagation();deleteMedia(${i})">🗑️</button>
        </div>
      </div>
    `).join('');
  }

  function deleteMedia(i) {
    URL.revokeObjectURL(mediaItems[i].url);
    mediaItems.splice(i, 1);
    renderGallery();
    showToast('🗑️ Removido');
  }

  function openLightbox(i) {
    lightboxIndex = i;
    renderLightboxMedia();
    document.getElementById('lightbox').classList.add('open');
  }

  function closeLightbox() { document.getElementById('lightbox').classList.remove('open'); }

  function renderLightboxMedia() {
    const item = mediaItems[lightboxIndex];
    const container = document.getElementById('lightbox-media');
    container.innerHTML = item.type === 'video'
      ? `<video src="${item.url}" controls autoplay style="max-width:90vw;max-height:80vh;border-radius:3px;"></video>`
      : `<img src="${item.url}" alt="foto" style="max-width:90vw;max-height:80vh;border-radius:3px;object-fit:contain;" />`;
    document.getElementById('lightbox-counter').textContent = (lightboxIndex + 1) + ' / ' + mediaItems.length;
  }

  function lightboxPrev() {
    lightboxIndex = (lightboxIndex - 1 + mediaItems.length) % mediaItems.length;
    renderLightboxMedia();
  }
  function lightboxNext() {
    lightboxIndex = (lightboxIndex + 1) % mediaItems.length;
    renderLightboxMedia();
  }

  document.getElementById('lightbox').addEventListener('click', function(e) {
    if (e.target === this) closeLightbox();
  });

  document.addEventListener('keydown', e => {
    if (!document.getElementById('lightbox').classList.contains('open')) return;
    if (e.key === 'ArrowLeft') lightboxPrev();
    if (e.key === 'ArrowRight') lightboxNext();
    if (e.key === 'Escape') closeLightbox();
  });

  createPetals();
</script>
</body>
</html>
