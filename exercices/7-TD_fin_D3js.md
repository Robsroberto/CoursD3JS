Voici une série de **20 exercices pratiques** pour préparer votre certification en D3.js. Ces exercices sont conçus pour aborder différents concepts de D3.js tout en utilisant des données réelles ou concrètes. Chaque exercice inclut un problème à résoudre, une question explicite qui pousse à comprendre les solutions, et des données réalistes. Ces exercices permettent de maîtriser les principales fonctionnalités de D3.js, de la manipulation des données à la création de graphiques avancés.

---

### **1. Créer un Graphique à Barres Simple avec des Données Réelles**
**Données** : Nombre de visiteurs d'un site web par mois.

**Exercice** : Créez un graphique à barres représentant les visites d’un site web au cours des 6 derniers mois. Utilisez les données suivantes :

```json
[
  { "mois": "Janvier", "visites": 1000 },
  { "mois": "Février", "visites": 1500 },
  { "mois": "Mars", "visites": 1300 },
  { "mois": "Avril", "visites": 1200 },
  { "mois": "Mai", "visites": 1700 },
  { "mois": "Juin", "visites": 1600 }
]
```

**Question** : Comment pouvez-vous mettre à l’échelle les barres pour qu’elles correspondent à la taille du SVG ? Quelle fonction de D3 vous permet de calculer les bonnes échelles ?

---

### **2. Ajouter des Labels à un Graphique à Barres**
**Données** : Suivez les mêmes données que dans l'exercice précédent.

**Exercice** : Ajoutez des labels au-dessus de chaque barre pour indiquer le nombre de visites pour chaque mois.

**Question** : Quelle méthode de D3 permet d’ajouter des textes dynamiquement et comment positionner les labels en fonction des valeurs des barres ?

---

### **3. Créer un Graphique Linéaire pour Suivre une Évolution**
**Données** : Evolution des prix du pétrole sur 12 mois (en USD par baril).

```json
[
  { "mois": "Janvier", "prix": 60 },
  { "mois": "Février", "prix": 65 },
  { "mois": "Mars", "prix": 62 },
  { "mois": "Avril", "prix": 70 },
  { "mois": "Mai", "prix": 72 },
  { "mois": "Juin", "prix": 74 },
  { "mois": "Juillet", "prix": 71 },
  { "mois": "Août", "prix": 69 },
  { "mois": "Septembre", "prix": 75 },
  { "mois": "Octobre", "prix": 80 },
  { "mois": "Novembre", "prix": 85 },
  { "mois": "Décembre", "prix": 90 }
]
```

**Exercice** : Créez un graphique linéaire pour visualiser l'évolution des prix du pétrole.

**Question** : Comment déterminer les échelles X et Y pour un graphique temporel, et pourquoi utiliser `d3.scaleTime()` pour l’axe des X ?

---

### **4. Ajouter des Interactions à un Graphique Linéaire**
**Données** : Utilisez les mêmes données du graphique linéaire sur les prix du pétrole.

**Exercice** : Ajoutez une interaction qui affiche une info-bulle avec le mois et le prix exact lorsque l’utilisateur survole un point de la ligne.

**Question** : Comment utiliser les événements de D3 pour interagir avec un graphique et afficher des informations supplémentaires au survol d’un point ?

---

### **5. Créer un Graphique à Nuage de Points avec des Données Réelles**
**Données** : Données sur les revenus et les dépenses de 10 entreprises en 2022 (en millions).

```json
[
  { "revenu": 20, "depenses": 18, "entreprise": "A" },
  { "revenu": 35, "depenses": 33, "entreprise": "B" },
  { "revenu": 50, "depenses": 40, "entreprise": "C" },
  { "revenu": 60, "depenses": 45, "entreprise": "D" },
  { "revenu": 70, "depenses": 50, "entreprise": "E" },
  { "revenu": 100, "depenses": 80, "entreprise": "F" },
  { "revenu": 150, "depenses": 120, "entreprise": "G" },
  { "revenu": 200, "depenses": 160, "entreprise": "H" },
  { "revenu": 250, "depenses": 200, "entreprise": "I" },
  { "revenu": 300, "depenses": 270, "entreprise": "J" }
]
```

**Exercice** : Créez un nuage de points où les revenus sont sur l'axe X et les dépenses sur l'axe Y.

**Question** : Comment pouvez-vous utiliser la taille des points pour refléter une autre dimension des données, comme le nombre d’employés ?

---

### **6. Créer un Graphique en Secteurs (Pie Chart)**
**Données** : Répartition du budget d’un gouvernement.

```json
[
  { "categorie": "Éducation", "montant": 50 },
  { "categorie": "Santé", "montant": 30 },
  { "categorie": "Sécurité", "montant": 15 },
  { "categorie": "Infrastructure", "montant": 5 }
]
```

**Exercice** : Créez un graphique en secteurs pour représenter la répartition du budget.

**Question** : Quel est le rôle de la fonction `d3.arc()` et comment l’utiliser pour dessiner des segments ?

---

### **7. Graphique en Barres Empilées pour Comparer les Ventes par Région**
**Données** : Ventes de 3 produits dans 4 régions.

