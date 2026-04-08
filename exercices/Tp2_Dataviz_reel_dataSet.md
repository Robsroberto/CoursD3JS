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

# **TP conception graphique basé sur des datasets avec D3.js**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 

<img src="d3js.jpeg" alt="D3JS" width="100px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  

 **Par Robert DIASSÉ**  

---

##  **Exercice 1 – Bar chart : comparaison du rendement agricole (Barley)**


**Dataset :**

[https://raw.githubusercontent.com/vega/vega/master/docs/data/barley.json](https://raw.githubusercontent.com/vega/vega/master/docs/data/barley.json)

### **Objectif :**

Créer un **bar chart** comparant le rendement moyen (`yield`) pour chaque variété (`variety`).

### **Travail demandé :**

1. Charger les données avec `d3.json()`.
2. Afficher les 10 premières lignes dans un tableau.
3. Calculer :

   * nombre total d’enregistrements
   * rendement moyen global
   * rendement moyen *par variété*
4. Construire un **bar chart vertical** :

   * X = variété
   * Y = rendement moyen
5. Colorier les barres en violet clair.
6. Ajouter un titre + axes.

---

#  **Exercice 2 – Line chart : évolution de la température maximale**


**Dataset :**
[https://raw.githubusercontent.com/vega/vega/master/docs/data/weather.csv](https://raw.githubusercontent.com/vega/vega/master/docs/data/weather.csv)

### **Objectif :**

Créer une **courbe temporelle** représentant l’évolution de la température maximale (`temp_max`).

### Travail demandé :

1. Charger le dataset avec `d3.csv()`.
2. Afficher les 30 premières lignes dans un tableau.
3. Calculer :

   * température maximale
   * température moyenne
   * nombre total de jours
4. Construire un **line chart** :

   * X = index du jour (1, 2, 3…)
   * Y = temp_max
5. Ajouter un titre + axes + graduations.

---

#  **Exercice 3 – Scatter Plot : relation entre notes de films**


**Dataset :**
[https://raw.githubusercontent.com/vega/vega/master/docs/data/movies.json](https://raw.githubusercontent.com/vega/vega/master/docs/data/movies.json)

### Objectif :

Visualiser la relation entre :

* IMDB_Rating
* Rotten_Tomatoes_Rating

### Travail demandé :

1. Charger les données JSON.
2. Afficher les 20 premières lignes dans un tableau.
3. Calculer :

   * score IMDB moyen
   * score Rotten moyen
   * nombre total de films
4. Construire un **scatter plot** :

   * X = IMDB_Rating
   * Y = Rotten_Tomatoes_Rating
5. Ajouter un titre + axes + points bleus.

---

#  **Exercice 4 – Scatter Plot  avec couleur : Manchots de Palmer**


**Dataset :**
[https://raw.githubusercontent.com/mwaskom/seaborn-data/master/penguins.csv](https://raw.githubusercontent.com/mwaskom/seaborn-data/master/penguins.csv)

### Objectif :

Créer un scatter plot distinguant les espèces de manchots par couleur.

### Travail demandé :

1. Charger le CSV.
2. Afficher les 15 premières lignes dans un tableau.
3. Calculer :

   * longueur moyenne du bec
   * profondeur moyenne du bec
   * nombre total de manchots
4. Construire un scatter plot :

   * X = bill_length_mm
   * Y = bill_depth_mm
5. Colorier selon l’espèce :

   * Adelie → bleu
   * Gentoo → vert
   * Chinstrap → orange
6. Ajouter une légende.

