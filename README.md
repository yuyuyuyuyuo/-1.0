# -1.0
英語学習
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="SpeakSnap">
<meta name="theme-color" content="#06060c">
<title>SpeakSnap — 英語学習トレーナー</title>
<link rel="manifest" href="data:application/json;base64,eyJuYW1lIjoiU3BlYWtTbmFwIiwic2hvcnRfbmFtZSI6IlNwZWFrU25hcCIsInN0YXJ0X3VybCI6Ii4iLCJkaXNwbGF5Ijoic3RhbmRhbG9uZSIsImJhY2tncm91bmRfY29sb3IiOiIjMDYwNjBjIiwidGhlbWVfY29sb3IiOiIjMDYwNjBjIn0=">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;500;600;700;800&family=JetBrains+Mono:wght@600;700&display=swap" rel="stylesheet">
<style>
/*═══════════════════════════════════════════
  DESIGN: "Neural Interface" — dark, glowing
═══════════════════════════════════════════*/
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
:root{
  --bg:#06060c;--bg2:#0c0c18;--surface:#111122;--surface2:#181830;
  --border:#1a1a35;--border-hi:#2a2a55;
  --text:#e4e2f0;--text2:#9896b0;--text3:#5c5a72;
  --mint:#00f0b5;--mint-dim:rgba(0,240,181,.12);--mint-glow:rgba(0,240,181,.3);
  --coral:#ff5678;--coral-dim:rgba(255,86,120,.12);--coral-glow:rgba(255,86,120,.3);
  --blue:#4d8eff;--blue-dim:rgba(77,142,255,.12);
  --gold:#ffc94d;
  --safe-t:env(safe-area-inset-top,20px);--safe-b:env(safe-area-inset-bottom,0px);
  --nav-h:68px;
}
html,body{height:100%;width:100%;overflow:hidden;background:var(--bg);color:var(--text);font-family:'Outfit',sans-serif;touch-action:manipulation;-webkit-user-select:none;user-select:none}

/* ─── Screen system ─── */
.screen{display:none;flex-direction:column;height:100dvh;padding:var(--safe-t) 16px 0;overflow:hidden}
.screen.active{display:flex}
.screen-body{flex:1;overflow-y:auto;-webkit-overflow-scrolling:touch;padding-bottom:calc(var(--nav-h) + var(--safe-b) + 12px)}
.screen-body::-webkit-scrollbar{display:none}

/* ─── Bottom Nav ─── */
.bottom-nav{
  position:fixed;bottom:0;left:0;right:0;
  height:calc(var(--nav-h) + var(--safe-b));padding-bottom:var(--safe-b);
  background:linear-gradient(180deg,rgba(6,6,12,.0) 0%,var(--bg) 25%);
  backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);
  display:none;justify-content:space-around;align-items:flex-start;padding-top:10px;
  z-index:90;
}
.bottom-nav.show{display:flex}
.nav-item{
  display:flex;flex-direction:column;align-items:center;gap:3px;
  cursor:pointer;padding:6px 16px;border-radius:12px;transition:background .2s;
  position:relative;
}
.nav-item .nav-icon{width:24px;height:24px;opacity:.45;transition:opacity .2s}
.nav-item .nav-label{font-size:10px;color:var(--text3);transition:color .2s;font-weight:600;letter-spacing:.5px}
.nav-item.active .nav-icon{opacity:1}
.nav-item.active .nav-label{color:var(--mint)}
.nav-item.active::after{
  content:'';position:absolute;top:-2px;left:50%;transform:translateX(-50%);
  width:20px;height:3px;border-radius:2px;background:var(--mint);
  box-shadow:0 0 12px var(--mint-glow);
}
.nav-badge{
  position:absolute;top:2px;right:8px;min-width:16px;height:16px;
  border-radius:8px;background:var(--coral);color:#fff;font-size:9px;
  font-weight:700;display:flex;align-items:center;justify-content:center;
  padding:0 4px;
}

/* ─── Common ─── */
.page-title{font-family:'JetBrains Mono',monospace;font-size:20px;font-weight:700;margin-bottom:16px;display:flex;align-items:center;gap:8px}
.btn-primary{
  width:100%;padding:15px;border:none;border-radius:14px;
  background:var(--mint);color:#06060c;
  font-family:'Outfit',sans-serif;font-size:15px;font-weight:700;
  cursor:pointer;transition:transform .1s,opacity .2s;
}
.btn-primary:active{transform:scale(.97)}
.btn-primary:disabled{opacity:.35}
.btn-outline{
  padding:10px 18px;border-radius:10px;border:1px solid var(--border);
  background:var(--surface);color:var(--text2);font-family:'Outfit',sans-serif;
  font-size:13px;font-weight:500;cursor:pointer;transition:border-color .2s,color .2s;
}
.btn-outline:active{border-color:var(--mint);color:var(--text)}
.chip{
  display:inline-flex;align-items:center;gap:4px;padding:5px 12px;
  border-radius:8px;font-size:12px;font-weight:600;
}
.chip-mint{background:var(--mint-dim);color:var(--mint)}
.chip-coral{background:var(--coral-dim);color:var(--coral)}

