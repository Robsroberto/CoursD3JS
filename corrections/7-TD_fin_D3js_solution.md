
### **1. Graphique à Barres : Evolution des Ventes Mensuelles**
**Données** :

```json
[
  { "mois": "Janvier", "ventes": 100 },
  { "mois": "Février", "ventes": 200 },
  { "mois": "Mars", "ventes": 300 },
  { "mois": "Avril", "ventes": 400 }
]
```

**Solution** :
Nous allons créer un graphique à barres qui montre l'évolution des ventes chaque mois.

```javascript
const data = [
  { "mois": "Janvier", "ventes": 100 },
  { "mois": "Février", "ventes": 200 },
  { "mois": "Mars", "ventes": 300 },
  { "mois": "Avril", "ventes": 400 }
];

const width = 500, height = 300;

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

const x = d3.scaleBand()
  .domain(data.map(d => d.mois))
  .range([0, width])
  .padding(0.1);

const y = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.ventes)])
  .nice()
  .range([height, 0]);

svg.selectAll(".bar")
  .data(data)
  .enter().append("rect")
  .attr("class", "bar")
  .attr("x", d => x(d.mois))
  .attr("y", d => y(d.ventes))
  .attr("width", x.bandwidth())
  .attr("height", d => height - y(d.ventes))
  .attr("fill", "steelblue");

svg.append("g")
  .selectAll(".tick")
  .data(x.domain())
  .enter().append("text")
  .attr("x", d => x(d) + x.bandwidth() / 2)
  .attr("y", height + 10)
  .attr("text-anchor", "middle")
  .text(d => d);

svg.append("g")
  .call(d3.axisLeft(y));

```

**Explication** :
- **x** est une échelle de type `band` pour les mois.
- **y** est une échelle linéaire pour les ventes, avec une plage allant de 0 à la valeur maximale des ventes.
- Chaque barre est dessinée avec des `rect` positionnés sur l'axe x et l'axe y.
- Les mois sont affichés en bas, et l'axe des ventes est tracé à gauche.

---

### **2. Graphique en Ligne : Température Mensuelle**
**Données** :

```json
[
  { "mois": "Janvier", "temperature": 5 },
  { "mois": "Février", "temperature": 7 },
  { "mois": "Mars", "temperature": 10 },
  { "mois": "Avril", "temperature": 15 },
  { "mois": "Mai", "temperature": 20 }
]
```

**Solution** :
Nous allons créer un graphique en ligne pour visualiser la température chaque mois.

```javascript
const data = [
  { "mois": "Janvier", "temperature": 5 },
  { "mois": "Février", "temperature": 7 },
  { "mois": "Mars", "temperature": 10 },
  { "mois": "Avril", "temperature": 15 },
  { "mois": "Mai", "temperature": 20 }
];

const width = 500, height = 300;

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

const x = d3.scaleBand()
  .domain(data.map(d => d.mois))
  .range([0, width])
  .padding(0.1);

const y = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.temperature)])
  .nice()
  .range([height, 0]);

const line = d3.line()
  .x(d => x(d.mois) + x.bandwidth() / 2)
  .y(d => y(d.temperature));

svg.append("path")
  .data([data])
  .attr("class", "line")
  .attr("d", line)
  .attr("fill", "none")
  .attr("stroke", "steelblue")
  .attr("stroke-width", 2);

svg.selectAll(".dot")
  .data(data)
  .enter().append("circle")
  .attr("class", "dot")
  .attr("cx", d => x(d.mois) + x.bandwidth() / 2)
  .attr("cy", d => y(d.temperature))
  .attr("r", 5)
  .attr("fill", "red");

svg.append("g")
  .call(d3.axisLeft(y));

svg.append("g")
  .attr("transform", "translate(0," + height + ")")
  .call(d3.axisBottom(x));
```

**Explication** :
- **x** et **y** sont des échelles définies comme précédemment.
- **line** est la fonction pour tracer la ligne, avec des coordonnées calculées en fonction des échelles.
- Les points de la ligne sont affichés sous forme de cercles (`circle`).
- Les axes sont ajoutés avec `axisLeft` et `axisBottom`.

---

### **3. Graphique à Secteurs (Pie Chart) : Répartition des Ventes par Produit**
**Données** :

```json
[
  { "produit": "Produit A", "ventes": 300 },
  { "produit": "Produit B", "ventes": 400 },
  { "produit": "Produit C", "ventes": 200 },
  { "produit": "Produit D", "ventes": 100 }
]
```

**Solution** :
Un graphique à secteurs peut être créé à l'aide de `d3.pie()` et `d3.arc()`.

