# Chapitre 6 : Graphiques Avancés

## 6.1 Graphique Radar (Spider Chart)

Idéal pour comparer plusieurs variables sur un même individu ou plusieurs profils.

```d3
const axes = ['Vitesse', 'Force', 'Endurance', 'Agilité', 'Technique'];
const profils = [
  { nom: 'Joueur A', vals: [85, 70, 60, 90, 75], color: '#6366f1' },
  { nom: 'Joueur B', vals: [60, 90, 80, 50, 85], color: '#10b981' },
];

const W = 460, H = 280;
const cx = W / 2, cy = H / 2, r = 100;
const n = axes.length;
const angle = i => (i / n) * 2 * Math.PI - Math.PI / 2;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H);

// Toiles (cercles guides)
[20, 40, 60, 80, 100].forEach(v => {
  const pts = axes.map((_, i) => {
    const a = angle(i), rr = (v / 100) * r;
    return [cx + rr * Math.cos(a), cy + rr * Math.sin(a)];
  });
  svg.append('polygon')
    .attr('points', pts.map(p => p.join(',')).join(' '))
    .attr('fill', 'none').attr('stroke', '#cbd5e1').attr('stroke-width', 0.5);
});

// Axes radiaux + labels
axes.forEach((a, i) => {
  const x2 = cx + r * Math.cos(angle(i)), y2 = cy + r * Math.sin(angle(i));
  svg.append('line').attr('x1', cx).attr('y1', cy).attr('x2', x2).attr('y2', y2)
    .attr('stroke', '#94a3b8').attr('stroke-width', 1);
  svg.append('text').attr('x', cx + (r + 16) * Math.cos(angle(i)))
    .attr('y', cy + (r + 16) * Math.sin(angle(i)))
    .attr('text-anchor', 'middle').attr('dominant-baseline', 'middle')
    .attr('font-size', 11).attr('fill', '#374151').text(a);
});

// Profils
profils.forEach(({ vals, color, nom }) => {
  const pts = vals.map((v, i) => {
    const a = angle(i), rr = (v / 100) * r;
    return [cx + rr * Math.cos(a), cy + rr * Math.sin(a)];
  });
  svg.append('polygon')
    .attr('points', pts.map(p => p.join(',')).join(' '))
    .attr('fill', color).attr('opacity', 0.25)
    .attr('stroke', color).attr('stroke-width', 2);
});

// Légende
profils.forEach(({ nom, color }, i) => {
  const g = svg.append('g').attr('transform', `translate(${W - 110}, ${20 + i * 22})`);
  g.append('rect').attr('width', 12).attr('height', 12).attr('rx', 2).attr('fill', color);
  g.append('text').attr('x', 18).attr('y', 10).attr('font-size', 12).attr('fill', '#374151').text(nom);
});
```

---

## 6.2 Carte de Chaleur (Heatmap)

```d3
const jours = ['Lun', 'Mar', 'Mer', 'Jeu', 'Ven', 'Sam', 'Dim'];
const heures = d3.range(8, 20); // 8h à 19h

const data = [];
jours.forEach((j, ji) => {
  heures.forEach((h, hi) => {
    data.push({ jour: j, heure: h, val: Math.floor(Math.random() * 100) });
  });
});

const W = 460, H = 200, m = { top: 10, right: 20, bottom: 30, left: 35 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleBand().domain(heures).range([0, w]).padding(0.05);
const y = d3.scaleBand().domain(jours).range([0, h]).padding(0.05);
const color = d3.scaleSequential(d3.interpolateYlOrRd).domain([0, 100]);

svg.append('g').attr('transform', `translate(0,${h})`)
  .call(d3.axisBottom(x).tickFormat(d => d + 'h'));
svg.append('g').call(d3.axisLeft(y));

svg.selectAll('rect').data(data).join('rect')
  .attr('x', d => x(d.heure))
  .attr('y', d => y(d.jour))
  .attr('width', x.bandwidth())
  .attr('height', y.bandwidth())
  .attr('fill', d => color(d.val))
  .attr('rx', 2);
```

---

## 6.3 Graphique à Bulles (Bubble Chart)

```d3
const data = [
  { pays: 'Nigeria', pop: 220, pib: 440, region: 'Ouest' },
  { pays: 'Ethiopie', pop: 120, pib: 111, region: 'Est' },
  { pays: 'Egypte', pop: 104, pib: 404, region: 'Nord' },
  { pays: 'Sénégal', pop: 17, pib: 28, region: 'Ouest' },
  { pays: 'Côte Ivoire', pop: 27, pib: 70, region: 'Ouest' },
  { pays: 'Ghana', pop: 32, pib: 76, region: 'Ouest' },
  { pays: 'Kenya', pop: 55, pib: 110, region: 'Est' },
  { pays: 'Maroc', pop: 37, pib: 142, region: 'Nord' },
];

const W = 460, H = 270, m = { top: 15, right: 15, bottom: 40, left: 50 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleLinear().domain([0, 500]).range([0, w]);
const y = d3.scaleLinear().domain([0, 250]).range([h, 0]);
const r = d3.scaleSqrt().domain([0, 220]).range([4, 40]);
const color = d3.scaleOrdinal(['Ouest','Est','Nord'], ['#6366f1','#10b981','#f59e0b']);

svg.append('g').attr('transform', `translate(0,${h})`)
  .call(d3.axisBottom(x).ticks(5).tickFormat(d => d + 'B$'))
  .append('text').attr('x', w / 2).attr('y', 35)
  .attr('fill', '#374151').attr('text-anchor', 'middle').text('PIB (Milliards $)');

svg.append('g').call(d3.axisLeft(y).ticks(5).tickFormat(d => d + 'M'));

svg.selectAll('circle').data(data).join('circle')
  .attr('cx', d => x(d.pib))
  .attr('cy', d => y(d.pop))
  .attr('r', d => r(d.pop))
  .attr('fill', d => color(d.region))
  .attr('opacity', 0.7)
  .attr('stroke', '#fff').attr('stroke-width', 1.5);

svg.selectAll('.lbl').data(data).join('text')
  .attr('class', 'lbl')
  .attr('x', d => x(d.pib))
  .attr('y', d => y(d.pop) - r(d.pop) - 3)
  .attr('text-anchor', 'middle')
  .attr('font-size', 10).attr('fill', '#374151')
  .text(d => d.pays);
```