/* ─── Setup Screen ─── */
#setup{justify-content:center;align-items:center;gap:24px}
.logo{font-family:'JetBrains Mono',monospace;font-size:34px;font-weight:700;letter-spacing:-1.5px}
.logo .s1{color:var(--mint)}
.logo .s2{color:var(--text)}
.setup-sub{color:var(--text3);font-size:13px;text-align:center;line-height:1.65;max-width:300px}
.api-field{width:100%;max-width:340px}
.api-field label{display:block;font-size:10px;text-transform:uppercase;letter-spacing:2px;color:var(--text3);margin-bottom:8px;font-weight:600}
.api-field input{
  width:100%;padding:14px 16px;border-radius:12px;
  border:1px solid var(--border);background:var(--surface);
  color:var(--text);font-size:16px;font-family:'Outfit',sans-serif;outline:none;
  transition:border-color .2s;
}
.api-field input:focus{border-color:var(--mint)}

/* ═══ MODE 1: VOICE TRAINING ═══ */
.trainer-top{display:flex;justify-content:space-between;align-items:center;padding:8px 0}
.streak-badge{font-family:'JetBrains Mono',monospace;font-size:13px;color:var(--gold);display:flex;align-items:center;gap:4px}
.streak-badge .streak-n{font-size:22px;font-weight:700}
.progress-text{font-size:11px;color:var(--text3);font-weight:600}

.card-zone{flex:1;display:flex;flex-direction:column;justify-content:center;align-items:center;gap:12px}

.flash-card{
  width:100%;padding:30px 20px;border-radius:20px;
  background:var(--surface);border:1.5px solid var(--border);
  text-align:center;position:relative;overflow:hidden;
  transition:border-color .35s,box-shadow .35s;
}
.flash-card::before{
  content:'';position:absolute;top:-50%;left:-50%;width:200%;height:200%;
  background:radial-gradient(circle,var(--mint-dim) 0%,transparent 70%);
  opacity:0;transition:opacity .4s;pointer-events:none;
}
.flash-card.correct{border-color:var(--mint);box-shadow:0 0 50px var(--mint-glow)}
.flash-card.correct::before{opacity:1}
.flash-card.incorrect{border-color:var(--coral);box-shadow:0 0 50px var(--coral-glow)}

.card-en{font-family:'JetBrains Mono',monospace;font-size:clamp(18px,5.5vw,30px);font-weight:700;line-height:1.4;margin-bottom:12px;position:relative;z-index:1}
.card-ja{font-size:13px;color:var(--text2);line-height:1.5;position:relative;z-index:1}

.card-actions{display:flex;justify-content:center}
.stock-btn{
  padding:6px 14px;border-radius:8px;border:1px solid var(--border);
  background:transparent;color:var(--text3);font-size:12px;font-weight:600;
  cursor:pointer;transition:all .2s;display:flex;align-items:center;gap:4px;
  font-family:'Outfit',sans-serif;
}
.stock-btn:active,.stock-btn.saved{border-color:var(--gold);color:var(--gold);background:rgba(255,201,77,.08)}

.feedback-line{font-size:14px;min-height:22px;text-align:center;color:var(--text3);transition:color .2s}
.feedback-line.ok{color:var(--mint)}.feedback-line.ng{color:var(--coral)}
.heard-line{font-size:11px;color:var(--text3);min-height:16px;text-align:center;opacity:.7}

.ctrl-zone{display:flex;flex-direction:column;align-items:center;gap:14px;padding-bottom:12px}

.mic-orb{
  width:130px;height:130px;border-radius:50%;
  border:3.5px solid var(--mint);
  background:var(--mint-dim);
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:5px;
  cursor:pointer;position:relative;
  transition:transform .12s,background .2s,box-shadow .25s;
}
.mic-orb:active,.mic-orb.recording{transform:scale(.92);background:rgba(0,240,181,.2);box-shadow:0 0 70px var(--mint-glow)}
.mic-orb.recording{animation:orb-pulse 1.1s ease-in-out infinite}
@keyframes orb-pulse{0%,100%{box-shadow:0 0 0 0 var(--mint-glow)}50%{box-shadow:0 0 0 22px transparent}}
.mic-orb svg{width:34px;height:34px;color:var(--mint)}
.mic-orb .orb-label{font-size:10px;color:var(--mint);font-weight:700;letter-spacing:1.2px;text-transform:uppercase}

.sub-actions{display:flex;gap:10px}

/* ═══ MODE 2: STOCK ═══ */
.stock-empty{text-align:center;padding:60px 20px;color:var(--text3);font-size:14px;line-height:1.7}
.stock-item{
  padding:14px 16px;border-radius:14px;background:var(--surface);
  border:1px solid var(--border);margin-bottom:10px;
  display:flex;justify-content:space-between;align-items:center;
  transition:border-color .2s;
}
.stock-item:active{border-color:var(--border-hi)}
.stock-item-text .stock-en{font-weight:600;font-size:14px;margin-bottom:3px}
.stock-item-text .stock-ja{font-size:12px;color:var(--text2)}
.stock-item-actions{display:flex;gap:6px}
.stock-item-actions button{
  width:34px;height:34px;border-radius:8px;border:1px solid var(--border);
  background:transparent;cursor:pointer;display:flex;align-items:center;justify-content:center;
  transition:border-color .2s,color .2s;color:var(--text3);font-size:16px;
}
.stock-item-actions button:active{border-color:var(--mint);color:var(--mint)}