```javascript
const data = [
  { "produit": "Produit A", "ventes": 300 },
  { "produit": "Produit B", "ventes": 400 },
  { "produit": "Produit C", "ventes": 200 },
  { "produit": "Produit D", "ventes": 100 }
];

const width = 500, height = 500;
const radius = Math.min(width, height) / 2;

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height)
  .append("g")
  .attr("transform", "translate(" + width / 2 + "," + height / 2 + ")");

const color = d3.scaleOrdinal()
  .domain(data.map(d => d.produit))
  .range(d3.schemeCategory10);

const pie = d3.pie().value(d => d.ventes);
const arc = d3.arc().outerRadius(radius - 10).innerRadius(0);

const arcs = svg.selectAll(".arc")
  .data(pie(data))
  .enter().append("g")
  .attr("class", "arc");

arcs.append("path")
  .attr("d", arc)
  .attr("fill", d => color(d.data.produit));

arcs.append("text")
  .attr("transform", d => "translate(" + arc.centroid(d) + ")")
  .attr("dy", ".35em")
  .text(d => d.data.produit);
```

**Explication** :
- **d3.pie()** crée une série d'angles pour chaque secteur basé sur la proportion des ventes.
- **d3.arc()** génère les chemins pour chaque secteur du graphique.
- Chaque secteur est coloré avec une échelle ordinale.

---

### **4. Graphique à Barres Empilées : Répartition des Ventes par Produit et Mois**
**Données** :

```json
[
  { "mois": "Janvier", "Produit A": 100, "Produit B": 150, "Produit C": 50 },
  { "mois": "Février", "Produit A": 200, "Produit B": 100, "Produit C": 150 }
]
```

**Solution** :
Nous allons créer un graphique à barres empilées où chaque barre est subdivisée par produit.

```javascript
const data = [
  { "mois": "Janvier", "Produit A": 100, "Produit B": 150, "Produit C": 50 },
  { "mois": "Février", "Produit A": 200, "Produit B": 100, "Produit C": 150 }
];

const width = 500, height = 300;
const x0 = d3.scaleBand().domain(data.map(d => d.mois)).range([0, width]).padding(0.1);
const x1 = d3.scaleBand().domain(["Produit A", "Produit B", "Produit C"]).range([0, x0.bandwidth()]).padding(

0.05);
const y = d3.scaleLinear().domain([0, d3.max(data, d => d["Produit A"] + d["Produit B"] + d["Produit C"])]).nice().range([height, 0]);

const color = d3.scaleOrdinal().domain(["Produit A", "Produit B", "Produit C"]).range(["#1f77b4", "#ff7f0e", "#2ca02c"]);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

const bars = svg.selectAll(".bar")
  .data(data)
  .enter().append("g")
  .attr("transform", d => "translate(" + x0(d.mois) + ",0)");

bars.selectAll("rect")
  .data(d => ["Produit A", "Produit B", "Produit C"].map(key => ({ key: key, value: d[key] })))
  .enter().append("rect")
  .attr("x", d => x1(d.key))
  .attr("y", d => y(d.value))
  .attr("width", x1.bandwidth())
  .attr("height", d => height - y(d.value))
  .attr("fill", d => color(d.key));
```

**Explication** :
- Le graphique est basé sur deux échelles x : l'une pour les mois (`x0`), et l'autre pour les produits (`x1`).
- Les barres sont empilées grâce aux valeurs cumulées sur l'axe y.


---

### **5. Graphique de Bulles : Analyse des Ventes en Fonction du Temps et de la Catégorie**
**Données** :

```json
[
  { "mois": "Janvier", "categorie": "A", "ventes": 100, "quantite": 50 },
  { "mois": "Février", "categorie": "B", "ventes": 200, "quantite": 70 },
  { "mois": "Mars", "categorie": "A", "ventes": 300, "quantite": 120 },
  { "mois": "Avril", "categorie": "B", "ventes": 400, "quantite": 150 }
]
```

**Solution** :
Le graphique de bulles permet de visualiser trois variables : le mois, les ventes, et la quantité (en utilisant la taille des bulles).

```javascript
const data = [
  { "mois": "Janvier", "categorie": "A", "ventes": 100, "quantite": 50 },
  { "mois": "Février", "categorie": "B", "ventes": 200, "quantite": 70 },
  { "mois": "Mars", "categorie": "A", "ventes": 300, "quantite": 120 },
  { "mois": "Avril", "categorie": "B", "ventes": 400, "quantite": 150 }
];

const width = 500, height = 300;

const x = d3.scaleBand()
  .domain(data.map(d => d.mois))
  .range([0, width])
  .padding(0.1);

const y = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.ventes)])
  .nice()
  .range([height, 0]);

const size = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.quantite)])
  .range([10, 40]);

const color = d3.scaleOrdinal()
  .domain(["A", "B"])
  .range(["steelblue", "orange"]);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

svg.selectAll(".bubble")
  .data(data)
  .enter().append("circle")
  .attr("class", "bubble")
  .attr("cx", d => x(d.mois) + x.bandwidth() / 2)
  .attr("cy", d => y(d.ventes))
  .attr("r", d => size(d.quantite))
  .attr("fill", d => color(d.categorie))
  .attr("stroke", "black")
  .attr("stroke-width", 1);
```

