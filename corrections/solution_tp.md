## **Exercice 1 : Visualiser la croissance d'une population**

**Code complet :**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Population par Ville</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="500" height="300"></svg>

  <script>
    const data = [
      { city: "Dakar", population: 1100000 },
      { city: "Thies", population: 500000 },
      { city: "Saint-Louis", population: 300000 },
    ];

    const svg = d3.select("svg");

    const circles = svg.selectAll("circle")
      .data(data)
      .enter()
      .append("circle")
      .attr("cx", (d, i) => 100 + i * 150)
      .attr("cy", 100)
      .attr("r", d => d.population / 40000)
      .attr("fill", "steelblue");

    svg.selectAll("text")
      .data(data)
      .enter()
      .append("text")
      .attr("x", (d, i) => 100 + i * 150)
      .attr("y", 160)
      .attr("text-anchor", "middle")
      .text(d => d.city);
  </script>
</body>
</html>
```

---

## **Exercice 2 : Suivi des ventes d'un produit**

**Code complet :**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Ventes de Produits</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="400" height="300"></svg>

  <script>
    const sales = [
      { product: "Savon Bio", unitsSold: 50 },
      { product: "Shampoing Bio", unitsSold: 70 },
      { product: "Lotion Hydratante", unitsSold: 30 },
    ];

    const svg = d3.select("svg");

    svg.selectAll("rect")
      .data(sales)
      .enter()
      .append("rect")
      .attr("x", (d, i) => 80 * i + 50)
      .attr("y", d => 250 - d.unitsSold * 3)
      .attr("width", 50)
      .attr("height", d => d.unitsSold * 3)
      .attr("fill", "teal");

    svg.selectAll("text")
      .data(sales)
      .enter()
      .append("text")
      .attr("x", (d, i) => 80 * i + 75)
      .attr("y", 270)
      .attr("text-anchor", "middle")
      .text(d => d.product);
  </script>
</body>
</html>
```

---

## **Exercice 3 : Comparer les températures d'une semaine**

**Code complet :**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Températures Hebdomadaires</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="600" height="300"></svg>

  <script>
    const temps = [
      { day: "Lundi", temperature: 30 },
      { day: "Mardi", temperature: 28 },
      { day: "Mercredi", temperature: 32 },
      { day: "Jeudi", temperature: 31 },
      { day: "Vendredi", temperature: 29 },
      { day: "Samedi", temperature: 27 },
      { day: "Dimanche", temperature: 30 },
    ];

    const svg = d3.select("svg");

    svg.selectAll("rect")
      .data(temps)
      .enter()
      .append("rect")
      .attr("x", 100)
      .attr("y", (d, i) => i * 35 + 20)
      .attr("width", d => d.temperature * 10)
      .attr("height", 20)
      .attr("fill", "orange");

    svg.selectAll("text")
      .data(temps)
      .enter()
      .append("text")
      .attr("x", 20)
      .attr("y", (d, i) => i * 35 + 35)
      .text(d => `${d.day} : ${d.temperature}°C`);
  </script>
</body>
</html>
```

---

## **Exercice 4 : Suivi des stocks dans un magasin**

**Code complet :**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Stocks du Magasin</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="400" height="200"></svg>

  <script>
    const stocks = [
      { product: "Tomates", quantity: 20 },
      { product: "Oignons", quantity: 15 },
      { product: "Riz", quantity: 10 },
    ];

    const colors = ["tomato", "goldenrod", "lightgreen"];

    const svg = d3.select("svg");

    svg.selectAll("circle")
      .data(stocks)
      .enter()
      .append("circle")
      .attr("cx", (d, i) => 100 + i * 120)
      .attr("cy", 80)
      .attr("r", d => d.quantity * 2)
      .attr("fill", (d, i) => colors[i]);

    svg.selectAll("text")
      .data(stocks)
      .enter()
      .append("text")
      .attr("x", (d, i) => 100 + i * 120)
      .attr("y", 150)
      .attr("text-anchor", "middle")
      .text(d => d.product);
  </script>
</body>
</html>
```

---

## **Exercice 5 : Simulation d'une playlist musicale**