.stock-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:16px}
.stock-train-btn{
  padding:8px 16px;border-radius:10px;border:none;
  background:var(--mint);color:#06060c;font-size:12px;font-weight:700;
  font-family:'Outfit',sans-serif;cursor:pointer;
}
.stock-train-btn:disabled{opacity:.35}

/* ═══ MODE 3: AI DIALOGUE ═══ */
.chat-area{flex:1;overflow-y:auto;-webkit-overflow-scrolling:touch;padding-bottom:12px}
.chat-area::-webkit-scrollbar{display:none}
.chat-bubble{
  max-width:88%;padding:14px 16px;border-radius:16px;margin-bottom:10px;
  line-height:1.6;font-size:14px;animation:bubble-in .3s ease-out;
}
@keyframes bubble-in{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.bubble-user{
  background:var(--mint-dim);border:1px solid rgba(0,240,181,.15);
  margin-left:auto;border-bottom-right-radius:4px;
}
.bubble-ai{
  background:var(--surface);border:1px solid var(--border);
  margin-right:auto;border-bottom-left-radius:4px;
}
.bubble-ai .b-en{font-weight:600;margin-bottom:6px}
.bubble-ai .b-ja{font-size:12px;color:var(--text2)}
.bubble-ai .b-play{
  margin-top:8px;padding:5px 12px;border-radius:8px;border:1px solid var(--border);
  background:transparent;color:var(--text2);font-size:11px;cursor:pointer;
  font-family:'Outfit',sans-serif;font-weight:600;transition:border-color .2s,color .2s;
}
.bubble-ai .b-play:active{border-color:var(--mint);color:var(--mint)}

.chat-input-bar{
  display:flex;gap:8px;padding:10px 0;
  border-top:1px solid var(--border);
}
.chat-text-input{
  flex:1;padding:12px 14px;border-radius:12px;
  border:1px solid var(--border);background:var(--surface);
  color:var(--text);font-size:15px;font-family:'Outfit',sans-serif;outline:none;
}
.chat-text-input:focus{border-color:var(--mint)}
.chat-mic-btn{
  width:48px;height:48px;border-radius:12px;border:1.5px solid var(--mint);
  background:var(--mint-dim);cursor:pointer;display:flex;align-items:center;justify-content:center;
  transition:background .2s,transform .1s;flex-shrink:0;
}
.chat-mic-btn:active,.chat-mic-btn.recording{background:rgba(0,240,181,.25);transform:scale(.92)}
.chat-mic-btn svg{width:22px;height:22px;color:var(--mint)}
.chat-send-btn{
  width:48px;height:48px;border-radius:12px;border:none;
  background:var(--mint);cursor:pointer;display:flex;align-items:center;justify-content:center;
  transition:transform .1s,opacity .2s;flex-shrink:0;
}
.chat-send-btn:active{transform:scale(.92)}
.chat-send-btn:disabled{opacity:.3}
.chat-send-btn svg{width:20px;height:20px;color:#06060c}

/* ─── Loading ─── */
.overlay{position:fixed;inset:0;background:rgba(6,6,12,.75);display:none;align-items:center;justify-content:center;z-index:100;backdrop-filter:blur(8px);-webkit-backdrop-filter:blur(8px)}
.overlay.show{display:flex}
.dot-loader{display:flex;gap:6px}
.dot-loader span{width:8px;height:8px;border-radius:50%;background:var(--mint);animation:dot-bounce .6s ease-in-out infinite}
.dot-loader span:nth-child(2){animation-delay:.15s}
.dot-loader span:nth-child(3){animation-delay:.3s}
@keyframes dot-bounce{0%,100%{transform:translateY(0);opacity:.4}50%{transform:translateY(-10px);opacity:1}}

/* ─── Confetti ─── */
#confetti{position:fixed;inset:0;pointer-events:none;z-index:200}

/* ─── Slide anim ─── */
@keyframes slide-up{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}
.anim-slide{animation:slide-up .3s ease-out}
</style>
</head>
<body>

<!-- ═══ SETUP ═══ -->
<div id="setup" class="screen active">
  <div class="logo"><span class="s1">Speak</span><span class="s2">Snap</span></div>
  <p class="setup-sub">聞く → 話す → 即判定 → 次へ。<br>爆速回転で英語脳を鍛える。</p>
  <div class="api-field">
    <label>Groq API Key</label>
    <input id="apiKeyInput" type="password" placeholder="gsk_xxxxxxxx…" autocomplete="off">
  </div>
  <button class="btn-primary" id="startBtn" disabled style="max-width:340px">トレーニング開始</button>
  <p class="setup-sub" style="font-size:10px;opacity:.5">APIキーはお使いの端末にのみ保存されます。</p>
</div>

<!-- ═══ MODE 1: VOICE TRAINER ═══ -->
<div id="modeVoice" class="screen">
  <div class="trainer-top">
    <div class="streak-badge">🔥 <span class="streak-n" id="streakN">0</span></div>
    <div class="progress-text" id="progText">1 / 30</div>
  </div>
  <div class="card-zone" id="cardZone">
    <div class="flash-card" id="flashCard">
      <div class="card-en" id="cardEn">Loading…</div>
      <div class="card-ja" id="cardJa"></div>
    </div>
    <div class="card-actions">
      <button class="stock-btn" id="stockSaveBtn">⭐ ストック</button>
    </div>
    <div class="feedback-line" id="fbLine"></div>
    <div class="heard-line" id="heardLine"></div>
  </div>
  <div class="ctrl-zone">
    <div class="mic-orb" id="micOrb">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"/><path d="M19 10v2a7 7 0 0 1-14 0v-2"/><line x1="12" y1="19" x2="12" y2="23"/><line x1="8" y1="23" x2="16" y2="23"/></svg>
      <span class="orb-label">押して発音</span>
    </div>
    <div class="sub-actions">
      <button class="btn-outline" id="replayBtn">🔊 もう一度</button>
      <button class="btn-outline" id="skipBtn">⏭ スキップ</button>
    </div>
  </div>
</div>

<!-- ═══ MODE 2: STOCK ═══ -->
<div id="modeStock" class="screen">
  <div class="screen-body">
    <div class="stock-header">
      <div class="page-title">⭐ ストック</div>
      <button class="stock-train-btn" id="stockTrainBtn" disabled>ストックで練習</button>
    </div>
    <div id="stockList"></div>
  </div>
</div>

<!-- ═══ MODE 3: AI DIALOGUE ═══ -->
<div id="modeChat" class="screen">
  <div class="page-title" style="padding:8px 0 4px">💬 AI対話</div>
  <div class="chat-area" id="chatArea">
    <div class="chat-bubble bubble-ai">
      <div class="b-en">Hi! I'm your English conversation partner. Ask me anything or just say hello!</div>
      <div class="b-ja">英語の会話パートナーです。何でも話しかけてください！</div>
    </div>
  </div>
  <div class="chat-input-bar">
    <input class="chat-text-input" id="chatInput" type="text" placeholder="英語 or 日本語で入力…">
    <div class="chat-mic-btn" id="chatMicBtn">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"/><path d="M19 10v2a7 7 0 0 1-14 0v-2"/><line x1="12" y1="19" x2="12" y2="23"/><line x1="8" y1="23" x2="16" y2="23"/></svg>
    </div>
    <button class="chat-send-btn" id="chatSendBtn" disabled>
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
    </button>
  </div>
</div>

<!-- NAV -->
<nav class="bottom-nav" id="bottomNav">
  <div class="nav-item active" data-mode="voice">
    <svg class="nav-icon" viewBox="0 0 24 24" fill="none" stroke="var(--mint)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"/><path d="M19 10v2a7 7 0 0 1-14 0v-2"/></svg>
    <span class="nav-label">トレーニング</span>
  </div>
  <div class="nav-item" data-mode="stock">
    <svg class="nav-icon" viewBox="0 0 24 24" fill="none" stroke="var(--gold)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
    <span class="nav-label">ストック</span>
    <span class="nav-badge" id="stockBadge" style="display:none">0</span>
  </div>
  <div class="nav-item" data-mode="chat">
    <svg class="nav-icon" viewBox="0 0 24 24" fill="none" stroke="var(--blue)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg>
    <span class="nav-label">AI対話</span>
  </div>
</nav>

<!-- Overlay -->
<div class="overlay" id="overlay"><div class="dot-loader"><span></span><span></span><span></span></div></div>
<canvas id="confetti"></canvas>

<script>
// ════════════════════════════════════════════════
//  SpeakSnap v2 — 統合型英語学習トレーナー
// ════════════════════════════════════════════════

// ── Phrase Bank ──
const PHRASE_BANK = [
  {en:"How's it going?",ja:"調子はどう？"},
  {en:"Nice to meet you.",ja:"はじめまして。"},
  {en:"What do you do for a living?",ja:"お仕事は何ですか？"},
  {en:"I'm looking forward to it.",ja:"楽しみにしています。"},
  {en:"Could you say that again?",ja:"もう一度言っていただけますか？"},
  {en:"Let me think about it.",ja:"考えさせてください。"},
  {en:"That makes sense.",ja:"納得です。"},
  {en:"I appreciate your help.",ja:"助けてくれてありがとう。"},
  {en:"What time works for you?",ja:"何時が都合いい？"},
  {en:"I'll take care of it.",ja:"私がやっておきます。"},
  {en:"Can I get the check?",ja:"お会計お願いします。"},
  {en:"Where is the restroom?",ja:"お手洗いはどこ？"},
  {en:"I'd like to make a reservation.",ja:"予約したいのですが。"},
  {en:"It was great talking to you.",ja:"お話できてよかった。"},
  {en:"I'm not sure about that.",ja:"ちょっとわかりません。"},
  {en:"Do you have any recommendations?",ja:"おすすめはありますか？"},
  {en:"I'll be right back.",ja:"すぐ戻ります。"},
  {en:"Sorry to keep you waiting.",ja:"お待たせしてすみません。"},
  {en:"That sounds like a great idea.",ja:"素晴らしいアイデアですね。"},
  {en:"Would you mind helping me?",ja:"手伝ってもらえますか？"},
  {en:"It depends on the situation.",ja:"状況によります。"},
  {en:"I'm on my way.",ja:"今向かっています。"},
  {en:"Let's get started.",ja:"始めましょう。"},
  {en:"Can you give me a hand?",ja:"ちょっと手を貸して。"},
  {en:"I didn't catch that.",ja:"聞き取れませんでした。"},
  {en:"What brings you here?",ja:"どうしてここに？"},
  {en:"I couldn't agree more.",ja:"まったく同感です。"},
  {en:"Take your time.",ja:"ゆっくりどうぞ。"},
  {en:"That's a good point.",ja:"いい指摘ですね。"},
  {en:"I'll keep that in mind.",ja:"覚えておきます。"},
];

// ── State ──
let API_KEY = '';
let currentIdx = 0;
let streak = 0;
let phrases = [...PHRASE_BANK]; // current working set
let stockItems = JSON.parse(localStorage.getItem('ss_stock') || '[]');
let isRecording = false;
let recorder = null;
let audioChunks = [];
let audioCtx = null;
let chatHistory = [];
let currentMode = 'voice';
let isTrainingStock = false;

// ── DOM shortcuts ──
const $ = id => document.getElementById(id);
const screens = {voice:$('modeVoice'),stock:$('modeStock'),chat:$('modeChat')};

// ════════════════════════════
//  iOS AUDIO UNLOCK
// ════════════════════════════
function unlockAudio(){
  if(!audioCtx) audioCtx = new(window.AudioContext||window.webkitAudioContext)();
  if(audioCtx.state==='suspended') audioCtx.resume();
  const b=audioCtx.createBuffer(1,1,22050),s=audioCtx.createBufferSource();
  s.buffer=b;s.connect(audioCtx.destination);s.start(0);
}

// ════════════════════════════
//  TTS — Web Speech API
// ════════════════════════════
let voicesReady = false;
function loadVoices(){speechSynthesis.getVoices();voicesReady=true}
loadVoices(); speechSynthesis.onvoiceschanged=loadVoices;

function speak(text, lang='en-US', rate=0.92){
  return new Promise(r=>{
    speechSynthesis.cancel();
    const u=new SpeechSynthesisUtterance(text);
    u.lang=lang; u.rate=rate; u.pitch=1;
    const voices=speechSynthesis.getVoices();
    if(lang.startsWith('en')){
      const v=voices.find(v=>v.lang.startsWith('en')&&v.name.includes('Samantha'))
        ||voices.find(v=>v.lang==='en-US')||voices.find(v=>v.lang.startsWith('en'));
      if(v)u.voice=v;
    } else if(lang.startsWith('ja')){
      const v=voices.find(v=>v.lang.startsWith('ja'));
      if(v)u.voice=v;
    }
    u.onend=r; u.onerror=r;
    speechSynthesis.speak(u);
  });
}

// Dual play: EN → JA
async function speakDual(en,ja){
  await speak(en,'en-US',0.9);
  await new Promise(r=>setTimeout(r,300));
  await speak(ja,'ja-JP',1.0);
}

// ════════════════════════════
//  RECORDING (Safari compat)
// ════════════════════════════
function getMime(){
  const types=['audio/mp4','audio/webm;codecs=opus','audio/webm','audio/ogg'];
  for(const t of types) if(typeof MediaRecorder!=='undefined'&&MediaRecorder.isTypeSupported(t)) return t;
  return '';
}

async function startRec(){
  try{
    const stream=await navigator.mediaDevices.getUserMedia({audio:{echoCancellation:true,noiseSuppression:true}});
    const mime=getMime();
    recorder=new MediaRecorder(stream,mime?{mimeType:mime}:{});
    audioChunks=[];
    recorder.ondataavailable=e=>{if(e.data.size>0)audioChunks.push(e.data)};
    recorder.start();
    isRecording=true;
  }catch(e){
    showFeedback('⚠ マイクへのアクセスを許可してください','ng');
  }
}

function stopRec(){
  return new Promise(r=>{
    if(!recorder||recorder.state==='inactive'){r(null);return}
    recorder.onstop=()=>{
      const blob=new Blob(audioChunks,{type:recorder.mimeType||'audio/mp4'});
      recorder.stream.getTracks().forEach(t=>t.stop());
      r(blob);
    };
    recorder.stop();
    isRecording=false;
  });
}

// ════════════════════════════
//  GROQ API
// ════════════════════════════
async function groqSTT(blob){
  const fd=new FormData();
  const ext=blob.type.includes('mp4')?'mp4':blob.type.includes('webm')?'webm':'ogg';
  fd.append('file',blob,`a.${ext}`);
  fd.append('model','whisper-large-v3');
  fd.append('language','en');
  fd.append('response_format','json');
  const res=await fetch('https://api.groq.com/openai/v1/audio/transcriptions',{
    method:'POST',headers:{'Authorization':`Bearer ${API_KEY}`},body:fd
  });
  if(!res.ok) throw new Error(`STT ${res.status}`);
  const d=await res.json();
  return d.text?.trim()||'';
}

async function groqSTTAuto(blob){
  // Auto-detect language for chat mode
  const fd=new FormData();
  const ext=blob.type.includes('mp4')?'mp4':blob.type.includes('webm')?'webm':'ogg';
  fd.append('file',blob,`a.${ext}`);
  fd.append('model','whisper-large-v3');
  fd.append('response_format','json');
  const res=await fetch('https://api.groq.com/openai/v1/audio/transcriptions',{
    method:'POST',headers:{'Authorization':`Bearer ${API_KEY}`},body:fd
  });
  if(!res.ok) throw new Error(`STT ${res.status}`);
  const d=await res.json();
  return d.text?.trim()||'';
}

async function groqJudge(expected, heard){
  const res=await fetch('https://api.groq.com/openai/v1/chat/completions',{
    method:'POST',
    headers:{'Authorization':`Bearer ${API_KEY}`,'Content-Type':'application/json'},
    body:JSON.stringify({
      model:'llama-3.3-70b-versatile',temperature:0,max_tokens:120,
      messages:[
        {role:'system',content:`You are a strict but fair English pronunciation judge. Compare expected phrase to what the student said (transcribed by Whisper).
Rules:
- Minor punctuation/capitalization/article differences → PASS
- Small filler words or slight changes preserving meaning → PASS
- Missing or wrong key words → FAIL
Respond ONLY with JSON: {"pass":true/false,"tip":"short tip in Japanese (max 20 chars), empty if pass"}`},
        {role:'user',content:`Expected: "${expected}"\nHeard: "${heard}"`}
      ]
    })
  });
  if(!res.ok) throw new Error(`LLM ${res.status}`);
  const d=await res.json();
  const c=d.choices[0].message.content;
  try{const m=c.match(/\{[\s\S]*\}/);return m?JSON.parse(m[0]):{pass:false,tip:'判定エラー'}}
  catch{return{pass:false,tip:'判定エラー'}}
}

async function groqChat(userMsg){
  const systemPrompt=`You are a friendly English conversation partner helping a Japanese learner practice.
RULES:
- Always respond in BOTH English AND Japanese.
- Format your response as JSON: {"en":"English response","ja":"Japanese translation"}
- Keep responses concise (1-3 sentences).
- If the user writes in Japanese, respond naturally but still provide both languages.
- Gently correct any English mistakes the user makes.
- Be encouraging and conversational.`;

  chatHistory.push({role:'user',content:userMsg});
  // Keep last 10 messages for context
  const msgs = chatHistory.slice(-10);

  const res=await fetch('https://api.groq.com/openai/v1/chat/completions',{
    method:'POST',
    headers:{'Authorization':`Bearer ${API_KEY}`,'Content-Type':'application/json'},
    body:JSON.stringify({
      model:'llama-3.3-70b-versatile',temperature:0.7,max_tokens:300,
      messages:[{role:'system',content:systemPrompt},...msgs]
    })
  });
  if(!res.ok) throw new Error(`Chat ${res.status}`);
  const d=await res.json();
  const c=d.choices[0].message.content;
  chatHistory.push({role:'assistant',content:c});
  try{
    const m=c.match(/\{[\s\S]*\}/);
    if(m) return JSON.parse(m[0]);
    return {en:c,ja:''};
  }catch{
    return {en:c,ja:''};
  }
}

// ════════════════════════════
//  HAPTICS
// ════════════════════════════
function vibeOk(){navigator.vibrate&&navigator.vibrate([35,25,35])}
function vibeNg(){navigator.vibrate&&navigator.vibrate(90)}

// ════════════════════════════
//  CONFETTI
// ════════════════════════════
function fireConfetti(){
  const cv=$('confetti'),ctx=cv.getContext('2d');
  cv.width=innerWidth;cv.height=innerHeight;
  const ps=Array.from({length:45},()=>({
    x:Math.random()*cv.width,y:-10,
    vx:(Math.random()-.5)*7,vy:Math.random()*4+3,
    r:Math.random()*5+2,
    c:['#00f0b5','#4d8eff','#ffc94d','#ff5678','#a78bfa'][Math.floor(Math.random()*5)],
    life:1
  }));
  let af;
  function draw(){
    ctx.clearRect(0,0,cv.width,cv.height);
    let alive=false;
    ps.forEach(p=>{if(p.life<=0)return;alive=true;p.x+=p.vx;p.y+=p.vy;p.vy+=.12;p.life-=.014;
      ctx.globalAlpha=p.life;ctx.fillStyle=p.c;ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);ctx.fill()});
    ctx.globalAlpha=1;
    if(alive) af=requestAnimationFrame(draw);
  }
  draw();
  setTimeout(()=>{cancelAnimationFrame(af);ctx.clearRect(0,0,cv.width,cv.height)},2200);
}

// ════════════════════════════
//  UI: NAVIGATION
// ════════════════════════════
function switchMode(mode){
  currentMode=mode;
  Object.values(screens).forEach(s=>s.classList.remove('active'));
  screens[mode].classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n=>{
    n.classList.toggle('active',n.dataset.mode===mode);
  });
  if(mode==='stock') renderStock();
}

