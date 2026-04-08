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

# Examen : Création d’un Tableau de Bord Interactif avec D3.js  


<img src="d3js.jpeg" alt="D3JS" width="100px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;     



**Durée : 1,5 semaines (projet individuel)**

**Technologies : HTML, CSS, JavaScript, D3.js**
**Rendu : Dashboard complet**


## Objectif du projet

L’objectif de ce projet est de concevoir un **dashboard de data visualisation** à l’aide de **D3.js**, à partir d’un jeu de données réel.

Chaque étudiant devra :

* choisir **un dataset parmi ceux proposés**,
* réaliser un **dashboard contenant au minimum 3 graphiques différents**,
* structurer correctement une page HTML avec une ou plusieurs zones SVG,
* utiliser correctement les **échelles**, **axes** et **liaisons de données**.

---

## Organisation du choix des datasets

* La classe compte **18 étudiants**.
* **5 datasets** sont proposés.
* **Un même dataset ne peut être choisi que par 4 étudiants maximum**.
* Les étudiants doivent **déclarer leur choix à l’avance**.

> Objectif : **diversité des dashboards et des visualisations**.

---

## Datasets disponibles

1. **Données d’éducation aux États-Unis (carte choroplèthe)**
   [https://cdn.freecodecamp.org/testable-projects-fcc/data/choropleth_map/counties.json](https://cdn.freecodecamp.org/testable-projects-fcc/data/choropleth_map/counties.json)
   [https://cdn.freecodecamp.org/testable-projects-fcc/data/choropleth_map/for_user_education.json](https://cdn.freecodecamp.org/testable-projects-fcc/data/choropleth_map/for_user_education.json)

2. **Financement de projets Kickstarter**
   [https://cdn.freecodecamp.org/testable-projects-fcc/data/tree_map/kickstarter-funding-data.json](https://cdn.freecodecamp.org/testable-projects-fcc/data/tree_map/kickstarter-funding-data.json)

3. **Données sur les films**
   [https://cdn.freecodecamp.org/testable-projects-fcc/data/tree_map/movie-data.json](https://cdn.freecodecamp.org/testable-projects-fcc/data/tree_map/movie-data.json)

4. **Ventes de jeux vidéo**
   [https://cdn.freecodecamp.org/testable-projects-fcc/data/tree_map/video-game-sales-data.json](https://cdn.freecodecamp.org/testable-projects-fcc/data/tree_map/video-game-sales-data.json)

---

##  VISUALISATIONS MINIMALES ATTENDUES PAR DATASET

Chaque étudiant doit réaliser **au moins 3 graphiques** parmi ceux proposés ci-dessous pour le dataset choisi.

---

##  DATASET 1 – ÉDUCATION (counties + education)

### Graphiques minimum à réaliser :

1️ **Carte choroplèthe**

* Carte des comtés américains
* Couleur basée sur le pourcentage de diplômés
* Utilisation de `geoPath`, `geoAlbersUsa`
* Échelle de couleur (`scaleThreshold` ou `scaleQuantize`)

2️⃣ **Histogramme / Bar chart**

* Regroupement des comtés par tranches de pourcentage
* Axe X : tranches (0–10, 10–20, …)
* Axe Y : nombre de comtés

3️⃣ **Diagramme circulaire (pie chart)**

* Répartition des comtés par niveau d’éducation
* Utilisation de `d3.pie()` et `d3.arc()`

---

##  DATASET 2 – KICKSTARTER (tree map)

### Graphiques minimum à réaliser :

1️⃣ **Treemap**

* Taille des rectangles basée sur le financement
* Couleur par catégorie
* Utilisation de `d3.treemap()`

2️⃣ **Diagramme en barres**

* Total des financements par catégorie
* Axe X : catégories
* Axe Y : montants

3️⃣ **Diagramme circulaire**

* Répartition du nombre de projets par catégorie

---

##  DATASET 3 – FILMS

### Graphiques minimum à réaliser :

1️⃣ **Treemap**

* Taille des rectangles basée sur les ventes ou revenus
* Couleur par genre

2️⃣ **Bar chart**

* Total des revenus par genre de film

3️⃣ **Scatter plot**

* X : revenus
* Y : note ou autre indicateur numérique
* Chaque point représente un film

---

##  DATASET 4 – JEUX VIDÉO

### Graphiques minimum à réaliser :

1️⃣ **Treemap**

* Taille basée sur les ventes
* Couleur par plateforme ou éditeur

2️⃣ **Bar chart**

* Total des ventes par plateforme

3️⃣ **Diagramme circulaire**

* Répartition des ventes par région (NA, EU, JP, Global)

---

#  Contraintes générales du dashboard

* Minimum **3 graphiques distincts**
* Chaque graphique doit :

  * être dans un **SVG**
  * utiliser les **échelles adaptées**
  * avoir des **axes si nécessaire**
* Les données doivent être **liées avec D3**
* Pas de transition obligatoire

## Exemple de dashboard
![alt text](<ChatGPT Image 13 janv. 2026, 12_23_32.png>)