<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>My Recipe Book</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300&family=Jost:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --cream: #f5f0e8;
    --warm-white: #faf7f2;
    --beige: #e8dfd0;
    --tan: #c9b99a;
    --brown: #8b6f4e;
    --dark-brown: #4a3728;
    --espresso: #2c1f14;
    --accent: #b5845a;
    --light-tan: #ede4d8;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background-color: var(--cream);
    font-family: 'Jost', sans-serif;
    color: var(--espresso);
    min-height: 100vh;
    background-image: 
      radial-gradient(ellipse at 20% 20%, rgba(181,132,90,0.08) 0%, transparent 50%),
      radial-gradient(ellipse at 80% 80%, rgba(139,111,78,0.07) 0%, transparent 50%);
  }

  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.4;
  }

  header {
    text-align: center;
    padding: 60px 20px 40px;
    position: relative;
  }

  .header-line {
    width: 80px;
    height: 1px;
    background: var(--tan);
    margin: 0 auto 24px;
  }

  .header-eyebrow {
    font-family: 'Jost', sans-serif;
    font-weight: 300;
    font-size: 11px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 16px;
  }

  h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.4rem, 6vw, 4rem);
    font-weight: 400;
    color: var(--dark-brown);
    line-height: 1.1;
    margin-bottom: 12px;
  }

  h1 em {
    font-style: italic;
    color: var(--accent);
  }

  .header-sub {
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
    font-size: 1.1rem;
    color: var(--brown);
    margin-bottom: 32px;
  }

  .header-ornament {
    font-size: 1.4rem;
    color: var(--tan);
    letter-spacing: 8px;
  }

  .controls {
    max-width: 700px;
    margin: 0 auto 48px;
    padding: 0 24px;
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
    justify-content: center;
  }

  .search-wrap {
    position: relative;
    flex: 1;
    min-width: 200px;
  }

  .search-wrap::before {
    content: '⌕';
    position: absolute;
    left: 16px;
    top: 50%;
    transform: translateY(-50%);
    color: var(--tan);
    font-size: 1.2rem;
    pointer-events: none;
  }

  input[type="search"] {
    width: 100%;
    padding: 12px 16px 12px 42px;
    background: var(--warm-white);
    border: 1px solid var(--beige);
    border-radius: 2px;
    font-family: 'Jost', sans-serif;
    font-size: 0.85rem;
    font-weight: 300;
    color: var(--espresso);
    outline: none;
    transition: border-color 0.2s;
  }

  input[type="search"]:focus { border-color: var(--tan); }
  input[type="search"]::placeholder { color: var(--tan); }

  .filter-btns {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    justify-content: center;
  }

  .filter-btn {
    padding: 10px 20px;
    background: transparent;
    border: 1px solid var(--beige);
    border-radius: 2px;
    font-family: 'Jost', sans-serif;
    font-size: 0.78rem;
    font-weight: 400;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--brown);
    cursor: pointer;
    transition: all 0.2s;
  }

  .filter-btn:hover, .filter-btn.active {
    background: var(--dark-brown);
    border-color: var(--dark-brown);
    color: var(--cream);
  }

  .grid {
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 24px 80px;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 32px;
  }

  .card {
    background: var(--warm-white);
    border: 1px solid var(--beige);
    cursor: pointer;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    position: relative;
    overflow: hidden;
    animation: fadeUp 0.5s ease both;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .card:hover {
    transform: translateY(-4px);
    box-shadow: 0 16px 40px rgba(74,55,40,0.12);
  }

  .card-banner { height: 6px; background: linear-gradient(90deg, var(--accent), var(--tan)); }

  .card-body { padding: 28px 28px 24px; }

  .card-tag {
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 10px;
  }

  .card-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.4rem;
    font-weight: 400;
    color: var(--dark-brown);
    line-height: 1.3;
    margin-bottom: 8px;
  }

  .card-desc {
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
    font-size: 1rem;
    color: var(--brown);
    line-height: 1.5;
    margin-bottom: 20px;
  }

  .card-meta {
    display: flex;
    gap: 16px;
    padding-top: 16px;
    border-top: 1px solid var(--light-tan);
  }

  .meta-item { display: flex; flex-direction: column; gap: 2px; }

  .meta-label {
    font-size: 9px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--tan);
  }

  .meta-value { font-size: 0.82rem; font-weight: 400; color: var(--brown); }

  .card-corner { position: absolute; bottom: 20px; right: 24px; font-size: 1.4rem; opacity: 0.15; }

  .modal-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(44,31,20,0.6);
    z-index: 500;
    backdrop-filter: blur(4px);
    align-items: center;
    justify-content: center;
    padding: 24px;
  }

  .modal-overlay.open { display: flex; animation: fadeIn 0.25s ease; }

  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

  .modal {
    background: var(--warm-white);
    max-width: 680px;
    width: 100%;
    max-height: 90vh;
    overflow-y: auto;
    position: relative;
    animation: slideUp 0.3s ease;
    scrollbar-width: thin;
    scrollbar-color: var(--tan) transparent;
  }

  @keyframes slideUp {
    from { transform: translateY(30px); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
  }

  .modal-banner { height: 8px; background: linear-gradient(90deg, var(--accent), var(--tan), var(--brown)); }
  .modal-content { padding: 40px 40px 48px; }

  .modal-close {
    position: absolute;
    top: 20px;
    right: 20px;
    background: none;
    border: 1px solid var(--beige);
    width: 34px;
    height: 34px;
    cursor: pointer;
    font-size: 1rem;
    color: var(--brown);
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
  }

  .modal-close:hover { background: var(--dark-brown); color: var(--cream); border-color: var(--dark-brown); }

  .modal-tag { font-size: 10px; font-weight: 500; letter-spacing: 3px; text-transform: uppercase; color: var(--accent); margin-bottom: 10px; }

  .modal-title {
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    font-weight: 400;
    color: var(--dark-brown);
    line-height: 1.2;
    margin-bottom: 8px;
  }

  .modal-desc {
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
    font-size: 1.1rem;
    color: var(--brown);
    margin-bottom: 32px;
  }

  .section-title {
    font-family: 'Jost', sans-serif;
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .section-title::after { content: ''; flex: 1; height: 1px; background: var(--beige); }

  .ingredients-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6px 20px;
    margin-bottom: 32px;
  }

  .ingredient {
    font-size: 0.88rem;
    color: var(--dark-brown);
    padding: 6px 0;
    border-bottom: 1px solid var(--light-tan);
    display: flex;
    justify-content: space-between;
    gap: 8px;
  }

  .ingredient-amount { color: var(--accent); font-weight: 500; white-space: nowrap; }
  .ingredient-name { color: var(--dark-brown); font-family: 'Cormorant Garamond', serif; font-size: 1rem; }

  .steps-list { list-style: none; display: flex; flex-direction: column; gap: 16px; }

  .step { display: flex; gap: 16px; align-items: flex-start; }

  .step-num { font-family: 'Playfair Display', serif; font-size: 1.1rem; color: var(--tan); min-width: 24px; line-height: 1.5; }

  .step-text { font-size: 0.9rem; line-height: 1.7; color: var(--espresso); font-weight: 300; }

  .modal-note {
    margin-top: 28px;
    padding: 16px 20px;
    background: var(--light-tan);
    border-left: 3px solid var(--accent);
    font-family: 'Cormorant Garamond', serif;
    font-style: italic;
    font-size: 0.95rem;
    color: var(--brown);
    line-height: 1.6;
  }

  .no-results { text-align: center; padding: 60px 20px; grid-column: 1/-1; }
  .no-results p { font-family: 'Cormorant Garamond', serif; font-style: italic; font-size: 1.2rem; color: var(--tan); }

  @media (max-width: 600px) {
    .modal-content { padding: 28px 24px 36px; }
    .ingredients-grid { grid-template-columns: 1fr; }
    .modal-title { font-size: 1.6rem; }
  }
</style>
</head>
<body>

<header>
  <div class="header-line"></div>
  <p class="header-eyebrow">A personal collection</p>
  <h1>My <em>Recipe</em> Book</h1>
  <p class="header-sub">Handpicked breads & bakes, made with love</p>
  <div class="header-ornament">· · ·</div>
</header>

<div class="controls">
  <div class="search-wrap">
    <input type="search" id="searchInput" placeholder="Search recipes…">
  </div>
  <div class="filter-btns">
    <button class="filter-btn active" data-filter="all">All</button>
    <button class="filter-btn" data-filter="bread">Bread</button>
    <button class="filter-btn" data-filter="tangzhong">Tangzhong</button>
  </div>
</div>

<div class="grid" id="recipeGrid"></div>

<div class="modal-overlay" id="modalOverlay">
  <div class="modal" id="modal">
    <div class="modal-banner"></div>
    <button class="modal-close" id="modalClose">✕</button>
    <div class="modal-content" id="modalContent"></div>
  </div>
</div>

<script>
const recipes = [
  {
    id: 1,
    title: "Whole Wheat Tangzhong Milk Bread",
    tag: "Bread · Tangzhong",
    categories: ["bread", "tangzhong"],
    desc: "A soft, pillowy whole wheat loaf enriched with egg, milk powder, and butter, built on a tangzhong base for an exceptionally tender crumb.",
    time: "3–4 hrs",
    difficulty: "Intermediate",
    yield: "1 loaf",
    emoji: "🍞",
    note: "Yeast adjusted to 4.5g (down from original 5.5g) for a slightly slower, more flavourful ferment while still being reliable through the long process. Expect the first rise to take around 1.5–2 hours.",
    sections: [
      {
        title: "Tangzhong",
        ingredients: [
          { amount: "20g", name: "whole wheat flour" },
          { amount: "100g", name: "water" },
        ]
      },
      {
        title: "Dough",
        ingredients: [
          { amount: "330g", name: "whole wheat flour" },
          { amount: "42g", name: "sugar" },
          { amount: "7g", name: "salt" },
          { amount: "17g", name: "milk powder" },
          { amount: "4.5g", name: "instant yeast" },
          { amount: "50g", name: "egg (about 1 egg)" },
          { amount: "120g", name: "water" },
          { amount: "45g", name: "unsalted butter, softened" },
        ]
      }
    ],
    steps: [
      "Make the tangzhong: heat 20g whole wheat flour and 100g water over low heat, stirring constantly, until thickened at 149°F (65°C). Do not boil. Let cool completely before use.",
      "Mix 330g whole wheat flour, 120g water, and the cooled tangzhong until no dry flour remains. Rest for 30 minutes (autolyse).",
      "Add 4.5g yeast, 7g salt, 42g sugar, 50g egg, and 17g milk powder to the rested dough. Mix for 3–5 minutes until the dough comes together. If too sticky, add a little flour gradually.",
      "Add 45g softened butter gradually and mix for 8–10 minutes until fully incorporated and smooth. Whole wheat dough takes longer to develop gluten and may need more time.",
      "Transfer dough to an oiled bowl and let rise at room temperature until doubled in size (about 1.5–2 hours).",
      "Divide the dough into 3 equal portions, shape into balls, and let rest for 30 minutes.",
      "Shape each portion into a log and place into an 8.5×4.5×4.5\" pullman pan. Proof until the dough reaches about 90% of the pan.",
      "For a rectangular loaf, bake with the lid on. For a domed top, brush with egg wash before baking.",
      "Bake at 350°F (175°C) for 30–35 minutes until golden brown."
    ]
  }
];

function renderCards(list) {
  const grid = document.getElementById('recipeGrid');
  grid.innerHTML = '';
  if (!list.length) {
    grid.innerHTML = '<div class="no-results"><p>No recipes found…</p></div>';
    return;
  }
  list.forEach((r, i) => {
    const card = document.createElement('div');
    card.className = 'card';
    card.style.animationDelay = `${i * 0.08}s`;
    card.innerHTML = `
      <div class="card-banner"></div>
      <div class="card-body">
        <div class="card-tag">${r.tag}</div>
        <div class="card-title">${r.title}</div>
        <div class="card-desc">${r.desc}</div>
        <div class="card-meta">
          <div class="meta-item"><span class="meta-label">Time</span><span class="meta-value">${r.time}</span></div>
          <div class="meta-item"><span class="meta-label">Level</span><span class="meta-value">${r.difficulty}</span></div>
          <div class="meta-item"><span class="meta-label">Yield</span><span class="meta-value">${r.yield}</span></div>
        </div>
        <div class="card-corner">${r.emoji}</div>
      </div>
    `;
    card.addEventListener('click', () => openModal(r));
    grid.appendChild(card);
  });
}

function openModal(r) {
  let ingredientsHTML = '';
  r.sections.forEach(sec => {
    ingredientsHTML += `<div class="section-title">${sec.title}</div><div class="ingredients-grid">`;
    sec.ingredients.forEach(ing => {
      ingredientsHTML += `<div class="ingredient"><span class="ingredient-name">${ing.name}</span><span class="ingredient-amount">${ing.amount}</span></div>`;
    });
    ingredientsHTML += `</div>`;
  });

  const stepsHTML = r.steps.map((s, i) => `
    <li class="step"><span class="step-num">${i + 1}</span><span class="step-text">${s}</span></li>`).join('');

  document.getElementById('modalContent').innerHTML = `
    <div class="modal-tag">${r.tag}</div>
    <div class="modal-title">${r.title}</div>
    <div class="modal-desc">${r.desc}</div>
    ${ingredientsHTML}
    <div class="section-title">Method</div>
    <ol class="steps-list">${stepsHTML}</ol>
    ${r.note ? `<div class="modal-note">📝 ${r.note}</div>` : ''}
  `;

  document.getElementById('modalOverlay').classList.add('open');
  document.body.style.overflow = 'hidden';
}

function closeModal() {
  document.getElementById('modalOverlay').classList.remove('open');
  document.body.style.overflow = '';
}

document.getElementById('modalClose').addEventListener('click', closeModal);
document.getElementById('modalOverlay').addEventListener('click', e => {
  if (e.target === document.getElementById('modalOverlay')) closeModal();
});
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeModal(); });

let currentFilter = 'all';
let currentSearch = '';

function applyFilters() {
  let list = recipes;
  if (currentFilter !== 'all') list = list.filter(r => r.categories.includes(currentFilter));
  if (currentSearch) list = list.filter(r =>
    r.title.toLowerCase().includes(currentSearch) ||
    r.desc.toLowerCase().includes(currentSearch)
  );
  renderCards(list);
}

document.querySelectorAll('.filter-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    currentFilter = btn.dataset.filter;
    applyFilters();
  });
});

document.getElementById('searchInput').addEventListener('input', e => {
  currentSearch = e.target.value.toLowerCase().trim();
  applyFilters();
});

renderCards(recipes);
</script>
</body>
</html>
