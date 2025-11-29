<!--
NIFTY Option Chain Dashboard — Final Fixed
This file is the corrected, self-contained HTML+JS for the dashboard.
Fixes made:
 - Removed any <script> tags embedded inside innerHTML (which caused the "Unexpected identifier 'STOCK'" error).
 - Analytics panel is created and then populated by separate JS (no inline scripts inside innerHTML).
 - Defensive DOM checks everywhere to avoid runtime errors.
 - All UI features retained: ITM shading, deep ITM, gradient strike, vol/reversal grey, hover highlight, OPEN A/C link, Top-50 analytics demo.

HOW TO CONFIGURE:
 - Set API_REST_URL / API_WS_URL / API_AUTH_KEY at the top to use live data.
 - ATM rounding uses Math.round(spot/50)*50. Change if you use different strike intervals.
-->

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>NIFTY Option Chain — Final</title>
  <style>
    :root{
      --orange:#f67d18; --deep-orange:#ff9900; --muted:#f4f4f8; --text:#111;
      --call-itm-1:#e3f7e0; --call-itm-2:#c0efb8; --call-itm-3:#a2e999; --call-itm-4:#8ae587;
      --put-itm-1:#d9eef4; --put-itm-2:#b1dceb; --put-itm-3:#8ecae0; --put-itm-4:#6bb8d7;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,Arial;color:var(--text);background:#fff}
    .sidebar{position:fixed;left:0;top:0;height:100vh;width:60px;background:#292933;display:flex;flex-direction:column;align-items:center;padding:10px 6px;gap:12px;z-index:200}
    .sidebar button{width:44px;height:44px;border-radius:8px;border:none;background:transparent;color:#fff;font-size:18px;cursor:pointer;display:flex;align-items:center;justify-content:center}
    .main{margin-left:60px;padding:10px}
    .top-header{background:var(--orange);padding:10px 14px;border-radius:6px;color:#fff;display:flex;align-items:center;gap:10px}
    .dropdown, .btn{padding:6px 10px;border-radius:6px;border:none;background:#fff;color:var(--orange);font-weight:700;cursor:pointer}
    .timestamp{margin-left:auto;font-weight:600;color:#000;background:rgba(255,255,255,0.85);padding:6px 10px;border-radius:6px}
    .price-info{margin-left:10px;font-weight:700}.price-info .spot{color:yellow}
    .header-buttons{display:flex;gap:8px;align-items:center}
    .risk-bar{display:flex;margin-top:10px;gap:10px}
    .risk-bar > div{flex:1;padding:12px;border-radius:8px;color:#fff;display:flex;flex-direction:column;gap:8px}
    .call-side{background:linear-gradient(90deg,#0bb150,#019b3a)}.middle{background:linear-gradient(90deg,#e65353,#c32b2b);align-items:center;justify-content:center}.right-side{background:linear-gradient(90deg,#d9534f,#b52b2b);align-items:flex-end}
    .label{background:rgba(255,255,255,0.12);padding:6px 8px;border-radius:6px;font-weight:700}.tag-yellow{background:#ffdc64;color:#000;padding:4px 8px;border-radius:6px;font-weight:800}
    .option-chain-container{margin-top:12px;background:#fff;border-radius:8px;padding:12px;box-shadow:0 6px 20px rgba(0,0,0,0.06);overflow:auto}
    table.option-chain{width:100%;border-collapse:collapse;min-width:1200px;font-size:13px}
    table.option-chain th, table.option-chain td{padding:8px 10px;border:1px solid #e6eef6;text-align:center}
    table.option-chain th{background:#ddf0ff;font-weight:700;position:sticky;top:0;z-index:10}
    .strike-col{background:var(--deep-orange);color:#fff;font-weight:700}
    td.heat{transition:background 0.25s ease-in-out}
    .green-text{color:#1b7c00;font-weight:700}.red-text{color:#c83232;font-weight:700}
    .atm{background:#ff9900;color:#fff;padding:6px 10px;border-radius:6px;font-weight:800}
    .flash{animation:flash 0.8s ease-in-out}
    @keyframes flash{0%{opacity:.2}50%{opacity:1}100%{opacity:.6}}
    .legend{display:flex;gap:8px;align-items:center;margin-top:8px}
    .legend .sw{width:22px;height:12px;border-radius:2px}
    .controls{display:flex;gap:8px;align-items:center;margin-top:10px}
    .chip{background:#f1f5f9;padding:6px 8px;border-radius:8px;font-weight:700}
    tfoot td{font-weight:800;background:#fafafa}
    @media (max-width:900px){.top-header{flex-direction:column;align-items:flex-start}.timestamp{margin-left:0}}

    /* ITM styling classes */
    .itm-call-1{background:var(--call-itm-1)!important}
    .itm-call-2{background:var(--call-itm-2)!important}
    .itm-call-3{background:var(--call-itm-3)!important}
    .itm-call-4{background:var(--call-itm-4)!important}
    .itm-put-1{background:var(--put-itm-1)!important}
    .itm-put-2{background:var(--put-itm-2)!important}
    .itm-put-3{background:var(--put-itm-3)!important}
    .itm-put-4{background:var(--put-itm-4)!important}
    .itm-strike{background:linear-gradient(180deg, rgba(0,0,0,0.06), rgba(0,0,0,0.02))!important}
    .deep-itm-call{box-shadow:inset 0 0 0 1px rgba(0,120,0,0.08)}
    .deep-itm-put{box-shadow:inset 0 0 0 1px rgba(0,80,120,0.08)}
    .premium-hover:hover{outline:2px solid #ffd24d;outline-offset:-2px;cursor:pointer}
    .vol-grey{background:#f4f4f4!important}
    .rev-grey{background:#f4f4f4!important}

    /* Analytics panel styles */
    #analyticsPanel{position:fixed;top:0;left:60px;width:calc(100% - 60px);height:100vh;background:#fff;z-index:6000;overflow:auto;padding:20px}
    #topStocksList{margin-top:20px;display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:16px}
    .stock-card{padding:14px;border:1px solid #e5e5e5;border-radius:10px;background:#fdfdfd;box-shadow:0 2px 6px rgba(0,0,0,0.06)}
  </style>
</head>
<body>
  <div class="sidebar" aria-hidden="false">
    <button title="Dashboard">☰</button>
    <button title="Analytics">📊</button>
    <button title="Target">🎯</button>
    <button title="Settings">⚙️</button>
    <button title="Zoom">🔍</button>
    <button title="Repair">🔧</button>
    <button title="Video">🎥</button>
    <button title="Crypto">₿</button>
    <button title="Currencies">₹</button>
  </div>

  <div class="main">
    <div class="top-header">
      <select id="symbolSelect" class="dropdown" aria-label="Index"><option>NIFTY</option><option>BANKNIFTY</option></select>
      <select id="expirySelect" class="dropdown" aria-label="Expiry"><option>11-11-2025</option></select>
      <select id="modeSelect" class="dropdown" aria-label="Spot/Future"><option>SPOT</option><option>FUTURE</option></select>
      <div class="price-info">Spot : <span id="spotVal" class="spot">-</span> / Future : <span id="futureVal">-</span></div>
      <div class="header-buttons">
        <button class="btn" id="openAcBtn">OPEN A/C</button>
        <button class="btn" id="compareBtn">COMPARE</button>
        <button class="btn">IV/TV</button>
        <button class="btn">PCR</button>
        <button class="btn">GREEKS</button>
        <button class="btn" style="background:#f44336;color:#fff">LIVE</button>
        <button class="btn" style="background:#f99521;color:#fff">Chain</button>
      </div>
      <div id="timestamp" class="timestamp">--</div>
    </div>

    <div class="risk-bar">
      <div class="call-side"><div class="title">CALL SIDE</div><div id="resistanceText">RESISTANCE —</div><div class="tag-yellow" id="callTag">WEAK TOWARDS BOTTOM</div></div>
      <div class="middle" id="middleRisk"><div class="label" id="riskLabel">Risky : NA</div><div class="label" id="lotLabel">LOT : 75</div></div>
      <div class="right-side"><div class="title">PUT SIDE</div><div id="supportText">SUPPORT —</div><div class="tag-yellow" id="putTag">WTT TO STRONG</div></div>
    </div>

    <div class="controls">
      <div class="chip">Filters:</div>
      <label>Strike range: <input id="strikeRange" type="range" min="1" max="12" value="12"></label>
      <label>OI Heat threshold: <input id="oiThreshold" type="number" min="0" max="100" value="50">%</label>
      <button id="sortOi" class="btn">Sort by OI</button>
      <button id="refreshBtn" class="btn">Refresh</button>
    </div>

    <div class="legend"><div class="sw" style="background:rgba(164,214,240,0.4)"></div><div>Call OI heat</div><div class="sw" style="background:rgba(244,211,211,0.4)"></div><div>Put OI heat</div></div>

    <div class="option-chain-container" id="tableWrap">
      <table class="option-chain" id="optionChainTable" aria-label="Option Chain Table">
        <thead>
          <tr><th>OI Chg</th><th>OI</th><th>VOLUME</th><th>S-REVERSAL</th><th class="strike-col">ATM &#9660; STRIKE</th><th>S-REVERSAL</th><th>VOLUME</th><th>OI</th><th>OI Chg</th></tr>
        </thead>
        <tbody id="tableBody"></tbody>
        <tfoot id="tableFoot"></tfoot>
      </table>
    </div>

  </div>

  <script>
    // CONFIGURE: REST / WS endpoints (leave blank to use demo)
    const API_REST_URL = "";
    const API_WS_URL = "";
    const API_AUTH_KEY = "";

    const REFRESH_INTERVAL_MS = 7000;
    const LOT_SIZE = 75;

    function sampleData(){
      const spot = 25543.65 + (Math.random()-0.5)*120;
      const rows = [];
      const atm = Math.round(spot/50)*50;
      for(let i=-6;i<=6;i++){
        const strike = atm + i*50;
        const callOi = Math.max(0, Math.floor( Math.random()*120000 - i*4000 ));
        const putOi  = Math.max(0, Math.floor( Math.random()*120000 + i*4000 ));
        const callOiCh = Math.floor((Math.random()-0.4)*80000);
        const putOiCh  = Math.floor((Math.random()-0.6)*80000);
        const callVol = Math.floor(Math.random()*300000);
        const putVol = Math.floor(Math.random()*300000);
        rows.push({strike,call:{oi:callOi,oiChange:callOiCh,volume:callVol},put:{oi:putOi,oiChange:putOiCh,volume:putVol}});
      }
      return {symbol:'NIFTY',expiry:'11-11-2025',spot:spot,future:spot+80,lot:LOT_SIZE,rows,atm};
    }

    function el(q){return document.querySelector(q);} 
    function fmt(n){return n.toLocaleString('en-IN');}

    function computeTotals(rows){
      let cOi=0,cVol=0,cOiCh=0,pOi=0,pVol=0,pOiCh=0;
      rows.forEach(r=>{ cOi+=r.call.oi; cVol+=r.call.volume; cOiCh+=r.call.oiChange; pOi+=r.put.oi; pVol+=r.put.volume; pOiCh+=r.put.oiChange; });
      return {cOi,cVol,cOiCh,pOi,pVol,pOiCh};
    }

    function calcMaxPain(rows, spot){
      const strikes = rows.map(r=>r.strike).sort((a,b)=>a-b);
      const pain = {};
      for(const s of strikes){
        let total = 0;
        for(const r of rows){
          const callPain = Math.max(0, r.strike - s) * r.call.oi;
          const putPain  = Math.max(0, s - r.strike) * r.put.oi;
          total += callPain + putPain;
        }
        pain[s] = total;
      }
      const sorted = Object.entries(pain).sort((a,b)=>a[1]-b[1]);
      return {maxPainStrike: Number(sorted[0][0]), painTable: pain};
    }

    function detectReversal(oiChange){ 
      if(oiChange === undefined || oiChange === null) return ''; 
      const pct = Math.abs(oiChange); 
      if(pct > 50000) return 'Break Out'; 
      if(pct > 15000) return 'Break Down'; 
      return 'Neutral';
    }

    function applyItmClass(cell, side, distance){
      // side = 'call' | 'put', distance = integer >=1
      if(distance <= 0) return;
      const d = Math.min(distance,4); // clamp
      if(side === 'call'){
        cell.classList.add(`itm-call-${d}`);
        if(distance >= 3) cell.classList.add('deep-itm-call');
      } else {
        cell.classList.add(`itm-put-${d}`);
        if(distance >= 3) cell.classList.add('deep-itm-put');
      }
    }

    function renderTable(data, opts={}){
      const tbody = el('#tableBody'); if(!tbody) return;
      tbody.innerHTML = '';
      const rows = Array.isArray(data.rows) ? data.rows.slice() : [];
      if(rows.length === 0) return;

      const atm = Math.round((data.spot || 0)/50)*50;
      const maxCall = Math.max(...rows.map(r=>r.call.oi));
      const maxPut  = Math.max(...rows.map(r=>r.put.oi));

      const visibleCount = parseInt(el('#strikeRange')?.value || 12,10);
      const center = atm;
      rows.sort((a,b)=>Math.abs(a.strike-center)-Math.abs(b.strike-center));
      const visible = rows.slice(0, visibleCount).sort((a,b)=>a.strike-b.strike);

      visible.forEach(r=>{
        const tr = document.createElement('tr');
        tr.classList.add('premium-hover');

        const strikeDist = Math.abs(r.strike - atm) / 50; // 1,2,3,...
        const isCallITM = r.strike < atm;
        const isPutITM  = r.strike > atm;
        const callCellHtml = `<td class=\"heat\">${fmt(r.call.oiChange)}</td><td class=\"heat call-oi\">${fmt(r.call.oi)}</td><td>${fmt(r.call.volume)}</td>`;
        const rightCellHtml = `<td>${detectReversal(r.call.oiChange)}</td><td class=\"strike-col\">${r.strike}</td><td>${detectReversal(r.put.oiChange)}</td><td>${fmt(r.put.volume)}</td><td class=\"heat put-oi\">${fmt(r.put.oi)}</td><td class=\"heat\">${fmt(r.put.oiChange)}</td>`;

        tr.innerHTML = callCellHtml + rightCellHtml;
        try{
          tr.children[2].classList.add('vol-grey');
          tr.children[3].classList.add('rev-grey');
          tr.children[5].classList.add('rev-grey');
          tr.children[6].classList.add('vol-grey');
        }catch(e){}

        // apply ITM classes to specific cells (call OI is child index 1, strike index 4, put OI index 7)
        try{
          const callOiCell = tr.children[1];
          const strikeCell = tr.children[4];
          const putOiCell = tr.children[7];

          if(isCallITM){ applyItmClass(callOiCell,'call', Math.round(strikeDist)); strikeCell.classList.add('itm-strike'); }
          if(isPutITM){ applyItmClass(putOiCell,'put', Math.round(strikeDist)); strikeCell.classList.add('itm-strike'); }

          // add OI heat backgrounds (subtle) without overriding ITM classes
          const callIntensity = maxCall ? (r.call.oi / maxCall) : 0;
          const putIntensity = maxPut ? (r.put.oi / maxPut) : 0;
          if(!callOiCell.classList.contains('itm-call-1') && !callOiCell.classList.contains('itm-call-2') && !callOiCell.classList.contains('itm-call-3') && !callOiCell.classList.contains('itm-call-4')){
            callOiCell.style.background = `rgba(164,214,240,${0.06 + callIntensity*0.18})`;
          }
          if(!putOiCell.classList.contains('itm-put-1') && !putOiCell.classList.contains('itm-put-2') && !putOiCell.classList.contains('itm-put-3') && !putOiCell.classList.contains('itm-put-4')){
            putOiCell.style.background = `rgba(244,211,211,${0.06 + putIntensity*0.18})`;
          }

          // ATM highlight
          if(r.strike === atm){ strikeCell.classList.add('atm'); }

        }catch(e){ console.warn('renderCell err', e); }

        tbody.appendChild(tr);
      });

      const totals = computeTotals(visible);
      const tfoot = el('#tableFoot'); if(tfoot) tfoot.innerHTML = `<tr><td>Total ${fmt(totals.cOiCh)}</td><td>Total ${fmt(totals.cOi)}</td><td>Total ${fmt(totals.cVol)}</td><td></td><td></td><td></td><td>Total ${fmt(totals.pVol)}</td><td>Total ${fmt(totals.pOi)}</td><td>Total ${fmt(totals.pOiCh)}</td></tr>`;

      // Max pain
      const mp = calcMaxPain(data.rows, data.spot);
      const middle = el('#middleRisk'); if(middle){ const rl = middle.querySelector('#riskLabel'); if(rl) rl.innerText = `Max Pain : ${mp.maxPainStrike}`; }

      const wrap = el('#tableWrap'); if(wrap){ wrap.classList.add('flash'); setTimeout(()=>{ wrap.classList.remove('flash'); },800); }
    }

    function updateRiskPanel(data){
      const rows = Array.isArray(data.rows)? data.rows : [];
      if(rows.length===0) return;
      const maxCallStrike = rows.reduce((a,b)=> a.call.oi > b.call.oi ? a : b).strike;
      const maxPutStrike = rows.reduce((a,b)=> a.put.oi > b.put.oi ? a : b).strike;
      const resEl = el('#resistanceText'); if(resEl) resEl.innerText = `RESISTANCE ${maxCallStrike} - WTB ${maxCallStrike-50}`;
      const supEl = el('#supportText'); if(supEl) supEl.innerText = `SUPPORT ${maxPutStrike} - STRONG`;
      const lotEl = el('#lotLabel'); if(lotEl) lotEl.innerText = `LOT : ${data.lot || LOT_SIZE}`;
      const callSum = rows.reduce((s,r)=>s + r.call.oi,0);
      const putSum = rows.reduce((s,r)=>s + r.put.oi,0);
      const callTag = el('#callTag'); if(callTag) callTag.innerText = callSum > putSum ? 'STRONG' : 'WEAK TOWARDS BOTTOM';
      const putTag = el('#putTag'); if(putTag) putTag.innerText = putSum > callSum ? 'STRONG' : 'WTT TO STRONG';
    }

    // WebSocket + REST wiring (supports Authorization: Bearer <key>)
    let ws = null;
    function initWebSocket(){
      if(!API_WS_URL) return;
      try{
        ws = new WebSocket(API_WS_URL);
        ws.onopen = ()=>console.log('WS connected');
        ws.onmessage = ev=>{ try{ const d = JSON.parse(ev.data); handleIncomingData(d); }catch(e){console.warn('WS parse',e);} };
        ws.onclose = ()=>setTimeout(initWebSocket,5000);
      }catch(e){console.warn('WS init',e);} 
    }

    async function fetchOnce(){
      if(API_REST_URL){
        try{
          const headers = {};
          if(API_AUTH_KEY) headers['Authorization'] = `Bearer ${API_AUTH_KEY}`;
          const res = await fetch(API_REST_URL,{headers,cache:'no-store'});
          if(!res.ok) throw new Error('non-ok');
          const json = await res.json();
          handleIncomingData(json);
          return;
        }catch(e){console.warn('REST fail',e);} 
      }
      handleIncomingData(sampleData());
    }

    function handleIncomingData(data){
      if(!data || !Array.isArray(data.rows)) return;
      data.rows = data.rows.sort((a,b)=>a.strike-b.strike);
      const spotEl = el('#spotVal'); if(spotEl) spotEl.innerText = (data.spot||0).toFixed(2);
      const futEl = el('#futureVal'); if(futEl) futEl.innerText = (data.future||0).toFixed(2);
      const ts = el('#timestamp'); if(ts) ts.innerText = new Date().toLocaleString('en-IN');
      renderTable(data);
      updateRiskPanel(data);
    }

    // UI events (attach safely)
    document.addEventListener('DOMContentLoaded', ()=>{
      const openAcBtn = el('#openAcBtn'); if(openAcBtn) openAcBtn.addEventListener('click', ()=> window.open('https://angel-one.onelink.me/Wjgr/miss3eee','_blank'));
      const refreshBtn = el('#refreshBtn'); if(refreshBtn) refreshBtn.addEventListener('click', ()=>fetchOnce());
      const sortBtn = el('#sortOi'); if(sortBtn) sortBtn.addEventListener('click', ()=>{
        const tbody = el('#tableBody'); if(!tbody) return;
        const rows = Array.from(tbody.children);
        rows.sort((a,b)=>{ const aVal = parseInt(a.children[1].innerText.replace(/,/g,''),10) || 0; const bVal = parseInt(b.children[1].innerText.replace(/,/g,''),10) || 0; return bVal - aVal; });
        tbody.innerHTML=''; rows.forEach(r=>tbody.appendChild(r));
      });
      const strikeRange = el('#strikeRange'); if(strikeRange) strikeRange.addEventListener('input', ()=>fetchOnce());

      // start fetching after DOM ready
      initWebSocket(); fetchOnce(); setInterval(fetchOnce, REFRESH_INTERVAL_MS);

      // keyboard shortcut
      window.addEventListener('keydown', (e)=>{ if(e && e.key === 'r') fetchOnce(); });
    });

  </script>

  <script>
    // Analytics button: create panel and populate separately (NO <script> inside innerHTML)
    (function(){
      function createAnalyticsPanel(){
        if(document.getElementById('analyticsPanel')) return document.getElementById('analyticsPanel');
        const panel = document.createElement('div');
        panel.id = 'analyticsPanel';
        panel.style.position = 'fixed';
        panel.style.top = '0';
        panel.style.left = '60px';
        panel.style.width = 'calc(100% - 60px)';
        panel.style.height = '100vh';
        panel.style.background = '#ffffff';
        panel.style.zIndex = '6000';
        panel.style.overflowY = 'auto';
        panel.style.padding = '20px';

        const header = document.createElement('div');
        header.innerHTML = '<h2 style="margin:0 0 8px 0;font-size:24px;color:#111;font-weight:800">📊 Top 50 Stocks</h2>';
        panel.appendChild(header);

        const desc = document.createElement('div');
        desc.innerHTML = '<p style="color:#333;font-size:15px;margin:0 0 12px 0">Ranked by <strong>Volume + |OI change|</strong> (demo data). Click Close to dismiss.</p>';
        panel.appendChild(desc);

        const list = document.createElement('div');
        list.id = 'topStocksList';
        panel.appendChild(list);

        const close = document.createElement('button');
        close.textContent = 'Close';
        close.style.cssText = 'padding:8px 14px;background:#ff6600;color:#fff;border:none;border-radius:6px;font-weight:700;cursor:pointer;margin-top:18px';
        close.addEventListener('click', ()=>{ panel.remove(); });
        panel.appendChild(close);

        document.body.appendChild(panel);
        return panel;
      }

      function populateTopStocksDemo(){
        const panel = createAnalyticsPanel();
        const list = document.getElementById('topStocksList');
        if(!list) return;
        list.innerHTML = '';
        const demoStocks = Array.from({length:50}).map((_,i)=>({
          name:`STOCK-${i+1}`,
          volume:Math.floor(Math.random()*5000000+500000),
          oiChange:Math.floor(Math.random()*200000-50000)
        }));
        const sorted = demoStocks.sort((a,b)=> (b.volume + Math.abs(b.oiChange)) - (a.volume + Math.abs(a.oiChange)) );
        sorted.forEach(s=>{
          const card = document.createElement('div');
          card.className = 'stock-card';
          card.innerHTML = `<strong>${s.name}</strong><br>📦 Volume: ${s.volume.toLocaleString()}<br>📈 OI Change: ${s.oiChange.toLocaleString()}`;
          list.appendChild(card);
        });
      }

      const analyticsBtn = document.querySelector('.sidebar button[title="Analytics"]');
      if(analyticsBtn){
        analyticsBtn.addEventListener('click', ()=>{
          populateTopStocksDemo();
        });
      }
    })();
  </script>
</body>
</html>