```json
[
  { "region": "Nord", "produit1": 30, "produit2": 45, "produit3": 15 },
  { "region": "Sud", "produit1": 50, "produit2": 40, "produit3": 20 },
  { "region": "Est", "produit1": 60, "produit2": 35, "produit3": 25 },
  { "region": "Ouest", "produit1": 70, "produit2": 30, "produit3": 40 }
]
```

**Exercice** : Créez un graphique en barres empilées pour visualiser la répartition des ventes par produit dans chaque région.

**Question** : Comment utiliser les fonctions d’agrégation et les échelles d’empilement de D3 pour gérer les données ?

---

### **8. Créer un Graphique de Distribution (Histogramme)**
**Données** : Distribution des âges d’un groupe de personnes.

```json
[
  { "age": 25 },
  { "age": 30 },
  { "age": 35 },
  { "age": 40 },
  { "age": 45 },
  { "age": 50 },
  { "age": 55 },
  { "age": 60 },
  { "age": 65 },
  { "age": 70 }
]
```

**Exercice** : Créez un histogramme pour visualiser la distribution des âges.

**Question** : Comment utiliser `d3.histogram()` pour regrouper les données et quelle est l’importance de définir des intervalles (bins) ?

---

### **9. Créer un Graphique de Boxplot**
**Données** : Salaires des employés dans une entreprise (en milliers de dollars).

```json
[
  35, 50, 75, 100, 120, 150, 180, 200, 220, 250
]
```

**Exercice** : Créez un diagramme de boîte pour afficher la répartition des salaires.

**Question** : Comment D3 calcule-t-il les quartiles pour générer le boxplot, et que représente chaque élément du diagramme (médiane, quartiles, valeurs aberrantes) ?

---

### **10. Créer une Carte Choroplèthe pour Visualiser des Données Géographiques**
**Données** : Population par région dans un pays fictif.

```json
[
  { "region": "Région A", "population": 500000 },
  { "region": "Région B", "population": 1000000 },
  { "region": "Région C", "population": 750000 },
  { "region": "Région D", "population": 200000 }
]
```

**Exercice** : Créez une carte choroplèthe représentant la population des différentes régions.

**Question** : Quelle échelle utiliser pour colorier les régions en fonction de la population et comment intégrer un fichier géospatial (GeoJSON) ?

---

### **11. Créer une Carte à Bulles**
**Données** : Ventes par pays pour une entreprise.

```json
[
  { "p

ays": "USA", "ventes": 50000 },
  { "pays": "Canada", "ventes": 35000 },
  { "pays": "France", "ventes": 45000 },
  { "pays": "Allemagne", "ventes": 60000 },
  { "pays": "Japon", "ventes": 70000 }
]
```

**Exercice** : Créez une carte où chaque pays est représenté par une bulle dont la taille est proportionnelle aux ventes.

**Question** : Comment gérer les projections géographiques pour visualiser correctement les données sur une carte ?

---

### **12. Créer un Diagramme en Radar**
**Données** : Note d’un étudiant dans 5 matières.

```json
[
  { "matiere": "Maths", "note": 18 },
  { "matiere": "Anglais", "note": 16 },
  { "matiere": "Physique", "note": 14 },
  { "matiere": "Histoire", "note": 15 },
  { "matiere": "Chimie", "note": 19 }
]
```

**Exercice** : Créez un diagramme en radar pour afficher les notes de l’étudiant.

**Question** : Comment ajuster les axes et les segments pour afficher des valeurs sur un cercle avec D3.js ?

---

### **13. Créer une Visualisation de Série Temporelle Interactif**
**Données** : Température quotidienne d’une ville durant une semaine.

```json
[
  { "date": "2023-01-01", "temperature": 12 },
  { "date": "2023-01-02", "temperature": 15 },
  { "date": "2023-01-03", "temperature": 13 },
  { "date": "2023-01-04", "temperature": 17 },
  { "date": "2023-01-05", "temperature": 19 },
  { "date": "2023-01-06", "temperature": 16 },
  { "date": "2023-01-07", "temperature": 14 }
]
```

**Exercice** : Créez un graphique de série temporelle avec des points représentant la température, et permettez à l’utilisateur de zoomer sur les données en cliquant sur l’axe des X.

**Question** : Comment gérer le zoom et le pan avec D3.js et quelles sont les implications de l’utilisation de `d3.zoom()` ?

---
Voici les **7 derniers exercices pratiques** pour compléter la série de 20, afin de couvrir des concepts plus avancés et des situations plus complexes dans D3.js :

---

### **14. Créer un Graphique de Gantt pour la Gestion de Projet**
**Données** : Planification de tâches dans un projet de développement logiciel.

```json
[
  { "tache": "Analyse des besoins", "debut": "2025-01-01", "fin": "2025-01-10" },
  { "tache": "Conception", "debut": "2025-01-11", "fin": "2025-01-20" },
  { "tache": "Développement", "debut": "2025-01-21", "fin": "2025-02-15" },
  { "tache": "Tests", "debut": "2025-02-16", "fin": "2025-03-05" },
  { "tache": "Déploiement", "debut": "2025-03-06", "fin": "2025-03-15" }
]
```

