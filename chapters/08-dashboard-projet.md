# Chapitre 8 : Projet Final - Dashboard D3.js

## 8.1 Architecture d'un Dashboard

Un dashboard D3.js bien structuré sépare :
- **Les données** : un dataset central
- **Les graphiques** : des fonctions render indépendantes
- **Les filtres** : interactions qui déclenchent les mises à jour

### Structure recommandée

```
dashboard/
├── index.html          (layout CSS Grid)
├── data.js             (dataset, fonctions de filtrage)
├── charts/
│   ├── barChart.js
│   ├── lineChart.js
│   └── donutChart.js
└── main.js             (orchestration, filtres)
```

---

## 8.2 KPI Cards - Vue d'ensemble

```d3
const kpis = [
  { label: 'CA Total', value: '12.4M', unit: 'FCFA', delta: '+8%', color: '#6366f1' },
  { label: 'Clients', value: '3 247', unit: 'actifs', delta: '+124', color: '#10b981' },
  { label: 'Commandes', value: '8 901', unit: 'ce mois', delta: '+12%', color: '#f59e0b' },
  { label: 'Panier moyen', value: '1 393', unit: 'FCFA', delta: '+3%', color: '#ef4444' },
];

const W = 460, H = 180;
const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H);

const cardW = W / kpis.length - 8;

kpis.forEach((kpi, i) => {
  const g = svg.append('g').attr('transform', `translate(${i * (cardW + 8) + 4}, 10)`);

  g.append('rect').attr('width', cardW).attr('height', 150)
    .attr('rx', 10).attr('fill', '#1e293b')
    .attr('stroke', kpi.color).attr('stroke-width', 1.5);

  g.append('rect').attr('width', cardW).attr('height', 4).attr('rx', 2)
    .attr('fill', kpi.color);

  g.append('text').attr('x', 12).attr('y', 30)
    .attr('font-size', 11).attr('fill', '#94a3b8').text(kpi.label);

  g.append('text').attr('x', 12).attr('y', 62)
    .attr('font-size', 22).attr('font-weight', 'bold').attr('fill', '#f1f5f9').text(kpi.value);

  g.append('text').attr('x', 12).attr('y', 82)
    .attr('font-size', 10).attr('fill', '#64748b').text(kpi.unit);

  g.append('text').attr('x', 12).attr('y', 112)
    .attr('font-size', 12).attr('fill', kpi.delta.startsWith('+') ? '#10b981' : '#ef4444')
    .attr('font-weight', '600').text(kpi.delta + ' vs mois dernier');
});
```

---

## 8.3 Dashboard Multi-graphiques Complet

