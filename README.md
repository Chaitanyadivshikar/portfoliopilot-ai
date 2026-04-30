<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PortfolioPilot AI — Intelligent Portfolio Analysis</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,400&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
:root{
--navy:#07091A;--navy2:#0D1028;--navy3:#141737;--card:#161A3A;--card2:#1C2145;
--border:#252A55;--border2:#2E3460;
--emerald:#00D4A0;--emerald2:#00F0B5;--eg:rgba(0,212,160,.12);--eg2:rgba(0,212,160,.25);
--gold:#F0B429;--gold2:#FFD166;--gdim:rgba(240,180,41,.12);
--red:#FF5B5B;--rdim:rgba(255,91,91,.12);
--blue:#4E9EFF;--bdim:rgba(78,158,255,.12);
--purple:#B47EFF;--pdim:rgba(180,126,255,.12);
--text:#E8EAF6;--text2:#9BA3C8;--text3:#5A6290;
--ff:'Syne',sans-serif;--fb:'DM Sans',sans-serif;--fm:'DM Mono',monospace;
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{background:var(--navy);color:var(--text);font-family:var(--fb);font-size:15px;line-height:1.6;overflow-x:hidden}
nav{position:sticky;top:0;z-index:100;background:rgba(7,9,26,.9);backdrop-filter:blur(20px);border-bottom:1px solid var(--border);padding:0 5vw;display:flex;align-items:center;justify-content:space-between;height:62px}
.logo{font-family:var(--ff);font-size:19px;font-weight:800;display:flex;align-items:center;gap:9px}
.logo-icon{width:30px;height:30px;border-radius:8px;background:linear-gradient(135deg,var(--emerald),#009b75);display:grid;place-items:center;font-size:12px;font-weight:800;color:#07091A}
.nav-links{display:flex;gap:24px;align-items:center}
.nav-links a{color:var(--text2);text-decoration:none;font-size:14px;transition:.2s}
.nav-links a:hover{color:var(--emerald)}
.nav-cta{background:var(--emerald);color:#07091A;border:none;padding:8px 18px;border-radius:6px;font-family:var(--fb);font-size:14px;font-weight:500;cursor:pointer;transition:.2s}
.nav-cta:hover{background:var(--emerald2)}
.hero{padding:90px 5vw 70px;text-align:center;position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;top:-180px;left:50%;transform:translateX(-50%);width:700px;height:700px;background:radial-gradient(circle,rgba(0,212,160,.07) 0%,transparent 70%);pointer-events:none}
.badge{display:inline-flex;align-items:center;gap:7px;background:var(--eg);border:1px solid rgba(0,212,160,.35);border-radius:99px;padding:5px 14px;font-size:11.5px;font-weight:600;color:var(--emerald);letter-spacing:.8px;text-transform:uppercase;margin-bottom:26px}
.badge-dot{width:6px;height:6px;border-radius:50%;background:var(--emerald);animation:pulse 2s infinite}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.4;transform:scale(1.5)}}
h1{font-family:var(--ff);font-size:clamp(38px,5.5vw,68px);font-weight:800;line-height:1.08;letter-spacing:-2px;margin-bottom:18px;max-width:800px;margin-left:auto;margin-right:auto}
h1 span{background:linear-gradient(90deg,var(--emerald),var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.hero-sub{font-size:17px;color:var(--text2);max-width:560px;margin:0 auto 36px;font-weight:300;line-height:1.75}
.hero-btns{display:flex;gap:12px;justify-content:center;flex-wrap:wrap}
.btn-primary{background:var(--emerald);color:#07091A;border:none;padding:13px 30px;border-radius:8px;font-family:var(--fb);font-size:15px;font-weight:600;cursor:pointer;transition:.2s}
.btn-primary:hover{background:var(--emerald2);transform:translateY(-2px);box-shadow:0 8px 28px rgba(0,212,160,.3)}
.btn-secondary{background:transparent;color:var(--text);border:1px solid var(--border2);padding:13px 30px;border-radius:8px;font-family:var(--fb);font-size:15px;cursor:pointer;transition:.2s}
.btn-secondary:hover{border-color:var(--emerald);color:var(--emerald)}
.hero-stats{display:flex;gap:36px;justify-content:center;margin-top:52px;flex-wrap:wrap}
.hero-stat .num{font-family:var(--ff);font-size:28px;font-weight:700;color:var(--emerald)}
.hero-stat .lbl{font-size:12px;color:var(--text3);margin-top:2px}
.features{padding:56px 5vw;border-top:1px solid var(--border)}
.section-label{font-size:11px;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;color:var(--emerald);margin-bottom:10px}
.section-title{font-family:var(--ff);font-size:clamp(24px,3vw,36px);font-weight:700;letter-spacing:-1px;margin-bottom:36px}
.features-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(230px,1fr));gap:14px}
.feature-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:22px;transition:.25s}
.feature-card:hover{border-color:var(--border2);transform:translateY(-2px)}
.feat-icon{width:38px;height:38px;border-radius:9px;display:grid;place-items:center;font-size:16px;margin-bottom:13px}
.fi-g{background:var(--eg)}.fi-b{background:var(--bdim)}.fi-y{background:var(--gdim)}.fi-r{background:var(--rdim)}.fi-p{background:var(--pdim)}
.feature-card h3{font-family:var(--ff);font-size:14.5px;font-weight:600;margin-bottom:5px}
.feature-card p{font-size:12.5px;color:var(--text2);line-height:1.5}
/* RISK SELECTOR */
.form-section{padding:56px 5vw;background:var(--navy2);border-top:1px solid var(--border)}
.form-wrap{max-width:940px;margin:0 auto}
.step-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:22px;margin-bottom:14px}
.step-label{font-size:11px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--text3);margin-bottom:6px}
.step-title{font-family:var(--ff);font-size:16px;font-weight:700;color:var(--text);margin-bottom:4px}
.step-sub{font-size:13px;color:var(--text2);margin-bottom:18px}
.risk-cards{display:grid;grid-template-columns:repeat(4,1fr);gap:10px}
@media(max-width:640px){.risk-cards{grid-template-columns:1fr 1fr}}
.risk-card{border:1.5px solid var(--border);border-radius:10px;padding:14px 12px;cursor:pointer;transition:.2s;text-align:center;background:var(--navy3);position:relative}
.risk-card:hover{border-color:var(--border2);transform:translateY(-1px)}
.risk-card.selected{background:var(--navy2)}
.risk-card.selected.rc-cons{border-color:var(--emerald);box-shadow:0 0 0 1px var(--emerald),0 4px 20px rgba(0,212,160,.15)}
.risk-card.selected.rc-mod{border-color:var(--blue);box-shadow:0 0 0 1px var(--blue),0 4px 20px rgba(78,158,255,.15)}
.risk-card.selected.rc-agg{border-color:var(--gold);box-shadow:0 0 0 1px var(--gold),0 4px 20px rgba(240,180,41,.15)}
.risk-card.selected.rc-spc{border-color:var(--red);box-shadow:0 0 0 1px var(--red),0 4px 20px rgba(255,91,91,.15)}
.risk-card .rc-icon{font-size:22px;margin-bottom:8px}
.risk-card .rc-name{font-family:var(--ff);font-size:13px;font-weight:700;margin-bottom:4px}
.risk-card .rc-desc{font-size:10.5px;color:var(--text2);line-height:1.4}
.risk-card .rc-check{position:absolute;top:8px;right:8px;width:16px;height:16px;border-radius:50%;display:none;align-items:center;justify-content:center;font-size:9px;font-weight:700}
.risk-card.selected .rc-check{display:flex}
.rc-cons .rc-name{color:var(--emerald)}
.rc-mod .rc-name{color:var(--blue)}
.rc-agg .rc-name{color:var(--gold)}
.rc-spc .rc-name{color:var(--red)}
.rc-cons.selected .rc-check{background:var(--emerald);color:#07091A}
.rc-mod.selected .rc-check{background:var(--blue);color:#fff}
.rc-agg.selected .rc-check{background:var(--gold);color:#07091A}
.rc-spc.selected .rc-check{background:var(--red);color:#fff}
/* HOLDINGS TABLE */
table.holdings{width:100%;border-collapse:collapse;font-size:14px}
table.holdings th{text-align:left;padding:9px 12px;font-size:11px;font-weight:500;color:var(--text3);letter-spacing:.5px;text-transform:uppercase;border-bottom:1px solid var(--border)}
table.holdings td{padding:7px 10px;border-bottom:1px solid var(--border)}
table.holdings td input,table.holdings td select{width:100%;background:var(--navy3);border:1px solid var(--border);border-radius:6px;color:var(--text);padding:7px 9px;font-family:var(--fb);font-size:13.5px;outline:none;transition:.2s}
table.holdings td input:focus,table.holdings td select:focus{border-color:var(--emerald);box-shadow:0 0 0 2px rgba(0,212,160,.12)}
.remove-btn{background:transparent;border:none;color:var(--text3);cursor:pointer;font-size:15px;padding:4px 8px;border-radius:4px;transition:.2s}
.remove-btn:hover{color:var(--red);background:var(--rdim)}
.form-actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:16px;align-items:center}
.add-row-btn{background:transparent;border:1px dashed var(--border2);color:var(--text2);padding:8px 16px;border-radius:7px;font-family:var(--fb);font-size:13px;cursor:pointer;transition:.2s}
.add-row-btn:hover{border-color:var(--emerald);color:var(--emerald)}
.demo-btn{background:var(--gdim);border:1px solid rgba(240,180,41,.4);color:var(--gold);padding:8px 16px;border-radius:7px;font-family:var(--fb);font-size:13px;cursor:pointer;transition:.2s}
.demo-btn:hover{background:var(--gold);color:#07091A}
.analyze-btn{background:var(--emerald);color:#07091A;border:none;padding:11px 28px;border-radius:8px;font-family:var(--fb);font-size:14.5px;font-weight:600;cursor:pointer;transition:.2s;margin-left:auto}
.analyze-btn:hover{background:var(--emerald2);transform:translateY(-1px);box-shadow:0 6px 22px rgba(0,212,160,.3)}
/* LOADING */
.loading{display:none;text-align:center;padding:50px}
.loading.visible{display:block}
.spinner{width:34px;height:34px;border:3px solid var(--border);border-top-color:var(--emerald);border-radius:50%;animation:spin 1s linear infinite;margin:0 auto 12px}
@keyframes spin{to{transform:rotate(360deg)}}
.load-steps{display:flex;justify-content:center;gap:20px;margin-top:16px;flex-wrap:wrap}
.load-step{font-size:12px;color:var(--text3);display:flex;align-items:center;gap:5px}
.load-step.active{color:var(--emerald)}
/* DASHBOARD */
.dashboard{display:none;padding:46px 5vw;border-top:1px solid var(--border)}
.dashboard.visible{display:block}
.dash-header{display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:14px;margin-bottom:24px}
.dash-title{font-family:var(--ff);font-size:24px;font-weight:700;letter-spacing:-.5px}
.portfolio-meta{font-size:13px;color:var(--text3);margin-top:3px}
.new-btn{background:transparent;border:1px solid var(--border2);color:var(--text2);padding:8px 16px;border-radius:7px;font-size:13.5px;cursor:pointer;transition:.2s;font-family:var(--fb)}
.new-btn:hover{border-color:var(--emerald);color:var(--emerald)}
/* BANNER */
.align-banner{border-radius:12px;padding:15px 18px;margin-bottom:16px;display:flex;align-items:center;gap:13px;font-size:14px;border:1px solid}
.align-banner .ab-icon{font-size:22px}
.align-banner strong{font-weight:600;display:block;margin-bottom:2px}
.align-banner span{color:var(--text2);font-size:13px}
.ab-match{background:rgba(0,212,160,.07);border-color:rgba(0,212,160,.25)}
.ab-low{background:rgba(78,158,255,.07);border-color:rgba(78,158,255,.25)}
.ab-high{background:rgba(255,91,91,.07);border-color:rgba(255,91,91,.25)}
/* SCORE */
.score-row{display:grid;grid-template-columns:210px 1fr;gap:14px;margin-bottom:16px;align-items:start}
@media(max-width:680px){.score-row{grid-template-columns:1fr}}
.score-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:26px;text-align:center;position:relative;overflow:hidden}
.score-card::before{content:'';position:absolute;top:-40px;left:50%;transform:translateX(-50%);width:180px;height:180px;background:radial-gradient(circle,rgba(0,212,160,.05) 0%,transparent 70%)}
.score-label{font-size:11px;font-weight:600;letter-spacing:2px;text-transform:uppercase;color:var(--text3);margin-bottom:10px}
.score-ring{position:relative;width:124px;height:124px;margin:0 auto 12px}
.score-ring svg{transform:rotate(-90deg)}
.score-num{position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);font-family:var(--ff);font-size:32px;font-weight:800;color:var(--emerald);line-height:1}
.score-sub2{font-size:10px;color:var(--text3);position:absolute;bottom:20px;left:50%;transform:translateX(-50%);white-space:nowrap}
.score-grade{display:inline-block;font-family:var(--ff);font-size:12px;font-weight:600;padding:4px 12px;border-radius:99px;background:var(--eg);color:var(--emerald);border:1px solid rgba(0,212,160,.3)}
.metrics-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
@media(max-width:580px){.metrics-grid{grid-template-columns:1fr 1fr}}
.metric{background:var(--card2);border:1px solid var(--border);border-radius:8px;padding:14px 16px}
.metric .m-label{font-size:10.5px;color:var(--text3);letter-spacing:.5px;text-transform:uppercase;margin-bottom:5px}
.metric .m-val{font-family:var(--ff);font-size:18px;font-weight:700;line-height:1.1}
.metric .m-sub{font-size:11.5px;color:var(--text2);margin-top:3px}
.metric.green .m-val{color:var(--emerald)}.metric.gold .m-val{color:var(--gold)}.metric.red .m-val{color:var(--red)}.metric.blue .m-val{color:var(--blue)}
/* CHARTS */
.charts-row{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-bottom:16px}
@media(max-width:680px){.charts-row{grid-template-columns:1fr}}
.chart-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px}
.chart-card h3{font-family:var(--ff);font-size:13.5px;font-weight:600;margin-bottom:3px}
.ch-sub{font-size:11.5px;color:var(--text3);margin-bottom:14px}
.legend{display:flex;flex-wrap:wrap;gap:8px;margin-top:12px}
.legend-item{display:flex;align-items:center;gap:5px;font-size:11.5px;color:var(--text2)}
.legend-dot{width:9px;height:9px;border-radius:2px;flex-shrink:0}
.gauge-wrap{display:flex;flex-direction:column;align-items:center}
.prog-bar-row{display:flex;align-items:center;gap:8px;margin-bottom:7px}
.prog-label{font-size:12.5px;color:var(--text2);width:120px;flex-shrink:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.prog-track{flex:1;height:5px;border-radius:3px;background:var(--navy3);overflow:hidden}
.prog-fill{height:100%;border-radius:3px;transition:width .7s ease}
.prog-pct{font-size:11.5px;color:var(--text3);width:36px;text-align:right;font-family:var(--fm)}
/* SCORE BREAKDOWN */
.breakdown-section{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px;margin-bottom:16px}
.breakdown-section h3{font-family:var(--ff);font-size:13.5px;font-weight:600;margin-bottom:14px}
.score-breakdown{display:grid;grid-template-columns:repeat(2,1fr);gap:12px}
@media(max-width:560px){.score-breakdown{grid-template-columns:1fr}}
.sb-item{background:var(--navy3);border:1px solid var(--border);border-radius:8px;padding:14px}
.sb-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px}
.sb-title{font-size:12.5px;font-weight:600;color:var(--text)}
.sb-score{font-family:var(--fm);font-size:13px;font-weight:500}
.sb-bar-track{height:4px;border-radius:2px;background:var(--navy2);overflow:hidden;margin-bottom:6px}
.sb-bar-fill{height:100%;border-radius:2px;transition:width .8s ease}
.sb-desc{font-size:11px;color:var(--text3);line-height:1.4}
/* RECO */
.reco-section{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px;margin-bottom:16px}
.reco-section h3{font-family:var(--ff);font-size:13.5px;font-weight:600;margin-bottom:3px}
.reco-section .sub{font-size:11.5px;color:var(--text3);margin-bottom:14px}
table.reco{width:100%;border-collapse:collapse;font-size:13px}
table.reco th{text-align:left;padding:8px 11px;font-size:10.5px;font-weight:500;color:var(--text3);letter-spacing:.5px;text-transform:uppercase;border-bottom:1px solid var(--border)}
table.reco td{padding:9px 11px;border-bottom:1px solid rgba(37,42,85,.5)}
table.reco tr:last-child td{border-bottom:none}
table.reco tr:hover td{background:rgba(20,23,55,.6)}
.sig-tag{display:inline-block;font-size:10.5px;font-weight:700;padding:2px 9px;border-radius:99px;letter-spacing:.3px}
.sig-buy{background:rgba(0,212,160,.14);color:var(--emerald);border:1px solid rgba(0,212,160,.25)}
.sig-hold{background:rgba(78,158,255,.14);color:var(--blue);border:1px solid rgba(78,158,255,.25)}
.sig-sell{background:rgba(255,91,91,.14);color:var(--red);border:1px solid rgba(255,91,91,.25)}
.sig-reduce{background:rgba(240,180,41,.14);color:var(--gold);border:1px solid rgba(240,180,41,.25)}
/* ALERTS */
.alerts-section{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px;margin-bottom:16px}
.alerts-section h3{font-family:var(--ff);font-size:13.5px;font-weight:600;margin-bottom:14px}
.alert-item{display:flex;gap:11px;align-items:flex-start;padding:11px 13px;border-radius:8px;margin-bottom:7px;font-size:13px}
.alert-item:last-child{margin-bottom:0}
.alert-warn{background:rgba(240,180,41,.07);border:1px solid rgba(240,180,41,.2)}
.alert-info{background:rgba(78,158,255,.07);border:1px solid rgba(78,158,255,.2)}
.alert-success{background:rgba(0,212,160,.07);border:1px solid rgba(0,212,160,.2)}
.alert-err{background:rgba(255,91,91,.07);border:1px solid rgba(255,91,91,.2)}
.alert-icon{font-size:14px;margin-top:1px}
.alert-text strong{display:block;font-weight:500;margin-bottom:1px}
.alert-text span{color:var(--text2);font-size:12px}
/* REBALANCING */
.rebal-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
@media(max-width:580px){.rebal-grid{grid-template-columns:1fr}}
.rebal-item{background:var(--navy3);border:1px solid var(--border);border-radius:8px;padding:13px}
.rebal-item .r-ticker{font-family:var(--fm);font-size:12.5px;font-weight:500;margin-bottom:3px}
.rebal-item .r-action{font-size:10.5px;font-weight:700;letter-spacing:.3px}
.rebal-item .r-reason{font-size:11.5px;color:var(--text2);margin-top:3px;line-height:1.4}
.r-buy{color:var(--emerald)}.r-sell{color:var(--red)}.r-trim{color:var(--gold)}.r-hold{color:var(--blue)}
/* BUY RECOMMENDATIONS */
.buy-reco{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px;margin-bottom:16px}
.buy-reco h3{font-family:var(--ff);font-size:13.5px;font-weight:600;margin-bottom:3px}
.buy-reco .sub{font-size:11.5px;color:var(--text3);margin-bottom:16px}
.buy-reco-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(210px,1fr));gap:10px}
.buy-card{background:var(--navy3);border:1px solid var(--border);border-radius:10px;padding:14px;transition:.2s;position:relative;overflow:hidden}
.buy-card::before{content:'';position:absolute;top:0;left:0;width:3px;height:100%}
.buy-card:hover{border-color:var(--border2);transform:translateY(-1px)}
.bc-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:6px}
.bc-ticker{font-family:var(--fm);font-size:14px;font-weight:500}
.bc-badge{font-size:10px;font-weight:600;padding:2px 7px;border-radius:99px;border:1px solid}
.bc-name{font-size:12.5px;color:var(--text);font-weight:500;margin-bottom:2px}
.bc-sector{font-size:11px;color:var(--text3);margin-bottom:6px}
.bc-reason{font-size:11.5px;color:var(--text2);line-height:1.4;margin-bottom:8px}
.bc-metrics{display:flex;gap:12px}
.bc-met .bm-label{font-size:10px;color:var(--text3)}
.bc-met .bm-val{font-family:var(--fm);font-size:11px;color:var(--text2)}
.buy-card.cons::before{background:var(--emerald)}
.buy-card.mod::before{background:var(--blue)}
.buy-card.agg::before{background:var(--gold)}
.buy-card.spc::before{background:var(--red)}
.bc-badge.cons{color:var(--emerald);border-color:rgba(0,212,160,.3)}
.bc-badge.mod{color:var(--blue);border-color:rgba(78,158,255,.3)}
.bc-badge.agg{color:var(--gold);border-color:rgba(240,180,41,.3)}
.bc-badge.spc{color:var(--red);border-color:rgba(255,91,91,.3)}
/* DISCLAIMER */
.disclaimer{background:var(--navy2);border-top:1px solid var(--border);padding:28px 5vw;text-align:center}
.disclaimer p{font-size:11.5px;color:var(--text3);max-width:700px;margin:0 auto;line-height:1.7}
.disclaimer strong{color:var(--text2);font-weight:500}
@keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
.fade-up{animation:fadeUp .5s ease forwards}
.d1{animation-delay:.07s;opacity:0}.d2{animation-delay:.14s;opacity:0}
.d3{animation-delay:.21s;opacity:0}.d4{animation-delay:.28s;opacity:0}
</style>
</head>
<body>