document.querySelectorAll('.nav-item').forEach(n=>{
  n.addEventListener('click',()=>switchMode(n.dataset.mode));
});

// ════════════════════════════
//  UI: LOADING
// ════════════════════════════
function showLoad(on){$('overlay').classList.toggle('show',on)}

// ════════════════════════════
//  MODE 1: VOICE TRAINER
// ════════════════════════════
function showFeedback(msg,type=''){
  $('fbLine').textContent=msg;
  $('fbLine').className='feedback-line'+(type?' '+type:'');
}

function showCard(){
  const p=phrases[currentIdx];
  $('cardEn').textContent=p.en;
  $('cardJa').textContent=p.ja;
  $('progText').textContent=`${currentIdx+1} / ${phrases.length}`;
  $('fbLine').textContent='';$('fbLine').className='feedback-line';
  $('heardLine').textContent='';
  $('flashCard').className='flash-card';
  // Update stock button state
  const isSaved=stockItems.some(s=>s.en===p.en);
  $('stockSaveBtn').classList.toggle('saved',isSaved);
  $('stockSaveBtn').textContent=isSaved?'⭐ 保存済':'⭐ ストック';
  // Animate
  const z=$('cardZone');z.style.animation='none';void z.offsetWidth;z.style.animation='slide-up .3s ease-out';
}