**Explication** :
- **x** : échelle pour les mois.
- **y** : échelle pour les ventes.
- **size** : échelle pour la taille des bulles (basée sur la quantité).
- **color** : échelle pour les catégories.
- Les bulles sont dessinées avec des cercles dont la position et la taille dépendent des données.

---

### **6. Diagramme de Venn : Chevauchement des Ventes entre Différents Produits**
**Données** :

```json
[
  { "produit": "Produit A", "ventes": 300, "cible": ["Secteur 1", "Secteur 2"] },
  { "produit": "Produit B", "ventes": 400, "cible": ["Secteur 2", "Secteur 3"] },
  { "produit": "Produit C", "ventes": 200, "cible": ["Secteur 1", "Secteur 3"] }
]
```

**Solution** :
Un diagramme de Venn peut être simulé avec des cercles chevauchants pour représenter l'intersection des ventes entre produits.

```javascript
const data = [
  { "produit": "Produit A", "ventes": 300, "cible": ["Secteur 1", "Secteur 2"] },
  { "produit": "Produit B", "ventes": 400, "cible": ["Secteur 2", "Secteur 3"] },
  { "produit": "Produit C", "ventes": 200, "cible": ["Secteur 1", "Secteur 3"] }
];

const width = 500, height = 500;

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

const color = d3.scaleOrdinal()
  .domain(["Produit A", "Produit B", "Produit C"])
  .range(["#1f77b4", "#ff7f0e", "#2ca02c"]);

const circles = [
  { x: 150, y: 150, radius: 100, product: "Produit A" },
  { x: 250, y: 150, radius: 100, product: "Produit B" },
  { x: 200, y: 250, radius: 100, product: "Produit C" }
];

svg.selectAll("circle")
  .data(circles)
  .enter().append("circle")
  .attr("cx", d => d.x)
  .attr("cy", d => d.y)
  .attr("r", d => d.radius)
  .attr("fill", d => color(d.product))
  .attr("fill-opacity", 0.5);

svg.selectAll("text")
  .data(circles)
  .enter().append("text")
  .attr("x", d => d.x)
  .attr("y", d => d.y)
  .attr("dy", ".35em")
  .attr("text-anchor", "middle")
  .text(d => d.product);
```

**Explication** :
- Trois cercles représentant les produits sont créés avec des positions et tailles spécifiques.
- Les cercles se chevauchent pour montrer les intersections, et des textes sont ajoutés pour identifier chaque produit.

---

### **7. Graphique à Lignes Multiples : Comparaison des Températures de Différentes Villes**
**Données** :

```json
[
  { "mois": "Janvier", "Paris": 5, "Lyon": 7, "Marseille": 10 },
  { "mois": "Février", "Paris": 6, "Lyon": 8, "Marseille": 12 },
  { "mois": "Mars", "Paris": 10, "Lyon": 12, "Marseille": 15 },
  { "mois": "Avril", "Paris": 14, "Lyon": 16, "Marseille": 18 }
]
```

**Solution** :
Un graphique à lignes multiples pour comparer les températures de différentes villes au cours des mois.

```javascript
const data = [
  { "mois": "Janvier", "Paris": 5, "Lyon": 7, "Marseille": 10 },
  { "mois": "Février", "Paris": 6, "Lyon": 8, "Marseille": 12 },
  { "mois": "Mars", "Paris": 10, "Lyon": 12, "Marseille": 15 },
  { "mois": "Avril", "Paris": 14, "Lyon": 16, "Marseille": 18 }
];

const width = 500, height = 300;

const x = d3.scaleBand()
  .domain(data.map(d => d.mois))
  .range([0, width])
  .padding(0.1);

const y = d3.scaleLinear()
  .domain([0, d3.max(data, d => Math.max(d.Paris, d.Lyon, d.Marseille))])
  .nice()
  .range([height, 0]);

const line = d3.line()
  .x(d => x(d.mois) + x.bandwidth() / 2)
  .y(d => y(d.value));

const cities = ["Paris", "Lyon", "Marseille"];

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

cities.forEach(city => {
  svg.append("path")
    .data([data.map(d => ({ mois: d.mois, value: d[city] }))])
    .attr("class", city)
    .attr("d", line)
    .attr("fill", "none")
    .attr("stroke", city === "Paris" ? "blue" : city === "Lyon" ? "green" : "red")
    .attr("stroke-width", 2);
});
```

**Explication** :
- Chaque ligne est tracée pour chaque ville avec des données mensuelles.
- Les lignes sont colorées différemment pour chaque ville afin de faciliter la comparaison.

---

### **8. Graphique en Radar : Comparaison des Performances de Divers Produits**
**Données** :

```json
[
  { "produit": "Produit A", "qualite": 4, "prix": 3, "popularite": 5, "disponibilite": 4 },
  { "produit": "Produit B", "qualite": 3, "prix": 4, "popularite": 4, "disponibilite": 3 },
  { "produit": "Produit C", "qualite": 5, "prix": 2, "popularite": 3, "disponibilite": 5 }
]
```

