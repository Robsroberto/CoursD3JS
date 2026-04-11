# Chapitre 3 : Sélections et Data Binding

## 3.1 Le concept fondamental de D3

Le **data binding** (liaison de données) est le coeur de D3.js. Il consiste à associer un tableau de données JavaScript à un ensemble d'éléments DOM, puis à définir comment chaque élément doit se comporter en fonction de sa donnée associée.

```
Données  →  D3  →  DOM
[10,20,30] → .data() → [rect, rect, rect]
```

---

## 3.2 Sélections

```javascript
// Sélectionner UN seul élément
d3.select('body')           // par balise
d3.select('#monId')         // par ID
d3.select('.maClasse')      // par classe

// Sélectionner PLUSIEURS éléments
d3.selectAll('rect')
d3.selectAll('.barre')
```

### Chaînage de méthodes

D3 utilise le chaînage : chaque méthode retourne la sélection, ce qui permet d'enchaîner les appels :

```javascript
d3.select('svg')
  .append('circle')       // ajoute un cercle, retourne la sélection du cercle
  .attr('cx', 100)        // fixe l'attribut cx
  .attr('cy', 100)        // fixe cy
  .attr('r', 40)          // fixe r
  .attr('fill', '#6366f1') // fixe la couleur
  .style('opacity', 0.8); // fixe l'opacité CSS
```

---

## 3.3 Le pattern Data Binding : .data().join()

### Pattern moderne (D3 v5+)

```javascript
svg.selectAll('rect')   // cible les rect (même s'ils n'existent pas encore)
  .data(monTableau)     // associe les données
  .join('rect')         // crée/met à jour/supprime automatiquement
  .attr('x', d => ...)  // d = la donnée associée à l'élément
  .attr('y', d => ...)
```

### Les trois états : Enter / Update / Exit

| État | Signification | Action |
|------|--------------|--------|
| **Enter** | Plus de données que d'éléments | Créer de nouveaux éléments |
| **Update** | Données et éléments correspondent | Mettre à jour les existants |
| **Exit** | Plus d'éléments que de données | Supprimer les éléments en trop |

---

## 3.4 Exemple complet : Bar chart avec données réelles

```d3
const ventes = [
  { mois: 'Jan', valeur: 4200 },
  { mois: 'Fev', valeur: 3800 },
  { mois: 'Mar', valeur: 5100 },
  { mois: 'Avr', valeur: 4700 },
  { mois: 'Mai', valeur: 6200 },
  { mois: 'Jun', valeur: 5800 },
];

const W = 460, H = 260;
const m = { top: 20, right: 20, bottom: 40, left: 55 };
const w = W - m.left - m.right, h = H - m.top - m.bottom;

const svg = d3.select('#chart').append('svg')
  .attr('width', W).attr('height', H)
  .append('g').attr('transform', `translate(${m.left},${m.top})`);

const x = d3.scaleBand()
  .domain(ventes.map(d => d.mois))
  .range([0, w]).padding(0.3);

const y = d3.scaleLinear()
  .domain([0, d3.max(ventes, d => d.valeur)])
  .nice().range([h, 0]);

svg.append('g').attr('transform', `translate(0,${h})`)
  .call(d3.axisBottom(x));

svg.append('g')
  .call(d3.axisLeft(y).ticks(5).tickFormat(d => d / 1000 + 'k'));

// Les barres — c'est ici que le data binding agit
svg.selectAll('rect')
  .data(ventes)            // d = { mois, valeur }
  .join('rect')
  .attr('x', d => x(d.mois))
  .attr('y', d => y(d.valeur))
  .attr('width', x.bandwidth())
  .attr('height', d => h - y(d.valeur))
  .attr('fill', '#6366f1')
  .attr('rx', 4);

// Labels au-dessus des barres
svg.selectAll('.lbl')
  .data(ventes)
  .join('text')
  .attr('class', 'lbl')
  .attr('x', d => x(d.mois) + x.bandwidth() / 2)
  .attr('y', d => y(d.valeur) - 5)
  .attr('text-anchor', 'middle')
  .attr('font-size', 11)
  .attr('fill', '#374151')
  .text(d => (d.valeur / 1000).toFixed(1) + 'k');
```
