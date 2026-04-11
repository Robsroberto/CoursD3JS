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
## **Chapitre 1 : Introduction à la Visualisation de Données**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 

<img src="d3js.jpeg" alt="D3JS" width="100px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   **Par Robert DIASSÉ**  

---


### **1.1 Qu'est-ce que la Visualisation de Données ?**

La visualisation de données est le processus de transformation de données brutes en graphiques visuels, permettant ainsi de faciliter leur interprétation et de communiquer des informations de manière efficace. Elle joue un rôle crucial dans plusieurs domaines, tels que les affaires, la science et le journalisme.

#### **Pourquoi utiliser la visualisation de données ?**
- **Synthétiser des informations** : Rendre des ensembles de données complexes plus lisibles et digestes.
- **Détection rapide des tendances** : Identifier des motifs ou des anomalies plus rapidement qu'avec de simples chiffres.
- **Améliorer la prise de décision** : Aider à prendre des décisions plus informées basées sur des faits.
- **Simplifier la communication** : Rendre les résultats d'analyses de données accessibles à un large public.

### **1.2 Principes de Base pour Réussir une Visualisation de Données**

Avant de plonger dans D3.js, il est essentiel de comprendre quelques notions clés qui permettent de créer des visualisations efficaces.

#### **1.2.1 Variables Visuelles**
Les variables visuelles sont les éléments graphiques utilisés pour représenter les données, notamment :
- **Position** : Emplacement d'un point ou d'une barre sur un graphique pour représenter une donnée.
- **Couleur** : Indique des catégories ou des intensités.
- **Taille** : Représente des valeurs numériques (hauteur d'une barre, taille d'un cercle).
- **Forme** : Distinction entre différentes catégories de données.

#### **1.2.2 Échelles**
Les échelles traduisent les valeurs des données en représentations visuelles proportionnelles :
- **Échelles linéaires** : Pour des valeurs continues (températures, distances).
- **Échelles ordinales** : Pour des catégories (jours de la semaine, types de produits).
- **Échelles de couleurs** : Pour représenter des intensités sur des cartes thermiques ou des dégradés.

#### **1.2.3 Axes X et Y**
Les axes structurent une visualisation bidimensionnelle :
- **L'axe X** : Représente souvent le temps ou les catégories.
- **L'axe Y** : Représente généralement des valeurs numériques.

##### **Exemple : Graphique en Barres pour les Ventes Mensuelles**
- **Axe X** : Montre les mois de l’année (janvier, février, etc.).
- **Axe Y** : Représente les montants des ventes en dollars.
- **Position des barres** : Chaque barre est placée sur l'axe X pour représenter un mois spécifique.
- **Hauteur des barres** : Indique le montant des ventes pour ce mois.
- **Couleur** : Peut être utilisée pour distinguer différentes régions ou types de produits.

### **1.3 Principes de Conception Visuelle**

Pour réussir une visualisation, il est essentiel de suivre certains principes de conception :

#### **1.3.1 Simplicité**
Évitez la surcharge d'informations. Une visualisation doit être claire et concise pour éviter la confusion.

#### **1.3.2 Clarté des Données**
L’objectif est de rendre les données aussi claires que possible, avec des axes bien définis et des légendes explicites.

#### **1.3.3 Hiérarchie Visuelle**
Organisez visuellement les informations pour refléter leur importance relative. Utilisez des tailles de polices et des épaisseurs de lignes différentes pour mettre en avant certaines données.

#### **1.3.4 Cohérence**
Maintenez la cohérence dans vos visualisations en utilisant les mêmes styles, couleurs et polices pour des représentations similaires.

---


### 1.4 Exemples Pratiques
#### Exemple 1 : Graphique à Barres
Imaginons que nous avons les ventes de différents produits :

| Produit  | Ventes |
|----------|--------|
| A        | 120    |
| B        | 80     |
| C        | 150    |
| D        | 90     |

Un graphique à barres pourrait être utilisé pour représenter ces données.

#### Exemple 2 : Graphique Linéaire
Considérons les ventes mensuelles sur une année :

| Mois      | Ventes |
|-----------|--------|
| Janvier   | 100    |
| Février   | 200    |
| Mars      | 150    |
| Avril     | 300    |

Un graphique linéaire montrerait l'évolution des ventes au fil des mois.

<!-- ## 1.5 Exercices -->
#### Exercice 1 : Identifier les Types de Visualisation
Pour chaque scénario ci-dessous, indiquez le type de visualisation le plus approprié :
1. Comparer le nombre de visiteurs d'un site web sur plusieurs mois.
2. Montrer la répartition des dépenses par catégorie dans un budget.
3. Analyser la croissance des ventes d'une entreprise sur plusieurs années.

<!-- ### Exercice 2 : Créer un Graphique à Barres
Utilisez un outil de visualisation (comme Excel ou Google Sheets) pour créer un graphique à barres à partir des données de ventes de produits fournies ci-dessus. -->


### Conclusion 

- La visualisation de données est essentielle pour extraire des insights significatifs de grands ensembles de données.
- Comprendre les principes des variables visuelles, des échelles, et des axes est fondamental pour structurer des visualisations claires et efficaces.
- En suivant les principes de conception visuelle (simplicité, clarté, hiérarchie, cohérence), vous pourrez transformer des données brutes en outils puissants de communication.

---

<!-- **TP Corrigé :**
Pour le TP, les étudiants doivent soumettre leurs graphiques créés à partir des exercices. Le formateur peut fournir des retours sur la clarté, l'utilisation des couleurs, et la présentation générale. -->