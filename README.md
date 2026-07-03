<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>海龟汤事务所 · 情境推理游戏</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@500;700;900&family=Noto+Sans+SC:wght@300;400;500;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --ink-950:#0B0E14;
    --ink-900:#141821;
    --ink-850:#1B212C;
    --paper-100:#EDE6D6;
    --paper-50:#F7F3E8;
    --lamp-500:#E8A33D;
    --lamp-600:#C77F1F;
    --blood-600:#9B3A3A;
    --blood-700:#7A2C2C;
    --fog-400:#8B93A3;
    --ink-text:#20222A;
    --line:rgba(237,230,214,0.14);
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--paper-100);
    color:var(--ink-text);
    font-family:'Noto Sans SC', sans-serif;
    line-height:1.7;
    -webkit-font-smoothing:antialiased;
  }
  @media (prefers-reduced-motion: reduce){
    *{animation:none !important; transition:none !important;}
  }
  a{color:inherit; text-decoration:none;}
  .mono{font-family:'JetBrains Mono', monospace;}
  .serif{font-family:'Noto Serif SC', serif;}

  /* ---------- HERO ---------- */
  .hero{
    position:relative;
    min-height:100vh;
    background:var(--ink-950);
    color:var(--paper-100);
    overflow:hidden;
    display:flex;
    flex-direction:column;
  }
  .hero::before{
    content:"";
    position:absolute; inset:0;
    background-image:
      radial-gradient(circle at 50% 38%, rgba(232,163,61,0.16), transparent 42%),
      repeating-linear-gradient(0deg, rgba(255,255,255,0.02) 0px, rgba(255,255,255,0.02) 1px, transparent 1px, transparent 3px);
    pointer-events:none;
  }
  .spotlight{
    position:absolute; inset:0;
    pointer-events:none;
    background:radial-gradient(circle 260px at var(--mx,50%) var(--my,30%), rgba(232,163,61,0.10), transparent 60%);
    transition:background 0.15s ease-out;
  }
  .hero-nav{
    position:relative; z-index:2;
    display:flex; justify-content:space-between; align-items:center;
    padding:28px 6vw;
    font-family:'JetBrains Mono', monospace;
    font-size:12px;
    letter-spacing:0.12em;
    color:var(--fog-400);
    border-bottom:1px solid var(--line);
  }
  .hero-nav .brand{color:var(--paper-100); font-size:13px;}
  .case-tag{
    border:1px solid var(--line);
    padding:4px 10px;
    border-radius:2px;
    color:var(--lamp-500);
  }
  .hero-main{
    position:relative; z-index:2;
    flex:1;
    display:flex; flex-direction:column; align-items:center; justify-content:center;
    text-align:center;
    padding:60px 6vw;
  }
  .eyebrow{
    font-family:'JetBrains Mono', monospace;
    font-size:12px;
    letter-spacing:0.3em;
    color:var(--lamp-500);
    text-transform:uppercase;
    margin-bottom:22px;
    opacity:0.9;
  }
  .hero-title{
    font-family:'Noto Serif SC', serif;
    font-weight:900;
    font-size:clamp(48px, 10vw, 108px);
    line-height:1.05;
    letter-spacing:0.02em;
    color:var(--paper-50);
    text-shadow:0 0 40px rgba(232,163,61,0.18);
  }
  .hero-title span{color:var(--lamp-500);}
  .hero-sub{
    max-width:560px;
    margin:26px auto 0;
    font-size:16px;
    color:var(--fog-400);
    font-weight:300;
  }
  .hero-sub b{color:var(--paper-100); font-weight:500;}
  .cta-row{
    margin-top:44px;
    display:flex; gap:18px; flex-wrap:wrap; justify-content:center;
  }
  .btn{
    display:inline-flex; align-items:center; gap:10px;
    padding:16px 32px;
    font-size:15px; font-weight:500;
    border-radius:2px;
    cursor:pointer;
    border:1px solid transparent;
    transition:transform 0.18s ease, box-shadow 0.18s ease, background 0.18s ease;
    font-family:'Noto Sans SC', sans-serif;
  }
  .btn:focus-visible{outline:2px solid var(--lamp-500); outline-offset:3px;}
  .btn-primary{
    background:var(--lamp-500);
    color:var(--ink-950);
    box-shadow:0 0 0 rgba(232,163,61,0);
  }
  .btn-primary:hover{
    background:var(--lamp-600);
    box-shadow:0 8px 30px rgba(232,163,61,0.35);
    transform:translateY(-2px);
  }
  .btn-ghost{
    border-color:var(--line);
    color:var(--paper-100);
  }
  .btn-ghost:hover{
    border-color:var(--lamp-500);
    color:var(--lamp-500);
  }
  .hero-foot{
    position:relative; z-index:2;
    display:flex; justify-content:center; gap:36px;
    padding:22px 6vw 34px;
    font-family:'JetBrains Mono', monospace;
    font-size:11px;
    letter-spacing:0.08em;
    color:var(--fog-400);
    border-top:1px solid var(--line);
  }
  .hero-foot span{color:var(--lamp-500);}

  /* ---------- SECTIONS ---------- */
  section{
    padding:100px 6vw;
    max-width:1120px;
    margin:0 auto;
  }
  .section-head{
    display:flex; align-items:baseline; gap:16px;
    margin-bottom:48px;
    border-bottom:2px solid var(--ink-text);
    padding-bottom:18px;
  }
  .section-num{
    font-family:'JetBrains Mono', monospace;
    font-size:13px;
    color:var(--blood-600);
    font-weight:600;
  }
  .section-title{
    font-family:'Noto Serif SC', serif;
    font-weight:700;
    font-size:clamp(26px, 3.4vw, 38px);
  }
  .section-desc{
    max-width:640px;
    color:#4A4E58;
    font-size:15px;
    margin-top:10px;
  }

  /* 案情简介 */
  .brief-grid{
    display:grid;
    grid-template-columns:1.1fr 0.9fr;
    gap:56px;
    align-items:start;
  }
  .brief-text p{margin-bottom:18px; font-size:15.5px; color:#333743;}
  .brief-text strong{color:var(--blood-700);}
  .doc-card{
    background:var(--paper-50);
    border:1px solid #D9CFB6;
    box-shadow:0 12px 32px rgba(20,20,15,0.08);
    padding:30px 28px;
    position:relative;
  }
  .doc-card::before{
    content:"机密";
    position:absolute;
    top:18px; right:-8px;
    font-family:'Noto Serif SC', serif;
    font-weight:900;
    font-size:13px;
    color:var(--blood-600);
    border:2px solid var(--blood-600);
    padding:3px 10px;
    transform:rotate(8deg);
    opacity:0.75;
    letter-spacing:0.1em;
  }
  .doc-label{
    font-family:'JetBrains Mono', monospace;
    font-size:11px;
    letter-spacing:0.1em;
    color:var(--blood-600);
    margin-bottom:10px;
  }
  .doc-line{
    display:flex; justify-content:space-between;
    padding:10px 0;
    border-bottom:1px dashed #CBC0A3;
    font-size:14px;
  }
  .doc-line span:first-child{color:#6B6656;}
  .doc-line span:last-child{font-weight:500;}

  /* 取证流程 steps */
  .steps{
    display:grid;
    grid-template-columns:repeat(4, 1fr);
    gap:2px;
    background:#D9CFB6;
    border:1px solid #D9CFB6;
  }
  .step{
    background:var(--paper-50);
    padding:32px 26px;
    position:relative;
  }
  .step-index{
    font-family:'JetBrains Mono', monospace;
    font-size:12px;
    color:var(--lamp-600);
    letter-spacing:0.1em;
  }
  .step h3{
    font-family:'Noto Serif SC', serif;
    font-size:19px;
    margin:14px 0 10px;
  }
  .step p{font-size:13.5px; color:#4A4E58;}

  /* 案卷架 modes */
  .cases{
    display:grid;
    grid-template-columns:repeat(auto-fit, minmax(240px,1fr));
    gap:22px;
  }
  .case-card{
    background:var(--paper-50);
    border:1px solid #D9CFB6;
    padding:26px 24px 24px;
    transition:transform 0.2s ease, box-shadow 0.2s ease;
    display:flex; flex-direction:column; height:100%;
  }
  .case-card:hover{
    transform:translateY(-6px);
    box-shadow:0 16px 34px rgba(20,20,15,0.12);
  }
  .case-tab{
    font-family:'JetBrains Mono', monospace;
    font-size:11px;
    color:#fff;
    background:var(--ink-900);
    display:inline-block;
    padding:4px 10px;
    margin-bottom:16px;
    align-self:flex-start;
  }
  .case-card h3{
    font-family:'Noto Serif SC', serif;
    font-size:20px;
    margin-bottom:8px;
  }
  .case-card p{font-size:13.5px; color:#4A4E58; flex:1;}
  .difficulty{
    margin-top:16px;
    display:flex; gap:5px;
  }
  .dot{width:7px; height:7px; border-radius:50%; background:#D9CFB6;}
  .dot.on{background:var(--blood-600);}

  /* 常见问题 */
  .faq-item{
    border-bottom:1px solid #D9CFB6;
    padding:20px 0;
  }
  .faq-item h4{
    font-family:'Noto Serif SC', serif;
    font-size:16.5px;
    margin-bottom:8px;
  }
  .faq-item p{font-size:14px; color:#4A4E58;}

  /* ---------- FOOTER CTA ---------- */
  .final-cta{
    background:var(--ink-950);
    color:var(--paper-100);
    text-align:center;
    padding:110px 6vw;
    position:relative;
    overflow:hidden;
  }
  .final-cta::before{
    content:"";
    position:absolute; inset:0;
    background:radial-gradient(circle at 50% 20%, rgba(232,163,61,0.14), transparent 55%);
  }
  .final-cta > *{position:relative; z-index:1;}
  .final-cta .eyebrow{color:var(--lamp-500);}
  .final-title{
    font-family:'Noto Serif SC', serif;
    font-weight:800;
    font-size:clamp(30px, 5vw, 48px);
    max-width:640px;
    margin:0 auto 18px;
  }
  .final-sub{
    color:var(--fog-400);
    max-width:480px;
    margin:0 auto 40px;
    font-size:15px;
  }
  footer{
    text-align:center;
    padding:26px 6vw;
    font-family:'JetBrains Mono', monospace;
    font-size:11px;
    color:var(--fog-400);
    background:var(--ink-950);
    border-top:1px solid var(--line);
  }

  @media (max-width:820px){
    .brief-grid{grid-template-columns:1fr;}
    .steps{grid-template-columns:1fr 1fr;}
  }
  @media (max-width:520px){
    .steps{grid-template-columns:1fr;}
    .hero-foot{flex-wrap:wrap; gap:14px 24px;}
  }
</style>
</head>
<body>

<!-- ============ HERO ============ -->
<div class="hero" id="hero">
  <div class="spotlight" id="spotlight"></div>

  <div class="hero-nav">
    <span class="brand serif">海龟汤事务所</span>
    <span class="case-tag">CASE FILE · OPEN</span>
  </div>

  <div class="hero-main">
    <div class="eyebrow">情境推理 · 海龟汤 · Lateral Thinking</div>
    <h1 class="hero-title">你负责提问<br><span>真相负责说话</span></h1>
    <p class="hero-sub">
      一句离奇的<b>"汤面"</b>，一段被藏起来的<b>"汤底"</b>。<br>
      你只能用"是 / 不是 / 无关"三种回答逼近真相——每一个问题，都是一次审讯。
    </p>
    <div class="cta-row">
      <a class="btn btn-primary" href="https://soup-riddle-game--liucaijing25.replit.app/" target="_blank" rel="noopener">
        进入案发现场 →
      </a>
      <a class="btn btn-ghost" href="#brief">先看看案情介绍</a>
    </div>
  </div>

  <div class="hero-foot">
    <span>案件类型 <b class="mono" style="color:#fff">悬疑 / 推理 / 脑洞</b></span>
    <span>参与方式 <b class="mono" style="color:#fff">单人 · 多人皆可</b></span>
    <span>侦破用时 <b class="mono" style="color:#fff">10–40 分钟 / 案</b></span>
  </div>
</div>

<!-- ============ 案情简介 ============ -->
<section id="brief">
  <div class="section-head">
    <span class="section-num mono">01</span>
    <h2 class="section-title">案情简介</h2>
  </div>
  <div class="brief-grid">
    <div class="brief-text">
      <p>
        海龟汤，正式名称"情境推理游戏"，是一种由<strong>主持人（汤主）</strong>抛出谜面、<strong>玩家</strong>通过提问逐步还原真相的推理游戏。
        它起源于一道经典谜题——"他喝了海龟汤后自杀了，为什么？"——由此得名。
      </p>
      <p>
        每一道题都由两部分组成：<strong>汤面</strong>是你能看到的、看似荒诞或矛盾的片段；<strong>汤底</strong>是隐藏在背后、逻辑自洽的完整故事。
        你的任务，就是通过不断提出"是非题"，一点点撬开汤面的裂缝，拼出汤底的全貌。
      </p>
      <p>
        它不需要知识储备，不比拼手速，考验的只有一件事：<strong>你会不会问问题</strong>。
        一个人可以细细推敲，一群人可以互相补位——不管是深夜自娱，还是聚会破冰，都合适。
      </p>
    </div>

    <div class="doc-card">
      <div class="doc-label mono">GAME BRIEFING</div>
      <div class="doc-line"><span>游戏类型</span><span>情境推理 / 海龟汤</span></div>
      <div class="doc-line"><span>提问方式</span><span>是 / 不是 / 无关</span></div>
      <div class="doc-line"><span>适合人数</span><span>1 人独查 或 多人围观推理</span></div>
      <div class="doc-line"><span>难度分级</span><span>入门 · 进阶 · 烧脑</span></div>
      <div class="doc-line"><span>核心能力</span><span>逻辑链 · 提问技巧 · 想象力</span></div>
      <div class="doc-line" style="border-bottom:none"><span>目标</span><span>说出与汤底一致的真相</span></div>
    </div>
  </div>
</section>

<!-- ============ 取证流程 ============ -->
<section id="how">
  <div class="section-head">
    <span class="section-num mono">02</span>
    <h2 class="section-title">如何破案</h2>
  </div>
  <p class="section-desc">整个推理过程分四步，顺序不能乱——这是唯一一处"编号"真正有意义的地方。</p>

  <div class="steps">
    <div class="step">
      <div class="step-index mono">STEP 01</div>
      <h3 class="serif">读汤面</h3>
      <p>阅读主持人给出的谜面。它往往简短、离奇，甚至有点荒谬——先别急着下结论。</p>
    </div>
    <div class="step">
      <div class="step-index mono">STEP 02</div>
      <h3 class="serif">提问题</h3>
      <p>只能问能用"是 / 不是 / 无关"回答的问题。问题越精准，逼近真相的速度越快。</p>
    </div>
    <div class="step">
      <div class="step-index mono">STEP 03</div>
      <h3 class="serif">拼线索</h3>
      <p>把主持人的每一次回答记下来，像拼图一样，在脑子里搭出一条自洽的逻辑链。</p>
    </div>
    <div class="step">
      <div class="step-index mono">STEP 04</div>
      <h3 class="serif">说汤底</h3>
      <p>当你觉得摸到真相时，完整复述你的推理。与汤底吻合，此案告破。</p>
    </div>
  </div>
</section>

<!-- ============ 案卷架 / 难度分类 ============ -->
<section id="modes">
  <div class="section-head">
    <span class="section-num mono">03</span>
    <h2 class="section-title">案卷架</h2>
  </div>
  <p class="section-desc">从案卷架上挑一份案子——按脑洞和烧脑程度分类，新人和老玩家都能找到合适的难度。</p>

  <div class="cases">
    <div class="case-card">
      <span class="case-tab">入门案</span>
      <h3 class="serif">日常疑云</h3>
      <p>谜面贴近生活，逻辑链短而清晰，适合第一次接触海龟汤的新玩家热身。</p>
      <div class="difficulty"><span class="dot on"></span><span class="dot"></span><span class="dot"></span><span class="dot"></span><span class="dot"></span></div>
    </div>
    <div class="case-card">
      <span class="case-tab">悬疑案</span>
      <h3 class="serif">暗夜谜局</h3>
      <p>带一点惊悚和反转，需要跳出常规思路，适合喜欢烧脑推理的玩家。</p>
      <div class="difficulty"><span class="dot on"></span><span class="dot on"></span><span class="dot on"></span><span class="dot"></span><span class="dot"></span></div>
    </div>
    <div class="case-card">
      <span class="case-tab">脑洞案</span>
      <h3 class="serif">异想天开</h3>
      <p>不局限于现实逻辑，天马行空，考验的是想象力而非常识。</p>
      <div class="difficulty"><span class="dot on"></span><span class="dot on"></span><span class="dot"></span><span class="dot"></span><span class="dot"></span></div>
    </div>
    <div class="case-card">
      <span class="case-tab">硬核案</span>
      <h3 class="serif">深潜真相</h3>
      <p>多重反转、长逻辑链，专为资深玩家准备，慎入。</p>
      <div class="difficulty"><span class="dot on"></span><span class="dot on"></span><span class="dot on"></span><span class="dot on"></span><span class="dot on"></span></div>
    </div>
  </div>
</section>

<!-- ============ FAQ ============ -->
<section id="faq">
  <div class="section-head">
    <span class="section-num mono">04</span>
    <h2 class="section-title">开庭须知</h2>
  </div>

  <div class="faq-item">
    <h4>只能问"是非题"吗？</h4>
    <p>是的。任何开放式问题主持人都无法直接回答，试着把问题拆成可以用"是 / 不是 / 无关"作答的形式。</p>
  </div>
  <div class="faq-item">
    <h4>没有思路了怎么办？</h4>
    <p>可以先确认汤面中每一个细节是否"重要"，把无关信息筛掉，逻辑链往往就清楚了。</p>
  </div>
  <div class="faq-item">
    <h4>一个人也能玩吗？</h4>
    <p>可以。系统会作为汤主陪你问答，也支持多人在同一个案卷里轮流提问、共同推理。</p>
  </div>
  <div class="faq-item">
    <h4>猜错了会怎样？</h4>
    <p>不会有惩罚，主持人只会告诉你"不是"或"无关"，你可以无限次调整方向，直到拼出真相。</p>
  </div>
</section>

<!-- ============ 最终 CTA ============ -->
<div class="final-cta">
  <div class="eyebrow">CASE FILE · READY</div>
  <h2 class="final-title serif">案卷已经摆在桌上<br>只差你来提问</h2>
  <p class="final-sub">灯已经亮了，汤主已经就位。第一个问题，由你来问。</p>
  <a class="btn btn-primary" href="https://soup-riddle-game--liucaijing25.replit.app/" target="_blank" rel="noopener">
    开始提问 →
  </a>
</div>

<footer>
  海龟汤事务所 · 情境推理游戏 · 本案卷仅供娱乐推理使用
</footer>

<script>
  const hero = document.getElementById('hero');
  const spotlight = document.getElementById('spotlight');
  hero.addEventListener('mousemove', (e) => {
    const rect = hero.getBoundingClientRect();
    const x = ((e.clientX - rect.left) / rect.width) * 100;
    const y = ((e.clientY - rect.top) / rect.height) * 100;
    spotlight.style.setProperty('--mx', x + '%');
    spotlight.style.setProperty('--my', y + '%');
  });
</script>

</body>
</html>
