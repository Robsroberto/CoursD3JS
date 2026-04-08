---
marp: false
size: 4:3
style: |
  h2, h3, p {
    font-size: 20px;
  }
  li {
    font-size:20px
  }
headingDivider: 1
header: 
paginate: true
# footer: Licence 2 Informatique &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ISI (Institut Supérieur D'Informatique) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RD
---
<img src="../isi.png" alt="ISI" width="100px">

---
# Chapitre 2 : Introduction à D3.js
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 

<img src="d3js.jpeg" alt="D3JS" width="100px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   **Par Robert DIASSÉ**  


---


#### **2.1 Qu'est-ce que D3.js ?**

D3.js, ou Data-Driven Documents, est une bibliothèque JavaScript puissante conçue pour créer des visualisations de données interactives et dynamiques sur le web. Elle permet de lier des données à un Document Object Model (DOM) et d'utiliser des standards web tels que HTML, SVG (Scalable Vector Graphics) et CSS pour manipuler ces données visuellement.

##### **Caractéristiques Clés de D3.js :**
- **Manipulation du DOM** : D3.js permet de créer, supprimer et modifier des éléments du DOM en fonction des données, rendant les visualisations réactives aux changements de données.
- **Liens de données** : Grâce à D3.js, vous pouvez lier des données à des éléments DOM, ce qui permet d'afficher des informations de manière dynamique.
- **Flexibilité** : D3.js est très flexible et permet de créer une variété de visualisations, allant des graphiques simples aux visualisations complexes et interactives.

#### **2.2 Pourquoi Utiliser D3.js ?**

D3.js se distingue des autres bibliothèques de visualisation par sa capacité à manipuler directement le DOM et à offrir un contrôle total sur l'apparence et le comportement des visualisations. Voici quelques raisons d'utiliser D3.js :

- **Personnalisation** : Vous pouvez personnaliser chaque aspect de la visualisation, y compris les couleurs, les animations et les interactions.
- **Interopérabilité** : D3.js fonctionne bien avec d'autres bibliothèques et frameworks JavaScript, permettant une intégration facile dans des applications web existantes.
- **Grande Communauté et Écosystème** : D3.js bénéficie d'une large communauté de développeurs et d'un écosystème riche de plugins et d'exemples, facilitant l'apprentissage et le développement.

#### Quelques fonctionnalités clés de D3.js3:

- **Sélections et transitions** : Créez, mettez à jour et animez le DOM en fonction des données sans la surcharge d’un DOM virtuel.
- **Échelles et axes** : Encodez les données abstraites en valeurs visuelles telles que la position, la taille et la couleur.
- **Formes** : Rendez des arcs, des zones, des courbes, des lignes, des liens, des diagrammes circulaires, des piles, des symboles, et plus encore.
- **Interactions** : Facilitez l’exploration avec des comportements interactifs réutilisables, y compris le panoramique, le zoom, le brossage et le glisser-déposer.
- **Mises en page** : Treemaps, arbres, graphes dirigés par la force, Voronoi, contours, accords, empaquetage circulaire, etc.
- **Cartes géographiques** : Projections sphériques avec des aspects arbitraires, échantillonnage adaptatif et découpage flexible.

#### **2.3 Installation de D3.js**
##### Pré-requis
Avant d'installer D3.js, assurez-vous d'avoir :
- Un éditeur de code (comme Visual Studio Code).
- Un navigateur web (comme Google Chrome).
Pour commencer à utiliser D3.js, vous devez d'abord l'installer dans votre projet. Voici les étapes pour l'installation :

1. **Inclusion via CDN** :
   Vous pouvez inclure D3.js directement depuis un Content Delivery Network (CDN) en ajoutant la ligne suivante dans la section `<head>` de votre fichier HTML :
   ```html
   <script src="https://d3js.org/d3.v7.min.js"></script>
   ```

2. **Installation via npm** :
   Si vous utilisez un gestionnaire de paquets comme npm, vous pouvez installer D3.js en exécutant la commande suivante dans votre terminal :
   ```bash
   npm install d3
   ```
### Étape 1 : Créer un fichier HTML de base

Pour utiliser D3.js, commencez par créer un fichier HTML. Voici un exemple minimaliste :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon Projet D3.js</title>
    <script src="https://d3js.org/d3.v7.min.js"></script>
     <style>
        /* Styles CSS ici */
    </style>
</head>
<body>
    <h1>Bienvenue dans D3.js</h1>
    <script>
        // Votre code D3.js ira ici
    </script>
</body>
</html>
```

- **Explication** :
  - `<!DOCTYPE html>` : Indique que le document est un document HTML5.
  - `<meta charset="UTF-8">` : Définit l'encodage de caractères utilisé dans le document.
  - `<script src="https://d3js.org/d3.v7.min.js"></script>` : Inclut la bibliothèque D3.js via un lien CDN.

### Étape 2 : Structure de Base d'un Projet D3.js

Une fois que vous avez créé votre fichier HTML, vous pouvez commencer à y écrire du code D3.js. Voici un exemple qui montre comment utiliser D3.js pour créer un simple élément SVG :

```javascript
// Sélectionner le corps du document et y ajouter un élément SVG
const svg = d3.select("body").append("svg")
    .attr("width", 500)
    .attr("height", 300);