<nav>
  <div class="logo"><div class="logo-icon">PP</div>PortfolioPilot <span style="color:var(--emerald);margin-left:2px">AI</span></div>
  <div class="nav-links">
    <a href="#features">Features</a><a href="#analyze">Analyze</a><a href="#disclaimer">Disclaimer</a>
    <button class="nav-cta" onclick="document.getElementById('analyze').scrollIntoView({behavior:'smooth'})">Try Free →</button>
  </div>
</nav>

<section class="hero fade-up">
  <div class="badge"><span class="badge-dot"></span>Rule-Based AI Portfolio Assistant · v2.0 with Risk Appetite</div>
  <h1>Your Portfolio.<br><span>Intelligently Scored.</span></h1>
  <p class="hero-sub">Enter your holdings and risk appetite — get a personalized AI score, Buy/Hold/Sell signals, stock recommendations matched to your profile, and a full rebalancing plan.</p>
  <div class="hero-btns">
    <button class="btn-primary" onclick="loadDemo();document.getElementById('analyze').scrollIntoView({behavior:'smooth'})">Try Demo Portfolio →</button>
    <button class="btn-secondary" onclick="document.getElementById('analyze').scrollIntoView({behavior:'smooth'})">Build Your Own</button>
  </div>
  <div class="hero-stats">
    <div class="hero-stat"><div class="num">100</div><div class="lbl">Portfolio Score</div></div>
    <div class="hero-stat"><div class="num">4</div><div class="lbl">Risk Profiles</div></div>
    <div class="hero-stat"><div class="num">32+</div><div class="lbl">Stock Suggestions</div></div>
    <div class="hero-stat"><div class="num">&lt;2s</div><div class="lbl">Analysis Time</div></div>
  </div>