**Solution** :
Le graphique radar est utilisé pour comparer les performances des produits sur différents critères.

```javascript
const data = [
  { "produit": "Produit A", "qualite": 4, "prix": 3, "popularite": 5, "disponibilite": 4 },
  { "produit": "Produit B", "qualite": 3, "prix": 4, "popularite": 4, "disponibilite": 3 },
  { "produit": "Produit C", "qualite": 5, "prix": 2, "popularite": 3, "disponibilite": 5 }
];

const width = 400, height = 400;
const radius = Math.min(width, height) / 2;
const angleSlice = Math.PI * 2 / 4; // 4 axes

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height)
  .append("g")
  .attr("transform", "translate(" + width / 2 + "," + height / 2 + ")");

const scales = {
  "qualite": d3.scaleLinear().domain([0, 5]).range([0, radius]),
  "prix": d3.scaleLinear().domain([0, 5]).range([0, radius]),
  "popularite": d3.scaleLinear().domain([0, 5]).range([0, radius]),
  "disponibilite": d3.scaleLinear().domain([0, 5]).range([0, radius])
};

const categories = ["qualite", "prix", "popularite", "disponibilite"];

const line = d3.lineRadial()
  .radius(d => scales[d[0]](d[1]))
  .angle((d, i) => i * angleSlice);

const color = d3.scaleOrdinal()
  .domain(["Produit A", "Produit B", "Produit C"])
  .range(["blue", "green", "red"]);

data.forEach(d => {
  const points = categories.map((cat, i) => [cat, d[cat]]);
  svg.append("path")
    .datum(points)
    .attr("d", line)
    .attr("fill", color(d.produit))
    .attr("fill-opacity", 0.3)
    .attr("stroke", color(d.produit))
    .attr("stroke-width", 2);
});
```

**Explication** :
- **scale** : Échelles pour chaque critère (qualité, prix, popularité, disponibilité).
- **lineRadial** : Fonction qui génère un chemin radial pour chaque produit.
- **color** : Attribue des couleurs aux produits pour les distinguer.

---

### **9. Histogramme Empilé : Comparaison des Ventes par Région**
**Données** :

```json
[
  { "mois": "Janvier", "Nord": 100, "Sud": 200, "Est": 150 },
  { "mois": "Février", "Nord": 120, "Sud": 220, "Est": 180 },
  { "mois": "Mars", "Nord": 130, "Sud": 250, "Est": 200 }
]
```

**Solution** :
Un histogramme empilé est utilisé pour comparer les ventes par région sur plusieurs mois.

```javascript
const data = [
  { "mois": "Janvier", "Nord": 100, "Sud": 200, "Est": 150 },
  { "mois": "Février", "Nord": 120, "Sud": 220, "Est": 180 },
  { "mois": "Mars", "Nord": 130, "Sud": 250, "Est": 200 }
];

const width = 500, height = 300;

const x = d3.scaleBand()
  .domain(data.map(d => d.mois))
  .range([0, width])
  .padding(0.1);

const y = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.Nord + d.Sud + d.Est)])
  .nice()
  .range([height, 0]);

const color = d3.scaleOrdinal()
  .domain(["Nord", "Sud", "Est"])
  .range(["blue", "green", "red"]);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

const stack = d3.stack().keys(["Nord", "Sud", "Est"]);

const series = stack(data);

svg.selectAll(".layer")
  .data(series)
  .enter().append("g")
  .attr("class", "layer")
  .attr("fill", (d, i) => color(d.key))
  .selectAll("rect")
  .data(d => d)
  .enter().append("rect")
  .attr("x", d => x(d.data.mois))
  .attr("y", d => y(d[1]))
  .attr("height", d => y(d[0]) - y(d[1]))
  .attr("width", x.bandwidth());
```

**Explication** :
- **stack** : Utilisation de `d3.stack()` pour empiler les valeurs des régions.
- **color** : Chaque région est colorée différemment pour la distinction.

---

### **10. Carte Choroplèthe : Visualisation des Ventes par Région Géographique**
**Données** :

```json
[
  { "region": "Nord", "ventes": 500 },
  { "region": "Sud", "ventes": 700 },
  { "region": "Est", "ventes": 300 },
  { "region": "Ouest", "ventes": 450 }
]
```

**Solution** :
Un graphique de carte choroplèthe pour visualiser les ventes par région géographique. Pour simplifier, supposons que les données géographiques soient disponibles sous forme de coordonnées et que la carte soit une simple division.

