<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>АналитЭко — лаборатория мониторинга воздуха и выбросов</title>
<meta name="description" content="Точные измерения атмосферного воздуха и промышленных выбросов. Официальные протоколы, которые примут контролирующие органы.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400..600;1,9..144,400..500&family=Manrope:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
/* ============ TOKENS ============ */
:root{
  --bg:#F4F3ED; --bg-2:#ECEAE1; --card:#FBFAF5; --white:#FCFBF7;
  --ink:#101812; --ink-2:#2A352C; --muted:#566257;
  --line:rgba(16,24,18,.10); --line-2:rgba(16,24,18,.20);
  --green:#2C4A37; --green-2:#1C3325; --green-3:#14271C;
  --sage:#A6BE98; --sage-soft:rgba(166,190,152,.16); --tint:#E7EDE2;
  --sh-sm:0 1px 2px rgba(16,24,18,.05);
  --sh:0 2px 4px rgba(16,24,18,.04),0 14px 34px -18px rgba(16,24,18,.20);
  --sh-lg:0 4px 10px rgba(16,24,18,.05),0 28px 64px -28px rgba(16,24,18,.30);
  --r-sm:10px; --r:16px; --r-lg:24px; --r-pill:999px;
  --disp:"Fraunces",Georgia,serif; --body:"Manrope",system-ui,sans-serif; --mono:"JetBrains Mono",ui-monospace,monospace;
  --wrap:1240px; --sec-pad:clamp(48px,6vw,72px); --range-w:200px;
}
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth;scroll-padding-top:86px}
body{font-family:var(--body);background:var(--bg);color:var(--ink);line-height:1.65;font-size:16px;-webkit-font-smoothing:antialiased;overflow-x:hidden}
::selection{background:var(--green);color:var(--white)}
img{max-width:100%;display:block} a{color:inherit;text-decoration:none} ul,ol{list-style:none}
:focus-visible{outline:2px solid var(--green);outline-offset:3px;border-radius:4px}
.wrap{max-width:var(--wrap);margin:0 auto;padding:0 24px}
.mono{font-family:var(--mono)}
.sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);white-space:nowrap;border:0}

/* ============ REVEAL / MOTION ============ */
.rv{opacity:0;transform:translateY(20px);transition:opacity .7s ease,transform .85s cubic-bezier(.22,1,.36,1);transition-delay:var(--d,0s)}
.rv.on{opacity:1;transform:none}
.mask{display:block;overflow:hidden}
.mask>span{display:block;transform:translateY(115%);transition:transform .9s cubic-bezier(.22,1,.36,1);transition-delay:var(--d,0s)}
.rv-lines.on .mask>span{transform:none}

/* ============ MASTHEAD ============ */
.masthead{position:sticky;top:0;z-index:100;background:rgba(244,243,237,.82);backdrop-filter:blur(16px) saturate(1.25);-webkit-backdrop-filter:blur(16px) saturate(1.25);border-bottom:1px solid var(--line);transition:box-shadow .35s,border-color .35s,background .35s}
.masthead.scrolled{box-shadow:var(--sh);border-bottom-color:var(--line-2)}
.masthead.nav-open{background:var(--green-2);border-color:transparent;backdrop-filter:none;-webkit-backdrop-filter:none}
.mast-in{display:flex;align-items:center;gap:18px;padding:14px 24px}
.brand{display:flex;align-items:center;gap:13px;flex-shrink:0}
.logo-slot{width:50px;height:50px;display:grid;place-items:center;border:1px solid var(--line-2);border-radius:14px;background:linear-gradient(150deg,var(--tint),var(--bg-2));color:var(--muted);flex-shrink:0}
.logo-ph{font-family:var(--mono);font-size:10px;letter-spacing:.24em;text-transform:uppercase}
.brand-text strong{font-family:var(--disp);font-weight:600;font-size:19px;letter-spacing:.01em;display:block;line-height:1.1}
.brand-text small{font-family:var(--mono);font-size:10px;letter-spacing:.2em;text-transform:uppercase;color:var(--muted)}
.masthead.nav-open .logo-slot{border-color:rgba(252,251,247,.3);background:rgba(252,251,247,.06);color:rgba(252,251,247,.7)}
.masthead.nav-open .brand-text strong{color:var(--white)}
.masthead.nav-open .brand-text small{color:rgba(252,251,247,.55)}
.main-nav{display:flex;gap:14px;margin-left:auto}
.main-nav a{font-family:var(--mono);font-size:12.5px;letter-spacing:.04em;text-transform:uppercase;position:relative;padding:7px 0;color:var(--ink-2);transition:color .25s;white-space:nowrap}
.main-nav a::after{content:"";position:absolute;left:0;bottom:2px;height:1.5px;width:100%;background:var(--green);transform:scaleX(0);transform-origin:left;transition:transform .35s cubic-bezier(.22,1,.36,1)}
.main-nav a:hover,.main-nav a.active{color:var(--ink)}
.main-nav a:hover::after,.main-nav a.active::after{transform:scaleX(1)}
.nav-drop{position:relative;display:flex;align-items:center}
.dropdown{position:absolute;top:100%;left:50%;transform:translate(-50%,12px);min-width:288px;background:var(--card);border:1px solid var(--line);border-radius:var(--r);box-shadow:var(--sh-lg);padding:8px;opacity:0;visibility:hidden;transition:opacity .25s ease,transform .35s cubic-bezier(.22,1,.36,1),visibility .25s;z-index:60}
.dropdown--about{min-width:312px}
.nav-drop:hover .dropdown,.nav-drop:focus-within .dropdown{opacity:1;visibility:visible;transform:translate(-50%,16px)}
.dropdown a{display:flex;align-items:baseline;gap:11px;font-family:var(--mono);font-size:12px;letter-spacing:.02em;padding:11px 14px;border-radius:9px;color:var(--ink-2);transition:background .2s,color .2s;white-space:normal}
.dropdown a::after{display:none}
.dropdown a i{font-style:normal;color:var(--green);font-size:10px;flex-shrink:0}
.dropdown a:hover{background:var(--tint);color:var(--ink)}
.burger{display:none;margin-left:auto;width:46px;height:46px;border:1px solid var(--line-2);border-radius:12px;background:transparent;cursor:pointer;flex-direction:column;justify-content:center;align-items:center;gap:6px}
.burger span{display:block;width:18px;height:2px;background:var(--ink);border-radius:2px;transition:transform .3s,opacity .3s,background .3s}
.burger[aria-expanded="true"] span:nth-child(1){transform:translateY(8px) rotate(45deg)}
.burger[aria-expanded="true"] span:nth-child(2){opacity:0}
.burger[aria-expanded="true"] span:nth-child(3){transform:translateY(-8px) rotate(-45deg)}
.masthead.nav-open .burger{border-color:rgba(252,251,247,.3)}
.masthead.nav-open .burger span{background:var(--white)}
.scroll-progress{position:absolute;left:0;right:0;bottom:-1px;height:2px;overflow:hidden}
.scroll-progress span{display:block;height:100%;background:var(--green);transform:scaleX(0);transform-origin:left}

/* ============ BUTTONS ============ */
.btn{display:inline-flex;align-items:center;gap:10px;font-family:var(--mono);font-size:12px;letter-spacing:.1em;text-transform:uppercase;padding:14px 24px;border-radius:var(--r-pill);border:1px solid var(--line-2);background:transparent;color:var(--ink);cursor:pointer;transition:background .28s,color .28s,border-color .28s,transform .28s,box-shadow .28s;white-space:nowrap}
.btn .ar{transition:transform .28s}
.btn:hover{transform:translateY(-2px)}
.btn:hover .ar{transform:translateX(4px)}
.btn-primary{background:var(--green);border-color:var(--green);color:var(--white);box-shadow:var(--sh)}
.btn-primary:hover{background:var(--green-2);border-color:var(--green-2);box-shadow:var(--sh-lg)}
.btn-ghost:hover{background:var(--ink);border-color:var(--ink);color:var(--white)}