</section>

<section class="features" id="features">
  <div class="section-label">Capabilities</div>
  <div class="section-title fade-up">Eight signals. One personalized dashboard.</div>
  <div class="features-grid">
    <div class="feature-card fade-up d1"><div class="feat-icon fi-g">📊</div><h3>AI Portfolio Score</h3><p>Composite 0–100 grade from 4 sub-scores: diversification, risk balance, sector coverage, and concentration.</p></div>
    <div class="feature-card fade-up d2"><div class="feat-icon fi-p">🎯</div><h3>Risk Appetite Input</h3><p>Select Conservative, Moderate, Aggressive, or Speculative — every insight adapts to your stated comfort level.</p></div>
    <div class="feature-card fade-up d3"><div class="feat-icon fi-b">⚖️</div><h3>Buy / Hold / Sell</h3><p>Position-level signals calibrated to your risk appetite, not just generic allocation rules.</p></div>
    <div class="feature-card fade-up d4"><div class="feat-icon fi-g">💡</div><h3>Stock Recommendations</h3><p>Curated buy suggestions matched to your exact risk profile — tickers, rationale, yield, and risk rating.</p></div>
    <div class="feature-card fade-up d1"><div class="feat-icon fi-y">🔔</div><h3>Concentration Alerts</h3><p>Context-aware flags — severity adjusts based on your risk appetite and portfolio structure.</p></div>
    <div class="feature-card fade-up d2"><div class="feat-icon fi-r">🗺️</div><h3>Sector Allocation</h3><p>Full GICS sector breakdown with bar chart and a coverage gap analysis.</p></div>
    <div class="feature-card fade-up d3"><div class="feat-icon fi-b">🔄</div><h3>Rebalancing Plan</h3><p>Trim / Buy / Hold / Sell guidance per position, weighted against your risk appetite.</p></div>
    <div class="feature-card fade-up d4"><div class="feat-icon fi-y">📐</div><h3>Score Breakdown</h3><p>See exactly how each sub-score was calculated — full transparency, no black box.</p></div>
  </div>