// Ajouter un cercle au SVG
svg.append("circle")
    .attr("cx", 250) // Coordonnée x du centre
    .attr("cy", 150) // Coordonnée y du centre
    .attr("r", 50)   // Rayon du cercle
    .style("fill", "blue"); // Couleur de remplissage
```

- **Explication** :
  - `d3.select("body")` : Sélectionne l'élément `<body>` du document.
  - `.append("svg")` : Ajoute un élément `<svg>` à l'intérieur du `<body>`.
  - `.attr("width", 500)` et `.attr("height", 300)` : Définit la largeur et la hauteur de l'élément SVG.
  - `.append("circle")` : Ajoute un élément `<circle>` à l'intérieur de l'élément SVG.
  - `.attr("cx", 250)` et `.attr("cy", 150)` : Définit la position du centre du cercle.
  - `.attr("r", 50)` : Définit le rayon du cercle.
  - `.style("fill", "blue")` : Applique une couleur de remplissage bleue au cercle.

#### **2.4 Base d'une Visualisation avec D3.js**

Une visualisation D3.js typique suit une structure de base. Voici un exemple simple pour illustrer cela :

1. **Chargement des Données** :
   Les données peuvent être chargées à partir de fichiers CSV, JSON ou d'autres sources. Par exemple :
   ```javascript
   d3.csv("data.csv").then(function(data) {
       console.log(data);
   });
   ```

2. **Création d'un SVG** :
   Un conteneur SVG est créé pour contenir la visualisation :
   ```javascript
   const svg = d3.select("body")
                 .append("svg")
                 .attr("width", 500)
                 .attr("height", 300);
   ```

3. **Ajout d'Éléments** :
   Les éléments graphiques (comme des cercles, des rectangles, etc.) peuvent être ajoutés au SVG en fonction des données :
   ```javascript
   svg.selectAll("circle")
      .data(data)
      .enter()
      .append("circle")
      .attr("cx", function(d) { return d.value * 10; }) // Exemple de transformation
      .attr("cy", 150)
      .attr("r", 10);
   ```

### **Conclusion**

D3.js est une bibliothèque essentielle pour quiconque souhaite créer des visualisations de données dynamiques et interactives sur le web. Sa flexibilité et son contrôle sur le DOM en font un outil puissant pour représenter visuellement des informations complexes. Dans les chapitres suivants, nous allons explorer en détail les différentes fonctionnalités de D3.js et comment les utiliser pour créer des visualisations impressionnantes.

---

## Ressources Complémentaires

Pour approfondir vos connaissances sur D3.js, voici quelques ressources utiles :

- [Documentation officielle de D3.js](https://d3js.org/)
- [Tutoriels sur freeCodeCamp](https://www.freecodecamp.org/)

---


<!-- 
### 2.4.1 Création d'un Repère
Avant de créer des visualisations, il est important de créer un repère (système de coordonnées) pour vos graphiques.

#### Étape 1 : Créer un élément SVG
L'élément SVG (Scalable Vector Graphics) est utilisé pour dessiner des graphiques.

```javascript
const svg = d3.select('body').append('svg')
    .attr('width', 500)    // Largeur de l'élément SVG
    .attr('height', 300);  // Hauteur de l'élément SVG
```
#### Explication
- `d3.select('body').append('svg')` : Crée un nouvel élément `<svg>` à l'intérieur du `<body>`.
- `.attr('width', 500)` et `.attr('height', 300)` : Définit la taille de l'élément SVG.

#### Étape 2 : Ajouter des Axes
Pour une visualisation, il est souvent utile d'ajouter des axes pour donner un contexte.

```javascript
svg.append('line') // Axe X
    .attr('x1', 0)
    .attr('y1', 250)
    .attr('x2', 500)
    .attr('y2', 250)
    .attr('stroke', 'black');

svg.append('line') // Axe Y
    .attr('x1', 0)
    .attr('y1', 0)
    .attr('x2', 0)
    .attr('y2', 250)
    .attr('stroke', 'black');