**Exercice** : Créez un graphique de Gantt pour afficher la planification des tâches d’un projet.

**Question** : Comment pouvez-vous ajuster l’échelle du temps pour gérer différentes durées de tâches et représenter les dates de début et de fin ?

---

### **15. Créer un Graphique de Sankey pour Visualiser les Flux de Données**
**Données** : Répartition des ventes entre différents canaux de distribution.

```json
[
  { "source": "Magasin A", "cible": "Magasin B", "valeur": 100 },
  { "source": "Magasin A", "cible": "Magasin C", "valeur": 200 },
  { "source": "Magasin B", "cible": "Magasin D", "valeur": 150 },
  { "source": "Magasin C", "cible": "Magasin D", "valeur": 250 }
]
```

**Exercice** : Créez un graphique de Sankey pour visualiser les flux de vente entre différents magasins.

**Question** : Quelle méthode de D3 permet de gérer la mise en forme des flux (en termes de largeur et de direction) et comment ajuster la taille de chaque flux selon la valeur ?

---

### **16. Créer une Visualisation Combinée avec Graphiques Linéaires et à Barres**
**Données** : Évolution des températures mensuelles et des précipitations.

```json
[
  { "mois": "Janvier", "temperature": 5, "precipitations": 10 },
  { "mois": "Février", "temperature": 7, "precipitations": 15 },
  { "mois": "Mars", "temperature": 10, "precipitations": 20 },
  { "mois": "Avril", "temperature": 15, "precipitations": 25 },
  { "mois": "Mai", "temperature": 20, "precipitations": 30 }
]
```

**Exercice** : Créez un graphique combiné qui affiche l’évolution des températures sous forme de ligne et les précipitations sous forme de barres.

**Question** : Comment gérez-vous deux échelles différentes pour superposer ces deux types de graphiques sur le même espace (un pour les températures et un autre pour les précipitations) ?

---

### **17. Créer un Graphique Dynamique avec des Données en Temps Réel**
**Données** : Données sur la température en temps réel depuis un capteur (exemples simulés).

```json
[
  { "timestamp": "2025-01-01T00:00:00Z", "temperature": 22 },
  { "timestamp": "2025-01-01T00:01:00Z", "temperature": 23 },
  { "timestamp": "2025-01-01T00:02:00Z", "temperature": 24 },
  { "timestamp": "2025-01-01T00:03:00Z", "temperature": 25 }
]
```

**Exercice** : Créez un graphique en temps réel où les nouvelles données de température sont ajoutées à un graphique linéaire toutes les secondes.

**Question** : Comment gérer l'ajout dynamique de nouvelles données dans un graphique en temps réel, et comment assurer que l’axe des X est mis à jour sans affecter les précédentes données ?

---

### **18. Créer un Graphique Interactif avec Plusieurs Filtres**
**Données** : Performance de plusieurs actions boursières sur un mois.

```json
[
  { "date": "2025-01-01", "action": "A", "prix": 100 },
  { "date": "2025-01-02", "action": "A", "prix": 105 },
  { "date": "2025-01-01", "action": "B", "prix": 200 },
  { "date": "2025-01-02", "action": "B", "prix": 205 }
]
```

**Exercice** : Créez un graphique linéaire où les utilisateurs peuvent sélectionner quelles actions afficher (par exemple, A, B ou les deux), et les prix sont tracés dans le graphique en fonction des filtres appliqués.

**Question** : Comment utiliser `d3.select()` et `d3.event` pour mettre à jour dynamiquement le graphique en fonction des interactions avec des filtres, et comment combiner les événements avec des axes réactifs ?

---

### **19. Créer un Graphique de Distribution avec des Données de Population par Pays**
**Données** : Population par pays (en millions).

```json
[
  { "pays": "USA", "population": 331 },
  { "pays": "Inde", "population": 1380 },
  { "pays": "Chine", "population": 1441 },
  { "pays": "Russie", "population": 145 },
  { "pays": "Brésil", "population": 213 }
]
```

**Exercice** : Créez un histogramme représentant la population des pays, avec des groupes par continent.

**Question** : Comment pouvez-vous adapter ce graphique pour gérer des groupes (par continent) tout en représentant la population individuelle de chaque pays à l’aide de différentes couleurs ?

---

### **20. Créer un Graphique de Corrélation avec des Données de Performances**
**Données** : Performance d'employés en fonction de l’expérience (en années).

```json
[
  { "experience": 1, "performance": 65 },
  { "experience": 2, "performance": 70 },
  { "experience": 3, "performance": 75 },
  { "experience": 4, "performance": 80 },
  { "experience": 5, "performance": 85 }
]
```

**Exercice** : Créez un graphique de corrélation (nuage de points) pour visualiser la relation entre l'expérience des employés et leur performance.

**Question** : Comment utiliser une échelle de couleur pour refléter la distribution de la performance, et quelles fonctions de D3 peuvent vous aider à calculer et tracer une ligne de tendance ?

---