</section>

<section class="form-section" id="analyze">
  <div class="form-wrap">
    <div class="fade-up">
      <div class="section-label">Portfolio Analyzer</div>
      <div class="section-title" style="margin-bottom:4px">Personalized portfolio analysis</div>
      <p style="color:var(--text2);font-size:13.5px;margin-bottom:20px">Complete both steps below for a fully personalized analysis.</p>
    </div>

    <!-- STEP 1: RISK APPETITE -->
    <div class="step-card fade-up d1">
      <div class="step-label">Step 1 of 2</div>
      <div class="step-title">What is your investment risk appetite?</div>
      <div class="step-sub">This shapes your score, Buy/Sell signals, rebalancing plan, and stock recommendations.</div>
      <div class="risk-cards">
        <div class="risk-card rc-cons" onclick="selectRisk('conservative',this)">
          <div class="rc-check">✓</div>
          <div class="rc-icon">🛡️</div>
          <div class="rc-name">Conservative</div>
          <div class="rc-desc">Capital preservation. Bonds, dividends, low volatility assets.</div>
        </div>
        <div class="risk-card rc-mod" onclick="selectRisk('moderate',this)">
          <div class="rc-check">✓</div>
          <div class="rc-icon">⚖️</div>
          <div class="rc-name">Moderate</div>
          <div class="rc-desc">Balanced growth and income. Medium volatility. Long-term focus.</div>
        </div>
        <div class="risk-card rc-agg" onclick="selectRisk('aggressive',this)">
          <div class="rc-check">✓</div>
          <div class="rc-icon">🚀</div>
          <div class="rc-name">Aggressive</div>
          <div class="rc-desc">Growth-focused. High-beta stocks and sector ETFs.</div>
        </div>
        <div class="risk-card rc-spc" onclick="selectRisk('speculative',this)">
          <div class="rc-check">✓</div>
          <div class="rc-icon">⚡</div>
          <div class="rc-name">Speculative</div>
          <div class="rc-desc">Crypto, small caps, leveraged plays. Maximum risk/reward.</div>
        </div>
      </div>
    </div>

    <!-- STEP 2: HOLDINGS -->
    <div class="step-card fade-up d2">
      <div class="step-label">Step 2 of 2</div>
      <div class="step-title" style="margin-bottom:4px">Enter your current holdings</div>
      <div class="step-sub">Add at least 2 positions with a USD value. Use the demo to see a sample analysis.</div>
      <div style="overflow-x:auto">
        <table class="holdings" id="holdingsTable">
          <thead><tr><th>Ticker / Name</th><th>Sector</th><th>Asset Type</th><th>Value (USD)</th><th></th></tr></thead>
          <tbody id="holdingsBody"></tbody>
        </table>
      </div>
      <div class="form-actions">
        <button class="add-row-btn" onclick="addRow()">+ Add Holding</button>
        <button class="demo-btn" onclick="loadDemo()">★ Load Demo Portfolio</button>
        <button class="analyze-btn" onclick="runAnalysis()">Analyze Portfolio →</button>
      </div>
    </div>
  </div>
</section>

<div class="loading" id="loadingState">
  <div class="spinner"></div>
  <p style="color:var(--text2);font-size:14px;margin-bottom:14px">Running personalized portfolio analysis…</p>
  <div class="load-steps">
    <div class="load-step" id="ls1">⬤ Scoring diversification</div>
    <div class="load-step" id="ls2">⬤ Checking risk alignment</div>
    <div class="load-step" id="ls3">⬤ Matching recommendations</div>
    <div class="load-step" id="ls4">⬤ Building dashboard</div>
  </div>
</div>

<section class="dashboard" id="dashboard">
  <div class="dash-header fade-up">
    <div><div class="dash-title">Portfolio Analysis Dashboard</div><div class="portfolio-meta" id="portfolioMeta">—</div></div>
    <button class="new-btn" onclick="resetDashboard()">← New Analysis</button>
  </div>
  <div id="alignBanner" class="align-banner fade-up"></div>

  <div class="score-row fade-up d1">
    <div class="score-card">
      <div class="score-label">AI Portfolio Score</div>
      <div class="score-ring">
        <svg width="124" height="124" viewBox="0 0 124 124">
          <circle cx="62" cy="62" r="52" fill="none" stroke="#252A55" stroke-width="8"/>
          <circle id="scoreArc" cx="62" cy="62" r="52" fill="none" stroke="url(#sg)" stroke-width="8" stroke-linecap="round" stroke-dasharray="326.7" stroke-dashoffset="326.7"/>
          <defs><linearGradient id="sg" x1="0" y1="0" x2="1" y2="0"><stop offset="0%" stop-color="#00D4A0"/><stop offset="100%" stop-color="#F0B429"/></linearGradient></defs>
        </svg>
        <div class="score-num" id="scoreNum">—</div>
        <div class="score-sub2">out of 100</div>
      </div>
      <div class="score-grade" id="scoreGrade">—</div>
    </div>
    <div class="metrics-grid">
      <div class="metric blue"><div class="m-label">Risk Appetite</div><div class="m-val" id="mAppetite">—</div><div class="m-sub">Your stated goal</div></div>
      <div class="metric green"><div class="m-label">Actual Risk</div><div class="m-val" id="mActual">—</div><div class="m-sub">Based on asset mix</div></div>
      <div class="metric gold"><div class="m-label">Total Value</div><div class="m-val" id="mTotal">—</div><div class="m-sub" id="mHoldings">—</div></div>
      <div class="metric green"><div class="m-label">Diversification</div><div class="m-val" id="mDiv">—</div><div class="m-sub" id="mDivSub">HHI based</div></div>
      <div class="metric red"><div class="m-label">Largest Position</div><div class="m-val" id="mTop">—</div><div class="m-sub" id="mTopTicker">—</div></div>
      <div class="metric gold"><div class="m-label">Sectors Covered</div><div class="m-val" id="mSectors">—</div><div class="m-sub">of 10 GICS</div></div>
    </div>
  </div>

  <div class="breakdown-section fade-up d2">
    <h3>📐 Score Breakdown — How Your Score Was Built</h3>
    <div class="score-breakdown" id="scoreBreakdown"></div>
  </div>

  <div class="charts-row fade-up d3">
    <div class="chart-card">
      <h3>Allocation Breakdown</h3><p class="ch-sub">Portfolio weight by holding</p>
      <div style="height:220px"><canvas id="pieChart"></canvas></div>
      <div class="legend" id="pieLegend"></div>
    </div>
    <div class="chart-card">
      <h3>Sector Allocation</h3><p class="ch-sub">Exposure by GICS sector (%)</p>
      <div id="sectorWrap" style="height:220px"><canvas id="sectorChart"></canvas></div>
    </div>
  </div>

  <div class="charts-row fade-up d4">
    <div class="chart-card">
      <h3>Risk Gauge</h3><p class="ch-sub">Estimated portfolio volatility profile</p>
      <div class="gauge-wrap">
        <div style="height:148px;width:100%"><canvas id="gaugeChart"></canvas></div>
        <div id="gaugeLabel" style="font-family:var(--ff);font-size:15px;font-weight:700;margin-top:4px">—</div>
        <div style="font-size:12px;color:var(--text3);margin-top:2px" id="gaugeSub">—</div>
      </div>
    </div>
    <div class="chart-card">
      <h3>Holdings Weight Distribution</h3><p class="ch-sub">Position size as % of portfolio</p>
      <div id="holdingsBars"></div>
    </div>
  </div>

  <div class="reco-section fade-up d1">
    <h3>⚖️ Buy / Hold / Sell Signals</h3>
    <p class="sub" id="recoSubtitle">Signals calibrated to your risk appetite</p>
    <div style="overflow-x:auto">
      <table class="reco">
        <thead><tr><th>Ticker</th><th>Sector</th><th>Type</th><th>Weight</th><th>Signal</th><th>Rationale</th></tr></thead>
        <tbody id="recoTableBody"></tbody>
      </table>
    </div>
  </div>

  <!-- BUY RECOMMENDATIONS -->
  <div class="buy-reco fade-up d2">
    <h3>💡 Personalized Stock & Asset Recommendations</h3>
    <p class="sub" id="buyRecoSub">Curated additions matched to your risk profile and portfolio gaps</p>
    <div class="buy-reco-grid" id="buyRecoGrid"></div>
    <p style="font-size:11px;color:var(--text3);margin-top:14px;padding:10px 12px;background:var(--navy3);border-radius:7px;border:1px solid var(--border)">⚠ These suggestions are educational and rule-based. They are not financial advice. Yields and risk ratings are illustrative. Always conduct your own research and consult a licensed financial advisor before investing.</p>
  </div>

  <div class="charts-row fade-up d3">
    <div class="alerts-section" style="margin-bottom:0">
      <h3>🔔 Concentration & Risk Alerts</h3>
      <div id="alertsContainer"></div>
    </div>
    <div class="reco-section" style="margin-bottom:0">
      <h3>🔄 Rebalancing Suggestions</h3>
      <p class="sub">Tailored to your risk appetite</p>
      <div class="rebal-grid" id="rebalContainer"></div>
    </div>
  </div>