**Code complet :**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Playlist musicale</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="600" height="300"></svg>

  <script>
    const playlist = [
      { title: "Youssou N'Dour - 7 Seconds", duration: 307 },
      { title: "Salif Keita - Africa", duration: 285 },
      { title: "Oumou Sangaré - Mogoya", duration: 230 },
    ];

    const currentSong = "Salif Keita - Africa";

    const svg = d3.select("svg");

    svg.selectAll("rect")
      .data(playlist)
      .enter()
      .append("rect")
      .attr("x", 100)
      .attr("y", (d, i) => 60 * i + 40)
      .attr("width", d => d.duration / 2)
      .attr("height", 30)
      .attr("fill", d => d.title === currentSong ? "green" : "gray");

    svg.selectAll("text")
      .data(playlist)
      .enter()
      .append("text")
      .attr("x", 100)
      .attr("y", (d, i) => 60 * i + 60)
      .attr("fill", "white")
      .text(d => d.title);
  </script>
</body>
</html>
```

## **Exercice 1 — Ventes journalières d’une boutique**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Ventes journalières</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="600" height="400"></svg>

  <script>
    const ventesJour = [
      {jour: "Lun", montant: 120},
      {jour: "Mar", montant: 180},
      {jour: "Mer", montant: 75},
      {jour: "Jeu", montant: 200},
      {jour: "Ven", montant: 140},
      {jour: "Sam", montant: 90},
      {jour: "Dim", montant: 50}
    ];

    const svg = d3.select("svg");

    svg.selectAll("rect")
      .data(ventesJour)
      .enter()
      .append("rect")
      .attr("x", (d, i) => 70 * i + 50)
      .attr("y", d => 350 - d.montant)
      .attr("width", 40)
      .attr("height", d => d.montant)
      .attr("fill", "#4CAF50");

    svg.selectAll("text")
      .data(ventesJour)
      .enter()
      .append("text")
      .attr("x", (d, i) => 70 * i + 70)
      .attr("y", 370)
      .attr("text-anchor", "middle")
      .text(d => d.jour);
  </script>
</body>
</html>
```

---

## **Exercice 2 — Nombre d’étudiants inscrits par filière**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Effectifs par filière</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="500" height="300"></svg>

  <script>
    const filieres = [
      {nom: "GL", effectif: 52},
      {nom: "IAGE", effectif: 48},
      {nom: "DITI", effectif: 33},
      {nom: "Finance", effectif: 60},
      {nom: "Droit", effectif: 45}
    ];

    const svg = d3.select("svg");

    svg.selectAll("rect")
      .data(filieres)
      .enter()
      .append("rect")
      .attr("x", 150)
      .attr("y", (d, i) => i * 40 + 30)
      .attr("width", d => d.effectif * 5)
      .attr("height", 25)
      .attr("fill", "#00796B");

    svg.selectAll("text")
      .data(filieres)
      .enter()
      .append("text")
      .attr("x", 10)
      .attr("y", (d, i) => i * 40 + 50)
      .text(d => `${d.nom} (${d.effectif})`);
  </script>
</body>
</html>
```

---

## **Exercice 3 — Classement des 10 meilleures villes touristiques**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Villes touristiques</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="1000" height="300"></svg>

  <script>
    const villes = [
      {ville: "Paris", visiteurs: 19000000},
      {ville: "Bangkok", visiteurs: 17000000},
      {ville: "Londres", visiteurs: 16000000},
      {ville: "Dubai", visiteurs: 15000000},
      {ville: "Singapour", visiteurs: 14000000},
      {ville: "New York", visiteurs: 13500000},
      {ville: "Istanbul", visiteurs: 13000000},
      {ville: "Tokyo", visiteurs: 12500000},
      {ville: "Rome", visiteurs: 10000000},
      {ville: "Barcelone", visiteurs: 9500000}
    ];

    const svg = d3.select("svg");

    svg.selectAll("circle")
      .data(villes)
      .enter()
      .append("circle")
      .attr("cx", (d, i) => 90 * i + 70)
      .attr("cy", 120)
      .attr("r", d => d.visiteurs / 600000)
      .attr("fill", "skyblue");

    svg.selectAll("text")
      .data(villes)
      .enter()
      .append("text")
      .attr("x", (d, i) => 90 * i + 70)
      .attr("y", 200)
      .attr("text-anchor", "middle")
      .text(d => d.ville);
  </script>
</body>
</html>
```

---