function updateStreak(v){streak=v;$('streakN').textContent=streak}

async function advanceCard(){
  currentIdx++;
  if(currentIdx>=phrases.length){
    fireConfetti();
    showFeedback('🎉 全フレーズ完了！おめでとう！','ok');
    currentIdx=0;
    if(isTrainingStock){
      isTrainingStock=false;
      phrases=[...PHRASE_BANK];
    }
    updateStreak(0);
    setTimeout(()=>{showCard();speak(phrases[currentIdx].en)},2200);
    return;
  }
  showCard();
  await speak(phrases[currentIdx].en);
}

async function handleVoiceResult(){
  showLoad(true);
  try{
    const blob=await stopRec();
    $('micOrb').classList.remove('recording');
    $('micOrb').querySelector('.orb-label').textContent='押して発音';
    if(!blob||blob.size<800){showFeedback('⚠ 音声が短すぎます','ng');showLoad(false);return}
    const heard=await groqSTT(blob);
    $('heardLine').textContent=heard?`認識: "${heard}"`:'認識できませんでした';
    if(!heard){showFeedback('🎤 認識できませんでした','ng');vibeNg();showLoad(false);return}
    const result=await groqJudge(phrases[currentIdx].en,heard);
    showLoad(false);
    if(result.pass){
      $('flashCard').className='flash-card correct';
      showFeedback('✅ Perfect!','ok');
      vibeOk();updateStreak(streak+1);
      if(streak>0&&streak%5===0) fireConfetti();
      setTimeout(()=>advanceCard(),750);
    } else {
      $('flashCard').className='flash-card incorrect';
      showFeedback(result.tip?`💡 ${result.tip}`:'❌ もう一度！','ng');
      vibeNg();updateStreak(0);
    }
  }catch(e){showLoad(false);showFeedback(`⚠ ${e.message}`,'ng');console.error(e)}
}