```javascript
const data = [
  { "region": "Nord", "ventes": 500 },
  { "region": "Sud", "ventes": 700 },
  { "region": "Est", "ventes": 300 },
  { "region": "Ouest", "ventes": 450 }
];

const width = 500, height = 300;

const color = d3.scaleQuantize()
  .domain([0, d3.max(data, d => d.ventes)])
  .range(["#f7fbff", "#9ecae1", "#3182bd"]);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

const regions = {
  "Nord": { x: 50, y: 50, width: 100, height: 100 },
  "Sud": { x: 150, y: 50, width: 100, height: 100 },
  "Est": { x: 250, y: 50, width: 100, height: 100 },
  "Ouest": { x: 350, y: 50, width: 100, height: 100 }
};

svg.selectAll("rect")
  .data(data)
  .enter().append("rect")
  .attr("x", d => regions[d.region].x)
  .attr("y", d => regions[d.region].y)
  .attr("width", d => regions[d.region].width)
  .attr("height", d => regions[d.region].height)
  .attr("fill", d => color(d.ventes));
```

**Explication** :
- La carte est simplifiée avec des rectangles représentant chaque région.
- La couleur des régions dépend des ventes, et chaque région est coloriée selon un schéma de couleurs graduées.

---

### **11. Graphique en Nuage de Points : Corrélation entre Revenu et Éducation**
**Données** :

```json
[
  { "revenu": 25000, "education": 12 },
  { "revenu": 35000, "education": 16 },
  { "revenu": 50000, "education": 18 },
  { "revenu": 45000, "education": 14 },
  { "revenu": 60000, "education": 20 }
]
```

**Solution** :
Un graphique de nuage de points (scatter plot) est utilisé pour visualiser la corrélation entre le revenu et le niveau d'éducation.

```javascript
const data = [
  { "revenu": 25000, "education": 12 },
  { "revenu": 35000, "education": 16 },
  { "revenu": 50000, "education": 18 },
  { "revenu": 45000, "education": 14 },
  { "revenu": 60000, "education": 20 }
];

const width = 500, height = 300;

const x = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.education)])
  .range([0, width]);

const y = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.revenu)])
  .range([height, 0]);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

svg.selectAll("circle")
  .data(data)
  .enter().append("circle")
  .attr("cx", d => x(d.education))
  .attr("cy", d => y(d.revenu))
  .attr("r", 5)
  .attr("fill", "blue");
```

**Explication** :
- **scaleLinear** : Utilisation d'échelles linéaires pour les axes x et y.
- Chaque point est représenté par un cercle avec une position déterminée par les valeurs de revenu et d'éducation.

---

### **12. Graphique de Barres Horizontales : Classement des Ventes par Produits**
**Données** :

```json
[
  { "produit": "Produit A", "ventes": 500 },
  { "produit": "Produit B", "ventes": 750 },
  { "produit": "Produit C", "ventes": 300 }
]
```

**Solution** :
Un graphique de barres horizontales est utilisé pour classer les produits en fonction des ventes.

```javascript
const data = [
  { "produit": "Produit A", "ventes": 500 },
  { "produit": "Produit B", "ventes": 750 },
  { "produit": "Produit C", "ventes": 300 }
];

const width = 500, height = 300;

const x = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.ventes)])
  .range([0, width]);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

svg.selectAll("rect")
  .data(data)
  .enter().append("rect")
  .attr("x", 0)
  .attr("y", (d, i) => i * 40)
  .attr("width", d => x(d.ventes))
  .attr("height", 30)
  .attr("fill", "green");

svg.selectAll("text")
  .data(data)
  .enter().append("text")
  .attr("x", d => x(d.ventes) + 10)
  .attr("y", (d, i) => i * 40 + 20)
  .text(d => d.produit)
  .attr("fill", "black");
```

**Explication** :
- Chaque barre est horizontale et représente le nombre de ventes d'un produit.
- Les valeurs sont affichées à droite des barres.

---

### **13. Graphique de Séries Temporelles : Visualisation des Ventes Mensuelles**
**Données** :

```json
[
  { "mois": "Jan", "ventes": 100 },
  { "mois": "Feb", "ventes": 200 },
  { "mois": "Mar", "ventes": 150 },
  { "mois": "Apr", "ventes": 250 }
]
```

**Solution** :
Un graphique de séries temporelles pour visualiser les ventes au cours de plusieurs mois.

```javascript
const data = [
  { "mois": "Jan", "ventes": 100 },
  { "mois": "Feb", "ventes": 200 },
  { "mois": "Mar", "ventes": 150 },
  { "mois": "Apr", "ventes": 250 }
];

const width = 500, height = 300;

const x = d3.scaleBand()
  .domain(data.map(d => d.mois))
  .range([0, width])
  .padding(0.1);

const y = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.ventes)])
  .range([height, 0]);

const line = d3.line()
  .x(d => x(d.mois) + x.bandwidth() / 2)
  .y(d => y(d.ventes));

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

svg.append("path")
  .data([data])
  .attr("d", line)
  .attr("fill", "none")
  .attr("stroke", "blue")
  .attr("stroke-width", 2);
```

**Explication** :
- Utilisation de `d3.line` pour créer une courbe de tendance des ventes sur la période donnée.
- Les points sont reliés et affichés avec une ligne bleue.

---