/* ============ SECTION SHELL ============ */
.sec{padding:var(--sec-pad) 0}
.sec-head{display:grid;grid-template-columns:1fr auto;align-items:end;gap:20px;margin-bottom:34px}
.sec-title{font-family:var(--disp);font-weight:500;font-size:clamp(1.7rem,3.4vw,2.7rem);line-height:1.08;letter-spacing:-.01em;margin-top:16px;color:var(--ink)}
.sec-note{font-family:var(--mono);font-size:11px;letter-spacing:.16em;text-transform:uppercase;color:var(--muted);padding-bottom:6px;display:flex;align-items:center;gap:8px}
.sec-note::before{content:"";width:6px;height:6px;border-radius:50%;background:var(--green)}
.sec-dark{background:var(--green-2);color:var(--white);position:relative;overflow:hidden}
.sec-dark::before{content:"";position:absolute;inset:0;background:radial-gradient(70% 60% at 85% 0%,rgba(166,190,152,.10),transparent 65%);pointer-events:none}
.sec-dark .sec-title{color:var(--white)}
.sec-dark .sec-note{color:var(--sage)}
.sec-dark .sec-note::before{background:var(--sage)}

/* ============ HERO / ГЛАВНАЯ ============ */
.hero-sec{padding:calc(var(--sec-pad) + 8px) 0 calc(var(--sec-pad) + 12px);position:relative;overflow:hidden}
.hero-sec::before{content:"";position:absolute;inset:0;background:radial-gradient(60% 55% at 82% -5%,var(--tint),transparent 70%);pointer-events:none}
.hero-grid{display:grid;grid-template-columns:1.12fr .88fr;gap:52px;align-items:center;position:relative}
h1{font-family:var(--disp);font-weight:500;font-size:clamp(2.1rem,4.6vw,3.5rem);line-height:1.06;letter-spacing:-.02em;max-width:15ch}
.lead{margin:26px 0 34px;font-size:17.5px;color:var(--muted);max-width:50ch}
.lead b{color:var(--ink);font-weight:600}
.hero-cta{display:flex;gap:14px;flex-wrap:wrap}
.hero-fig{position:relative;margin:0}
.hero-fig::after{content:"";position:absolute;inset:-14px;border:1px solid var(--line);border-radius:calc(var(--r-lg) + 10px);pointer-events:none}

/* image placeholders */
.fig-slot{border:1px solid var(--line-2);border-radius:var(--r-lg);background:linear-gradient(140deg,var(--tint),var(--bg-2));display:grid;place-items:center;align-content:center;justify-items:center;gap:12px;color:var(--muted);box-shadow:var(--sh);position:relative;overflow:hidden;aspect-ratio:6/5}
.fig-slot img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover}
.fig-ic{width:50px;height:50px;color:var(--green);opacity:.55}
.fig-label{font-family:var(--mono);font-size:12px;letter-spacing:.2em;text-transform:uppercase}
.fig-size{font-family:var(--mono);font-size:11px;letter-spacing:.12em;opacity:.6}

/* ============ SERVICES (bento) ============ */
.svc-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:18px}
.svc{scroll-margin-top:90px}
.svc-in{position:relative;display:flex;flex-direction:column;height:100%;padding:24px 22px;min-height:236px;border-radius:var(--r);background:var(--card);border:1px solid var(--line);box-shadow:var(--sh-sm);transition:background .35s,color .35s,transform .35s,box-shadow .35s,border-color .35s}
.svc-in h3{font-family:var(--disp);font-weight:500;font-size:1.05rem;line-height:1.32;letter-spacing:0;transition:color .35s}
.svc-body{position:relative;flex:1;margin-top:16px;overflow:hidden;min-height:96px}
.svc-desc,.svc-list{position:absolute;inset:0;transition:opacity .35s ease,transform .45s cubic-bezier(.22,1,.36,1)}
.svc-desc{color:var(--muted);font-size:13.5px;line-height:1.6}
.svc-list{opacity:0;transform:translateY(10px);pointer-events:none;overflow-y:auto;padding-right:6px}
.svc-list::-webkit-scrollbar{width:5px}
.svc-list::-webkit-scrollbar-thumb{background:rgba(166,190,152,.4);border-radius:3px}
.svc-list li{border-bottom:1px solid var(--sage-soft);padding:9px 0;font-size:11.5px;line-height:1.45}
.svc-list li:first-child{padding-top:0}
.svc-list li:last-child{border-bottom:0}
.svc-list a{display:block;color:rgba(252,251,247,.85);cursor:pointer;transition:color .2s;padding-left:18px;position:relative}
.svc-list a::before{content:"→";position:absolute;left:0;color:var(--sage);transition:transform .2s}
.svc-list a:hover{color:var(--sage)}
.svc-list a:hover::before{transform:translateX(3px)}
.svc-in.show-svc{background:var(--green-2);border-color:var(--green-2);color:var(--white);transform:translateY(-4px);box-shadow:var(--sh-lg)}
.svc-in.show-svc h3{color:var(--white)}
.svc-in.show-svc .svc-desc{opacity:0;transform:translateY(-10px);pointer-events:none}
.svc-in.show-svc .svc-list{opacity:1;transform:none;pointer-events:auto}
@media (hover:hover){
  .svc-in:hover{background:var(--green-2);border-color:var(--green-2);color:var(--white);transform:translateY(-4px);box-shadow:var(--sh-lg)}
  .svc-in:hover h3{color:var(--white)}
  .svc-in:hover .svc-desc{opacity:0;transform:translateY(-10px);pointer-events:none}
  .svc-in:hover .svc-list{opacity:1;transform:none;pointer-events:auto}
}
@media (hover:none){
  .svc-in{min-height:0}
  .svc-body{overflow:visible}
  .svc-desc,.svc-list{position:static;inset:auto}
  .svc-desc{opacity:1;transform:none}
  .svc-list{opacity:0;max-height:0;overflow:hidden;transform:none;transition:max-height .5s cubic-bezier(.22,1,.36,1),opacity .3s}
  .svc-in.show-svc .svc-desc{display:none}
  .svc-in.show-svc .svc-list{opacity:1;max-height:1400px;overflow:visible;pointer-events:auto}
}

/* ============ INDICATOR TABLES ============ */
.ind-grid{display:grid;grid-template-columns:1.55fr 1fr;gap:30px;align-items:stretch}
.ind-table{min-width:0}
.ind-scroll{max-height:600px;overflow:auto;border:1px solid var(--line-2);border-radius:var(--r);background:var(--card);box-shadow:var(--sh)}
.ind-scroll::-webkit-scrollbar{width:8px;height:8px}
.ind-scroll::-webkit-scrollbar-thumb{background:var(--line-2);border-radius:8px}
.ind-scroll table{width:100%;border-collapse:collapse;font-family:var(--mono);font-size:12px;table-layout:fixed}
.ind-scroll th{text-align:left;padding:13px 16px;position:sticky;top:0;background:var(--tint);z-index:2;text-transform:uppercase;letter-spacing:.1em;font-size:10px;color:var(--muted);border-bottom:1px solid var(--line-2);white-space:nowrap}
.ind-scroll th:nth-child(1){width:56px}
.ind-scroll th:nth-child(3){width:var(--range-w)}
.ind-scroll td{padding:11px 16px;border-bottom:1px solid var(--line);vertical-align:top;overflow-wrap:break-word;transition:background .2s}
.ind-scroll td:nth-child(1){white-space:nowrap;color:var(--muted);font-size:11px}
.ind-scroll td.ind-ranges{text-align:right;color:var(--ink-2)}
.ind-scroll td.ind-ranges span{display:block;white-space:nowrap}
.ind-scroll tbody tr{transition:background .2s,box-shadow .2s}
.ind-scroll tbody tr:hover{background:rgba(44,74,55,.05);box-shadow:inset 3px 0 0 var(--green)}
.ind-scroll td .ind-name{display:block;font-family:var(--body);font-weight:500;font-size:13px;line-height:1.35;color:var(--ink)}
.ind-scroll td .ind-sub{display:block;font-family:var(--body);font-size:9.5px;color:var(--muted);opacity:.8;margin-top:4px;line-height:1.5}
.ind-photo{aspect-ratio:auto;min-height:360px;height:100%;margin:0}
.ind-photo .fig-label{font-size:11px}
.sec-dark .ind-scroll{background:var(--green-3);border-color:rgba(166,190,152,.18);box-shadow:none}
.sec-dark .ind-scroll::-webkit-scrollbar-thumb{background:rgba(166,190,152,.3)}
.sec-dark .ind-scroll th{background:rgba(166,190,152,.1);border-color:rgba(166,190,152,.2);color:var(--sage)}
.sec-dark .ind-scroll td{border-color:rgba(166,190,152,.12);color:rgba(252,251,247,.82)}
.sec-dark .ind-scroll td.ind-ranges{color:var(--sage)}
.sec-dark .ind-scroll td .ind-name{color:var(--white)}
.sec-dark .ind-scroll td .ind-sub{color:rgba(252,251,247,.5)}
.sec-dark .ind-scroll tbody tr:hover{background:rgba(166,190,152,.08);box-shadow:inset 3px 0 0 var(--sage)}
.sec-dark .ind-photo{background:rgba(166,190,152,.08);border-color:rgba(166,190,152,.2);box-shadow:none;color:rgba(252,251,247,.6)}
.sec-dark .ind-photo .fig-ic{color:var(--sage);opacity:.7}
.cta-col{display:flex;flex-direction:column;align-items:flex-start;gap:18px;margin-top:34px}
.cta-col p{max-width:60ch;color:var(--muted);font-size:15px;line-height:1.65}
.sec-dark .cta-col p{color:rgba(252,251,247,.72)}

