<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Quản lý Đội</title>
<style>
:root{
  --blue:#2563eb; --navy:#1e40af; --ink:#1f2a44; --muted:#5b6b88; --line:#d9e2f2;
  --card:#ffffff; --sky1:#bfe3ff; --sky2:#eaf6ff; --grass:#9fd8a4; --gold:#f5b800;
  box-sizing:border-box; padding-top:env(safe-area-inset-top,0px); padding-bottom:env(safe-area-inset-bottom,0px);
}
@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){--card:#16213a;--ink:#e8eefc;--muted:#9fb0d0;--line:#2b3b60;--sky1:#10264d;--sky2:#17335f;--grass:#1d4a37}
}
*{box-sizing:border-box}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
body{margin:0;min-height:100vh;font-family:"Be Vietnam Pro","Segoe UI",Roboto,Arial,sans-serif;color:var(--ink);background:linear-gradient(rgba(255,255,255,.12),rgba(255,255,255,.12)),url(nen.jpg) center/cover no-repeat fixed,var(--sky1)}
.wrap{max-width:1000px;margin:0 auto;padding:18px 14px 40px}
header{text-align:center;margin-bottom:14px}
header h1{margin:0;font-size:clamp(1.5rem,4vw,2.2rem);color:#fff;text-shadow:0 2px 8px rgba(0,40,120,.7)}
header p{margin:2px 0 0;color:#fff;font-size:.95rem;text-shadow:0 1px 6px rgba(0,40,120,.8)}

.demo{background:var(--navy);border-radius:16px;border:2px dashed #fcd34d;overflow:hidden;color:#fff;
  box-shadow:0 12px 30px rgba(30,64,175,.35)}
.stripe{background:repeating-linear-gradient(135deg,#f5b800 0 14px,#2b2b2b 14px 28px);text-align:center;padding:5px 0;font-weight:700;font-size:.78rem}
.stripe span{background:#f5b800;color:#4a3300;padding:1px 14px;border-radius:4px}
.demo-in{padding:14px 16px 18px}
.demo-top{display:flex;flex-wrap:wrap;gap:10px;align-items:center;justify-content:space-between}
.demo-top h2{margin:0;font-size:1.1rem}
.chips{display:flex;flex-wrap:wrap;gap:6px}
.chip{font-size:.72rem;padding:5px 10px;border-radius:99px;background:rgba(255,255,255,.14);border:1px solid rgba(255,255,255,.22)}
.chip.gold{background:var(--gold);color:#3b2a00;font-weight:600;border:0}
.cols{display:grid;grid-template-columns:1fr 2fr;gap:14px;margin-top:12px}
.cols h3{margin:0 0 6px;font-size:.72rem;letter-spacing:.08em;color:#a9c3ff}
.grid1,.grid2{display:grid;gap:8px}
.grid2{grid-template-columns:repeat(2,1fr)}
.role{display:flex;align-items:center;gap:10px;text-align:left;width:100%;padding:10px 12px;border-radius:10px;
  background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.25);color:#fff;font:inherit;cursor:pointer}
.role:hover{background:rgba(255,255,255,.22)}
.role:focus-visible,.tab:focus-visible,button:focus-visible,input:focus-visible,a:focus-visible{outline:3px solid #fcd34d;outline-offset:2px}
.role .ic{font-size:1.4rem}
.role b{display:block;font-size:.88rem}
.role small{font-size:.7rem;color:#c9d8ff}
.span2{grid-column:span 2}

.auth{max-width:350px;margin:22px auto 0}
.divider{display:flex;align-items:center;gap:10px;color:#fff;text-shadow:0 1px 4px rgba(0,0,0,.6);font-size:.72rem;font-weight:600;margin-bottom:10px}
.divider::before,.divider::after{content:"";flex:1;height:1px;background:var(--muted);opacity:.4}
.tabs{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:10px}
.tab{padding:10px;border-radius:10px;border:1px solid var(--line);background:var(--card);color:var(--ink);font:inherit;font-weight:600;font-size:.88rem;cursor:pointer}
.tab[aria-selected="true"]{background:var(--blue);color:#fff;border-color:var(--blue)}
.card{background:var(--card);border-radius:16px;padding:18px;box-shadow:0 10px 28px rgba(30,64,175,.18)}
label{display:block;font-size:.82rem;color:var(--muted);margin:0 0 6px}
.field{margin-bottom:14px}
input{width:100%;padding:12px;border:1px solid var(--line);border-radius:10px;font:inherit;background:transparent;color:var(--ink)}
.pw{position:relative}
.pw button{position:absolute;right:6px;top:50%;transform:translateY(-50%);background:none;border:0;cursor:pointer;font-size:1.1rem;padding:6px}
.primary{width:100%;padding:12px;border:0;border-radius:10px;background:var(--blue);color:#fff;font:inherit;font-weight:700;cursor:pointer}
.primary:hover{background:#1d4fd8}
.link{display:block;text-align:center;margin-top:12px;font-size:.85rem;color:var(--blue);text-decoration:none}
.msg{min-height:1.2em;font-size:.82rem;margin:-4px 0 10px;color:#c62828}
.install{display:block;margin:16px auto 0;padding:10px 18px;border-radius:12px;border:0;background:var(--navy);color:#fff;font:inherit;font-weight:600;font-size:.85rem;cursor:pointer}
.install small{opacity:.8;margin-left:6px;font-weight:400}

.welcome{display:none;text-align:center;padding:30px 10px}
.welcome h2{color:var(--navy);margin:0 0 6px}
.welcome button{margin-top:14px;padding:10px 20px;border-radius:10px;border:1px solid var(--blue);background:var(--card);color:var(--blue);font:inherit;font-weight:600;cursor:pointer}
body.in .login-view{display:none} body.in .welcome{display:block}
[hidden]{display:none!important}
@media (max-width:720px){.cols{grid-template-columns:1fr}.grid2{grid-template-columns:1fr}.span2{grid-column:auto}}
.mailbox{background:#fff8dc;border:1px dashed #d4a800;color:#5a4500;border-radius:10px;padding:10px 12px;font-size:.8rem;margin-bottom:12px}.mailbox b{font-size:1.1rem;letter-spacing:.2em}
.app{display:none;max-width:640px;margin:0 auto}body.in .app{display:block}
.bar{display:flex;justify-content:space-between;align-items:center;gap:10px;margin-bottom:12px}
.ghost{padding:8px 14px;border-radius:10px;border:1px solid var(--blue);background:transparent;color:var(--blue);font:inherit;font-weight:600;cursor:pointer}
.atabs{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:12px}
.atab{padding:11px;border-radius:12px;border:0;background:rgba(255,255,255,.85);color:var(--navy);font:inherit;font-weight:700;cursor:pointer}
.atab[aria-selected="true"]{background:var(--blue);color:#fff}
.panel h2{margin:0 0 12px;font-size:1.15rem;color:var(--navy)}.panel h3{margin:20px 0 8px;font-size:1rem}
.row{display:grid;grid-template-columns:1fr 1fr;gap:0 12px}.full{grid-column:1/-1}
textarea,select{width:100%;padding:12px;border:1px solid var(--line);border-radius:10px;font:inherit;background:transparent;color:var(--ink)}
select option{color:#111}
.item{border:1px solid var(--line);border-radius:12px;padding:10px 12px;margin-bottom:8px;display:flex;justify-content:space-between;gap:10px;align-items:flex-start}
.item small{color:var(--muted);display:block;margin-top:2px}
.del{background:none;border:0;color:#c62828;cursor:pointer;font-size:.8rem;font-weight:600;white-space:nowrap}
.pts{color:#c62828;font-weight:700;white-space:nowrap}
.filter{display:flex;flex-wrap:wrap;gap:10px;align-items:center;margin:18px 0 10px}.sum{font-size:.85rem;font-weight:600;color:var(--navy)}
.empty{color:var(--muted);font-size:.88rem;text-align:center;padding:14px}
@media (max-width:480px){.row{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <h1>Quản lý Đội</h1>
    <p>Thi đua tuần &amp; phong trào Đoàn trường</p>
  </header>

  <main class="app" id="app">
    <div class="bar card">
      <div><b>Xin chào, <span id="who"></span></b><div style="font-size:.8rem;color:var(--muted)">Nhập báo cáo thi đua &amp; phong trào</div></div>
      <button class="ghost" id="logout">Đăng xuất</button>
    </div>
    <div class="atabs" role="tablist">
      <button class="atab" aria-selected="true" data-p="pMove">🚩 Phong trào</button>
      <button class="atab" aria-selected="false" data-p="pViol">📝 Vi phạm trong ngày</button>
    </div>

    <section id="pMove" class="panel card">
      <h2>Tạo phong trào của nhà trường</h2>
      <form id="moveForm" class="row">
        <div class="field full"><label for="mn">Tên phong trào</label><input id="mn" placeholder="VD: Em yêu trường em"></div>
        <div class="field"><label for="ms">Bắt đầu</label><input id="ms" type="date"></div>
        <div class="field"><label for="me">Kết thúc</label><input id="me" type="date"></div>
        <div class="field full"><label for="md">Nội dung, mục tiêu</label><textarea id="md" rows="3"></textarea></div>
        <div class="msg full" id="mmsg" role="alert"></div>
        <button class="primary full" type="submit">Tạo phong trào</button>
      </form>
      <h3>Danh sách phong trào</h3>
      <div id="moveList"></div>
    </section>

    <section id="pViol" class="panel card" hidden>
      <h2>Lỗi vi phạm trong ngày</h2>
      <form id="violForm" class="row">
        <div class="field"><label for="vd">Ngày</label><input id="vd" type="date"></div>
        <div class="field"><label for="vcl">Lớp</label><input id="vcl" placeholder="VD: 8A1"></div>
        <div class="field full"><label for="vn">Học sinh vi phạm</label><input id="vn" placeholder="Họ và tên"></div>
        <div class="field"><label for="vt">Lỗi vi phạm</label><select id="vt"></select></div>
        <div class="field"><label for="vp">Điểm trừ</label><input id="vp" type="number" min="0" max="20" value="2"></div>
        <div class="field full"><label for="vnote">Ghi chú</label><input id="vnote" placeholder="Không bắt buộc"></div>
        <div class="msg full" id="vmsg2" role="alert"></div>
        <button class="primary full" type="submit">Lưu vi phạm</button>
      </form>
      <div class="filter"><label for="vf" style="margin:0">Xem ngày</label><input id="vf" type="date" style="width:auto"><span id="vsum" class="sum"></span></div>
      <div id="violList"></div>
    </section>
  </main>

  <div class="login-view">
    <section class="demo" aria-label="Trải nghiệm sản phẩm">
      <div class="stripe"><span>BẢN DEMO · DÀNH CHO BAN GIÁM KHẢO</span></div>
      <div class="demo-in">
        <div class="demo-top">
          <h2>📋 Trải nghiệm sản phẩm</h2>
          <div class="chips">
            <span class="chip gold">🏫 THPT Demo Sản Phẩm</span>
            <span class="chip">👥 1.050 học sinh · 25 lớp</span>
            <span class="chip">✏️ Dữ liệu mẫu</span>
            <span class="chip">🔑 Không cần mật khẩu</span>
          </div>
        </div>
        <div class="cols">
          <div>
            <h3>QUẢN LÝ</h3>
            <div class="grid1">
              <button class="role" data-role="Bí thư Đoàn"><span class="ic">👔</span><span><b>Bí thư Đoàn</b><small>Toàn trường</small></span></button>
              <button class="role" data-role="Quản lí lớp"><span class="ic">🏫</span><span><b>Quản lí lớp</b><small>Tài khoản lớp</small></span></button>
              <button class="role" data-role="Ủy viên BCH"><span class="ic">📁</span><span><b>Ủy viên BCH</b><small>Được phân quyền mảng</small></span></button>
            </div>
          </div>
          <div>
            <h3>HỌC SINH</h3>
            <div class="grid2">
              <button class="role" data-role="Học sinh"><span class="ic">🎓</span><span><b>Học sinh</b><small>Đoàn viên</small></span></button>
              <button class="role" data-role="Lớp trưởng"><span class="ic">👑</span><span><b>Lớp trưởng</b><small>Cán sự lớp</small></span></button>
              <button class="role" data-role="Bí thư Chi đoàn"><span class="ic">🎗️</span><span><b>Bí thư Chi đoàn</b><small>Cán sự lớp</small></span></button>
              <button class="role" data-role="Cờ đỏ lớp"><span class="ic">🚩</span><span><b>Cờ đỏ lớp</b><small>Chấm thi đua</small></span></button>
              <button class="role span2" data-role="Cờ đỏ trực cổng"><span class="ic">🚪</span><span><b>Cờ đỏ trực cổng</b><small>Ghi đi trễ ở cổng</small></span></button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="auth">
      <div class="divider">Tài khoản trường</div>
      <div class="tabs" role="tablist">
        <button class="tab" role="tab" aria-selected="true" id="t-login">Đăng nhập</button>
        <button class="tab" role="tab" aria-selected="false" id="t-reg">Tạo tài khoản</button>
      </div>

      <form class="card" id="loginForm" novalidate>
        <div class="field"><label for="u">Tên đăng nhập</label><input id="u" autocomplete="username"></div>
        <div class="field"><label for="p">Mật khẩu</label>
          <div class="pw"><input id="p" type="password" autocomplete="current-password"><button type="button" id="eye" aria-label="Hiện mật khẩu">👁️</button></div>
        </div>
        <div class="msg" id="msg" role="alert"></div>
        <button class="primary" type="submit">Đăng nhập</button>
        <a class="link" href="#quen-mat-khau" id="forgot">Quên mật khẩu?</a>
      </form>

      <form class="card" id="regForm" novalidate hidden>
        <div class="field"><label for="ru">Tên đăng nhập</label><input id="ru" autocomplete="username"></div>
        <div class="field"><label for="re">Gmail nhận mã xác nhận</label><input id="re" type="email" placeholder="ten@gmail.com" autocomplete="email"></div>
        <div class="field"><label for="rp">Mật khẩu (từ 6 ký tự)</label><input id="rp" type="password" autocomplete="new-password"></div>
        <div class="msg" id="rmsg" role="alert"></div>
        <button class="primary" type="submit">Gửi mã về Gmail</button>
      </form>

      <form class="card" id="verifyForm" novalidate hidden>
        <p style="margin:0 0 12px;font-size:.88rem">Mã 6 số đã được gửi tới <b id="vmail"></b>. Mã có hiệu lực 10 phút.</p>
        <div class="mailbox" id="mailbox"></div>
        <div class="field"><label for="vc">Mã xác nhận</label><input id="vc" inputmode="numeric" maxlength="6" autocomplete="one-time-code" style="letter-spacing:.4em;text-align:center;font-size:1.2rem"></div>
        <div class="msg" id="vmsg" role="alert"></div>
        <button class="primary" type="submit">Xác nhận &amp; tạo tài khoản</button>
        <a class="link" href="#" id="resend">Gửi lại mã</a>
        <a class="link" href="#" id="back" style="margin-top:6px;color:var(--muted)">Đổi Gmail</a>
      </form>

      <button class="install" id="install">📲 Cài app vào máy <small>(1 chạm · có thông báo)</small></button>
    </section>
  </div>
</div>

<script>
const $=s=>document.querySelector(s);
const enter=name=>{$('#who').textContent=name;document.body.classList.add('in');window.scrollTo(0,0)};
document.querySelectorAll('.role').forEach(b=>b.onclick=()=>enter(b.dataset.role));
$('#logout').onclick=()=>{document.body.classList.remove('in');$('#u').value='';$('#p').value=''};

$('#eye').onclick=()=>{const p=$('#p');p.type=p.type==='password'?'text':'password'};
const KEY='qld_accounts';
const getAcc=()=>{try{return JSON.parse(localStorage.getItem(KEY))||{}}catch(e){return {}}};
const saveAcc=a=>{try{localStorage.setItem(KEY,JSON.stringify(a))}catch(e){}};
const sha=async t=>[...new Uint8Array(await crypto.subtle.digest('SHA-256',new TextEncoder().encode(t)))].map(b=>b.toString(16).padStart(2,'0')).join('');
const say=(el,t,ok)=>{el.style.color=ok?'#15803d':'#c62828';el.textContent=t};
let pending=null;

function show(which){
  $('#t-login').setAttribute('aria-selected',which==='login');
  $('#t-reg').setAttribute('aria-selected',which!=='login');
  $('#loginForm').hidden=which!=='login';
  $('#regForm').hidden=which!=='reg';
  $('#verifyForm').hidden=which!=='verify';
}
$('#t-login').onclick=()=>show('login');
$('#t-reg').onclick=()=>show(pending?'verify':'reg');

$('#loginForm').onsubmit=async e=>{
  e.preventDefault();
  const u=$('#u').value.trim().toLowerCase(),p=$('#p').value;
  if(!u||!p){say($('#msg'),'Vui lòng nhập tên đăng nhập và mật khẩu.');return}
  if(u==='admin'&&p==='123456'){say($('#msg'),'');enter('Quản trị viên');return}
  const a=getAcc()[u];
  if(a&&a.hash===await sha(u+':'+p)){say($('#msg'),'');enter(u)}
  else say($('#msg'),'Sai tên đăng nhập hoặc mật khẩu.');
};

// Gửi mã. Bản demo không có máy chủ gửi mail nên hiện mã trong "hộp thư giả lập".
// Khi có máy chủ thật, thay nội dung hàm này bằng lệnh gọi dịch vụ gửi email.
async function sendCode(email,code){
  $('#mailbox').innerHTML='📬 <b>Hộp thư giả lập (bản demo)</b><br>Thư gửi tới '+email.replace(/</g,'&lt;')+': mã xác nhận của bạn là <b>'+code+'</b>';
}
function newCode(){const n=crypto.getRandomValues(new Uint32Array(1))[0]%1000000;return String(n).padStart(6,'0')}
async function issue(){
  pending.code=newCode();pending.exp=Date.now()+10*60*1000;pending.tries=0;
  await sendCode(pending.email,pending.code);
  $('#vmail').textContent=pending.email;$('#vc').value='';say($('#vmsg'),'');
}

$('#regForm').onsubmit=async e=>{
  e.preventDefault();
  const u=$('#ru').value.trim().toLowerCase(),em=$('#re').value.trim().toLowerCase(),p=$('#rp').value,m=$('#rmsg');
  if(!/^[a-z0-9._-]{3,}$/.test(u)){say(m,'Tên đăng nhập từ 3 ký tự, chỉ gồm chữ không dấu, số, . _ -');return}
  if(!/^[^\s@]+@gmail\.com$/.test(em)){say(m,'Vui lòng nhập địa chỉ Gmail hợp lệ (đuôi @gmail.com).');return}
  if(p.length<6){say(m,'Mật khẩu cần ít nhất 6 ký tự.');return}
  if(u==='admin'||getAcc()[u]){say(m,'Tên đăng nhập này đã có người dùng.');return}
  pending={user:u,email:em,hash:await sha(u+':'+p)};
  await issue();say(m,'');show('verify');
};
$('#verifyForm').onsubmit=e=>{
  e.preventDefault();
  const c=$('#vc').value.trim(),m=$('#vmsg');
  if(!pending)return;
  if(Date.now()>pending.exp){say(m,'Mã đã hết hạn. Bấm "Gửi lại mã".');return}
  if(pending.tries>=5){say(m,'Nhập sai quá nhiều lần. Bấm "Gửi lại mã" để nhận mã mới.');return}
  if(c!==pending.code){pending.tries++;say(m,'Mã chưa đúng, vui lòng kiểm tra lại.');return}
  const a=getAcc();a[pending.user]={email:pending.email,hash:pending.hash};saveAcc(a);
  $('#u').value=pending.user;$('#p').value='';pending=null;
  show('login');say($('#msg'),'Tạo tài khoản thành công! Hãy nhập mật khẩu để đăng nhập.',true);
  $('#p').focus();
};
$('#resend').onclick=async e=>{e.preventDefault();await issue();say($('#vmsg'),'Đã gửi mã mới.',true)};
$('#back').onclick=e=>{e.preventDefault();pending=null;show('reg')};
$('#forgot').onclick=e=>{e.preventDefault();say($('#msg'),'Liên hệ quản trị trường để đặt lại mật khẩu.')};


// ===== Báo cáo sau đăng nhập =====
const DK='qld_data';
const load=()=>{try{return Object.assign({movements:[],violations:[]},JSON.parse(localStorage.getItem(DK)))}catch(e){return {movements:[],violations:[]}}};
const store=d=>{try{localStorage.setItem(DK,JSON.stringify(d))}catch(e){}};
const esc=t=>String(t==null?'':t).replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));
const today=()=>{const d=new Date();return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0')};
const vdate=iso=>iso.split('-').reverse().join('/');
const TYPES=[['Đi trễ',2],['Không đồng phục',2],['Thiếu khăn quàng / huy hiệu',1],['Mất trật tự trong giờ',1],['Sử dụng điện thoại',3],['Xả rác bừa bãi',1],['Nghỉ học không phép',3],['Vi phạm khác',1]];
$('#vt').innerHTML=TYPES.map(t=>'<option>'+t[0]+'</option>').join('');
$('#vt').onchange=()=>{$('#vp').value=TYPES[$('#vt').selectedIndex][1]};
$('#vd').value=$('#vf').value=today();

document.querySelectorAll('.atab').forEach(b=>b.onclick=()=>{
  document.querySelectorAll('.atab').forEach(x=>x.setAttribute('aria-selected',x===b));
  $('#pMove').hidden=b.dataset.p!=='pMove';$('#pViol').hidden=b.dataset.p!=='pViol';
});

function renderMoves(){
  const m=load().movements;
  $('#moveList').innerHTML=m.length?m.slice().reverse().map(x=>'<div class="item"><div><b>'+esc(x.name)+'</b><small>'+vdate(x.start)+' → '+vdate(x.end)+'</small>'+(x.desc?'<small>'+esc(x.desc)+'</small>':'')+'</div><button class="del" data-id="'+x.id+'">Xóa</button></div>').join(''):'<div class="empty">Chưa có phong trào nào. Hãy tạo phong trào đầu tiên.</div>';
  $('#moveList').querySelectorAll('.del').forEach(b=>b.onclick=()=>{const d=load();d.movements=d.movements.filter(x=>String(x.id)!==b.dataset.id);store(d);renderMoves()});
}
$('#moveForm').onsubmit=e=>{
  e.preventDefault();
  const n=$('#mn').value.trim(),st=$('#ms').value,en=$('#me').value,m=$('#mmsg');
  if(!n||!st||!en){say(m,'Vui lòng nhập tên phong trào và ngày bắt đầu, kết thúc.');return}
  if(en<st){say(m,'Ngày kết thúc phải sau ngày bắt đầu.');return}
  const d=load();d.movements.push({id:Date.now(),name:n,start:st,end:en,desc:$('#md').value.trim(),by:$('#who').textContent});store(d);
  $('#moveForm').reset();say(m,'Đã tạo phong trào.',true);renderMoves();
};

function renderViol(){
  const day=$('#vf').value,l=load().violations.filter(v=>v.date===day);
  const tot=l.reduce((a,v)=>a+v.pts,0);
  $('#vsum').textContent=l.length+' lỗi · trừ '+tot+' điểm';
  $('#violList').innerHTML=l.length?l.slice().reverse().map(v=>'<div class="item"><div><b>'+esc(v.name)+'</b> · '+esc(v.cls)+'<small>'+esc(v.type)+(v.note?' — '+esc(v.note):'')+'</small><small>Ghi bởi '+esc(v.by)+'</small></div><div style="text-align:right"><div class="pts">-'+v.pts+'</div><button class="del" data-id="'+v.id+'">Xóa</button></div></div>').join(''):'<div class="empty">Chưa ghi nhận vi phạm nào trong ngày này.</div>';
  $('#violList').querySelectorAll('.del').forEach(b=>b.onclick=()=>{const d=load();d.violations=d.violations.filter(x=>String(x.id)!==b.dataset.id);store(d);renderViol()});
}
$('#vf').onchange=renderViol;
$('#violForm').onsubmit=e=>{
  e.preventDefault();
  const date=$('#vd').value,cls=$('#vcl').value.trim().toUpperCase(),name=$('#vn').value.trim(),m=$('#vmsg2');
  if(!date||!cls||!name){say(m,'Vui lòng nhập ngày, lớp và tên học sinh.');return}
  const d=load();d.violations.push({id:Date.now(),date,cls,name,type:$('#vt').value,pts:Math.max(0,+$('#vp').value||0),note:$('#vnote').value.trim(),by:$('#who').textContent});store(d);
  $('#vn').value='';$('#vnote').value='';$('#vf').value=date;say(m,'Đã lưu vi phạm.',true);renderViol();$('#vn').focus();
};
renderMoves();renderViol();

let deferred;
addEventListener('beforeinstallprompt',e=>{e.preventDefault();deferred=e});
$('#install').onclick=()=>{deferred?deferred.prompt():alert('Trên điện thoại: mở menu trình duyệt → "Thêm vào màn hình chính".')};
</script>
</body>
</html>
