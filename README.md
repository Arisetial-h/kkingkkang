<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>WALL ST. — 아메리칸 드림의 해부학</title>
<style>
  :root{
    --bone:#EFEAE1;
    --ink:#0E0D0C;
    --ink-2:#403c37;
    --red:#E23A15;
    --line:rgba(14,13,12,.20);
    --serif:"Times New Roman",Times,Georgia,serif;
    --sans:system-ui,-apple-system,"Helvetica Neue",Helvetica,"Apple SD Gothic Neo","Nanum Gothic",sans-serif;
  }
  *{box-sizing:border-box}
  html,body{margin:0;padding:0}
  body{background:var(--bone);color:var(--ink);font-family:var(--sans);-webkit-font-smoothing:antialiased;overflow-x:hidden}
  .wrap{max-width:1240px;margin:0 auto;padding:0 24px}
  img{display:block;width:100%;height:100%;object-fit:cover}

  /* 공통 이미지 처리 : 듀오톤 + 비네트 */
  .frame{position:relative;overflow:hidden;background:var(--ink)}
  /* ── 이미지 슬롯 : 실제 파일은 나중에 삽입 ── */
  .slot{display:flex;align-items:flex-end;justify-content:flex-start;
    background:repeating-linear-gradient(45deg,#1a1917 0 10px,#141312 10px 20px);
    border:1px solid rgba(239,234,225,.20)}
  .slot .tagname{font-size:9.5px;letter-spacing:.2em;text-transform:uppercase;
    color:rgba(239,234,225,.5);padding:12px 14px;line-height:1.7}
  .slot .tagname b{color:var(--red);display:block;letter-spacing:.24em}
  .slot::after{display:none}
  .frame img{filter:grayscale(1) contrast(1.08) brightness(.96)}
  .frame.warm img{filter:grayscale(1) sepia(.42) contrast(1.06) saturate(1.5) brightness(.98)}
  .frame::after{ /* 비네트 */
    content:"";position:absolute;inset:0;pointer-events:none;
    background:radial-gradient(120% 90% at 50% 40%,rgba(0,0,0,0) 38%,rgba(0,0,0,.55) 100%);
    mix-blend-mode:multiply;
  }
  .grain{position:fixed;inset:0;pointer-events:none;z-index:60;opacity:.30;
    background-image:url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='140' height='140'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='3'/></filter><rect width='140' height='140' filter='url(%23n)' opacity='.5'/></svg>");
    mix-blend-mode:multiply;}

  /* ── 러너 / 티커 ─────────────────────────── */
  .runner{position:relative;z-index:20;border-bottom:1px solid rgba(239,234,225,.28);
    font-size:10.5px;letter-spacing:.24em;text-transform:uppercase;color:rgba(239,234,225,.82);
    display:flex;justify-content:space-between;gap:16px;padding:16px 0;flex-wrap:wrap}
  .runner .red{color:var(--red)}

  /* ── HERO : 풀블리드 사진 + 초대형 타이포 겹침 ─ */
  .hero{position:relative;min-height:104vh;display:flex;flex-direction:column;justify-content:space-between;background:#0B0A09;overflow:hidden}
  .hero-bg{position:absolute;inset:0}
  .hero-bg img{filter:grayscale(.72) contrast(1.15) brightness(.62) saturate(1.25)}
  .hero-bg::after{content:"";position:absolute;inset:0;
    background:
      linear-gradient(180deg,rgba(11,10,9,.86) 0%,rgba(11,10,9,.28) 34%,rgba(11,10,9,.55) 68%,rgba(11,10,9,.97) 100%),
      radial-gradient(105% 80% at 50% 45%,rgba(0,0,0,0) 30%,rgba(0,0,0,.72) 100%);}
  .hero-inner{position:relative;z-index:15;padding:0 24px;max-width:1240px;margin:0 auto;width:100%;flex:1;
    display:flex;flex-direction:column;justify-content:center}
  .kicker{font-size:11px;letter-spacing:.34em;text-transform:uppercase;color:rgba(239,234,225,.72);margin-bottom:.9em}
  .mega{
    font-weight:800;text-transform:uppercase;margin:0;color:var(--bone);
    font-size:clamp(64px,22.5vw,368px);line-height:.78;letter-spacing:-.055em;
    word-break:keep-all;overflow-wrap:normal;
    text-shadow:0 18px 60px rgba(0,0,0,.55);
  }
  .mega .ghost{color:transparent;-webkit-text-stroke:2px rgba(239,234,225,.62)}
  .mega .red{color:var(--red)}
  .mega .row2{display:block;margin-left:.06em}
  /* 사진 위로 걸치는 세로 라벨 */
  .vlabel{position:absolute;right:24px;top:50%;transform:translateY(-50%) rotate(180deg);writing-mode:vertical-rl;
    font-size:10.5px;letter-spacing:.4em;text-transform:uppercase;color:rgba(239,234,225,.55);z-index:16}
  .hero-foot{position:relative;z-index:15;border-top:1px solid rgba(239,234,225,.28)}
  .hero-foot .wrap{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px 14px;padding:16px 24px;
    font-size:10.5px;letter-spacing:.2em;text-transform:uppercase;color:rgba(239,234,225,.7)}
  .hero-foot .red{color:var(--red)}
  /* 스크롤 큐 : 히어로 본문 흐름 안에 배치 (겹침 방지) */
  .scrollcue{display:inline-flex;align-items:center;gap:10px;margin-top:clamp(22px,4vw,44px);
    font-size:10.5px;letter-spacing:.26em;text-transform:uppercase;color:var(--red)}
  .scrollcue::before{content:"";width:clamp(28px,7vw,64px);height:1px;background:var(--red);opacity:.8}

  /* ── 서론 : 스티키 사진 + 드롭캡 본문 ───────── */
  .lede{display:grid;grid-template-columns:.9fr 1.35fr;gap:56px;padding:78px 0 88px;align-items:start}
  .lede .visual{position:sticky;top:32px}
  .lede .frame{aspect-ratio:3/4}
  .lede .cap{margin-top:10px;font-size:10.5px;letter-spacing:.2em;text-transform:uppercase;color:var(--ink-2)}
  .lede h2{font-family:var(--serif);font-weight:400;font-style:italic;
    font-size:clamp(34px,4.6vw,64px);line-height:1.0;margin:0 0 28px;letter-spacing:-.015em}
  .lede p{font-size:17px;line-height:1.9;margin:0 0 1.05em;color:var(--ink-2);max-width:62ch}
  .lede p:first-of-type::first-letter{float:left;font-family:var(--serif);font-size:92px;line-height:.74;
    padding:8px 14px 0 0;color:var(--ink)}
  .dropnote{display:block;margin-top:32px;font-size:10.5px;letter-spacing:.24em;text-transform:uppercase;color:var(--red)}

  /* ── 섹션 헤드 ───────────────────────────── */
  section{border-top:1px solid var(--line)}
  .sec-head{display:flex;align-items:flex-end;justify-content:space-between;gap:28px;padding:34px 0 14px;flex-wrap:wrap}
  .num{font-weight:800;font-size:clamp(64px,10.5vw,158px);line-height:.76;letter-spacing:-.06em}
  .sec-title{font-weight:800;font-size:clamp(32px,5.4vw,72px);line-height:.9;letter-spacing:-.04em;text-transform:uppercase;margin:0}
  .sec-tag{font-size:10.5px;letter-spacing:.24em;text-transform:uppercase;color:var(--ink-2)}

  /* 01 : 사진 위에 숫자 겹치기 */
  .overlap{position:relative;margin-top:8px}
  .overlap .frame{aspect-ratio:16/9}
  .overlap .stamp{position:absolute;left:-.03em;bottom:-.10em;z-index:5;
    font-weight:800;font-size:clamp(120px,21vw,300px);line-height:.72;letter-spacing:-.06em;
    color:var(--bone);mix-blend-mode:difference;pointer-events:none}
  .overlap .onphoto{position:absolute;right:26px;top:26px;z-index:6;max-width:22ch;color:var(--bone);
    font-size:12px;letter-spacing:.06em;line-height:1.75;text-shadow:0 2px 18px rgba(0,0,0,.8)}
  .overlap .onphoto b{display:block;font-size:11px;letter-spacing:.22em;text-transform:uppercase;color:var(--red);margin-bottom:8px}

  .cols{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));border-top:1px solid var(--ink);margin-top:42px}
  .cell{padding:22px 24px 30px;border-right:1px solid var(--line)}
  .cell:last-child{border-right:0}
  .cell h4{font-size:12.5px;letter-spacing:.16em;text-transform:uppercase;margin:0 0 12px}
  .cell p{font-size:14.5px;line-height:1.8;color:var(--ink-2);margin:0}
  .facts{display:grid;grid-template-columns:repeat(auto-fit,minmax(190px,1fr));gap:1px;background:var(--line);border-top:1px solid var(--ink);margin-top:0}
  .fact{background:var(--bone);padding:22px 20px 26px}
  .fact b{display:block;font-size:clamp(34px,4.8vw,60px);letter-spacing:-.045em;line-height:1}
  .fact span{display:block;margin-top:10px;font-size:11px;letter-spacing:.16em;text-transform:uppercase;color:var(--ink-2)}

  /* ── 풀블리드 인용 밴드 : 사진 + 텍스트 겹침 ── */
  .band{position:relative;min-height:86vh;display:flex;align-items:center;border-top:0;overflow:hidden;background:#111}
  .band .bg{position:absolute;inset:0}
  .band .bg img{filter:contrast(1.1) saturate(1.15) brightness(.82)}
  .band .bg::after{content:"";position:absolute;inset:0;
    background:radial-gradient(90% 75% at 30% 50%,rgba(0,0,0,.72) 0%,rgba(0,0,0,.30) 55%,rgba(0,0,0,.82) 100%)}
  .band .wrap{position:relative;z-index:5}
  .band .tag{font-size:10.5px;letter-spacing:.3em;text-transform:uppercase;color:rgba(239,234,225,.72)}
  .band blockquote{margin:18px 0 0;color:var(--bone);font-family:var(--serif);font-style:italic;
    font-size:clamp(32px,6vw,86px);line-height:1.0;letter-spacing:-.02em;max-width:20ch;
    text-shadow:0 10px 44px rgba(0,0,0,.7)}
  .band blockquote em{color:#FF6A3D;font-style:italic}
  .band .src{margin-top:26px;font-size:11px;letter-spacing:.22em;text-transform:uppercase;color:rgba(239,234,225,.6)}

  /* ── 02 개츠비 : 다크 + 오프셋 이미지 그리드 ── */
  .dark{background:var(--ink);color:var(--bone)}
  .dark .sec-tag{color:rgba(239,234,225,.62)}
  .dark .cell p{color:rgba(239,234,225,.68)}
  .dark .cell{border-color:rgba(239,234,225,.20)}
  .dark .cols{border-top-color:rgba(239,234,225,.5)}
  .gats{display:grid;grid-template-columns:1.05fr 1fr;gap:34px;align-items:end;margin-top:18px}
  .gats .a{position:relative}
  .gats .a .frame{aspect-ratio:3/4}
  .gats .a .over{position:absolute;left:-26px;bottom:34px;z-index:5;background:var(--red);color:#fff;
    padding:12px 18px;font-size:11px;letter-spacing:.2em;text-transform:uppercase}
  .gats .b{display:grid;gap:26px}
  .gats .b .frame{aspect-ratio:4/3}
  .gats .b .lead{font-family:var(--serif);font-style:italic;font-size:clamp(22px,2.7vw,38px);line-height:1.15;margin:0}
  .gats .b .lead span{color:#FF6A3D}
  .cap-d{margin-top:10px;font-size:10.5px;letter-spacing:.2em;text-transform:uppercase;color:rgba(239,234,225,.55)}

  /* ── 03 맛집 : 최하위 위계 (작게, 조밀하게) ── */
  .minor{padding:44px 0 54px}
  .minor-head{display:flex;align-items:baseline;gap:18px;border-bottom:1px solid var(--ink);padding-bottom:10px;flex-wrap:wrap}
  .minor-head .n{font-size:11px;letter-spacing:.2em;color:var(--red)}
  .minor-head h3{margin:0;font-size:15px;letter-spacing:.2em;text-transform:uppercase;font-weight:800}
  .minor-head .t{font-size:10.5px;letter-spacing:.2em;text-transform:uppercase;color:var(--ink-2);margin-left:auto}
  .minor-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:1px;background:var(--line);margin-top:1px}
  .m-item{background:var(--bone);padding:14px 16px 18px}
  .m-item .yr{font-size:9.5px;letter-spacing:.2em;color:var(--red)}
  .m-item h5{margin:6px 0 2px;font-size:15.5px;letter-spacing:-.01em;font-weight:700}
  .m-item .adr{font-size:9.5px;letter-spacing:.18em;text-transform:uppercase;color:var(--ink-2)}
  .m-item p{margin:8px 0 0;font-size:12px;line-height:1.68;color:var(--ink-2)}

  /* 아카이브 썸네일 스트립 */
  .strip{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:12px;margin-top:34px}
  .strip .frame{aspect-ratio:3/4}
  .strip figcaption{margin-top:7px;font-size:9.5px;letter-spacing:.18em;text-transform:uppercase;color:var(--ink-2)}
  .strip figure{margin:0}

  footer{border-top:3px solid var(--ink);padding:26px 0 66px;display:flex;justify-content:space-between;gap:20px;
    flex-wrap:wrap;font-size:10.5px;letter-spacing:.22em;text-transform:uppercase;color:var(--ink-2)}

  /* ══════════ MOBILE TYPOGRAPHY ══════════ */
  @media (max-width:700px){
    .wrap{padding:0 18px}
    /* 자간 과다 방지 : 라벨류 트래킹 축소 */
    .runner,.hero-foot .wrap,.sec-tag,.kicker,.scrollcue,.vlabel,
    .dropnote,.cap,.cap-d,.fact span,.cell h4,.minor-head h3,
    .minor-head .t,.m-item .adr,.m-item .yr,.strip figcaption,
    .band .tag,.band .src,.dos-top,.fields dt,.tagwrap h6,.dos-foot,footer{letter-spacing:.14em}
    .kicker{letter-spacing:.2em;font-size:10px;line-height:1.7}

    .hero{min-height:100svh}
    .hero-inner{padding:0 18px}
    .mega{font-size:23vw;line-height:.82;letter-spacing:-.045em}
    .mega .ghost{-webkit-text-stroke:1.2px rgba(239,234,225,.66)}
    .runner{font-size:9.5px;gap:6px;padding:12px 0;flex-direction:column}
    /* 하단 메타 : 2열 고정 — 세로 나열로 흐트러지지 않게 */
    .hero-foot .wrap{grid-template-columns:1fr 1fr;font-size:9.5px;padding:12px 18px 14px}
    .hero-foot .wrap span:nth-child(4){grid-column:1/-1}

    .num{font-size:clamp(52px,17vw,88px)}
    .sec-title{font-size:clamp(28px,10.5vw,44px);line-height:.94;letter-spacing:-.03em}
    .sec-head{gap:12px;padding-top:26px}
    .lede h2{font-size:clamp(28px,9vw,40px);line-height:1.08}
    .lede p{font-size:15.5px;line-height:1.85}
    .lede p:first-of-type::first-letter{font-size:66px;padding:6px 10px 0 0}
    .overlap .stamp{font-size:26vw;bottom:-.06em}
    .band{min-height:74svh}
    .band blockquote{font-size:clamp(28px,8.6vw,44px);line-height:1.12;max-width:none}
    .gats .b .lead{font-size:clamp(21px,7vw,32px);line-height:1.2}
    .fact b{font-size:clamp(30px,10vw,44px)}

    /* 개츠비 프로필 : 두 행 충돌 방지 */
    .dossier{padding-top:44px}
    .dos-top{flex-direction:column;gap:5px;font-size:9.5px}
    .dos-name{font-size:19vw;line-height:.92;letter-spacing:-.045em}
    .dos-name .hollow{-webkit-text-stroke:1.1px var(--ink)}
    .dos-name .l2{margin-left:0}
    .dos-body{font-size:13px;line-height:1.85}
    .tags span{font-size:10.5px;padding:4px 9px}
    .fields{grid-template-columns:74px 1fr;font-size:12px}
    .dos-foot{flex-direction:column;gap:5px}

    .minor-head h3{font-size:13px}
    footer{flex-direction:column;gap:8px}
  }
  @media (max-width:380px){
    .mega{font-size:21.5vw}
    .dos-name{font-size:17.5vw}
    .hero-foot .wrap{grid-template-columns:1fr}
  }


  /* ══ GATSBY PROFILE / DOSSIER ══ */
  .dossier{position:relative;background:#F2EEE6;color:var(--ink);overflow:hidden;padding:66px 0 0}
  .dossier .graph{position:absolute;inset:0;pointer-events:none;opacity:.55;
    background-image:
      linear-gradient(to right,rgba(14,13,12,.10) 1px,transparent 1px),
      linear-gradient(to bottom,rgba(14,13,12,.10) 1px,transparent 1px),
      linear-gradient(to right,rgba(14,13,12,.045) 1px,transparent 1px),
      linear-gradient(to bottom,rgba(14,13,12,.045) 1px,transparent 1px);
    background-size:96px 96px,96px 96px,16px 16px,16px 16px}
  .dossier .wrap{position:relative;z-index:4}
  .dos-top{display:flex;justify-content:space-between;gap:16px;flex-wrap:wrap;
    font-size:10.5px;letter-spacing:.24em;text-transform:uppercase;color:var(--ink-2);
    border-bottom:1px solid var(--ink);padding-bottom:10px}
  .dos-top .red{color:var(--red)}

  .dos-stage{position:relative;margin-top:28px;padding-bottom:34px}
  .dos-name{position:relative;z-index:2;font-weight:800;text-transform:uppercase;margin:0;
    font-size:clamp(56px,15.5vw,226px);line-height:.79;letter-spacing:-.055em}
  .dos-name .l2{display:block;margin-left:.02em}
  .dos-name .hollow{color:transparent;-webkit-text-stroke:1.8px var(--ink)}
  .dos-name .red{color:var(--red)}

  /* 누끼 슬롯 : 이름 위로 올라타고 본문 위를 덮음 */
  .cutout{position:absolute;right:-1.5%;top:-9%;width:clamp(260px,44%,540px);height:118%;z-index:3;
    filter:drop-shadow(-24px 24px 32px rgba(14,13,12,.32))}
  .cutout img{width:100%;height:100%;object-fit:contain;object-position:bottom}
  .cutout .slotbox{width:100%;height:100%;border:1px dashed rgba(14,13,12,.45);
    background:repeating-linear-gradient(45deg,rgba(14,13,12,.055) 0 12px,rgba(14,13,12,.015) 12px 24px);
    display:flex;align-items:flex-end;padding:14px}
  .cutout .slotbox span{font-size:10px;letter-spacing:.2em;text-transform:uppercase;color:var(--ink-2);line-height:1.85}
  .cutout .slotbox b{display:block;color:var(--red);letter-spacing:.24em;margin-bottom:4px}

  /* 본문 : 이름 아래로 파고들어 겹침 */
  .dos-body{position:relative;z-index:1;margin-top:-1.1em;max-width:min(60ch,54%);
    column-count:2;column-gap:26px;font-size:12.5px;line-height:1.8;color:var(--ink-2)}
  .dos-body p{margin:0 0 .9em}
  .dos-body p:first-child::first-letter{font-weight:800;font-size:17px;color:var(--ink)}

  .stampline{position:absolute;left:1%;bottom:2%;z-index:5;transform:rotate(-6.5deg);
    border:2px solid var(--red);color:var(--red);padding:6px 14px;
    font-size:11px;letter-spacing:.28em;text-transform:uppercase;opacity:.9;background:rgba(242,238,230,.55)}

  .dos-meta{position:relative;z-index:4;display:grid;grid-template-columns:1.1fr 1fr;gap:36px;
    border-top:1px solid var(--ink);margin-top:12px;padding:22px 0 0}
  .fields{display:grid;grid-template-columns:88px 1fr;row-gap:9px;column-gap:18px;font-size:12.5px;line-height:1.6;margin:0}
  .fields dt{font-size:9.5px;letter-spacing:.2em;text-transform:uppercase;color:var(--ink-2);padding-top:3px}
  .fields dd{margin:0;font-weight:700}
  .tagwrap h6{margin:0 0 12px;font-size:9.5px;letter-spacing:.24em;text-transform:uppercase;color:var(--ink-2)}
  .tags{display:flex;flex-wrap:wrap;gap:7px}
  .tags span{border:1px solid var(--ink);padding:5px 11px;font-size:11px;letter-spacing:.08em;white-space:nowrap}
  .tags span.fill{background:var(--ink);color:var(--bone)}
  .tags span.hot{border-color:var(--red);color:var(--red)}
  .dos-foot{position:relative;z-index:4;border-top:1px solid var(--line);margin-top:28px;padding:12px 0 44px;
    display:flex;justify-content:space-between;gap:14px;flex-wrap:wrap;
    font-size:9.5px;letter-spacing:.2em;text-transform:uppercase;color:var(--ink-2)}

  @media (max-width:900px){
    .cutout{position:relative;right:auto;top:auto;width:100%;height:auto;aspect-ratio:3/4;margin-top:18px;left:0}
    .dos-body{max-width:100%;column-count:1;margin-top:22px}
    .dos-meta{grid-template-columns:1fr}
    .stampline{position:static;display:inline-block;margin-top:20px;transform:rotate(-3deg)}
  }

  @media (max-width:900px){
    .lede{grid-template-columns:1fr;gap:26px;padding-top:44px}
    .lede .visual{position:static}
    .gats{grid-template-columns:1fr}
    .gats .a .over{left:0}
    .cell{border-right:0;border-bottom:1px solid var(--line)}
    .overlap .onphoto{display:none}
    .vlabel{display:none}
  }
</style>
</head>
<body>
<div class="grain"></div>

<!-- ══ HERO ══ -->
<header class="hero">
  <div class="hero-bg"></div><!-- SLOT/HERO : 로어 맨해튼 스카이라인 (풀블리드, 16:9 이상 권장) -->
  <div class="wrap"><div class="runner">
    <span>NEW YORK STOCK EXCHANGE — 11 WALL ST</span>
    <span>ISSUE 07</span>
    <span class="red">MONEY IS LANGUAGE</span>
  </div></div>
  <div class="hero-inner">
    <span class="kicker">한 블록 반의 거리, 세계의 절반</span>
    <h1 class="mega">WALL<span class="red">ST</span><span class="row2 ghost">DREAM</span></h1>
    <span class="scrollcue">↓ SCROLL &nbsp;CH. 01—04</span>
  </div>
  <span class="vlabel">AMERICAN DREAM / ANATOMY OF A PROMISE</span>
  <div class="hero-foot"><div class="wrap">
    <span>LOWER MANHATTAN</span>
    <span>1653 — PRESENT</span>
    <span>0.7 MILE</span>
    <span class="red">EDITORIAL LONG READ</span>
  </div></div>
</header>

<!-- ══ 서론 (위치 확정) ══ -->
<div class="wrap">
  <div class="lede">
    <div class="visual">
      <div class="frame slot"><span class="tagname"><b>SLOT / LEDE</b>WALL ST 표지판 · 3:4 세로</span></div>
      <div class="cap">Fig. 01 — WALL ST &amp; BROAD ST, 표지판</div>
    </div>
    <div class="body">
      <h2>서론<br>— 벽이었던 길,<br>길이 된 벽</h2>
      <p>월 스트리트는 지도에서 놀랄 만큼 짧다. 브로드웨이에서 이스트 리버까지, 걸어서 십 분이면 끝나는 0.7마일의 골목이다. 그런데 이 골목의 이름은 도시의 이름보다 더 자주 불린다.</p>
      <p>이름의 기원은 방어벽이다. 17세기 네덜란드인들이 뉴암스테르담을 지키려 세운 목책(wall)이 이 거리의 원형이었다. 벽은 사라졌지만 기능은 남았다. 안과 밖을 가르는 선, 들어온 자와 남겨진 자를 가르는 선.</p>
      <p>1792년, 스물넷의 상인들이 플라타너스 나무 아래에서 협정을 맺는다. 뉴욕 증권거래소의 시작이었다. 그 뒤로 이 좁은 길은 미국이 스스로를 설명하는 방식이 되었다. 노력하면 오를 수 있다는 문장, 즉 아메리칸 드림 말이다.</p>
      <p>하지만 이 거리는 그 문장의 증거이면서 동시에 반증이다. 1929년 10월의 폭락, 1987년 블랙 먼데이, 2008년 리먼의 붕괴. 상승의 신화는 늘 같은 자리에서 무너졌고, 같은 자리에서 다시 세워졌다.</p>
      <p>그래서 우리는 이 길을 세 겹으로 읽는다. 돈의 역사로서의 월 스트리트, 소설이 기록한 꿈의 형태로서의 개츠비, 그리고 그 사이에서 오늘도 점심을 먹는 사람들의 거리로서의 다운타운.</p>
      <p>아래의 장(章)들은 그 세 겹을 차례로 벗겨낸다. 결론은 마지막에 두었다. 이 거리가 그랬듯이.</p>
      <span class="dropnote">↓ CHAPTER 01 — THE STREET</span>
    </div>
  </div>
</div>

<!-- ══ 01 ══ -->
<section>
  <div class="wrap">
    <div class="sec-head">
      <div class="num">01</div>
      <h3 class="sec-title">돈이 세워<br>올린 협곡</h3>
      <span class="sec-tag">THE STREET / 1653 — NOW</span>
    </div>
    <div class="overlap">
      <div class="frame slot" style="min-height:340px"><span class="tagname"><b>SLOT / CH.01</b>c.1900 NYSE 거리 흑백 · 16:9</span></div>
      <div class="onphoto"><b>Fig. 02 — c.1900</b>코린트식 기둥 여섯 개가 떠받친 NYSE 본관. 금융을 신전의 형식으로 지은 순간, 시장은 종교의 표정을 얻었다.</div>
      <span class="stamp">1792</span>
    </div>
    <div class="cols">
      <div class="cell"><h4>1792 · 버튼우드 협정</h4><p>24명의 중개인이 수수료율과 거래 우선권을 약속한 두 문장짜리 문서. 오늘날 수십조 달러 시장의 헌법이 되었다.</p></div>
      <div class="cell"><h4>1903 · 그리스 신전의 얼굴</h4><p>브로드 스트리트 18번지에 세워진 본관. 파사드의 조각은 「인간의 노동을 보호하는 성실」이라는 이름을 갖고 있다.</p></div>
      <div class="cell"><h4>1929 · 검은 화요일</h4><p>사흘 만에 시장의 4분의 1이 사라졌다. 대공황은 아메리칸 드림이 상승만 하는 직선이 아님을 증명한 첫 대규모 실험이었다.</p></div>
      <div class="cell"><h4>1989 · 돌진하는 황소</h4><p>조각가 아르투로 디 모디카가 허가 없이 밤중에 놓고 간 3,200kg의 청동 황소. 시는 철거하려 했고, 시민들은 남기라 했다.</p></div>
    </div>
    <div class="facts">
      <div class="fact"><b>0.7mi</b><span>거리 전체 길이</span></div>
      <div class="fact"><b>1653</b><span>목책이 세워진 해</span></div>
      <div class="fact"><b>−25%</b><span>1929년 10월 사흘간</span></div>
      <div class="fact"><b>3,200kg</b><span>청동 황소의 무게</span></div>
    </div>
  </div>
</section>

<!-- ══ 풀블리드 인용 밴드 ══ -->
<section class="band">
  <div class="bg"></div><!-- SLOT/BAND : 붉은 하프톤 스카이라인 콜라주 (풀블리드) -->
  <div class="wrap">
    <span class="tag">CHAPTER 02 — THE NOVEL</span>
    <blockquote>그는 초록 불빛을 향해 손을 뻗었다.<br>그것은 <em>미래</em>가 아니라<br>돌아갈 수 없는 <em>과거</em>였다.</blockquote>
    <div class="src">F. Scott Fitzgerald, The Great Gatsby · 1925</div>
  </div>
</section>

<!-- ══ 02 개츠비 ══ -->
<section class="dark">
  <div class="wrap">
    <div class="sec-head">
      <div class="num">02</div>
      <h3 class="sec-title">위대한<br>개츠비</h3>
      <span class="sec-tag">JAZZ AGE / 1925</span>
    </div>
    <div class="gats">
      <div class="a">
        <div class="frame slot"><span class="tagname"><b>SLOT / CH.02-A</b>파티의 인물 · 3:4 세로</span></div>
        <span class="over">THE PARTY / EVERY SATURDAY</span>
      </div>
      <div class="b">
        <p class="lead">부(富)는 획득되지만,<br>신분은 <span>상속된다</span>.</p>
        <div>
          <div class="frame slot" style="min-height:230px"><span class="tagname"><b>SLOT / CH.02-B</b>거래소의 뒷골목 · 4:3</span></div>
          <div class="cap-d">Fig. 03 — 거래소의 뒷골목, 스크린이 기록한 방식</div>
        </div>
      </div>
    </div>
    <div class="cols">
      <div class="cell"><h4>줄거리 · 세 문장</h4><p>가난한 청년 제이 개츠비는 이름과 재산을 새로 만들어 롱아일랜드에 저택을 세운다. 매주 열리는 파티의 목적은 단 하나, 만(灣) 건너의 옛 연인 데이지가 우연히 들어오는 것. 그리고 그 우연이 그를 죽인다.</p></div>
      <div class="cell"><h4>돈의 출처 · 월가의 그늘</h4><p>개츠비의 부는 금주법 시대의 밀주와 채권 사기에서 나온다. 그의 후원자 울프심은 실존 인물 아널드 로스스타인을 모델로 한다. 1920년대의 도금은 늘 거래소의 뒷골목을 통과했다.</p></div>
      <div class="cell"><h4>아메리칸 드림의 해부</h4><p>이 소설이 위대한 이유는 꿈을 찬양하지 않기 때문이다. 개츠비는 계급의 사다리를 끝까지 오르지만, 마지막 칸이 없다는 사실만 확인한다. 그것이 재즈 시대의 진짜 회계장부다.</p></div>
      <div class="cell"><h4>일화 · 실패한 책</h4><p>1925년 출간 당시 판매는 참담했고, 피츠제럴드는 1940년 자신이 잊혔다고 믿으며 죽었다. 2차 대전 중 미군에 무료 배포되며 부활했다. 작가의 꿈은 사후에야 이루어졌다.</p></div>
    </div>
  </div>
</section>


<!-- ══ 02.5 개츠비 프로필 / DOSSIER ══ -->
<section class="dossier">
  <div class="graph"></div>
  <div class="wrap">
    <div class="dos-top">
      <span>PROFILE — SUBJECT NO. 02</span>
      <span>WEST EGG, LONG ISLAND, N.Y.</span>
      <span class="red">SUMMER 1922</span>
    </div>

    <div class="dos-stage">
      <h3 class="dos-name">JAY<span class="l2 hollow">GATSBY</span></h3>

      <!-- ▼▼ 누끼(투명 PNG) 삽입 지점 : slotbox를 <img>로 교체 ▼▼
           <div class="cutout"><img src="gatsby-cutout.png" alt="제이 개츠비 인물 누끼"></div>  -->
      <div class="cutout">
        <div class="slotbox"><span><b>SLOT / CUTOUT</b>개츠비 누끼 PNG<br>세로 길게 · 상반신 이상<br>배경 투명 권장</span></div>
      </div>

      <div class="dos-body">
        <p>이름은 직업이 아니다. 제임스 개츠는 밀너슈타 생이지만, 이름보다 먼저 버린 것은 과거 자체였다. 옥스퍼드를 잠시 거쳤다는 문장, 전쟁에서 훈장을 받았다는 문장, 집안의 유산을 물려받았다는 문장 — 그가 자신을 소개하는 언어는 사실의 목록이 아니라 설계된 파사드다.</p>
        <p>재산의 구조는 단순하다. 금주법이 만들어낸 공백을 유통망이 채우고, 그 수입은 다시 문서화되지 않는 채권 거래로 세탁된다. 그의 돈은 월 스트리트를 지나가지만 장부에는 한 번도 들르지 않는다.</p>
        <p>매주 토요일의 파티는 사교가 아니다. 별자리처럼 많은 사람을 불러 단 한 명이 우연히 들어오게 만드는 장치이며, 개츠비는 그 장치의 주인보다 관리자에 가깝다. 그는 자신의 파티에서 술을 마시지 않는다.</p>
        <p>계급은 그가 구매하지 못한 단 하나의 항목이다. 초록 불빛은 항상 만(灣) 건너에 있고, 그를 끝까지 밖에 남긴다. 그의 생애는 상승의 기록이면서, 상승이 어느 칸에서 멈추는지에 대한 기록이다.</p>
      </div>

      <span class="stampline">SELF-MADE / UNVERIFIED</span>
    </div>

    <div class="dos-meta">
      <dl class="fields">
        <dt>나이</dt><dd>32 · 노스다코타 출생</dd>
        <dt>본명</dt><dd>James Gatz — 17세에 개명</dd>
        <dt>계급</dt><dd>신흥부호 (New Money) · 상속 없음</dd>
        <dt>거주</dt><dd>West Egg — 만 건너 East Egg를 마주봄</dd>
        <dt>자금원</dt><dd>금주법기 유통 · 채권 (무증빙)</dd>
        <dt>관계</dt><dd>Daisy Buchanan — 1917년, 5년간 대기</dd>
      </dl>
      <div class="tagwrap">
        <h6>키워드 · 취미 · 습관</h6>
        <div class="tags">
          <span class="fill">토요일 파티</span>
          <span>수상 보트</span>
          <span>하이드로플레인</span>
          <span class="hot">초록 불빛 응시</span>
          <span>분홍 스리피스 수트</span>
          <span>노란 롤스로이스</span>
          <span>재즈 레코드</span>
          <span class="fill">Old Sport</span>
          <span>비음주 호스트</span>
          <span class="hot">자기 연출</span>
          <span>수영장</span>
          <span>서신 보관</span>
        </div>
      </div>
    </div>

    <div class="dos-foot">
      <span>FIG. 04 — 누끼 이미지 삽입 예정 (SLOT / CUTOUT)</span>
      <span>SOURCE: F. S. FITZGERALD, 1925</span>
      <span>CH. 02.5 · PROFILE</span>
    </div>
  </div>
</section>

<!-- ══ 03 맛집/일화 : 최하위 위계 ══ -->
<section>
  <div class="wrap minor">
    <div class="minor-head">
      <span class="n">03</span>
      <h3>거래가 끝난 뒤 · 도보 5분</h3>
      <span class="t">NOTES / EAT &amp; WALK</span>
    </div>
    <div class="minor-grid">
      <div class="m-item"><span class="yr">EST. 1837</span><h5>Delmonico's</h5><div class="adr">56 Beaver St</div>
        <p>미국 최초의 파인다이닝. 랍스터 뉴버그와 베이크드 알래스카가 태어난 곳.</p></div>
      <div class="m-item"><span class="yr">EST. 1762</span><h5>Fraunces Tavern</h5><div class="adr">54 Pearl St</div>
        <p>1783년 워싱턴이 장교들에게 작별 연설을 한 방이 2층에 남아 있다. 아래층은 여전히 술을 판다.</p></div>
      <div class="m-item"><span class="yr">1660s</span><h5>Stone Street</h5><div class="adr">Stone St, 자갈길 블록</div>
        <p>차가 못 들어오는 짧은 자갈길. 여름 저녁이면 야외 테이블로 덮인다.</p></div>
      <div class="m-item"><span class="yr">1697</span><h5>Trinity Church 묘지</h5><div class="adr">89 Broadway</div>
        <p>해밀턴이 시장 한복판을 바라보며 누워 있다. 점심 산책 코스.</p></div>
    </div>

    <div class="strip">
      <figure><div class="frame slot"><span class="tagname"><b>SLOT / A</b>3:4</span></div><figcaption>Ref. A — 반복 타이포</figcaption></figure>
      <figure><div class="frame slot"><span class="tagname"><b>SLOT / B</b>3:4</span></div><figcaption>Ref. B — 그리드 위계</figcaption></figure>
      <figure><div class="frame slot"><span class="tagname"><b>SLOT / C</b>3:4</span></div><figcaption>Ref. C — 텍스트 밀도</figcaption></figure>
      <figure><div class="frame slot"><span class="tagname"><b>SLOT / D</b>3:4</span></div><figcaption>Ref. D — 제목 겹침</figcaption></figure>
    </div>
  </div>
</section>

<!-- ══ 04 결론 ══ -->
<section>
  <div class="wrap">
    <div class="sec-head">
      <div class="num">04</div>
      <h3 class="sec-title">결론</h3>
      <span class="sec-tag">CONCLUSION</span>
    </div>
    <div class="cols">
      <div class="cell"><h4>왜 아직도 이 길인가</h4><p>거래는 이미 뉴저지의 서버실로 옮겨갔다. 그럼에도 사람들은 황소 앞에서 사진을 찍는다. 월 스트리트는 장소가 아니라 믿음의 주소이기 때문이다.</p></div>
      <div class="cell"><h4>개츠비가 남긴 각주</h4><p>초록 불빛은 여전히 만 건너에 있다. 도달하는 것이 목적이 아닌 빛, 그것이 아메리칸 드림의 정확한 정의다.</p></div>
      <div class="cell"><h4>독자를 위한 한 줄</h4><p>다운타운에 간다면 거래소보다 자갈길을 먼저 걸어보길. 신전은 사진으로 충분하지만, 저녁의 소음은 직접 들어야 한다.</p></div>
    </div>
  </div>
  <div class="wrap"><footer>
    <span>WALL ST. EDITORIAL © 2026</span>
    <span>SET IN SYSTEM SANS &amp; TIMES</span>
    <span style="color:var(--red)">END OF ISSUE 07</span>
  </footer></div>
</section>

</body>
</html>