</section>

<footer class="disclaimer" id="disclaimer">
  <p><strong>⚠ Educational Use Only.</strong> PortfolioPilot AI is a student-built assistant for academic purposes. All outputs are generated by rule-based logic — not predictive AI, licensed financial advice, or market forecasting. Stock suggestions are illustrative. <strong>Do not make investment decisions based on this output.</strong> Consult a licensed financial advisor.</p>
  <p style="margin-top:8px;color:var(--text3);font-size:10.5px">PortfolioPilot AI · Simon Business School Student Project · Educational MVP · Not affiliated with any financial institution</p>
</footer>

<script>
const SECTORS=['Technology','Financials','Healthcare','Consumer Disc.','Industrials','Energy','Utilities','Real Estate','Materials','Consumer Staples'];
const COLORS=['#00D4A0','#4E9EFF','#F0B429','#FF5B5B','#B47EFF','#FF9B54','#54D6FF','#FF6B9D','#7BDD8A','#C4A96A'];
let selectedRisk=null, pieInst=null, secInst=null, gaugeInst=null;

const PROFILES={
  conservative:{label:'Conservative',color:'var(--emerald)',buys:[
    {ticker:'BND', name:'Vanguard Total Bond ETF',   type:'ETF',  sector:'Financials',      reason:'Core bond exposure — lowers portfolio beta and smooths returns.',         risk:'Low',   yield:'4.5%',cls:'cons'},
    {ticker:'VYM', name:'Vanguard High Dividend ETF',type:'ETF',  sector:'Consumer Staples',reason:'High-yield dividend ETF for stable income with lower volatility.',         risk:'Low',   yield:'3.1%',cls:'cons'},
    {ticker:'JNJ', name:'Johnson & Johnson',          type:'Stock',sector:'Healthcare',      reason:'Defensive blue chip with 60+ consecutive years of dividend growth.',       risk:'Low',   yield:'3.0%',cls:'cons'},
    {ticker:'PG',  name:'Procter & Gamble',           type:'Stock',sector:'Consumer Staples',reason:'Recession-resistant consumer staples — reliable cash flow generator.',    risk:'Low',   yield:'2.5%',cls:'cons'},
    {ticker:'NEE', name:'NextEra Energy',             type:'Stock',sector:'Utilities',       reason:'Regulated utility + renewables — predictable revenue, low beta.',          risk:'Low',   yield:'2.6%',cls:'cons'},
    {ticker:'SCHP',name:'Schwab TIPS Bond ETF',       type:'ETF',  sector:'Financials',      reason:'Inflation-protected bonds shield real purchasing power over time.',        risk:'Low',   yield:'3.8%',cls:'cons'},
    {ticker:'VNQ', name:'Vanguard REIT ETF',          type:'REIT', sector:'Real Estate',     reason:'Diversified REIT basket adds income and an inflation hedge.',              risk:'Low-Med',yield:'4.0%',cls:'cons'},
    {ticker:'MCD', name:'McDonald\'s Corp',            type:'Stock',sector:'Consumer Disc.',  reason:'Franchise model generates steady cash flow across economic cycles.',       risk:'Low',   yield:'2.3%',cls:'cons'},
  ]},
  moderate:{label:'Moderate',color:'var(--blue)',buys:[
    {ticker:'VOO', name:'Vanguard S&P 500 ETF',      type:'ETF',  sector:'Technology',      reason:'Core S&P 500 — broad diversification, low cost, proven long-term returns.',risk:'Med',   yield:'1.4%',cls:'mod'},
    {ticker:'MSFT',name:'Microsoft Corp',             type:'Stock',sector:'Technology',      reason:'Mega-cap tech with durable cloud and enterprise software moats.',           risk:'Med',   yield:'0.8%',cls:'mod'},
    {ticker:'JPM', name:'JPMorgan Chase',             type:'Stock',sector:'Financials',      reason:'Best-in-class diversified bank with strong capital returns.',               risk:'Med',   yield:'2.4%',cls:'mod'},
    {ticker:'VEA', name:'Vanguard Developed Markets',type:'ETF',  sector:'Industrials',     reason:'International equity exposure reduces US home-country concentration bias.',  risk:'Med',   yield:'3.2%',cls:'mod'},
    {ticker:'VTI', name:'Vanguard Total Market ETF', type:'ETF',  sector:'Technology',      reason:'Entire US market in one fund — maximum domestic diversification.',           risk:'Med',   yield:'1.3%',cls:'mod'},
    {ticker:'BRK.B',name:'Berkshire Hathaway B',     type:'Stock',sector:'Financials',      reason:'Diversified holding company — a portfolio within a portfolio.',              risk:'Med',   yield:'0.0%',cls:'mod'},
    {ticker:'AGG', name:'iShares Core Bond ETF',      type:'ETF',  sector:'Financials',      reason:'Investment-grade bond anchor stabilizes equity-driven volatility.',         risk:'Low',   yield:'4.3%',cls:'mod'},
    {ticker:'AAPL',name:'Apple Inc',                  type:'Stock',sector:'Technology',      reason:'Largest company by market cap — services growth + consistent buybacks.',    risk:'Med',   yield:'0.5%',cls:'mod'},
  ]},
  aggressive:{label:'Aggressive',color:'var(--gold)',buys:[
    {ticker:'QQQ', name:'Invesco Nasdaq 100 ETF',    type:'ETF',  sector:'Technology',      reason:'Pure tech growth exposure across the 100 largest Nasdaq companies.',        risk:'High',  yield:'0.6%',cls:'agg'},
    {ticker:'NVDA',name:'NVIDIA Corporation',         type:'Stock',sector:'Technology',      reason:'AI chip infrastructure leader — dominant market share in GPU compute.',     risk:'High',  yield:'0.0%',cls:'agg'},
    {ticker:'META',name:'Meta Platforms',             type:'Stock',sector:'Technology',      reason:'Social media dominance + AI + AR/VR — multiple compounding growth vectors.',risk:'Med-High',yield:'0.4%',cls:'agg'},
    {ticker:'AMZN',name:'Amazon.com Inc',             type:'Stock',sector:'Consumer Disc.',  reason:'AWS cloud growth + retail flywheel creates durable competitive advantage.',  risk:'Med-High',yield:'0.0%',cls:'agg'},
    {ticker:'TSLA',name:'Tesla Inc',                  type:'Stock',sector:'Consumer Disc.',  reason:'EV + energy storage + autonomy optionality. High beta, high upside.',       risk:'High',  yield:'0.0%',cls:'agg'},
    {ticker:'ARKK',name:'ARK Innovation ETF',         type:'ETF',  sector:'Technology',      reason:'Disruptive technology basket — genomics, AI, fintech, robotics exposure.',  risk:'High',  yield:'0.0%',cls:'agg'},
    {ticker:'XBI', name:'SPDR Biotech ETF',           type:'ETF',  sector:'Healthcare',      reason:'Biotech sector offers high asymmetric return potential with pipeline risk.',  risk:'High',  yield:'0.3%',cls:'agg'},
    {ticker:'SMCI',name:'Super Micro Computer',       type:'Stock',sector:'Technology',      reason:'AI server infrastructure beneficiary riding the data center buildout cycle.',risk:'High',  yield:'0.0%',cls:'agg'},
  ]},
  speculative:{label:'Speculative',color:'var(--red)',buys:[
    {ticker:'BTC', name:'Bitcoin',                    type:'Crypto',sector:'Technology',     reason:'Largest crypto by market cap. Digital store of value and inflation hedge.',  risk:'VeryHigh',yield:'0.0%',cls:'spc'},
    {ticker:'ETH', name:'Ethereum',                   type:'Crypto',sector:'Technology',     reason:'Smart contract platform powering DeFi and Web3 applications.',               risk:'VeryHigh',yield:'0.0%',cls:'spc'},
    {ticker:'MSTR',name:'MicroStrategy Inc',          type:'Stock',sector:'Technology',      reason:'Leveraged Bitcoin proxy — 2-3x correlated to BTC price movements.',         risk:'VeryHigh',yield:'0.0%',cls:'spc'},
    {ticker:'SOXL',name:'Direxion 3x Semis ETF',     type:'ETF',  sector:'Technology',      reason:'3x leveraged semiconductor ETF — maximum upside and downside amplification.',risk:'VeryHigh',yield:'0.0%',cls:'spc'},
    {ticker:'IONQ',name:'IonQ Inc',                   type:'Stock',sector:'Technology',      reason:'Pure-play quantum computing company. Early stage, highly speculative.',       risk:'VeryHigh',yield:'0.0%',cls:'spc'},
    {ticker:'RKLB',name:'Rocket Lab USA',             type:'Stock',sector:'Industrials',     reason:'Small-cap space economy play with growing launch cadence.',                  risk:'VeryHigh',yield:'0.0%',cls:'spc'},
    {ticker:'COIN',name:'Coinbase Global',            type:'Stock',sector:'Financials',      reason:'Crypto exchange benefits directly from surges in trading volume.',           risk:'VeryHigh',yield:'0.0%',cls:'spc'},
    {ticker:'PLTR',name:'Palantir Technologies',      type:'Stock',sector:'Technology',      reason:'AI/data analytics for government and enterprise. High growth, high multiple.',risk:'High',   yield:'0.0%',cls:'spc'},
  ]}
};

