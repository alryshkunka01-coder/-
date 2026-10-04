<!doctype html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CASELAB — CS2 Case Demo</title>
<style>
:root{
  --bg:#0b0d10; --panel:#111419; --panel2:#171b21; --line:#262c34;
  --text:#e9edf2; --muted:#8c95a1; --accent:#ffb000; --blue:#5da9ff;
  --purple:#b77cff; --pink:#ff5f9e; --red:#ff625f; --gold:#ffd15c;
}
*{box-sizing:border-box}
body{margin:0;background:radial-gradient(circle at 50% -20%,#202630 0,#0b0d10 42%);color:var(--text);font:14px Arial,Helvetica,sans-serif}
button,input{font:inherit}
button{cursor:pointer}
.top{height:64px;border-bottom:1px solid var(--line);background:rgba(12,14,18,.94);display:flex;align-items:center;gap:28px;padding:0 30px;position:sticky;top:0;z-index:20;backdrop-filter:blur(10px)}
.logo{font-weight:900;letter-spacing:1.6px;font-size:20px}
.logo span{color:var(--accent)}
.nav{display:flex;gap:8px}
.nav button{border:0;background:transparent;color:#aeb6c0;padding:10px 13px;border-radius:8px}
.nav button:hover,.nav button.active{background:#1a1f26;color:#fff}
.wallet{margin-left:auto;display:flex;align-items:center;gap:10px}
.balance{background:#171b21;border:1px solid var(--line);padding:10px 14px;border-radius:8px;font-weight:700}
.reset{background:#20252c;color:#b9c1cb;border:1px solid var(--line);padding:10px 12px;border-radius:8px}
main{max-width:1240px;margin:0 auto;padding:28px 24px 50px}
.page{display:none}.page.active{display:block}
h1{font-size:28px;margin:0 0 8px}.sub{color:var(--muted);margin-bottom:24px}
.grid{display:grid;grid-template-columns:repeat(4,1fr);gap:15px}
.card{background:linear-gradient(180deg,#171b21,#111419);border:1px solid var(--line);border-radius:12px;overflow:hidden;transition:.18s;position:relative}
.card:hover{transform:translateY(-3px);border-color:#3a434f}
.case-art{height:180px;background:
 linear-gradient(135deg,rgba(255,176,0,.14),transparent 35%),
 linear-gradient(160deg,#242a32,#0c0f13);
display:flex;align-items:center;justify-content:center;position:relative}
.case-box{width:175px;height:112px;border-radius:7px;background:linear-gradient(180deg,#39424c,#1d232b);border:2px solid #68737f;box-shadow:0 20px 40px #0008,inset 0 2px #9ca6b0;position:relative}
.case-box:before,.case-box:after{content:"";position:absolute;top:-6px;bottom:-6px;width:8px;background:#4c5662;border:1px solid #737d88}.case-box:before{left:12px}.case-box:after{right:12px}
.case-label{position:absolute;left:18px;right:18px;top:29px;height:48px;border-radius:4px;background:#111419;border:1px solid #707b86;display:flex;align-items:center;justify-content:center;color:#dce3eb;font-weight:800;letter-spacing:1px}
.case-lock{position:absolute;bottom:10px;left:50%;transform:translateX(-50%);width:20px;height:15px;border:2px solid #7c8793;border-radius:3px}
.card-body{padding:14px}.row{display:flex;justify-content:space-between;align-items:center;gap:10px}
.title{font-weight:800;font-size:16px}.price{color:var(--accent);font-weight:800}
.small{color:var(--muted);font-size:12px;margin-top:6px}
.btn{border:0;border-radius:8px;padding:11px 14px;font-weight:800}
.btn.primary{background:var(--accent);color:#16110a}.btn.dark{background:#1c2229;color:#dbe1e8;border:1px solid var(--line)}
.btn.full{width:100%;margin-top:12px}
.open-wrap{display:grid;grid-template-columns:310px 1fr;gap:20px}
.preview{background:#12161b;border:1px solid var(--line);border-radius:12px;padding:18px}
.reel{margin-top:15px;height:165px;border:1px solid #303740;border-radius:8px;background:#0d1014;overflow:hidden;position:relative}
.marker{position:absolute;left:50%;top:0;bottom:0;width:2px;background:var(--accent);z-index:3;box-shadow:0 0 18px #ffb00088}
.items{height:100%;display:flex;align-items:center;gap:10px;padding:0 40px;transform:translateX(0)}
.skin{min-width:155px;height:115px;background:#151a20;border:1px solid #2a3139;border-radius:8px;padding:10px;display:flex;flex-direction:column;justify-content:space-between}
.skin-img{height:66px;border-radius:5px;background:linear-gradient(135deg,#222a34,#0e1115);display:flex;align-items:center;justify-content:center;color:#687583;font-size:32px}
.skin.blue{border-bottom:3px solid var(--blue)} .skin.purple{border-bottom:3px solid var(--purple)}
.skin.pink{border-bottom:3px solid var(--pink)} .skin.red{border-bottom:3px solid var(--red)} .skin.gold{border-bottom:3px solid var(--gold)}
.skin-name{font-size:12px;font-weight:700}.skin-price{font-size:11px;color:var(--muted)}
.result{margin-top:15px;padding:14px;border:1px solid var(--line);border-radius:8px;background:#13171c}
.result strong{color:#fff}.muted{color:var(--muted)}
.upgrade{display:grid;grid-template-columns:1fr 1.15fr;gap:20px}
.panel{background:#111419;border:1px solid var(--line);border-radius:12px;padding:18px}
.item-list{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;max-height:500px;overflow:auto}
.inv-item{padding:10px;border:1px solid var(--line);border-radius:8px;background:#15191e}.inv-item.selected{border-color:var(--accent);box-shadow:0 0 0 1px var(--accent) inset}
.inv-item .skin-img{height:72px}.inv-item button{margin-top:7px}
.inputrow{display:flex;gap:10px;align-items:center}.percent{display:flex;align-items:center;gap:10px;margin:18px 0}
.percent input[type=number]{width:100px;background:#0d1115;border:1px solid var(--line);color:#fff;padding:10px;border-radius:8px}
.percent input[type=range]{flex:1}
.bigchance{font-size:42px;font-weight:900;margin:8px 0}.target-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;max-height:410px;overflow:auto}
.target{cursor:pointer;padding:10px;border:1px solid var(--line);border-radius:8px;background:#15191e}.target.selected{border-color:var(--blue);box-shadow:0 0 0 1px var(--blue) inset}
.note{color:#7f8995;font-size:12px;line-height:1.5;margin-top:10px}
.toast{position:fixed;right:20px;bottom:20px;background:#171c22;border:1px solid #38414b;padding:12px 16px;border-radius:8px;display:none;z-index:50}
@media(max-width:1000px){.grid{grid-template-columns:repeat(3,1fr)}.open-wrap,.upgrade{grid-template-columns:1fr}}
@media(max-width:720px){.grid{grid-template-columns:repeat(2,1fr)}.top{padding:0 14px}.nav{gap:0}.nav button{padding:9px 7px}.wallet .reset{display:none}.item-list,.target-grid{grid-template-columns:repeat(2,1fr)}}
</style>
</head>
<body>
<header class="top">
  <div class="logo">CASE<span>LAB</span></div>
  <nav class="nav">
    <button class="active" data-page="cases">Cases</button>
    <button data-page="upgrade">Upgrade</button>
    <button data-page="inventory">Inventory</button>
  </nav>
  <div class="wallet"><div class="balance">🪙 <span id="balance">10000</span> C</div><button class="reset" id="reset">Reset</button></div>
</header>

<main>
<section id="cases" class="page active">
  <h1>Cases</h1><div class="sub">Открывай контейнеры и собирай виртуальную коллекцию.</div>
  <div class="grid" id="caseGrid"></div>
</section>

<section id="open" class="page">
  <div class="open-wrap">
    <div class="preview">
      <div class="small">CASE</div><h1 id="openTitle">Case</h1>
      <div class="small">Цена открытия: <span class="price" id="openPrice">0 C</span></div>
      <button class="btn primary full" id="openBtn">Открыть кейс</button>
      <button class="btn dark full" id="backCases">Назад к кейсам</button>
      <div class="note">Демо-режим: используются только виртуальные монеты.</div>
    </div>
    <div class="preview">
      <div class="small">ROLL</div>
      <div class="reel"><div class="marker"></div><div class="items" id="reelItems"></div></div>
      <div class="result" id="caseResult">Выбери кейс и нажми «Открыть кейс».</div>
    </div>
  </div>
</section>

<section id="upgrade" class="page">
  <h1>Upgrade</h1><div class="sub">Выбери свой предмет, target и установи шанс вручную.</div>
  <div class="upgrade">
    <div class="panel">
      <div class="row"><strong>Твой предмет</strong><span class="muted">выбери один</span></div>
      <div class="item-list" id="invSelect"></div>
    </div>
    <div class="panel">
      <div class="row"><strong>Target</strong><span class="muted">выбери один</span></div>
      <div class="target-grid" id="targetSelect"></div>
      <div class="percent">
        <input type="range" min="0" max="100" step="0.01" id="chanceRange" value="50">
        <input type="number" min="0" max="100" step="0.01" id="chanceInput" value="50">
        <b>%</b>
      </div>
      <div class="bigchance" id="chanceText">50.00%</div>
      <div class="muted" id="upgradeInfo">Выбери предмет и target.</div>
      <button class="btn primary full" id="upgradeBtn">UPGRADE</button>
      <div class="note">Шанс в этой демо-версии задаётся вручную и не зависит от цены предметов.</div>
    </div>
  </div>
</section>

<section id="inventory" class="page">
  <h1>Inventory</h1><div class="sub">Твои виртуальные предметы.</div>
  <div class="grid" id="inventoryGrid"></div>
</section>
</main>

<div class="toast" id="toast"></div>

<script>
const SKINS = [
 {id:1,name:'AK-47 | Elite Build',price:120,rarity:'blue',icon:'🔫'},
 {id:2,name:'Glock-18 | Vogue',price:170,rarity:'blue',icon:'🔫'},
 {id:3,name:'MP9 | Starlight Protector',price:220,rarity:'blue',icon:'🔫'},
 {id:4,name:'P250 | See Ya Later',price:320,rarity:'purple',icon:'🔫'},
 {id:5,name:'USP-S | Cortex',price:430,rarity:'purple',icon:'🔫'},
 {id:6,name:'M4A4 | The Emperor',price:900,rarity:'pink',icon:'🔫'},
 {id:7,name:'AK-47 | Neon Rider',price:1150,rarity:'pink',icon:'🔫'},
 {id:8,name:'AWP | Asiimov',price:1800,rarity:'red',icon:'🎯'},
 {id:9,name:'M4A1-S | Printstream',price:2200,rarity:'red',icon:'🔫'},
 {id:10,name:'AWP | Dragon Lore',price:8500,rarity:'gold',icon:'🏆'},
 {id:11,name:'Karambit | Doppler',price:5200,rarity:'gold',icon:'🔪'},
 {id:12,name:'Butterfly Knife | Doppler',price:6800,rarity:'gold',icon:'🔪'}
];

const CASES = [
 {name:'Starter Case',price:120,pool:[1,2,3,4]},
 {name:'Prisma Case',price:280,pool:[1,2,3,4,5]},
 {name:'Recoil Case',price:520,pool:[2,3,4,5,6]},
 {name:'Kilowatt Case',price:850,pool:[3,4,5,6,7]},
 {name:'Revolution Case',price:1200,pool:[4,5,6,7,8]},
 {name:'Premium Case',price:1800,pool:[5,6,7,8,9]},
 {name:'Redline Case',price:2600,pool:[6,7,8,9,11]},
 {name:'Elite Case',price:3600,pool:[7,8,9,11,12]},
 {name:'Gold Case',price:5200,pool:[8,9,10,11,12]},
 {name:'Blackout Case',price:7000,pool:[9,10,11,12]}
];

let state = JSON.parse(localStorage.getItem('caselab') || 'null') || {
 balance:10000, inventory:[1,2,3]
};
let selectedCase=null, selectedInv=null, selectedTarget=null;

function save(){localStorage.setItem('caselab',JSON.stringify(state))}
function money(n){return Number(n).toLocaleString('ru-RU')}
function skin(id){return SKINS.find(x=>x.id===Number(id))}
function toast(msg){const el=document.getElementById('toast');el.textContent=msg;el.style.display='block';clearTimeout(window.t);window.t=setTimeout(()=>el.style.display='none',2400)}
function skinCard(s,buttonText='Выбрать',cls=''){
 return `<div class="skin ${s.rarity}"><div class="skin-img">${s.icon}</div><div class="skin-name">${s.name}</div><div class="row"><span class="skin-price">${money(s.price)} C</span>${cls?`<span class="small">${cls}</span>`:''}</div><button class="btn dark full" style="margin-top:6px">${buttonText}</button></div>`
}
function renderCases(){
 const el=document.getElementById('caseGrid'); el.innerHTML='';
 CASES.forEach((c,i)=>{
   const node=document.createElement('div');node.className='card';
   node.innerHTML=`<div class="case-art"><div class="case-box"><div class="case-label">${c.name.toUpperCase()}</div><div class="case-lock"></div></div></div>
   <div class="card-body"><div class="row"><div class="title">${c.name}</div><div class="price">${money(c.price)} C</div></div>
   <div class="small">${c.pool.length} possible items</div><button class="btn primary full">OPEN CASE</button></div>`;
   node.querySelector('button').onclick=()=>openCasePage(i); el.appendChild(node);
 });
}
function openCasePage(i){
 selectedCase=i; const c=CASES[i];
 document.getElementById('openTitle').textContent=c.name;
 document.getElementById('openPrice').textContent=money(c.price)+' C';
 document.getElementById('caseResult').innerHTML='Готово к открытию.';
 document.getElementById('reelItems').innerHTML=c.pool.concat(c.pool,c.pool).map(id=>skinCard(skin(id),'','')).join('');
 showPage('open');
}
document.getElementById('openBtn').onclick=()=>{
 if(selectedCase===null)return;
 const c=CASES[selectedCase];
 if(state.balance<c.price){toast('Недостаточно виртуальных монет');return}
 state.balance-=c.price;
 const rewardId=c.pool[Math.floor(Math.random()*c.pool.length)];
 const reward=skin(rewardId);
 const items=document.getElementById('reelItems'); items.style.transition='none';items.style.transform='translateX(0)';
 void items.offsetWidth;
 const cardWidth=165;
 const idx=c.pool.length*2+Math.floor(Math.random()*c.pool.length);
 const offset=Math.max(0,idx*cardWidth-430);
 items.style.transition='transform 2.7s cubic-bezier(.12,.82,.16,1)';
 items.style.transform=`translateX(-${offset}px)`;
 setTimeout(()=>{
   state.inventory.push(rewardId);save();renderAll();
   document.getElementById('caseResult').innerHTML=`Вы выиграли <strong>${reward.name}</strong> за <strong>${money(reward.price)} C</strong>.`;
   toast(`Получен ${reward.name}`);
 },2750);
};
document.getElementById('backCases').onclick=()=>showPage('cases');

function renderInventory(){
 const el=document.getElementById('inventoryGrid'); el.innerHTML='';
 state.inventory.forEach((id,idx)=>{
   const s=skin(id); if(!s)return;
   const n=document.createElement('div'); n.className='card';n.innerHTML=`<div style="padding:14px">${skinCard(s,'В Upgrade')}</div>`;
   n.querySelector('button').onclick=()=>{showPage('upgrade');selectInv(idx)};
   el.appendChild(n);
 });
 if(!state.inventory.length) el.innerHTML='<div class="muted">Инвентарь пуст.</div>';
}
function selectInv(index){
 selectedInv=index;
 document.querySelectorAll('#invSelect .inv-item').forEach((x,i)=>x.classList.toggle('selected',i===index));
 updateUpgradeInfo();
}
function renderUpgradeLists(){
 const inv=document.getElementById('invSelect');inv.innerHTML='';
 state.inventory.forEach((id,i)=>{
   const s=skin(id); if(!s)return;
   const d=document.createElement('div');d.className='inv-item'+(i===selectedInv?' selected':'');
   d.innerHTML=`<div class="skin ${s.rarity}"><div class="skin-img">${s.icon}</div><div class="skin-name">${s.name}</div><div class="skin-price">${money(s.price)} C</div></div>`;
   d.onclick=()=>selectInv(i);inv.appendChild(d);
 });
 const tg=document.getElementById('targetSelect');tg.innerHTML='';
 SKINS.filter(s=>!selectedInv===false || true).forEach(s=>{
   const d=document.createElement('div');d.className='target'+(selectedTarget===s.id?' selected':'');
   d.innerHTML=`<div class="skin ${s.rarity}"><div class="skin-img">${s.icon}</div><div class="skin-name">${s.name}</div><div class="skin-price">${money(s.price)} C</div></div>`;
   d.onclick=()=>{selectedTarget=s.id;renderUpgradeLists();updateUpgradeInfo()};tg.appendChild(d);
 });
 updateUpgradeInfo();
}
function updateUpgradeInfo(){
 const a=selectedInv===null?null:skin(state.inventory[selectedInv]);
 const b=selectedTarget===null?null:skin(selectedTarget);
 const chance=Number(document.getElementById('chanceInput').value||0);
 document.getElementById('chanceText').textContent=chance.toFixed(2)+'%';
 document.getElementById('upgradeInfo').textContent =
   a&&b ? `${a.name} (${money(a.price)} C) → ${b.name} (${money(b.price)} C)` : 'Выбери предмет и target.';
}
['chanceRange','chanceInput'].forEach(id=>document.getElementById(id).addEventListener('input',e=>{
 let v=Math.max(0,Math.min(100,Number(e.target.value||0)));
 document.getElementById('chanceRange').value=v;document.getElementById('chanceInput').value=v;updateUpgradeInfo();
}));
document.getElementById('upgradeBtn').onclick=()=>{
 if(selectedInv===null||selectedTarget===null){toast('Выбери исходный и целевой скин');return}
 const chance=Math.max(0,Math.min(100,Number(document.getElementById('chanceInput').value||0)));
 const target=skin(selectedTarget), source=skin(state.inventory[selectedInv]);
 if(chance>=100){
   state.inventory[selectedInv]=target.id; save(); renderAll(); selectedInv=null;
   toast('Upgrade успешен на 100%'); return;
 }
 const win=Math.random()*100<chance;
 if(win){
   state.inventory[selectedInv]=target.id;toast(`Успех! Получен ${target.name}`);
 }else{
   state.inventory.splice(selectedInv,1);toast(`Неудача. ${source.name} потерян`);
 }
 save();selectedInv=null;selectedTarget=null;renderAll();
};
document.getElementById('reset').onclick=()=>{
 state={balance:10000,inventory:[1,2,3]};selectedInv=null;selectedTarget=null;save();renderAll();toast('Демо сброшено');
};
document.querySelectorAll('.nav button').forEach(btn=>btn.onclick=()=>showPage(btn.dataset.page));
function showPage(page){
 document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
 document.getElementById(page).classList.add('active');
 document.querySelectorAll('.nav button').forEach(b=>b.classList.toggle('active',b.dataset.page===page));
 if(page==='upgrade')renderUpgradeLists();
 if(page==='inventory')renderInventory();
}
function renderAll(){
 document.getElementById('balance').textContent=money(state.balance);
 renderCases();renderInventory();if(document.getElementById('upgrade').classList.contains('active'))renderUpgradeLists();
}
renderAll();
</script>
</body>
</html>
