# matutko-profi.github.io
<!DOCTYPE html>
<html lang="sk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mám pre teba otázku 🌸</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>
<script>emailjs.init('nUU0KSm6GR2D2pxRW');</script>
<style>
  :root {
    --pink: #ff6b9d;
    --rose: #ff3d77;
    --blush: #ffe0ec;
    --cream: #fff7f0;
    --dark: #1a0a12;
    --text: #3d1a2b;
    --gold: #f5c842;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--cream);
    min-height: 100vh;
    overflow-x: hidden;
    color: var(--text);
  }

  /* ---- FLOATING HEARTS BG ---- */
  .hearts-bg {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 0;
    overflow: hidden;
  }
  .heart-float {
    position: absolute;
    bottom: -50px;
    font-size: 1.2rem;
    animation: floatUp linear infinite;
    opacity: 0;
  }
  @keyframes floatUp {
    0%   { transform: translateY(0) rotate(0deg); opacity: 0; }
    10%  { opacity: 0.6; }
    90%  { opacity: 0.4; }
    100% { transform: translateY(-110vh) rotate(360deg); opacity: 0; }
  }

  /* ---- SCREENS ---- */
  .screen {
    display: none;
    min-height: 100vh;
    position: relative;
    z-index: 1;
    animation: fadeIn 0.6s ease;
  }
  .screen.active { display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 2rem 1.5rem; }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ---- SCREEN 1: ASK ---- */
  #screen-ask {
    text-align: center;
    gap: 2rem;
  }

  .big-emoji {
    font-size: 4rem;
    animation: pulse 1.5s ease-in-out infinite;
  }
  @keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.12); }
  }

  .ask-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 8vw, 3.2rem);
    font-weight: 700;
    line-height: 1.2;
    color: var(--dark);
  }
  .ask-title span {
    color: var(--pink);
    font-style: italic;
  }

  .ask-sub {
    font-size: 1rem;
    color: #7a3a55;
    font-weight: 300;
    max-width: 320px;
  }

  .btn-group {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 0.5rem;
  }

  .btn-yes {
    background: linear-gradient(135deg, var(--pink), var(--rose));
    color: #fff;
    border: none;
    padding: 1rem 2.5rem;
    border-radius: 100px;
    font-size: 1.1rem;
    font-family: 'DM Sans', sans-serif;
    font-weight: 500;
    cursor: pointer;
    box-shadow: 0 8px 30px rgba(255,61,119,0.4);
    transition: transform 0.15s, box-shadow 0.15s;
    position: relative;
    overflow: hidden;
  }
  .btn-yes::after {
    content: '';
    position: absolute;
    inset: 0;
    background: rgba(255,255,255,0.15);
    opacity: 0;
    transition: opacity 0.2s;
  }
  .btn-yes:hover { transform: scale(1.05); box-shadow: 0 12px 40px rgba(255,61,119,0.5); }
  .btn-yes:hover::after { opacity: 1; }
  .btn-yes:active { transform: scale(0.97); }

  .btn-no {
    background: transparent;
    color: #c0a0ae;
    border: 2px solid #e8c8d5;
    padding: 1rem 2rem;
    border-radius: 100px;
    font-size: 1rem;
    font-family: 'DM Sans', sans-serif;
    cursor: default !important;
    position: relative;
    transition: transform 0.1s;
    user-select: none;
  }

  /* ---- SCREEN 2: CHOOSE ACTIVITY ---- */
  #screen-activity {
    gap: 1.5rem;
    max-width: 600px;
    margin: 0 auto;
  }

  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.6rem, 6vw, 2.4rem);
    font-weight: 700;
    text-align: center;
    color: var(--dark);
  }
  .section-title span { color: var(--pink); font-style: italic; }

  .section-sub {
    text-align: center;
    color: #7a3a55;
    font-size: 0.95rem;
    margin-top: -0.5rem;
  }

  .activity-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 0.85rem;
    width: 100%;
  }

  .activity-card {
    background: #fff;
    border: 2.5px solid #f2d9e4;
    border-radius: 20px;
    padding: 1.2rem 1rem;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s;
    box-shadow: 0 2px 12px rgba(255,107,157,0.06);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
  }
  .activity-card:hover {
    border-color: var(--pink);
    transform: translateY(-3px);
    box-shadow: 0 8px 25px rgba(255,61,119,0.15);
  }
  .activity-card.selected {
    background: linear-gradient(135deg, #fff0f6, #ffe4ef);
    border-color: var(--rose);
    box-shadow: 0 8px 25px rgba(255,61,119,0.25);
    transform: translateY(-3px);
  }

  .activity-emoji { font-size: 2.2rem; }
  .activity-name {
    font-size: 0.88rem;
    font-weight: 500;
    color: var(--text);
  }

  .btn-next {
    background: linear-gradient(135deg, var(--pink), var(--rose));
    color: #fff;
    border: none;
    padding: 1rem 3rem;
    border-radius: 100px;
    font-size: 1rem;
    font-family: 'DM Sans', sans-serif;
    font-weight: 500;
    cursor: pointer;
    box-shadow: 0 8px 30px rgba(255,61,119,0.35);
    transition: all 0.2s;
    opacity: 0.4;
    pointer-events: none;
  }
  .btn-next.active {
    opacity: 1;
    pointer-events: all;
  }
  .btn-next.active:hover {
    transform: scale(1.04);
    box-shadow: 0 12px 40px rgba(255,61,119,0.5);
  }

  /* ---- SCREEN 3: DATE & TIME ---- */
  #screen-datetime {
    gap: 1.8rem;
    max-width: 420px;
    margin: 0 auto;
  }

  .datetime-card {
    background: #fff;
    border: 2.5px solid #f2d9e4;
    border-radius: 24px;
    padding: 1.8rem 1.5rem;
    width: 100%;
    box-shadow: 0 4px 20px rgba(255,107,157,0.08);
  }

  .datetime-label {
    font-size: 0.8rem;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--pink);
    margin-bottom: 0.6rem;
  }

  .datetime-card input[type="date"],
  .datetime-card input[type="time"] {
    width: 100%;
    border: none;
    outline: none;
    font-family: 'DM Sans', sans-serif;
    font-size: 1.4rem;
    font-weight: 500;
    color: var(--dark);
    background: transparent;
    cursor: pointer;
  }

  /* ---- SCREEN 4: CONFIRM ---- */
  #screen-confirm {
    text-align: center;
    gap: 1.5rem;
  }

  .confirm-emoji {
    font-size: 5rem;
    animation: bounce 0.8s ease infinite alternate;
  }
  @keyframes bounce {
    from { transform: translateY(0); }
    to   { transform: translateY(-12px); }
  }

  .confirm-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.8rem, 7vw, 2.8rem);
    font-weight: 700;
    color: var(--dark);
    line-height: 1.2;
  }
  .confirm-title span { color: var(--pink); font-style: italic; }

  .confirm-card {
    background: linear-gradient(135deg, #fff0f6, #ffe4ef);
    border: 2px solid #f5c8d8;
    border-radius: 24px;
    padding: 1.5rem 2rem;
    width: 100%;
    max-width: 340px;
    text-align: left;
    box-shadow: 0 8px 30px rgba(255,61,119,0.12);
  }

  .confirm-row {
    display: flex;
    align-items: center;
    gap: 0.8rem;
    padding: 0.6rem 0;
    border-bottom: 1px solid rgba(255,107,157,0.15);
  }
  .confirm-row:last-child { border-bottom: none; }
  .confirm-row-icon { font-size: 1.3rem; }
  .confirm-row-text { font-size: 0.95rem; color: var(--text); }
  .confirm-row-text strong { font-weight: 600; }

  .confetti-container {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 999;
    overflow: hidden;
  }
  .confetti-piece {
    position: absolute;
    top: -20px;
    width: 10px;
    height: 10px;
    border-radius: 2px;
    animation: confettiFall linear forwards;
  }
  @keyframes confettiFall {
    to {
      transform: translateY(110vh) rotate(720deg);
      opacity: 0;
    }
  }

  /* ---- SHARED ---- */
  .pill-tag {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    background: var(--blush);
    color: var(--rose);
    font-size: 0.75rem;
    font-weight: 500;
    padding: 0.35rem 0.9rem;
    border-radius: 100px;
    text-transform: uppercase;
    letter-spacing: 0.07em;
  }

  .no-run { animation: runAway 0.3s ease forwards; }
  @keyframes runAway {
    to { transform: translate(var(--rx), var(--ry)); }
  }
</style>
</head>
<body>

<!-- Floating hearts background -->
<div class="hearts-bg" id="heartsBg"></div>

<!-- Confetti container -->
<div class="confetti-container" id="confettiContainer"></div>

<!-- ========== SCREEN 1: Ask ========== -->
<div class="screen active" id="screen-ask">
  <div class="pill-tag">💌 Máš správu</div>
  <div class="big-emoji">🌸</div>
  <h1 class="ask-title">Chceš ísť<br>so mnou na<br><span>rande?</span></h1>
  <p class="ask-sub">Mám pre teba niečo výnimočné naplánované... 🥹</p>
  <div class="btn-group">
    <button class="btn-yes" onclick="goToActivity()">💖 Áno, idem!</button>
    <button class="btn-no" id="btnNo" onmouseenter="runAway(this)" ontouchstart="runAway(this)">Nie... 😶</button>
  </div>
</div>

<!-- ========== SCREEN 2: Choose Activity ========== -->
<div class="screen" id="screen-activity">
  <div class="pill-tag">🎉 Skvelé!</div>
  <h2 class="section-title">Čo si dáme<br><span>dnes?</span></h2>
  <p class="section-sub">Vyber jednu aktivitu pre naše rande ✨</p>

  <div class="activity-grid">
    <div class="activity-card" onclick="selectActivity(this, 'Kino')">
      <span class="activity-emoji">🎬</span>
      <span class="activity-name">Kino</span>
    </div>
    <div class="activity-card" onclick="selectActivity(this, 'Wellness')">
      <span class="activity-emoji">🧖‍♀️</span>
      <span class="activity-name">Wellness</span>
    </div>
    <div class="activity-card" onclick="selectActivity(this, 'Prechádzka s Kirou')">
      <span class="activity-emoji">🐾</span>
      <span class="activity-name">Prechádzka s Kirou</span>
    </div>
    <div class="activity-card" onclick="selectActivity(this, 'Bike')">
      <span class="activity-emoji">🚴</span>
      <span class="activity-name">Bike</span>
    </div>
    <div class="activity-card" onclick="selectActivity(this, 'Tenis')">
      <span class="activity-emoji">🎾</span>
      <span class="activity-name">Tenis</span>
    </div>
    <div class="activity-card" onclick="selectActivity(this, 'Padel')">
      <span class="activity-emoji">🏸</span>
      <span class="activity-name">Padel</span>
    </div>
    <div class="activity-card" onclick="selectActivity(this, 'Venčenie psíkov')">
      <span class="activity-emoji">🐶</span>
      <span class="activity-name">Venčenie psíkov</span>
    </div>
    <div class="activity-card" onclick="selectActivity(this, 'DIY')">
      <span class="activity-emoji">🛠️</span>
      <span class="activity-name">DIY</span>
    </div>
  </div>

  <button class="btn-next" id="btnNextActivity" onclick="goToDatetime()">Ďalej →</button>
</div>

<!-- ========== SCREEN 3: Date & Time ========== -->
<div class="screen" id="screen-datetime">
  <div class="pill-tag">📅 Naplánujme to</div>
  <h2 class="section-title">Kedy sa<br><span>stretneme?</span></h2>

  <div class="datetime-card">
    <div class="datetime-label">📅 Dátum</div>
    <input type="date" id="inputDate" min="">
  </div>

  <div class="datetime-card">
    <div class="datetime-label">🕐 Čas začiatku</div>
    <input type="time" id="inputTime" value="18:00">
  </div>

  <button class="btn-next active" onclick="goToConfirm()">Potvrdiť rande 💕</button>
</div>

<!-- ========== SCREEN 4: Confirm ========== -->
<div class="screen" id="screen-confirm">
  <div class="confirm-emoji">🎊</div>
  <h2 class="confirm-title">Je to<br><span>dohodnuté!</span></h2>
  <p style="color:#7a3a55; font-size:0.95rem;">Nemôžem sa dočkať 🥰</p>

  <div class="confirm-card">
    <div class="confirm-row">
      <span class="confirm-row-icon">🎭</span>
      <span class="confirm-row-text">Aktivita: <strong id="confirmActivity"></strong></span>
    </div>
    <div class="confirm-row">
      <span class="confirm-row-icon">📅</span>
      <span class="confirm-row-text">Dátum: <strong id="confirmDate"></strong></span>
    </div>
    <div class="confirm-row">
      <span class="confirm-row-icon">🕐</span>
      <span class="confirm-row-text">Čas: <strong id="confirmTime"></strong></span>
    </div>
  </div>

  <p style="font-size:0.85rem; color:#b07090; font-style:italic;" id="confirmNote">Posielam ti správu... 💌</p>
  <p style="font-size:0.85rem; color:#4caf50; font-style:italic; display:none;" id="confirmSent">✅ Notifikácia odoslaná na email!</p>
  <p style="font-size:0.85rem; color:#e57373; font-style:italic; display:none;" id="confirmError">⚠️ Email sa nepodarilo odoslať, ale rande je dohodnuté! 🌸</p>
</div>

<script>
  let chosenActivity = '';

  // ---- Floating hearts ----
  const heartsBg = document.getElementById('heartsBg');
  const heartChars = ['🤍','💗','🌸','💕','✨','🫶','💓','🌷'];
  function spawnHeart() {
    const el = document.createElement('div');
    el.className = 'heart-float';
    el.textContent = heartChars[Math.floor(Math.random() * heartChars.length)];
    el.style.left = Math.random() * 100 + 'vw';
    el.style.fontSize = (0.8 + Math.random() * 1.2) + 'rem';
    const dur = 6 + Math.random() * 8;
    el.style.animationDuration = dur + 's';
    el.style.animationDelay = Math.random() * 3 + 's';
    heartsBg.appendChild(el);
    setTimeout(() => el.remove(), (dur + 3) * 1000);
  }
  setInterval(spawnHeart, 800);
  for(let i=0; i<5; i++) setTimeout(spawnHeart, i*300);

  // ---- Set min date ----
  const today = new Date().toISOString().split('T')[0];
  document.getElementById('inputDate').min = today;
  document.getElementById('inputDate').value = today;

  // ---- Run away "Nie" button ----
  function runAway(btn) {
    const vw = window.innerWidth;
    const vh = window.innerHeight;
    const rect = btn.getBoundingClientRect();
    const maxX = Math.min(vw - rect.right, 150) * (Math.random() > 0.5 ? 1 : -1);
    const maxY = Math.min(vh - rect.bottom, 120) * (Math.random() > 0.5 ? 1 : -1);
    btn.style.setProperty('--rx', maxX + 'px');
    btn.style.setProperty('--ry', maxY + 'px');
    btn.classList.remove('no-run');
    void btn.offsetWidth;
    btn.classList.add('no-run');
    setTimeout(() => {
      btn.style.setProperty('--rx', '0px');
      btn.style.setProperty('--ry', '0px');
      btn.classList.remove('no-run');
    }, 400);
  }

  // ---- Navigation ----
  function showScreen(id) {
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    window.scrollTo(0,0);
  }

  function goToActivity() {
    showScreen('screen-activity');
  }

  function selectActivity(card, name) {
    document.querySelectorAll('.activity-card').forEach(c => c.classList.remove('selected'));
    card.classList.add('selected');
    chosenActivity = name;
    document.getElementById('btnNextActivity').classList.add('active');
  }

  function goToDatetime() {
    if (!chosenActivity) return;
    showScreen('screen-datetime');
  }

  function goToConfirm() {
    const dateVal = document.getElementById('inputDate').value;
    const timeVal = document.getElementById('inputTime').value;
    if (!dateVal || !timeVal) return;

    // Format date
    const [y,m,d] = dateVal.split('-');
    const months = ['januára','februára','marca','apríla','mája','júna','júla','augusta','septembra','októbra','novembra','decembra'];
    const formattedDate = `${parseInt(d)}. ${months[parseInt(m)-1]} ${y}`;

    document.getElementById('confirmActivity').textContent = chosenActivity;
    document.getElementById('confirmDate').textContent = formattedDate;
    document.getElementById('confirmTime').textContent = timeVal;

    showScreen('screen-confirm');
    setTimeout(launchConfetti, 300);

    // Send email notification via EmailJS
    const templateParams = {
      activity: chosenActivity,
      date: formattedDate,
      time: timeVal,
      to_email: 'matus.hazda@gmail.com'
    };

    emailjs.send('service_b24hhia', 'template_kukd9hq', templateParams)
      .then(() => {
        document.getElementById('confirmNote').style.display = 'none';
        document.getElementById('confirmSent').style.display = 'block';
      })
      .catch(() => {
        document.getElementById('confirmNote').style.display = 'none';
        document.getElementById('confirmError').style.display = 'block';
      });
  }

  // ---- Confetti ----
  function launchConfetti() {
    const container = document.getElementById('confettiContainer');
    const colors = ['#ff6b9d','#ff3d77','#f5c842','#ffe0ec','#a8edea','#fed6e3'];
    for (let i = 0; i < 80; i++) {
      const el = document.createElement('div');
      el.className = 'confetti-piece';
      el.style.left = Math.random() * 100 + 'vw';
      el.style.background = colors[Math.floor(Math.random() * colors.length)];
      el.style.width = (6 + Math.random() * 8) + 'px';
      el.style.height = (6 + Math.random() * 8) + 'px';
      el.style.borderRadius = Math.random() > 0.5 ? '50%' : '2px';
      const dur = 2 + Math.random() * 2;
      el.style.animationDuration = dur + 's';
      el.style.animationDelay = Math.random() * 1 + 's';
      container.appendChild(el);
      setTimeout(() => el.remove(), (dur + 2) * 1000);
    }
  }
</script>
</body>
</html>
