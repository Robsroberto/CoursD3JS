# Chapitre 7 : TD et Exercices Pratiques

## 7.1 Exercice 1 : Bar Chart des températures

Visualiser les températures moyennes mensuelles de Dakar.

```d3
const data = [
  { mois: 'Jan', tmin: 18, tmax: 27 },
  { mois: 'Fev', tmin: 18, tmax: 28 },
  { mois: 'Mar', tmin: 19, tmax: 29 },
  { mois: 'Avr', tmin: 20, tmax: 30 },
  { mois: 'Mai', tmin: 22, tmax: 31 },
  { mois: 'Jun', tmin: 24, tmax: 33 },
  { mois: 'Jul', tmin: 25, tmax: 32 },
  { mois: 'Aoû', tmin: 25, tmax: 32 },
  { mois: 'Sep', tmin: 25, tmax: 33 },
  { mois: 'Oct', tmin: 24, tmax: 32 },
  { mois: 'Nov', tmin: 22, tmax: 30 },
  { mois: 'Dec', tmin: 19, tmax: 28 },
];

const W = 460, H = 260, m = { top: 20, right: 15, bottom: 40, left: 40 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleBand().domain(data.map(d => d.mois)).range([0, w]).padding(0.15);
const y = d3.scaleLinear().domain([10, 36]).range([h, 0]);

svg.append('g').attr('transform', `translate(0,${h})`)
  .call(d3.axisBottom(x))
  .selectAll('text').attr('font-size', 10);
svg.append('g').call(d3.axisLeft(y).ticks(6).tickFormat(d => d + '°'));

// Barres tmax (rouge)
svg.selectAll('.tmax').data(data).join('rect')
  .attr('class', 'tmax')
  .attr('x', d => x(d.mois))
  .attr('y', d => y(d.tmax))
  .attr('width', x.bandwidth() / 2)
  .attr('height', d => h - y(d.tmax))
  .attr('fill', '#ef4444').attr('rx', 2);

// Barres tmin (bleu)
svg.selectAll('.tmin').data(data).join('rect')
  .attr('class', 'tmin')
  .attr('x', d => x(d.mois) + x.bandwidth() / 2)
  .attr('y', d => y(d.tmin))
  .attr('width', x.bandwidth() / 2)
  .attr('height', d => h - y(d.tmin))
  .attr('fill', '#3b82f6').attr('rx', 2);

// Légende
const leg = svg.append('g').attr('transform', `translate(${w - 100}, 0)`);
[{c:'#ef4444',t:'Tmax'},{c:'#3b82f6',t:'Tmin'}].forEach(({c,t}, i) => {
  leg.append('rect').attr('x', 0).attr('y', i * 18).attr('width', 12).attr('height', 12).attr('fill', c).attr('rx', 2);
  leg.append('text').attr('x', 16).attr('y', i * 18 + 10).attr('font-size', 11).attr('fill', '#374151').text(t);
});
```

---

## 7.2 Exercice 2 : Courbe de croissance

Visualiser la croissance des utilisateurs d'une application sur 24 mois.

```d3
const mois = d3.range(24);
const utilisateurs = mois.map(m => Math.round(200 * Math.pow(1.12, m) + Math.random() * 100));

const W = 460, H = 240, mar = { top: 20, right: 20, bottom: 35, left: 60 };
const w = W - mar.left - mar.right, h = H - mar.top - mar.bottom;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${mar.left},${mar.top})`);

const x = d3.scaleLinear().domain([0, 23]).range([0, w]);
const y = d3.scaleLinear().domain([0, d3.max(utilisateurs)]).nice().range([h, 0]);

// Grille horizontale
svg.append('g').attr('class', 'grid')
  .call(d3.axisLeft(y).ticks(5).tickSize(-w).tickFormat(''))
  .selectAll('line').attr('stroke', '#e2e8f0');

svg.append('g').attr('transform', `translate(0,${h})`)
  .call(d3.axisBottom(x).ticks(8).tickFormat(d => `M${d + 1}`));
svg.append('g').call(d3.axisLeft(y).ticks(5).tickFormat(d => d >= 1000 ? (d/1000).toFixed(0) + 'k' : d));

// Zone
const area = d3.area().x((d, i) => x(i)).y0(h).y1(d => y(d)).curve(d3.curveMonotoneX);
svg.append('path').datum(utilisateurs).attr('d', area)
  .attr('fill', '#6366f1').attr('opacity', 0.1);

// Courbe
const line = d3.line().x((d, i) => x(i)).y(d => y(d)).curve(d3.curveMonotoneX);
svg.append('path').datum(utilisateurs).attr('d', line)
  .attr('fill', 'none').attr('stroke', '#6366f1').attr('stroke-width', 2.5);

// Valeur finale
const last = utilisateurs[23];
svg.append('text')
  .attr('x', w).attr('y', y(last) - 8)
  .attr('text-anchor', 'end').attr('font-size', 12)
  .attr('fill', '#6366f1').attr('font-weight', 'bold')
  .text(last.toLocaleString() + ' users');
```

---

## 7.3 Exercice 3 : Répartition budget

Visualiser la répartition d'un budget annuel par poste en donut chart.

```d3
const budget = [
  { poste: 'Salaires', montant: 450000, color: '#6366f1' },
  { poste: 'Matériel', montant: 120000, color: '#10b981' },
  { poste: 'Marketing', montant: 80000, color: '#f59e0b' },
  { poste: 'Formation', montant: 55000, color: '#ef4444' },
  { poste: 'Loyer', montant: 95000, color: '#3b82f6' },
  { poste: 'Divers', montant: 30000, color: '#8b5cf6' },
];

const total = d3.sum(budget, d => d.montant);
const W = 460, H = 260, r = 90;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H);
const g = svg.append('g').attr('transform', `translate(${r + 20},${H / 2})`);

const pie = d3.pie().value(d => d.montant).sort(null);
const arc = d3.arc().innerRadius(r * 0.55).outerRadius(r);
const arcHover = d3.arc().innerRadius(r * 0.55).outerRadius(r + 8);

g.selectAll('path').data(pie(budget)).join('path')
  .attr('d', arc)
  .attr('fill', d => d.data.color)
  .attr('stroke', '#fff').attr('stroke-width', 2)
  .on('mouseover', function() { d3.select(this).transition().duration(150).attr('d', arcHover); })
  .on('mouseout', function() { d3.select(this).transition().duration(150).attr('d', arc); });

// Total au centre
g.append('text').attr('text-anchor', 'middle').attr('dy', '-6')
  .attr('font-size', 13).attr('fill', '#374151').attr('font-weight', 'bold')
  .text('Total');
g.append('text').attr('text-anchor', 'middle').attr('dy', '14')
  .attr('font-size', 12).attr('fill', '#6b7280')
  .text((total / 1000).toFixed(0) + 'k FCFA');

// Légende
const leg = svg.append('g').attr('transform', `translate(${r * 2 + 40}, 20)`);
budget.forEach((d, i) => {
  const row = leg.append('g').attr('transform', `translate(0,${i * 36})`);
  row.append('rect').attr('width', 12).attr('height', 12).attr('rx', 3).attr('fill', d.color);
  row.append('text').attr('x', 18).attr('y', 10).attr('font-size', 11).attr('fill', '#374151').text(d.poste);
  row.append('text').attr('x', 18).attr('y', 24).attr('font-size', 10).attr('fill', '#6b7280')
    .text((d.montant / 1000).toFixed(0) + 'k - ' + Math.round(d.montant / total * 100) + '%');
});
```
