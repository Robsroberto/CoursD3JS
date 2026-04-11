# Chapitre 5 : Transitions, Animations et Interactions

## 5.1 Les Transitions

Une **transition** en D3 permet d'animer le passage d'un état à un autre de manière fluide.

```javascript
selection
  .transition()          // démarre une transition
  .duration(800)         // durée en millisecondes
  .delay(200)            // délai avant de démarrer
  .ease(d3.easeCubicOut) // fonction d'accélération
  .attr('height', 100)   // valeur cible
```

### Fonctions d'easing disponibles

| Fonction | Effet |
|----------|-------|
| `d3.easeLinear` | Vitesse constante |
| `d3.easeCubicOut` | Ralentit à la fin (par défaut) |
| `d3.easeElastic` | Rebond élastique |
| `d3.easeBounce` | Effet rebond |
| `d3.easeBack` | Légère surtension |

---

## 5.2 Bar Chart animé au chargement

```d3
const data = [65, 40, 85, 55, 75, 30, 90, 50];
const W = 460, H = 250, m = { top: 15, right: 15, bottom: 35, left: 40 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleBand().domain(d3.range(data.length)).range([0, w]).padding(0.25);
const y = d3.scaleLinear().domain([0, 100]).range([h, 0]);
const color = d3.scaleSequential(d3.interpolateViridis).domain([0, data.length]);

svg.append('g').attr('transform', `translate(0,${h})`).call(d3.axisBottom(x).tickFormat(i => `V${i + 1}`));
svg.append('g').call(d3.axisLeft(y).ticks(5));

// Les barres démarrent à 0 et montent avec une transition
svg.selectAll('rect')
  .data(data)
  .join('rect')
  .attr('x', (d, i) => x(i))
  .attr('y', h)              // départ en bas
  .attr('width', x.bandwidth())
  .attr('height', 0)         // hauteur 0 au départ
  .attr('fill', (d, i) => color(i))
  .attr('rx', 4)
  .transition()              // ANIMATION
  .duration(800)
  .delay((d, i) => i * 80)  // effet cascade
  .ease(d3.easeCubicOut)
  .attr('y', d => y(d))     // position cible
  .attr('height', d => h - y(d)); // hauteur cible
```

---

## 5.3 Interactions - Survol et Tooltip

```d3
const data = [
  { label: 'Jan', valeur: 4200, detail: 'Premier trimestre' },
  { label: 'Fev', valeur: 3800, detail: 'Vacances scolaires' },
  { label: 'Mar', valeur: 5100, detail: 'Fin T1' },
  { label: 'Avr', valeur: 4700, detail: 'Début T2' },
  { label: 'Mai', valeur: 6200, detail: 'Pic de ventes' },
  { label: 'Jun', valeur: 5500, detail: 'Fin T2' },
];

const W = 460, H = 250, m = { top: 15, right: 15, bottom: 35, left: 50 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

// Tooltip
const tooltip = d3.select('#chart').append('div')
  .style('position', 'absolute')
  .style('background', '#1e293b')
  .style('color', '#f1f5f9')
  .style('padding', '8px 12px')
  .style('border-radius', '6px')
  .style('font-size', '12px')
  .style('pointer-events', 'none')
  .style('opacity', 0)
  .style('transition', 'opacity 0.2s');

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .style('overflow', 'visible')
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleBand().domain(data.map(d => d.label)).range([0, w]).padding(0.3);
const y = d3.scaleLinear().domain([0, d3.max(data, d => d.valeur)]).nice().range([h, 0]);

svg.append('g').attr('transform', `translate(0,${h})`).call(d3.axisBottom(x));
svg.append('g').call(d3.axisLeft(y).ticks(5).tickFormat(d => d / 1000 + 'k'));

svg.selectAll('rect').data(data).join('rect')
  .attr('x', d => x(d.label))
  .attr('y', d => y(d.valeur))
  .attr('width', x.bandwidth())
  .attr('height', d => h - y(d.valeur))
  .attr('fill', '#6366f1').attr('rx', 4)
  .style('cursor', 'pointer')
  .on('mouseover', function(event, d) {
    d3.select(this).transition().duration(150).attr('fill', '#818cf8');
    tooltip.style('opacity', 1)
      .html(`<strong>${d.label}</strong><br>${d.valeur.toLocaleString()} FCFA<br><em>${d.detail}</em>`);
  })
  .on('mousemove', function(event) {
    tooltip.style('left', (event.pageX + 12) + 'px').style('top', (event.pageY - 30) + 'px');
  })
  .on('mouseout', function() {
    d3.select(this).transition().duration(150).attr('fill', '#6366f1');
    tooltip.style('opacity', 0);
  });
```

---

## 5.4 Mise à jour dynamique des données

```d3
let dataset = [40, 65, 25, 80, 55, 70, 35];
const W = 460, H = 220, m = { top: 15, right: 15, bottom: 30, left: 35 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

d3.select('#chart').append('button')
  .text('Nouvelles données')
  .style('margin', '8px')
  .style('padding', '6px 14px')
  .style('background', '#6366f1')
  .style('color', '#fff')
  .style('border', 'none')
  .style('border-radius', '6px')
  .style('cursor', 'pointer')
  .on('click', update);

const svg = d3.select('#chart').append('svg').attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleBand().domain(d3.range(dataset.length)).range([0, w]).padding(0.25);
const y = d3.scaleLinear().domain([0, 100]).range([h, 0]);

const xAxis = svg.append('g').attr('transform', `translate(0,${h})`).call(d3.axisBottom(x).tickFormat(i => `D${i+1}`));
svg.append('g').call(d3.axisLeft(y).ticks(4));

function update() {
  dataset = dataset.map(() => Math.floor(Math.random() * 90) + 10);

  // Mise à jour avec transition fluide
  svg.selectAll('rect')
    .data(dataset)
    .join('rect')
    .attr('x', (d, i) => x(i))
    .attr('width', x.bandwidth())
    .attr('rx', 4)
    .attr('fill', (d, i) => d3.interpolateRainbow(i / dataset.length))
    .transition().duration(600).ease(d3.easeCubicInOut)
    .attr('y', d => y(d))
    .attr('height', d => h - y(d));
}

update();
