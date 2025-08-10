<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>BTS K-BANK</title>
<style>
  :root{
    --brand-blue:#0b57b7;
    --brand-gold:#f0b429;
    --bg:#eef4fb;
    --card:#ffffff;
    --muted:#6b7280;
  }
  *{box-sizing:border-box}
  body{
    margin:0;
    font-family: "Segoe UI", Roboto, Arial, sans-serif;
    background: radial-gradient(circle at 10% 10%, #f7fbff 0%, var(--bg) 35%, #e6f0fb 100%);
    color:#0b1726;
    -webkit-font-smoothing:antialiased;
  }

  /* Floating icons background (visible across pages) */
  .scene{
    position:fixed;
    inset:0;
    pointer-events:none;
    overflow:hidden;
    z-index:0;
  }
  .float{
    position:absolute;
    opacity:0.12;
    filter:blur(0.4px);
    animation:floaty linear infinite;
  }
  @keyframes floaty{
    from{transform:translateY(0) rotate(0deg)}
    to{transform:translateY(-1200px) rotate(360deg)}
  }

  /* Layout */
  .wrap{position:relative;z-index:1;max-width:1100px;margin:36px auto;padding:20px;}
  .card{
    background:var(--card);
    border-radius:14px;
    padding:22px;
    box-shadow:0 8px 30px rgba(12,35,70,0.08);
    margin-bottom:18px;
  }

  /* Header / logo */
  .header{
    display:flex;
    align-items:center;
    gap:18px;
    justify-content:space-between;
  }
  .brand{
    display:flex;
    gap:12px;
    align-items:center;
  }
  .logo{
    width:64px;height:64px;background:linear-gradient(135deg,var(--brand-blue),#0a6bd6);
    border-radius:12px;display:flex;align-items:center;justify-content:center;
    box-shadow:0 6px 18px rgba(11,87,183,0.18);
    position:relative;overflow:hidden;
  }
  .logo svg{transform:scale(0.9)}
  .brand-title{font-size:20px;font-weight:700;color:var(--brand-blue)}
  .brand-sub{font-size:12px;color:var(--muted);margin-top:4px}

  /* Hero / Front */
  .hero{
    display:flex;gap:20px;align-items:center;margin-top:18px;
  }
  .hero-left{flex:1}
  .hero-right{width:360px}

  .hero h1{margin:0;font-size:28px;color:var(--brand-blue)}
  .hero p{margin:8px 0 0;color:var(--muted)}

  .cta-row{margin-top:18px;display:flex;gap:12px}
  .btn{
    padding:12px 18px;border-radius:10px;border:none;font-weight:700;cursor:pointer;
    box-shadow:0 6px 18px rgba(11,87,183,0.12);
  }
  .btn-primary{background:linear-gradient(90deg,var(--brand-blue),#1e7fe6);color:white}
  .btn-ghost{background:transparent;border:2px solid rgba(11,87,183,0.08);color:var(--brand-blue)}

  /* Carousel */
  .carousel-container{
    position:relative;
    width:100%;
    height:320px;
    overflow:hidden;
    border-radius:12px;
    box-shadow:0 8px 20px rgba(0,0,0,0.12);
  }
  .carousel-slide{
    display:flex;
    width:500%;
    animation:slide 20s infinite;
  }
  .carousel-slide img{
    width:20%;
    height:320px;
    object-fit:cover;
  }
  @keyframes slide{
    0%{transform:translateX(0%)} 20%{transform:translateX(0%)} 
    25%{transform:translateX(-100%)} 45%{transform:translateX(-100%)} 
    50%{transform:translateX(-200%)} 70%{transform:translateX(-200%)} 
    75%{transform:translateX(-300%)} 95%{transform:translateX(-300%)} 
    100%{transform:translateX(-400%)}
  }

  /* Forms and panels */
  .panel{display:flex;gap:18px;margin-top:14px;flex-wrap:wrap}
  .left-panel{flex:1;min-width:300px}
  .right-panel{flex:1;min-width:300px}

  .form{
    background:linear-gradient(180deg,rgba(255,255,255,0.6),rgba(255,255,255,0.9));
    padding:16px;border-radius:10px;border:1px solid rgba(11,20,40,0.03);
  }
  .input{width:100%;padding:10px;margin:8px 0;border-radius:8px;border:1px solid #d1d5db}
  label{font-size:12px;color:var(--muted);display:block;margin-top:8px}

  /* Login/Signup pages (sectioned) */
  .section{display:none}
  .section.active{display:block;animation:fadeIn .36s ease both}
  @keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}

  /* K-BANK UI small styles (from original) */
  .navbar{background:linear-gradient(180deg,var(--brand-blue),#0a5bb0);color:#fff;padding:12px;border-radius:8px}
  .balance-section{background:white;padding:12px;text-align:center;font-weight:700;color:var(--brand-blue);border-radius:8px;margin-top:14px}
  .main-buttons{display:flex;gap:12px;justify-content:center;margin-top:14px}
  .small-btn{padding:10px 14px;border-radius:8px;background:var(--brand-blue);color:white;border:none;cursor:pointer}

  /* animations for buttons */
  .glow{box-shadow:0 6px 28px rgba(11,87,183,0.16);transition:transform .18s,box-shadow .18s}
  .glow:hover{transform:translateY(-4px);box-shadow:0 18px 40px rgba(11,87,183,0.22)}

  /* Shake on error */
  .shake{animation:shake .4s}
  @keyframes shake{
    10%,90%{transform:translateX(-1px)}
    20%,80%{transform:translateX(2px)}
    30%,50%,70%{transform:translateX(-4px)}
    40%,60%{transform:translateX(4px)}
  }

  .note{font-size:12px;color:var(--muted);text-align:center;margin-top:12px}

  @media (max-width:900px){
    .hero{flex-direction:column}
    .hero-right{width:100%}
    .carousel-slide img{height:220px}
  }
</style>
</head>
<body>

  <!-- floating background icons -->
  <div class="scene" aria-hidden="true">
    <!-- coin -->
    <svg class="float" style="left:8%;bottom:-120px;width:96px;animation-duration:34s;" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10" fill="#f0b429"/></svg>
    <!-- card -->
    <svg class="float" style="left:45%;bottom:-140px;width:80px;animation-duration:28s;" viewBox="0 0 24 24"><rect x="0" y="2" width="24" height="16" rx="2" fill="#0b57b7"/></svg>
    <!-- building -->
    <svg class="float" style="left:78%;bottom:-160px;width:120px;animation-duration:44s;" viewBox="0 0 24 24"><path fill="#1e7fe6" d="M3 3h18v4H3zM6 8h3v11H6zM11 8h3v11h-3zM16 8h3v11h-3z"/></svg>
  </div>

  <div class="wrap">
    <div class="card header">
      <div class="brand">
        <!-- Modified safe logo (SVG) -->
        <div class="logo" aria-hidden="true">
          <svg viewBox="0 0 100 100" width="48" height="48" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="BTS K-BANK logo">
            <defs>
              <linearGradient id="g1" x1="0" x2="1"><stop offset="0" stop-color="#0b57b7"/><stop offset="1" stop-color="#1e7fe6"/></linearGradient>
              <linearGradient id="g2" x1="0" x2="1"><stop offset="0" stop-color="#f0b429"/><stop offset="1" stop-color="#e6a81a"/></linearGradient>
            </defs>
            <rect x="6" y="6" width="88" height="88" rx="14" fill="url(#g1)"/>
            <path d="M30 68 L46 36 L64 68 Z" fill="url(#g2)" />
            <circle cx="46" cy="36" r="6" fill="white" opacity="0.15"/>
          </svg>
        </div>
        <div>
          <div class="brand-title">BTS K-BANK</div>
          <!-- front page only note shown in front section, not here (kept out here) -->
        </div>
      </div>
      <div>
        <div style="text-align:right">
          <button class="btn btn-ghost" onclick="showSection('front')">Home</button>
        </div>
      </div>
    </div>

    <!-- FRONT SECTION -->
    <div id="front" class="card section active">
      <div class="hero">
        <div class="hero-left">
          <h1>BTS K-BANK</h1>
          <p style="color:var(--muted);margin-top:6px">A polished bank interface for entertainment.</p>

          <div class="cta-row">
            <button class="btn btn-primary glow" onclick="showSection('login')">Login</button>
            <button class="btn btn-ghost glow" onclick="showSection('signup')">Sign Up</button>
          </div>

          <div style="margin-top:18px">
            <!-- extra little features or marketing blocks could go here -->
          </div>
        </div>

        <div class="hero-right">
          <div class="card" style="padding:10px;">
            <div class="carousel-container">
              <div class="carousel-slide" aria-hidden="true">
                <img src="https://images.unsplash.com/photo-1607082349566-32f1cbbe43b0?auto=format&fit=crop&w=1400&q=80" alt="Bank building">
                <img src="https://images.unsplash.com/photo-1581091870622-81f92e8362a2?auto=format&fit=crop&w=1400&q=80" alt="Credit cards">
                <img src="https://images.unsplash.com/photo-1556742044-3c52d6e88c62?auto=format&fit=crop&w=1400&q=80" alt="Money transfer">
                <img src="https://images.unsplash.com/photo-1607083206963-1f8a7a3d4a4c?auto=format&fit=crop&w=1400&q=80" alt="ATM">
                <img src="https://images.unsplash.com/photo-1605902711622-cfb43c4437d1?auto=format&fit=crop&w=1400&q=80" alt="Online banking">
              </div>
            </div>

            <div style="text-align:center;margin-top:12px">
              <button class="small-btn glow" onclick="showSection('login')">Login</button>
              <button class="small-btn" onclick="showSection('signup')">Sign Up</button>
            </div>
            <div class="note" style="margin-top:10px;text-align:center">For entertainment purposes only</div>
          </div>
        </div>
      </div>
    </div>

    <!-- LOGIN SECTION -->
    <div id="login" class="card section">
      <div style="display:flex;gap:20px;flex-direction:column;align-items:center">
        <div style="width:420px">
          <div class="form">
            <h3 style="margin:0">Login</h3>
            <label for="login-username">Username</label>
            <input id="login-username" class="input" placeholder="Username" />
            <label for="login-password">Password</label>
            <input id="login-password" type="password" class="input" placeholder="Password" />
            <div style="display:flex;gap:10px;margin-top:12px">
              <button class="btn btn-primary glow" onclick="attemptLogin()">Login</button>
              <button class="btn btn-ghost" onclick="alert('Forgot Password clicked — demo only')">Forgot Password?</button>
            </div>
            <div id="login-error" style="color:red;margin-top:10px;display:none">Invalid username or password.</div>
          </div>
        </div>
      </div>
    </div>

    <!-- SIGNUP SECTION -->
    <div id="signup" class="card section">
      <div style="max-width:540px;margin:auto">
        <div class="form">
          <h3 style="margin:0">Sign Up</h3>
          <label>Bank account number</label>
          <input id="su-account" class="input" placeholder="e.g. 1234567890" />
          <label>Phone number</label>
          <input id="su-phone" class="input" placeholder="+1 555-000-0000" />
          <label>Bank card number</label>
          <input id="su-card" class="input" placeholder="e.g. 4111 1111 1111 1111" />
          <div style="display:flex;gap:10px;margin-top:12px">
            <button class="btn btn-primary glow" onclick="fakeSendCode()">Send Code</button>
            <button class="btn btn-ghost" onclick="showSection('front')">Cancel</button>
          </div>
          <div id="su-error" style="margin-top:10px;display:none;color:#b91c1c;font-weight:700">Error: report to the bank.</div>
        </div>
      </div>
    </div>

    <!-- MAIN K-BANK INTERFACE (after successful login) -->
    <div id="bank" class="card section">
      <div class="navbar">BTS K-BANK</div>
      <div class="balance-section">
        Account Balance: ₩86,293,500,000<br>계좌 잔액: ₩86,293,500,000
      </div>

      <div class="main-buttons">
        <button class="small-btn glow" onclick="showTransfer('local')">💸 Local Transfer (국내 송금)</button>
        <button class="small-btn glow" onclick="showTransfer('intl-country')">🌍 International Transfer (국제 송금)</button>
      </div>

      <!-- Local Transfer Form -->
      <div id="form-local" style="display:none;margin-top:18px">
        <div class="card" style="padding:18px">
          <div style="font-weight:800;margin-bottom:8px">Local Transfer</div>
          <select id="bank-local" class="input">
            <option value="">은행 선택 (Select Bank)</option>
            <option>하나은행 (Hana Bank)</option>
            <option>국민은행 (KB Kookmin Bank)</option>
            <option>우리은행 (Woori Bank)</option>
            <option>신한은행 (Shinhan Bank)</option>
          </select>
          <input id="local-account" class="input" placeholder="Account Number" />
          <input id="local-amount" class="input" type="number" placeholder="Amount (₩ KRW)" />
          <div style="display:flex;gap:10px;justify-content:flex-end">
            <button class="btn btn-primary" onclick="startLoading('local')">Send</button>
          </div>
        </div>
      </div>

      <!-- International Country Selection -->
      <div id="intl-country" style="display:none;margin-top:18px">
        <div class="card" style="padding:18px">
          <div style="font-weight:800;margin-bottom:8px">Choose Country</div>
          <select id="country" class="input" onchange="fillIntlBanks()">
            <option value="">Select a country</option>
            <option value="Chile">Chile</option>
            <option value="USA">USA</option>
            <option value="Germany">Germany</option>
            <option value="Denmark">Denmark</option>
            <option value="Iran">Iran</option>
            <option value="Afghanistan">Afghanistan</option>
            <option value="Israel">Israel</option>
          </select>
        </div>
      </div>

      <!-- International Transfer Form -->
      <div id="form-intl" style="display:none;margin-top:18px">
        <div class="card" style="padding:18px">
          <div style="font-weight:800;margin-bottom:8px">International Transfer</div>
          <select id="intl-bank" class="input"></select>
          <input id="intl-account" class="input" placeholder="Account Number" />
          <input id="intl-amount" class="input" type="number" placeholder="Amount (₩ KRW Equivalent)" />
          <div style="display:flex;gap:10px;justify-content:flex-end">
            <button class="btn btn-primary" onclick="startLoading('intl')">Send</button>
          </div>
        </div>
      </div>

      <!-- Loading Screen -->
      <div id="loading" style="display:none;margin-top:18px">
        <div class="card" style="text-align:center">
          <div style="font-weight:800">Processing Transaction...</div>
          <div style="margin-top:12px">
            <svg width="64" height="64" viewBox="0 0 50 50">
              <circle cx="25" cy="25" r="20" stroke="#e6eefc" stroke-width="6" fill="none"></circle>
              <circle cx="25" cy="25" r="20" stroke="var(--brand-blue)" stroke-width="6" stroke-linecap="round" fill="none" stroke-dasharray="31.4 31.4">
                <animateTransform attributeName="transform" type="rotate" from="0 25 25" to="360 25 25" dur="1s" repeatCount="indefinite"/>
              </circle>
            </svg>
          </div>
          <div id="loading-text" style="margin-top:12px;color:var(--muted)">Pending... 승인 대기 중입니다...</div>
        </div>
      </div>

      <!-- Decline Message -->
      <div id="decline" style="display:none;margin-top:18px">
        <div class="card" style="text-align:center">
          <div style="font-weight:800;color:#b91c1c">⚠️ Transfer Failed</div>
          <div style="margin-top:8px;color:var(--muted)">❌ Transaction Declined<br>거래가 거절되었습니다<br><br>Please report to your bank. 은행에 문의하십시오.</div>
        </div>
      </div>

    </div>

    <div class="note" style="margin-top:12px"> </div>
  </div>

<script>
  // Sections control
  function showSection(id){
    document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
    const el = document.getElementById(id);
    if(el){ el.classList.add('active'); window.scrollTo({top:0,behavior:'smooth'}); }
    // hide all bank sub-areas when switching out
    hideTransfers();
  }

  // Randomize floating durations and positions
  document.querySelectorAll('.float').forEach((el,i)=>{
    const dur = 24 + Math.random()*36;
    el.style.animationDuration = dur + 's';
    el.style.bottom = (-80 - Math.random()*120) + 'px';
    el.style.left = (5 + Math.random()*85) + '%';
  });

  // CAROUSEL: nothing to do — pure CSS sliding used for right-side images; left side uses big slide group.
  // For the carousel in the hero right (the wide slide) the animation is CSS-driven.

  // Login behavior
  function attemptLogin(){
    const user = document.getElementById('login-username').value.trim();
    const pass = document.getElementById('login-password').value.trim();
    const err = document.getElementById('login-error');
    if(user === 'Jungkookbts' && pass === 'Jungkook1997'){
      err.style.display='none';
      showSection('bank');
    } else {
      err.style.display='block';
      // shake effect
      const box = err.parentElement;
      box.classList.remove('shake');
      void box.offsetWidth;
      box.classList.add('shake');
    }
  }

  // Signup fake send code
  function fakeSendCode(){
    document.getElementById('su-error').style.display='none';
    // flash error after slight delay
    setTimeout(()=>{ document.getElementById('su-error').style.display='block';
      const el = document.getElementById('su-error'); el.classList.remove('shake'); void el.offsetWidth; el.classList.add('shake');
    },450);
  }

  // K-BANK transfer logic
  var intlBanks = {
    'Chile': ['Banco de Chile', 'BancoEstado'],
    'USA': ['Bank of America', 'Chase', 'Wells Fargo'],
    'Germany': ['Deutsche Bank', 'Commerzbank'],
    'Denmark': ['Danske Bank', 'Nordea'],
    'Iran': ['Bank Melli Iran', 'Bank Sepah'],
    'Afghanistan': ['Azizi Bank', 'Afghanistan International Bank'],
    'Israel': ['Bank Leumi', 'Bank Hapoalim']
  };

  function hideTransfers(){
    ['form-local','intl-country','form-intl','loading','decline'].forEach(id=>{
      const el = document.getElementById(id);
      if(el) el.style.display='none';
    });
  }

  function showTransfer(which){
    hideTransfers();
    if(which === 'local') document.getElementById('form-local').style.display='block';
    if(which === 'intl-country') document.getElementById('intl-country').style.display='block';
    if(which === 'intl-form') document.getElementById('form-intl').style.display='block';
  }

  function fillIntlBanks(){
    const country = document.getElementById('country').value;
    const select = document.getElementById('intl-bank');
    select.innerHTML = '';
    if(intlBanks[country]){
      intlBanks[country].forEach(b=>{
        const opt = document.createElement('option'); opt.value=b; opt.textContent=b; select.appendChild(opt);
      });
      showTransfer('intl-form');
    }
  }

  function startLoading(type){
    let valid = true;
    if(type === 'local'){
      valid = document.getElementById('bank-local').value && document.getElementById('local-account').value && document.getElementById('local-amount').value;
    } else {
      valid = document.getElementById('intl-bank').value && document.getElementById('intl-account').value && document.getElementById('intl-amount').value;
    }
    if(!valid){ alert('Please fill in all required fields.'); return; }
    hideTransfers();
    document.getElementById('loading').style.display='block';
    // after 6s show decline (demo faster)
    setTimeout(()=>{ document.getElementById('loading').style.display='none'; document.getElementById('decline').style.display='block'; },6000);
  }

  // initialise view
  showSection('front');
</script>
</body>
</html>
