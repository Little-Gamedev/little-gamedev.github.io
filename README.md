# little-gamedev.github.io[Enclave_Tactical_Layer_1.html](https://github.com/user-attachments/files/26399438/Enclave_Tactical_Layer_1.html)
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Enclave — Тактический боевой слой</title>
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
--bg:#0c0e12;--bg2:#12151b;--bg3:#1a1e27;--bg4:#222733;
--text:#e8e6e0;--text2:#9b9a94;--text3:#5e5d58;
--accent:#d4a04a;--accent2:#e8b960;--accent-dim:#6b5225;
--red:#c04040;--red-dim:#3a1818;
--green:#3d8b5e;--green-dim:#142b1e;
--blue:#4a7bb5;--blue-dim:#182838;
--cyan:#4ab5a0;--cyan-dim:#183530;
--border:#2a2e38;
--radius:10px;
}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--text);font-family:'Outfit',sans-serif;font-weight:400;line-height:1.7;overflow-x:hidden}
.noise{position:fixed;top:0;left:0;width:100%;height:100%;pointer-events:none;z-index:9999;opacity:.03;
background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E")}
nav{position:fixed;top:0;left:0;right:0;z-index:100;background:rgba(12,14,18,.85);backdrop-filter:blur(20px);border-bottom:1px solid var(--border);padding:0 2rem;height:56px;display:flex;align-items:center;gap:2rem}
nav .logo{font-weight:800;font-size:1.1rem;letter-spacing:.15em;color:var(--accent)}
nav a{color:var(--text2);text-decoration:none;font-size:.8rem;font-weight:500;letter-spacing:.08em;text-transform:uppercase;transition:color .2s}
nav a:hover{color:var(--accent)}
.hero{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:6rem 2rem 4rem;position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;top:50%;left:50%;width:800px;height:800px;transform:translate(-50%,-50%);background:radial-gradient(circle,rgba(212,160,74,.08) 0%,transparent 60%);pointer-events:none}
.hero h1{font-size:clamp(3rem,8vw,6rem);font-weight:900;letter-spacing:.05em;line-height:1;margin-bottom:1rem}
.hero h1 span{color:var(--accent);display:block;font-size:.35em;font-weight:500;letter-spacing:.3em;text-transform:uppercase;margin-bottom:.5rem}
.hero p{color:var(--text2);font-size:1.1rem;max-width:600px;margin-bottom:2rem}
.hero .tags{display:flex;gap:.75rem;flex-wrap:wrap;justify-content:center}
.tag{background:var(--bg3);border:1px solid var(--border);border-radius:100px;padding:.35rem 1rem;font-size:.75rem;color:var(--text2);font-family:'JetBrains Mono',monospace;font-weight:500}
section{padding:5rem 2rem;max-width:1100px;margin:0 auto}
section h2{font-size:2rem;font-weight:700;margin-bottom:.5rem;display:flex;align-items:center;gap:.75rem}
section h2 .num{font-family:'JetBrains Mono',monospace;font-size:.9rem;color:var(--accent);background:var(--accent-dim);padding:.25rem .6rem;border-radius:6px;font-weight:600}
section>p{color:var(--text2);margin-bottom:2rem;max-width:700px}
.card-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:1rem;margin:2rem 0}
.card{background:var(--bg2);border:1px solid var(--border);border-radius:var(--radius);padding:1.25rem;transition:border-color .2s,transform .2s}
.card:hover{border-color:var(--accent-dim);transform:translateY(-2px)}
.card h3{font-size:1rem;font-weight:600;margin-bottom:.5rem;display:flex;align-items:center;gap:.5rem}
.card h3 .icon{width:28px;height:28px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:.8rem;flex-shrink:0}
.card p{color:var(--text2);font-size:.85rem;line-height:1.6}
.card .meta{margin-top:.75rem;display:flex;gap:.5rem;flex-wrap:wrap}
.badge{font-family:'JetBrains Mono',monospace;font-size:.65rem;padding:.2rem .5rem;border-radius:4px;font-weight:500}
.badge.green{background:var(--green-dim);color:var(--green)}
.badge.red{background:var(--red-dim);color:var(--red)}
.badge.blue{background:var(--blue-dim);color:var(--blue)}
.badge.cyan{background:var(--cyan-dim);color:var(--cyan)}
.badge.gold{background:var(--accent-dim);color:var(--accent)}
.tbl{width:100%;border-collapse:collapse;margin:1.5rem 0;font-size:.85rem}
.tbl th{text-align:left;padding:.65rem .75rem;background:var(--bg3);color:var(--accent);font-weight:600;font-size:.75rem;text-transform:uppercase;letter-spacing:.08em;border-bottom:2px solid var(--accent-dim)}
.tbl td{padding:.6rem .75rem;border-bottom:1px solid var(--border);color:var(--text2)}
.tbl tr:hover td{background:var(--bg2)}
.pipeline{display:flex;gap:0;margin:2rem 0;flex-wrap:wrap}
.pipe-step{flex:1;min-width:200px;background:var(--bg2);border:1px solid var(--border);padding:1.5rem;position:relative}
.pipe-step:first-child{border-radius:var(--radius) 0 0 var(--radius)}
.pipe-step:last-child{border-radius:0 var(--radius) var(--radius) 0}
.pipe-step:not(:last-child)::after{content:'\2192';position:absolute;right:-14px;top:50%;transform:translateY(-50%);font-size:1.2rem;color:var(--accent);z-index:2;background:var(--bg);padding:0 4px}
.pipe-step .step-num{font-family:'JetBrains Mono',monospace;font-size:.7rem;color:var(--accent);font-weight:600;margin-bottom:.5rem}
.pipe-step h4{font-size:.95rem;font-weight:600;margin-bottom:.35rem}
.pipe-step p{color:var(--text2);font-size:.8rem}
.eq-slots{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:.75rem;margin:2rem 0}
.eq-slot{background:var(--bg3);border-radius:8px;padding:.75rem 1rem;display:flex;align-items:center;gap:.6rem}
.eq-slot .dot{width:6px;height:6px;border-radius:50%;background:var(--accent);flex-shrink:0}
.eq-slot span{font-size:.85rem;color:var(--text2)}
.battle-frame{background:var(--bg2);border:1px solid var(--border);border-radius:var(--radius);overflow:hidden;margin:2rem 0}
.battle-frame-header{padding:.75rem 1.25rem;border-bottom:1px solid var(--border);display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:.5rem}
.battle-frame-header h3{font-size:.9rem;font-weight:600}
.battle-frame-header .legend{display:flex;gap:1rem;font-size:.7rem;color:var(--text3);font-family:'JetBrains Mono',monospace}
.legend-item{display:flex;align-items:center;gap:.35rem}
.legend-dot{width:8px;height:8px;border-radius:50%}
.battle-svg-wrap svg{display:block;width:100%}
.stat-bars{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:1rem;margin:2rem 0}
.stat-bar{background:var(--bg2);border:1px solid var(--border);border-radius:var(--radius);padding:1rem 1.25rem}
.stat-bar label{font-size:.75rem;font-weight:600;text-transform:uppercase;letter-spacing:.08em;color:var(--text2);margin-bottom:.5rem;display:block}
.bar-track{height:8px;background:var(--bg4);border-radius:4px;overflow:hidden;margin:.4rem 0}
.bar-fill{height:100%;border-radius:4px}
.stat-bar .value{font-family:'JetBrains Mono',monospace;font-size:1.5rem;font-weight:700}
.divider{height:1px;background:linear-gradient(90deg,transparent,var(--border),transparent);margin:4rem 0}
footer{text-align:center;padding:3rem 2rem;color:var(--text3);font-size:.8rem;border-top:1px solid var(--border)}
@media(max-width:700px){.pipeline{flex-direction:column}.pipe-step{border-radius:var(--radius)!important}.pipe-step:not(:last-child)::after{display:none}nav{padding:0 1rem;gap:1rem}nav a{font-size:.7rem}}
@keyframes fadeUp{from{opacity:0;transform:translateY(30px)}to{opacity:1;transform:translateY(0)}}
.anim{opacity:0;animation:fadeUp .6s ease forwards}
.anim.d1{animation-delay:.1s}.anim.d2{animation-delay:.2s}.anim.d3{animation-delay:.3s}.anim.d4{animation-delay:.4s}
</style>
</head>
<body>
<div class="noise"></div>
<nav>
  <div class="logo">ENCLAVE</div>
  <a href="#squads">Отряды</a>
  <a href="#equipment">Снаряжение</a>
  <a href="#battle">Бой</a>
  <a href="#cohesion">Собранность</a>
  <a href="#structures">Постройки</a>