### **14. Heatmap : Visualisation de la Température dans une Ville**
**Données** :

```json
[
  { "jour": "Lundi", "heure": 6, "temperature": 15 },
  { "jour": "Lundi", "heure": 12, "temperature": 25 },
  { "jour": "Lundi", "heure": 18, "temperature": 20 },
  { "jour": "Mardi", "heure": 6, "temperature": 16 },
  { "jour": "Mardi", "heure": 12, "temperature": 26 },
  { "jour": "Mardi", "heure": 18, "temperature": 21 }
]
```

**Solution** :
Une heatmap pour visualiser la température tout au long de la journée, pour différents jours.

```javascript
const data = [
  { "jour": "Lundi", "heure": 6, "temperature": 15 },
  { "jour": "Lundi", "heure": 12, "temperature": 25 },
  { "jour": "Lundi", "heure": 18, "temperature": 20 },
  { "jour": "Mardi", "heure": 6, "temperature": 16 },
  { "jour": "Mardi", "heure": 12, "temperature": 26 },
  { "jour": "Mardi", "heure": 18, "temperature": 21 }
];

const width = 500, height = 300;

const x = d3.scaleBand()
  .domain(data.map(d => d.heure))
  .range([0, width]);

const y = d3.scaleBand()
  .domain(data.map(d => d.jour))
  .range([0, height]);

const color = d3.scaleSequential(d3.interpolateBlues)
  .domain([0, d3.max(data, d => d.temperature)]);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

svg.selectAll("rect")
  .data(data)
  .enter().append("rect")
  .attr("x", d => x(d.heure))
  .attr("y", d => y(d.jour))
  .attr("width", x.bandwidth())
  .attr("height", y.bandwidth())
  .attr("fill", d => color(d.temperature));
```

**Explication** :
- **scaleBand** : Utilisation d'échelles pour positionner les éléments (heure et jour).
- **color** : La couleur de chaque cellule est déterminée par la température, avec un dégradé de bleu.

---


### **15. Graphique en secteurs : Répartition des Parts de Marché**
**Données** :

```json
[
  { "secteur": "Automobile", "part": 40 },
  { "secteur": "Technologie", "part": 30 },
  { "secteur": "Santé", "part": 20 },
  { "secteur": "Énergie", "part": 10 }
]
```

**Solution** :
Un graphique en secteurs (pie chart) pour visualiser la répartition des parts de marché par secteur.

```javascript
const data = [
  { "secteur": "Automobile", "part": 40 },
  { "secteur": "Technologie", "part": 30 },
  { "secteur": "Santé", "part": 20 },
  { "secteur": "Énergie", "part": 10 }
];

const width = 500, height = 500;
const radius = Math.min(width, height) / 2;

const color = d3.scaleOrdinal(d3.schemeCategory10);

const pie = d3.pie().value(d => d.part);
const arc = d3.arc().innerRadius(0).outerRadius(radius);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height)
  .append("g")
  .attr("transform", `translate(${width / 2}, ${height / 2})`);

const arcs = svg.selectAll(".arc")
  .data(pie(data))
  .enter().append("g")
  .attr("class", "arc");

arcs.append("path")
  .attr("d", arc)
  .attr("fill", d => color(d.data.secteur));

arcs.append("text")
  .attr("transform", d => `translate(${arc.centroid(d)})`)
  .attr("dy", ".35em")
  .text(d => d.data.secteur);
```

**Explication** :
- Utilisation de **d3.pie** pour diviser les données en tranches de secteurs et **d3.arc** pour générer les chemins de chaque secteur.
- Les couleurs des secteurs sont générées avec **d3.scaleOrdinal**.

---

### **16. Graphique en Radar : Comparaison des Performances de Différents Produits**
**Données** :

```json
[
  { "produit": "Produit A", "qualité": 7, "prix": 8, "service": 6 },
  { "produit": "Produit B", "qualité": 6, "prix": 9, "service": 7 },
  { "produit": "Produit C", "qualité": 8, "prix": 7, "service": 8 }
]
```

**Solution** :
Un graphique en radar pour comparer les performances des produits en termes de qualité, prix et service.

```javascript
const data = [
  { "produit": "Produit A", "qualité": 7, "prix": 8, "service": 6 },
  { "produit": "Produit B", "qualité": 6, "prix": 9, "service": 7 },
  { "produit": "Produit C", "qualité": 8, "prix": 7, "service": 8 }
];

const width = 500, height = 500, radius = 200;
const angles = ["qualité", "prix", "service"];

const color = d3.scaleOrdinal(d3.schemeCategory10);

const radialScale = d3.scaleLinear()
  .domain([0, 10])
  .range([0, radius]);

const line = d3.lineRadial()
  .radius(d => radialScale(d.value))
  .angle((d, i) => (i / angles.length) * 2 * Math.PI);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height)
  .append("g")
  .attr("transform", `translate(${width / 2}, ${height / 2})`);

svg.selectAll("path")
  .data(data)
  .enter().append("path")
  .attr("d", d => line(angles.map(a => ({ name: a, value: d[a] }))))
  .attr("fill", (d, i) => color(i))
  .attr("stroke", "black")
  .attr("stroke-width", 2);

svg.selectAll("text")
  .data(angles)
  .enter().append("text")
  .attr("x", (d, i) => radialScale(10) * Math.cos(i * 2 * Math.PI / angles.length))
  .attr("y", (d, i) => radialScale(10) * Math.sin(i * 2 * Math.PI / angles.length))
  .text(d => d)
  .attr("text-anchor", "middle");
```

