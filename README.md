<!doctype html>
<html lang="th">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no" />
<title>CoupleSplit — ต้น & แป๋ม</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Mitr:wght@300;400;500&display=swap');
:root {
  --main: #ffb6c1;
  --accent: #ff8fab;
  --bg: #fff6fa;
  --shadow: rgba(255,182,193,0.4);
}
*{box-sizing:border-box;}
body {
  margin:0;
  font-family:'Mitr', sans-serif;
  background: linear-gradient(160deg,#ffe4ec,#fff6fa,#ffeaf4);
  color:#444;
  display:flex;
  justify-content:center;
  align-items:flex-start;
  min-height:100vh;
}
.wrap {
  width:100%;
  max-width:480px;
  margin:20px;
  background:rgba(255,255,255,0.8);
  backdrop-filter:blur(10px);
  border-radius:24px;
  box-shadow:0 8px 20px var(--shadow);
  overflow:hidden;
  animation:fadeIn 0.5s ease;
}
header {
  background:linear-gradient(45deg,var(--main),var(--accent));
  color:white;
  padding:20px 10px;
  text-align:center;
  border-radius:24px 24px 0 0;
}
.logo{font-size:40px;}
h1{margin:6px 0 0 0;font-size:24px;}
.names{display:flex;justify-content:center;align-items:center;gap:10px;margin-top:10px;flex-wrap:wrap;}
.name-field input{
  padding:8px;
  border:none;
  border-radius:10px;
  width:100px;
  text-align:center;
  font-weight:500;
  color:#555;
}
.swap{
  background:white;
  color:var(--accent);
  border-radius:50%;
  width:36px;height:36px;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;
  box-shadow:0 3px 8px var(--shadow);
  transition:transform 0.2s;
}
.swap:hover{transform:rotate(180deg) scale(1.1);}
main{padding:20px;}
.add-card{
  background:white;
  border-radius:18px;
  padding:16px;
  box-shadow:0 4px 12px var(--shadow);
}
.add-card input,select{
  width:100%;
  margin:6px 0;
  padding:10px;
  border:1px solid #ffdbe6;
  border-radius:12px;
  font-size:15px;
}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.btn{
  border:none;
  border-radius:12px;
  padding:10px;
  cursor:pointer;
  font-weight:600;
  transition:transform 0.1s,box-shadow 0.2s;
}
.btn:active{transform:scale(0.95);}
.btn.primary{
  background:var(--accent);
  color:white;
  box-shadow:0 4px 10px var(--shadow);
}
.btn.primary:hover{background:#ff99b5;}
.btn.danger{
  background:#ff8c94;
  color:white;
}
.btn.danger:hover{background:#ff757d;}
.list{margin-top:14px;display:flex;flex-direction:column;gap:8px;}
.item{
  background:rgba(255,255,255,0.9);
  border-radius:14px;
  padding:10px 14px;
  box-shadow:0 2px 8px var(--shadow);
  display:flex;justify-content:space-between;align-items:center;
  animation:itemIn 0.4s ease;
}
.item span{font-size:15px;}
#billPopup{
  position:fixed;
  inset:0;
  background:rgba(0,0,0,0.4);
  backdrop-filter:blur(5px);
  display:none;
  justify-content:center;
  align-items:center;
  animation:fadeIn 0.3s ease;
  z-index:10;
}
#billContent{
  background:white;
  border-radius:20px;
  padding:20px;
  width:90%;
  max-width:400px;
  box-shadow:0 4px 15px var(--shadow);
  animation:popin 0.4s ease;
}
#billContent h2{
  text-align:center;
  margin-top:0;
  color:var(--accent);
}
.bill-item{display:flex;justify-content:space-between;border-bottom:1px solid #f1f1f1;padding:6px 0;}
.bill-summary{text-align:center;font-weight:bold;color:var(--accent);margin-top:10px;}
.close-bill{
  margin:16px auto 0 auto;
  display:block;
  background:var(--accent);
  color:white;
  border:none;
  border-radius:12px;
  padding:8px 20px;
  font-weight:600;
  cursor:pointer;
  transition:transform 0.2s;
}
.close-bill:hover{transform:scale(1.05);}
@keyframes fadeIn{from{opacity:0;}to{opacity:1;}}
@keyframes itemIn{from{opacity:0;transform:translateY(10px);}to{opacity:1;transform:translateY(0);}}
@keyframes popin{from{transform:scale(0.9);opacity:0;}to{transform:scale(1);opacity:1;}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <div class="logo">💖</div>
    <h1>CoupleSplit</h1>
    <div class="names">
      <div class="name-field"><input type="text" id="you" placeholder="ต้น"></div>
      <div class="swap" id="swapBtn">🔄</div>
      <div class="name-field"><input type="text" id="partner" placeholder="แป๋ม"></div>
    </div>
  </header>
  <main>
    <div class="add-card">
      <input type="text" id="title" placeholder="ชื่อรายการ เช่น ข้าว">
      <input type="number" id="amount" placeholder="จำนวนเงินเต็ม (บาท)">
      <div class="grid2">
        <select id="payer">
          <option value="you">คุณจ่าย</option>
          <option value="partner">คู่รักจ่าย</option>
        </select>
        <button class="btn primary" id="addBtn">เพิ่มรายการ 💕</button>
      </div>
    </div>
    <div class="list" id="list"></div>
    <button class="btn primary" id="showBillBtn">ดูบิลสรุป 💌</button>
  </main>
</div>

<div id="billPopup">
  <div id="billContent">
    <h2>บิลสรุปค่าใช้จ่าย 💝</h2>
    <div id="billItems"></div>
    <div class="bill-summary" id="billSummary"></div>
    <button class="close-bill" id="closeBillBtn">ปิด</button>
  </div>
</div>

<audio id="clickSound" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_1c81d0299e.mp3?filename=button-click-124467.mp3"></audio>
<audio id="popupSound" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_6219e30acb.mp3?filename=pop-up-124463.mp3"></audio>

<script>
let youInput = document.getElementById('you');
let partnerInput = document.getElementById('partner');
let swapBtn = document.getElementById('swapBtn');
let title = document.getElementById('title');
let amount = document.getElementById('amount');
let payer = document.getElementById('payer');
let addBtn = document.getElementById('addBtn');
let list = document.getElementById('list');
let showBillBtn = document.getElementById('showBillBtn');
let billPopup = document.getElementById('billPopup');
let billItems = document.getElementById('billItems');
let billSummary = document.getElementById('billSummary');
let closeBillBtn = document.getElementById('closeBillBtn');
let clickSound = document.getElementById('clickSound');
let popupSound = document.getElementById('popupSound');

let expenses = JSON.parse(localStorage.getItem('expenses')||'[]');

swapBtn.onclick = () => {
  const tmp = youInput.value;
  youInput.value = partnerInput.value;
  partnerInput.value = tmp;
  clickSound.play();
};

addBtn.onclick = () => {
  const t = title.value.trim(), a = parseFloat(amount.value);
  if(!t||!a||a<=0){alert('กรุณากรอกข้อมูลให้ครบ'); return;}
  const nameAtEntry = payer.value==='you'?youInput.value:partnerInput.value;
  expenses.push({title:t,amount:a,payer:payer.value,nameAtEntry});
  title.value='';amount.value='';
  save();render();clickSound.play();
};

function save(){localStorage.setItem('expenses',JSON.stringify(expenses));}
function render(){
  list.innerHTML='';
  expenses.forEach((ex,i)=>{
    const item=document.createElement('div');
    item.className='item';
    item.innerHTML=`<span>${ex.nameAtEntry} ซื้อ ${ex.title} ${ex.amount.toFixed(2)} บาท</span>
    <button class="btn danger" onclick="deleteItem(${i})">ลบ</button>`;
    list.appendChild(item);
  });
}
function deleteItem(i){
  if(confirm('ลบรายการนี้ไหม?')){
    expenses.splice(i,1);
    save();render();clickSound.play();
  }
}
showBillBtn.onclick=()=>{
  billItems.innerHTML='';
  let totalYou=0,totalPartner=0;
  expenses.forEach(ex=>{
    const div=document.createElement('div');
    div.className='bill-item';
    div.innerHTML=`<span>${ex.nameAtEntry} ซื้อ ${ex.title}</span><span>${ex.amount.toFixed(2)} ฿</span>`;
    billItems.appendChild(div);
    if(ex.payer==='you') totalYou+=ex.amount; else totalPartner+=ex.amount;
  });
  let total=totalYou+totalPartner;
  let half=total/2;
  let youOwe=half-totalYou;
  if(Math.abs(youOwe)<0.01){
    billSummary.textContent='ยอดเสมอกัน ไม่มีใครติดใคร 💞';
  } else if(youOwe>0){
    billSummary.textContent=`${youInput.value} ติด ${partnerInput.value}: ${youOwe.toFixed(2)} ฿ 💗`;
  } else {
    billSummary.textContent=`${partnerInput.value} ติด ${youInput.value}: ${(-youOwe).toFixed(2)} ฿ 💗`;
  }
  billPopup.style.display='flex';
  popupSound.play();
}
closeBillBtn.onclick=()=>{billPopup.style.display='none';clickSound.play();}
render();
</script>
</body>
</html>