// Mic Orb — press & hold
$('micOrb').addEventListener('touchstart',e=>{e.preventDefault();unlockAudio();startRec().then(()=>{
  $('micOrb').classList.add('recording');$('micOrb').querySelector('.orb-label').textContent='離して送信';
})},{passive:false});
$('micOrb').addEventListener('touchend',e=>{e.preventDefault();if(isRecording)handleVoiceResult()},{passive:false});
$('micOrb').addEventListener('mousedown',e=>{e.preventDefault();unlockAudio();startRec().then(()=>{
  $('micOrb').classList.add('recording');$('micOrb').querySelector('.orb-label').textContent='離して送信';
})});
$('micOrb').addEventListener('mouseup',e=>{e.preventDefault();if(isRecording)handleVoiceResult()});

$('replayBtn').addEventListener('click',()=>{unlockAudio();speak(phrases[currentIdx].en)});
$('skipBtn').addEventListener('click',()=>{updateStreak(0);advanceCard()});

// ════════════════════════════
//  MODE 1: STOCK SAVE
// ════════════════════════════
$('stockSaveBtn').addEventListener('click',()=>{
  const p=phrases[currentIdx];
  const idx=stockItems.findIndex(s=>s.en===p.en);
  if(idx>=0){
    stockItems.splice(idx,1);
    $('stockSaveBtn').classList.remove('saved');
    $('stockSaveBtn').textContent='⭐ ストック';
  } else {
    stockItems.push({en:p.en,ja:p.ja,ts:Date.now()});
    $('stockSaveBtn').classList.add('saved');
    $('stockSaveBtn').textContent='⭐ 保存済';
  }
  saveStock();
  updateStockBadge();
});

