<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Two-Week Training Planner</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;background:#f5f4f0;padding:1.5rem;color:#1a1a18}
.planner{max-width:960px;margin:0 auto}
.week-section{margin-bottom:1.25rem}
.week-label{font-size:11px;font-weight:500;color:#5f5e5a;text-transform:uppercase;letter-spacing:0.05em;margin-bottom:6px;display:flex;align-items:center;gap:8px}
.week-label-line{flex:1;height:0.5px;background:#d3d1c7}
.week-status{font-size:10px;font-weight:500;padding:2px 8px;border-radius:20px;white-space:nowrap;flex-shrink:0}
.ws-ok{background:#EAF3DE;color:#3B6D11;border:0.5px solid #C0DD97}
.ws-warn{background:#FCEBEB;color:#A32D2D;border:0.5px solid #F7C1C1}
.ws-info{background:#eeecea;color:#5f5e5a;border:0.5px solid #d3d1c7}
.week-grid{display:grid;grid-template-columns:repeat(7,minmax(0,1fr));gap:5px}
.day-col{min-height:110px;border:0.5px solid #d3d1c7;border-radius:8px;padding:6px;background:#eeecea;transition:border 0.1s,background 0.1s}
.day-col.highlight{border:1.5px dashed #888780;background:#fff}
.day-col.conflict{border:1px solid rgba(226,75,74,0.35);background:rgba(252,235,235,0.2)}
.day-header{font-size:10px;font-weight:500;color:#5f5e5a;text-transform:uppercase;letter-spacing:0.04em;margin-bottom:5px;text-align:center}
.day-header span{display:block;font-size:15px;font-weight:500;color:#1a1a18;letter-spacing:0;text-transform:none}
.drop-zone{min-height:50px;display:flex;flex-direction:column;gap:3px}
.workout-card{border-radius:5px;padding:4px 6px;font-size:11px;font-weight:500;cursor:grab;user-select:none;border:0.5px solid transparent;transition:opacity 0.12s,transform 0.1s;display:flex;align-items:center;justify-content:space-between;gap:3px}
.workout-card:active{cursor:grabbing;opacity:0.6;transform:scale(0.96)}
.workout-card.dragging{opacity:0.35}
.card-label{flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.card-actions{display:none;gap:2px;flex-shrink:0}
.workout-card:hover .card-actions{display:flex}
.card-btn{background:none;border:none;cursor:pointer;padding:1px 3px;border-radius:3px;font-size:10px;opacity:0.65;line-height:1}
.card-btn:hover{opacity:1;background:rgba(0,0,0,0.08)}
.wc-strength{background:#E6F1FB;color:#0C447C;border-color:#B5D4F4}
.wc-cardio-z2{background:#EAF3DE;color:#27500A;border-color:#C0DD97}
.wc-cardio-hi{background:#FAEEDA;color:#633806;border-color:#FAC775}
.wc-wrestling{background:#EEEDFE;color:#3C3489;border-color:#CECBF6}
.wc-custom{background:#eeecea;color:#1a1a18;border-color:#888780}
.bank-row{display:flex;flex-wrap:wrap;gap:5px;padding:8px 10px;border:0.5px solid #d3d1c7;border-radius:8px;background:#fff;min-height:38px;align-items:flex-start}
.top-bar{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px;flex-wrap:wrap;gap:6px}
.top-bar-right{display:flex;gap:6px;flex-wrap:wrap;align-items:center}
.legend{display:flex;flex-wrap:wrap;gap:6px}
.leg-item{display:flex;align-items:center;gap:4px;font-size:11px;color:#5f5e5a}
.leg-dot{width:9px;height:9px;border-radius:50%;flex-shrink:0}
.btn-sm{font-size:11px;padding:4px 9px;cursor:pointer;border-radius:6px;border:0.5px solid #888780;background:transparent;color:#5f5e5a;white-space:nowrap}
.btn-sm:hover{background:#eeecea}
.btn-primary{background:#E6F1FB;color:#0C447C;border-color:#B5D4F4}
.btn-primary:hover{background:#B5D4F4}
.btn-advance{background:#EEEDFE;color:#3C3489;border-color:#CECBF6}
.btn-advance:hover{background:#CECBF6}
.btn-save{background:#EAF3DE;color:#27500A;border-color:#C0DD97}
.btn-save:hover{background:#C0DD97}
.btn-divider{width:0.5px;height:18px;background:#d3d1c7;align-self:center}
.save-indicator{font-size:10px;color:#3B6D11;opacity:0;transition:opacity 0.3s;align-self:center}
.save-indicator.show{opacity:1}
.global-warns{display:flex;flex-direction:column;gap:3px;margin:6px 0 8px}
.warn{font-size:11px;color:#A32D2D;background:#FCEBEB;border:0.5px solid #F7C1C1;border-radius:5px;padding:3px 8px}
.info-msg{font-size:11px;color:#5f5e5a;background:#eeecea;border:0.5px solid #d3d1c7;border-radius:5px;padding:3px 8px}
.section-label{font-size:11px;font-weight:500;color:#5f5e5a;text-transform:uppercase;letter-spacing:0.04em;margin-bottom:5px}
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,0.35);display:flex;align-items:center;justify-content:center;z-index:100}
.modal{background:#fff;border:0.5px solid #888780;border-radius:12px;padding:18px;width:300px;max-width:90vw}
.modal h3{font-size:14px;font-weight:500;margin-bottom:14px;color:#1a1a18}
.modal p{font-size:12px;color:#5f5e5a;margin-bottom:14px;line-height:1.6}
.modal label{font-size:12px;color:#5f5e5a;display:block;margin-bottom:3px}
.modal input,.modal select{width:100%;padding:6px 8px;font-size:13px;border:0.5px solid #888780;border-radius:6px;background:#eeecea;color:#1a1a18;margin-bottom:10px;outline:none}
.modal input:focus,.modal select:focus{border-color:#444441}
.modal-actions{display:flex;justify-content:flex-end;gap:6px;margin-top:4px}
.modal-del{margin-right:auto}
</style>
</head>
<body>
<div class="planner">
  <div class="top-bar">
    <div class="legend">
      <div class="leg-item"><div class="leg-dot" style="background:#378ADD"></div>Strength</div>
      <div class="leg-item"><div class="leg-dot" style="background:#639922"></div>Z2</div>
      <div class="leg-item"><div class="leg-dot" style="background:#BA7517"></div>Threshold/VO2</div>
      <div class="leg-item"><div class="leg-dot" style="background:#7F77DD"></div>Wrestling</div>
    </div>
    <div class="top-bar-right">
      <span class="save-indicator" id="save-indicator">Saved ✓</span>
      <button class="btn-sm btn-save" onclick="saveState()">Save</button>
      <div class="btn-divider"></div>
      <button class="btn-sm btn-advance" onclick="confirmAdvanceWeek()">Advance week →</button>
      <button class="btn-sm btn-primary" onclick="openAddModal()">+ New workout</button>
      <button class="btn-sm" onclick="confirmReset()">Reset</button>
    </div>
  </div>

  <div class="week-section">
    <div class="week-label">Week 1 <div class="week-label-line"></div><span class="week-status ws-info" id="status-w1">—</span></div>
    <div class="week-grid" id="grid-w1"></div>
  </div>
  <div class="week-section">
    <div class="week-label">Week 2 <div class="week-label-line"></div><span class="week-status ws-info" id="status-w2">—</span></div>
    <div class="week-grid" id="grid-w2"></div>
  </div>

  <div class="global-warns" id="global-warns"></div>

  <div>
    <div class="section-label">Unscheduled</div>
    <div class="bank-row" id="bank"></div>
  </div>
</div>

<div id="modal-container"></div>

<script>
const DAYS=['Mon','Tue','Wed','Thu','Fri','Sat','Sun'];
const WEEKS=['w1','w2'];
const STORAGE_KEY='training-planner-v1';

const DEFAULT_WORKOUTS={
  'lower-a-1': {label:'Lower A \u2013 Squat',    cls:'wc-strength',  heavy:true,  type:'strength'},
  'upper-a-1': {label:'Upper A \u2013 Bench',    cls:'wc-strength',  heavy:false, type:'strength'},
  'lower-b-1': {label:'Lower B \u2013 Deadlift', cls:'wc-strength',  heavy:true,  type:'strength'},
  'upper-b-1': {label:'Upper B \u2013 Bench+',   cls:'wc-strength',  heavy:false, type:'strength'},
  'wrestling-1':{label:'Wrestling',              cls:'wc-wrestling', heavy:true,  type:'wrestling'},
  'z2-w1-1':  {label:'Z2 cardio',                cls:'wc-cardio-z2', heavy:false, type:'z2'},
  'z2-w1-2':  {label:'Z2 cardio',                cls:'wc-cardio-z2', heavy:false, type:'z2'},
  'hi-w1-1':  {label:'Threshold / VO2',          cls:'wc-cardio-hi', heavy:true,  type:'hi'},
  'lower-a-2': {label:'Lower A \u2013 Squat',    cls:'wc-strength',  heavy:true,  type:'strength'},
  'upper-a-2': {label:'Upper A \u2013 Bench',    cls:'wc-strength',  heavy:false, type:'strength'},
  'lower-b-2': {label:'Lower B \u2013 Deadlift', cls:'wc-strength',  heavy:true,  type:'strength'},
  'upper-b-2': {label:'Upper B \u2013 Bench+',   cls:'wc-strength',  heavy:false, type:'strength'},
  'wrestling-2':{label:'Wrestling',              cls:'wc-wrestling', heavy:true,  type:'wrestling'},
  'z2-w2-1':  {label:'Z2 cardio',                cls:'wc-cardio-z2', heavy:false, type:'z2'},
  'z2-w2-2':  {label:'Z2 cardio',                cls:'wc-cardio-z2', heavy:false, type:'z2'},
  'hi-w2-1':  {label:'Threshold / VO2',          cls:'wc-cardio-hi', heavy:true,  type:'hi'},
};

let workouts={};
let schedule={};
let dragId=null,dragFrom=null,uidCounter=200;

function genId(){return 'custom-'+(++uidCounter)}

function defaultSchedule(){
  const s={};
  WEEKS.forEach(w=>DAYS.forEach(d=>s[`${w}-${d}`]=[]));
  return s;
}

function saveState(){
  const state={workouts,schedule,uidCounter};
  try{
    localStorage.setItem(STORAGE_KEY,JSON.stringify(state));
    const ind=document.getElementById('save-indicator');
    ind.classList.add('show');
    setTimeout(()=>ind.classList.remove('show'),2200);
  }catch(e){alert('Could not save to localStorage: '+e.message)}
}

function loadState(){
  try{
    const raw=localStorage.getItem(STORAGE_KEY);
    if(!raw) return false;
    const state=JSON.parse(raw);
    workouts=state.workouts||{...DEFAULT_WORKOUTS};
    schedule=state.schedule||defaultSchedule();
    uidCounter=state.uidCounter||200;
    WEEKS.forEach(w=>DAYS.forEach(d=>{const k=`${w}-${d}`;if(!schedule[k])schedule[k]=[];}));
    return true;
  }catch(e){return false}
}

function init(){
  if(!loadState()){
    workouts={...DEFAULT_WORKOUTS};
    schedule=defaultSchedule();
  }
  render();
}

function advanceWeek(){
  // w2 → w1, w1 falls to bank, w2 cleared
  const newSchedule=defaultSchedule();
  DAYS.forEach(d=>{
    newSchedule[`w1-${d}`]=[...(schedule[`w2-${d}`]||[])];
    // w1 workouts naturally surface in bank since they're not in any slot
  });
  schedule=newSchedule;
  render();
}

function confirmAdvanceWeek(){
  const w1HasWorkouts=DAYS.some(d=>(schedule[`w1-${d}`]||[]).length>0);
  if(w1HasWorkouts){
    showConfirmModal(
      'Advance week?',
      'Week 1 workouts will return to the unscheduled bank. Week 2 slides into Week 1. Week 2 will be cleared for you to plan the next cycle.',
      advanceWeek
    );
  } else {
    advanceWeek();
  }
}

function confirmReset(){
  showConfirmModal(
    'Reset planner?',
    'All scheduled workouts will be cleared and the default card set restored. This does not affect your saved data until you press Save.',
    ()=>{workouts={...DEFAULT_WORKOUTS};schedule=defaultSchedule();render();}
  );
}

function getBank(){
  const used=new Set([].concat(...Object.values(schedule)));
  return Object.keys(workouts).filter(id=>!used.has(id));
}

function allSlotKeys(){
  const k=[];WEEKS.forEach(w=>DAYS.forEach(d=>k.push(`${w}-${d}`)));return k;
}

function makeCard(id,fromSlot){
  const wt=workouts[id];if(!wt)return null;
  const card=document.createElement('div');
  card.className=`workout-card ${wt.cls}`;
  card.draggable=true;card.dataset.id=id;
  card.innerHTML=`<span class="card-label">${wt.label}</span><span class="card-actions"><button class="card-btn" title="Edit" onclick="event.stopPropagation();openEditModal('${id}','${fromSlot||'bank'}')">&#9998;</button><button class="card-btn" title="Unschedule" onclick="event.stopPropagation();removeCard('${id}','${fromSlot||'bank'}')">&#x2715;</button></span>`;
  card.addEventListener('dragstart',()=>{dragId=id;dragFrom=fromSlot||'bank';setTimeout(()=>card.classList.add('dragging'),0)});
  card.addEventListener('dragend',()=>card.classList.remove('dragging'));
  return card;
}

function removeCard(id,fromSlot){
  if(fromSlot&&fromSlot!=='bank') schedule[fromSlot]=schedule[fromSlot].filter(x=>x!==id);
  render();
}

function renderGrid(week,containerId){
  const grid=document.getElementById(containerId);grid.innerHTML='';
  DAYS.forEach(day=>{
    const slotKey=`${week}-${day}`;
    const col=document.createElement('div');
    col.className='day-col';col.dataset.slot=slotKey;
    col.innerHTML=`<div class="day-header">${day}<span></span></div><div class="drop-zone" id="dz-${slotKey}"></div>`;
    grid.appendChild(col);
    const dz=col.querySelector('.drop-zone');
    dz.addEventListener('dragover',e=>{e.preventDefault();col.classList.add('highlight')});
    dz.addEventListener('dragleave',()=>col.classList.remove('highlight'));
    dz.addEventListener('drop',e=>{
      e.preventDefault();col.classList.remove('highlight');
      if(!dragId)return;
      if(dragFrom&&dragFrom!=='bank') schedule[dragFrom]=schedule[dragFrom].filter(x=>x!==dragId);
      if(!schedule[slotKey].includes(dragId)) schedule[slotKey].push(dragId);
      dragId=null;dragFrom=null;render();
    });
    (schedule[slotKey]||[]).forEach(id=>{const c=makeCard(id,slotKey);if(c)dz.appendChild(c)});
  });
}

function renderBank(){
  const bank=document.getElementById('bank');bank.innerHTML='';
  bank.addEventListener('dragover',e=>e.preventDefault());
  bank.addEventListener('drop',e=>{
    e.preventDefault();if(!dragId)return;
    if(dragFrom&&dragFrom!=='bank') schedule[dragFrom]=schedule[dragFrom].filter(x=>x!==dragId);
    dragId=null;dragFrom=null;render();
  });
  const bk=getBank();
  if(!bk.length){
    const msg=document.createElement('span');
    msg.style.cssText='font-size:11px;color:#888780;padding:2px 0';
    msg.textContent='All workouts scheduled';bank.appendChild(msg);return;
  }
  bk.forEach(id=>{const c=makeCard(id,'bank');if(c)bank.appendChild(c)});
}

function getOrderedSlots(){
  const s=[];WEEKS.forEach(w=>DAYS.forEach(d=>s.push(`${w}-${d}`)));return s;
}

function slotLabel(slot){
  const p=slot.split('-');
  return `${p[0]==='w1'?'Wk1':'Wk2'} ${p[1]}`;
}

function analyzeWeek(week){
  const warns=[];
  const slots=getOrderedSlots();
  const weekSlots=DAYS.map(d=>`${week}-${d}`);
  weekSlots.forEach(slot=>{
    const curr=schedule[slot]||[];if(!curr.length)return;
    const hasHeavyStr=curr.some(id=>{const wt=workouts[id];return wt&&wt.type==='strength'&&wt.heavy});
    const gi=slots.indexOf(slot);
    if(hasHeavyStr&&gi>0){
      const prev=slots[gi-1];
      if((schedule[prev]||[]).some(id=>workouts[id]&&workouts[id].heavy))
        warns.push(`${slotLabel(slot)}: heavy strength after hard session on ${slotLabel(prev)}`);
    }
    const strCount=curr.filter(id=>workouts[id]&&workouts[id].type==='strength').length;
    if(strCount>1) warns.push(`${slotLabel(slot)}: ${strCount} strength sessions on same day`);
    if(curr.filter(id=>workouts[id]&&workouts[id].heavy).length>1)
      warns.push(`${slotLabel(slot)}: multiple hard workouts stacked`);
  });
  const allIds=[].concat(...weekSlots.map(s=>schedule[s]||[]));
  const str=allIds.filter(id=>workouts[id]&&workouts[id].type==='strength').length;
  const z2=allIds.filter(id=>workouts[id]&&workouts[id].type==='z2').length;
  const hi=allIds.filter(id=>workouts[id]&&workouts[id].type==='hi').length;
  const wr=allIds.filter(id=>workouts[id]&&workouts[id].type==='wrestling').length;
  return{warns,complete:str===4&&z2>=2&&hi>=1&&wr===1};
}

function renderWeekStatus(week){
  const el=document.getElementById(`status-${week}`);
  const{warns,complete}=analyzeWeek(week);
  const allIds=[].concat(...DAYS.map(d=>schedule[`${week}-${d}`]||[]));
  if(!allIds.length){el.textContent='—';el.className='week-status ws-info';return}
  if(warns.length){el.textContent=`${warns.length} conflict${warns.length>1?'s':''}`;el.className='week-status ws-warn';}
  else if(complete){el.textContent='Well planned';el.className='week-status ws-ok';}
  else{el.textContent='In progress';el.className='week-status ws-info';}
}

function renderGlobalWarns(){
  const box=document.getElementById('global-warns');box.innerHTML='';
  WEEKS.forEach(w=>{
    analyzeWeek(w).warns.forEach(msg=>{
      const el=document.createElement('div');el.className='warn';el.textContent=msg;box.appendChild(el);
    });
  });
  const rem=getBank().length;
  if(rem){const el=document.createElement('div');el.className='info-msg';el.textContent=`${rem} workout${rem>1?'s':''} not yet scheduled`;box.appendChild(el)}
}

function highlightConflicts(){
  document.querySelectorAll('.day-col').forEach(c=>c.classList.remove('conflict'));
  const slots=getOrderedSlots();
  slots.forEach((slot,i)=>{
    const col=document.querySelector(`[data-slot="${slot}"]`);if(!col)return;
    const curr=schedule[slot]||[];
    const hasHeavyStr=curr.some(id=>{const wt=workouts[id];return wt&&wt.type==='strength'&&wt.heavy});
    if(hasHeavyStr&&i>0&&(schedule[slots[i-1]]||[]).some(id=>workouts[id]&&workouts[id].heavy))
      col.classList.add('conflict');
    if(curr.filter(id=>workouts[id]&&workouts[id].heavy).length>1)
      col.classList.add('conflict');
  });
}

function render(){
  renderGrid('w1','grid-w1');renderGrid('w2','grid-w2');
  renderBank();
  WEEKS.forEach(w=>renderWeekStatus(w));
  renderGlobalWarns();
  highlightConflicts();
}

/* ── Modals ── */
function openAddModal(){showWorkoutModal({label:'',type:'strength',heavy:true},false)}
function openEditModal(id,slot){const wt=workouts[id];if(wt)showWorkoutModal({label:wt.label,type:wt.type,heavy:wt.heavy},true,id,slot)}
function typeToClass(t){return{strength:'wc-strength',z2:'wc-cardio-z2',hi:'wc-cardio-hi',wrestling:'wc-wrestling',custom:'wc-custom'}[t]||'wc-custom'}
function typeToHeavy(t){return['strength','wrestling','hi'].includes(t)}

function showWorkoutModal(data,isEdit,id,slot){
  const mc=document.getElementById('modal-container');
  mc.innerHTML=`<div class="modal-bg" id="modal-bg"><div class="modal" onclick="event.stopPropagation()">
    <h3>${isEdit?'Edit workout':'New workout'}</h3>
    <label>Name</label>
    <input id="m-label" value="${(data.label||'').replace(/"/g,'&quot;')}" placeholder="e.g. Lower A">
    <label>Type</label>
    <select id="m-type">
      <option value="strength" ${data.type==='strength'?'selected':''}>Strength</option>
      <option value="z2" ${data.type==='z2'?'selected':''}>Z2 cardio</option>
      <option value="hi" ${data.type==='hi'?'selected':''}>Threshold / VO2</option>
      <option value="wrestling" ${data.type==='wrestling'?'selected':''}>Wrestling</option>
      <option value="custom" ${data.type==='custom'?'selected':''}>Custom</option>
    </select>
    <label style="display:flex;align-items:center;gap:6px;margin-bottom:10px">
      <input type="checkbox" id="m-heavy" ${data.heavy?'checked':''} style="width:auto;margin:0"> Counts as hard session
    </label>
    <div class="modal-actions">
      ${isEdit?`<button class="btn-sm modal-del" onclick="deleteWorkout('${id}')">Delete</button>`:''}
      <button class="btn-sm" onclick="closeModal()">Cancel</button>
      <button class="btn-sm btn-primary" id="modal-save-btn">${isEdit?'Save':'Add'}</button>
    </div>
  </div></div>`;
  document.getElementById('modal-bg').addEventListener('click',closeModal);
  document.getElementById('m-type').addEventListener('change',function(){document.getElementById('m-heavy').checked=typeToHeavy(this.value)});
  document.getElementById('modal-save-btn').addEventListener('click',()=>saveModal(id||'',isEdit));
}

function showConfirmModal(title,message,onConfirm){
  const mc=document.getElementById('modal-container');
  mc.innerHTML=`<div class="modal-bg" id="modal-bg"><div class="modal" onclick="event.stopPropagation()">
    <h3>${title}</h3><p>${message}</p>
    <div class="modal-actions">
      <button class="btn-sm" onclick="closeModal()">Cancel</button>
      <button class="btn-sm btn-primary" id="confirm-btn">Confirm</button>
    </div>
  </div></div>`;
  document.getElementById('modal-bg').addEventListener('click',closeModal);
  document.getElementById('confirm-btn').addEventListener('click',()=>{closeModal();onConfirm()});
}

function closeModal(){document.getElementById('modal-container').innerHTML=''}

function saveModal(id,isEdit){
  const label=document.getElementById('m-label').value.trim();if(!label)return;
  const type=document.getElementById('m-type').value;
  const heavy=document.getElementById('m-heavy').checked;
  const cls=typeToClass(type);
  if(isEdit&&id&&workouts[id]){workouts[id]={...workouts[id],label,type,heavy,cls}}
  else{workouts[genId()]={label,type,heavy,cls}}
  closeModal();render();
}

function deleteWorkout(id){
  allSlotKeys().forEach(s=>{schedule[s]=(schedule[s]||[]).filter(x=>x!==id)});
  delete workouts[id];closeModal();render();
}

init();
</script>
</body>
</html>