</nav>

<div class="hero">
  <h1 class="anim"><span>Tactical Combat Layer</span>ENCLAVE</h1>
  <p class="anim d1">Тактический боевой слой. Реальное время с паузой. Отряды из жителей анклава. Точки захвата. Линии приказов.</p>
  <div class="tags anim d2">
    <span class="tag">Real-time + Pause</span>
    <span class="tag">5–25 мин</span>
    <span class="tag">до 10 отрядов</span>
    <span class="tag">Capture Points</span>
    <span class="tag">Постапокалипсис</span>
  </div>
</div>

<section id="squads">
  <h2 class="anim"><span class="num">01</span>Система отрядов</h2>
  <p class="anim d1">Каждый отряд — реальные жители анклава. Офицер + сержант + до 8 слотов. Максимум 10 человек, максимум 10 отрядов. Главнокомандующий командует всей армией.</p>
  <div class="card-grid">
    <div class="card anim d1"><h3><span class="icon" style="background:var(--green-dim);color:var(--green)">⚔</span>Стрелок</h3><p>Стандартная пехота, базовый бой. Не ограничивает размер отряда.</p><div class="meta"><span class="badge green">Без ограничений</span></div></div>
    <div class="card anim d2"><h3><span class="icon" style="background:var(--red-dim);color:var(--red)">🔫</span>Пулемётчик + помощник</h3><p>Тяжёлый подавляющий огонь. Работают в паре.</p><div class="meta"><span class="badge red">1 → макс 10</span><span class="badge red">2 → макс 6</span></div></div>
    <div class="card anim d3"><h3><span class="icon" style="background:var(--blue-dim);color:var(--blue)">💣</span>Гранатомётчик + помощник</h3><p>Против укреплений. Работают в паре.</p><div class="meta"><span class="badge blue">1 → макс 10</span><span class="badge blue">2 → макс 6</span></div></div>
    <div class="card anim d1"><h3><span class="icon" style="background:var(--cyan-dim);color:var(--cyan)">🎯</span>Снайпер</h3><p>Точный огонь на дальней дистанции.</p><div class="meta"><span class="badge cyan">1 → макс 10</span><span class="badge cyan">2 → макс 6</span></div></div>
    <div class="card anim d2"><h3><span class="icon" style="background:var(--green-dim);color:var(--green)">➕</span>Медик</h3><p>Лечит бойцов отряда в бою.</p><div class="meta"><span class="badge green">1 → макс 10</span><span class="badge green">2 → макс 6</span></div></div>
    <div class="card anim d3"><h3><span class="icon" style="background:var(--accent-dim);color:var(--accent)">🔧</span>Инженер</h3><p>Строит полевые сооружения.</p><div class="meta"><span class="badge gold">1 → макс 10</span><span class="badge gold">2 → макс 6</span></div></div>
    <div class="card anim d4"><h3><span class="icon" style="background:var(--red-dim);color:var(--red)">👁</span>Спецназовец</h3><p>Элитный боец. Строгие ограничения на размер отряда.</p><div class="meta"><span class="badge red">1 → макс 6</span><span class="badge red">2 → макс 4</span></div></div>
    <div class="card anim d4"><h3><span class="icon" style="background:var(--blue-dim);color:var(--blue)">🚛</span>Обеспечение</h3><p>До 16 человек. Техника. Подвоз припасов к постройкам и пунктам боепитания.</p><div class="meta"><span class="badge blue">Особый тип</span><span class="badge blue">Макс 16</span></div></div>
  </div>
  <h3 style="margin-top:2rem;font-size:1.1rem;font-weight:600">Шаблоны отрядов</h3>
  <table class="tbl"><thead><tr><th>Шаблон</th><th>Состав</th><th>Итого</th></tr></thead><tbody>
    <tr><td>Пехотный взвод</td><td>Офицер, сержант, 8 стрелков</td><td>10</td></tr>
    <tr><td>Огневая группа</td><td>Офицер, сержант, 2 ПК + 2 пом., 2 стрелка</td><td>8</td></tr>
    <tr><td>Штурмовая ячейка</td><td>Офицер, сержант, 1 гранатомёт + 1 пом., 1 медик, 3 стрелка</td><td>8</td></tr>
    <tr><td>Полевой госпиталь</td><td>Офицер, сержант, 2 медика, 2 инженера, 2 стрелка</td><td>8</td></tr>
    <tr><td>Охотники</td><td>Офицер, сержант, 2 снайпера, 4 стрелка</td><td>8</td></tr>
    <tr><td>Тени</td><td>Офицер, сержант, 2–4 спецназовца</td><td>4–6</td></tr>
    <tr><td style="color:var(--accent)">Кастомный</td><td>Игрок собирает сам по правилам</td><td>—</td></tr>
  </tbody></table>
