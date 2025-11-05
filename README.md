# 청소년봉사학습 성장교육😀
마지막 메시지를 풀어보세요.
<html lang="ko">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Mission Final 🔐</title>
<style>
  :root{
    --bg:#0f1220; --card:#1c2140; --accent:#ffd84d; --muted:#a9b3c9; --ok:#8ef7a9; --danger:#ff7a90;
  }
  *{box-sizing:border-box;}
  body{
    margin:0; background: radial-gradient(1200px 600px at 20% -10%, #2a2f57, #0f1220); 
    font-family: "Pretendard", "Noto Sans KR", system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple SD Gothic Neo", "Noto Sans", sans-serif;
    color: #eef2ff; 
    min-height:100vh; display:grid; place-items:center; padding:20px;
  }
  .card{
    width:min(720px, 92vw); background:linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.02));
    border:1px solid rgba(255,255,255,.14); border-radius:20px; padding:28px 24px 32px;
    box-shadow: 0 20px 60px rgba(0,0,0,.35);
  }
  .title{font-weight:800; font-size:28px; margin:2px 0 10px; letter-spacing:.4px;}
  .sub{color:var(--muted); font-size:15px; margin-bottom:22px;}
  .lock{display:flex; gap:14px; align-items:center; margin:10px 0 18px;}
  .lock .emoji{font-size:28px;}
  .pw-wrap{display:flex; gap:10px; align-items:center; margin-top:6px;}
  input[type=password]{
    flex:1; padding:14px 16px; border-radius:14px; border:1px solid rgba(255,255,255,.2);
    background:#121631; color:#e6ebff; font-size:16px; outline:none;
    transition:border .2s, box-shadow .2s;
  }
  input[type=password]:focus{ border-color: var(--accent); box-shadow:0 0 0 4px rgba(255,216,77,.15) }
  button{
    padding:12px 16px; border-radius:12px; border:0; background:var(--accent); color:#1b1c22; font-weight:800;
    font-size:16px; cursor:pointer; transition:transform .05s ease;
  }
  button:active{ transform: translateY(1px); }
  .hint{font-size:13px; color:var(--muted); margin-top:8px;}
  .msg{
    display:none; margin-top:18px; padding:18px; border-radius:16px; border:1px dashed rgba(255,255,255,.25);
    background:linear-gradient(180deg, rgba(142,247,169,.06), rgba(142,247,169,.02));
  }
  .msg h2{margin:4px 0 8px; font-size:22px;}
  .msg p{margin:0; color:#e9fff0; line-height:1.65;}
  .tag{display:inline-block; padding:6px 10px; margin-right:6px; border-radius:999px; background:#0c152a; color:#c4d1ff; font-size:12px; border:1px solid rgba(255,255,255,.12)}
  .foot{margin-top:18px; font-size:12.5px; color:#bfc7e6; opacity:.85}
  .err{ color: var(--danger); margin-top:10px; display:none; font-size:14px;}
  .ok{ color: var(--ok); margin-top:10px; display:none; font-size:14px;}
  .confetti{position:fixed; inset:0; pointer-events:none; display:none;}
</style>
</head>
<body>
<canvas class="confetti" id="confetti"></canvas>
<main class="card">
  <div class="lock">
    <div class="emoji">🔐</div>
    <div>
      <div class="title">MISSION FINAL</div>
      <div class="sub">비밀번호를 입력하면 마지막 메시지가 열립니다.</div>
    </div>
  </div>
  <div class="pw-wrap">
    <input id="pw" type="password" placeholder="비밀번호를 입력하세요" autocomplete="off" />
    <button id="btn">열기</button>
  </div>
  <div class="hint">힌트: <span class="tag">무한</span> <span class="tag">가보자고</span> <span class="tag">해보자고</span> — 힌트를 참고해주세요.</div>
  <div class="err" id="err">비밀번호가 달라요. 다시 시도해요.</div>
  <div class="ok" id="ok">✔ 해제 성공! 메시지가 열립니다.</div>

  <section class="msg" id="msg">
    <h2>🔓 Mission Complete!</h2>
    <p>수고했어요! <b>여러분의 경험은 이미 충분히 값져요.</b></p>
    <p>성공을 하면 물론 좋지만, 실패해도 상관 없어요!,</p>
    <p>그것 또한 <b>여러분의 성장을 보여주는</b>단서가 됩니다.</p>
    <p style="margin-top:10px">활동을 통해 실패했더라도, 실패를 바탕삼아 성장할 수 있으니까요. </p>
   <p> <b>활동을 멋지게 마친 여러분 모두 고생 많았습니다.</b></p>
   <p> <b>다음에는 또 어떤 도전을 해볼까요?</b></p>

  <div class="foot">© 서울시자원봉사센터 성장교육</div>

<script>
const PASS = ["도전", "ehwjs", "ㄷㅗㅈㅓㄴ"].map(v => v.toLowerCase());
const pw = document.getElementById('pw');
const btn = document.getElementById('btn');
const err = document.getElementById('err');
const ok  = document.getElementById('ok');
const msg = document.getElementById('msg');

btn.addEventListener('click', unlock);
pw.addEventListener('keyup', (e)=>{ if(e.key==='Enter') unlock(); });

function unlock(){
  // 
  err.style.display='none';
  ok.style.display='none';

  // 
  const value = (pw.value || '').trim().toLowerCase();
  const isValid = PASS.includes(value);

  if (isValid){
    ok.style.display='block';
    msg.style.display='block';
    pw.disabled = true;
    btn.disabled = true;
    startConfetti();
  } else {
    err.style.display='block';
  }
}

/* minimal confetti */
function startConfetti(){
  const c = document.getElementById('confetti');
  const ctx = c.getContext('2d');
  const W = c.width = window.innerWidth;
  const H = c.height = window.innerHeight;
  c.style.display='block';
  let pieces = [];
  for(let i=0;i<180;i++){
    pieces.push({
      x: Math.random()*W,
      y: Math.random()*-H/2,
      r: Math.random()*6+2,
      c: `hsl(${Math.random()*360}, 90%, 60%)`,
      v: Math.random()*1.5+1.2
    });
  }
  const start = performance.now();
  function draw(t){
    ctx.clearRect(0,0,W,H);
    pieces.forEach(p=>{
      p.y += p.v;
      ctx.fillStyle=p.c;
      ctx.beginPath(); ctx.arc(p.x,p.y,p.r,0,Math.PI*2); ctx.fill();
    });
    if(t - start < 3200){ requestAnimationFrame(draw); }
    else { c.style.display='none'; }
  }
  requestAnimationFrame(draw);
}
</script>