/* ============ LAB (часть Услуги) ============ */
.ab-2col{display:grid;grid-template-columns:1.4fr 1fr;gap:34px;align-items:start}
#lab .ab-2col{align-items:stretch}
.ab-text{margin-top:14px;display:grid;gap:14px;max-width:82ch}
.ab-text p{color:var(--muted);font-size:15.5px;line-height:1.7}
.ab-text p b{color:var(--ink);font-weight:600}
.ab-sub{font-family:var(--disp);font-weight:500;font-size:1.1rem;letter-spacing:0;color:var(--ink)}
.fig-cert{aspect-ratio:4/5}
#lab .fig-cert{aspect-ratio:auto;min-height:0}
.status-stats{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;margin-top:26px}
.ss{background:var(--green-2);border-radius:var(--r);padding:26px 22px;box-shadow:var(--sh)}
.ss b{font-family:var(--disp);font-weight:600;font-size:clamp(1.6rem,2.8vw,2.1rem);color:var(--sage);display:block;line-height:1.1;font-variant-numeric:tabular-nums;letter-spacing:-.01em}
.ss span{font-family:var(--mono);font-size:11px;letter-spacing:.06em;text-transform:uppercase;color:rgba(252,251,247,.6);display:block;margin-top:12px;line-height:1.4}

/* ============ ABOUT ============ */
.about-list{display:grid;gap:16px}
.ab{position:relative;background:var(--card);border:1px solid var(--line);border-radius:var(--r);padding:26px 30px 28px;box-shadow:var(--sh-sm);transition:background .3s,box-shadow .3s,transform .3s}
.ab::before{content:"";position:absolute;left:0;top:24px;bottom:24px;width:3px;border-radius:3px;background:var(--green);transform:scaleY(0);transform-origin:top;transition:transform .45s cubic-bezier(.22,1,.36,1)}
.ab:hover{background:var(--white);box-shadow:var(--sh);transform:translateY(-2px)}
.ab:hover::before{transform:scaleY(1)}
.ab h3{font-family:var(--disp);font-weight:500;font-size:1.2rem;letter-spacing:0;line-height:1.3;margin-bottom:6px}
.why-grid{display:grid;grid-template-columns:1fr 1fr;gap:24px 40px;margin-top:18px}
.why-col{display:grid;gap:22px}
.why-item h4{font-family:var(--disp);font-weight:500;font-size:1rem;margin-bottom:8px;color:var(--ink)}
.why-item p{font-size:14px;color:var(--muted);line-height:1.65}
.company-text{margin-top:14px;display:grid;gap:14px}
.company-text p{color:var(--muted);font-size:15px;line-height:1.7}
.steps{display:grid;grid-template-columns:repeat(4,1fr);gap:24px;margin-top:22px}
.step{border-top:2px solid var(--line-2);padding-top:16px;transition:border-color .3s}
.step:hover{border-top-color:var(--green)}
.step-num{font-family:var(--disp);font-weight:600;font-size:1.7rem;color:var(--green);line-height:1;display:block;letter-spacing:-.02em}
.step h4{font-family:var(--disp);font-weight:500;font-size:.95rem;margin:12px 0 8px;line-height:1.35}
.step p{font-size:13px;color:var(--muted)}