</section>

<div class="divider"></div>

<section id="equipment">
  <h2><span class="num">02</span>Система снаряжения</h2>
  <p>Трёхслойный конвейер: от чертежа до бойца. Стандарт утверждается раз в 3 года для каждой роли отдельно.</p>
  <div class="pipeline">
    <div class="pipe-step"><div class="step-num">СЛОЙ 1</div><h4>Разработка</h4><p>Научный центр создаёт чертежи: оружие, форму, броню, гранаты, снаряжение</p></div>
    <div class="pipe-step"><div class="step-num">СЛОЙ 2</div><h4>Утверждение</h4><p>Раз в 3 года игрок выбирает стандарт для каждой роли из доступных разработок</p></div>
    <div class="pipe-step"><div class="step-num">СЛОЙ 3</div><h4>Производство</h4><p>Завод производит снаряжение. Нет ресурсов = нет экипировки</p></div>
  </div>
  <h3 style="margin-top:2rem;font-size:1.1rem;font-weight:600">Слоты снаряжения <span style="font-weight:400;color:var(--text3);font-size:.85rem">— для каждой роли отдельно</span></h3>
  <div class="eq-slots">
    <div class="eq-slot"><div class="dot"></div><span>Форма</span></div>
    <div class="eq-slot"><div class="dot"></div><span>Основное оружие</span></div>
    <div class="eq-slot"><div class="dot"></div><span>Доп. оружие</span></div>
    <div class="eq-slot"><div class="dot"></div><span>Гранаты</span></div>
    <div class="eq-slot"><div class="dot"></div><span>Снаряжение</span></div>
    <div class="eq-slot"><div class="dot"></div><span>Броня</span></div>
  </div>