function saveStock(){localStorage.setItem('ss_stock',JSON.stringify(stockItems))}
function updateStockBadge(){
  const b=$('stockBadge');
  if(stockItems.length>0){b.style.display='flex';b.textContent=stockItems.length}
  else b.style.display='none';
}

// ════════════════════════════
//  MODE 2: STOCK LIST
// ════════════════════════════
function renderStock(){
  const list=$('stockList');
  if(stockItems.length===0){
    list.innerHTML='<div class="stock-empty">まだストックがありません。<br>トレーニング中に ⭐ ボタンで<br>フレーズを保存できます。</div>';
    $('stockTrainBtn').disabled=true;
    return;
  }
  $('stockTrainBtn').disabled=false;
  list.innerHTML=stockItems.map((s,i)=>`
    <div class="stock-item anim-slide" style="animation-delay:${i*0.04}s">
      <div class="stock-item-text">
        <div class="stock-en">${s.en}</div>
        <div class="stock-ja">${s.ja}</div>
      </div>
      <div class="stock-item-actions">
        <button onclick="playStockItem(${i})" title="再生">🔊</button>
        <button onclick="removeStockItem(${i})" title="削除">✕</button>
      </div>
    </div>
  `).join('');
}

window.playStockItem=function(i){
  unlockAudio();
  speakDual(stockItems[i].en, stockItems[i].ja);
};

