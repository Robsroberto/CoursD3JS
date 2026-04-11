# Chapitre 2 : Introduction à D3.js

## 2.1 Qu'est-ce que D3.js ?

**D3.js** (Data-Driven Documents) est une bibliothèque JavaScript open-source qui permet de créer des visualisations de données dynamiques et interactives dans un navigateur web. Elle utilise les standards web : **SVG**, **HTML**, **CSS** et **JavaScript**.

### Fonctionnement de D3

D3 associe des **données** à des **éléments DOM**. Quand les données changent, le DOM se met à jour automatiquement. C'est la philosophie "data-driven" : ce sont les données qui conduisent le rendu.

---

## 2.2 Installation

### Via CDN (le plus simple)

```html
<script src="https://d3js.org/d3.v7.min.js"></script>
```

### Via npm

```bash
npm install d3
```

```javascript
import * as d3 from 'd3';
```

---

## 2.3 SVG - Le canvas de D3

D3 dessine principalement en **SVG** (Scalable Vector Graphics). Le système de coordonnées SVG place l'origine (0,0) en **haut à gauche**.

```d3
// Créer un SVG avec D3
const svg = d3.select('#chart')
  .append('svg')
  .attr('width', 460)
  .attr('height', 200)
  .style('background', '#f8fafc')
  .style('border-radius', '8px');

// Rectangle
svg.append('rect')
  .attr('x', 20).attr('y', 20)
  .attr('width', 100).attr('height', 60)
  .attr('fill', '#6366f1').attr('rx', 6);

// Cercle
svg.append('circle')
  .attr('cx', 200).attr('cy', 80)
  .attr('r', 45)
  .attr('fill', '#10b981');

// Texte
svg.append('text')
  .attr('x', 320).attr('y', 90)
  .attr('font-size', 16)
  .attr('fill', '#f59e0b')
  .attr('font-weight', 'bold')
  .text('D3.js !');

// Ligne
svg.append('line')
  .attr('x1', 20).attr('y1', 150)
  .attr('x2', 440).attr('y2', 150)
  .attr('stroke', '#94a3b8')
  .attr('stroke-width', 2)
  .attr('stroke-dasharray', '6,3');
```

---

## 2.4 Éléments SVG essentiels

| Élément | Attributs principaux | Usage |
|---------|---------------------|-------|
| `<rect>` | x, y, width, height, rx | Barres, zones |
| `<circle>` | cx, cy, r | Points, bulles |
| `<line>` | x1, y1, x2, y2 | Séparateurs, axes |
| `<path>` | d | Courbes, formes libres |
| `<text>` | x, y, font-size | Labels, titres |
| `<g>` | transform | Grouper des éléments |

---

## 2.5 Sélections D3 - La base

D3 utilise un système de sélections pour manipuler le DOM :

```d3
const data = [60, 40, 75, 30, 85, 50];
const W = 460, H = 200;
const margin = { top: 15, right: 15, bottom: 30, left: 35 };
const w = W - margin.left - margin.right;
const h = H - margin.top - margin.bottom;

const svg = d3.select('#chart').append('svg')
  .attr('width', W).attr('height', H)
  .append('g')
  .attr('transform', `translate(${margin.left},${margin.top})`);

const x = d3.scaleBand().domain(d3.range(data.length)).range([0, w]).padding(0.2);
const y = d3.scaleLinear().domain([0, 100]).range([h, 0]);

svg.append('g').attr('transform', `translate(0,${h})`).call(d3.axisBottom(x).tickFormat(i => `S${i+1}`));
svg.append('g').call(d3.axisLeft(y).ticks(4));

// d3.select()    -> sélectionne UN élément
// d3.selectAll() -> sélectionne TOUS les éléments correspondants
// .data()        -> associe un tableau de données
// .join()        -> crée/met à jour/supprime les éléments

svg.selectAll('rect')
  .data(data)
  .join('rect')
  .attr('x', (d, i) => x(i))
  .attr('y', d => y(d))
  .attr('width', x.bandwidth())
  .attr('height', d => h - y(d))
  .attr('fill', (d, i) => d3.interpolateViridis(i / data.length))
  .attr('rx', 3);
```