</section>

<div class="divider"></div>

<section id="battle">
  <h2><span class="num">03</span>Тактический бой</h2>
  <p>Линии приказов + контрольные точки + построения. Рисуем маршрут, назначаем действия, снимаем с паузы. Ниже — стоп-кадр типичного столкновения.</p>
  <div class="battle-frame">
    <div class="battle-frame-header">
      <h3>⏸ Карта боя — стоп-кадр</h3>
      <div class="legend">
        <div class="legend-item"><div class="legend-dot" style="background:#3d8b5e"></div>Игрок</div>
        <div class="legend-item"><div class="legend-dot" style="background:#c04040"></div>Противник</div>
        <div class="legend-item"><div class="legend-dot" style="background:#d4a04a"></div>Точки захвата</div>
        <div class="legend-item"><div class="legend-dot" style="background:#4ab5a0"></div>Линии приказов</div>
      </div>
    </div>
    <div class="battle-svg-wrap">
      <svg viewBox="0 0 1100 550" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <radialGradient id="gg" cx="50%" cy="50%" r="50%"><stop offset="0%" stop-color="#3d8b5e" stop-opacity=".35"/><stop offset="100%" stop-color="#3d8b5e" stop-opacity="0"/></radialGradient>
          <radialGradient id="gr" cx="50%" cy="50%" r="50%"><stop offset="0%" stop-color="#c04040" stop-opacity=".35"/><stop offset="100%" stop-color="#c04040" stop-opacity="0"/></radialGradient>
          <radialGradient id="ga" cx="50%" cy="50%" r="50%"><stop offset="0%" stop-color="#d4a04a" stop-opacity=".25"/><stop offset="100%" stop-color="#d4a04a" stop-opacity="0"/></radialGradient>
          <marker id="ac" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="5" markerHeight="5" orient="auto"><path d="M2 2L8 5L2 8" fill="none" stroke="#4ab5a0" stroke-width="1.5"/></marker>
        </defs>
        <!-- LANDSCAPE -->
        <rect width="1100" height="550" fill="#1a1e14"/>
        <ellipse cx="200" cy="180" rx="160" ry="80" fill="#222816" opacity=".7"/>
        <ellipse cx="750" cy="350" rx="180" ry="90" fill="#222816" opacity=".6"/>
        <ellipse cx="550" cy="250" rx="120" ry="60" fill="#262b18" opacity=".5"/>
        <ellipse cx="400" cy="420" rx="100" ry="50" fill="#20250f" opacity=".6"/>
        <ellipse cx="900" cy="150" rx="140" ry="70" fill="#222816" opacity=".5"/>
        <path d="M0 320Q150 290,300 330Q450 370,550 310Q650 250,800 280Q950 310,1100 270" fill="none" stroke="#2a2818" stroke-width="25" opacity=".5"/>
        <path d="M0 320Q150 290,300 330Q450 370,550 310Q650 250,800 280Q950 310,1100 270" fill="none" stroke="#332f1c" stroke-width="6" opacity=".3" stroke-dasharray="12 8"/>
        <rect x="440" y="210" width="30" height="20" rx="2" fill="#2e2e28" stroke="#3a3a30" stroke-width=".5"/>
        <rect x="460" y="195" width="20" height="15" rx="2" fill="#2e2e28" stroke="#3a3a30" stroke-width=".5"/>
        <rect x="520" y="240" width="25" height="18" rx="2" fill="#2e2e28" stroke="#3a3a30" stroke-width=".5"/>
        <rect x="340" y="380" width="22" height="16" rx="2" fill="#2e2e28" stroke="#3a3a30" stroke-width=".5"/>
        <rect x="780" y="180" width="28" height="20" rx="2" fill="#2e2e28" stroke="#3a3a30" stroke-width=".5"/>
        <pattern id="grid" width="50" height="50" patternUnits="userSpaceOnUse"><path d="M50 0V50H0" fill="none" stroke="#2a2e1e" stroke-width=".3"/></pattern>
        <rect width="1100" height="550" fill="url(#grid)"/>
        <!-- CAPTURE POINTS -->
        <circle cx="220" cy="170" r="40" fill="url(#ga)"/><circle cx="220" cy="170" r="28" fill="none" stroke="#d4a04a" stroke-width="1.5" stroke-dasharray="5 3"/>
        <text x="220" y="126" text-anchor="middle" font-family="Outfit" font-size="11" font-weight="600" fill="#d4a04a">АЛЬФА</text>
        <text x="220" y="175" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="500" fill="#e8e6e0" opacity=".7">+100</text>
        <circle cx="380" cy="400" r="40" fill="url(#ga)"/><circle cx="380" cy="400" r="28" fill="none" stroke="#d4a04a" stroke-width="1.5" stroke-dasharray="5 3"/>
        <text x="380" y="356" text-anchor="middle" font-family="Outfit" font-size="11" font-weight="600" fill="#d4a04a">БРАВО</text>
        <text x="380" y="405" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="500" fill="#e8e6e0" opacity=".7">+72</text>
        <circle cx="550" cy="250" r="45" fill="url(#ga)"/><circle cx="550" cy="250" r="32" fill="none" stroke="#d4a04a" stroke-width="2" stroke-dasharray="5 3"/>
        <text x="550" y="202" text-anchor="middle" font-family="Outfit" font-size="12" font-weight="700" fill="#d4a04a">ЦЕНТР</text>
        <text x="550" y="255" text-anchor="middle" font-family="JetBrains Mono" font-size="11" font-weight="600" fill="#e8b960">−12</text>
        <circle cx="720" cy="140" r="40" fill="url(#ga)"/><circle cx="720" cy="140" r="28" fill="none" stroke="#d4a04a" stroke-width="1.5" stroke-dasharray="5 3"/>
        <text x="720" y="96" text-anchor="middle" font-family="Outfit" font-size="11" font-weight="600" fill="#d4a04a">ДЕЛЬТА</text>
        <text x="720" y="145" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="500" fill="#e8e6e0" opacity=".7">−100</text>
        <circle cx="880" cy="380" r="40" fill="url(#ga)"/><circle cx="880" cy="380" r="28" fill="none" stroke="#d4a04a" stroke-width="1.5" stroke-dasharray="5 3"/>
        <text x="880" y="336" text-anchor="middle" font-family="Outfit" font-size="11" font-weight="600" fill="#d4a04a">ЭХО</text>
        <text x="880" y="385" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="500" fill="#e8e6e0" opacity=".7">−85</text>
        <!-- ORDER LINES -->
        <path d="M130 170Q200 200,420 260" fill="none" stroke="#4ab5a0" stroke-width="2" stroke-dasharray="8 4" marker-end="url(#ac)" opacity=".7"/>
        <path d="M120 310Q250 360,380 400" fill="none" stroke="#4ab5a0" stroke-width="2" stroke-dasharray="8 4" marker-end="url(#ac)" opacity=".7"/>
        <path d="M160 430Q320 380,500 270" fill="none" stroke="#4ab5a0" stroke-width="2" stroke-dasharray="8 4" marker-end="url(#ac)" opacity=".7"/>
        <circle cx="320" cy="350" r="4" fill="#4ab5a0" opacity=".8"/>
        <text x="320" y="340" text-anchor="middle" font-family="JetBrains Mono" font-size="8" fill="#4ab5a0" opacity=".7">ЖДАТЬ</text>
        <!-- PLAYER SQUADS -->
        <circle cx="130" cy="170" r="24" fill="url(#gg)"/><circle cx="130" cy="170" r="14" fill="#142b1e" stroke="#3d8b5e" stroke-width="2"/>
        <text x="130" y="174" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="700" fill="#3d8b5e">10</text>
        <text x="130" y="197" text-anchor="middle" font-family="Outfit" font-size="9" font-weight="500" fill="#9b9a94">1-й Пехотный</text>
        <rect x="115" y="152" width="30" height="3" rx="1.5" fill="#222733"/><rect x="115" y="152" width="27" height="3" rx="1.5" fill="#3d8b5e"/>
        <circle cx="120" cy="310" r="24" fill="url(#gg)"/><circle cx="120" cy="310" r="14" fill="#142b1e" stroke="#3d8b5e" stroke-width="2"/>
        <text x="120" y="314" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="700" fill="#3d8b5e">8</text>
        <text x="120" y="337" text-anchor="middle" font-family="Outfit" font-size="9" font-weight="500" fill="#9b9a94">2-й Огневая</text>
        <rect x="105" y="292" width="30" height="3" rx="1.5" fill="#222733"/><rect x="105" y="292" width="25" height="3" rx="1.5" fill="#3d8b5e"/>
        <circle cx="160" cy="430" r="24" fill="url(#gg)"/><circle cx="160" cy="430" r="14" fill="#142b1e" stroke="#3d8b5e" stroke-width="2"/>
        <text x="160" y="434" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="700" fill="#3d8b5e">8</text>
        <text x="160" y="457" text-anchor="middle" font-family="Outfit" font-size="9" font-weight="500" fill="#9b9a94">3-й Штурм</text>
        <rect x="145" y="412" width="30" height="3" rx="1.5" fill="#222733"/><rect x="145" y="412" width="22" height="3" rx="1.5" fill="#d4a04a"/>
        <circle cx="95" cy="480" r="20" fill="url(#gg)"/><circle cx="95" cy="480" r="12" fill="#142b1e" stroke="#3d8b5e" stroke-width="1.5"/>
        <text x="95" y="484" text-anchor="middle" font-family="JetBrains Mono" font-size="9" font-weight="700" fill="#3d8b5e">16</text>
        <text x="95" y="504" text-anchor="middle" font-family="Outfit" font-size="8" font-weight="500" fill="#9b9a94">Обеспечение</text>
        <!-- ENEMY SQUADS -->
        <circle cx="680" cy="250" r="24" fill="url(#gr)"/><circle cx="680" cy="250" r="14" fill="#3a1818" stroke="#c04040" stroke-width="2"/>
        <text x="680" y="254" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="700" fill="#c04040">10</text>
        <text x="680" y="277" text-anchor="middle" font-family="Outfit" font-size="9" font-weight="500" fill="#9b9a94">Враг-1</text>
        <circle cx="820" cy="190" r="24" fill="url(#gr)"/><circle cx="820" cy="190" r="14" fill="#3a1818" stroke="#c04040" stroke-width="2"/>
        <text x="820" y="194" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="700" fill="#c04040">8</text>
        <text x="820" y="217" text-anchor="middle" font-family="Outfit" font-size="9" font-weight="500" fill="#9b9a94">Враг-2</text>
        <circle cx="940" cy="320" r="24" fill="url(#gr)"/><circle cx="940" cy="320" r="14" fill="#3a1818" stroke="#c04040" stroke-width="2"/>
        <text x="940" y="324" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="700" fill="#c04040">10</text>
        <text x="940" y="347" text-anchor="middle" font-family="Outfit" font-size="9" font-weight="500" fill="#9b9a94">Враг-3</text>
        <circle cx="980" cy="450" r="24" fill="url(#gr)"/><circle cx="980" cy="450" r="14" fill="#3a1818" stroke="#c04040" stroke-width="2"/>
        <text x="980" y="454" text-anchor="middle" font-family="JetBrains Mono" font-size="10" font-weight="700" fill="#c04040">6</text>
        <text x="980" y="477" text-anchor="middle" font-family="Outfit" font-size="9" font-weight="500" fill="#9b9a94">Враг-4</text>
        <!-- FIELD STRUCTURES -->
        <path d="M350 430Q370 440,400 435" fill="none" stroke="#6b5225" stroke-width="3" stroke-linecap="round"/>
        <text x="375" y="452" text-anchor="middle" font-family="JetBrains Mono" font-size="7" fill="#6b5225">ОКОПЫ</text>
        <path d="M460 290L520 275" fill="none" stroke="#5e5d58" stroke-width="1.5" stroke-dasharray="3 2"/>
        <text x="490" y="268" text-anchor="middle" font-family="JetBrains Mono" font-size="7" fill="#5e5d58">ПРОВОЛОКА</text>
        <!-- PAUSE BADGE -->
        <rect x="500" y="505" width="100" height="28" rx="14" fill="#12151b" stroke="#2a2e38" stroke-width="1"/>
        <text x="530" y="523" font-family="JetBrains Mono" font-size="10" font-weight="600" fill="#d4a04a">⏸</text>
        <text x="545" y="523" font-family="JetBrains Mono" font-size="10" font-weight="500" fill="#9b9a94">ПАУЗА</text>
      </svg>
    </div>
  </div>
  <h3 style="margin-top:2rem;font-size:1.1rem;font-weight:600">Построения</h3>
  <table class="tbl"><thead><tr><th>Построение</th><th>Скорость</th><th>Огн. мощь</th><th>Защита</th><th>Лучше всего для</th></tr></thead><tbody>
    <tr><td>Колонна</td><td style="color:var(--green)">Быстрая</td><td style="color:var(--red)">Низкая</td><td style="color:var(--red)">Уязвим с флангов</td><td>Марш</td></tr>
    <tr><td>Шеренга</td><td style="color:var(--red)">Медленная</td><td style="color:var(--green)">Максимальная</td><td style="color:var(--red)">Широкая мишень</td><td>Фронтальная атака</td></tr>
    <tr><td>Клин</td><td style="color:var(--accent)">Средняя</td><td style="color:var(--green)">Хорошая</td><td style="color:var(--accent)">Средняя</td><td>Прорыв</td></tr>
    <tr><td>Каре</td><td style="color:var(--red)">Оч. медленная</td><td style="color:var(--accent)">Круговая</td><td style="color:var(--green)">Сильная</td><td>Окружение</td></tr>
    <tr><td>Рассредоточенный</td><td style="color:var(--accent)">Средняя</td><td style="color:var(--red)">Слабая</td><td style="color:var(--green)">Мин. от взрывов</td><td>Под огнём</td></tr>
  </tbody></table>