window.removeStockItem=function(i){
  stockItems.splice(i,1);
  saveStock();updateStockBadge();renderStock();
};

// Stock Training mode
$('stockTrainBtn').addEventListener('click',()=>{
  if(stockItems.length===0) return;
  isTrainingStock=true;
  phrases=stockItems.map(s=>({en:s.en,ja:s.ja}));
  currentIdx=0;streak=0;updateStreak(0);
  switchMode('voice');
  showCard();
  setTimeout(()=>speak(phrases[currentIdx].en),350);
});

// ════════════════════════════
//  MODE 3: AI DIALOGUE
// ════════════════════════════
function addBubble(type, content){
  const area=$('chatArea');
  const div=document.createElement('div');
  div.className=`chat-bubble bubble-${type}`;
  if(type==='user'){
    div.textContent=content;
  } else {
    const id='play_'+Date.now();
    div.innerHTML=`<div class="b-en">${content.en}</div>
      ${content.ja?`<div class="b-ja">${content.ja}</div>`:''}
      <button class="b-play" id="${id}">▶ 日英再生</button>`;
    setTimeout(()=>{
      const btn=document.getElementById(id);
      if(btn) btn.addEventListener('click',()=>{unlockAudio();speakDual(content.en,content.ja||'')});
    },50);
  }
  area.appendChild(div);
  area.scrollTop=area.scrollHeight;
}

async function sendChatMsg(text){
  if(!text.trim()) return;
  addBubble('user',text);
  $('chatInput').value='';
  $('chatSendBtn').disabled=true;
  showLoad(true);
  try{
    const reply=await groqChat(text);
    showLoad(false);
    addBubble('ai',reply);
    // Auto-play
    unlockAudio();
    await speakDual(reply.en, reply.ja||'');
  }catch(e){
    showLoad(false);
    addBubble('ai',{en:`Error: ${e.message}`,ja:'エラーが発生しました'});
  }
}

$('chatSendBtn').addEventListener('click',()=>sendChatMsg($('chatInput').value));
$('chatInput').addEventListener('input',()=>{$('chatSendBtn').disabled=!$('chatInput').value.trim()});
$('chatInput').addEventListener('keydown',e=>{if(e.key==='Enter'&&!e.isComposing){e.preventDefault();sendChatMsg($('chatInput').value)}});

// Chat mic — press & hold
let chatRecording=false;
$('chatMicBtn').addEventListener('touchstart',e=>{
  e.preventDefault();unlockAudio();chatRecording=true;
  $('chatMicBtn').classList.add('recording');
  startRec();
},{passive:false});
$('chatMicBtn').addEventListener('touchend',async e=>{
  e.preventDefault();
  if(!chatRecording) return; chatRecording=false;
  $('chatMicBtn').classList.remove('recording');
  showLoad(true);
  try{
    const blob=await stopRec();
    if(!blob||blob.size<800){showLoad(false);return}
    const heard=await groqSTTAuto(blob);
    showLoad(false);
    if(heard) sendChatMsg(heard);
  }catch(er){showLoad(false);console.error(er)}
},{passive:false});
// Mouse fallback
$('chatMicBtn').addEventListener('mousedown',e=>{
  e.preventDefault();unlockAudio();chatRecording=true;
  $('chatMicBtn').classList.add('recording');
  startRec();
});
$('chatMicBtn').addEventListener('mouseup',async e=>{
  e.preventDefault();
  if(!chatRecording) return; chatRecording=false;
  $('chatMicBtn').classList.remove('recording');
  showLoad(true);
  try{
    const blob=await stopRec();
    if(!blob||blob.size<800){showLoad(false);return}
    const heard=await groqSTTAuto(blob);
    showLoad(false);
    if(heard) sendChatMsg(heard);
  }catch(er){showLoad(false);console.error(er)}
});

// ════════════════════════════
//  SETUP & INIT
// ════════════════════════════
const savedKey=localStorage.getItem('ss_apikey');
if(savedKey){$('apiKeyInput').value=savedKey;$('startBtn').disabled=false}

$('apiKeyInput').addEventListener('input',()=>{$('startBtn').disabled=$('apiKeyInput').value.trim().length<10});

$('startBtn').addEventListener('click',()=>{
  API_KEY=$('apiKeyInput').value.trim();
  localStorage.setItem('ss_apikey',API_KEY);
  unlockAudio();
  $('setup').classList.remove('active');
  screens.voice.classList.add('active');
  $('bottomNav').classList.add('show');
  currentIdx=0;updateStreak(0);updateStockBadge();
  showCard();
  setTimeout(()=>speak(phrases[currentIdx].en),400);
});

// Prevent zoom
document.addEventListener('dblclick',e=>e.preventDefault());
window.addEventListener('resize',()=>{const c=$('confetti');c.width=innerWidth;c.height=innerHeight});
</script>
</body>
</html>