function selectRisk(profile,el){
  selectedRisk=profile;
  document.querySelectorAll('.risk-card').forEach(c=>c.classList.remove('selected'));
  el.classList.add('selected');
}

function addRow(ticker='',sector='Technology',type='Stock',value=''){
  const tb=document.getElementById('holdingsBody');
  const tr=document.createElement('tr');
  tr.innerHTML=`
    <td><input type="text" placeholder="e.g. AAPL" value="${ticker}" style="width:105px"></td>
    <td><select>${SECTORS.map(s=>`<option${s===sector?' selected':''}>${s}</option>`).join('')}</select></td>
    <td><select>${['Stock','ETF','Bond','REIT','Crypto','Cash','Mutual Fund'].map(t=>`<option${t===type?' selected':''}>${t}</option>`).join('')}</select></td>
    <td><input type="number" placeholder="e.g. 5000" min="0" value="${value}" style="width:115px"></td>
    <td><button class="remove-btn" onclick="this.closest('tr').remove()">✕</button></td>`;
  tb.appendChild(tr);
}

function loadDemo(){
  document.getElementById('holdingsBody').innerHTML='';
  [['AAPL','Technology','Stock',15000],['MSFT','Technology','Stock',12000],
   ['JPM','Financials','Stock',8000],['JNJ','Healthcare','Stock',7500],
   ['VOO','Technology','ETF',10000],['TSLA','Consumer Disc.','Stock',5000],
   ['AMZN','Consumer Disc.','Stock',8500],['BRK.B','Financials','Stock',6000],
   ['XOM','Energy','Stock',4000],['PLD','Real Estate','REIT',3000]
  ].forEach(([t,s,tp,v])=>addRow(t,s,tp,v));
  if(!selectedRisk){selectRisk('moderate',document.querySelector('.rc-mod'));}
}

function runAnalysis(){
  if(!selectedRisk){alert('Please select your risk appetite in Step 1.');return;}
  const rows=[...document.querySelectorAll('#holdingsBody tr')];
  const holdings=rows.map(r=>{
    const ins=r.querySelectorAll('input,select');
    return{ticker:(ins[0].value||'N/A').toUpperCase().trim(),sector:ins[1].value,type:ins[2].value,value:parseFloat(ins[3].value)||0};
  }).filter(h=>h.value>0);
  if(holdings.length<2){alert('Please add at least 2 holdings with positive values.');return;}
  document.getElementById('loadingState').classList.add('visible');
  ['ls1','ls2','ls3','ls4'].forEach((id,i)=>setTimeout(()=>document.getElementById(id).classList.add('active'),i*320));
  setTimeout(()=>{document.getElementById('loadingState').classList.remove('visible');buildDashboard(holdings);},1700);
}