</section>

<div class="divider"></div>

<section id="cohesion">
  <h2><span class="num">04</span>Собранность и усталость</h2>
  <p>Два ключевых параметра. Усталость усиливает падение собранности и замедляет её восстановление. Собранность = 0 → бесконтрольное бегство.</p>
  <div class="stat-bars">
    <div class="stat-bar"><label>Собранность (Cohesion)</label><div class="value" style="color:var(--green)">78%</div><div class="bar-track"><div class="bar-fill" style="width:78%;background:linear-gradient(90deg,var(--red),var(--accent),var(--green))"></div></div><p style="font-size:.75rem;color:var(--text3);margin-top:.5rem">0% = бегство · Движение не ниже 30% · Только бой роняет до 0</p></div>
    <div class="stat-bar"><label>Усталость (Fatigue)</label><div class="value" style="color:var(--accent)">35%</div><div class="bar-track"><div class="bar-fill" style="width:35%;background:linear-gradient(90deg,var(--green),var(--accent),var(--red))"></div></div><p style="font-size:.75rem;color:var(--text3);margin-top:.5rem">Растёт от активности · Падает от отдыха · Множитель на собранность</p></div>
  </div>
  <table class="tbl"><thead><tr><th>Ситуация</th><th>Отход на 1 позицию</th><th>Отход на 2 позиции</th></tr></thead><tbody>
    <tr><td>Игрок сам выводит</td><td style="color:var(--accent)">50% скорости</td><td style="color:var(--green)">100% скорости</td></tr>
    <tr><td>Бесконтрольное бегство</td><td style="color:var(--red)">25% скорости</td><td style="color:var(--accent)">50% скорости</td></tr>
  </tbody></table>
  <div class="card-grid" style="margin-top:1.5rem;grid-template-columns:repeat(3,1fr)">
    <div class="card" style="border-color:var(--red)"><h3 style="color:var(--red)">Ниже 50%</h3><p>После бегства: отрядом НЕЛЬЗЯ управлять</p></div>
    <div class="card" style="border-color:var(--accent)"><h3 style="color:var(--accent)">50–80%</h3><p>Можно управлять, но восстановление в 2x медленнее</p></div>
    <div class="card" style="border-color:var(--green)"><h3 style="color:var(--green)">Выше 80%</h3><p>Полностью восстановлен, все дебаффы сняты</p></div>
  </div>