```
#### Explication
- `svg.append('line')` : Crée une ligne pour l'axe.
- `.attr('x1', ...)`, `.attr('y1', ...)`, `.attr('x2', ...)`, `.attr('y2', ...)` : Définit les coordonnées des extrémités de la ligne.
- `.attr('stroke', 'black')` : Définit la couleur de la ligne.

### 2.4.2 Gestion des Données
D3.js permet de manipuler des données de manière efficace. Les données peuvent être sous forme de tableaux ou d'objets.

#### Exemple de données
```javascript
const data = [
    { product: 'A', sales: 120 },
    { product: 'B', sales: 80 },
    { product: 'C', sales: 150 },
    { product: 'D', sales: 90 }
];
```
#### Structure des Objets
Chaque objet a des propriétés (ici, `product` et `sales`) qui peuvent être utilisées pour créer des visualisations.

### 2.4.3 Liaison de Données
La liaison de données est un concept central de D3.js. Vous pouvez lier un tableau de données à des éléments DOM pour créer des visualisations dynamiques.

```javascript
const bars = svg.selectAll('rect')
    .data(data)            // Lie les données aux éléments <rect>
    .enter()               // Gère les éléments entrants
    .append('rect')        // Ajoute un nouvel élément <rect> pour chaque donnée
    .attr('width', 40)     // Largeur des barres
    .attr('height', d => d.sales) // Hauteur selon les ventes
    .attr('x', (d, i) => i * 45) // Position x des barres
    .attr('y', d => 250 - d.sales) // Position y inversée
    .attr('fill', 'steelblue'); // Couleur de remplissage
```
#### Explication du Code
- `svg.selectAll('rect')` : Sélectionne tous les éléments `<rect>` existants.
- `.data(data)` : Lie le tableau `data` aux éléments sélectionnés.
- `.enter()` : Crée une sélection pour les nouvelles données qui n'ont pas encore d'éléments DOM associés.
- `.append('rect')` : Ajoute un rectangle pour chaque élément de données.
- `.attr('width', 40)` : Définit la largeur fixe des barres.
- `.attr('height', d => d.sales)` : Définit la hauteur de chaque barre en fonction des ventes.
- `.attr('x', (d, i) => i * 45)` : Positionne chaque barre le long de l'axe x.
- `.attr('y', d => 250 - d.sales)` : Inverse l'axe y pour ajuster la hauteur des barres.

### 2.4.4 Transitions
Les transitions ajoutent une dynamique aux visualisations.

```javascript
bars.transition()            // Démarre une transition sur les barres
    .duration(1000)         // Durée de la transition en millisecondes
    .attr('height', d => d.sales * 1.5); // Modifie la hauteur
```
#### Explication
- `bars.transition()` : Démarre une transition sur tous les éléments sélectionnés.
- `.duration(1000)` : Définit la durée de la transition à 1000 millisecondes (1 seconde).
- `.attr('height', d => d.sales * 1.5)` : Change la hauteur des barres pendant la transition.

## 2.5 Création d'une Visualisation Simple

### Exemple : Graphique à Barres Complet
Voici un exemple complet qui intègre toutes les étapes :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Visualisation avec D3.js</title>
    <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
    <script>
        const svg = d3.select('body').append('svg')
            .attr('width', 500)
            .attr('height', 300);

        svg.append('line') // Axe X
            .attr('x1', 0)
            .attr('y1', 250)
            .attr('x2', 500)
            .attr('y2', 250)
            .attr('stroke', 'black');

        svg.append('line') // Axe Y
            .attr('x1', 0)
            .attr('y1', 0)
            .attr('x2', 0)
            .attr('y2', 250)
            .attr('stroke', 'black');

        const data = [
            { product: 'A', sales: 120 },
            { product: 'B', sales: 80 },
            { product: 'C', sales: 150 },
            { product: 'D', sales: 90 }
        ];

        const bars = svg.selectAll('rect')
            .data(data)
            .enter()
            .append('rect')
            .attr('width', 40)
            .attr('height', d => d.sales)
            .attr('x', (d, i) => i * 45)
            .attr('y', d => 250 - d.sales)
            .attr('fill', 'steelblue');

        bars.transition()
            .duration(1000)
            .attr('height', d => d.sales * 1.5);
    </script>
</body>
</html>
```

### Résultat
Lorsque vous ouvrez `index.html` dans votre navigateur, vous devriez voir un graphique à barres représentant les ventes des produits, avec des axes visibles.

## 2.6 Exercices
### Exercice 1 : Modifier le Graphique
- Changez les valeurs des ventes et observez comment le graphique se met à jour.
- Modifiez la couleur des barres.

### Exercice 2 : Ajouter des Étiquettes
- Utilisez `svg.append('text')` pour ajouter des étiquettes à chaque barre montrant le nom du produit et le nombre de ventes.

### Exercice 3 : Créer un Graphique Linéaire
- À partir des données de ventes mensuelles, créez un graphique linéaire et expliquez chaque étape.

## 2.7 Conclusion
D3.js est un outil puissant pour créer des visualisations interactives. En maîtrisant les concepts de base et en comprenant le code, vous serez en mesure de créer des graphiques dynamiques qui peuvent transformer des données en insights visuels.

---

**TP Corrigé :**
Pour le TP, les étudiants doivent soumettre leurs graphiques modifiés et ajouter des commentaires expliquant les changements apportés. Le formateur peut fournir des retours sur l'esthétique et la clarté des visualisations. -->