## **Exercice 4 — Notes d’un étudiant dans différentes matières**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Notes d'un étudiant</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="500" height="300"></svg>

  <script>
    const notes = [
      {matiere: "Maths", note: 14},
      {matiere: "Physique", note: 12},
      {matiere: "Programmation", note: 18},
      {matiere: "Base de Données", note: 15},
      {matiere: "Réseaux", note: 10}
    ];

    const svg = d3.select("svg");

    svg.selectAll("rect")
      .data(notes)
      .enter()
      .append("rect")
      .attr("x", (d, i) => i * 90 + 50)
      .attr("y", d => 250 - d.note * 10)
      .attr("width", 50)
      .attr("height", d => d.note * 10)
      .attr("fill", d => d.note >= 15 ? "green" : "orange");

    svg.selectAll("text")
      .data(notes)
      .enter()
      .append("text")
      .attr("x", (d, i) => i * 90 + 75)
      .attr("y", 270)
      .attr("text-anchor", "middle")
      .text(d => d.matiere);
  </script>
</body>
</html>
```

---

## **Exercice 5 — Dépenses mensuelles d’un foyer**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Dépenses mensuelles</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="600" height="250"></svg>

  <script>
    const depenses = [
      {categorie: "Loyer", montant: 250000},
      {categorie: "Nourriture", montant: 120000},
      {categorie: "Transport", montant: 40000},
      {categorie: "Santé", montant: 30000},
      {categorie: "Loisirs", montant: 20000},
      {categorie: "Électricité", montant: 35000}
    ];

    const svg = d3.select("svg");

    let x = 20;
    svg.selectAll("rect")
      .data(depenses)
      .enter()
      .append("rect")
      .attr("x", (d, i) => {
        const pos = x;
        x += d.montant / 1000 + 10;
        return pos;
      })
      .attr("y", 80)
      .attr("width", d => d.montant / 1000)
      .attr("height", 50)
      .attr("fill", (d, i) => d3.schemeCategory10[i]);

    svg.selectAll("text")
      .data(depenses)
      .enter()
      .append("text")
      .attr("x", (d, i) => 20 + i * 90)
      .attr("y", 75)
      .text(d => d.categorie);
  </script>
</body>
</html>
```

---

## **Exercice 6 — Répartition du trafic Internet par appareil**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Trafic Internet</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <svg width="400" height="400"></svg>

  <script>
    const traffic = [
      {appareil: "Smartphone", part: 62},
      {appareil: "Ordinateur", part: 30},
      {appareil: "Tablette", part: 8}
    ];

    const svg = d3.select("svg").append("g")
      .attr("transform", "translate(200,200)");

    const pie = d3.pie().value(d => d.part);
    const arc = d3.arc().innerRadius(0).outerRadius(100);
    const color = d3.scaleOrdinal(d3.schemeSet2);

    svg.selectAll("path")
      .data(pie(traffic))
      .enter()
      .append("path")
      .attr("d", arc)
      .attr("fill", (d, i) => color(i));

    svg.selectAll("text")
      .data(pie(traffic))
      .enter()
      .append("text")
      .attr("transform", d => `translate(${arc.centroid(d)})`)
      .attr("text-anchor", "middle")
      .text(d => `${d.data.appareil}`);
  </script>
</body>
</html>
```

---

## **Exercice 7 — Actualisation automatique (mini dashboard)**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Actualisation de Températures</title>
  <script src="https://d3js.org/d3.v7.min.js"></script>
</head>
<body>
  <button id="refresh">Actualiser</button>
  <svg width="600" height="300"></svg>

  <script>
    let temperature = [28, 30, 27, 29, 31, 32, 30];
    const svg = d3.select("svg");

    function update(data) {
      const bars = svg.selectAll("rect").data(data);

      bars.enter()
        .append("rect")
        .merge(bars)
        .attr("x", (d, i) => 80 * i + 50)
        .attr("y", d => 250 - d * 5)
        .attr("width", 40)
        .attr("height", d => d * 5)
        .attr("fill", "steelblue");

      bars.exit().remove();
    }

    update(temperature);

    d3.select("#refresh").on("click", () => {
      temperature = temperature.map(() => Math.floor(Math.random() * 10) + 26);
      update(temperature);
    });
  </script>
</body>
</html>
```

