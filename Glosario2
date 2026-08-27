<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Glosario Interactivo — Desarrollo Embrionario y Fetal</title>
<style>
  :root{
    --bg-0:#0f1222;
    --bg-1:#171b34;
    --panel:#1d2140;
    --panel-2:#242a4f;
    --ink:#eef0fb;
    --ink-dim:#a8adcf;
    --accent:#7c8cff;
    --accent-2:#ff8fb3;
    --accent-3:#5eead4;
    --good:#4ade80;
    --bad:#f87171;
    --warn:#fbbf24;
    --radius:18px;
    --shadow: 0 20px 50px -20px rgba(0,0,0,.6);
    font-size: 16px;
  }
  *{box-sizing:border-box;}
  html,body{height:100%;}
  body{
    margin:0;
    font-family: "Segoe UI", Avenir, "Helvetica Neue", Arial, sans-serif;
    color:var(--ink);
    background:
      radial-gradient(1200px 700px at 15% -10%, rgba(124,140,255,.25), transparent 60%),
      radial-gradient(900px 600px at 100% 0%, rgba(255,143,179,.18), transparent 55%),
      radial-gradient(900px 700px at 50% 120%, rgba(94,234,212,.15), transparent 55%),
      linear-gradient(180deg, var(--bg-0), var(--bg-1));
    min-height:100%;
    display:flex;
    flex-direction:column;
    align-items:center;
    padding: 18px 16px 30px;
  }
  .wrap{ width:100%; max-width: 980px; }
  header{ text-align:center; margin-bottom: 10px; position:relative; padding: 0 44px; }
  header h1{
    font-size: clamp(1.3rem, 2.4vw, 1.9rem);
    margin: 0 0 4px;
    background: linear-gradient(90deg, var(--accent), var(--accent-2) 60%, var(--accent-3));
    -webkit-background-clip:text;
    background-clip:text;
    color:transparent;
    font-weight:800;
    letter-spacing:.2px;
  }
  header p{ margin:0; color:var(--ink-dim); font-size:.88rem; }

  .help-btn{
    appearance:none; cursor:pointer; position:absolute; top:0; right:0;
    width:34px; height:34px; border-radius:50%;
    background: var(--panel); color:var(--ink);
    border:1px solid rgba(255,255,255,.12);
    font-size:1rem; font-weight:800; line-height:1;
    display:flex; align-items:center; justify-content:center;
    transition: all .15s ease;
  }
  .help-btn:hover{ background: var(--panel-2); border-color: rgba(124,140,255,.5); transform: scale(1.06); }

  .modal-overlay{
    display:none; position:fixed; inset:0; background:rgba(8,9,20,.65);
    backdrop-filter: blur(3px); z-index:80; align-items:center; justify-content:center; padding:20px;
  }
  .modal-overlay.open{ display:flex; }
  .modal{
    width:100%; max-width:560px; max-height:85vh; overflow-y:auto;
    background: linear-gradient(180deg, var(--panel), var(--panel-2));
    border:1px solid rgba(255,255,255,.08); border-radius:20px;
    box-shadow: var(--shadow); padding: 26px 26px 22px;
  }
  .modal h2{ margin:0 0 14px; font-size:1.25rem; }
  .modal h3{ margin: 16px 0 6px; font-size:.95rem; color: var(--accent-3); }
  .modal p{ margin: 0 0 4px; color:var(--ink-dim); font-size:.9rem; line-height:1.5; }
  .modal .modal-close{ display:block; margin: 20px auto 0; }

  nav.tabs{
    display:flex;
    gap:8px;
    justify-content:center;
    flex-wrap:wrap;
    margin: 14px 0;
  }
  nav.tabs button{
    appearance:none;
    border:1px solid rgba(255,255,255,.08);
    background: var(--panel);
    color:var(--ink-dim);
    padding: 10px 18px;
    border-radius: 999px;
    font-size:.92rem;
    font-weight:600;
    cursor:pointer;
    transition: all .18s ease;
    display:flex;
    align-items:center;
    gap:8px;
  }
  nav.tabs button:hover{ color:var(--ink); border-color: rgba(255,255,255,.2); }
  nav.tabs button.active{
    background: linear-gradient(135deg, var(--accent), #5b6bff);
    color:#0d0f1f;
    color:#fff;
    border-color:transparent;
    box-shadow: 0 8px 24px -10px rgba(124,140,255,.7);
  }

  .panel{
    background: linear-gradient(180deg, var(--panel), var(--panel-2));
    border:1px solid rgba(255,255,255,.06);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    padding: clamp(16px, 3.2vw, 26px);
    min-height: 420px;
  }

  .view{ display:none; animation: fadein .35s ease; }
  .view.active{ display:block; }
  @keyframes fadein{ from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:none;} }

  /* ---------- Flashcards ---------- */
  .fc-topbar{ display:flex; justify-content:space-between; align-items:center; gap:12px; margin-bottom:14px; flex-wrap:wrap;}
  .fc-progress{ flex:1; min-width:160px; height:8px; background:rgba(255,255,255,.08); border-radius:999px; overflow:hidden;}
  .fc-progress > div{ height:100%; background:linear-gradient(90deg,var(--accent-3),var(--accent)); border-radius:999px; transition: width .35s ease;}
  .fc-stats{ font-size:.85rem; color:var(--ink-dim); white-space:nowrap;}
  .fc-stage{ display:flex; flex-direction:column; align-items:center; gap:14px; }
  .card-scene{ perspective: 1400px; width:100%; max-width:560px; height:240px; }
  .card{
    position:relative; width:100%; height:100%;
    transform-style:preserve-3d; transition: transform .55s cubic-bezier(.2,.9,.25,1);
    cursor:pointer;
  }
  .card.flipped{ transform: rotateY(180deg); }
  .face{
    position:absolute; inset:0; backface-visibility:hidden;
    border-radius: 20px; display:flex; align-items:center; justify-content:center;
    text-align:center; padding: 22px; font-weight:600;
    box-shadow: 0 18px 40px -18px rgba(0,0,0,.6);
  }
  .face.front{
    background: linear-gradient(135deg, #2b3168, #1c2048);
    border: 1px solid rgba(124,140,255,.35);
    font-size: clamp(1.4rem, 4vw, 2rem);
    color:var(--ink);
  }
  .face.back{
    background: linear-gradient(135deg, #223a3a, #17233a);
    border: 1px solid rgba(94,234,212,.35);
    transform: rotateY(180deg);
    font-size: clamp(1rem, 2.6vw, 1.2rem);
    font-weight:500;
    line-height:1.45;
    color:var(--ink);
  }
  .hint{ color:var(--ink-dim); font-size:.82rem; }
  .fc-controls{ display:flex; gap:12px; flex-wrap:wrap; justify-content:center; }
  .btn{
    appearance:none; border:none; cursor:pointer; border-radius:14px;
    padding: 12px 20px; font-size:.95rem; font-weight:700;
    transition: transform .12s ease, box-shadow .12s ease; color:#fff;
  }
  .btn:active{ transform: scale(.96); }
  .btn-know{ background: linear-gradient(135deg,#22c55e,#16a34a); box-shadow: 0 10px 24px -12px rgba(34,197,94,.7); }
  .btn-again{ background: linear-gradient(135deg,#f87171,#dc2626); box-shadow: 0 10px 24px -12px rgba(248,113,113,.7);}
  .btn-ghost{ background: rgba(255,255,255,.08); color:var(--ink); }
  .btn-ghost:hover{ background: rgba(255,255,255,.14); }
  .btn-primary{ background: linear-gradient(135deg, var(--accent), #5b6bff); box-shadow: 0 10px 24px -12px rgba(124,140,255,.7);}

  .celebrate{ text-align:center; padding: 20px 10px; }
  .celebrate .big{ font-size: 2.6rem; margin-bottom:4px; }
  .celebrate h2{ margin:0 0 6px; }
  .celebrate p{ color:var(--ink-dim); margin:0 0 14px; }

  /* ---------- Quiz ---------- */
  .quiz-head{ display:flex; justify-content:space-between; align-items:center; margin-bottom:14px; flex-wrap:wrap; gap:10px;}
  .quiz-pill{ background: rgba(255,255,255,.07); border-radius:999px; padding:6px 14px; font-size:.82rem; color:var(--ink-dim); }
  .quiz-q{ font-size: clamp(1.05rem,2.6vw,1.3rem); font-weight:700; margin: 6px 0 16px; line-height:1.4; }
  .quiz-q .term-badge{
    display:inline-block; margin-top:8px; padding:6px 14px; border-radius:10px;
    background: linear-gradient(135deg, rgba(124,140,255,.25), rgba(255,143,179,.2));
    border:1px solid rgba(124,140,255,.4); font-size:1.15em;
  }
  .options{ display:grid; gap:12px; }
  .opt{
    text-align:left; padding:14px 16px; border-radius:14px; cursor:pointer;
    background: rgba(255,255,255,.05); border:1px solid rgba(255,255,255,.08);
    color:var(--ink); font-size:.95rem; line-height:1.4; transition: all .15s ease;
  }
  .opt:hover{ background: rgba(255,255,255,.09); border-color: rgba(124,140,255,.4); }
  .opt.correct{ background: rgba(74,222,128,.18); border-color: var(--good); }
  .opt.wrong{ background: rgba(248,113,113,.18); border-color: var(--bad); }
  .opt.disabled{ pointer-events:none; opacity:.85; }
  .quiz-foot{ display:flex; justify-content:space-between; align-items:center; margin-top:22px; gap:10px; flex-wrap:wrap;}
  .feedback{ min-height:1.3em; font-weight:700; font-size:.92rem; }
  .feedback.good{ color:var(--good); }
  .feedback.bad{ color:var(--bad); }

  .score-ring-wrap{ display:flex; flex-direction:column; align-items:center; gap:10px; margin: 10px 0 24px;}
  .review-list{ display:grid; gap:10px; margin-top:10px; text-align:left; }
  .review-item{ background:rgba(255,255,255,.05); border-radius:12px; padding:12px 14px; font-size:.88rem; }
  .review-item b{ color:var(--accent-3); }
  .review-item .miss{ color:var(--accent-2); }

  /* ---------- Matching ---------- */
  .match-head{ display:flex; justify-content:space-between; align-items:center; margin-bottom:16px; flex-wrap:wrap; gap:10px;}
  .match-grid{ display:grid; grid-template-columns: repeat(2, 1fr); gap: 20px; }
  @media (max-width: 720px){ .match-grid{ grid-template-columns: 1fr; } }
  .match-col h3{ margin: 0 0 10px; font-size:.85rem; text-transform:uppercase; letter-spacing:.08em; color:var(--ink-dim); }
  .match-items{ display:flex; flex-direction:column; gap:10px; }
  .match-item{
    padding: 12px 14px; border-radius:12px; cursor:pointer; font-size:.9rem; line-height:1.35;
    background: rgba(255,255,255,.05); border:1px solid rgba(255,255,255,.09);
    transition: all .15s ease; user-select:none;
  }
  .match-item:hover{ border-color: rgba(124,140,255,.5); }
  .match-item.selected{ border-color: var(--accent); background: rgba(124,140,255,.18); }
  .match-item.matched{ background: rgba(74,222,128,.14); border-color: var(--good); color: var(--ink-dim); cursor:default; }
  .match-item.shake{ animation: shake .38s ease; border-color: var(--bad); background: rgba(248,113,113,.14); }
  @keyframes shake{ 0%,100%{transform:translateX(0);} 25%{transform:translateX(-6px);} 75%{transform:translateX(6px);} }
  .match-stats{ display:flex; gap:18px; font-size:.85rem; color:var(--ink-dim); }
  .match-stats b{ color:var(--ink); }

  .confetti{ position:fixed; inset:0; pointer-events:none; overflow:hidden; z-index:50; }
  .confetti span{
    position:absolute; top:-10px; width:8px; height:14px; opacity:.9;
    animation: fall linear forwards;
  }
  @keyframes fall{ to{ transform: translateY(110vh) rotate(540deg); opacity:0; } }
</style>
</head>
<body>
<div class="wrap">
  <header>
    <button class="help-btn" id="helpBtn" title="¿Cómo funciona?" aria-label="¿Cómo funciona esta plataforma?">?</button>
    <h1>GLOSARIO INTERACTIVO</h1>
    <p>DESARROLLO EMBRIONARIO Y FETAL: conceptos clave</p>
  </header>

  <nav class="tabs">
    <button data-view="flash" class="active">🃏 Tarjetas</button>
    <button data-view="quiz">🧠 Quiz</button>
    <button data-view="match">🔗 Emparejar</button>
  </nav>

  <div class="panel">

    <!-- FLASHCARDS -->
    <section id="flash" class="view active">
      <div class="fc-topbar">
        <div class="fc-progress"><div id="fcProgressBar" style="width:0%"></div></div>
        <div class="fc-stats" id="fcStats">0 / 22</div>
      </div>

      <div id="fcStage" class="fc-stage">
        <div class="card-scene">
          <div class="card" id="fcCard">
            <div class="face front" id="fcFront">Etapa embrionaria</div>
            <div class="face back" id="fcBack">Definición aquí</div>
          </div>
        </div>
        <div class="hint">Toca la tarjeta para ver la definición</div>
        <div class="fc-controls">
          <button class="btn btn-again" id="fcAgain">🔁 Repasar de nuevo</button>
          <button class="btn btn-know" id="fcKnow">✅ Ya lo sé</button>
        </div>
        <button class="btn btn-ghost" id="fcShuffle">🔀 Barajar mazo</button>
      </div>

      <div id="fcDone" class="celebrate" style="display:none;">
        <div class="big">🎉</div>
        <h2>¡Completaste el mazo!</h2>
        <p id="fcDoneText">Dominaste todas las tarjetas.</p>
        <button class="btn btn-primary" id="fcRestart">Empezar de nuevo</button>
      </div>
    </section>

    <!-- QUIZ -->
    <section id="quiz" class="view">
      <div id="quizPlay">
        <div class="quiz-head">
          <div class="quiz-pill" id="quizProgress">Pregunta 1 / 22</div>
          <div class="quiz-pill">✅ <span id="quizScore">0</span> correctas</div>
        </div>
        <div class="quiz-q" id="quizQuestion"></div>
        <div class="options" id="quizOptions"></div>
        <div class="quiz-foot">
          <div class="feedback" id="quizFeedback"></div>
          <button class="btn btn-primary" id="quizNext" style="display:none;">Siguiente →</button>
        </div>
      </div>

      <div id="quizDone" class="celebrate" style="display:none;">
        <div class="big" id="quizBigEmoji">🏆</div>
        <h2 id="quizDoneTitle">¡Quiz completado!</h2>
        <div class="score-ring-wrap">
          <p id="quizFinalScore" style="font-size:1.6rem; font-weight:800; margin:0;">22 / 22</p>
          <p id="quizFinalMsg" style="color:var(--ink-dim); margin:0;">Excelente dominio del tema</p>
        </div>
        <div id="quizReview" class="review-list"></div>
        <div style="margin-top:20px;">
          <button class="btn btn-primary" id="quizRestart">Intentar de nuevo</button>
        </div>
      </div>
    </section>

    <!-- MATCHING -->
    <section id="match" class="view">
      <div id="matchPlay">
        <div class="match-head">
          <div class="match-stats">
            <span>Pares: <b id="matchPairs">0/6</b></span>
            <span>Intentos: <b id="matchTries">0</b></span>
            <span>Tiempo: <b id="matchTime">0s</b></span>
          </div>
          <button class="btn btn-ghost" id="matchReshuffle">🔀 Nueva ronda</button>
        </div>
        <div class="match-grid">
          <div class="match-col">
            <h3>Términos</h3>
            <div class="match-items" id="matchTerms"></div>
          </div>
          <div class="match-col">
            <h3>Definiciones</h3>
            <div class="match-items" id="matchDefs"></div>
          </div>
        </div>
      </div>

      <div id="matchDone" class="celebrate" style="display:none;">
        <div class="big">✨</div>
        <h2>¡Ronda completada!</h2>
        <p id="matchDoneText"></p>
        <button class="btn btn-primary" id="matchRestart">Jugar otra ronda</button>
      </div>
    </section>

  </div>

</div>

<div class="modal-overlay" id="helpOverlay">
  <div class="modal">
    <h2>¿Cómo funciona esta plataforma? 🤔</h2>
    <p>Usa las tres pestañas de arriba para practicar los 22 conceptos de tres formas distintas. Tu progreso se guarda solo mientras tienes esta página abierta.</p>

    <h3>🃏 Tarjetas</h3>
    <p>Toca la tarjeta para voltearla y ver la definición. Si ya te la sabes, pulsa "Ya lo sé" y sale del mazo; si necesitas repasarla, pulsa "Repasar de nuevo" y vuelve más adelante. "Barajar mazo" cambia el orden.</p>

    <h3>🧠 Quiz</h3>
    <p>Lee el término y elige la definición correcta entre las opciones. Verás al instante si acertaste y, al final, un resumen con lo que debes repasar.</p>

    <h3>🔗 Emparejar</h3>
    <p>Selecciona un término y luego su definición para formar la pareja. Completa los 6 pares con la menor cantidad de intentos y en el menor tiempo posible. "Nueva ronda" elige otros conceptos al azar.</p>

    <button class="btn btn-primary modal-close" id="helpClose">Entendido</button>
  </div>
</div>

<script>
/* ---------------- Data ---------------- */
const TERMS = [
  {t:"Etapa embrionaria", d:"Periodo que se extiende desde la implantación del blastocisto en el útero hasta el final de la octava semana después de la fecundación."},
  {t:"Gastrulación", d:"Proceso por el cual se generan las tres capas celulares principales del embrión (ectodermo, mesodermo, endodermo)."},
  {t:"Ectodermo", d:"Capa externa que da origen al sistema nervioso y epidermis."},
  {t:"Mesodermo", d:"Capa media que da origen a los músculos, esqueleto, tejido conectivo, sistema circulatorio, excretor urinario, gónadas, glándulas suprarrenales y vasos."},
  {t:"Endodermo", d:"Capa interna que da origen al sistema digestivo, intestinos, hígado, páncreas, pulmones, entre otros."},
  {t:"Neurulación", d:"Proceso mediante el cual se forma el tubo neural."},
  {t:"Neuroblasto", d:"Célula neural primitiva."},
  {t:"Epitelio", d:"Tejido celular que reviste al organismo."},
  {t:"Neuroepitelio", d:"Tejido formado por células, que reviste lo que será el sistema nervioso."},
  {t:"Neurogénesis", d:"Procesos mediante los cuales las células nerviosas desarrollan sus características especializadas."},
  {t:"Proliferación celular", d:"Proceso por el cual se generan los neuroblastos o células neurales primitivas (neuronas, células gliales)."},
  {t:"Migración celular", d:"Proceso mediante el cual los neuroblastos empiezan a desplazarse hasta sus destinos."},
  {t:"Diferenciación celular", d:"Proceso por el cual las células comienzan a adquirir la apariencia distintiva de las neuronas características de sus respectivas regiones."},
  {t:"Células gliales", d:"Conforman tejido en el que se encuentran las neuronas."},
  {t:"Neurona", d:"Unidad básica estructural del sistema nervioso."},
  {t:"Sinapsis", d:"Unión entre dos neuronas."},
  {t:"Sinaptogénesis", d:"Proceso por el cual se forman nuevas conexiones / sinapsis entre las neuronas."},
  {t:"Axón, dendritas y espinas dendríticas", d:"Apéndices de la neurona que, al aumentar su superficie de contacto, le permiten establecer conexiones con otras neuronas."},
  {t:"Apoptosis", d:"Mecanismo natural y necesario para esculpir la estructura y funcionalidad del sistema."},
  {t:"Formación de vesículas", d:"Proceso por el cual se generan las vesículas primordiales del encéfalo."},
  {t:"Etapa fetal", d:"Periodo que se extiende desde las 8-12 semanas hasta el nacimiento."},
  {t:"Testosterona", d:"Hormona cuya función básica es el desarrollo de las glándulas genitales y otros rasgos masculinos. Tiene un papel de gran importancia en el desarrollo del cerebro de ambos sexos."},
];

function shuffle(arr){
  const a = arr.slice();
  for(let i=a.length-1;i>0;i--){
    const j = Math.floor(Math.random()*(i+1));
    [a[i],a[j]] = [a[j],a[i]];
  }
  return a;
}

function fireConfetti(){
  const colors = ['#7c8cff','#ff8fb3','#5eead4','#fbbf24','#4ade80'];
  const holder = document.createElement('div');
  holder.className = 'confetti';
  document.body.appendChild(holder);
  for(let i=0;i<60;i++){
    const s = document.createElement('span');
    s.style.left = Math.random()*100 + 'vw';
    s.style.background = colors[Math.floor(Math.random()*colors.length)];
    s.style.animationDuration = (2 + Math.random()*1.5) + 's';
    s.style.animationDelay = (Math.random()*0.4) + 's';
    s.style.borderRadius = Math.random() > .5 ? '50%' : '2px';
    holder.appendChild(s);
  }
  setTimeout(()=> holder.remove(), 4000);
}

/* ---------------- Help modal ---------------- */
const helpOverlay = document.getElementById('helpOverlay');
document.getElementById('helpBtn').addEventListener('click', ()=> helpOverlay.classList.add('open'));
document.getElementById('helpClose').addEventListener('click', ()=> helpOverlay.classList.remove('open'));
helpOverlay.addEventListener('click', (e)=>{ if(e.target === helpOverlay) helpOverlay.classList.remove('open'); });
document.addEventListener('keydown', (e)=>{ if(e.key === 'Escape') helpOverlay.classList.remove('open'); });

/* ---------------- Tabs ---------------- */
const tabButtons = document.querySelectorAll('nav.tabs button');
tabButtons.forEach(btn=>{
  btn.addEventListener('click', ()=>{
    tabButtons.forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
    document.getElementById(btn.dataset.view).classList.add('active');
  });
});

/* ---------------- Flashcards ---------------- */
let fcDeck = [];
let fcIndex = 0;
let fcMastered = 0;
let fcTotal = TERMS.length;

function fcInit(){
  fcDeck = shuffle(TERMS);
  fcIndex = 0;
  fcMastered = 0;
  document.getElementById('fcDone').style.display = 'none';
  document.getElementById('fcStage').style.display = 'flex';
  fcRender();
}

function fcRender(){
  const card = document.getElementById('fcCard');
  card.classList.remove('flipped');
  const item = fcDeck[fcIndex];
  document.getElementById('fcFront').textContent = item.t;
  document.getElementById('fcBack').textContent = item.d;
  document.getElementById('fcStats').textContent = `${fcMastered} / ${fcTotal} dominadas`;
  document.getElementById('fcProgressBar').style.width = (fcMastered/fcTotal*100) + '%';
}

document.getElementById('fcCard').addEventListener('click', ()=>{
  document.getElementById('fcCard').classList.toggle('flipped');
});

function fcAdvance(knew){
  if(knew){ fcMastered++; fcDeck.splice(fcIndex,1); }
  else { fcIndex++; }
  if(fcDeck.length === 0){
    document.getElementById('fcStage').style.display = 'none';
    document.getElementById('fcDone').style.display = 'block';
    document.getElementById('fcDoneText').textContent = `Dominaste las ${fcTotal} tarjetas. ¡Buen trabajo!`;
    fireConfetti();
    return;
  }
  if(fcIndex >= fcDeck.length) fcIndex = 0;
  fcRender();
}

document.getElementById('fcKnow').addEventListener('click', ()=> fcAdvance(true));
document.getElementById('fcAgain').addEventListener('click', ()=>{
  // move current card to the back of the deck for spaced repetition feel
  const [item] = fcDeck.splice(fcIndex,1);
  fcDeck.push(item);
  if(fcIndex >= fcDeck.length) fcIndex = 0;
  fcRender();
});
document.getElementById('fcShuffle').addEventListener('click', ()=>{
  fcDeck = shuffle(fcDeck);
  fcIndex = 0;
  fcRender();
});
document.getElementById('fcRestart').addEventListener('click', fcInit);

/* ---------------- Quiz ---------------- */
let quizOrder = [];
let quizIdx = 0;
let quizScore = 0;
let quizMissed = [];
let quizAnswered = false;

function quizInit(){
  quizOrder = shuffle(TERMS);
  quizIdx = 0;
  quizScore = 0;
  quizMissed = [];
  document.getElementById('quizDone').style.display = 'none';
  document.getElementById('quizPlay').style.display = 'block';
  quizRender();
}

function quizRender(){
  quizAnswered = false;
  const item = quizOrder[quizIdx];
  document.getElementById('quizProgress').textContent = `Pregunta ${quizIdx+1} / ${quizOrder.length}`;
  document.getElementById('quizScore').textContent = quizScore;
  document.getElementById('quizFeedback').textContent = '';
  document.getElementById('quizFeedback').className = 'feedback';
  document.getElementById('quizNext').style.display = 'none';

  document.getElementById('quizQuestion').innerHTML =
    `¿Cuál es la definición correcta de:<br><span class="term-badge">${item.t}</span>`;

  // build 3 distractors + correct
  const others = shuffle(TERMS.filter(x=>x.t!==item.t)).slice(0,3);
  const options = shuffle([item, ...others]);

  const optsWrap = document.getElementById('quizOptions');
  optsWrap.innerHTML = '';
  options.forEach(opt=>{
    const div = document.createElement('div');
    div.className = 'opt';
    div.textContent = opt.d;
    div.addEventListener('click', ()=> quizAnswer(div, opt, item));
    optsWrap.appendChild(div);
  });
}

function quizAnswer(el, chosen, correctItem){
  if(quizAnswered) return;
  quizAnswered = true;
  const allOpts = document.querySelectorAll('#quizOptions .opt');
  allOpts.forEach(o=> o.classList.add('disabled'));

  const isCorrect = chosen.t === correctItem.t;
  if(isCorrect){
    el.classList.add('correct');
    quizScore++;
    document.getElementById('quizFeedback').textContent = '¡Correcto! ✅';
    document.getElementById('quizFeedback').className = 'feedback good';
  } else {
    el.classList.add('wrong');
    quizMissed.push({term: correctItem.t, def: correctItem.d});
    document.getElementById('quizFeedback').textContent = 'No es correcto ❌';
    document.getElementById('quizFeedback').className = 'feedback bad';
    allOpts.forEach(o=>{
      if(o.textContent === correctItem.d) o.classList.add('correct');
    });
  }
  document.getElementById('quizScore').textContent = quizScore;
  document.getElementById('quizNext').style.display = 'inline-block';
}

document.getElementById('quizNext').addEventListener('click', ()=>{
  quizIdx++;
  if(quizIdx >= quizOrder.length){
    quizFinish();
    return;
  }
  quizRender();
});

function quizFinish(){
  document.getElementById('quizPlay').style.display = 'none';
  document.getElementById('quizDone').style.display = 'block';
  document.getElementById('quizFinalScore').textContent = `${quizScore} / ${quizOrder.length}`;

  const pct = quizScore / quizOrder.length;
  let emoji = '🏆', msg = '¡Dominio excelente del tema!';
  if(pct < 0.5){ emoji = '📚'; msg = 'Sigue practicando, vas por buen camino.'; }
  else if(pct < 0.8){ emoji = '💪'; msg = '¡Buen trabajo! Repasa los que fallaste.'; }
  document.getElementById('quizBigEmoji').textContent = emoji;
  document.getElementById('quizFinalMsg').textContent = msg;

  const reviewWrap = document.getElementById('quizReview');
  reviewWrap.innerHTML = '';
  if(quizMissed.length === 0){
    const div = document.createElement('div');
    div.className = 'review-item';
    div.innerHTML = '🎉 No fallaste ninguna definición.';
    reviewWrap.appendChild(div);
  } else {
    quizMissed.forEach(m=>{
      const div = document.createElement('div');
      div.className = 'review-item';
      div.innerHTML = `<span class="miss">Repasar:</span> <b>${m.term}</b> — ${m.def}`;
      reviewWrap.appendChild(div);
    });
  }

  if(pct >= 0.8) fireConfetti();
}

document.getElementById('quizRestart').addEventListener('click', quizInit);

/* ---------------- Matching ---------------- */
const MATCH_SET_SIZE = 6;
let matchPool = [];
let matchTerms = [];
let matchDefs = [];
let matchSelectedTerm = null;
let matchSelectedDef = null;
let matchMatched = 0;
let matchTries = 0;
let matchTimer = null;
let matchSeconds = 0;

function matchInit(){
  clearInterval(matchTimer);
  matchSeconds = 0;
  matchTries = 0;
  matchMatched = 0;
  matchSelectedTerm = null;
  matchSelectedDef = null;
  document.getElementById('matchDone').style.display = 'none';
  document.getElementById('matchPlay').style.display = 'block';

  matchPool = shuffle(TERMS).slice(0, MATCH_SET_SIZE);
  matchTerms = shuffle(matchPool);
  matchDefs = shuffle(matchPool);

  renderMatchCols();
  updateMatchStats();

  matchTimer = setInterval(()=>{
    matchSeconds++;
    document.getElementById('matchTime').textContent = matchSeconds + 's';
  }, 1000);
}

function renderMatchCols(){
  const termsWrap = document.getElementById('matchTerms');
  const defsWrap = document.getElementById('matchDefs');
  termsWrap.innerHTML = '';
  defsWrap.innerHTML = '';

  matchTerms.forEach(item=>{
    const div = document.createElement('div');
    div.className = 'match-item';
    div.textContent = item.t;
    div.dataset.term = item.t;
    div.addEventListener('click', ()=> selectTerm(div, item));
    termsWrap.appendChild(div);
  });

  matchDefs.forEach(item=>{
    const div = document.createElement('div');
    div.className = 'match-item';
    div.textContent = item.d;
    div.dataset.term = item.t;
    div.addEventListener('click', ()=> selectDef(div, item));
    defsWrap.appendChild(div);
  });
}

function selectTerm(el, item){
  if(el.classList.contains('matched')) return;
  document.querySelectorAll('#matchTerms .match-item').forEach(i=>i.classList.remove('selected'));
  el.classList.add('selected');
  matchSelectedTerm = {el, item};
  tryMatch();
}
function selectDef(el, item){
  if(el.classList.contains('matched')) return;
  document.querySelectorAll('#matchDefs .match-item').forEach(i=>i.classList.remove('selected'));
  el.classList.add('selected');
  matchSelectedDef = {el, item};
  tryMatch();
}

function tryMatch(){
  if(!matchSelectedTerm || !matchSelectedDef) return;
  matchTries++;
  updateMatchStats();

  if(matchSelectedTerm.item.t === matchSelectedDef.item.t){
    matchSelectedTerm.el.classList.remove('selected');
    matchSelectedDef.el.classList.remove('selected');
    matchSelectedTerm.el.classList.add('matched');
    matchSelectedDef.el.classList.add('matched');
    matchMatched++;
    updateMatchStats();
    matchSelectedTerm = null;
    matchSelectedDef = null;

    if(matchMatched === MATCH_SET_SIZE){
      clearInterval(matchTimer);
      setTimeout(()=>{
        document.getElementById('matchPlay').style.display = 'none';
        document.getElementById('matchDone').style.display = 'block';
        document.getElementById('matchDoneText').textContent =
          `Emparejaste ${MATCH_SET_SIZE} conceptos en ${matchSeconds}s con ${matchTries} intentos.`;
        fireConfetti();
      }, 400);
    }
  } else {
    const t = matchSelectedTerm.el, d = matchSelectedDef.el;
    t.classList.add('shake'); d.classList.add('shake');
    setTimeout(()=>{
      t.classList.remove('selected','shake');
      d.classList.remove('selected','shake');
      matchSelectedTerm = null;
      matchSelectedDef = null;
    }, 420);
  }
}

function updateMatchStats(){
  document.getElementById('matchPairs').textContent = `${matchMatched}/${MATCH_SET_SIZE}`;
  document.getElementById('matchTries').textContent = matchTries;
}

document.getElementById('matchReshuffle').addEventListener('click', matchInit);
document.getElementById('matchRestart').addEventListener('click', matchInit);

/* ---------------- Init all ---------------- */
fcInit();
quizInit();
matchInit();
</script>
</body>
</html>
