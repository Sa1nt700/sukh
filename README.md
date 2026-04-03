<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Trade Journal — Halal Swing Trading</title>
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>◆</text></svg>">
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0a0c12;--card:#0f1117;--card2:#161922;--border:#1e2130;
  --text:#e2e4ed;--dim:#5a5f7a;--dim2:#3a3d52;
  --green:#4ade80;--red:#f87171;--cyan:#22d3ee;--purple:#c084fc;--yellow:#fbbf24;
  --green-bg:#1a2f1a;--red-bg:#2f1a1a;--cyan-bg:#1a2535;--purple-bg:#1a1a2f;
  --green-bdr:#2d5a2d;--red-bdr:#5a2d2d;--cyan-bdr:#2d4a5a;--purple-bdr:#2d2d5a;
}
html{background:var(--bg);color:var(--text);font-family:'DM Sans',system-ui,sans-serif;font-size:14px;line-height:1.5}
body{min-height:100vh}
input,select,textarea,button{font-family:inherit;font-size:inherit}
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--border);border-radius:3px}

/* ── Layout ── */
.app{max-width:1280px;margin:0 auto;padding:0 24px 40px}
.header{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:16px;padding:24px 0 20px;border-bottom:1px solid var(--border)}
.logo{font-family:'Space Mono',monospace;font-size:20px;font-weight:700;background:linear-gradient(135deg,var(--green),var(--cyan));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.subtitle{font-size:11px;color:var(--dim2);margin-top:2px;letter-spacing:.5px}
.header-actions{display:flex;gap:10px;align-items:center}

/* ── Tabs ── */
.tabs{display:flex;gap:4px;margin-top:20px;border-bottom:1px solid var(--border);padding-bottom:0}
.tab{padding:10px 20px;font-size:12px;font-weight:600;letter-spacing:.5px;text-transform:uppercase;cursor:pointer;border:none;background:none;color:var(--dim);border-bottom:2px solid transparent;transition:.2s}
.tab:hover{color:var(--text)}
.tab.active{color:var(--cyan);border-bottom-color:var(--cyan)}

/* ── Buttons ── */
.btn{padding:9px 20px;border-radius:8px;font-size:13px;font-weight:600;cursor:pointer;border:1px solid var(--border);background:transparent;color:var(--dim);transition:.15s}
.btn:hover{border-color:var(--dim);color:var(--text)}
.btn-primary{background:linear-gradient(135deg,var(--green),var(--cyan));color:#0a0c12;border:none;font-weight:700;box-shadow:0 4px 20px rgba(74,222,128,.12)}
.btn-primary:hover{opacity:.9}
.btn-sm{padding:4px 12px;font-size:11px;border-radius:6px}
.btn-green{background:var(--green-bg);color:var(--green);border-color:var(--green-bdr)}
.btn-red{background:var(--red-bg);color:var(--red);border-color:var(--red-bdr)}
.btn-purple{background:var(--purple-bg);color:var(--purple);border-color:var(--purple-bdr)}

/* ── Stats Grid ── */
.stats{display:flex;gap:14px;flex-wrap:wrap;margin-top:20px}
.stat-card{background:linear-gradient(135deg,var(--card),var(--card2));border:1px solid var(--border);border-radius:14px;padding:20px 22px;flex:1 1 170px;min-width:160px}
.stat-label{font-size:10px;text-transform:uppercase;letter-spacing:1.5px;color:var(--dim);margin-bottom:8px}
.stat-value{font-size:24px;font-weight:700;font-family:'Space Mono',monospace;line-height:1.1}
.stat-sub{font-size:11px;color:var(--dim);margin-top:6px}

/* ── Table ── */
.table-wrap{background:linear-gradient(135deg,var(--card),var(--card2));border:1px solid var(--border);border-radius:14px;overflow:hidden;margin-top:16px}
.table-scroll{overflow-x:auto}
table{width:100%;border-collapse:collapse;min-width:960px}
th{padding:14px 12px;text-align:left;font-size:10px;text-transform:uppercase;letter-spacing:1.2px;color:var(--dim2);font-weight:600;border-bottom:1px solid var(--border);white-space:nowrap}
td{padding:12px 12px;border-bottom:1px solid rgba(30,33,48,.5);font-size:13px;white-space:nowrap}
.ticker{font-family:'Space Mono',monospace;font-weight:700;color:var(--text);font-size:14px}
.mono{font-family:'Space Mono',monospace;color:#c0c3d4;font-size:13px}
.pnl-pos{color:var(--green);font-weight:600;font-family:'Space Mono',monospace}
.pnl-neg{color:var(--red);font-weight:600;font-family:'Space Mono',monospace}
.badge{display:inline-block;padding:3px 10px;border-radius:6px;font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.6px}
.badge-open{background:rgba(251,191,36,.1);color:var(--yellow);border:1px solid rgba(251,191,36,.2)}
.badge-closed{background:rgba(74,222,128,.1);color:var(--green);border:1px solid rgba(74,222,128,.2)}
.badge-stopped{background:rgba(248,113,113,.1);color:var(--red);border:1px solid rgba(248,113,113,.2)}
.empty-row{text-align:center;color:var(--dim2);padding:48px 12px !important}
.actions{display:flex;gap:5px}

/* ── Filters ── */
.filters{display:flex;gap:10px;margin-top:20px;align-items:center;flex-wrap:wrap}
.filter-btn{padding:7px 16px;border-radius:7px;font-size:11px;font-weight:600;cursor:pointer;text-transform:uppercase;letter-spacing:.6px;border:1px solid var(--border);background:transparent;color:var(--dim);transition:.15s}
.filter-btn.active{background:var(--cyan-bg);color:var(--cyan);border-color:var(--cyan-bdr)}
.search-input{margin-left:auto;padding:8px 14px;background:var(--card);border:1px solid var(--border);border-radius:8px;color:var(--text);font-size:13px;outline:none;width:170px}
.search-input:focus{border-color:var(--cyan)}
.search-input::placeholder{color:var(--dim2)}

/* ── Chart ── */
.chart-card{background:linear-gradient(135deg,var(--card),var(--card2));border:1px solid var(--border);border-radius:14px;padding:20px 22px;margin-top:16px}
.chart-label{font-size:10px;text-transform:uppercase;letter-spacing:1.5px;color:var(--dim);margin-bottom:12px}

/* ── Modal ── */
.overlay{position:fixed;inset:0;background:rgba(0,0,0,.7);z-index:1000;display:flex;align-items:center;justify-content:center;backdrop-filter:blur(4px)}
.modal{background:var(--card2);border:1px solid var(--border);border-radius:18px;padding:32px;width:95%;max-width:560px;max-height:90vh;overflow:auto}
.modal h3{font-family:'Space Mono',monospace;font-size:18px;margin-bottom:24px}
.form-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px}
.form-group label{display:block;font-size:10px;text-transform:uppercase;letter-spacing:1.2px;color:var(--dim);margin-bottom:5px}
.form-input{width:100%;padding:10px 12px;background:var(--bg);border:1px solid var(--border);border-radius:8px;color:var(--text);font-size:13px;outline:none}
.form-input:focus{border-color:var(--cyan)}
.form-input::placeholder{color:var(--dim2)}
.form-full{grid-column:1/-1}
textarea.form-input{min-height:70px;resize:vertical}
.form-actions{display:flex;gap:12px;justify-content:flex-end;margin-top:24px}

/* ── Analytics ── */
.analytics-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-top:20px}
.analytics-card{background:linear-gradient(135deg,var(--card),var(--card2));border:1px solid var(--border);border-radius:14px;padding:20px 22px}
.analytics-card h4{font-size:11px;text-transform:uppercase;letter-spacing:1.2px;color:var(--dim);margin-bottom:14px}
.bar-row{display:flex;align-items:center;gap:10px;margin-bottom:8px}
.bar-label{width:100px;font-size:12px;color:#c0c3d4;text-overflow:ellipsis;overflow:hidden;white-space:nowrap}
.bar-track{flex:1;height:18px;background:var(--bg);border-radius:4px;overflow:hidden;position:relative}
.bar-fill{height:100%;border-radius:4px;transition:width .4s}
.bar-val{font-size:11px;font-family:'Space Mono',monospace;width:70px;text-align:right}

/* ── Footer ── */
.footer{text-align:center;padding:28px 0 8px;font-size:11px;color:var(--dim2);letter-spacing:.5px}

@media(max-width:640px){
  .form-grid{grid-template-columns:1fr}
  .analytics-grid{grid-template-columns:1fr}
  .stats{flex-direction:column}
  .header{flex-direction:column;align-items:flex-start}
}
</style>
</head>
<body>

<div class="app" id="app"></div>

<script>
// ─── Data Layer ───
const STORAGE_KEY = 'halal-trade-journal-v1';
const SECTORS = ['Technology','Healthcare','Energy','Financials','Consumer Discretionary','Consumer Staples','Industrials','Materials','Real Estate','Utilities','Communication'];
const SETUPS = ['Breakout','Pullback to Support','Moving Avg Bounce','Gap & Go','Range Break','Trend Continuation','Reversal','VWAP Reclaim','Other'];

function loadTrades(){ try{return JSON.parse(localStorage.getItem(STORAGE_KEY))||[]}catch(e){return[]} }
function saveTrades(t){ localStorage.setItem(STORAGE_KEY, JSON.stringify(t)) }
function genId(){ return Date.now().toString(36)+Math.random().toString(36).slice(2,7) }
function fmt$(n){ return n==null||isNaN(n)?'—':n.toLocaleString('en-US',{style:'currency',currency:'USD'}) }
function fmtDate(d){ return d?new Date(d).toLocaleDateString('en-US',{month:'short',day:'numeric',year:'2-digit'}):'—' }
function fmtPct(n){ return n==null||isNaN(n)?'—':(n>=0?'+':'')+n.toFixed(2)+'%' }

// ─── State ───
let state = {
  trades: loadTrades(),
  tab: 'dashboard',
  filter: 'all',
  search: '',
  modal: null, // null | 'new' | trade object for edit
  confirmDelete: null,
};

function setState(patch){
  Object.assign(state, patch);
  render();
}

// ─── Computed ───
function getStats(){
  const {trades}=state;
  const closed=trades.filter(t=>t.status!=='open'&&t.exitPrice!=null);
  const wins=closed.filter(t=>t.exitPrice>t.entryPrice);
  const losses=closed.filter(t=>t.exitPrice<=t.entryPrice);
  const totalPnl=closed.reduce((s,t)=>s+(t.exitPrice-t.entryPrice)*t.shares,0);
  const avgWin=wins.length?wins.reduce((s,t)=>s+(t.exitPrice-t.entryPrice)*t.shares,0)/wins.length:0;
  const avgLoss=losses.length?Math.abs(losses.reduce((s,t)=>s+(t.exitPrice-t.entryPrice)*t.shares,0)/losses.length):0;
  const bestTrade=closed.length?Math.max(...closed.map(t=>(t.exitPrice-t.entryPrice)*t.shares)):0;
  const worstTrade=closed.length?Math.min(...closed.map(t=>(t.exitPrice-t.entryPrice)*t.shares)):0;
  return {
    total:trades.length, closedCount:closed.length, openCount:trades.filter(t=>t.status==='open').length,
    winRate:closed.length?(wins.length/closed.length*100):0, totalPnl, avgWin, avgLoss,
    profitFactor:avgLoss?(avgWin/avgLoss):0, wins:wins.length, losses:losses.length, bestTrade, worstTrade,
  };
}

function getFiltered(){
  let t=state.trades;
  if(state.filter!=='all') t=t.filter(tr=>tr.status===state.filter);
  if(state.search) t=t.filter(tr=>tr.ticker.includes(state.search.toUpperCase()));
  return t.sort((a,b)=>new Date(b.entryDate)-new Date(a.entryDate));
}

function getSectorData(){
  const closed=state.trades.filter(t=>t.status!=='open'&&t.exitPrice!=null);
  const map={};
  closed.forEach(t=>{
    const s=t.sector||'Unknown';
    if(!map[s])map[s]={trades:0,pnl:0,wins:0};
    map[s].trades++;
    const pnl=(t.exitPrice-t.entryPrice)*t.shares;
    map[s].pnl+=pnl;
    if(pnl>0)map[s].wins++;
  });
  return Object.entries(map).sort((a,b)=>b[1].pnl-a[1].pnl);
}

function getSetupData(){
  const closed=state.trades.filter(t=>t.status!=='open'&&t.exitPrice!=null);
  const map={};
  closed.forEach(t=>{
    const s=t.setup||'Unknown';
    if(!map[s])map[s]={trades:0,pnl:0,wins:0};
    map[s].trades++;
    const pnl=(t.exitPrice-t.entryPrice)*t.shares;
    map[s].pnl+=pnl;
    if(pnl>0)map[s].wins++;
  });
  return Object.entries(map).sort((a,b)=>b[1].pnl-a[1].pnl);
}

// ─── Actions ───
function saveTrade(form){
  const trade={
    ...form,
    entryPrice:parseFloat(form.entryPrice),
    exitPrice:form.exitPrice?parseFloat(form.exitPrice):null,
    shares:parseInt(form.shares),
    stopLoss:form.stopLoss?parseFloat(form.stopLoss):null,
    target:form.target?parseFloat(form.target):null,
    id:form.id||genId(),
  };
  const trades=[...state.trades];
  const idx=trades.findIndex(t=>t.id===trade.id);
  if(idx>=0)trades[idx]=trade; else trades.unshift(trade);
  saveTrades(trades);
  setState({trades, modal:null});
}

function deleteTrade(id){
  const trades=state.trades.filter(t=>t.id!==id);
  saveTrades(trades);
  setState({trades, confirmDelete:null});
}

function exportCSV(){
  const rows=[['Ticker','Sector','Setup','Entry Date','Exit Date','Entry Price','Exit Price','Shares','Stop Loss','Target','Status','P&L ($)','P&L (%)','Notes']];
  state.trades.forEach(t=>{
    const pnl=t.exitPrice!=null?((t.exitPrice-t.entryPrice)*t.shares):null;
    const pnlPct=t.exitPrice!=null?((t.exitPrice-t.entryPrice)/t.entryPrice*100):null;
    rows.push([t.ticker,t.sector,t.setup,t.entryDate,t.exitDate||'',t.entryPrice,t.exitPrice||'',t.shares,t.stopLoss||'',t.target||'',t.status,pnl!=null?pnl.toFixed(2):'',pnlPct!=null?pnlPct.toFixed(2):'',t.notes||'']);
  });
  const csv=rows.map(r=>r.map(c=>`"${c}"`).join(',')).join('\n');
  const blob=new Blob([csv],{type:'text/csv'});
  const a=document.createElement('a');
  a.href=URL.createObjectURL(blob);
  a.download='trade_journal_export.csv';
  a.click();
}

// ─── Rendering ───
function h(tag,attrs,...children){
  const el=document.createElement(tag);
  if(attrs) Object.entries(attrs).forEach(([k,v])=>{
    if(k==='style'&&typeof v==='object') Object.assign(el.style,v);
    else if(k.startsWith('on')) el.addEventListener(k.slice(2).toLowerCase(),v);
    else if(k==='className') el.className=v;
    else if(k==='innerHTML') el.innerHTML=v;
    else el.setAttribute(k,v);
  });
  children.flat(9).forEach(c=>{
    if(c==null||c===false)return;
    el.appendChild(typeof c==='string'||typeof c==='number'?document.createTextNode(c):c);
  });
  return el;
}

function renderEquityCurve(){
  const closed=state.trades.filter(t=>t.status!=='open'&&t.exitPrice!=null)
    .sort((a,b)=>new Date(a.exitDate||a.entryDate)-new Date(b.exitDate||b.entryDate));
  if(closed.length<2)return null;
  let cum=[0];
  closed.forEach(t=>{cum.push(cum[cum.length-1]+(t.exitPrice-t.entryPrice)*t.shares)});
  const max=Math.max(...cum),min=Math.min(...cum),range=max-min||1;
  const W=700,H=180,P=24;
  const pts=cum.map((v,i)=>{
    const x=P+(i/(cum.length-1))*(W-P*2);
    const y=P+(1-(v-min)/range)*(H-P*2);
    return [x,y];
  });
  const last=cum[cum.length-1];
  const col=last>=0?'var(--green)':'var(--red)';
  const line=pts.map(p=>p.join(',')).join(' ');
  const area=`${P},${H-P} ${line} ${pts[pts.length-1][0]},${H-P}`;
  const zeroY=min<0&&max>0?P+(1-(0-min)/range)*(H-P*2):null;
  return h('div',{className:'chart-card'},
    h('div',{className:'chart-label'},'Equity Curve'),
    h('div',{innerHTML:`<svg viewBox="0 0 ${W} ${H}" style="width:100%;height:auto">
      <defs><linearGradient id="ef" x1="0" y1="0" x2="0" y2="1">
        <stop offset="0%" stop-color="${col}" stop-opacity="0.2"/>
        <stop offset="100%" stop-color="${col}" stop-opacity="0"/>
      </linearGradient></defs>
      ${zeroY!=null?`<line x1="${P}" y1="${zeroY}" x2="${W-P}" y2="${zeroY}" stroke="var(--border)" stroke-dasharray="4,4"/>`:''}
      <polygon points="${area}" fill="url(#ef)"/>
      <polyline points="${line}" fill="none" stroke="${col}" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
      ${pts.map(([x,y])=>`<circle cx="${x}" cy="${y}" r="3" fill="${col}"/>`).join('')}
    </svg>`})
  );
}

function renderBarChart(data, maxAbs){
  if(!maxAbs) maxAbs=Math.max(...data.map(d=>Math.abs(d[1].pnl)),1);
  return data.map(([name,d])=>{
    const pct=Math.abs(d.pnl)/maxAbs*100;
    const col=d.pnl>=0?'var(--green)':'var(--red)';
    return h('div',{className:'bar-row'},
      h('span',{className:'bar-label'},name),
      h('div',{className:'bar-track'},
        h('div',{className:'bar-fill',style:{width:pct+'%',background:col}}),
      ),
      h('span',{className:'bar-val',style:{color:col}},fmt$(d.pnl)),
    );
  });
}

function renderModal(){
  const isEdit=state.modal&&typeof state.modal==='object';
  const init=isEdit?state.modal:{
    ticker:'',entryPrice:'',exitPrice:'',shares:'',entryDate:new Date().toISOString().slice(0,10),
    exitDate:'',stopLoss:'',target:'',sector:'',setup:'',notes:'',status:'open'
  };
  const form={...init};

  function field(label, key, type='text', opts=null){
    const grp=h('div',{className:'form-group'});
    grp.appendChild(h('label',null,label));
    if(opts){
      const sel=h('select',{className:'form-input',onChange:e=>{form[key]=e.target.value}});
      sel.appendChild(h('option',{value:''},'Select'));
      opts.forEach(o=>{ const op=h('option',{value:o},o); if(form[key]===o)op.selected=true; sel.appendChild(op) });
      grp.appendChild(sel);
    } else {
      const inp=h('input',{className:'form-input',type,value:form[key]||'',placeholder:type==='number'?'0.00':type==='date'?'':'',onChange:e=>{
        form[key]=type==='text'&&key==='ticker'?e.target.value.toUpperCase():e.target.value;
      }});
      if(type==='number')inp.step='0.01';
      grp.appendChild(inp);
    }
    return grp;
  }

  return h('div',{className:'overlay',onClick:()=>setState({modal:null})},
    h('div',{className:'modal',onClick:e=>e.stopPropagation()},
      h('h3',null,isEdit?'Edit Trade':'Log New Trade'),
      h('div',{className:'form-grid'},
        field('Ticker *','ticker'),
        field('Sector','sector','text',SECTORS),
        field('Entry Price *','entryPrice','number'),
        field('Exit Price','exitPrice','number'),
        field('Shares *','shares','number'),
        field('Setup','setup','text',SETUPS),
        field('Entry Date *','entryDate','date'),
        field('Exit Date','exitDate','date'),
        field('Stop Loss','stopLoss','number'),
        field('Target','target','number'),
        field('Status','status','text',['open','closed','stopped']),
      ),
      h('div',{className:'form-group form-full',style:{marginTop:'16px'}},
        h('label',{style:{display:'block',fontSize:'10px',textTransform:'uppercase',letterSpacing:'1.2px',color:'var(--dim)',marginBottom:'5px'}},'Notes'),
        h('textarea',{className:'form-input',placeholder:'Trade thesis, lessons learned...',onChange:e=>{form.notes=e.target.value}},form.notes||''),
      ),
      h('div',{className:'form-actions'},
        h('button',{className:'btn',onClick:()=>setState({modal:null})},'Cancel'),
        h('button',{className:'btn btn-primary',onClick:()=>{
          if(!form.ticker||!form.entryPrice||!form.shares||!form.entryDate)return;
          saveTrade(form);
        }},isEdit?'Update':'Log Trade'),
      ),
    )
  );
}

function renderDashboard(){
  const stats=getStats();
  const frag=document.createDocumentFragment();

  // Stats cards
  const cards=[
    {label:'Total P&L',value:fmt$(stats.totalPnl),accent:stats.totalPnl>=0?'var(--green)':'var(--red)',sub:`${stats.closedCount} closed trades`},
    {label:'Win Rate',value:stats.closedCount?stats.winRate.toFixed(1)+'%':'—',accent:'var(--cyan)',sub:`${stats.wins}W / ${stats.losses}L`},
    {label:'Profit Factor',value:stats.profitFactor?stats.profitFactor.toFixed(2):'—',accent:'var(--purple)',sub:`Avg win ${fmt$(stats.avgWin)}`},
    {label:'Open Positions',value:stats.openCount,accent:'var(--yellow)',sub:`of ${stats.total} total`},
    {label:'Best Trade',value:fmt$(stats.bestTrade),accent:'var(--green)',sub:'single trade'},
    {label:'Worst Trade',value:fmt$(stats.worstTrade),accent:'var(--red)',sub:'single trade'},
  ];

  const grid=h('div',{className:'stats'});
  cards.forEach(c=>{
    grid.appendChild(h('div',{className:'stat-card'},
      h('div',{className:'stat-label'},c.label),
      h('div',{className:'stat-value',style:{color:c.accent}},String(c.value)),
      c.sub?h('div',{className:'stat-sub'},c.sub):null,
    ));
  });
  frag.appendChild(grid);

  // Equity curve
  const curve=renderEquityCurve();
  if(curve)frag.appendChild(curve);

  // Analytics
  const sectorData=getSectorData();
  const setupData=getSetupData();
  if(sectorData.length||setupData.length){
    const ag=h('div',{className:'analytics-grid'});
    if(sectorData.length){
      const card=h('div',{className:'analytics-card'},h('h4',null,'P&L by Sector'));
      renderBarChart(sectorData).forEach(r=>card.appendChild(r));
      ag.appendChild(card);
    }
    if(setupData.length){
      const card=h('div',{className:'analytics-card'},h('h4',null,'P&L by Setup'));
      renderBarChart(setupData).forEach(r=>card.appendChild(r));
      ag.appendChild(card);
    }
    frag.appendChild(ag);
  }

  return frag;
}

function renderTradeLog(){
  const frag=document.createDocumentFragment();

  // Filters
  const filters=h('div',{className:'filters'});
  ['all','open','closed','stopped'].forEach(f=>{
    filters.appendChild(h('button',{
      className:'filter-btn'+(state.filter===f?' active':''),
      onClick:()=>setState({filter:f})
    },f));
  });
  const search=h('input',{className:'search-input',placeholder:'Search ticker...',value:state.search,onInput:e=>setState({search:e.target.value})});
  filters.appendChild(search);
  frag.appendChild(filters);

  // Table
  const displayed=getFiltered();
  const wrap=h('div',{className:'table-wrap'},
    h('div',{className:'table-scroll'},
      h('table',null,
        h('thead',null,h('tr',null,
          ...['Ticker','Status','Entry Date','Entry','Exit','Shares','R:R','P&L','Setup',''].map(t=>h('th',null,t))
        )),
        h('tbody',null,
          ...(displayed.length===0?
            [h('tr',null,h('td',{colspan:'10',className:'empty-row',innerHTML:'No trades yet — hit <strong style="color:var(--green)">+ New Trade</strong> to start logging'}))]:
            displayed.map(t=>{
              const pnl=t.status==='open'||!t.exitPrice?null:(t.exitPrice-t.entryPrice)*t.shares;
              const pnlPct=t.status==='open'||!t.exitPrice?null:((t.exitPrice-t.entryPrice)/t.entryPrice*100);
              const rr=t.stopLoss&&t.target&&t.entryPrice&&t.entryPrice!==t.stopLoss?((t.target-t.entryPrice)/(t.entryPrice-t.stopLoss)).toFixed(1):null;
              const badgeCls=t.status==='open'?'badge-open':t.status==='closed'?'badge-closed':'badge-stopped';
              return h('tr',null,
                h('td',null,h('span',{className:'ticker'},t.ticker),h('br'),h('span',{style:{fontSize:'11px',color:'var(--dim)'}},t.sector||'')),
                h('td',null,h('span',{className:'badge '+badgeCls},t.status)),
                h('td',{className:'mono'},fmtDate(t.entryDate)),
                h('td',{className:'mono'},fmt$(t.entryPrice)),
                h('td',{className:'mono'},t.exitPrice?fmt$(t.exitPrice):'—'),
                h('td',{className:'mono'},String(t.shares)),
                h('td',{className:'mono'},rr?rr+'R':'—'),
                h('td',{className:pnl==null?'mono':pnl>=0?'pnl-pos':'pnl-neg'},pnl!=null?`${fmt$(pnl)}  ${fmtPct(pnlPct)}`:'—'),
                h('td',{style:{fontSize:'12px',color:'var(--dim)',maxWidth:'130px',overflow:'hidden',textOverflow:'ellipsis'}},t.setup||'—'),
                h('td',null,h('div',{className:'actions'},
                  t.status==='open'?h('button',{className:'btn btn-sm btn-green',onClick:()=>setState({modal:{...t,status:'closed',exitDate:new Date().toISOString().slice(0,10),exitPrice:t.exitPrice||''}})},'Close'):null,
                  h('button',{className:'btn btn-sm btn-purple',onClick:()=>setState({modal:t})},'Edit'),
                  h('button',{className:'btn btn-sm btn-red',onClick:()=>deleteTrade(t.id)},'✕'),
                )),
              );
            }))
        ),
      )
    )
  );
  frag.appendChild(wrap);
  return frag;
}

function render(){
  const app=document.getElementById('app');
  app.innerHTML='';

  // Header
  app.appendChild(h('div',{className:'header'},
    h('div',null,
      h('div',{className:'logo'},'◆ TRADE JOURNAL'),
      h('div',{className:'subtitle'},'Halal Swing Trading · Long Only · NYSE / NASDAQ'),
    ),
    h('div',{className:'header-actions'},
      h('button',{className:'btn',onClick:exportCSV},'Export CSV'),
      h('button',{className:'btn',onClick:()=>{if(confirm('Clear all trades?')){saveTrades([]);setState({trades:[]})}}},'Reset'),
      h('button',{className:'btn btn-primary',onClick:()=>setState({modal:'new'})},'+ New Trade'),
    ),
  ));

  // Tabs
  const tabs=h('div',{className:'tabs'});
  [['dashboard','Dashboard'],['trades','Trade Log']].forEach(([key,label])=>{
    tabs.appendChild(h('button',{className:'tab'+(state.tab===key?' active':''),onClick:()=>setState({tab:key})},label));
  });
  app.appendChild(tabs);

  // Content
  if(state.tab==='dashboard') app.appendChild(renderDashboard());
  else app.appendChild(renderTradeLog());

  // Footer
  app.appendChild(h('div',{className:'footer'},'Data saved locally in your browser · Works offline · Long-only · No leverage · Shariah-compliant'));

  // Modal
  if(state.modal) app.appendChild(renderModal());
}

render();
</script>
</body>
</html>
