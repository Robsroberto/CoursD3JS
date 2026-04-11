# Chapitre 1 : Introduction à la Visualisation de Données

## 1.1 Qu'est-ce que la Visualisation de Données ?

La visualisation de données est le processus de transformation de données brutes en représentations graphiques, permettant de faciliter leur interprétation et de communiquer des informations de manière efficace.

### Pourquoi visualiser les données ?

- **Synthétiser** des ensembles de données complexes en représentations lisibles
- **Détecter rapidement** des tendances, anomalies ou patterns
- **Améliorer la prise de décision** grâce à des informations visuelles claires
- **Communiquer efficacement** des résultats à un large public

---

## 1.2 Principes de Base d'une Bonne Visualisation

### 1.2.1 Variables Visuelles

Les variables visuelles sont les éléments graphiques utilisés pour représenter les données :

| Variable | Description | Exemple |
|----------|-------------|---------|
| **Position** | Emplacement sur les axes X et Y | Graphique en nuage de points |
| **Couleur** | Indique des catégories ou intensités | Carte de chaleur |
| **Taille** | Représente des valeurs numériques | Graphique à bulles |
| **Forme** | Distinction entre catégories | Symboles différents par série |

### 1.2.2 Échelles

Les échelles traduisent les valeurs des données en représentations visuelles :

- **Échelles linéaires** : pour des valeurs continues (températures, distances)
- **Échelles logarithmiques** : pour des données avec de grands écarts
- **Échelles ordinales** : pour des catégories (noms, labels)

---

## 1.3 Types de Graphiques et leurs Usages

| Type de Graphique | Cas d'utilisation |
|-------------------|-------------------|
| **Barres** | Comparer des valeurs entre catégories |
| **Courbes** | Montrer l'évolution dans le temps |
| **Camembert / Donut** | Répartition proportionnelle d'un total |
| **Nuage de points** | Corréler deux variables quantitatives |
| **Carte de chaleur** | Intensité sur une grille 2D |
| **Histogramme** | Distribution d'une variable continue |

---

## 1.4 Exemple interactif : Premier graphique en barres

```d3
const data = [45, 80, 30, 65, 90, 55, 70];
const labels = ['Lun', 'Mar', 'Mer', 'Jeu', 'Ven', 'Sam', 'Dim'];
const width = 500, height = 280;
const margin = { top: 20, right: 20, bottom: 40, left: 40 };
const W = width - margin.left - margin.right;
const H = height - margin.top - margin.bottom;

const svg = d3.select('#chart')
  .append('svg')
  .attr('width', width)
  .attr('height', height)
  .append('g')
  .attr('transform', `translate(${margin.left},${margin.top})`);

const x = d3.scaleBand().domain(labels).range([0, W]).padding(0.25);
const y = d3.scaleLinear().domain([0, 100]).range([H, 0]);
const color = d3.scaleOrdinal(d3.schemeTableau10);

svg.append('g').attr('transform', `translate(0,${H})`).call(d3.axisBottom(x));
svg.append('g').call(d3.axisLeft(y).ticks(5).tickFormat(d => d + '%'));

svg.selectAll('rect')
  .data(data)
  .join('rect')
  .attr('x', (d, i) => x(labels[i]))
  .attr('y', d => y(d))
  .attr('width', x.bandwidth())
  .attr('height', d => H - y(d))
  .attr('fill', (d, i) => color(i))
  .attr('rx', 4);

svg.selectAll('.label')
  .data(data)
  .join('text')
  .attr('class', 'label')
  .attr('x', (d, i) => x(labels[i]) + x.bandwidth() / 2)
  .attr('y', d => y(d) - 5)
  .attr('text-anchor', 'middle')
  .attr('font-size', 11)
  .attr('fill', '#333')
  .text(d => d + '%');
```

---

## 1.5 Pourquoi D3.js ?

**D3.js** (Data-Driven Documents) est la bibliothèque JavaScript la plus puissante pour la visualisation de données sur le web.

### D3.js vs autres bibliothèques

| | D3.js | Chart.js | Highcharts |
|-|-------|----------|------------|
| **Flexibilité** | Totale | Limitée | Moyenne |
| **Courbe d'apprentissage** | Élevée | Faible | Faible |
| **Personnalisation** | Illimitée | Templates | Limitée |
| **Taille** | 87 Ko | 63 Ko | 300 Ko |
| **Standard web** | SVG/HTML/CSS natifs | Canvas | SVG propriétaire |

D3 est le bon choix quand tu veux un **contrôle total** sur le rendu et créer des visualisations sur mesure impossibles avec les autres bibliothèques.
