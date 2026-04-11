# Chapitre 4 : Création de Graphiques de Base

## 4.1 Les Échelles (Scales)

Les échelles sont des fonctions qui transforment vos données en pixels. C'est l'outil le plus important de D3.

| Échelle | Usage | Exemple |
|---------|-------|---------|
| `d3.scaleLinear()` | Valeurs continues | Températures, prix |
| `d3.scaleBand()` | Catégories en barres | Mois, noms |
| `d3.scaleTime()` | Dates | Séries temporelles |
| `d3.scaleOrdinal()` | Catégories → couleurs | Légendes |
| `d3.scaleSqrt()` | Aires de cercles | Graphiques à bulles |
| `d3.scaleLog()` | Données exponentielles | Magnitude, population |

### Anatomy d'une échelle

```javascript
const y = d3.scaleLinear()
  .domain([0, 100])   // plage des données (min, max)
  .range([400, 0])    // plage en pixels (bas, haut — inversé pour SVG)
  .nice();            // arrondit les extremes pour des axes propres

// Utilisation :
y(50)  // → 200 (pixels)
y(0)   // → 400 (pixels, en bas)
y(100) // → 0   (pixels, en haut)
```

---

## 4.2 Bar Chart (Histogramme)

```d3
const data = [
  { pays: 'Sénégal', pib: 27.6 },
  { pays: 'Côte Ivoire', pib: 70.0 },
  { pays: 'Ghana', pib: 76.0 },
  { pays: 'Cameroun', pib: 47.0 },
  { pays: 'Mali', pib: 19.1 },
];

const W = 460, H = 260, m = { top: 15, right: 20, bottom: 60, left: 50 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleBand().domain(data.map(d => d.pays)).range([0, w]).padding(0.3);
const y = d3.scaleLinear().domain([0, d3.max(data, d => d.pib)]).nice().range([h, 0]);
const color = d3.scaleOrdinal(['#6366f1','#10b981','#f59e0b','#ef4444','#3b82f6']);

svg.append('g').attr('transform', `translate(0,${h})`)
  .call(d3.axisBottom(x))
  .selectAll('text')
  .attr('transform', 'rotate(-15)')
  .style('text-anchor', 'end')
  .attr('dx', '-0.4em').attr('dy', '0.6em');

svg.append('g').call(d3.axisLeft(y).ticks(5).tickFormat(d => d + 'B$'));

svg.selectAll('rect').data(data).join('rect')
  .attr('x', d => x(d.pays))
  .attr('y', d => y(d.pib))
  .attr('width', x.bandwidth())
  .attr('height', d => h - y(d.pib))
  .attr('fill', (d, i) => color(i))
  .attr('rx', 4);
```

---

## 4.3 Graphique Linéaire (Line Chart)

```d3
const data = [
  { mois: 0, temp: 23 }, { mois: 1, temp: 25 },
  { mois: 2, temp: 28 }, { mois: 3, temp: 30 },
  { mois: 4, temp: 33 }, { mois: 5, temp: 31 },
  { mois: 6, temp: 28 }, { mois: 7, temp: 26 },
  { mois: 8, temp: 24 }, { mois: 9, temp: 22 },
  { mois: 10, temp: 21 }, { mois: 11, temp: 22 },
];
const mois = ['Jan','Fev','Mar','Avr','Mai','Jun','Jul','Aoû','Sep','Oct','Nov','Déc'];

const W = 460, H = 240, m = { top: 15, right: 20, bottom: 35, left: 40 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleLinear().domain([0, 11]).range([0, w]);
const y = d3.scaleLinear().domain([18, 36]).range([h, 0]);

svg.append('g').attr('transform', `translate(0,${h})`)
  .call(d3.axisBottom(x).ticks(11).tickFormat(i => mois[i]));
svg.append('g').call(d3.axisLeft(y).ticks(6).tickFormat(d => d + '°C'));

// Zone sous la courbe
const area = d3.area()
  .x(d => x(d.mois)).y0(h).y1(d => y(d.temp))
  .curve(d3.curveCatmullRom);

svg.append('path').datum(data).attr('d', area)
  .attr('fill', '#6366f1').attr('opacity', 0.15);

// Courbe
const line = d3.line()
  .x(d => x(d.mois)).y(d => y(d.temp))
  .curve(d3.curveCatmullRom);

svg.append('path').datum(data).attr('d', line)
  .attr('fill', 'none').attr('stroke', '#6366f1')
  .attr('stroke-width', 2.5);

// Points
svg.selectAll('circle').data(data).join('circle')
  .attr('cx', d => x(d.mois)).attr('cy', d => y(d.temp))
  .attr('r', 4).attr('fill', '#6366f1').attr('stroke', '#fff').attr('stroke-width', 2);
```