**Explication** :
- Utilisation de **d3.lineRadial** pour dessiner les lignes radiales représentant les scores dans chaque catégorie (qualité, prix, service).
- Chaque produit est une ligne dans le graphique avec une couleur distincte.

---

### **17. Graphique en Diagramme de Gantt : Planification d'un Projet**
**Données** :

```json
[
  { "tâche": "Conception", "début": "2025-01-01", "fin": "2025-01-10" },
  { "tâche": "Développement", "début": "2025-01-11", "fin": "2025-02-20" },
  { "tâche": "Tests", "début": "2025-02-21", "fin": "2025-03-10" }
]
```

**Solution** :
Un graphique de Gantt pour visualiser les différentes phases du projet avec leurs dates de début et de fin.

```javascript
const data = [
  { "tâche": "Conception", "début": "2025-01-01", "fin": "2025-01-10" },
  { "tâche": "Développement", "début": "2025-01-11", "fin": "2025-02-20" },
  { "tâche": "Tests", "début": "2025-02-21", "fin": "2025-03-10" }
];

const width = 600, height = 200;
const parseDate = d3.timeParse("%Y-%m-%d");

const x = d3.scaleTime()
  .domain([parseDate("2025-01-01"), parseDate("2025-03-10")])
  .range([0, width]);

const y = d3.scaleBand()
  .domain(data.map(d => d.tâche))
  .range([0, height])
  .padding(0.1);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

svg.selectAll("rect")
  .data(data)
  .enter().append("rect")
  .attr("x", d => x(parseDate(d.début)))
  .attr("y", d => y(d.tâche))
  .attr("width", d => x(parseDate(d.fin)) - x(parseDate(d.début)))
  .attr("height", y.bandwidth())
  .attr("fill", "steelblue");

svg.selectAll("text")
  .data(data)
  .enter().append("text")
  .attr("x", d => x(parseDate(d.début)) + 5)
  .attr("y", d => y(d.tâche) + y.bandwidth() / 2)
  .attr("dy", ".35em")
  .text(d => d.tâche)
  .attr("fill", "white");
```

**Explication** :
- Utilisation de **d3.scaleTime** pour l'échelle du temps et **d3.scaleBand** pour l'échelle des tâches.
- Les barres du graphique représentent la durée de chaque tâche, et le texte montre le nom de la tâche.

---

### **18. Graphique en Boxplot : Analyse des Scores d'Étudiants**
**Données** :

```json
[
  { "score": 55 },
  { "score": 78 },
  { "score": 62 },
  { "score": 85 },
  { "score": 90 },
  { "score": 60 },
  { "score": 72 },
  { "score": 88 }
]
```

**Solution** :
Un graphique en boxplot pour analyser la distribution des scores des étudiants.

```javascript
const data = [
  { "score": 55 },
  { "score": 78 },
  { "score": 62 },
  { "score": 85 },
  { "score": 90 },
  { "score": 60 },
  { "score": 72 },
  { "score": 88 }
];

const width = 500, height = 300;

const x = d3.scaleBand().domain([0]).range([0, width]);

const y = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.score)])
  .range([height, 0]);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("

height", height);

const scores = data.map(d => d.score);
const q1 = d3.quantile(scores.sort(d3.ascending), 0.25);
const median = d3.quantile(scores.sort(d3.ascending), 0.5);
const q3 = d3.quantile(scores.sort(d3.ascending), 0.75);
const interQuantileRange = q3 - q1;
const min = d3.min(scores);
const max = d3.max(scores);

svg.append("line")
  .attr("x1", x(0))
  .attr("x2", x(0))
  .attr("y1", y(min))
  .attr("y2", y(max))
  .attr("stroke", "black");

svg.append("rect")
  .attr("x", x(0) - 20)
  .attr("y", y(q3))
  .attr("width", 40)
  .attr("height", y(q1) - y(q3))
  .attr("fill", "steelblue");

svg.append("line")
  .attr("x1", x(0) - 20)
  .attr("x2", x(0) + 20)
  .attr("y1", y(median))
  .attr("y2", y(median))
  .attr("stroke", "black");

svg.selectAll("circle")
  .data([min, max])
  .enter().append("circle")
  .attr("cx", x(0))
  .attr("cy", d => y(d))
  .attr("r", 5)
  .attr("fill", "black");
```