function buildDashboard(holdings){
  const profile=PROFILES[selectedRisk];
  const total=holdings.reduce((s,h)=>s+h.value,0);
  holdings.forEach(h=>h.weight=h.value/total);
  holdings.sort((a,b)=>b.weight-a.weight);

  const sectorMap={},types={};
  holdings.forEach(h=>{
    sectorMap[h.sector]=(sectorMap[h.sector]||0)+h.weight;
    types[h.type]=(types[h.type]||0)+h.weight;
  });
  const stockW=types['Stock']||0,etfW=types['ETF']||0,bondW=types['Bond']||0;
  const cryptoW=types['Crypto']||0,reitW=types['REIT']||0;

  // ── SCORING ──
  const hhi=holdings.reduce((s,h)=>s+h.weight*h.weight,0);
  const hhiScore=Math.max(0,Math.min(25,25*(1-hhi)*1.15));

  const avgVol=stockW*0.7+cryptoW*2.0+reitW*0.5+bondW*0.1+etfW*0.5;
  const volTargets={conservative:0.3,moderate:0.55,aggressive:0.8,speculative:1.2};
  const targetVol=volTargets[selectedRisk];
  const volDiff=Math.abs(avgVol-targetVol);
  let riskScore=18;
  if(bondW>0.1)riskScore+=4;
  if(etfW>0.15)riskScore+=3;
  if(cryptoW>0.2)riskScore-=6;
  if(stockW>0.9)riskScore-=3;
  riskScore=Math.max(0,Math.min(25,riskScore-volDiff*8));

  const numSectors=Object.keys(sectorMap).length;
  const sectorScore=Math.min(25,numSectors*3.2);

  const maxW=holdings[0].weight,top3=holdings.slice(0,3).reduce((s,h)=>s+h.weight,0);
  let concScore=25;
  if(maxW>0.25)concScore-=10; else if(maxW>0.15)concScore-=4;
  if(top3>0.6)concScore-=6; else if(top3>0.45)concScore-=2;
  concScore=Math.max(0,Math.min(25,concScore));

  const totalScore=Math.round(hhiScore+riskScore+sectorScore+concScore);
  const grade=totalScore>=85?'Excellent ▲':totalScore>=70?'Good ●':totalScore>=55?'Fair ◐':'Needs Work ▼';

  // actual risk
  const riskOrder={Conservative:0,Moderate:1,Aggressive:2,Speculative:3};
  let actualRiskLabel,gaugeVal;
  if(avgVol<0.4){actualRiskLabel='Conservative';gaugeVal=20;}
  else if(avgVol<0.65){actualRiskLabel='Moderate';gaugeVal=45;}
  else if(avgVol<0.85){actualRiskLabel='Aggressive';gaugeVal=70;}
  else{actualRiskLabel='Speculative';gaugeVal=92;}

  const desiredIdx=riskOrder[profile.label];
  const actualIdx=riskOrder[actualRiskLabel];

  // ── BANNER ──
  let bannerClass,bannerIcon,bannerTitle,bannerSub;
  if(desiredIdx===actualIdx){
    bannerClass='ab-match';bannerIcon='✅';
    bannerTitle=`Portfolio risk aligns with your ${profile.label} appetite.`;
    bannerSub='Great alignment. Signals and stock suggestions are tuned to maintain and optimize this balance.';
  } else if(actualIdx<desiredIdx){
    bannerClass='ab-low';bannerIcon='ℹ️';
    bannerTitle=`Portfolio is more ${actualRiskLabel} than your ${profile.label} target.`;
    bannerSub='You have headroom to take more risk. See stock recommendations below for growth-oriented additions.';
  } else {
    bannerClass='ab-high';bannerIcon='⚠️';
    bannerTitle=`Portfolio risk (${actualRiskLabel}) exceeds your ${profile.label} appetite.`;
    bannerSub='Consider trimming high-volatility positions and adding stabilizers from the recommendations below.';
  }
  const banner=document.getElementById('alignBanner');
  banner.className=`align-banner fade-up ${bannerClass}`;
  banner.innerHTML=`<span class="ab-icon">${bannerIcon}</span><div class="alert-text"><strong>${bannerTitle}</strong><span>${bannerSub}</span></div>`;

  // ── POPULATE ──
  document.getElementById('portfolioMeta').textContent=`${holdings.length} holdings · $${total.toLocaleString('en-US',{maximumFractionDigits:0})} total · Risk Appetite: ${profile.label} · ${new Date().toLocaleDateString('en-US',{month:'short',day:'numeric',year:'numeric'})}`;

  const arc=document.getElementById('scoreArc');
  document.getElementById('scoreNum').textContent=totalScore;
  document.getElementById('scoreGrade').textContent=grade;
  setTimeout(()=>{arc.style.strokeDashoffset=326.7-(326.7*(totalScore/100));arc.style.transition='stroke-dashoffset 1.2s ease';},200);

  document.getElementById('mAppetite').textContent=profile.label;
  document.getElementById('mActual').textContent=actualRiskLabel;
  document.getElementById('mTotal').textContent='$'+total.toLocaleString('en-US',{maximumFractionDigits:0});
  document.getElementById('mHoldings').textContent=holdings.length+' positions';
  document.getElementById('mDiv').textContent=hhi<0.1?'Excellent':hhi<0.2?'Good':hhi<0.35?'Moderate':'Poor';
  document.getElementById('mDivSub').textContent='HHI: '+(hhi*100).toFixed(1)+'%';
  document.getElementById('mTop').textContent=(maxW*100).toFixed(1)+'%';
  document.getElementById('mTopTicker').textContent=holdings[0].ticker;
  document.getElementById('mSectors').textContent=numSectors;

  // ── SCORE BREAKDOWN ──
  const bd=[
    {t:'Diversification (HHI)',s:hhiScore,max:25,d:`HHI: ${(hhi*100).toFixed(1)}%. Lower = more diversified. ${hhi<0.15?'Well spread across positions.':'Consider adding more holdings.'}`,c:'#00D4A0'},
    {t:'Risk Balance',s:riskScore,max:25,d:`Portfolio volatility vs your ${profile.label} target. Misalignment penalty: ${(volDiff*8).toFixed(1)} pts. Tighter alignment = higher score.`,c:'#4E9EFF'},
    {t:'Sector Coverage',s:sectorScore,max:25,d:`${numSectors}/10 sectors covered. Each sector adds ~3.2 pts. Target: 8+ sectors for maximum score.`,c:'#F0B429'},
    {t:'Concentration Control',s:concScore,max:25,d:`Top position: ${(maxW*100).toFixed(1)}% (${holdings[0].ticker}). Top 3: ${(top3*100).toFixed(0)}%. Target: top position under 15%.`,c:'#B47EFF'},
  ];
  document.getElementById('scoreBreakdown').innerHTML=bd.map(b=>`
    <div class="sb-item">
      <div class="sb-top"><div class="sb-title">${b.t}</div><div class="sb-score" style="color:${b.c}">${b.s.toFixed(1)} / ${b.max}</div></div>
      <div class="sb-bar-track"><div class="sb-bar-fill" style="width:${Math.min(100,(b.s/b.max*100)).toFixed(0)}%;background:${b.c}"></div></div>
      <div class="sb-desc">${b.d}</div>
    </div>`).join('');

  // ── PIE ──
  if(pieInst)pieInst.destroy();
  pieInst=new Chart(document.getElementById('pieChart').getContext('2d'),{type:'doughnut',data:{labels:holdings.map(h=>h.ticker),datasets:[{data:holdings.map(h=>(h.weight*100).toFixed(1)),backgroundColor:COLORS.map((c,i)=>i<holdings.length?c:'#252A55'),borderColor:'#07091A',borderWidth:3,hoverOffset:5}]},options:{responsive:true,maintainAspectRatio:false,cutout:'64%',plugins:{legend:{display:false},tooltip:{callbacks:{label:ctx=>`${ctx.label}: ${ctx.raw}%`}}}}});
  document.getElementById('pieLegend').innerHTML=holdings.map((h,i)=>`<span class="legend-item"><span class="legend-dot" style="background:${COLORS[i%COLORS.length]}"></span>${h.ticker} ${(h.weight*100).toFixed(1)}%</span>`).join('');

  // ── SECTOR CHART ──
  if(secInst)secInst.destroy();
  const secEntries=Object.entries(sectorMap).sort((a,b)=>b[1]-a[1]);
  document.getElementById('sectorWrap').style.height=Math.max(180,secEntries.length*42+50)+'px';
  secInst=new Chart(document.getElementById('sectorChart').getContext('2d'),{type:'bar',data:{labels:secEntries.map(e=>e[0]),datasets:[{label:'%',data:secEntries.map(e=>(e[1]*100).toFixed(1)),backgroundColor:secEntries.map((_,i)=>COLORS[i%COLORS.length]+'BB'),borderColor:secEntries.map((_,i)=>COLORS[i%COLORS.length]),borderWidth:1,borderRadius:4}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{callbacks:{label:c=>`${c.raw}%`}}},scales:{x:{grid:{color:'rgba(37,42,85,.4)'},ticks:{color:'#9BA3C8',font:{family:'DM Mono'},callback:v=>v+'%'},border:{color:'transparent'}},y:{grid:{display:false},ticks:{color:'#9BA3C8',font:{size:11.5}},border:{color:'transparent'}}}}});

  // ── GAUGE ──
  if(gaugeInst)gaugeInst.destroy();
  gaugeInst=new Chart(document.getElementById('gaugeChart').getContext('2d'),{type:'doughnut',data:{datasets:[{data:[(gaugeVal/100)*100,(100-(gaugeVal/100)*100),100],backgroundColor:[gaugeVal<40?'#00D4A0':gaugeVal<70?'#F0B429':'#FF5B5B','#1C2145','#07091A'],borderWidth:0,circumference:180,rotation:270}]},options:{responsive:true,maintainAspectRatio:false,cutout:'72%',plugins:{legend:{display:false},tooltip:{enabled:false}}}});
  const gc=gaugeVal<40?'var(--emerald)':gaugeVal<70?'var(--gold)':'var(--red)';
  document.getElementById('gaugeLabel').style.color=gc;
  document.getElementById('gaugeLabel').textContent=actualRiskLabel;
  document.getElementById('gaugeSub').textContent=`Risk Score: ${gaugeVal}/100`;

  // ── BARS ──
  document.getElementById('holdingsBars').innerHTML=holdings.map((h,i)=>`
    <div class="prog-bar-row">
      <div class="prog-label" title="${h.ticker}">${h.ticker}</div>
      <div class="prog-track"><div class="prog-fill" style="width:${(h.weight*100).toFixed(1)}%;background:${COLORS[i%COLORS.length]}"></div></div>
      <div class="prog-pct">${(h.weight*100).toFixed(1)}%</div>
    </div>`).join('');

  // ── RECO TABLE ──
  document.getElementById('recoSubtitle').textContent=`Signals calibrated for your ${profile.label} risk appetite`;
  document.getElementById('recoTableBody').innerHTML=holdings.map(h=>{
    const w=h.weight*100,sW=(sectorMap[h.sector]||0)*100;
    let signal,rationale;
    if(h.type==='Crypto'&&selectedRisk==='conservative'){signal='sell';rationale='Crypto incompatible with Conservative appetite. Move to bonds or dividend ETFs.';}
    else if(h.type==='Crypto'&&selectedRisk==='moderate'&&h.weight>0.05){signal='reduce';rationale='Moderate profile: keep crypto under 5%. Trim and redirect to diversified ETFs.';}
    else if(h.type==='Bond'&&selectedRisk==='speculative'){signal='sell';rationale='Bonds cap return potential for Speculative profiles. Redeploy into high-growth assets.';}
    else if(w>25){signal='sell';rationale='Exceeds 25% single-position limit — critical concentration risk.';}
    else if(w>18&&sW>35){signal='reduce';rationale=`Both position and ${h.sector} sector are elevated. Trim to reduce overexposure.`;}
    else if(actualIdx>desiredIdx&&h.type==='Stock'&&w>12){signal='reduce';rationale=`Portfolio too risky for ${profile.label} appetite. Trim equity, add stabilizers.`;}
    else if(actualIdx<desiredIdx&&h.type==='Bond'){signal='reduce';rationale=`Portfolio too conservative for ${profile.label} appetite. Reduce bonds, shift to growth assets.`;}
    else if(sW>35){signal='hold';rationale='Sector overweight. Hold but avoid adding more exposure here.';}
    else if(w<3&&h.type==='ETF'){signal='buy';rationale='Small ETF position — increasing adds efficient diversification.';}
    else{signal='hold';rationale=`Within acceptable range for your ${profile.label} profile.`;}
    const tc={'buy':'sig-buy','hold':'sig-hold','sell':'sig-sell','reduce':'sig-reduce'}[signal];
    return`<tr><td style="font-family:var(--fm);font-weight:500">${h.ticker}</td><td style="color:var(--text2)">${h.sector}</td><td style="color:var(--text2)">${h.type}</td><td style="font-family:var(--fm)">${w.toFixed(1)}%</td><td><span class="${tc} sig-tag">${signal.toUpperCase()}</span></td><td style="color:var(--text2);font-size:12px">${rationale}</td></tr>`;
  }).join('');

  // ── BUY RECOMMENDATIONS ──
  const existing=new Set(holdings.map(h=>h.ticker));
  let buys=profile.buys.filter(b=>!existing.has(b.ticker));
  // if portfolio misaligned, blend in some from adjacent profile
  if(actualIdx<desiredIdx&&desiredIdx>0){
    const adjKey=Object.keys(PROFILES)[desiredIdx];
    const extra=PROFILES[adjKey].buys.filter(b=>!existing.has(b.ticker)&&!buys.find(x=>x.ticker===b.ticker)).slice(0,2);
    buys=[...buys,...extra];
  }
  buys=buys.slice(0,8);
  document.getElementById('buyRecoSub').textContent=`Personalized additions for your ${profile.label} risk profile — filtered by portfolio gaps`;
  document.getElementById('buyRecoGrid').innerHTML=buys.map(b=>`
    <div class="buy-card ${b.cls}">
      <div class="bc-header">
        <div class="bc-ticker">${b.ticker}</div>
        <div class="bc-badge ${b.cls}">${b.type}</div>
      </div>
      <div class="bc-name">${b.name}</div>
      <div class="bc-sector">${b.sector}</div>
      <div class="bc-reason">${b.reason}</div>
      <div class="bc-metrics">
        <div class="bc-met"><div class="bm-label">Risk</div><div class="bm-val">${b.risk}</div></div>
        ${b.yield!=='0.0%'?`<div class="bc-met"><div class="bm-label">Yield</div><div class="bm-val">${b.yield}</div></div>`:''}
      </div>
    </div>`).join('');

  // ── ALERTS ──
  const alerts=[];
  if(maxW>0.25)alerts.push({t:'err',i:'⚠',h:`${holdings[0].ticker} is ${(maxW*100).toFixed(1)}% — critical overweight`,s:'Exceeds the 25% single-position limit. Strongly consider trimming immediately.'});
  else if(maxW>0.15)alerts.push({t:'warn',i:'△',h:`${holdings[0].ticker} at ${(maxW*100).toFixed(1)}% — approaching limit`,s:'Getting close to the 25% concentration threshold. Monitor closely.'});
  Object.entries(sectorMap).forEach(([sec,w])=>{if(w>0.35)alerts.push({t:'warn',i:'△',h:`${sec} sector at ${(w*100).toFixed(0)}%`,s:'Above the 35% sector concentration guideline. Diversify into underrepresented sectors.'});});
  if(cryptoW>0.1&&selectedRisk==='conservative')alerts.push({t:'err',i:'⚠',h:'Crypto conflicts with your Conservative appetite',s:'Any meaningful crypto allocation creates volatility incompatible with capital preservation.'});
  if(bondW===0&&(selectedRisk==='conservative'||selectedRisk==='moderate'))alerts.push({t:'warn',i:'△',h:'No bonds detected',s:`${profile.label} profiles benefit from 10–35% bond allocation. Consider BND or AGG.`});
  if(actualIdx>desiredIdx)alerts.push({t:'warn',i:'△',h:`Actual risk (${actualRiskLabel}) exceeds your ${profile.label} target`,s:'See buy recommendations for stabilizers and the rebalancing plan for trim targets.'});
  if(actualIdx<desiredIdx)alerts.push({t:'info',i:'ℹ',h:`Portfolio is more ${actualRiskLabel} than your ${profile.label} target`,s:'You may be leaving potential returns on the table. See recommendations for growth additions.'});
  if(numSectors<3)alerts.push({t:'err',i:'⚠',h:`Only ${numSectors} sector(s) covered`,s:'Very low diversification. Aim for 5+ GICS sectors to reduce drawdown risk.'});
  if(!alerts.length)alerts.push({t:'success',i:'✓',h:'Portfolio is well-aligned with your risk appetite',s:'No major concentration or risk misalignment issues detected. Well done.'});
  const tMap={err:'alert-err',warn:'alert-warn',info:'alert-info',success:'alert-success'};
  document.getElementById('alertsContainer').innerHTML=alerts.map(a=>`<div class="alert-item ${tMap[a.t]}"><span class="alert-icon">${a.i}</span><div class="alert-text"><strong>${a.h}</strong><span>${a.s}</span></div></div>`).join('');

  // ── REBALANCING ──
  document.getElementById('rebalContainer').innerHTML=holdings.map(h=>{
    const w=h.weight*100;
    let action,cls,reason;
    if(h.type==='Crypto'&&selectedRisk==='conservative'){action='SELL';cls='r-sell';reason='Exit crypto entirely. Move to bonds or dividend ETFs for capital preservation.';}
    else if(h.type==='Bond'&&selectedRisk==='speculative'){action='SELL';cls='r-sell';reason='Bonds cap return potential. Redeploy into high-growth speculative assets.';}
    else if(w>20){action='TRIM';cls='r-trim';reason=`Reduce by ~${(w-14).toFixed(0)}% to bring position below 15% threshold.`;}
    else if(actualIdx<desiredIdx&&h.type==='ETF'&&w<15){action='BUY';cls='r-buy';reason='Increase ETF weight to raise portfolio risk toward your target appetite.';}
    else if(actualIdx>desiredIdx&&h.type==='Stock'&&w>10){action='TRIM';cls='r-trim';reason=`Trim equity to lower volatility and align with your ${profile.label} target.`;}
    else{action='HOLD';cls='r-hold';reason=`Weight fits your ${profile.label} profile. Maintain current allocation.`;}
    return`<div class="rebal-item"><div class="r-ticker">${h.ticker} — ${w.toFixed(1)}%</div><div class="r-action ${cls}">${action}</div><div class="r-reason">${reason}</div></div>`;
  }).join('');

  document.getElementById('dashboard').classList.add('visible');
  setTimeout(()=>document.getElementById('dashboard').scrollIntoView({behavior:'smooth',block:'start'}),100);
}

function resetDashboard(){
  document.getElementById('dashboard').classList.remove('visible');
  ['ls1','ls2','ls3','ls4'].forEach(id=>document.getElementById(id).classList.remove('active'));
  document.getElementById('analyze').scrollIntoView({behavior:'smooth'});
}

addRow();addRow();addRow();
</script>
</body>
</html>