---

## 4.4 Graphique Circulaire (Pie / Donut)

```d3
const data = [
  { label: 'Web', valeur: 35 },
  { label: 'Mobile', valeur: 28 },
  { label: 'Desktop', valeur: 20 },
  { label: 'Tablette', valeur: 12 },
  { label: 'Autre', valeur: 5 },
];

const W = 460, H = 260;
const radius = Math.min(W, H) / 2 - 20;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${W / 2 - 40},${H / 2})`);

const color = d3.scaleOrdinal(['#6366f1','#10b981','#f59e0b','#ef4444','#3b82f6']);

const pie = d3.pie().value(d => d.valeur).sort(null);
const arc = d3.arc().innerRadius(radius * 0.5).outerRadius(radius); // Donut
const arcHover = d3.arc().innerRadius(radius * 0.5).outerRadius(radius + 8);

const arcs = svg.selectAll('path').data(pie(data)).join('path')
  .attr('d', arc)
  .attr('fill', (d, i) => color(i))
  .attr('stroke', '#fff').attr('stroke-width', 2)
  .on('mouseover', function(event, d) {
    d3.select(this).attr('d', arcHover);
  })
  .on('mouseout', function(event, d) {
    d3.select(this).attr('d', arc);
  });

// Labels
const labelArc = d3.arc().innerRadius(radius * 0.8).outerRadius(radius * 0.8);
svg.selectAll('text').data(pie(data)).join('text')
  .attr('transform', d => `translate(${labelArc.centroid(d)})`)
  .attr('text-anchor', 'middle').attr('font-size', 12).attr('fill', '#fff')
  .text(d => d.data.valeur + '%');

// Légende à droite
const legend = d3.select('#chart').select('svg').append('g')
  .attr('transform', `translate(${W - 90}, 40)`);

data.forEach((d, i) => {
  legend.append('rect').attr('x', 0).attr('y', i * 22)
    .attr('width', 12).attr('height', 12).attr('rx', 2)
    .attr('fill', color(i));
  legend.append('text').attr('x', 18).attr('y', i * 22 + 10)
    .attr('font-size', 11).attr('fill', '#374151').text(d.label);
});
```

---

## 4.5 Nuage de Points (Scatter Plot)

```d3
const data = Array.from({ length: 40 }, (_, i) => ({
  x: Math.random() * 90 + 10,
  y: Math.random() * 90 + 10,
  r: Math.random() * 12 + 4,
  cat: ['A', 'B', 'C'][Math.floor(Math.random() * 3)]
}));

const W = 460, H = 260, m = { top: 15, right: 20, bottom: 35, left: 40 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleLinear().domain([0, 100]).range([0, w]);
const y = d3.scaleLinear().domain([0, 100]).range([h, 0]);
const color = d3.scaleOrdinal(['A','B','C'], ['#6366f1','#10b981','#f59e0b']);

svg.append('g').attr('transform', `translate(0,${h})`).call(d3.axisBottom(x).ticks(5));
svg.append('g').call(d3.axisLeft(y).ticks(5));

svg.selectAll('circle').data(data).join('circle')
  .attr('cx', d => x(d.x))
  .attr('cy', d => y(d.y))
  .attr('r', d => d.r)
  .attr('fill', d => color(d.cat))
  .attr('opacity', 0.7)
  .attr('stroke', '#fff')
  .attr('stroke-width', 1);
```