**Explication** :
- Les éléments du **boxplot** (boîte, lignes et cercles) sont dessinés pour visualiser la distribution des scores.


---

### **19. Graphique en Heatmap : Visualisation des Corrélations entre Variables**
**Données** :
```json
[
  { "variable1": 0.1, "variable2": 0.8, "variable3": 0.5 },
  { "variable1": 0.3, "variable2": 0.4, "variable3": 0.7 },
  { "variable1": 0.7, "variable2": 0.6, "variable3": 0.3 },
  { "variable1": 0.9, "variable2": 0.2, "variable3": 0.1 }
]
```

**Solution** :
Un graphique de type **heatmap** pour visualiser les corrélations entre plusieurs variables.

```javascript
const data = [
  { "variable1": 0.1, "variable2": 0.8, "variable3": 0.5 },
  { "variable1": 0.3, "variable2": 0.4, "variable3": 0.7 },
  { "variable1": 0.7, "variable2": 0.6, "variable3": 0.3 },
  { "variable1": 0.9, "variable2": 0.2, "variable3": 0.1 }
];

const width = 400, height = 200;
const x = d3.scaleBand().domain(["variable1", "variable2", "variable3"]).range([0, width]);
const y = d3.scaleBand().domain([0, 1, 2, 3]).range([0, height]);

const color = d3.scaleSequential(d3.interpolateYlOrRd).domain([0, 1]);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height);

svg.selectAll("rect")
  .data(data)
  .enter().append("rect")
  .attr("x", (d, i) => x(`variable${i+1}`))
  .attr("y", (d, i) => y(i))
  .attr("width", x.bandwidth())
  .attr("height", y.bandwidth())
  .attr("fill", d => color(d.variable1));
```

**Explication** :
- Utilisation de **d3.scaleBand** pour positionner les variables sur l'axe X et les lignes sur l'axe Y.
- Le **d3.scaleSequential** est utilisé pour la coloration des cellules en fonction des valeurs.

---

### **20. Graphique en Chord Diagram : Visualisation des Flux de Données**
**Données** :
```json
{
  "nodes": [
    { "name": "A" },
    { "name": "B" },
    { "name": "C" },
    { "name": "D" }
  ],
  "links": [
    { "source": 0, "target": 1, "value": 10 },
    { "source": 1, "target": 2, "value": 20 },
    { "source": 2, "target": 3, "value": 30 },
    { "source": 3, "target": 0, "value": 40 }
  ]
}
```

**Solution** :
Un graphique en **Chord Diagram** pour visualiser les flux entre les différentes entités.

```javascript
const data = {
  "nodes": [
    { "name": "A" },
    { "name": "B" },
    { "name": "C" },
    { "name": "D" }
  ],
  "links": [
    { "source": 0, "target": 1, "value": 10 },
    { "source": 1, "target": 2, "value": 20 },
    { "source": 2, "target": 3, "value": 30 },
    { "source": 3, "target": 0, "value": 40 }
  ]
};

const width = 500, height = 500;
const innerRadius = 150, outerRadius = 200;

const color = d3.scaleOrdinal(d3.schemeCategory10);

const chord = d3.chord().padAngle(0.05).sortSubgroups(d3.descending);
const arc = d3.arc().innerRadius(innerRadius).outerRadius(outerRadius);
const ribbon = d3.ribbon().radius(innerRadius);

const svg = d3.select("body").append("svg")
  .attr("width", width)
  .attr("height", height)
  .append("g")
  .attr("transform", `translate(${width / 2}, ${height / 2})`);

const chords = chord(data.links);

svg.selectAll(".group")
  .data(chords.groups)
  .enter().append("g")
  .attr("class", "group")
  .append("path")
  .attr("d", arc)
  .style("fill", (d, i) => color(i));

svg.selectAll(".ribbon")
  .data(chords)
  .enter().append("path")
  .attr("d", ribbon)
  .style("fill", d => color(d.source.index))
  .style("stroke", d => color(d.source.index));

svg.selectAll(".group")
  .append("text")
  .attr("transform", d => `rotate(${(d.startAngle + d.endAngle) / 2 * 180 / Math.PI}) translate(0, ${innerRadius + 10})`)
  .attr("text-anchor", "middle")
  .text(d => data.nodes[d.index].name);
```

**Explication** :
- **d3.chord** est utilisé pour transformer les données de liens en un format adapté à la création du diagramme de cordes.
- **d3.arc** pour créer les arcs représentant chaque groupe.
- **d3.ribbon** pour dessiner les liens entre les groupes.

---

### Conclusion
Ce sont les solutions aux 20 exercices pratiques sur D3.js. Chaque exercice permet d'explorer un aspect différent de la création graphique avec D3.js, de l'utilisation de graphiques simples (barres, lignes, etc.) à des visualisations avancées comme les diagrammes de cordes ou les heatmaps.

Chaque solution est suivie d'une explication détaillée pour vous aider à comprendre comment aborder chaque problème et appliquer les concepts et techniques fondamentaux de D3.js.