</section>

<div class="divider"></div>

<section id="structures">
  <h2><span class="num">05</span>Полевые постройки</h2>
  <p>Ставятся в конкретную точку на карте. Строятся из припасов, доставляемых подразделением обеспечения.</p>
  <h3 style="margin-top:1.5rem;font-size:1rem;font-weight:600;color:var(--text2)">Любой отряд (команда «окопаться»)</h3>
  <table class="tbl"><thead><tr><th>Постройка</th><th>Стоимость</th><th>Эффект</th></tr></thead><tbody>
    <tr><td>Простые окопы</td><td style="color:var(--green)">Бесплатно</td><td>Бонус к защите</td></tr>
    <tr><td>Окопы с мешками</td><td style="color:var(--accent)">Припасы</td><td>Улучшенный бонус к защите</td></tr>
  </tbody></table>
  <h3 style="margin-top:2rem;font-size:1rem;font-weight:600;color:var(--text2)">Только инженеры</h3>
  <table class="tbl"><thead><tr><th>Постройка</th><th>Эффект</th><th>Размещение</th></tr></thead><tbody>
    <tr><td>Колючая проволока</td><td>Замедляет врагов</td><td>Линия на карте</td></tr>
    <tr><td>Пулемётное гнездо</td><td>Стационарная огневая точка</td><td>Точка</td></tr>
    <tr><td>Наблюдательный пост</td><td>Снимает туман войны</td><td>Точка</td></tr>
    <tr><td>Полевой медпункт</td><td>Ускоряет восстановление HP</td><td>Точка</td></tr>
    <tr><td>Пункт отдыха</td><td>Снижает усталость и восстанавливает собранность</td><td>Точка</td></tr>
    <tr><td>Склад припасов</td><td>Точка хранения, обеспечение подвозит</td><td>Точка</td></tr>
    <tr><td>Пункт боепитания</td><td>Отряды пополняют боеприпасы</td><td>Точка</td></tr>
    <tr><td>Ежи / завалы</td><td>Блокируют технику противника</td><td>Точка</td></tr>
    <tr><td>Минное поле</td><td>Урон врагу при входе в зону</td><td>Зона</td></tr>
    <tr><td>Блиндаж</td><td>Укрытие от навесного огня (отряд не стреляет)</td><td>Точка</td></tr>
  </tbody></table>
</section>

<div class="divider"></div>

<footer>
  <p style="color:var(--accent);font-weight:600;letter-spacing:.1em;margin-bottom:.5rem">ENCLAVE</p>
  <p>Тактический боевой слой · GDD v1.0 · Все параметры настраиваются в GameBalance</p>
</footer>
</body>
</html>
