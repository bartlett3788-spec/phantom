<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Phantom</title>
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-title" content="Phantom" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css" />
  <style>
    :root{--color-text-primary:#1a1a1a;--color-text-secondary:#6b7280;--color-text-tertiary:#9ca3af;--color-background-primary:#ffffff;--color-background-secondary:#f3f4f6;--color-border-primary:#1a1a1a;--color-border-secondary:#d1d5db;--color-border-tertiary:#e5e7eb;--color-text-danger:#991b1b;--color-border-danger:#fca5a5;--border-radius-md:8px;--border-radius-lg:12px;--font-sans:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;}
    @media(prefers-color-scheme:dark){:root{--color-text-primary:#f9fafb;--color-text-secondary:#9ca3af;--color-text-tertiary:#6b7280;--color-background-primary:#111827;--color-background-secondary:#1f2937;--color-border-primary:#f9fafb;--color-border-secondary:#374151;--color-border-tertiary:#1f2937;--color-text-danger:#fca5a5;--color-border-danger:#991b1b;}}
    *{box-sizing:border-box;margin:0;padding:0}
    body{font-family:var(--font-sans);background:var(--color-background-primary);color:var(--color-text-primary);max-width:680px;margin:0 auto;padding:0 16px;min-height:100vh}
    .nav-bar{display:flex;align-items:center;border-bottom:0.5px solid var(--color-border-tertiary);margin-bottom:1.5rem;padding-top:12px}
    .nav-logo{display:flex;align-items:center;gap:8px;margin-right:auto;padding-bottom:12px}
    .nav-logo-mark{width:30px;height:30px;background:#1a1a1a;border-radius:8px;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:500;font-size:14px}
    .nav-logo-name{font-size:16px;font-weight:500;color:var(--color-text-primary)}
    .nav-links{display:flex}
    .nav-link{padding:10px 12px;font-size:13px;color:var(--color-text-secondary);cursor:pointer;border-bottom:2px solid transparent;white-space:nowrap}
    .nav-link.active{color:var(--color-text-primary);font-weight:500;border-bottom-color:#1a1a1a}
    .bottom-nav{display:flex;border-top:0.5px solid var(--color-border-tertiary);padding:.5rem 0 .25rem;margin-top:2rem;position:sticky;bottom:0;background:var(--color-background-primary)}
    .bn-item{flex:1;display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;padding:.5rem}
    .bn-icon{font-size:20px;color:var(--color-text-secondary)}
    .bn-label{font-size:10px;color:var(--color-text-secondary)}
    .bn-item.active .bn-icon,.bn-item.active .bn-label{color:var(--color-text-primary);font-weight:500}
    .screen{display:none}.screen.visible{display:block}
    .app-tab{display:none;padding-bottom:80px}
    .chip{display:inline-flex;align-items:center;gap:6px;padding:7px 14px;border-radius:20px;border:0.5px solid var(--color-border-secondary);font-size:13px;color:var(--color-text-primary);background:var(--color-background-primary);cursor:pointer;user-select:none;transition:all .15s}
    .chip:hover{background:var(--color-background-secondary)}
    .chip.active{background:#1a1a1a;color:#fff;border-color:#1a1a1a}
    .chip.warn.active{background:#993C1D;color:#fff;border-color:#993C1D}
    .chip-tk{font-size:11px;display:none}
    .chip.active .chip-tk{display:inline}
    .days-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:6px;margin-bottom:1.25rem}
    .day-chip{padding:10px 4px 5px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);font-size:13px;text-align:center;cursor:pointer;color:var(--color-text-primary);background:var(--color-background-primary);user-select:none;transition:all .15s}
    .day-chip.active{background:#1a1a1a;color:#fff;border-color:#1a1a1a}
    .day-tk{display:none;font-size:9px;margin-top:3px}
    .day-chip.active .day-tk{display:block}
    .struct-card{border:0.5px solid var(--color-border-secondary);border-radius:var(--border-radius-md);padding:.875rem 1rem;cursor:pointer;transition:all .15s;margin-bottom:8px;display:flex;align-items:flex-start;gap:10px}
    .struct-card:hover{background:var(--color-background-secondary)}
    .struct-card.sel{border:1.5px solid #1a1a1a;background:var(--color-background-secondary)}
    .struct-icon{width:22px;height:22px;border-radius:50%;border:1.5px solid var(--color-border-secondary);display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px;transition:all .15s;font-size:11px;color:transparent}
    .struct-card.sel .struct-icon{background:#1a1a1a;border-color:#1a1a1a;color:#fff}
    .struct-title{font-size:13px;font-weight:500;color:var(--color-text-primary)}
    .struct-desc{font-size:12px;color:var(--color-text-secondary);margin-top:2px}
    .day-strip{display:flex;gap:5px;margin-bottom:1.25rem;overflow-x:auto;-webkit-overflow-scrolling:touch}
    .ds-btn{min-width:42px;padding:8px 6px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);font-size:12px;text-align:center;cursor:pointer;color:var(--color-text-secondary);background:var(--color-background-primary);transition:all .15s;user-select:none;flex-shrink:0}
    .ds-btn.viewing{background:#1a1a1a;color:#fff;border-color:#1a1a1a}
    .ds-btn.rest-day{border-style:dashed}
    .ds-btn.today-dot::after{content:'';display:block;width:4px;height:4px;border-radius:50%;background:currentColor;margin:2px auto 0}
    .card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);overflow:hidden;margin-bottom:1rem}
    .card-head{padding:.875rem 1.25rem;border-bottom:0.5px solid var(--color-border-tertiary);display:flex;align-items:center;justify-content:space-between}
    .card-title{font-size:14px;font-weight:500;color:var(--color-text-primary)}
    .stats-grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:10px;margin-bottom:1rem}
    .stat-c{background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:.875rem 1rem;text-align:center}
    .stat-n{font-size:20px;font-weight:500;color:var(--color-text-primary)}
    .stat-l{font-size:11px;color:var(--color-text-secondary);margin-top:3px}
    .section-label{font-size:12px;font-weight:500;color:var(--color-text-secondary);text-transform:uppercase;letter-spacing:.05em;margin-bottom:.6rem}
    .section-hint{font-size:12px;color:var(--color-text-secondary);margin-bottom:.75rem;line-height:1.5}
    .name-input{width:100%;padding:12px 14px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);font-size:18px;font-weight:500;color:var(--color-text-primary);background:var(--color-background-primary);margin-bottom:.75rem}
    .name-input:focus{outline:none;border-color:var(--color-border-primary)}
    .stat-grid-2{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-bottom:1.25rem}
    .stat-card{background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:.875rem}
    .stat-lbl{font-size:12px;color:var(--color-text-secondary);margin-bottom:6px}
    .stat-inp{width:100%;padding:0;border:none;background:transparent;font-size:22px;font-weight:500;color:var(--color-text-primary)}
    .stat-inp:focus{outline:none}
    .stat-unit{font-size:12px;color:var(--color-text-secondary);margin-top:2px}
    .stat-sel{width:100%;border:none;background:transparent;font-size:18px;font-weight:500;color:var(--color-text-primary);padding:0}
    .range-block{margin-bottom:1.25rem}
    .range-header{display:flex;justify-content:space-between;margin-bottom:8px}
    .range-label{font-size:13px;color:var(--color-text-secondary)}
    .range-val{font-size:13px;font-weight:500;color:var(--color-text-primary)}
    .range-row{display:flex;align-items:center;gap:10px}
    .range-row span{font-size:12px;color:var(--color-text-secondary)}
    .range-row input[type=range]{flex:1}
    .btn-pri{width:100%;padding:14px;border-radius:var(--border-radius-md);border:none;background:#1a1a1a;color:#fff;font-size:15px;font-weight:500;cursor:pointer;transition:opacity .15s;margin-top:.5rem}
    .btn-pri:hover{opacity:.85}
    .btn-pri:disabled{opacity:.35;cursor:not-allowed}
    .btn-ghost{background:none;border:none;font-size:13px;color:var(--color-text-secondary);cursor:pointer;padding:8px;display:block;margin:0 auto}
    .ob-wrap{max-width:480px;margin:0 auto;padding:1rem 0}
    .ob-logo{width:52px;height:52px;background:#1a1a1a;border-radius:14px;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:500;font-size:22px;margin:0 auto 1.25rem}
    .avatar-large{width:72px;height:72px;border-radius:50%;background:var(--color-background-secondary);border:0.5px solid var(--color-border-tertiary);display:flex;align-items:center;justify-content:center;font-size:26px;font-weight:500;color:var(--color-text-secondary);margin:0 auto 1rem}
    .ob-progress{display:flex;gap:4px;margin-bottom:2rem}
    .ob-dot{height:3px;border-radius:2px;background:var(--color-border-tertiary);flex:1;transition:background .3s}
    .ob-dot.done,.ob-dot.active{background:#1a1a1a}
    .ob-title{font-size:22px;font-weight:500;color:var(--color-text-primary);margin-bottom:6px}
    .ob-sub{font-size:14px;color:var(--color-text-secondary);margin-bottom:1.5rem;line-height:1.6}
    .ob-card{background:var(--color-background-secondary);border-radius:var(--border-radius-lg);padding:1.25rem;margin-bottom:1rem}
    .summary-row{display:flex;align-items:center;justify-content:space-between;padding:8px 0;border-bottom:0.5px solid var(--color-border-tertiary)}
    .summary-row:last-child{border-bottom:none}
    .summary-key{font-size:13px;color:var(--color-text-secondary)}
    .summary-val{font-size:13px;font-weight:500;color:var(--color-text-primary);text-align:right;max-width:65%}
    .generating-wrap{text-align:center;padding:2rem 0}
    .gen-steps{display:flex;flex-direction:column;gap:8px;text-align:left;max-width:280px;margin:1.25rem auto 0}
    .gen-step{display:flex;align-items:center;gap:8px;font-size:13px;color:var(--color-text-secondary)}
    .gen-step.ga{color:var(--color-text-primary);font-weight:500}
    .gen-step.gd{color:var(--color-text-primary)}
    .gen-dot{width:8px;height:8px;border-radius:50%;background:var(--color-border-secondary);flex-shrink:0}
    .gen-dot.ga{background:#1a1a1a;box-shadow:0 0 0 2px var(--color-background-primary),0 0 0 3.5px #1a1a1a}
    .gen-dot.gd{background:#1a1a1a}
    .spinner{width:28px;height:28px;border:2.5px solid var(--color-border-tertiary);border-top-color:#1a1a1a;border-radius:50%;animation:spin .7s linear infinite;margin:0 auto}
    @keyframes spin{to{transform:rotate(360deg)}}
    .ex-table{width:100%;border-collapse:collapse}
    .ex-table th{font-size:11px;font-weight:500;color:var(--color-text-secondary);text-align:left;padding:8px 1.25rem;border-bottom:0.5px solid var(--color-border-tertiary);background:var(--color-background-secondary)}
    .ex-table th:not(:first-child){text-align:center}
    .ex-table td{padding:10px 1.25rem;font-size:13px;color:var(--color-text-primary);border-bottom:0.5px solid var(--color-border-tertiary);vertical-align:middle}
    .ex-table td:not(:first-child){text-align:center}
    .ex-table tr:last-child td{border-bottom:none}
    .log-btn{padding:5px 12px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);background:transparent;font-size:12px;color:var(--color-text-secondary);cursor:pointer}
    .log-btn.done{background:#1a1a1a;color:#fff;border-color:#1a1a1a}
    .progress-wrap{padding:.75rem 1.25rem 1rem;border-top:0.5px solid var(--color-border-tertiary)}
    .progress-header{display:flex;justify-content:space-between;font-size:12px;color:var(--color-text-secondary);margin-bottom:6px}
    .progress-track{height:4px;background:var(--color-border-tertiary);border-radius:2px}
    .progress-fill{height:4px;background:#1a1a1a;border-radius:2px;transition:width .3s}
    .finisher-card{background:#EAF3DE;border:0.5px solid #97C459;border-radius:var(--border-radius-md);padding:.875rem 1.25rem;margin:0 1.25rem 1.25rem}
    .finisher-title{font-size:13px;font-weight:500;color:#27500A;margin-bottom:4px}
    .finisher-item{font-size:12px;color:#3B6D11;padding:1px 0}
    .timer-bar{display:flex;align-items:center;gap:12px;padding:10px 1.25rem;background:var(--color-background-secondary);border-bottom:0.5px solid var(--color-border-tertiary)}
    .timer-ring{position:relative;width:40px;height:40px;flex-shrink:0}
    .timer-ring svg{transform:rotate(-90deg)}
    .timer-inner{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:500}
    .week-nav{display:flex;border:0.5px solid var(--color-border-secondary);border-radius:var(--border-radius-md);overflow:hidden;margin-bottom:1.25rem}
    .wk-btn{flex:1;padding:9px;font-size:13px;font-weight:500;border:none;background:transparent;color:var(--color-text-secondary);cursor:pointer;border-right:0.5px solid var(--color-border-tertiary)}
    .wk-btn:last-child{border-right:none}
    .wk-btn.active{background:#1a1a1a;color:#fff}
    .wk-btn.w4{color:#854F0B}.wk-btn.w4.active{background:#633806;color:#FAC775}
    .day-card{border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);overflow:hidden;margin-bottom:.75rem}
    .day-head{padding:.875rem 1.25rem;background:var(--color-background-secondary);border-bottom:0.5px solid var(--color-border-tertiary);display:flex;align-items:center;justify-content:space-between}
    .day-body{padding:.75rem 1.25rem}
    .ex-row-ai{display:flex;align-items:flex-start;gap:10px;padding:8px 0;border-bottom:0.5px solid var(--color-border-tertiary)}
    .ex-row-ai:last-child{border-bottom:none}
    .ex-num{width:22px;height:22px;border-radius:50%;background:#1a1a1a;color:#fff;font-size:11px;font-weight:500;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px}
    .toggle-row{display:flex;align-items:center;justify-content:space-between;padding:12px 0;border-bottom:0.5px solid var(--color-border-tertiary)}
    .toggle-row:last-child{border-bottom:none}
    .toggle{position:relative;width:44px;height:24px;flex-shrink:0}
    .toggle input{opacity:0;width:0;height:0}
    .toggle-slider{position:absolute;inset:0;background:var(--color-border-secondary);border-radius:12px;cursor:pointer;transition:.2s}
    .toggle-slider:before{content:'';position:absolute;width:18px;height:18px;left:3px;top:3px;background:#fff;border-radius:50%;transition:.2s}
    .toggle input:checked+.toggle-slider{background:#1a1a1a}
    .toggle input:checked+.toggle-slider:before{transform:translateX(20px)}
    .profile-row{display:flex;align-items:center;justify-content:space-between;padding:9px 1.25rem;border-bottom:0.5px solid var(--color-border-tertiary)}
    .profile-row:last-child{border-bottom:none}
    .pr-key{font-size:13px;color:var(--color-text-secondary)}
    .pr-val{font-size:13px;font-weight:500;color:var(--color-text-primary);text-align:right;max-width:60%}
    .divider{height:0.5px;background:var(--color-border-tertiary);margin:1.5rem 0}
    .api-setup{background:var(--color-background-secondary);border-radius:var(--border-radius-lg);padding:1.5rem;margin-bottom:1rem}
    .api-input{width:100%;padding:10px 12px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);font-size:14px;color:var(--color-text-primary);background:var(--color-background-primary);margin-bottom:.75rem;font-family:monospace}
    .api-input:focus{outline:none;border-color:#1a1a1a}
  </style>
</head>
<body>
<div class="screen visible" id="screen-ob">
  <div class="ob-wrap" id="ob-inner"></div>
</div>

<div class="screen" id="screen-app">
  <div class="nav-bar">
    <div class="nav-logo">
      <div class="nav-logo-mark">Ph</div>
      <div class="nav-logo-name">Phantom</div>
    </div>
    <div class="nav-links">
      <div class="nav-link active" onclick="goTab('today')" id="nl-today">Today</div>
      <div class="nav-link" onclick="goTab('programme')" id="nl-programme">Programme</div>
      <div class="nav-link" onclick="goTab('progress')" id="nl-progress">Progress</div>
      <div class="nav-link" onclick="goTab('profile')" id="nl-profile">Profile</div>
    </div>
  </div>

  <div class="app-tab" id="tab-today">
    <div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:1rem">
      <div>
        <div style="font-size:22px;font-weight:500;color:var(--color-text-primary)" id="t-greeting">Good morning</div>
        <div style="font-size:13px;color:var(--color-text-secondary);margin-top:2px" id="t-sub">—</div>
      </div>
      <div style="text-align:right">
        <div style="font-size:13px;font-weight:500;color:var(--color-text-primary)" id="t-block">Block 1</div>
        <div style="font-size:11px;color:var(--color-text-secondary)" id="t-week">Week 1 of 4</div>
      </div>
    </div>
    <div class="stats-grid">
      <div class="stat-c"><div class="stat-n" id="s-sess">0</div><div class="stat-l">Sessions</div></div>
      <div class="stat-c"><div class="stat-n" id="s-sets">0</div><div class="stat-l">Sets logged</div></div>
      <div class="stat-c"><div class="stat-n" id="s-pbs">0</div><div class="stat-l">PBs set</div></div>
      <div class="stat-c"><div class="stat-n" id="s-wk">1</div><div class="stat-l">Week</div></div>
    </div>
    <div class="day-strip" id="day-strip"></div>
    <div id="t-session"></div>
    <div id="t-modal"></div>
  </div>

  <div class="app-tab" id="tab-programme">
    <div style="font-size:22px;font-weight:500;color:var(--color-text-primary);margin-bottom:4px" id="p-title">Programme</div>
    <div style="font-size:13px;color:var(--color-text-secondary);margin-bottom:1.25rem" id="p-sub">—</div>
    <div class="week-nav">
      <button class="wk-btn active" onclick="setPW(1,this)">Week 1</button>
      <button class="wk-btn" onclick="setPW(2,this)">Week 2</button>
      <button class="wk-btn" onclick="setPW(3,this)">Week 3</button>
      <button class="wk-btn w4" onclick="setPW(4,this)">Week 4 🔥</button>
    </div>
    <div id="p-content"></div>
  </div>

  <div class="app-tab" id="tab-progress">
    <div style="font-size:22px;font-weight:500;color:var(--color-text-primary);margin-bottom:4px">Progress</div>
    <div style="font-size:13px;color:var(--color-text-secondary);margin-bottom:1.25rem" id="pr-sub">—</div>
    <div class="stats-grid">
      <div class="stat-c"><div class="stat-n" id="pr-sets">0</div><div class="stat-l">Sets</div></div>
      <div class="stat-c"><div class="stat-n" id="pr-vol">0<span style="font-size:11px">kg</span></div><div class="stat-l">Volume</div></div>
      <div class="stat-c"><div class="stat-n" id="pr-pbs">0</div><div class="stat-l">PBs</div></div>
      <div class="stat-c"><div class="stat-n" id="pr-sess">0</div><div class="stat-l">Sessions</div></div>
    </div>
    <div class="card"><div class="card-head"><div class="card-title">Personal bests</div></div><div id="pr-pblist" style="padding:.5rem 0"></div></div>
  </div>

  <div class="app-tab" id="tab-profile">
    <div style="display:flex;align-items:center;gap:14px;margin-bottom:1.5rem">
      <div style="width:52px;height:52px;border-radius:50%;background:#1a1a1a;display:flex;align-items:center;justify-content:center;font-size:18px;font-weight:500;color:#fff" id="pf-av">?</div>
      <div>
        <div style="font-size:18px;font-weight:500;color:var(--color-text-primary)" id="pf-name">—</div>
        <div style="font-size:13px;color:var(--color-text-secondary)" id="pf-sub">—</div>
      </div>
    </div>
    <div id="pf-editable"></div>
    <button style="width:100%;padding:13px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-danger);background:transparent;font-size:14px;font-weight:500;color:var(--color-text-danger);cursor:pointer;margin-top:.5rem" onclick="fullReset()">Reset & restart</button>
  </div>

  <div class="bottom-nav">
    <div class="bn-item active" onclick="goTab('today')" id="bn-today"><i class="ti ti-bolt bn-icon"></i><span class="bn-label">Today</span></div>
    <div class="bn-item" onclick="goTab('programme')" id="bn-programme"><i class="ti ti-calendar bn-icon"></i><span class="bn-label">Programme</span></div>
    <div class="bn-item" onclick="goTab('progress')" id="bn-progress"><i class="ti ti-chart-bar bn-icon"></i><span class="bn-label">Progress</span></div>
    <div class="bn-item" onclick="goTab('profile')" id="bn-profile"><i class="ti ti-user bn-icon"></i><span class="bn-label">Profile</span></div>
  </div>
</div>

<script>
const STORAGE_KEY='phantom-v1';
const DAYS=['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
const DAYS_SHORT=['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];
const S2F={Sun:'Sunday',Mon:'Monday',Tue:'Tuesday',Wed:'Wednesday',Thu:'Thursday',Fri:'Friday',Sat:'Saturday'};
const F2S=Object.fromEntries(Object.entries(S2F).map(([s,f])=>[f,s]));
const STRUCTURES=[
  {id:'PPL_UL',label:'PPL / Upper-Lower',desc:'Alternates Push, Pull, Legs with Upper/Lower. Great for 4–5 days.'},
  {id:'PPL',label:'Push Pull Legs',desc:'Rotates Push → Pull → Legs. Ideal for 3–6 training days.'},
  {id:'UL',label:'Upper / Lower',desc:'Alternates upper and lower body. Best for 4 days per week.'},
  {id:'MSG',label:'Muscle group split',desc:'Dedicated day per muscle group. Best for 5+ days.'},
  {id:'TB',label:'Total body',desc:'Full-body compounds every session. Perfect for 3 days.'},
  {id:'CIRCUIT',label:'Circuit / HIIT',desc:'Timed rounds of mixed movements. High calorie burn.'},
];
const EX={
  Push:[{name:'Barbell bench press',sets:4,reps:'6-8',tw:'60kg',notes:'Control the descent'},{name:'Overhead press',sets:3,reps:'8-10',tw:'40kg',notes:'Full lockout overhead'},{name:'Incline dumbbell press',sets:3,reps:'10-12',tw:'22kg',notes:'Slight arch, full ROM'},{name:'Lateral raises',sets:3,reps:'12-15',tw:'10kg',notes:'Lead with elbows'},{name:'Tricep pushdown',sets:3,reps:'12-15',tw:'25kg',notes:'Elbows pinned to sides'}],
  Pull:[{name:'Barbell row',sets:4,reps:'6-8',tw:'60kg',notes:'Retract scapula at top'},{name:'Pull-ups',sets:3,reps:'6-8',tw:'BW',notes:'Dead hang start'},{name:'Cable row',sets:3,reps:'10-12',tw:'50kg',notes:'Squeeze at peak'},{name:'Face pulls',sets:3,reps:'15',tw:'20kg',notes:'Elbows high'},{name:'Dumbbell curl',sets:3,reps:'12',tw:'16kg',notes:'Supinate fully at top'}],
  Legs:[{name:'Barbell squat',sets:4,reps:'6-8',tw:'80kg',notes:'Break hips and knees together'},{name:'Romanian deadlift',sets:3,reps:'8-10',tw:'70kg',notes:'Hinge at hips, soft knee'},{name:'Leg press',sets:3,reps:'10-12',tw:'120kg',notes:'Feet shoulder-width'},{name:'Leg curl',sets:3,reps:'12',tw:'40kg',notes:'Full extension at bottom'},{name:'Calf raises',sets:4,reps:'15',tw:'60kg',notes:'Full stretch at bottom'}],
  Upper:[{name:'Deadlift',sets:4,reps:'5',tw:'100kg',notes:'Brace hard, drive through floor'},{name:'Dumbbell shoulder press',sets:3,reps:'8-10',tw:'28kg',notes:"Don't flare elbows"},{name:'Chest-supported row',sets:3,reps:'10-12',tw:'20kg',notes:'Chest stays on pad'},{name:'Dips',sets:3,reps:'8-10',tw:'BW',notes:'Lean forward for chest'},{name:'EZ bar curl',sets:3,reps:'10-12',tw:'30kg',notes:'No swinging'}],
  Lower:[{name:'Front squat',sets:4,reps:'6-8',tw:'65kg',notes:'Elbows high, upright torso'},{name:'Good mornings',sets:3,reps:'10-12',tw:'40kg',notes:'Soft knee, hinge at hip'},{name:'Walking lunges',sets:3,reps:'12 each',tw:'20kg',notes:'Knee tracks over toe'},{name:'Nordic curl',sets:3,reps:'8',tw:'BW',notes:'Slow eccentric'},{name:'Seated calf raises',sets:4,reps:'15',tw:'50kg',notes:'Pause at bottom'}],
  'Total Body A':[{name:'Barbell squat',sets:4,reps:'6-8',tw:'75kg',notes:'Full depth'},{name:'Bench press',sets:3,reps:'8-10',tw:'60kg',notes:'Controlled tempo'},{name:'Barbell row',sets:3,reps:'8-10',tw:'55kg',notes:'Strict form'},{name:'Romanian deadlift',sets:3,reps:'10-12',tw:'65kg',notes:'Hamstring stretch'},{name:'Overhead press',sets:2,reps:'12',tw:'35kg',notes:'Core tight throughout'}],
  'Total Body B':[{name:'Deadlift',sets:4,reps:'5',tw:'100kg',notes:'Perfect bracing'},{name:'Incline dumbbell press',sets:3,reps:'8-10',tw:'24kg',notes:'Full range of motion'},{name:'Pull-ups',sets:3,reps:'6-8',tw:'BW',notes:'Dead hang, full extension'},{name:'Leg press',sets:3,reps:'10-12',tw:'110kg',notes:"Don't lock out knees"},{name:'Dumbbell curl',sets:3,reps:'12',tw:'16kg',notes:'Supinate at top'}],
  Circuit:[{name:'Burpees',sets:4,reps:'45 sec',tw:'BW',notes:'Full extension at top'},{name:'Dumbbell thrusters',sets:4,reps:'12',tw:'16kg',notes:'Squat to press in one motion'},{name:'Mountain climbers',sets:3,reps:'30 sec',tw:'BW',notes:'Hips level'},{name:'Kettlebell swings',sets:3,reps:'15',tw:'20kg',notes:'Hip hinge, not a squat'},{name:'Box jumps',sets:3,reps:'10',tw:'BW',notes:'Soft landing, full depth'}],
  'Chest & Triceps':[{name:'Barbell bench press',sets:4,reps:'6-8',tw:'65kg',notes:'Full ROM, controlled eccentric'},{name:'Incline dumbbell press',sets:3,reps:'10-12',tw:'24kg',notes:'Slight arch'},{name:'Cable fly',sets:3,reps:'12-15',tw:'20kg',notes:'Squeeze at centre'},{name:'Tricep pushdown',sets:3,reps:'12',tw:'27kg',notes:'Elbows fixed'},{name:'Skull crushers',sets:3,reps:'10-12',tw:'30kg',notes:'Lower to forehead'}],
  'Back & Biceps':[{name:'Deadlift',sets:4,reps:'5',tw:'100kg',notes:'Brace and drive'},{name:'Barbell row',sets:4,reps:'6-8',tw:'65kg',notes:'Bar to belly button'},{name:'Cable row',sets:3,reps:'10-12',tw:'55kg',notes:'Neutral spine'},{name:'Barbell curl',sets:3,reps:'10-12',tw:'35kg',notes:'No swinging'},{name:'Hammer curl',sets:3,reps:'12',tw:'16kg',notes:'Neutral grip throughout'}],
  Shoulders:[{name:'Barbell overhead press',sets:4,reps:'6-8',tw:'45kg',notes:'Full lockout'},{name:'Dumbbell lateral raise',sets:4,reps:'12-15',tw:'10kg',notes:'Lead with elbows'},{name:'Cable face pulls',sets:3,reps:'15',tw:'22kg',notes:'Elbows high'},{name:'Rear delt fly',sets:3,reps:'15',tw:'8kg',notes:'Slight forward lean'},{name:'Arnold press',sets:3,reps:'10-12',tw:'18kg',notes:'Rotate palms as you press'}],
  Arms:[{name:'EZ bar curl',sets:4,reps:'8-10',tw:'32kg',notes:'Full supination'},{name:'Tricep pushdown',sets:4,reps:'10-12',tw:'28kg',notes:'Elbows pinned'},{name:'Incline dumbbell curl',sets:3,reps:'10-12',tw:'14kg',notes:'Stretch at bottom'},{name:'Overhead tricep extension',sets:3,reps:'10-12',tw:'25kg',notes:'Elbows close to head'},{name:'Hammer curl',sets:3,reps:'12',tw:'16kg',notes:'Neutral grip'}],
};
const SEQ={PPL_UL:['Push','Pull','Legs','Upper','Lower','Push','Pull'],PPL:['Push','Pull','Legs','Push','Pull','Legs','Push'],UL:['Upper','Lower','Upper','Lower','Upper','Lower','Upper'],MSG:['Chest & Triceps','Back & Biceps','Legs','Shoulders','Arms','Chest & Triceps','Back & Biceps'],TB:['Total Body A','Total Body B','Total Body A','Total Body B','Total Body A','Total Body B','Total Body A'],CIRCUIT:['Circuit','Circuit','Circuit','Circuit','Circuit','Circuit','Circuit']};
const WK_ADJ=[0,2.5,5,7.5];
let obStep=0;
const OB_STEPS=9;
let P={name:'',type:'Strength',structure:'PPL_UL',goal:'Muscle gain',exp:'Intermediate',age:30,weight:80,height:178,sex:'Male',days:{Mon:true,Tue:false,Wed:true,Thu:false,Fri:true,Sat:true,Sun:false},time:60,equip:[],injuries:[],rest:'Medium'};
let ST={loggedSets:{},pbs:{},totalSets:0,totalSessions:0,block:1,week:1,onboarded:false,programme:null,apiKey:''};
let viewDayIdx=new Date().getDay();
let progWeek=1,modalCtx=null,rpe=null,timerSecs=0,timerInt=null;

function loadState(){
  try{const raw=localStorage.getItem(STORAGE_KEY);if(raw){const s=JSON.parse(raw);if(s.profile)P={...P,...s.profile};const{profile:_,...rest}=s;ST={...ST,...rest};if(ST.programme&&!isValidProg(ST.programme)){ST.programme=null;ST.onboarded=false;}}}catch(e){}
  viewDayIdx=new Date().getDay();
  if(ST.onboarded&&ST.programme)launchApp();else{obStep=0;renderOB();}
}
function save(){try{localStorage.setItem(STORAGE_KEY,JSON.stringify({...ST,profile:P}));}catch(e){}}
function activeFull(){return DAYS.filter(fd=>P.days[F2S[fd]]);}
function isValidProg(p){if(!p||!Array.isArray(p.weeks)||p.weeks.length===0)return false;const w1=p.weeks[0];if(!Array.isArray(w1.days)||w1.days.length!==7)return false;return w1.days.some(d=>!d.isRest&&Array.isArray(d.exercises)&&d.exercises.length>0);}
function avInit(n){const p=n.trim().split(' ').filter(Boolean);return(p.length>=2?p[0][0]+p[p.length-1][0]:n.trim().slice(0,2)).toUpperCase()||'?';}
function soloChip(el,gid){document.querySelectorAll('#'+gid+' .chip').forEach(c=>c.classList.remove('active'));el.classList.add('active');}
function toggleArr(arr,val){const i=arr.indexOf(val);if(i>-1)arr.splice(i,1);else arr.push(val);}
function selStruct(el){document.querySelectorAll('.struct-card').forEach(c=>c.classList.remove('sel'));el.classList.add('sel');}
function chip(label,active,onclick){return`<div class="chip ${active?'active':''}" onclick="${onclick}"><i class="ti ti-check chip-tk"></i>${label}</div>`;}
function warnChip(label,active,onclick){return`<div class="chip warn ${active?'active':''}" onclick="${onclick}"><i class="ti ti-check chip-tk"></i>${label}</div>`;}
function structCard(s,selected){return`<div class="struct-card ${selected?'sel':''}" onclick="P.structure='${s.id}';selStruct(this)"><div class="struct-icon"><i class="ti ti-check"></i></div><div><div class="struct-title">${s.label}</div><div class="struct-desc">${s.desc}</div></div></div>`;}
function obProg(){return`<div class="ob-progress">${Array.from({length:OB_STEPS},(_,i)=>`<div class="ob-dot ${i<obStep?'done':i===obStep?'active':''}"></div>`).join('')}</div>`;}
function nextOB(){obStep=Math.min(obStep+1,OB_STEPS-1);renderOB();}
function prevOB(){obStep=Math.max(obStep-1,0);renderOB();}

function renderOB(){
  const c=document.getElementById('ob-inner');
  const SK=DAYS_SHORT;
  if(obStep===0){c.innerHTML=`<div style="text-align:center;padding:2rem 0 1rem"><div class="ob-logo">Ph</div><div style="font-size:28px;font-weight:500;color:var(--color-text-primary);margin-bottom:8px">Welcome to Phantom</div><div style="font-size:15px;color:var(--color-text-secondary);line-height:1.7;margin-bottom:2rem">Your AI-powered personal trainer.<br>A programme built entirely around you.</div><div style="display:flex;flex-direction:column;gap:10px;text-align:left;max-width:300px;margin:0 auto 2rem">${[['ti-bolt','AI-generated 4-week programmes'],['ti-chart-bar','Progressive overload calculated weekly'],['ti-flame','Week 4 max-effort progress day'],['ti-repeat','Continuous blocks built from your data']].map(([ic,tx])=>`<div style="display:flex;align-items:center;gap:10px;font-size:14px;color:var(--color-text-primary)"><div style="width:30px;height:30px;background:var(--color-background-secondary);border-radius:8px;display:flex;align-items:center;justify-content:center;flex-shrink:0"><i class="ti ${ic}" style="font-size:16px;color:var(--color-text-secondary)"></i></div>${tx}</div>`).join('')}</div><button class="btn-pri" style="max-width:320px;margin:0 auto" onclick="nextOB()">Get started →</button></div>`;return;}
  if(obStep===1){c.innerHTML=`${obProg()}<div class="ob-title">Connect your AI</div><div class="ob-sub">Phantom uses Claude AI to generate your programme. You need a free Anthropic API key.</div><div class="api-setup"><div style="display:flex;flex-direction:column;gap:10px;margin-bottom:1rem"><div style="display:flex;align-items:center;gap:10px;font-size:13px;color:var(--color-text-primary)"><div style="width:24px;height:24px;background:#1a1a1a;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:12px;font-weight:500;flex-shrink:0">1</div>Go to <a href="https://console.anthropic.com" target="_blank" style="color:#3C3489">console.anthropic.com</a> and sign up free</div><div style="display:flex;align-items:center;gap:10px;font-size:13px;color:var(--color-text-primary)"><div style="width:24px;height:24px;background:#1a1a1a;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:12px;font-weight:500;flex-shrink:0">2</div>Click <strong>API Keys</strong> in the left sidebar</div><div style="display:flex;align-items:center;gap:10px;font-size:13px;color:var(--color-text-primary)"><div style="width:24px;height:24px;background:#1a1a1a;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:12px;font-weight:500;flex-shrink:0">3</div>Click <strong>Create Key</strong>, copy it and paste below</div></div><input class="api-input" id="api-key-input" type="password" placeholder="sk-ant-api03-..." value="${ST.apiKey||''}" oninput="ST.apiKey=this.value" /><div style="font-size:12px;color:var(--color-text-secondary);line-height:1.5">Your key is stored only on this device and sent only to Anthropic to generate your programme.</div></div><button class="btn-pri" onclick="const v=document.getElementById('api-key-input').value.trim();if(v.startsWith('sk-')){ST.apiKey=v;nextOB();}else{alert('Please enter a valid key starting with sk-ant-');}">Continue →</button><button class="btn-ghost" onclick="prevOB()">Back</button>`;return;}
  if(obStep===2){c.innerHTML=`${obProg()}<div class="avatar-large" id="ob-av">${avInit(P.name)||'?'}</div><div class="ob-title">What's your name?</div><div class="ob-sub">Phantom will personalise everything around you.</div><input class="name-input" id="ob-name" placeholder="Your name" value="${P.name}" oninput="P.name=this.value;const el=document.getElementById('ob-av');if(el)el.textContent=avInit(this.value)||'?'" /><button class="btn-pri" onclick="P.name.trim()?nextOB():document.getElementById('ob-name').focus()">Continue →</button><button class="btn-ghost" onclick="prevOB()">Back</button>`;setTimeout(()=>document.getElementById('ob-name')?.focus(),80);return;}
  if(obStep===3){c.innerHTML=`${obProg()}<div class="ob-title">Programme type</div><div class="ob-sub">What are you training for?</div><div class="section-label">Type</div><div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:1.25rem" id="ob-type">${['Strength','Physique','Fitness','Hobby'].map(t=>chip(t,P.type===t,`P.type='${t}';soloChip(this,'ob-type')`)).join('')}</div><div class="section-label">Primary goal</div><div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:1.25rem" id="ob-goal">${['Muscle gain','Fat loss','Recomposition','Strength gains','General fitness'].map(g=>chip(g,P.goal===g,`P.goal='${g}';soloChip(this,'ob-goal')`)).join('')}</div><div class="section-label">Experience</div><div style="display:flex;flex-wrap:wrap;gap:8px" id="ob-exp">${[['Novice','0–6 months'],['Intermediate','6–24 months'],['Experienced','24+ months']].map(([e,d])=>chip(`${e} <span style="font-size:11px;opacity:.6">${d}</span>`,P.exp===e,`P.exp='${e}';soloChip(this,'ob-exp')`)).join('')}</div><button class="btn-pri" style="margin-top:1.25rem" onclick="nextOB()">Continue →</button><button class="btn-ghost" onclick="prevOB()">Back</button>`;return;}
  if(obStep===4){c.innerHTML=`${obProg()}<div class="ob-title">Programme structure</div><div class="ob-sub">How should your sessions be arranged across the week?</div><div id="structures">${STRUCTURES.map(s=>structCard(s,P.structure===s.id)).join('')}</div><button class="btn-pri" style="margin-top:.5rem" onclick="nextOB()">Continue →</button><button class="btn-ghost" onclick="prevOB()">Back</button>`;return;}
  if(obStep===5){c.innerHTML=`${obProg()}<div class="ob-title">About you</div><div class="ob-sub">Used to calculate personalised starting weights.</div><div class="stat-grid-2"><div class="stat-card"><div class="stat-lbl">Age</div><input type="number" class="stat-inp" value="${P.age}" oninput="P.age=parseInt(this.value)||P.age" /><div class="stat-unit">years</div></div><div class="stat-card"><div class="stat-lbl">Weight</div><input type="number" class="stat-inp" value="${P.weight}" oninput="P.weight=parseFloat(this.value)||P.weight" /><div class="stat-unit">kg</div></div><div class="stat-card"><div class="stat-lbl">Height</div><input type="number" class="stat-inp" value="${P.height}" oninput="P.height=parseInt(this.value)||P.height" /><div class="stat-unit">cm</div></div><div class="stat-card"><div class="stat-lbl">Sex</div><select class="stat-sel" onchange="P.sex=this.value"><option ${P.sex==='Male'?'selected':''}>Male</option><option ${P.sex==='Female'?'selected':''}>Female</option><option ${P.sex==='Other'?'selected':''}>Other</option></select><div class="stat-unit">—</div></div></div><button class="btn-pri" onclick="nextOB()">Continue →</button><button class="btn-ghost" onclick="prevOB()">Back</button>`;return;}
  if(obStep===6){c.innerHTML=`${obProg()}<div class="ob-title">Training schedule</div><div class="ob-sub">Which days can you train, and how long per session?</div><div class="section-label">Training days</div><div class="days-grid">${SK.map(sk=>`<div class="day-chip ${P.days[sk]?'active':''}" onclick="P.days['${sk}']=!P.days['${sk}'];this.classList.toggle('active')">${sk}<div class="day-tk"><i class="ti ti-check"></i></div></div>`).join('')}</div><div class="range-block"><div class="range-header"><span class="range-label">Session length</span><span class="range-val" id="ob-tv">${P.time} min</span></div><div class="range-row"><span>20m</span><input type="range" min="20" max="120" step="5" value="${P.time}" oninput="P.time=parseInt(this.value);document.getElementById('ob-tv').textContent=this.value+' min'" /><span>2hr</span></div></div><div class="section-label">Rest periods</div><div style="display:flex;flex-wrap:wrap;gap:8px" id="ob-rest">${['Short (30–60s)','Medium (60–90s)','Long (2–3 min)'].map(r=>chip(r,P.rest===r,`P.rest='${r}';soloChip(this,'ob-rest')`)).join('')}</div><button class="btn-pri" style="margin-top:1.25rem" onclick="nextOB()">Continue →</button><button class="btn-ghost" onclick="prevOB()">Back</button>`;return;}
  if(obStep===7){const equips=['Full gym','Dumbbells','Bench','Pull-up bar','Barbell','Cable machine','Resistance bands','Dip bar','Treadmill','Rower'];const injList=['Shoulder','Lower back','Knee','Hip','Wrist','Elbow','Ankle','None'];c.innerHTML=`${obProg()}<div class="ob-title">Equipment & limitations</div><div class="ob-sub">Phantom only prescribes exercises you can do.</div><div class="section-label">Equipment available</div><div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:1.25rem">${equips.map(e=>chip(e,P.equip.includes(e),`toggleArr(P.equip,'${e}');this.classList.toggle('active')`)).join('')}</div><div class="section-label">Injuries or areas to avoid</div><div class="section-hint">Phantom substitutes exercises around these</div><div style="display:flex;flex-wrap:wrap;gap:8px">${injList.map(inj=>warnChip(inj,P.injuries.includes(inj),`toggleArr(P.injuries,'${inj}');this.classList.toggle('active')`)).join('')}</div><button class="btn-pri" style="margin-top:1.25rem" onclick="nextOB()">Continue →</button><button class="btn-ghost" onclick="prevOB()">Back</button>`;return;}
  if(obStep===8){const af=activeFull();const sLabel=STRUCTURES.find(s=>s.id===P.structure)?.label||P.structure;c.innerHTML=`${obProg()}<div style="text-align:center;margin-bottom:1.5rem"><div class="avatar-large">${avInit(P.name)||'?'}</div><div style="font-size:20px;font-weight:500;color:var(--color-text-primary);margin-bottom:4px">${P.name||'Ready'}</div><div style="font-size:13px;color:var(--color-text-secondary)">${P.type} · ${P.exp} · ${P.goal}</div></div><div class="ob-card"><div class="summary-row"><div class="summary-key">Structure</div><div class="summary-val">${sLabel}</div></div><div class="summary-row"><div class="summary-key">Goal</div><div class="summary-val">${P.goal}</div></div><div class="summary-row"><div class="summary-key">Experience</div><div class="summary-val">${P.exp}</div></div><div class="summary-row"><div class="summary-key">Stats</div><div class="summary-val">${P.age}yo · ${P.weight}kg · ${P.height}cm</div></div><div class="summary-row"><div class="summary-key">Training days</div><div class="summary-val">${af.join(', ')||'None'}</div></div><div class="summary-row"><div class="summary-key">Session time</div><div class="summary-val">${P.time} min</div></div><div class="summary-row"><div class="summary-key">Equipment</div><div class="summary-val">${P.equip.length?P.equip.slice(0,3).join(', ')+(P.equip.length>3?' +'+(P.equip.length-3)+' more':''):'Not set'}</div></div><div class="summary-row"><div class="summary-key">Injuries</div><div class="summary-val">${P.injuries.length?P.injuries.join(', '):'None'}</div></div></div><div style="display:flex;align-items:center;justify-content:center;gap:6px;margin-bottom:1rem;font-size:13px;color:var(--color-text-secondary)">✦ Claude AI generates your personalised plan</div><button class="btn-pri" id="gen-btn" onclick="generate()">⚡ Build my programme</button><button class="btn-ghost" onclick="prevOB()">Back</button>`;return;}
}

async function generate(){
  document.getElementById('gen-btn').disabled=true;
  const af=activeFull();
  const sLabel=STRUCTURES.find(s=>s.id===P.structure)?.label||P.structure;
  const equip=P.equip.length?P.equip.join(', '):'standard gym equipment';
  const inj=(P.injuries.length&&!P.injuries.includes('None'))?P.injuries.join(', '):'None';
  const structInstr={PPL_UL:'Rotate Push, Pull, Legs, Upper, Lower across training days.',PPL:'Rotate Push, Pull, Legs across training days.',UL:'Alternate Upper body and Lower body sessions.',MSG:'Assign: Chest & Triceps, Back & Biceps, Legs, Shoulders, Arms in order.',TB:'Every training day is a Total Body session.',CIRCUIT:'Every training day is a Circuit session.'};
  document.getElementById('ob-inner').innerHTML=`<div class="generating-wrap"><div class="spinner"></div><div style="font-size:16px;font-weight:500;color:var(--color-text-primary);margin-top:1.25rem">Building your programme</div><div style="font-size:13px;color:var(--color-text-secondary);margin-top:4px">${P.name} · ${sLabel}</div><div class="gen-steps">${['Analysing your profile','Designing '+sLabel+' structure','Selecting exercises','Calculating progressive overload','Adding coaching notes'].map((s,i)=>`<div class="gen-step ${i===0?'ga':''}" id="gs${i}"><div class="gen-dot ${i===0?'ga':''}"></div>${s}</div>`).join('')}</div></div>`;
  [800,1600,2400,3200].forEach((t,i)=>setTimeout(()=>{const prev=document.getElementById('gs'+i);const next=document.getElementById('gs'+(i+1));if(prev){prev.classList.replace('ga','gd');prev.querySelector('.gen-dot')?.classList.replace('ga','gd');}if(next){next.classList.add('ga');next.querySelector('.gen-dot')?.classList.add('ga');}},t));
  const prompt=`You are Phantom, an expert personal trainer AI. Generate a complete 4-week progressive ${P.type} programme.
PROFILE: Name=${P.name}, Structure=${sLabel}, Goal=${P.goal}, Experience=${P.exp}, Age=${P.age}, Weight=${P.weight}kg, Sex=${P.sex}
Training days (ONLY these): ${af.join(', ')}
Session time: ${P.time} minutes, Equipment: ${equip}, Avoid: ${inj}
STRUCTURE INSTRUCTION: ${structInstr[P.structure]||structInstr.PPL_UL}
STRICT RULES:
1. Output ONLY valid JSON. No markdown. No explanation.
2. "days" array must have EXACTLY 7 items in this order: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday.
3. Non-training days: isRest:true, no exercises field.
4. Training days (${af.join(', ')}): isRest:false, unique sessionType, 4-6 exercises, finisher string.
5. Each training day must have DIFFERENT exercises from other training days.
6. Only use equipment: ${equip}. Avoid exercises loading: ${inj}.
7. Weeks 2,3,4 must have progressively heavier targetWeight than week 1.
Return: {"programmeTitle":"string","summary":"string","weeks":[{"week":1,"days":[{"day":"Sunday","isRest":true},{"day":"Monday","isRest":false,"sessionType":"Push","duration":"${P.time} min","exercises":[{"name":"Exercise","sets":4,"reps":"6-8","targetWeight":"60kg","notes":"cue"}],"finisher":"description"},...5 more days]}],"phantomNotes":["note1","note2","note3"]}
Generate all 4 weeks with progressive weights.`;
  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json','x-api-key':ST.apiKey,'anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:4000,messages:[{role:'user',content:prompt}]})});
    const data=await res.json();
    if(data.error)throw new Error(data.error.message);
    const raw=data.content?.map(b=>b.text||'').join('')||'';
    const parsed=JSON.parse(raw.replace(/^```(?:json)?\s*/,'').replace(/\s*```$/,'').trim());
    if(!isValidProg(parsed))throw new Error('Invalid structure');
    ST.programme=parsed;
  }catch(e){console.warn('AI failed, using fallback:',e.message);ST.programme=buildFallback();}
  ST.onboarded=true;save();setTimeout(()=>launchApp(),300);
}

function buildFallback(){
  const af=activeFull();const seq=SEQ[P.structure]||SEQ.PPL_UL;const sLabel=STRUCTURES.find(s=>s.id===P.structure)?.label||P.structure;
  return{programmeTitle:`${P.name}'s 4-week ${P.type} programme`,summary:`A ${P.exp.toLowerCase()} ${P.type.toLowerCase()} programme using the ${sLabel} structure, training ${af.join(', ')}.`,phantomNotes:['Weights increase by ~2.5kg each week — stick to the targets.',`Sessions are ${P.time} minutes including warm-up.`,(P.injuries.length&&!P.injuries.includes('None'))?`Avoiding exercises loading the ${P.injuries.join(', ')}.`:'Full exercise selection in use.'],
  weeks:[1,2,3,4].map(wk=>({week:wk,days:DAYS.map(fullDay=>{const isTraining=af.includes(fullDay);if(!isTraining)return{day:fullDay,isRest:true};const tIdx=af.indexOf(fullDay);const sType=seq[tIdx%seq.length];const baseExs=EX[sType]||EX['Total Body A'];const adj=WK_ADJ[wk-1];return{day:fullDay,sessionType:sType,isRest:false,duration:`${P.time} min`,exercises:baseExs.map(ex=>{const b=parseFloat(ex.tw);return{name:ex.name,sets:ex.sets,reps:ex.reps,targetWeight:!isNaN(b)?(Math.round((b+adj)*2)/2)+'kg':ex.tw,notes:ex.notes};}),finisher:'3 rounds: 10 press-ups + 10 dumbbell rows, 30s rest'};})}))};}
  function launchApp(){
  document.getElementById('screen-ob').classList.remove('visible');
  document.getElementById('screen-app').classList.add('visible');
  document.querySelectorAll('.app-tab').forEach(t=>t.style.display='none');
  document.getElementById('tab-today').style.display='block';
  document.querySelectorAll('.nav-link,.bn-item').forEach(el=>el.classList.remove('active'));
  document.getElementById('nl-today').classList.add('active');
  document.getElementById('bn-today').classList.add('active');
  viewDayIdx=new Date().getDay();progWeek=ST.week;
  refreshToday();
}

function goTab(name){
  document.querySelectorAll('.app-tab').forEach(t=>t.style.display='none');
  document.getElementById('tab-'+name).style.display='block';
  document.querySelectorAll('.nav-link,.bn-item').forEach(el=>el.classList.remove('active'));
  document.getElementById('nl-'+name).classList.add('active');
  document.getElementById('bn-'+name).classList.add('active');
  if(name==='today')refreshToday();
  if(name==='programme'){progWeek=ST.week;renderProg();}
  if(name==='progress')renderProgress();
  if(name==='profile')renderProfileTab();
}

function refreshToday(){updateHeader();renderDayStrip();renderSession();}

function updateHeader(){
  const hr=new Date().getHours();
  const greet=hr<12?'Good morning':hr<17?'Good afternoon':'Good evening';
  const vd=DAYS[viewDayIdx];
  const wk=ST.programme?.weeks.find(w=>w.week===ST.week)||ST.programme?.weeks[0];
  const sess=wk?.days[viewDayIdx];
  const sDesc=(sess&&!sess.isRest)?` · ${sess.sessionType}`:'· Rest day';
  document.getElementById('t-greeting').textContent=`${greet}, ${P.name}`;
  document.getElementById('t-sub').textContent=`Block ${ST.block} · Week ${ST.week} · ${vd} ${sDesc}`;
  document.getElementById('t-block').textContent=`Block ${ST.block}`;
  document.getElementById('t-week').textContent=`Week ${ST.week} of 4`;
  document.getElementById('s-sess').textContent=ST.totalSessions;
  document.getElementById('s-sets').textContent=ST.totalSets;
  document.getElementById('s-pbs').textContent=Object.keys(ST.pbs).length;
  document.getElementById('s-wk').textContent=ST.week;
  const av=avInit(P.name)||'?';
  document.getElementById('pf-av').textContent=av;
  document.getElementById('pf-name').textContent=P.name;
  document.getElementById('pf-sub').textContent=`Block ${ST.block} · ${P.exp} · ${P.type}`;
}

function renderDayStrip(){
  const strip=document.getElementById('day-strip');
  const todayIdx=new Date().getDay();
  const wk=ST.programme?.weeks.find(w=>w.week===ST.week)||ST.programme?.weeks[0];
  strip.innerHTML=DAYS.map((fullDay,idx)=>{
    const dayData=wk?.days[idx];
    const isRest=!dayData||dayData.isRest;
    const isToday=idx===todayIdx;
    const isViewing=idx===viewDayIdx;
    return`<div class="ds-btn${isRest?' rest-day':''}${isViewing?' viewing':''}${isToday?' today-dot':''}" onclick="viewDayIdx=${idx};renderDayStrip();renderSession();updateHeader()" title="${fullDay}">${DAYS_SHORT[idx]}</div>`;
  }).join('');
}

function renderSession(){
  const c=document.getElementById('t-session');
  if(!ST.programme){c.innerHTML='';return;}
  const vd=DAYS[viewDayIdx];
  const wk=ST.programme.weeks.find(w=>w.week===ST.week)||ST.programme.weeks[0];
  const dayData=wk?.days[viewDayIdx];
  if(!dayData||dayData.isRest){c.innerHTML=`<div style="background:var(--color-background-secondary);border-radius:var(--border-radius-lg);padding:2rem;text-align:center"><div style="font-size:28px;color:var(--color-text-secondary);margin-bottom:.5rem">🌙</div><div style="font-size:15px;font-weight:500;color:var(--color-text-primary)">Rest day</div><div style="font-size:13px;color:var(--color-text-secondary);margin-top:4px">${vd} — recovery is where the gains happen.</div></div>`;return;}
  const sk=`w${ST.week}:${viewDayIdx}`;
  const exs=dayData.exercises||[];
  const logged=ST.loggedSets[sk]||{};
  const totalSets=exs.reduce((a,e)=>a+e.sets,0);
  const doneSets=exs.reduce((a,_,i)=>a+(logged[i]?.length||0),0);
  const pct=totalSets>0?Math.round((doneSets/totalSets)*100):0;
  const allDone=doneSets>=totalSets&&totalSets>0;
  const badges={Push:'#E6F1FB|#0C447C',Pull:'#E1F5EE|#085041',Legs:'#EEEDFE|#3C3489',Upper:'#FAEEDA|#412402',Lower:'#FAF0FB|#5C0A6E','Total Body A':'#F0F4FF|#1A3A8F','Total Body B':'#F0F4FF|#1A3A8F',Circuit:'#FAECE7|#712B13','Chest & Triceps':'#E6F1FB|#0C447C','Back & Biceps':'#E1F5EE|#085041',Shoulders:'#FAEEDA|#412402',Arms:'#EEEDFE|#3C3489'};
  const [bg,tc]=(badges[dayData.sessionType]||'#F0F0F0|#333').split('|');
  c.innerHTML=`<div class="card"><div class="card-head"><div><div class="card-title">${vd} — ${dayData.sessionType}</div><div style="font-size:12px;color:var(--color-text-secondary);margin-top:2px">⏱ ${dayData.duration} · ${exs.length} exercises · Week ${ST.week}</div></div><span style="background:${bg};color:${tc};padding:3px 10px;border-radius:20px;font-size:11px;font-weight:500">${dayData.sessionType}</span></div><div id="t-timer"></div><table class="ex-table"><thead><tr><th style="width:40%">Exercise</th><th>Sets</th><th>Target</th><th>Log</th></tr></thead><tbody>${exs.map((ex,i)=>{const sets=logged[i]||[];const exDone=sets.length>=ex.sets;const isPB=ST.pbs[ex.name]&&sets.some(s=>s.w>0&&s.w>=(ST.pbs[ex.name]-0.01));return`<tr><td><div style="font-size:13px;font-weight:500;color:var(--color-text-primary)">${ex.name}${isPB?` <span style="background:#EEEDFE;color:#3C3489;padding:1px 6px;border-radius:10px;font-size:10px">PB</span>`:''}</div><div style="font-size:11px;color:var(--color-text-secondary);margin-top:2px">${ex.notes||''}</div></td><td style="text-align:center"><div style="font-size:13px;font-weight:500">${ex.sets}</div><div style="font-size:11px;color:var(--color-text-secondary)">${sets.length}/${ex.sets}</div></td><td style="text-align:center"><div style="font-size:12px;font-weight:500">${ex.targetWeight}</div><div style="font-size:11px;color:var(--color-text-secondary)">${ex.reps}</div></td><td style="text-align:center"><button class="log-btn ${exDone?'done':''}" onclick="openModal('${sk}',${i})">${exDone?'✓':'Log'}</button></td></tr>`;}).join('')}</tbody></table><div class="progress-wrap"><div class="progress-header"><span>Session progress</span><span>${pct}%</span></div><div class="progress-track"><div class="progress-fill" style="width:${pct}%"></div></div></div>${dayData.finisher?`<div class="finisher-card"><div class="finisher-title">⚡ Finisher</div><div class="finisher-item">${dayData.finisher}</div></div>`:''} ${allDone?`<button style="margin:0 1.25rem 1.25rem;width:calc(100% - 2.5rem);padding:12px;border-radius:var(--border-radius-md);border:none;background:#1a1a1a;color:#fff;font-size:14px;font-weight:500;cursor:pointer" onclick="completeSession()">✓ Complete session</button>`:''}</div>`;
}

function completeSession(){ST.totalSessions++;ST.week=Math.min(ST.week+1,4);save();refreshToday();}

function openModal(sk,exIdx){modalCtx={sk,exIdx};rpe=null;renderModal();}
function closeModal(){modalCtx=null;document.getElementById('t-modal').innerHTML='';}

function renderModal(){
  if(!modalCtx){document.getElementById('t-modal').innerHTML='';return;}
  const{sk,exIdx}=modalCtx;
  const wk=ST.programme.weeks.find(w=>w.week===ST.week)||ST.programme.weeks[0];
  const ex=wk?.days[viewDayIdx]?.exercises[exIdx];
  if(!ex)return;
  const logged=ST.loggedSets[sk]?.[exIdx]||[];
  const nextSet=logged.length+1;
  const pb=ST.pbs[ex.name]||0;
  const rpes=['Very easy','Easy','Moderate','Hard','Max effort'];
  document.getElementById('t-modal').innerHTML=`<div style="position:fixed;inset:0;background:rgba(0,0,0,0.5);display:flex;align-items:flex-end;justify-content:center;z-index:100" onclick="if(event.target===this)closeModal()"><div style="background:var(--color-background-primary);border-radius:var(--border-radius-lg) var(--border-radius-lg) 0 0;width:100%;max-width:680px;overflow:hidden"><div style="width:36px;height:4px;background:var(--color-border-secondary);border-radius:2px;margin:12px auto 0"></div><div style="padding:1rem 1.25rem .75rem;border-bottom:0.5px solid var(--color-border-tertiary)"><div style="font-size:15px;font-weight:500;color:var(--color-text-primary)">${ex.name}</div><div style="font-size:12px;color:var(--color-text-secondary);margin-top:2px">Set ${nextSet} of ${ex.sets} · Target: ${ex.targetWeight} · PB: ${pb>0?pb+'kg':'—'}</div></div><div style="padding:1.25rem"><div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:1rem"><div><div style="font-size:12px;color:var(--color-text-secondary);margin-bottom:6px">Weight (kg)</div><input type="number" step="0.5" id="m-w" style="width:100%;padding:10px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-primary);font-size:22px;font-weight:500;color:var(--color-text-primary);background:var(--color-background-primary);text-align:center" placeholder="${ex.targetWeight?.replace(/[^0-9.]/g,'')||''}" /></div><div><div style="font-size:12px;color:var(--color-text-secondary);margin-bottom:6px">Reps completed</div><input type="number" id="m-r" style="width:100%;padding:10px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);font-size:22px;font-weight:500;color:var(--color-text-primary);background:var(--color-background-primary);text-align:center" placeholder="${ex.reps?.split('-')[1]||ex.reps?.split(' ')[0]||'—'}" /></div></div><div style="display:flex;gap:5px;margin-bottom:1rem">${rpes.map((l,i)=>`<button style="flex:1;padding:7px 3px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);font-size:11px;font-weight:500;cursor:pointer;background:${rpe===i?'#1a1a1a':'transparent'};color:${rpe===i?'#fff':'var(--color-text-secondary)'}" onclick="rpe=${i};renderModal()">${l}</button>`).join('')}</div><textarea id="m-notes" style="width:100%;padding:9px 12px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);font-size:13px;color:var(--color-text-primary);background:var(--color-background-primary);resize:none;font-family:var(--font-sans)" rows="2" placeholder="Notes..."></textarea></div><div style="display:grid;grid-template-columns:1fr 2fr;gap:8px;padding:0 1.25rem 1.25rem"><button style="padding:11px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);background:transparent;font-size:13px;font-weight:500;color:var(--color-text-primary);cursor:pointer" onclick="closeModal()">Cancel</button><button style="padding:11px;border-radius:var(--border-radius-md);border:none;background:#1a1a1a;color:#fff;font-size:13px;font-weight:500;cursor:pointer" onclick="saveSet()">Save set ${nextSet} →</button></div></div></div>`;
  setTimeout(()=>document.getElementById('m-w')?.focus(),80);
}

function saveSet(){
  if(!modalCtx)return;
  const{sk,exIdx}=modalCtx;
  const wk=ST.programme.weeks.find(w=>w.week===ST.week)||ST.programme.weeks[0];
  const ex=wk?.days[viewDayIdx]?.exercises[exIdx];if(!ex)return;
  const w=parseFloat(document.getElementById('m-w')?.value)||0;
  const r=parseInt(document.getElementById('m-r')?.value)||0;
  const notes=document.getElementById('m-notes')?.value||'';
  if(!ST.loggedSets[sk])ST.loggedSets[sk]={};
  if(!ST.loggedSets[sk][exIdx])ST.loggedSets[sk][exIdx]=[];
  ST.loggedSets[sk][exIdx].push({w,r,rpe,notes,ts:Date.now()});
  ST.totalSets++;
  if(w>0&&w>(ST.pbs[ex.name]||0))ST.pbs[ex.name]=w;
  const isLast=ST.loggedSets[sk][exIdx].length>=ex.sets;
  closeModal();renderSession();updateHeader();save();
  if(!isLast)startTimer();
}

function startTimer(){if(timerInt)clearInterval(timerInt);timerSecs=90;timerInt=setInterval(()=>{timerSecs--;renderTimer();if(timerSecs<=0){clearInterval(timerInt);timerInt=null;timerSecs=0;renderTimer();}},1000);renderTimer();}
function skipTimer(){if(timerInt)clearInterval(timerInt);timerInt=null;timerSecs=0;renderTimer();}
function renderTimer(){
  const z=document.getElementById('t-timer');if(!z)return;
  if(!timerInt&&timerSecs===0){z.innerHTML='';return;}
  const pct=timerSecs/90;const circ=2*Math.PI*16;const off=circ*(1-pct);
  const col=timerSecs<=10?'#E24B4A':timerSecs<=30?'#EF9F27':'#1a1a1a';
  const m=Math.floor(timerSecs/60);const s=timerSecs%60;const ts=m>0?`${m}:${String(s).padStart(2,'0')}`:`${timerSecs}s`;
  z.innerHTML=`<div class="timer-bar"><div class="timer-ring"><svg width="40" height="40" viewBox="0 0 40 40"><circle cx="20" cy="20" r="16" fill="none" stroke="var(--color-border-tertiary)" stroke-width="2.5"/><circle cx="20" cy="20" r="16" fill="none" stroke="${col}" stroke-width="2.5" stroke-dasharray="${circ.toFixed(1)}" stroke-dashoffset="${off.toFixed(1)}" stroke-linecap="round" style="transition:stroke-dashoffset .9s linear"/></svg><div class="timer-inner" style="color:${timerSecs<=10?'#A32D2D':timerSecs<=30?'#633806':'var(--color-text-primary)'}">${ts}</div></div><div style="flex:1"><div style="font-size:13px;font-weight:500;color:var(--color-text-primary)">Rest period</div><div style="font-size:11px;color:var(--color-text-secondary)">Next set when ready</div></div><button style="padding:4px 10px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);background:transparent;font-size:12px;color:var(--color-text-secondary);cursor:pointer" onclick="skipTimer()">Skip</button></div>`;
}

function setPW(w,btn){progWeek=w;document.querySelectorAll('.wk-btn').forEach(b=>b.classList.remove('active'));btn.classList.add('active');renderProg();}

function renderProg(){
  if(!ST.programme)return;
  const sLabel=STRUCTURES.find(s=>s.id===P.structure)?.label||P.structure;
  document.getElementById('p-title').textContent=ST.programme.programmeTitle||'Programme';
  document.getElementById('p-sub').textContent=`Block ${ST.block} · ${sLabel}`;
  const wk=ST.programme.weeks.find(w=>w.week===progWeek)||ST.programme.weeks[0];
  const c=document.getElementById('p-content');
  c.innerHTML=(wk?.days||[]).map(day=>{
    if(day.isRest)return`<div class="day-card"><div class="day-head" style="cursor:default"><div style="font-size:14px;font-weight:500;color:var(--color-text-primary)">${day.day}</div><span style="background:var(--color-background-primary);color:var(--color-text-secondary);padding:2px 8px;border-radius:10px;font-size:11px">Rest</span></div></div>`;
    const exRows=(day.exercises||[]).map((ex,i)=>`<div class="ex-row-ai"><div class="ex-num">${i+1}</div><div style="flex:1"><div style="font-size:13px;font-weight:500;color:var(--color-text-primary)">${ex.name}</div><div style="font-size:12px;color:var(--color-text-secondary);margin-top:2px">${ex.sets}×${ex.reps} · ${ex.targetWeight}${ex.notes?' · <em>'+ex.notes+'</em>':''}</div></div></div>`).join('');
    const fin=day.finisher?`<div class="finisher-card" style="margin:0;margin-top:.75rem"><div class="finisher-title">⚡ Finisher</div><div class="finisher-item">${day.finisher}</div></div>`:'';
    return`<div class="day-card"><div class="day-head"><div><div style="font-size:14px;font-weight:500;color:var(--color-text-primary)">${day.day}</div><div style="font-size:12px;color:var(--color-text-secondary);margin-top:2px">${day.sessionType} · ${day.duration} · ${(day.exercises||[]).length} exercises</div></div><span style="background:#E6F1FB;color:#0C447C;padding:2px 8px;border-radius:10px;font-size:11px;font-weight:500">${day.sessionType}</span></div><div class="day-body">${exRows}${fin}</div></div>`;
  }).join('');
  if(ST.programme.phantomNotes?.length)c.innerHTML+=`<div class="card"><div class="card-head"><div class="card-title">⚡ Phantom notes</div></div>${ST.programme.phantomNotes.map(n=>`<div style="padding:8px 1.25rem;border-bottom:0.5px solid var(--color-border-tertiary);font-size:13px;color:var(--color-text-primary);line-height:1.5">${n}</div>`).join('')}</div>`;
}

function renderProgress(){
  const vol=Object.values(ST.loggedSets).flatMap(d=>Object.values(d).flat()).reduce((a,s)=>a+(s.w*s.r),0);
  document.getElementById('pr-sets').textContent=ST.totalSets;
  document.getElementById('pr-vol').innerHTML=Math.round(vol)+'<span style="font-size:11px">kg</span>';
  document.getElementById('pr-pbs').textContent=Object.keys(ST.pbs).length;
  document.getElementById('pr-sess').textContent=ST.totalSessions;
  document.getElementById('pr-sub').textContent=`Block ${ST.block} · Week ${ST.week} of 4`;
  const list=document.getElementById('pr-pblist');
  const entries=Object.entries(ST.pbs);
  list.innerHTML=entries.length?entries.map(([n,w])=>`<div style="display:flex;align-items:center;justify-content:space-between;padding:9px 1.25rem;border-bottom:0.5px solid var(--color-border-tertiary)"><div style="font-size:13px;font-weight:500;color:var(--color-text-primary)">${n}</div><div style="font-size:13px;font-weight:500;color:#3C3489">${w}kg <span style="background:#EEEDFE;color:#3C3489;padding:1px 6px;border-radius:10px;font-size:10px">PB</span></div></div>`).join(''):`<div style="padding:1rem 1.25rem;font-size:13px;color:var(--color-text-secondary)">No PBs yet — log sets to track your bests.</div>`;
}

function renderProfileTab(){
  const equips=['Full gym','Dumbbells','Bench','Pull-up bar','Barbell','Cable machine','Resistance bands','Dip bar','Treadmill','Rower'];
  const injList=['Shoulder','Lower back','Knee','Hip','Wrist','Elbow','Ankle','None'];
  const SK=DAYS_SHORT;
  document.getElementById('pf-editable').innerHTML=`<div class="card" style="padding:1.25rem"><div class="section-label">Programme type</div><div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:1.25rem" id="pf-type">${['Strength','Physique','Fitness','Hobby'].map(t=>chip(t,P.type===t,`P.type='${t}';soloChip(this,'pf-type')`)).join('')}</div><div class="section-label">Primary goal</div><div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:1.25rem" id="pf-goal">${['Muscle gain','Fat loss','Recomposition','Strength gains','General fitness'].map(g=>chip(g,P.goal===g,`P.goal='${g}';soloChip(this,'pf-goal')`)).join('')}</div><div class="section-label">Experience</div><div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:1.25rem" id="pf-exp">${[['Novice','0–6 months'],['Intermediate','6–24 months'],['Experienced','24+ months']].map(([e,d])=>chip(`${e} <span style="font-size:11px;opacity:.6">${d}</span>`,P.exp===e,`P.exp='${e}';soloChip(this,'pf-exp')`)).join('')}</div></div><div class="card" style="padding:1.25rem"><div class="section-label">Programme structure</div><div id="pf-structs">${STRUCTURES.map(s=>structCard(s,P.structure===s.id)).join('')}</div></div><div class="card" style="padding:1.25rem"><div class="section-label">About you</div><div class="stat-grid-2"><div class="stat-card"><div class="stat-lbl">Age</div><input type="number" class="stat-inp" value="${P.age}" oninput="P.age=parseInt(this.value)||P.age" /><div class="stat-unit">years</div></div><div class="stat-card"><div class="stat-lbl">Weight</div><input type="number" class="stat-inp" value="${P.weight}" oninput="P.weight=parseFloat(this.value)||P.weight" /><div class="stat-unit">kg</div></div><div class="stat-card"><div class="stat-lbl">Height</div><input type="number" class="stat-inp" value="${P.height}" oninput="P.height=parseInt(this.value)||P.height" /><div class="stat-unit">cm</div></div><div class="stat-card"><div class="stat-lbl">Sex</div><select class="stat-sel" onchange="P.sex=this.value"><option ${P.sex==='Male'?'selected':''}>Male</option><option ${P.sex==='Female'?'selected':''}>Female</option><option ${P.sex==='Other'?'selected':''}>Other</option></select><div class="stat-unit">—</div></div></div></div><div class="card" style="padding:1.25rem"><div class="section-label">Training days</div><div class="days-grid">${SK.map(sk=>`<div class="day-chip ${P.days[sk]?'active':''}" onclick="P.days['${sk}']=!P.days['${sk}'];this.classList.toggle('active')">${sk}<div class="day-tk"><i class="ti ti-check"></i></div></div>`).join('')}</div><div class="range-block"><div class="range-header"><span class="range-label">Session length</span><span class="range-val" id="pf-tv">${P.time} min</span></div><div class="range-row"><span>20m</span><input type="range" min="20" max="120" step="5" value="${P.time}" oninput="P.time=parseInt(this.value);document.getElementById('pf-tv').textContent=this.value+' min'" /><span>2hr</span></div></div><div class="section-label">Rest periods</div><div style="display:flex;flex-wrap:wrap;gap:8px" id="pf-rest">${['Short (30–60s)','Medium (60–90s)','Long (2–3 min)'].map(r=>chip(r,P.rest===r,`P.rest='${r}';soloChip(this,'pf-rest')`)).join('')}</div></div><div class="card" style="padding:1.25rem"><div class="section-label">Equipment available</div><div style="display:flex;flex-wrap:wrap;gap:8px;margin-bottom:1.25rem">${equips.map(e=>chip(e,P.equip.includes(e),`toggleArr(P.equip,'${e}');this.classList.toggle('active')`)).join('')}</div><div class="section-label">Injuries or areas to avoid</div><div class="section-hint">Ticked areas are avoided in exercise selection</div><div style="display:flex;flex-wrap:wrap;gap:8px">${injList.map(inj=>warnChip(inj,P.injuries.includes(inj),`toggleArr(P.injuries,'${inj}');this.classList.toggle('active')`)).join('')}</div></div><div class="card" style="padding:0 1.25rem"><div class="toggle-row"><div><div style="font-size:14px;color:var(--color-text-primary)">Daily finisher</div><div style="font-size:12px;color:var(--color-text-secondary);margin-top:2px">End each session with a short high-intensity finisher</div></div><label class="toggle"><input type="checkbox" checked /><span class="toggle-slider"></span></label></div><div class="toggle-row"><div><div style="font-size:14px;color:var(--color-text-primary)">Week 4 progress day</div><div style="font-size:12px;color:var(--color-text-secondary);margin-top:2px">Max effort test to calibrate your next block</div></div><label class="toggle"><input type="checkbox" checked /><span class="toggle-slider"></span></label></div><div class="toggle-row"><div><div style="font-size:14px;color:var(--color-text-primary)">Progressive overload targets</div><div style="font-size:12px;color:var(--color-text-secondary);margin-top:2px">Phantom auto-calculates weekly weight targets</div></div><label class="toggle"><input type="checkbox" checked /><span class="toggle-slider"></span></label></div></div><button style="width:100%;padding:13px;border-radius:var(--border-radius-md);border:none;background:#1a1a1a;color:#fff;font-size:14px;font-weight:500;cursor:pointer;margin-top:.5rem" onclick="saveAndRegen()">↺ Save & regenerate programme</button>`;
}

function saveAndRegen(){ST.onboarded=false;ST.programme=null;ST.loggedSets={};ST.week=1;ST.totalSessions=0;save();document.getElementById('screen-app').classList.remove('visible');document.getElementById('screen-ob').classList.add('visible');obStep=8;renderOB();}

function fullReset(){if(!confirm('Reset everything and start fresh?'))return;localStorage.removeItem(STORAGE_KEY);ST={loggedSets:{},pbs:{},totalSets:0,totalSessions:0,block:1,week:1,onboarded:false,programme:null,apiKey:''};P={name:'',type:'Strength',structure:'PPL_UL',goal:'Muscle gain',exp:'Intermediate',age:30,weight:80,height:178,sex:'Male',days:{Mon:true,Tue:false,Wed:true,Thu:false,Fri:true,Sat:true,Sun:false},time:60,equip:[],injuries:[],rest:'Medium'};obStep=0;document.getElementById('screen-app').classList.remove('visible');document.getElementById('screen-ob').classList.add('visible');renderOB();}

loadState();
</script>
</body>
</html>