```d3
// Dataset ventes par mois et catégorie
const categories = ['Électronique', 'Mode', 'Alimentation', 'Maison'];
const moisLabels = ['Jan','Fev','Mar','Avr','Mai','Jun','Jul','Aoû','Sep','Oct','Nov','Déc'];
const seed = (n, s) => (Math.sin(n * s) * 0.5 + 0.5);

const ventesData = moisLabels.map((m, mi) => ({
  mois: m,
  values: categories.map((c, ci) => ({
    categorie: c,
    valeur: Math.round(seed(mi + 1, ci + 1) * 800 + 200)
  }))
}));

const totauxMois = ventesData.map(d => ({
  mois: d.mois,
  total: d3.sum(d.values, v => v.valeur)
}));

const totauxCat = categories.map((c, ci) => ({
  cat: c,
  total: d3.sum(ventesData, d => d.values[ci].valeur)
}));

const W = 460, H = 580;
const colors = ['#6366f1', '#10b981', '#f59e0b', '#ef4444'];
const catColor = d3.scaleOrdinal(categories, colors);

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H);

// ----- TITRE -----
svg.append('text').attr('x', W / 2).attr('y', 22)
  .attr('text-anchor', 'middle').attr('font-size', 15).attr('font-weight', 'bold')
  .attr('fill', '#1e293b').text('Dashboard des Ventes - Annuel');

// ----- GRAPHE 1 : Courbe totaux mensuels -----
const m1 = { top: 40, right: 15, bottom: 35, left: 45 };
const w1 = W - m1.left - m1.right, h1 = 140;
const g1 = svg.append('g').attr('transform', `translate(${m1.left},${m1.top})`);

const x1 = d3.scaleBand().domain(moisLabels).range([0, w1]).padding(0);
const y1 = d3.scaleLinear().domain([0, d3.max(totauxMois, d => d.total)]).nice().range([h1, 0]);

const line1 = d3.line().x(d => x1(d.mois) + x1.bandwidth() / 2).y(d => y1(d.total)).curve(d3.curveMonotoneX);
const area1 = d3.area().x(d => x1(d.mois) + x1.bandwidth() / 2).y0(h1).y1(d => y1(d.total)).curve(d3.curveMonotoneX);

g1.append('text').attr('x', 0).attr('y', -8).attr('font-size', 11).attr('fill', '#64748b').text('CA mensuel total');
g1.append('g').attr('transform', `translate(0,${h1})`).call(d3.axisBottom(x1).tickSize(0)).selectAll('text').attr('font-size', 9);
g1.append('g').call(d3.axisLeft(y1).ticks(4).tickFormat(d => d / 1000 + 'k')).select('.domain').remove();
g1.append('path').datum(totauxMois).attr('d', area1).attr('fill', '#6366f1').attr('opacity', 0.1);
g1.append('path').datum(totauxMois).attr('d', line1).attr('fill', 'none').attr('stroke', '#6366f1').attr('stroke-width', 2.5);

// ----- GRAPHE 2 : Bar chart par catégorie -----
const m2 = { top: 220, right: 15, bottom: 60, left: 45 };
const w2 = W - m2.left - m2.right, h2 = 140;
const g2 = svg.append('g').attr('transform', `translate(${m2.left},${m2.top})`);

const x2 = d3.scaleBand().domain(categories).range([0, w2]).padding(0.3);
const y2 = d3.scaleLinear().domain([0, d3.max(totauxCat, d => d.total)]).nice().range([h2, 0]);

g2.append('text').attr('x', 0).attr('y', -8).attr('font-size', 11).attr('fill', '#64748b').text('Ventes par catégorie (annuel)');
g2.append('g').attr('transform', `translate(0,${h2})`).call(d3.axisBottom(x2).tickSize(0)).selectAll('text').attr('font-size', 10).attr('transform', 'rotate(-10)').style('text-anchor', 'end');
g2.append('g').call(d3.axisLeft(y2).ticks(4).tickFormat(d => d / 1000 + 'k')).select('.domain').remove();
g2.selectAll('rect').data(totauxCat).join('rect')
  .attr('x', d => x2(d.cat)).attr('y', d => y2(d.total))
  .attr('width', x2.bandwidth()).attr('height', d => h2 - y2(d.total))
  .attr('fill', d => catColor(d.cat)).attr('rx', 5);

// ----- GRAPHE 3 : Donut répartition -----
const m3 = { top: 420, cx: W / 2, cy: 80 };
const g3 = svg.append('g').attr('transform', `translate(${m3.cx},${m3.top + m3.cy})`);
const r3 = 65;
const pie3 = d3.pie().value(d => d.total).sort(null);
const arc3 = d3.arc().innerRadius(r3 * 0.6).outerRadius(r3);

g3.append('text').attr('text-anchor', 'middle').attr('y', -r3 - 12)
  .attr('font-size', 11).attr('fill', '#64748b').text('Répartition par catégorie');

g3.selectAll('path').data(pie3(totauxCat)).join('path')
  .attr('d', arc3).attr('fill', d => catColor(d.data.cat))
  .attr('stroke', '#fff').attr('stroke-width', 2);

const legG = svg.append('g').attr('transform', `translate(${W - 140}, 430)`);
totauxCat.forEach((d, i) => {
  legG.append('rect').attr('y', i * 22).attr('width', 12).attr('height', 12).attr('rx', 3).attr('fill', catColor(d.cat));
  legG.append('text').attr('x', 18).attr('y', i * 22 + 10).attr('font-size', 11).attr('fill', '#374151').text(d.cat);
});
```

---

## 8.4 Conseils pour aller plus loin

| Technique | Bibliothèque / Méthode |
|-----------|----------------------|
| **Carte géographique** | D3 GeoJSON + `d3.geoMercator()` |
| **Graphe de réseau** | `d3.forceSimulation()` |
| **Treemap** | `d3.treemap()` |
| **Timeline** | `d3.scaleTime()` + brushing |
| **Animation au scroll** | IntersectionObserver + transitions |
| **Export SVG** | `new Blob([svg.outerHTML])` |
| **React + D3** | useRef + useEffect pour cibler le DOM |

> **Bonnes pratiques** : Toujours utiliser la "margin convention", déclarer les échelles avec `.nice()`, préférer `.join()` à `.enter().append()`, et séparer les données du rendu.