/* tree — «Наша история» */
.tree{position:relative;max-width:740px;margin:22px auto 0;padding:6px 0}
.trunk{position:absolute;left:50%;top:0;bottom:0;width:3px;border-radius:3px;background:linear-gradient(var(--green),#7d9672);transform:translateX(-50%) scaleY(0);transform-origin:top center}
.tl{position:relative;width:50%;padding:0 30px 24px;opacity:0;transform:translateY(26px);transition:opacity .55s ease,transform .65s cubic-bezier(.22,1,.36,1)}
.tl.b-r{margin-left:50%;text-align:left}
.tl.b-l{text-align:right}
.tl .leaf{position:absolute;top:8px;width:14px;height:14px;background:var(--green);border-radius:50%;box-shadow:0 0 0 4px var(--tint);transform:scale(0);transition:transform .5s cubic-bezier(.34,1.56,.64,1) .12s}
.tl.b-l .leaf{right:-7px}
.tl.b-r .leaf{left:-7px}
.tl.on{opacity:1;transform:none}
.tl.on .leaf{transform:scale(1)}
.tl-card{display:inline-block;text-align:left;border:1px solid var(--line);background:var(--white);border-radius:var(--r-sm);padding:14px 18px;max-width:100%;box-shadow:var(--sh-sm)}
.tl-card b{font-family:var(--disp);font-weight:600;font-size:.85rem;display:block;margin-bottom:5px}
.tl-card span{font-size:13px;color:var(--muted)}

/* FAQ */
.faq{display:grid;gap:12px;margin-top:18px}
.faq-item{background:var(--white);border:1px solid var(--line);border-radius:var(--r-sm);overflow:hidden;transition:border-color .3s,box-shadow .3s}
.faq-item.open{border-color:var(--line-2);box-shadow:var(--sh-sm)}
.faq-q{width:100%;text-align:left;cursor:pointer;background:none;border:0;padding:18px 22px;font-family:var(--disp);font-weight:500;font-size:.98rem;line-height:1.35;color:var(--ink);display:flex;justify-content:space-between;align-items:center;gap:18px}
.faq-ic{position:relative;width:16px;height:16px;flex-shrink:0}
.faq-ic::before,.faq-ic::after{content:"";position:absolute;background:var(--green);border-radius:2px;transition:transform .35s,opacity .3s}
.faq-ic::before{left:50%;top:0;bottom:0;width:2px;transform:translateX(-50%)}
.faq-ic::after{top:50%;left:0;right:0;height:2px;transform:translateY(-50%)}
.faq-item.open .faq-ic::after{opacity:0}
.faq-a{display:grid;grid-template-rows:0fr;transition:grid-template-rows .45s cubic-bezier(.22,1,.36,1)}
.faq-item.open .faq-a{grid-template-rows:1fr}
.faq-a-in{overflow:hidden}
.faq-a-in p{padding:0 22px 20px;color:var(--muted);font-size:14.5px;line-height:1.65;max-width:82ch}

/* ============ CONTACTS ============ */
.con-list{display:grid;grid-template-columns:1fr 1fr;gap:24px 56px;padding-top:18px;max-width:960px}
.con-item{display:grid;grid-template-columns:120px 1fr;gap:16px;align-items:baseline}
.con-item .k{font-family:var(--mono);font-size:11px;letter-spacing:.16em;text-transform:uppercase;color:var(--muted)}
.con-item .v{font-size:17px;color:var(--ink)}
.con-item .v a{border-bottom:1px solid var(--line-2);transition:border-color .2s,color .2s}
.con-item .v a:hover{color:var(--green);border-color:var(--green)}
.con-sub{display:block;font-family:var(--mono);font-size:11.5px;letter-spacing:.03em;color:var(--muted);margin-top:8px}

/* ============ FOOTER ============ */
footer{background:var(--green-3);color:var(--white);position:relative;overflow:hidden}
footer::before{content:"";position:absolute;inset:0;background:radial-gradient(70% 80% at 15% 0%,rgba(166,190,152,.10),transparent 60%);pointer-events:none}
footer{border-top:1px solid rgba(166,190,152,.22)}
.foot-grid{display:grid;grid-template-columns:1.6fr 1fr 1fr;gap:34px 30px;padding:48px 0 26px;position:relative}
.foot-brand .logo-slot{width:46px;height:46px;border-color:rgba(252,251,247,.3);background:rgba(252,251,247,.06);color:rgba(252,251,247,.7)}
.foot-brand .brand-text strong{font-size:20px;color:var(--white)}
.foot-brand .brand-text small{color:rgba(252,251,247,.5)}
.foot-acc{margin-top:22px;font-size:12px;line-height:1.7;color:rgba(252,251,247,.6);max-width:42ch}
.foot-acc a{color:inherit;border-bottom:1px dashed rgba(252,251,247,.3);transition:color .2s,border-color .2s}
.foot-acc a:hover{color:var(--sage);border-color:var(--sage)}
.foot-acc b{color:var(--sage);font-weight:600}
.foot-copy{margin-top:14px;font-family:var(--mono);font-size:11px;letter-spacing:.06em;color:rgba(252,251,247,.5)}
.fcol h4{font-family:var(--mono);font-size:11px;letter-spacing:.2em;text-transform:uppercase;color:var(--sage);margin-bottom:18px}
.fcol li{margin-bottom:11px}
.fcol a{font-size:14px;color:rgba(252,251,247,.78);transition:color .2s,padding-left .25s}
.fcol a:hover{color:var(--sage);padding-left:6px}
.fcol .mono{font-size:13px;color:rgba(252,251,247,.78);display:block;margin-bottom:11px}
.foot-bot{border-top:1px solid rgba(252,251,247,.14);padding:16px 0;display:flex;justify-content:flex-end;position:relative}
.foot-bot a{font-family:var(--mono);font-size:11px;letter-spacing:.1em;text-transform:uppercase;color:rgba(252,251,247,.55);transition:color .2s}
.foot-bot a:hover{color:var(--sage)}

/* ============ RESPONSIVE ============ */
@media (max-width:1080px){
  .hero-grid{grid-template-columns:1fr;gap:36px}
  .ab-2col{grid-template-columns:1fr}
  #lab .fig-cert{aspect-ratio:4/3;max-width:380px}
  .foot-grid{grid-template-columns:1fr 1fr;gap:28px 24px}
  .svc-grid{grid-template-columns:1fr 1fr}
  .ind-grid{grid-template-columns:1fr;align-items:start}
  :root{--range-w:150px}
  .ind-scroll th:nth-child(1){width:48px}
  .ind-photo{aspect-ratio:3/4;min-height:0;height:auto;max-width:440px;margin:0 auto}
}
@media (max-width:840px){
  .main-nav{position:fixed;inset:0;background:var(--green-2);z-index:-1;flex-direction:column;justify-content:flex-start;align-items:flex-start;padding:104px 24px 40px;gap:6px;overflow-y:auto;transform:translateY(-104%);transition:transform .5s cubic-bezier(.22,1,.36,1)}
  .masthead.nav-open .main-nav{transform:none}
  .main-nav a{font-family:var(--disp);font-size:20px;color:var(--white);letter-spacing:.02em;white-space:normal;text-transform:none}
  .main-nav a.active{color:var(--sage)}
  .nav-drop{display:block;width:100%}
  .dropdown{position:static;opacity:1;visibility:visible;transform:none;background:transparent;border:0;box-shadow:none;min-width:0;padding:6px 0 16px 16px;display:grid;gap:2px}
  .dropdown a{font-family:var(--mono);font-size:13px;color:rgba(252,251,247,.65);text-transform:none;letter-spacing:.05em;padding:9px 12px}
  .burger{display:flex}
  .svc-grid{grid-template-columns:1fr}
  .con-list{grid-template-columns:1fr;gap:22px}
  .foot-grid{grid-template-columns:1fr;gap:24px}
  .sec{padding:40px 0}
  .steps{grid-template-columns:1fr 1fr}
  .status-stats{grid-template-columns:1fr 1fr}
  .cta-col{align-items:flex-start}
  .why-grid{grid-template-columns:1fr;gap:22px}
}
@media (max-width:560px){
  :root{--range-w:140px}
  .ind-scroll th:nth-child(1){width:44px}
  .tree{max-width:100%}
  .trunk{left:14px}
  .tl{width:100%;margin-left:0!important;text-align:left!important;padding:0 0 22px 38px}
  .tl .leaf{left:7px!important;right:auto!important}
  .con-item{grid-template-columns:1fr;gap:6px}
}

/* ============ REDUCED MOTION ============ */
@media (prefers-reduced-motion:reduce){
  html{scroll-behavior:auto}
  *,*::before,*::after{animation:none!important;transition:none!important}
  .rv,.mask>span{opacity:1;transform:none}
  .svc-desc,.svc-list{transition:none}
  .trunk{transform:translateX(-50%) scaleY(1)!important}
  .tl{opacity:1;transform:none}
  .tl .leaf{transform:scale(1)}
}
</style>
</head>
<body>

<header class="masthead" id="top">
  <div class="wrap mast-in">
    <a class="brand" href="#top" aria-label="АналитЭко — на главную">
      <span class="logo-slot" title="Место для логотипа">
        <!-- ▼ МЕСТО ДЛЯ ЛОГОТИПА: <img src="путь/к/логотипу.svg" alt="АналитЭко"> -->
        <span class="logo-ph">Лого</span>
      </span>
    </a>
    <nav class="main-nav" id="main-nav" aria-label="Основная навигация">
      <a href="#home">Главная</a>
      <a href="#research">Услуги</a>
      <span class="nav-drop">
        <a href="#air" class="drop-toggle">Мониторинг воздуха</a>
        <div class="dropdown">
          <a href="#air"><i>01</i>Анализ атмосферного воздуха</a>
          <a href="#air"><i>02</i>Измерения шума на границе СЗЗ</a>
        </div>
      </span>
      <span class="nav-drop">
        <a href="#emissions" class="drop-toggle">Контроль выбросов</a>
        <div class="dropdown">
          <a href="#emissions"><i>01</i>Контроль промышленных выбросов</a>
          <a href="#emissions"><i>02</i>Определение эффективности работы ГОУ</a>
          <a href="#emissions"><i>03</i>Обследование источников выбросов</a>
        </div>
      </span>
      <span class="nav-drop">
        <a href="#blog" class="drop-toggle">Исследования и разработки</a>
        <div class="dropdown">
          <a href="#blog"><i>01</i>Научно-прикладные исследования в области экологии</a>
          <a href="#blog"><i>02</i>Решение нестандартных задач в области экологии</a>
          <a href="#blog"><i>03</i>Внедрение методик измерений</a>
        </div>
      </span>
      <span class="nav-drop">
        <a href="#about" class="drop-toggle">О нас</a>
        <div class="dropdown dropdown--about">
          <a href="#about-team"><i>01</i>Команда</a>
          <a href="#about-why"><i>02</i>Почему нас выбирают</a>
          <a href="#about-company"><i>03</i>Компания</a>
          <a href="#about-how"><i>04</i>Как мы работаем</a>
          <a href="#about-faq"><i>05</i>Частые вопросы</a>
        </div>
      </span>
      <a href="#contacts">Контакты</a>
    </nav>
    <button class="burger" id="burger" aria-expanded="false" aria-controls="main-nav" aria-label="Открыть меню"><span></span><span></span><span></span></button>
  </div>
  <div class="scroll-progress" aria-hidden="true"><span id="progress"></span></div>
</header>

<main>
<!-- 1. ГЛАВНАЯ -->
<section id="home" class="hero-sec" aria-labelledby="h-main">
  <div class="wrap hero-grid">
    <div>
      <h1 id="h-main">КОМПЛЕКСНЫЙ МОНИТОРИНГ ВОЗДУХА И ВЫБРОСОВ</h1>
      <p class="lead rv" style="--d:.1s">Проводим точные измерения атмосферного воздуха и промышленных выбросов. Работаем строго по методикам. Выдаем официальные протоколы, которые точно примут контролирующие органы.</p>
      <div class="hero-cta rv" style="--d:.2s">
        <a class="btn btn-primary" href="#contacts">Рассчитать стоимость <span class="ar">→</span></a>
        <a class="btn btn-ghost" href="#research">Все услуги <span class="ar">→</span></a>
      </div>
    </div>
    <!-- ▼ МЕСТО ДЛЯ ИЗОБРАЖЕНИЯ: <img src="путь/к/картинке.jpg" alt="..."> -->
    <figure class="hero-fig rv" style="--d:.18s">
      <div class="fig-slot">
        <svg class="fig-ic" viewBox="0 0 48 48" aria-hidden="true">
          <rect x="6" y="8" width="36" height="28" fill="none" stroke="currentColor" stroke-width="2"/>
          <circle cx="17" cy="18" r="4" fill="none" stroke="currentColor" stroke-width="2"/>
          <path d="M6 34l10-9 8 7 7-6 11 9" fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round"/>
        </svg>
        <span class="fig-label">Место для изображения</span>
        <span class="fig-size">640 × 560</span>
      </div>
    </figure>
  </div>
</section>

<!-- 2. УСЛУГИ -->
<section id="research" class="sec" aria-labelledby="h-research">
  <div class="wrap">
    <header class="sec-head">
      <div>
        <h2 class="sec-title rv-lines rv" id="h-research"><span class="mask"><span>Девять направлений</span></span></h2>
      </div>
      <p class="sec-note rv">наведите, чтобы раскрыть услуги</p>
    </header>

    <div class="svc-grid">
      <div class="svc rv" id="svc-air"><div class="svc-in">
        <h3>Анализ атмосферного воздуха</h3>
        <div class="svc-body">
          <p class="svc-desc">Быстро и качественно проведем анализ воздуха для ПЭК. Знаем все тонкости отбора проб и измерений. Точно определим источник загрязнения с учетом розы ветров. Превратим сухие цифры в наглядные отчеты</p>
          <ul class="svc-list">
            <li><a href="#air">Инструментальные замеры для подтверждения границ СЗЗ</a></li>
            <li><a href="#air">Экологический мониторинг на границе СЗЗ</a></li>
            <li><a href="#air">Ежегодный производственный экологический контроль (ПЭК)</a></li>
            <li><a href="#air">Измерение метеорологических параметров</a></li>
          </ul>
        </div>
      </div></div>

      <div class="svc rv" id="svc-industrial" style="--d:.05s"><div class="svc-in">
        <h3>Контроль промышленных выбросов</h3>
        <div class="svc-body">
          <p class="svc-desc">Проведем замеры даже если высоко и горячо. Заполним отчетность по выбросам. Несем ответственность за результат. Предоставим понятный отчет с рекомендациями</p>
          <ul class="svc-list">
            <li><a href="#emissions">Измерения при инвентаризации выбросов и установлении НДВ</a></li>
            <li><a href="#emissions">Измерения параметров газопылевых потоков</a></li>
            <li><a href="#emissions">Выполнение план-графиков контроля за соблюдением НДВ в рамках ПЭК</a></li>
            <li><a href="#emissions">Параллельные измерения при проверках</a></li>
          </ul>
        </div>
      </div></div>

      <div class="svc rv" id="svc-noise" style="--d:.1s"><div class="svc-in">
        <h3>Измерения шума на границе СЗЗ</h3>
        <div class="svc-body">
          <p class="svc-desc">Измерим шум днем и ночью в сложной акустической обстановке. Проведем прецизионный спектральный анализ шума от конкретных источников с помощью шумомера 1 класса точности</p>
          <ul class="svc-list">
            <li><a href="#air">Измерения шума на границе СЗЗ</a></li>
          </ul>
        </div>
      </div></div>

      <div class="svc rv" id="svc-gou" style="--d:.05s"><div class="svc-in">
        <h3>Определение эффективности работы ГОУ</h3>
        <div class="svc-body">
          <p class="svc-desc">Проведем точные измерения и подготовим акты проверки эффективности. Поможем понять как оптимизировать работу ГОУ, снизить платежи и продлить срок службы оборудования</p>
          <ul class="svc-list">
            <li><a href="#emissions">Оценка эффективности ГОУ</a></li>
            <li><a href="#emissions">Контроль работы пылеуловителей</a></li>
            <li><a href="#emissions">Проверка гидравлического сопротивления</a></li>
          </ul>
        </div>
      </div></div>

      <div class="svc rv" id="svc-sources" style="--d:.1s"><div class="svc-in">
        <h3>Обследование источников выбросов</h3>
        <div class="svc-body">
          <p class="svc-desc">Поможем понять где сделать отверстия на газоходе</p>
          <ul class="svc-list">
            <li><a href="#emissions">Анализ соответствия источников выбросов и мест отбора проб требованиям нормативных документов</a></li>
            <li><a href="#emissions">Подготовка рекомендаций по приведению мест отбора проб в соответствие требованиям</a></li>
          </ul>
        </div>
      </div></div>

      <div class="svc rv" id="svc-applied" style="--d:.15s"><div class="svc-in">
        <h3>Научно-прикладные исследования в области экологии</h3>
        <div class="svc-body">
          <p class="svc-desc">Разработаем и реализуем нестандартные практические подходы и методики</p>
          <ul class="svc-list">
            <li><a href="#blog">Разработка методик определения эффективности систем пылеподавления на открытых площадках хранения инертных грузов</a></li>
            <li><a href="#blog">Инструментальные определения компонентного состава выбросов от открытых площадок хранения инертных грузов</a></li>
          </ul>
        </div>
      </div></div>

      <div class="svc rv" id="svc-nonstandard" style="--d:.05s"><div class="svc-in">
        <h3>Решение нестандартных задач в области экологии</h3>
        <div class="svc-body">
          <p class="svc-desc">Проведем измерения там, где другие не знают как. Поможем понять как снизить выброс и не платить сверхплату</p>
          <ul class="svc-list">
            <li><a href="#blog">Измерения выбросов с поверхностей испарения и емкостей хранения нефтепродуктов</a></li>
            <li><a href="#blog">Определение эффективности работы понтонов в резервуарах</a></li>
            <li><a href="#blog">Измерения на котлах и ГТУ для составления режимных карт</a></li>
            <li><a href="#blog">Измерения на котлах и ГТУ с целью подбора оптимального режима работы при проверках</a></li>
            <li><a href="#blog">Разработка программы испытаний для определения причин аномальных выбросов с целью их снижения</a></li>
          </ul>
        </div>
      </div></div>

      <div class="svc rv" id="svc-methods" style="--d:.1s"><div class="svc-in">
        <h3>Внедрение методик измерений атмосферного воздуха и промышленных выбросов</h3>
        <div class="svc-body">
          <p class="svc-desc">Знаем методики изнутри, поэтому найдем ответы, когда даже разработчик не знает. Подберем подходящее оборудование и материалы</p>
          <ul class="svc-list">
            <li><a href="#blog">Разбор и помощь в верификации методик измерений и отбора проб</a></li>
            <li><a href="#blog">Решение возникающих проблем и вопросов</a></li>
            <li><a href="#blog">Подбор необходимого оборудования и материалов</a></li>
          </ul>
        </div>
      </div></div>

      <div class="svc rv" id="svc-eco" style="--d:.15s"><div class="svc-in">
        <h3>Экологическое проектирование</h3>
        <div class="svc-body">
          <p class="svc-desc">Разработаем и согласуем НДВ и СЗЗ</p>
          <ul class="svc-list">
            <li><a href="#contacts">Инвентаризация источников выбросов</a></li>
            <li><a href="#contacts">Разработка нормативов допустимых выбросов (НДВ)</a></li>
            <li><a href="#contacts">Разработка проекта СЗЗ</a></li>
            <li><a href="#contacts">Разработка мероприятий при НМУ</a></li>
            <li><a href="#contacts">Разработка декларации о воздействии на окружающую среду (ДВОС)</a></li>
          </ul>
        </div>
      </div></div>
    </div>
  </div>
</section>

<!-- 3. ЛАБОРАТОРИЯ (часть блока Услуги) -->
<section id="lab" class="sec" aria-labelledby="h-lab">
  <div class="wrap">
    <header class="sec-head">
      <div>
        <h2 class="sec-title rv-lines rv" id="h-lab"><span class="mask"><span>Лаборатория</span></span></h2>
      </div>
      <p class="sec-note rv">аккредитация RA.RU.21СО07</p>
    </header>
    <div class="ab-2col rv">
      <div class="ab-text" style="max-width:none">
        <h4 class="ab-sub">Аккредитованная экоаналитическая лаборатория</h4>
        <p>Экоаналитическая лаборатория осуществляет комплексные исследования атмосферного воздуха, промышленных выбросов и шума различного уровня сложности. Также лаборатория обеспечивает реализацию аналитической составляющей научно-прикладных исследований в области экологии. Квалифицированные сотрудники и высокоточное оборудование позволяют быть уверенными в высоком качестве и достоверности полученных результатов. Экоаналитическая лаборатория аккредитована национальным органом по аккредитации – Федеральной службой по аккредитации. Уникальный номер записи об аккредитации в реестре аккредитованных лиц <b>RA.RU.21СО07</b>.</p>
      </div>
      <!-- ▼ МЕСТО ДЛЯ ИЗОБРАЖЕНИЯ: аттестат аккредитации <img src="путь/к/аттестату.jpg" alt="Аттестат аккредитации"> -->
      <figure class="fig-slot fig-cert">
        <svg class="fig-ic" viewBox="0 0 48 48" aria-hidden="true">
          <rect x="8" y="6" width="32" height="36" fill="none" stroke="currentColor" stroke-width="2"/>
          <line x1="14" y1="14" x2="34" y2="14" stroke="currentColor" stroke-width="2"/>
          <line x1="14" y1="20" x2="34" y2="20" stroke="currentColor" stroke-width="2"/>
          <line x1="14" y1="26" x2="27" y2="26" stroke="currentColor" stroke-width="2"/>
          <circle cx="30" cy="34" r="5" fill="none" stroke="currentColor" stroke-width="2"/>
        </svg>
        <span class="fig-label">Аттестат аккредитации</span>
      </figure>
    </div>
    <div class="status-stats rv" style="--d:.1s">
      <div class="ss"><b data-count="100">0</b><span>показателей в области аккредитации</span></div>
      <div class="ss"><b data-count="42">0</b><span>методики измерений в области аккредитации</span></div>
      <div class="ss"><b data-count="30000">0</b><span>наш потенциал исследований в год</span></div>
      <div class="ss"><b data-count="69">0</b><span>единиц основных приборов и оборудования</span></div>
    </div>
  </div>
</section>

<!-- 4. МОНИТОРИНГ ВОЗДУХА -->
<section id="air" class="sec" aria-labelledby="h-air">
  <div class="wrap">
    <header class="sec-head">
      <div>
        <h2 class="sec-title rv-lines rv" id="h-air"><span class="mask"><span>Мониторинг воздуха</span></span></h2>
      </div>
    </header>

    <div class="ind-grid">
      <div class="ind-table rv">
        <div class="ind-scroll">
          <table>
            <caption class="sr-only">Измеряемые показатели атмосферного воздуха</caption>
            <colgroup><col class="c-code"><col class="c-name"><col class="c-range"></colgroup>
            <thead><tr><th>Код</th><th>Показатель</th><th>Диапазон измерений</th></tr></thead>
            <tbody>
              <tr>
                <td>0301</td>
                <td><span class="ind-name">Азота диоксид</span><span class="ind-sub">Азота диоксид (двуокись азота; пероксид азота)</span></td>
                <td class="ind-ranges"><span>(0,024 – 0,5) мг/м³</span><span>(0,100 – 10) мг/м³</span></td>
              </tr>
              <tr>
                <td>0304</td>
                <td><span class="ind-name">Азота оксид</span><span class="ind-sub">Азот (II) оксид (Азот монооксид)</span></td>
                <td class="ind-ranges"><span>(0,036 – 2,5) мг/м³</span></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- ▼ МЕСТО ДЛЯ ФОТО: <img src="путь/к/фото.jpg" alt="..."> -->
      <figure class="fig-slot ind-photo rv" style="--d:.1s">
        <svg class="fig-ic" viewBox="0 0 48 48" aria-hidden="true">
          <rect x="6" y="8" width="36" height="28" fill="none" stroke="currentColor" stroke-width="2"/>
          <circle cx="17" cy="18" r="4" fill="none" stroke="currentColor" stroke-width="2"/>
          <path d="M6 34l10-9 8 7 7-6 11 9" fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round"/>
        </svg>
        <span class="fig-label">Место для фото</span>
      </figure>
    </div>

    <div class="cta-col rv" style="--d:.15s">
      <a class="btn btn-primary" href="#contacts">Рассчитать стоимость <span class="ar">→</span></a>
      <p>Просто отправьте нам план-график контроля и мы определим точный объем работ и рассчитаем их стоимость. Остались вопросы или нужна консультация — позвоните или напишите нам прямо сейчас.</p>
    </div>
  </div>
</section>

<!-- 5. КОНТРОЛЬ ВЫБРОСОВ -->
<section id="emissions" class="sec sec-dark" aria-labelledby="h-emissions">
  <div class="wrap">
    <header class="sec-head">
      <div>
        <h2 class="sec-title rv-lines rv" id="h-emissions"><span class="mask"><span>Выбросы — под контролем у самого источника</span></span></h2>
      </div>
    </header>

    <div class="ind-grid">
      <div class="ind-table rv">
        <div class="ind-scroll">
          <table>
            <caption class="sr-only">Измеряемые показатели промышленных выбросов</caption>
            <colgroup><col class="c-code"><col class="c-name"><col class="c-range"></colgroup>
            <thead><tr><th>Код</th><th>Показатель</th><th>Диапазон измерений</th></tr></thead>
            <tbody>
              <tr>
                <td>0301</td>
                <td><span class="ind-name">Азота диоксид</span><span class="ind-sub">Азота диоксид (двуокись азота; пероксид азота)</span></td>
                <td class="ind-ranges"><span>(30 – 500) мг/м³</span></td>
              </tr>
              <tr>
                <td>0304</td>
                <td><span class="ind-name">Азота оксид</span><span class="ind-sub">Азот (II) оксид (Азот монооксид)</span></td>
                <td class="ind-ranges"><span>(25 – 2000) мг/м³</span></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- ▼ МЕСТО ДЛЯ ФОТО: <img src="путь/к/фото.jpg" alt="..."> -->
      <figure class="fig-slot ind-photo rv" style="--d:.1s">
        <svg class="fig-ic" viewBox="0 0 48 48" aria-hidden="true">
          <rect x="6" y="8" width="36" height="28" fill="none" stroke="currentColor" stroke-width="2"/>
          <circle cx="17" cy="18" r="4" fill="none" stroke="currentColor" stroke-width="2"/>
          <path d="M6 34l10-9 8 7 7-6 11 9" fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round"/>
        </svg>
        <span class="fig-label">Место для фото</span>
      </figure>
    </div>

    <div class="cta-col rv" style="--d:.15s">
      <a class="btn btn-primary" href="#contacts">Рассчитать стоимость <span class="ar">→</span></a>
      <p>Просто отправьте нам план-график контроля и мы определим точный объем работ и рассчитаем их стоимость. Остались вопросы или нужна консультация — позвоните или напишите нам прямо сейчас.</p>
    </div>
  </div>
</section>

<!-- 6. ИССЛЕДОВАНИЯ И РАЗРАБОТКИ -->
<section id="blog" class="sec" aria-labelledby="h-blog">
  <div class="wrap">
    <header class="sec-head">
      <div>
        <h2 class="sec-title rv-lines rv" id="h-blog"><span class="mask"><span>Исследования и разработки</span></span></h2>
      </div>
    </header>
    <div class="ph-block rv" style="max-width:920px;border:1px solid var(--line);border-radius:var(--r);background:var(--card);padding:34px 40px;box-shadow:var(--sh-sm)">
      <span class="ph-label mono" style="display:block;font-size:10px;letter-spacing:.2em;text-transform:uppercase;color:var(--muted);opacity:.7;margin-bottom:14px">место для текста</span>
      <span class="skeleton" style="display:block;height:12px;border-radius:6px;background:var(--line);margin:11px 0;width:96%"></span>
      <span class="skeleton" style="display:block;height:12px;border-radius:6px;background:var(--line);margin:11px 0;width:90%"></span>
      <span class="skeleton" style="display:block;height:12px;border-radius:6px;background:var(--line);margin:11px 0;width:93%"></span>
      <span class="skeleton" style="display:block;height:12px;border-radius:6px;background:var(--line);margin:11px 0;width:62%"></span>
    </div>
  </div>
</section>

<!-- 7. О НАС -->
<section id="about" class="sec" aria-labelledby="h-about">
  <div class="wrap">
    <header class="sec-head">
      <div>
        <h2 class="sec-title rv-lines rv" id="h-about"><span class="mask"><span>Команда, которой доверяют</span></span></h2>
      </div>
      <p class="sec-note rv">на рынке с 2026 года</p>
    </header>

    <div class="about-list">
      <article class="ab rv" id="about-team">
        <h3>Команда</h3>
        <div class="ab-text">
          <p>Высокая точность измерений и достоверность результатов зависят от людей, которые проводят измерения.</p>
        </div>
      </article>

      <article class="ab rv" id="about-why" style="--d:.05s">
        <h3>Почему нас выбирают</h3>
        <div class="why-grid">
          <div class="why-col">
            <div class="why-item">
              <h4>Современное оборудование</h4>
              <p>Лаборатория оснащена современным и высокоточным измерительным оборудованием, позволяющим решать множество аналитических и исследовательских задач. Многокомпонентные переносные газоанализаторы, портативные хроматографы и профессиональные метеостанции позволяют проводить точные измерения с максимальной мобильностью.</p>
            </div>
          </div>
          <div class="why-col">
            <div class="why-item">
              <h4>Широкий спектр исследований</h4>
              <p>Наша лаборатория предлагает комплексный контроль качества промышленных выбросов и атмосферного воздуха по более чем 50 показателям. Мы непрерывно развиваемся, осваивая новые методы измерений, внедряя новое оборудование и регулярно повышая квалификацию сотрудников.</p>
            </div>
          </div>
        </div>
      </article>

      <article class="ab rv" id="about-company" style="--d:.1s">
        <h3>Компания</h3>
        <div class="company-text">
          <p>Центр научно-прикладных исследований «АналитЭко» – молодая динамично развивающаяся организация с собственной аккредитованной лабораторией, оказывающая услуги по экологическим измерениям и научно-прикладным исследованиям в области экологии.</p>
        </div>

        <h4 class="ab-sub" style="margin-top:22px">Наша история</h4>
        <div class="tree" id="tree">
          <div class="trunk" id="trunk"></div>
          <div class="tl b-l" data-instant="true"><span class="leaf"></span><div class="tl-card"><b>Октябрь 2026</b><span>Создание сайта и информационного портала Экоаналитической лаборатории</span></div></div>
          <div class="tl b-r" data-instant="true"><span class="leaf"></span><div class="tl-card"><b>Сентябрь 2026</b><span>Успешная аккредитация Экоаналитической лаборатории в Национальной системе аккредитации</span></div></div>
          <div class="tl b-l"><span class="leaf"></span><div class="tl-card"><b>Март 2026</b><span>Создание Экоаналитической лаборатории, подготовка к аккредитации</span></div></div>
          <div class="tl b-r"><span class="leaf"></span><div class="tl-card"><b>Декабрь 2025</b><span>Принятие решения о создании компании ООО «ЦНПИ «АналитЭко»</span></div></div>
        </div>
      </article>

      <article class="ab rv" id="about-how" style="--d:.15s">
        <h3>Как мы работаем</h3>
        <div class="steps">
          <div class="step"><span class="step-num">01</span><h4>Заявка и договор</h4><p>Изучаем заявку, связываемся для согласования объема работ и сроков, направляем коммерческое предложение и заключаем договор</p></div>
          <div class="step"><span class="step-num">02</span><h4>Выезд и отбор проб</h4><p>Проводим отбор проб и измерения в контрольных точках</p></div>
          <div class="step"><span class="step-num">03</span><h4>Лабораторные измерения</h4><p>Проводим анализ отобранных проб и обрабатываем результаты измерений</p></div>
          <div class="step"><span class="step-num">04</span><h4>Протокол испытаний</h4><p>Оформляем протокол испытаний с приложением рекомендаций и направляем вам</p></div>
        </div>
      </article>

      <article class="ab rv" id="about-faq" style="--d:.2s">
        <h3>Частые вопросы</h3>
        <div class="faq">
          <div class="faq-item open">
            <button class="faq-q" aria-expanded="true">Сколько времени занимает подтверждение размеров СЗЗ?<span class="faq-ic"></span></button>
            <div class="faq-a"><div class="faq-a-in"><p>Для подтверждения размеров санитарно-защитной зоны (СЗЗ) требуется проведение длительных натурных исследований атмосферного воздуха и физических факторов (30–50 дней замеров в зависимости от класса опасности объекта). Мы проводим циклические измерения и подготавливаем пакет документов, который гарантированно пройдет экспертизу.</p></div></div>
          </div>
          <div class="faq-item">
            <button class="faq-q" aria-expanded="false">Что делать, если утерян бумажный оригинал протокола испытаний (измерений)?<span class="faq-ic"></span></button>
            <div class="faq-a"><div class="faq-a-in"><p>Если вам срочно нужен бумажный экземпляр с синей печатью, мы бесплатно подготовим дубликат и отправим его вам в день обращения.</p></div></div>
          </div>
        </div>
      </article>
    </div>
  </div>
</section>

<!-- 8. КОНТАКТЫ -->
<section id="contacts" class="sec" aria-labelledby="h-contacts">
  <div class="wrap">
    <header class="sec-head">
      <div>
        <h2 class="sec-title rv-lines rv" id="h-contacts"><span class="mask"><span>Заказать исследование</span></span></h2>
      </div>
    </header>
    <div class="con-list rv">
      <div class="con-item"><span class="k">Телефон</span><span class="v"><a class="js-tel" aria-label="Позвонить нам"></a></span></div>
      <div class="con-item"><span class="k">E-mail</span><span class="v"><a class="js-mail" aria-label="Написать на почту"></a></span></div>
      <div class="con-item"><span class="k">Адрес</span><span class="v">г. Краснодар, ул. Ставропольская, д. 107/10</span></div>
      <div class="con-item"><span class="k">График</span><span class="v">Пн. – Пт., с 08:00 до 17:00<span class="con-sub">Выездная бригада работает 24/7 по согласованию</span></span></div>
    </div>
  </div>
</section>
</main>

<!-- ПОДВАЛ -->
<footer>
  <div class="wrap">
    <div class="foot-grid">
      <div class="foot-brand">
        <a class="brand" href="#top">
          <span class="logo-slot" title="Место для логотипа"><span class="logo-ph">Лого</span></span>
          <span class="brand-text"><strong>АналитЭко</strong><small>лаборатория</small></span>
        </a>
        <p class="foot-acc"><a href="https://pub.fsa.gov.ru/ral/view/39037/accredited-entity" target="_blank" rel="noopener">Уникальный номер записи об аккредитации в реестре аккредитованных лиц <b>RA.RU.21СО07</b> · ООО «ЦНПИ» АналитЭко</a></p>
        <p class="foot-copy">© 2026 ООО «ЦНПИ» АналитЭко</p>
      </div>
      <div class="fcol">
        <h4>Услуги</h4>
        <ul>
          <li><a href="#research">Все услуги</a></li>
          <li><a href="#lab">Лаборатория</a></li>
        </ul>
      </div>
      <div class="fcol">
        <h4>Контакты</h4>
        <a class="mono js-tel" aria-label="Позвонить нам"></a>
        <a class="mono js-mail" aria-label="Написать на почту"></a>
      </div>
    </div>
    <div class="foot-bot"><a href="#top" id="to-top">Наверх ↑</a></div>
  </div>
</footer>

<script>
(function(){
  "use strict";
  var RM = matchMedia('(prefers-reduced-motion: reduce)').matches;
  var $  = function(s,c){ return (c||document).querySelector(s); };
  var $$ = function(s,c){ return Array.prototype.slice.call((c||document).querySelectorAll(s)); };

  /* КОНТАКТЫ (защита от ботов: собираем на лету) */
  var TEL = ['+7','(918)','264-26-27'].join(' ');
  var MAIL = ['analiteco','@','mail','.ru'].join('');
  var TEL_HREF = 'tel:' + ['+7','918','264','26','27'].join('');
  $$('.js-tel').forEach(function(a){ a.textContent = TEL; a.href = TEL_HREF; });
  $$('.js-mail').forEach(function(a){ a.textContent = MAIL; a.href = 'mailto:' + MAIL; });

  /* «Наверх» */
  $$('a[href="#top"]').forEach(function(a){
    a.addEventListener('click', function(e){
      e.preventDefault();
      window.scrollTo({top:0, behavior: RM ? 'auto' : 'smooth'});
    });
  });

  /* бургер */
  var burger = $('#burger'), mast = $('.masthead');
  burger.addEventListener('click', function(){
    var open = mast.classList.toggle('nav-open');
    burger.setAttribute('aria-expanded', open);
    document.body.style.overflow = open ? 'hidden' : '';
  });
  $$('#main-nav a').forEach(function(a){
    a.addEventListener('click', function(){
      mast.classList.remove('nav-open');
      burger.setAttribute('aria-expanded','false');
      document.body.style.overflow = '';
    });
  });

  /* тень + прогресс */
  var prog = $('#progress');
  addEventListener('scroll', function(){
    mast.classList.toggle('scrolled', scrollY > 10);
    var h = document.documentElement;
    var p = h.scrollTop / (h.scrollHeight - h.clientHeight || 1);
    prog.style.transform = 'scaleX(' + p + ')';
  }, {passive:true});

  /* scrollspy — #lab маппится на #research */
  var navLinks = $$('#main-nav > a, #main-nav .drop-toggle');
  var spy = new IntersectionObserver(function(es){
    es.forEach(function(e){
      if(e.isIntersecting){
        var id = e.target.id;
        if(id === 'lab') id = 'research';
        navLinks.forEach(function(a){ a.classList.toggle('active', a.getAttribute('href') === '#' + id); });
      }
    });
  }, {rootMargin:'-40% 0px -55% 0px'});
  ['home','research','lab','air','emissions','blog','about','contacts'].forEach(function(id){
    var s = document.getElementById(id); if(s) spy.observe(s);
  });

  /* reveal */
  var io = new IntersectionObserver(function(es){
    es.forEach(function(e){ if(e.isIntersecting){ e.target.classList.add('on'); io.unobserve(e.target); } });
  }, {threshold:.15, rootMargin:'0px 0px -40px'});
  $$('.rv').forEach(function(el){ io.observe(el); });

  /* счётчики */
  var ioCnt = new IntersectionObserver(function(es){
    es.forEach(function(e){
      if(!e.isIntersecting) return;
      ioCnt.unobserve(e.target);
      var el = e.target, to = +el.dataset.count;
      if(RM){ el.textContent = to.toLocaleString('ru-RU'); return; }
      var t0 = performance.now(), dur = 1500;
      (function step(t){
        var k = Math.min(1, (t - t0) / dur);
        el.textContent = Math.round(to * (1 - Math.pow(1 - k, 3))).toLocaleString('ru-RU');
        if(k < 1) requestAnimationFrame(step);
      })(t0);
    });
  }, {threshold:.6});
  $$('[data-count]').forEach(function(el){ ioCnt.observe(el); });

  /* услуги: тап на тач */
  if(matchMedia('(hover: none)').matches){
    $$('.svc-in').forEach(function(card){
      card.addEventListener('click', function(e){
        if(e.target.closest('a')) return;
        card.classList.toggle('show-svc');
      });
    });
  }

  /* FAQ */
  $$('.faq-q').forEach(function(btn){
    btn.addEventListener('click', function(){
      var item = btn.closest('.faq-item');
      var open = item.classList.toggle('open');
      btn.setAttribute('aria-expanded', open);
    });
  });

  /* ДЕРЕВО ИСТОРИИ — двухфазное появление.
     Фаза 1: дерево вошло во вьюпорт → сразу Октябрь и Сентябрь, ствол до Сентября.
     Фаза 2: Март и Декабрь проявляются по мере того, как ИХ САМИ вводит в зону видимости. */
  var tree = $('#tree');
  if(tree){
    var trunk = $('#trunk');
    var tls = $$('.tl', tree);
    var instant = tls.filter(function(t){ return t.hasAttribute('data-instant'); });
    var scrollItems = tls.filter(function(t){ return !t.hasAttribute('data-instant'); });

    function leafFrac(item){
      var tr = tree.getBoundingClientRect();
      var leaf = item.querySelector('.leaf');
      if(!leaf || !tr.height) return 1;
      var lr = leaf.getBoundingClientRect();
      var f = (lr.top + lr.height / 2 - tr.top) / tr.height;
      return Math.max(0.02, Math.min(1, f));
    }
    function growTrunk(f, animate){
      trunk.style.transition = (animate && !RM) ? 'transform .6s cubic-bezier(.22,1,.36,1)' : 'none';
      trunk.style.transform = 'translateX(-50%) scaleY(' + f + ')';
    }

    if(RM){
      trunk.style.transform = 'translateX(-50%) scaleY(1)';
      tls.forEach(function(t){ t.classList.add('on'); });
    } else {
      var maxF = 0;
      var phase2 = false;

      function revealInstant(){
        instant.forEach(function(t){ t.classList.add('on'); });
        if(instant.length){
          var f = leafFrac(instant[instant.length - 1]);
          maxF = Math.max(maxF, f);
          growTrunk(maxF, true);
        }
      }

      function checkScrollItems(){
        if(!phase2) return;
        var line = innerHeight * 0.9;
        scrollItems.forEach(function(item){
          if(item.classList.contains('on')) return;
          var r = item.getBoundingClientRect();
          if(r.top < line && r.bottom > 0){
            item.classList.add('on');
            var f = leafFrac(item);
            if(f > maxF){ maxF = f; growTrunk(maxF, true); }
          }
        });
      }

      var treeIO = new IntersectionObserver(function(es){
        es.forEach(function(e){
          if(e.isIntersecting){
            revealInstant();
            phase2 = true;
            checkScrollItems();
            treeIO.disconnect();
          }
        });
      }, {threshold:0.12});
      treeIO.observe(tree);

      var ticking = false;
      function onMove(){
        if(!ticking){
          requestAnimationFrame(function(){ checkScrollItems(); ticking = false; });
          ticking = true;
        }
      }
      addEventListener('scroll', onMove, {passive:true});
      addEventListener('resize', onMove, {passive:true});
    }
  }
})();
</script>
</body>
</html>
