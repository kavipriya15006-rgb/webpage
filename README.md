<!DOCTYPE html>
<html lang="en">
<head>
<title>CreatorOS AI</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{
  font-family:Inter,Segoe UI,Arial,sans-serif;
  background:linear-gradient(135deg,#f7f2ff,#fff8fb 50%,#eef8ff);
  color:#18205a;
}
button,input,select,textarea{font:inherit}
button{cursor:pointer;border:0}
.app{display:flex;min-height:100vh}

/* SIDEBAR */
.sidebar{
  width:235px;position:fixed;left:0;top:0;bottom:0;
  background:linear-gradient(180deg,#171542,#2c2168);
  color:#fff;padding:24px 15px;z-index:5;
}
.logo{font-size:21px;font-weight:800;padding:5px 10px 28px}
.logo span{color:#ee55dc}
.nav{display:grid;gap:7px}
.nav button{
  background:transparent;color:#cbc8e4;text-align:left;
  padding:12px 13px;border-radius:12px;transition:.2s
}
.nav button:hover,.nav button.active{
  color:white;background:linear-gradient(90deg,#6740ef,#a74ce4)
}
.sidebar-bottom{position:absolute;left:15px;right:15px;bottom:20px}
.upgrade{
  background:#ffffff12;border:1px solid #ffffff18;
  border-radius:15px;padding:14px
}
.upgrade small{display:block;color:#c9c5e2;line-height:1.5;margin-top:6px}
.upgrade button{
  width:100%;margin-top:12px;padding:9px;border-radius:9px;
  color:#5c3be3;background:#fff;font-weight:700
}

/* MAIN */
.main{margin-left:235px;width:calc(100% - 235px);padding:20px 25px 40px}
.topbar{display:flex;justify-content:space-between;align-items:center;margin-bottom:18px}
.search{
  width:360px;padding:11px 14px;border-radius:12px;
  border:1px solid #e4e1f0;background:#fff;outline:none
}
.user{display:flex;align-items:center;gap:10px}
.avatar{
  width:38px;height:38px;border-radius:50%;
  display:grid;place-items:center;color:#fff;font-weight:800;
  background:linear-gradient(135deg,#f59ddc,#6341e9)
}

/* CARDS */
.card,.hero{
  background:#ffffffeb;border:1px solid #e4e1f0;
  border-radius:19px;box-shadow:0 15px 38px #4b3b8b13
}
.hero{
  min-height:330px;padding:28px;position:relative;overflow:hidden;
  background:
    radial-gradient(circle at 82% 28%,#f4cfff 0,transparent 22%),
    radial-gradient(circle at 65% 80%,#c8efff 0,transparent 23%),
    #fff;
}
.hero:after{
  content:"✦  ✧  ✦  ✧  ✦";
  position:absolute;right:30px;bottom:30px;color:#dfb3ef;
  font-size:24px;letter-spacing:20px;opacity:.6
}
.badge{
  display:inline-block;background:#f0eaff;color:#613de6;
  padding:7px 11px;border-radius:30px;font-size:11px;font-weight:800
}
.hero h1{font-size:42px;line-height:1.12;max-width:650px;margin:16px 0}
.gradient{
  background:linear-gradient(90deg,#3c25b5,#ed48d6);
  -webkit-background-clip:text;color:transparent
}
.hero p{max-width:650px;color:#73779a;line-height:1.6}
.actions{display:flex;gap:10px;margin-top:20px}
.primary,.secondary{
  padding:11px 17px;border-radius:11px;font-weight:700
}
.primary{background:linear-gradient(90deg,#703df3,#e849d5);color:#fff}
.secondary{background:#fff;color:#5636cf;border:1px solid #dcd7ed}
.stats{display:flex;gap:35px;margin-top:26px}
.stats strong{font-size:21px;display:block}.stats small{color:#7c7d9a}

/* GRID */
.grid{display:grid;grid-template-columns:1.05fr 1.35fr 1.05fr;gap:16px;margin-top:16px}
.card{padding:18px}
.head{display:flex;justify-content:space-between;align-items:center;margin-bottom:13px}
.head h2{font-size:16px}.head p{font-size:11px;color:#7b7d9a}
.icon{
  width:35px;height:35px;border-radius:11px;background:#f0eaff;
  color:#633ee5;display:grid;place-items:center
}
.tool-grid{display:grid;grid-template-columns:1fr 1fr;gap:9px}
.tool{
  border:1px solid #e8e5f1;border-radius:12px;padding:12px;
  transition:.2s;background:#fff
}
.tool:hover{transform:translateY(-2px);box-shadow:0 8px 18px #4c3d8a12}
.tool b{font-size:12px;display:block;margin:5px 0}.tool small{color:#85879e;font-size:10px}

.filters{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:10px}
.filter{
  padding:7px 9px;border:1px solid #e2dfec;border-radius:9px;
  background:#fff;font-size:10px
}
.creator{
  display:flex;align-items:center;gap:10px;padding:10px;
  border:1px solid #e8e5f0;border-radius:12px;margin-bottom:8px
}
.creator .avatar{width:42px;height:42px;flex:none}
.creator-info{flex:1}.creator-info b{font-size:12px}.creator-info small{display:block;color:#85879e;margin-top:3px}
.match{font-weight:800;color:#20a978;font-size:15px}
.view{background:#f0eaff;color:#5c3bd7;border-radius:8px;padding:7px 9px;font-size:10px;font-weight:700}

/* SCORE */
.score{
  background:linear-gradient(145deg,#171442,#5841a5);
  color:#fff
}
.ring{
  width:115px;height:115px;border-radius:50%;margin:15px auto;
  display:grid;place-items:center;
  background:conic-gradient(#65e4af 0 97%,#50457a 97%)
}
.ring div{
  width:88px;height:88px;border-radius:50%;
  display:grid;place-items:center;background:#28205b;
  font-size:25px;font-weight:800
}
.checks{display:grid;gap:7px;color:#d8d5ef;font-size:11px}

/* LOWER SECTIONS */
.full{grid-column:1/-1}
.progress{height:8px;background:#eceaf4;border-radius:20px;overflow:hidden}
.progress span{
  display:block;width:82%;height:100%;
  background:linear-gradient(90deg,#6c3ef0,#e94bd7)
}
.metric{
  display:flex;justify-content:space-between;padding:9px 0;
  border-bottom:1px solid #eeeef5;font-size:12px
}
.metric:last-child{border:0}
.quality{
  display:grid;grid-template-columns:1fr 95px;gap:14px;align-items:center
}
.product{
  height:130px;border-radius:13px;
  display:grid;place-items:center;font-size:43px;color:#fff;
  background:linear-gradient(135deg,#171542,#bb673b,#ffd78e)
}
.quality-score{text-align:center}.quality-score strong{font-size:27px;color:#26ad7e}
.small-btn{
  padding:8px 11px;border-radius:9px;background:#f0eaff;color:#5c39d7;font-size:11px;font-weight:700
}

/* MODAL */
.modal{
  position:fixed;inset:0;background:#17133d99;display:none;
  place-items:center;padding:20px;z-index:20
}
.modal.show{display:grid}
.modal-box{
  width:min(700px,100%);max-height:90vh;overflow:auto;
  background:#fff;border-radius:19px;padding:24px
}
.modal-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:15px}
.close{background:#f0eef7;padding:7px 10px;border-radius:9px}
label{font-size:11px;font-weight:800;display:block;margin:11px 0 5px}
input,select,textarea{
  width:100%;padding:10px 11px;border:1px solid #e0ddec;
  border-radius:9px;outline:none
}
textarea{min-height:90px;resize:vertical}
.two{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.result{
  margin-top:14px;padding:13px;border-radius:12px;
  background:#f6f1ff;border:1px solid #e5d9ff
}
.toast{
  position:fixed;right:22px;bottom:22px;background:#201a4d;
  color:#fff;padding:12px 15px;border-radius:10px;display:none;z-index:30
}
.toast.show{display:block}
footer{text-align:center;color:#85879c;font-size:11px;margin-top:22px}

@media(max-width:1000px){
  .grid{grid-template-columns:1fr 1fr}
}
@media(max-width:700px){
  .sidebar{display:none}.main{margin:0;width:100%;padding:14px}
  .grid{grid-template-columns:1fr}.hero h1{font-size:31px}
  .search{width:210px}.stats{gap:15px;flex-wrap:wrap}
  .two{grid-template-columns:1fr}
}
</style>
</head>

<body>
<div class="app">

<aside class="sidebar">
  <div class="logo">✦ CreatorOS <span>AI</span></div>
  <nav class="nav">
    <button class="active" onclick="toast('Home opened')">⌂ &nbsp; Home</button>
    <button onclick="toast('Explore opened')">⌕ &nbsp; Explore</button>
    <button onclick="go('creators')">◉ &nbsp; Creators</button>
    <button onclick="openBrief()">▣ &nbsp; Briefs</button>
    <button onclick="go('workspace')">◈ &nbsp; My Projects</button>
    <button onclick="toast('Settings opened')">⚙ &nbsp; Settings</button>
  </nav>
  <div class="sidebar-bottom">
    <div class="upgrade">
      <b>✨ CreatorOS Pro</b>
      <small>Advanced AI matching, campaign intelligence and creator analytics.</small>
      <button onclick="toast('Upgrade flow started')">Upgrade</button>
    </div>
  </div>
</aside>

<main class="main">

  <header class="topbar">
    <input id="search" class="search" placeholder="⌕  Search creators, skills, tools..." oninput="searchCreators()">
    <div class="user"><span>🔔</span><div class="avatar">KP</div><b>Kavi Priya</b></div>
  </header>

  <section class="hero">
    <span class="badge">✦ AI-NATIVE MARKETPLACE</span>
    <h1>The AI-native marketplace for <span class="gradient">creative talent</span></h1>
    <p>Discover verified AI creators, generate smart briefs, compare talent, build creative teams and manage the entire campaign from discovery to delivery.</p>
    <div class="actions">
      <button class="primary" onclick="openBrief()">✦ Create AI Brief</button>
      <button class="secondary" onclick="go('creators')">Explore Creators →</button>
    </div>
    <div class="stats">
      <div><strong>10K+</strong><small>AI Creators</small></div>
      <div><strong>1K+</strong><small>Brands & Agencies</small></div>
      <div><strong>50K+</strong><small>Projects Completed</small></div>
      <div><strong>99%</strong><small>Satisfaction</small></div>
    </div>
  </section>

  <section class="grid">

    <!-- NEW FEATURES -->
    <div class="card">
      <div class="head">
        <div><h2>✦ AI Creative Tools</h2><p>Smart features for brands</p></div>
        <div class="icon">AI</div>
      </div>
      <div class="tool-grid">
        <div class="tool" onclick="openBrief()"><b>📝 AI Brief Builder</b><small>Turn ideas into structured briefs</small></div>
        <div class="tool" onclick="smartBudget()"><b>💰 Smart Pricing</b><small>Estimate project budget instantly</small></div>
        <div class="tool" onclick="campaignPlan()"><b>🎯 Campaign Planner</b><small>Generate a complete campaign</small></div>
        <div class="tool" onclick="teamBuilder()"><b>🤝 AI Team Builder</b><small>Build the perfect creative team</small></div>
        <div class="tool" onclick="toast('Authenticity scan started')"><b>🔐 Content Authenticity</b><small>Verify AI content & tools</small></div>
        <div class="tool" onclick="toast('Repurposing workflow started')"><b>♻️ Content Repurposer</b><small>One asset → many formats</small></div>
      </div>
    </div>

    <!-- CREATOR MATCH -->
    <div class="card" id="creators">
      <div class="head">
        <div><h2>Find the Perfect AI Creator</h2><p>AI-ranked matches based on your brief</p></div>
        <button class="small-btn" onclick="openBrief()">+ Brief</button>
      </div>
      <div class="filters">
        <button class="filter">Skills ▾</button>
        <button class="filter">Specialization ▾</button>
        <button class="filter">Tools ▾</button>
        <button class="filter">Budget ▾</button>
        <button class="filter">Location ▾</button>
      </div>

      <div class="creator" data-name="neshiga ai studio runway cinematic fashion">
        <div class="avatar">NS</div>
        <div class="creator-info"><b>Neshiga AI Studio</b><small>Runway • Midjourney • Cinematic</small></div>
        <span class="match">96%</span><button class="view" onclick="creator('Neshiga AI Studio')">View</button>
      </div>
      <div class="creator" data-name="dreamframes studio kling animation">
        <div class="avatar">DF</div>
        <div class="creator-info"><b>DreamFrames Studio</b><small>Kling • Animation • Product Ads</small></div>
        <span class="match">91%</span><button class="view" onclick="creator('DreamFrames Studio')">View</button>
      </div>
      <div class="creator" data-name="pixelperfect ai midjourney product">
        <div class="avatar">PP</div>
        <div class="creator-info"><b>PixelPerfect AI</b><small>Midjourney • Product • Fashion</small></div>
        <span class="match">88%</span><button class="view" onclick="creator('PixelPerfect AI')">View</button>
      </div>
    </div>

    <!-- TRUST -->
    <div class="card score">
      <div class="head">
        <div><h2>Creator Trust Score</h2><p style="color:#c9c4df">Verified profile intelligence</p></div>
        <div class="icon" style="background:#ffffff16;color:#fff">✓</div>
      </div>
      <div class="ring"><div>97%</div></div>
      <div class="checks">
        <span>✓ Tool Verified</span>
        <span>✓ Portfolio Verified</span>
        <span>✓ Work History Verified</span>
        <span>✓ Commercial Ready</span>
        <span>✓ On-time Delivery 96%</span>
      </div>
    </div>

    <!-- PROJECT WORKSPACE -->
    <div class="card" id="workspace">
      <div class="head">
        <div><h2>◈ Project Workspace</h2><p>Track your campaign in one place</p></div>
        <span class="badge">82%</span>
      </div>
      <p class="muted">Luxury Perfume Ad Campaign</p>
      <div style="margin:14px 0 4px;display:flex;justify-content:space-between;font-size:11px">
        <b>Project Progress</b><span>82%</span>
      </div>
      <div class="progress"><span></span></div>
      <div class="metric"><span>✓ Brief Approved</span><b>Done</b></div>
      <div class="metric"><span>✓ Content Created</span><b>Done</b></div>
      <div class="metric"><span>✓ First Draft Submitted</span><b>Done</b></div>
      <div class="metric"><span>○ Revision Requested</span><b>Today</b></div>
      <div class="metric"><span>○ Final Delivery</span><b>Tomorrow</b></div>
    </div>

    <!-- QUALITY -->
    <div class="card">
      <div class="head">
        <div><h2>✦ AI Quality Inspector</h2><p>Check content before delivery</p></div>
        <span class="badge">AI</span>
      </div>
      <div class="quality">
        <div class="product">◈</div>
        <div class="quality-score"><strong>95%</strong><small>Quality Score</small></div>
      </div>
      <div class="checks" style="color:#3a9e7a;margin-top:12px">
        <span>✓ Resolution</span><span>✓ Aspect Ratio</span><span>✓ Brand Logo</span><span>✓ Product Visibility</span><span>✓ Grammar & Spelling</span>
      </div>
    </div>

    <!-- AI CAMPAIGN INTELLIGENCE -->
    <div class="card">
      <div class="head">
        <div><h2>📊 Campaign Intelligence</h2><p>Predict performance before publishing</p></div>
        <div class="icon">↗</div>
      </div>
      <div class="metric"><span>Audience Fit</span><b style="color:#25ad80">92%</b></div>
      <div class="metric"><span>Engagement Potential</span><b style="color:#25ad80">8.4%</b></div>
      <div class="metric"><span>Conversion Potential</span><b style="color:#25ad80">High</b></div>
      <div class="metric"><span>Creative Trend Fit</span><b style="color:#673fe0">94%</b></div>
      <button class="primary" style="width:100%;margin-top:12px" onclick="toast('Campaign report generated')">Generate AI Report</button>
    </div>

    <!-- BRAND MEMORY -->
    <div class="card">
      <div class="head">
        <div><h2>🧠 Brand Memory</h2><p>AI remembers your brand preferences</p></div>
        <div class="icon">✦</div>
      </div>
      <div class="metric"><span>Brand Voice</span><b>Premium • Elegant</b></div>
      <div class="metric"><span>Target Audience</span><b>Luxury Shoppers</b></div>
      <div class="metric"><span>Preferred Style</span><b>Cinematic</b></div>
      <div class="metric"><span>Colors</span><b>Black • Gold</b></div>
      <button class="primary" style="width:100%;margin-top:12px" onclick="openBrief()">Create New Brief</button>
    </div>

    <!-- REPUTATION -->
    <div class="card full">
      <div class="head">
        <div><h2>🏆 Creator Reputation & Growth</h2><p>Transparent performance metrics for creators</p></div>
        <button class="small-btn" onclick="toast('Creator analytics opened')">View Analytics</button>
      </div>
      <div class="grid" style="margin:0">
        <div class="metric"><span>⭐ Client Satisfaction</span><b>98%</b></div>
        <div class="metric"><span>⏱ On-time Delivery</span><b>96%</b></div>
        <div class="metric"><span>🔁 Repeat Clients</span><b>87%</b></div>
        <div class="metric"><span>👁 Portfolio Views</span><b>1,245</b></div>
        <div class="metric"><span>📩 Project Invites</span><b>34</b></div>
        <div class="metric"><span>💰 Project Earnings</span><b>₹48,500</b></div>
      </div>
    </div>

  </section>

  <footer>CreatorOS AI • Smarter Briefs • Better Matches • Verified Creators • Amazing Content</footer>
</main>
</div>

<!-- BRIEF MODAL -->
<div class="modal" id="briefModal">
  <div class="modal-box">
    <div class="modal-head">
      <div><h2>✦ AI Brief Builder</h2><p class="muted">Create a structured brief using AI</p></div>
      <button class="close" onclick="closeModal()">✕</button>
    </div>
    <label>What do you need?</label>
    <textarea id="briefInput" placeholder="Example: I need a cinematic AI video for my sneaker brand..."></textarea>
    <div class="two">
      <div><label>Content Type</label><select id="type"><option>AI Video</option><option>Product Images</option><option>Social Media Campaign</option><option>Advertisement</option></select></div>
      <div><label>Format</label><select><option>9:16 Vertical</option><option>1:1 Square</option><option>16:9 Landscape</option></select></div>
    </div>
    <div class="two">
      <div><label>Budget</label><select><option>₹5,000 – ₹10,000</option><option>₹10,000 – ₹20,000</option><option>₹20,000 – ₹50,000</option></select></div>
      <div><label>Delivery</label><select><option>3 days</option><option>5 days</option><option>7 days</option></select></div>
    </div>
    <button class="primary" style="width:100%;margin-top:16px" onclick="generateBrief()">Generate AI Brief ✦</button>
    <div class="result" id="briefResult" style="display:none"></div>
  </div>
</div>

<!-- GENERIC MODAL -->
<div class="modal" id="infoModal">
  <div class="modal-box">
    <div class="modal-head"><h2 id="infoTitle">AI Feature</h2><button class="close" onclick="closeInfo()">✕</button></div>
    <div class="result" id="infoBody"></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
function toast(message){
  const t=document.getElementById('toast');
  t.textContent=message;t.classList.add('show');
  clearTimeout(window.toastTimer);
  window.toastTimer=setTimeout(()=>t.classList.remove('show'),2200);
}
function go(id){document.getElementById(id).scrollIntoView({behavior:'smooth'})}
function openBrief(){document.getElementById('briefModal').classList.add('show')}
function closeModal(){document.getElementById('briefModal').classList.remove('show')}
function closeInfo(){document.getElementById('infoModal').classList.remove('show')}

function generateBrief(){
  const input=document.getElementById('briefInput').value.trim();
  const type=document.getElementById('type').value;
  const result=document.getElementById('briefResult');
  if(!input){toast('Please enter your creative idea');return}
  result.style.display='block';
  result.innerHTML=`
    <b>✦ AI Generated Brief</b><br><br>
    <b>Project:</b> ${escapeHTML(input)}<br>
    <b>Content:</b> ${type}<br>
    <b>Style:</b> Premium + Cinematic<br>
    <b>Recommended tools:</b> Runway, Midjourney, Kling<br>
    <b>Suggested creator match:</b> 96%<br>
    <b>Estimated budget:</b> ₹10,000 – ₹20,000<br>
    <b>Estimated delivery:</b> 3–5 days
  `;
}
function escapeHTML(s){
  return s.replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#039;'}[m]));
}
function openInfo(title,html){
  document.getElementById('infoTitle').textContent=title;
  document.getElementById('infoBody').innerHTML=html;
  document.getElementById('infoModal').classList.add('show');
}
function smartBudget(){
  openInfo('💰 Smart Pricing',`
    <h3>Estimated project budget: ₹12,000 – ₹20,000</h3>
    <br>
    <p>AI calculates cost using content type, number of assets, complexity, creator experience and delivery time.</p>
    <br>
    <b>Recommended:</b> 1 AI video creator + 1 editor
  `);
}
function campaignPlan(){
  openInfo('🎯 AI Campaign Planner',`
    <h3>Luxury Product Launch</h3><br>
    ✓ 3 Instagram Reels<br>
    ✓ 5 Product Images<br>
    ✓ 2 YouTube Shorts<br>
    ✓ 1 Story Campaign<br>
    ✓ Creator team + budget recommendation
  `);
}
function teamBuilder(){
  openInfo('🤝 AI Team Builder',`
    <h3>Recommended Team — 94% compatibility</h3><br>
    🎬 AI Video Creator — Neshiga AI Studio<br>
    🎨 AI Image Creator — PixelPerfect AI<br>
    ✍️ AI Copywriter — CopyCraft AI<br>
    🎵 AI Music Creator — SonicFrame
  `);
}
function creator(name){
  openInfo(name,`
    <h3>AI Creator Profile</h3><br>
    ⭐ Match Score: <b>96%</b><br>
    🛡 Trust Score: <b>98%</b><br>
    ⏱ Delivery: <b>3 days</b><br>
    🔧 Tools: Runway, Midjourney, Kling<br>
    🎯 Specialization: Luxury Ads, Fashion, Product Videos<br><br>
    <button class="primary" onclick="toast('Creator hire request sent');closeInfo()">Hire Creator →</button>
  `);
}
function searchCreators(){
  const q=document.getElementById('search').value.toLowerCase();
  document.querySelectorAll('.creator').forEach(c=>{
    c.style.display=c.dataset.name.includes(q)?'flex':'none';
  });
}
window.addEventListener('click',e=>{
  if(e.target.classList.contains('modal')){
    e.target.classList.remove('show');
  }
});
</script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CreatorOS AI</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{
  font-family:Inter,Segoe UI,Arial,sans-serif;
  background:linear-gradient(135deg,#f7f2ff,#fff8fb 50%,#eef8ff);
  color:#18205a;
}
button,input,select,textarea{font:inherit}
button{cursor:pointer;border:0}
.app{display:flex;min-height:100vh}

/* SIDEBAR */
.sidebar{
  width:235px;position:fixed;left:0;top:0;bottom:0;
  background:linear-gradient(180deg,#171542,#2c2168);
  color:#fff;padding:24px 15px;z-index:5;
}
.logo{font-size:21px;font-weight:800;padding:5px 10px 28px}
.logo span{color:#ee55dc}
.nav{display:grid;gap:7px}
.nav button{
  background:transparent;color:#cbc8e4;text-align:left;
  padding:12px 13px;border-radius:12px;transition:.2s
}
.nav button:hover,.nav button.active{
  color:white;background:linear-gradient(90deg,#6740ef,#a74ce4)
}
.sidebar-bottom{position:absolute;left:15px;right:15px;bottom:20px}
.upgrade{
  background:#ffffff12;border:1px solid #ffffff18;
  border-radius:15px;padding:14px
}
.upgrade small{display:block;color:#c9c5e2;line-height:1.5;margin-top:6px}
.upgrade button{
  width:100%;margin-top:12px;padding:9px;border-radius:9px;
  color:#5c3be3;background:#fff;font-weight:700
}

/* MAIN */
.main{margin-left:235px;width:calc(100% - 235px);padding:20px 25px 40px}
.topbar{display:flex;justify-content:space-between;align-items:center;margin-bottom:18px}
.search{
  width:360px;padding:11px 14px;border-radius:12px;
  border:1px solid #e4e1f0;background:#fff;outline:none
}
.user{display:flex;align-items:center;gap:10px}
.avatar{
  width:38px;height:38px;border-radius:50%;
  display:grid;place-items:center;color:#fff;font-weight:800;
  background:linear-gradient(135deg,#f59ddc,#6341e9)
}

/* CARDS */
.card,.hero{
  background:#ffffffeb;border:1px solid #e4e1f0;
  border-radius:19px;box-shadow:0 15px 38px #4b3b8b13
}
.hero{
  min-height:330px;padding:28px;position:relative;overflow:hidden;
  background:
    radial-gradient(circle at 82% 28%,#f4cfff 0,transparent 22%),
    radial-gradient(circle at 65% 80%,#c8efff 0,transparent 23%),
    #fff;
}
.hero:after{
  content:"✦  ✧  ✦  ✧  ✦";
  position:absolute;right:30px;bottom:30px;color:#dfb3ef;
  font-size:24px;letter-spacing:20px;opacity:.6
}
.badge{
  display:inline-block;background:#f0eaff;color:#613de6;
  padding:7px 11px;border-radius:30px;font-size:11px;font-weight:800
}
.hero h1{font-size:42px;line-height:1.12;max-width:650px;margin:16px 0}
.gradient{
  background:linear-gradient(90deg,#3c25b5,#ed48d6);
  -webkit-background-clip:text;color:transparent
}
.hero p{max-width:650px;color:#73779a;line-height:1.6}
.actions{display:flex;gap:10px;margin-top:20px}
.primary,.secondary{
  padding:11px 17px;border-radius:11px;font-weight:700
}
.primary{background:linear-gradient(90deg,#703df3,#e849d5);color:#fff}
.secondary{background:#fff;color:#5636cf;border:1px solid #dcd7ed}
.stats{display:flex;gap:35px;margin-top:26px}
.stats strong{font-size:21px;display:block}.stats small{color:#7c7d9a}

/* GRID */
.grid{display:grid;grid-template-columns:1.05fr 1.35fr 1.05fr;gap:16px;margin-top:16px}
.card{padding:18px}
.head{display:flex;justify-content:space-between;align-items:center;margin-bottom:13px}
.head h2{font-size:16px}.head p{font-size:11px;color:#7b7d9a}
.icon{
  width:35px;height:35px;border-radius:11px;background:#f0eaff;
  color:#633ee5;display:grid;place-items:center
}
.tool-grid{display:grid;grid-template-columns:1fr 1fr;gap:9px}
.tool{
  border:1px solid #e8e5f1;border-radius:12px;padding:12px;
  transition:.2s;background:#fff
}
.tool:hover{transform:translateY(-2px);box-shadow:0 8px 18px #4c3d8a12}
.tool b{font-size:12px;display:block;margin:5px 0}.tool small{color:#85879e;font-size:10px}

.filters{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:10px}
.filter{
  padding:7px 9px;border:1px solid #e2dfec;border-radius:9px;
  background:#fff;font-size:10px
}
.creator{
  display:flex;align-items:center;gap:10px;padding:10px;
  border:1px solid #e8e5f0;border-radius:12px;margin-bottom:8px
}
.creator .avatar{width:42px;height:42px;flex:none}
.creator-info{flex:1}.creator-info b{font-size:12px}.creator-info small{display:block;color:#85879e;margin-top:3px}
.match{font-weight:800;color:#20a978;font-size:15px}
.view{background:#f0eaff;color:#5c3bd7;border-radius:8px;padding:7px 9px;font-size:10px;font-weight:700}

/* SCORE */
.score{
  background:linear-gradient(145deg,#171442,#5841a5);
  color:#fff
}
.ring{
  width:115px;height:115px;border-radius:50%;margin:15px auto;
  display:grid;place-items:center;
  background:conic-gradient(#65e4af 0 97%,#50457a 97%)
}
.ring div{
  width:88px;height:88px;border-radius:50%;
  display:grid;place-items:center;background:#28205b;
  font-size:25px;font-weight:800
}
.checks{display:grid;gap:7px;color:#d8d5ef;font-size:11px}

/* LOWER SECTIONS */
.full{grid-column:1/-1}
.progress{height:8px;background:#eceaf4;border-radius:20px;overflow:hidden}
.progress span{
  display:block;width:82%;height:100%;
  background:linear-gradient(90deg,#6c3ef0,#e94bd7)
}
.metric{
  display:flex;justify-content:space-between;padding:9px 0;
  border-bottom:1px solid #eeeef5;font-size:12px
}
.metric:last-child{border:0}
.quality{
  display:grid;grid-template-columns:1fr 95px;gap:14px;align-items:center
}
.product{
  height:130px;border-radius:13px;
  display:grid;place-items:center;font-size:43px;color:#fff;
  background:linear-gradient(135deg,#171542,#bb673b,#ffd78e)
}
.quality-score{text-align:center}.quality-score strong{font-size:27px;color:#26ad7e}
.small-btn{
  padding:8px 11px;border-radius:9px;background:#f0eaff;color:#5c39d7;font-size:11px;font-weight:700
}

/* MODAL */
.modal{
  position:fixed;inset:0;background:#17133d99;display:none;
  place-items:center;padding:20px;z-index:20
}
.modal.show{display:grid}
.modal-box{
  width:min(700px,100%);max-height:90vh;overflow:auto;
  background:#fff;border-radius:19px;padding:24px
}
.modal-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:15px}
.close{background:#f0eef7;padding:7px 10px;border-radius:9px}
label{font-size:11px;font-weight:800;display:block;margin:11px 0 5px}
input,select,textarea{
  width:100%;padding:10px 11px;border:1px solid #e0ddec;
  border-radius:9px;outline:none
}
textarea{min-height:90px;resize:vertical}
.two{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.result{
  margin-top:14px;padding:13px;border-radius:12px;
  background:#f6f1ff;border:1px solid #e5d9ff
}
.toast{
  position:fixed;right:22px;bottom:22px;background:#201a4d;
  color:#fff;padding:12px 15px;border-radius:10px;display:none;z-index:30
}
.toast.show{display:block}
footer{text-align:center;color:#85879c;font-size:11px;margin-top:22px}

@media(max-width:1000px){
  .grid{grid-template-columns:1fr 1fr}
}
@media(max-width:700px){
  .sidebar{display:none}.main{margin:0;width:100%;padding:14px}
  .grid{grid-template-columns:1fr}.hero h1{font-size:31px}
  .search{width:210px}.stats{gap:15px;flex-wrap:wrap}
  .two{grid-template-columns:1fr}
}
</style>
</head>

<body>
<div class="app">

<aside class="sidebar">
  <div class="logo">✦ CreatorOS <span>AI</span></div>
  <nav class="nav">
    <button class="active" onclick="toast('Home opened')">⌂ &nbsp; Home</button>
    <button onclick="toast('Explore opened')">⌕ &nbsp; Explore</button>
    <button onclick="go('creators')">◉ &nbsp; Creators</button>
    <button onclick="openBrief()">▣ &nbsp; Briefs</button>
    <button onclick="go('workspace')">◈ &nbsp; My Projects</button>
    <button onclick="toast('Settings opened')">⚙ &nbsp; Settings</button>
  </nav>
  <div class="sidebar-bottom">
    <div class="upgrade">
      <b>✨ CreatorOS Pro</b>
      <small>Advanced AI matching, campaign intelligence and creator analytics.</small>
      <button onclick="toast('Upgrade flow started')">Upgrade</button>
    </div>
  </div>
</aside>

<main class="main">

  <header class="topbar">
    <input id="search" class="search" placeholder="⌕  Search creators, skills, tools..." oninput="searchCreators()">
    <div class="user"><span>🔔</span><div class="avatar">KP</div><b>Kavi Priya</b></div>
  </header>

  <section class="hero">
    <span class="badge">✦ AI-NATIVE MARKETPLACE</span>
    <h1>The AI-native marketplace for <span class="gradient">creative talent</span></h1>
    <p>Discover verified AI creators, generate smart briefs, compare talent, build creative teams and manage the entire campaign from discovery to delivery.</p>
    <div class="actions">
      <button class="primary" onclick="openBrief()">✦ Create AI Brief</button>
      <button class="secondary" onclick="go('creators')">Explore Creators →</button>
    </div>
    <div class="stats">
      <div><strong>10K+</strong><small>AI Creators</small></div>
      <div><strong>1K+</strong><small>Brands & Agencies</small></div>
      <div><strong>50K+</strong><small>Projects Completed</small></div>
      <div><strong>99%</strong><small>Satisfaction</small></div>
    </div>
  </section>

  <section class="grid">

    <!-- NEW FEATURES -->
    <div class="card">
      <div class="head">
        <div><h2>✦ AI Creative Tools</h2><p>Smart features for brands</p></div>
        <div class="icon">AI</div>
      </div>
      <div class="tool-grid">
        <div class="tool" onclick="openBrief()"><b>📝 AI Brief Builder</b><small>Turn ideas into structured briefs</small></div>
        <div class="tool" onclick="smartBudget()"><b>💰 Smart Pricing</b><small>Estimate project budget instantly</small></div>
        <div class="tool" onclick="campaignPlan()"><b>🎯 Campaign Planner</b><small>Generate a complete campaign</small></div>
        <div class="tool" onclick="teamBuilder()"><b>🤝 AI Team Builder</b><small>Build the perfect creative team</small></div>
        <div class="tool" onclick="toast('Authenticity scan started')"><b>🔐 Content Authenticity</b><small>Verify AI content & tools</small></div>
        <div class="tool" onclick="toast('Repurposing workflow started')"><b>♻️ Content Repurposer</b><small>One asset → many formats</small></div>
      </div>
    </div>

    <!-- CREATOR MATCH -->
    <div class="card" id="creators">
      <div class="head">
        <div><h2>Find the Perfect AI Creator</h2><p>AI-ranked matches based on your brief</p></div>
        <button class="small-btn" onclick="openBrief()">+ Brief</button>
      </div>
      <div class="filters">
        <button class="filter">Skills ▾</button>
        <button class="filter">Specialization ▾</button>
        <button class="filter">Tools ▾</button>
        <button class="filter">Budget ▾</button>
        <button class="filter">Location ▾</button>
      </div>

      <div class="creator" data-name="neshiga ai studio runway cinematic fashion">
        <div class="avatar">NS</div>
        <div class="creator-info"><b>Neshiga AI Studio</b><small>Runway • Midjourney • Cinematic</small></div>
        <span class="match">96%</span><button class="view" onclick="creator('Neshiga AI Studio')">View</button>
      </div>
      <div class="creator" data-name="dreamframes studio kling animation">
        <div class="avatar">DF</div>
        <div class="creator-info"><b>DreamFrames Studio</b><small>Kling • Animation • Product Ads</small></div>
        <span class="match">91%</span><button class="view" onclick="creator('DreamFrames Studio')">View</button>
      </div>
      <div class="creator" data-name="pixelperfect ai midjourney product">
        <div class="avatar">PP</div>
        <div class="creator-info"><b>PixelPerfect AI</b><small>Midjourney • Product • Fashion</small></div>
        <span class="match">88%</span><button class="view" onclick="creator('PixelPerfect AI')">View</button>
      </div>
    </div>

    <!-- TRUST -->
    <div class="card score">
      <div class="head">
        <div><h2>Creator Trust Score</h2><p style="color:#c9c4df">Verified profile intelligence</p></div>
        <div class="icon" style="background:#ffffff16;color:#fff">✓</div>
      </div>
      <div class="ring"><div>97%</div></div>
      <div class="checks">
        <span>✓ Tool Verified</span>
        <span>✓ Portfolio Verified</span>
        <span>✓ Work History Verified</span>
        <span>✓ Commercial Ready</span>
        <span>✓ On-time Delivery 96%</span>
      </div>
    </div>

    <!-- PROJECT WORKSPACE -->
    <div class="card" id="workspace">
      <div class="head">
        <div><h2>◈ Project Workspace</h2><p>Track your campaign in one place</p></div>
        <span class="badge">82%</span>
      </div>
      <p class="muted">Luxury Perfume Ad Campaign</p>
      <div style="margin:14px 0 4px;display:flex;justify-content:space-between;font-size:11px">
        <b>Project Progress</b><span>82%</span>
      </div>
      <div class="progress"><span></span></div>
      <div class="metric"><span>✓ Brief Approved</span><b>Done</b></div>
      <div class="metric"><span>✓ Content Created</span><b>Done</b></div>
      <div class="metric"><span>✓ First Draft Submitted</span><b>Done</b></div>
      <div class="metric"><span>○ Revision Requested</span><b>Today</b></div>
      <div class="metric"><span>○ Final Delivery</span><b>Tomorrow</b></div>
    </div>

    <!-- QUALITY -->
    <div class="card">
      <div class="head">
        <div><h2>✦ AI Quality Inspector</h2><p>Check content before delivery</p></div>
        <span class="badge">AI</span>
      </div>
      <div class="quality">
        <div class="product">◈</div>
        <div class="quality-score"><strong>95%</strong><small>Quality Score</small></div>
      </div>
      <div class="checks" style="color:#3a9e7a;margin-top:12px">
        <span>✓ Resolution</span><span>✓ Aspect Ratio</span><span>✓ Brand Logo</span><span>✓ Product Visibility</span><span>✓ Grammar & Spelling</span>
      </div>
    </div>

    <!-- AI CAMPAIGN INTELLIGENCE -->
    <div class="card">
      <div class="head">
        <div><h2>📊 Campaign Intelligence</h2><p>Predict performance before publishing</p></div>
        <div class="icon">↗</div>
      </div>
      <div class="metric"><span>Audience Fit</span><b style="color:#25ad80">92%</b></div>
      <div class="metric"><span>Engagement Potential</span><b style="color:#25ad80">8.4%</b></div>
      <div class="metric"><span>Conversion Potential</span><b style="color:#25ad80">High</b></div>
      <div class="metric"><span>Creative Trend Fit</span><b style="color:#673fe0">94%</b></div>
      <button class="primary" style="width:100%;margin-top:12px" onclick="toast('Campaign report generated')">Generate AI Report</button>
    </div>

    <!-- BRAND MEMORY -->
    <div class="card">
      <div class="head">
        <div><h2>🧠 Brand Memory</h2><p>AI remembers your brand preferences</p></div>
        <div class="icon">✦</div>
      </div>
      <div class="metric"><span>Brand Voice</span><b>Premium • Elegant</b></div>
      <div class="metric"><span>Target Audience</span><b>Luxury Shoppers</b></div>
      <div class="metric"><span>Preferred Style</span><b>Cinematic</b></div>
      <div class="metric"><span>Colors</span><b>Black • Gold</b></div>
      <button class="primary" style="width:100%;margin-top:12px" onclick="openBrief()">Create New Brief</button>
    </div>

    <!-- REPUTATION -->
    <div class="card full">
      <div class="head">
        <div><h2>🏆 Creator Reputation & Growth</h2><p>Transparent performance metrics for creators</p></div>
        <button class="small-btn" onclick="toast('Creator analytics opened')">View Analytics</button>
      </div>
      <div class="grid" style="margin:0">
        <div class="metric"><span>⭐ Client Satisfaction</span><b>98%</b></div>
        <div class="metric"><span>⏱ On-time Delivery</span><b>96%</b></div>
        <div class="metric"><span>🔁 Repeat Clients</span><b>87%</b></div>
        <div class="metric"><span>👁 Portfolio Views</span><b>1,245</b></div>
        <div class="metric"><span>📩 Project Invites</span><b>34</b></div>
        <div class="metric"><span>💰 Project Earnings</span><b>₹48,500</b></div>
      </div>
    </div>

  </section>

  <footer>CreatorOS AI • Smarter Briefs • Better Matches • Verified Creators • Amazing Content</footer>
</main>
</div>

<!-- BRIEF MODAL -->
<div class="modal" id="briefModal">
  <div class="modal-box">
    <div class="modal-head">
      <div><h2>✦ AI Brief Builder</h2><p class="muted">Create a structured brief using AI</p></div>
      <button class="close" onclick="closeModal()">✕</button>
    </div>
    <label>What do you need?</label>
    <textarea id="briefInput" placeholder="Example: I need a cinematic AI video for my sneaker brand..."></textarea>
    <div class="two">
      <div><label>Content Type</label><select id="type"><option>AI Video</option><option>Product Images</option><option>Social Media Campaign</option><option>Advertisement</option></select></div>
      <div><label>Format</label><select><option>9:16 Vertical</option><option>1:1 Square</option><option>16:9 Landscape</option></select></div>
    </div>
    <div class="two">
      <div><label>Budget</label><select><option>₹5,000 – ₹10,000</option><option>₹10,000 – ₹20,000</option><option>₹20,000 – ₹50,000</option></select></div>
      <div><label>Delivery</label><select><option>3 days</option><option>5 days</option><option>7 days</option></select></div>
    </div>
    <button class="primary" style="width:100%;margin-top:16px" onclick="generateBrief()">Generate AI Brief ✦</button>
    <div class="result" id="briefResult" style="display:none"></div>
  </div>
</div>

<!-- GENERIC MODAL -->
<div class="modal" id="infoModal">
  <div class="modal-box">
    <div class="modal-head"><h2 id="infoTitle">AI Feature</h2><button class="close" onclick="closeInfo()">✕</button></div>
    <div class="result" id="infoBody"></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
function toast(message){
  const t=document.getElementById('toast');
  t.textContent=message;t.classList.add('show');
  clearTimeout(window.toastTimer);
  window.toastTimer=setTimeout(()=>t.classList.remove('show'),2200);
}
function go(id){document.getElementById(id).scrollIntoView({behavior:'smooth'})}
function openBrief(){document.getElementById('briefModal').classList.add('show')}
function closeModal(){document.getElementById('briefModal').classList.remove('show')}
function closeInfo(){document.getElementById('infoModal').classList.remove('show')}

function generateBrief(){
  const input=document.getElementById('briefInput').value.trim();
  const type=document.getElementById('type').value;
  const result=document.getElementById('briefResult');
  if(!input){toast('Please enter your creative idea');return}
  result.style.display='block';
  result.innerHTML=`
    <b>✦ AI Generated Brief</b><br><br>
    <b>Project:</b> ${escapeHTML(input)}<br>
    <b>Content:</b> ${type}<br>
    <b>Style:</b> Premium + Cinematic<br>
    <b>Recommended tools:</b> Runway, Midjourney, Kling<br>
    <b>Suggested creator match:</b> 96%<br>
    <b>Estimated budget:</b> ₹10,000 – ₹20,000<br>
    <b>Estimated delivery:</b> 3–5 days
  `;
}
function escapeHTML(s){
  return s.replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#039;'}[m]));
}
function openInfo(title,html){
  document.getElementById('infoTitle').textContent=title;
  document.getElementById('infoBody').innerHTML=html;
  document.getElementById('infoModal').classList.add('show');
}
function smartBudget(){
  openInfo('💰 Smart Pricing',`
    <h3>Estimated project budget: ₹12,000 – ₹20,000</h3>
    <br>
    <p>AI calculates cost using content type, number of assets, complexity, creator experience and delivery time.</p>
    <br>
    <b>Recommended:</b> 1 AI video creator + 1 editor
  `);
}
function campaignPlan(){
  openInfo('🎯 AI Campaign Planner',`
    <h3>Luxury Product Launch</h3><br>
    ✓ 3 Instagram Reels<br>
    ✓ 5 Product Images<br>
    ✓ 2 YouTube Shorts<br>
    ✓ 1 Story Campaign<br>
    ✓ Creator team + budget recommendation
  `);
}
function teamBuilder(){
  openInfo('🤝 AI Team Builder',`
    <h3>Recommended Team — 94% compatibility</h3><br>
    🎬 AI Video Creator — Neshiga AI Studio<br>
    🎨 AI Image Creator — PixelPerfect AI<br>
    ✍️ AI Copywriter — CopyCraft AI<br>
    🎵 AI Music Creator — SonicFrame
  `);
}
function creator(name){
  openInfo(name,`
    <h3>AI Creator Profile</h3><br>
    ⭐ Match Score: <b>96%</b><br>
    🛡 Trust Score: <b>98%</b><br>
    ⏱ Delivery: <b>3 days</b><br>
    🔧 Tools: Runway, Midjourney, Kling<br>
    🎯 Specialization: Luxury Ads, Fashion, Product Videos<br><br>
    <button class="primary" onclick="toast('Creator hire request sent');closeInfo()">Hire Creator →</button>
  `);
}
function searchCreators(){
  const q=document.getElementById('search').value.toLowerCase();
  document.querySelectorAll('.creator').forEach(c=>{
    c.style.display=c.dataset.name.includes(q)?'flex':'none';
  });
}
window.addEventListener('click',e=>{
  if(e.target.classList.contains('modal')){
    e.target.classList.remove('show');
  }
});
</script>
</body>
</html>
