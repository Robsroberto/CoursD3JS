
# 🧪 Solutions par exercice

## Exercice 1 – Mise en place

**HTML**

```html
<div id="app"></div>
<script src="script.js"></script>
```

**JS (`script.js`)**

```js
console.log("Bienvenue !");
document.getElementById("app").textContent = "Bienvenue dans la Data Visualisation !";
```

---

## Exercice 2 – Création dynamique d’éléments

```js
const app = document.getElementById("app");
for (let i = 1; i <= 5; i++) {
  const div = document.createElement("div");
  div.textContent = `Bloc ${i}`;
  app.appendChild(div);
}
```

---

## Exercice 3 – Modifier le style avec JavaScript

```js
const couleurs = ["red", "blue", "green", "orange", "purple"];
const blocs = app.querySelectorAll("div"); // ceux créés à l'exercice 2
blocs.forEach((div, i) => {
  div.style.width = "100px";
  div.style.height = "50px";
  div.style.margin = "6px 0";
  div.style.display = "flex";
  div.style.alignItems = "center";
  div.style.justifyContent = "center";
  div.style.backgroundColor = couleurs[i % couleurs.length];
  div.style.color = "white";
  div.style.borderRadius = "8px";
});
```

---

## Exercice 4 – Représentation de données simples (barres)

```js
const valeurs = [10, 30, 60, 20, 50];
const zoneBarres = document.createElement("div");
zoneBarres.id = "zone-barres";
zoneBarres.style.display = "flex";
zoneBarres.style.alignItems = "flex-end";
zoneBarres.style.gap = "8px";
zoneBarres.style.marginTop = "12px";
app.appendChild(zoneBarres);

valeurs.forEach(v => {
  const bar = document.createElement("div");
  bar.className = "bar";
  bar.style.width = "40px";
  bar.style.height = (v * 3) + "px"; // proportionnel à la valeur
  bar.style.background = "#0ea5e9";
  bar.style.borderRadius = "6px 6px 0 0";
  zoneBarres.appendChild(bar);
});
```

---

## Exercice 5 – Ajouter des étiquettes

```js
const bars = zoneBarres.querySelectorAll(".bar");
bars.forEach((bar, i) => {
  bar.style.position = "relative";
  const label = document.createElement("span");
  label.textContent = valeurs[i];
  label.style.position = "absolute";
  label.style.bottom = "100%";
  label.style.left = "50%";
  label.style.transform = "translate(-50%, -4px)";
  label.style.fontSize = "12px";
  label.style.color = "#111";
  bar.appendChild(label);
});
```

---

## Exercice 6 – Interaction simple (clic)

```js
bars.forEach((bar, i) => {
  bar.style.cursor = "pointer";
  bar.addEventListener("click", () => {
    bar.style.background = "#f97316"; // orange au clic
    alert(`Valeur : ${valeurs[i]}`);
  });
});
```

---

## Exercice 7 – Couleurs selon la valeur (mapping visuel)

```js
function couleurParValeur(v) {
  if (v < 20) return "#ef4444";       // rouge
  if (v <= 50) return "#f59e0b";      // orange
  return "#22c55e";                   // vert
}

bars.forEach((bar, i) => {
  bar.style.background = couleurParValeur(valeurs[i]);
});
```

---

## Exercice 8 – Mettre à jour les données (bouton)

```js
const btn = document.createElement("button");
btn.textContent = "Mettre à jour";
btn.style.marginTop = "12px";
btn.style.padding = "6px 10px";
btn.style.borderRadius = "6px";
btn.style.border = "1px solid #ddd";
btn.style.cursor = "pointer";
app.appendChild(btn);

btn.addEventListener("click", () => {
  for (let i = 0; i < valeurs.length; i++) {
    valeurs[i] = Math.floor(10 + Math.random() * 91); // 10..100
  }
  // MAJ hauteur, couleur, label
  const bars = zoneBarres.querySelectorAll(".bar");
  bars.forEach((bar, i) => {
    bar.style.height = (valeurs[i] * 3) + "px";
    bar.style.background = couleurParValeur(valeurs[i]);
    bar.querySelector("span").textContent = valeurs[i];
  });
});
```

---

## Exercice 9 – Mini-légende

```js
const legende = document.createElement("div");
legende.style.marginTop = "12px";
legende.innerHTML = `
  <strong>Légende :</strong>
  <span style="color:#ef4444">Rouge</span> : valeur < 20 |
  <span style="color:#f59e0b">Orange</span> : 20–50 |
  <span style="color:#22c55e">Vert</span> : > 50
`;
app.appendChild(legende);
```

---

## Exercice 10 – Mini-dashboard (titre, total, moyenne)

```js
// Titre dynamique
const h1 = document.createElement("h1");
h1.textContent = "Mini-dashboard JS (sans D3)";
h1.style.fontSize = "20px";
h1.style.margin = "16px 0";
app.prepend(h1);

// Zone KPIs
const kpis = document.createElement("div");
kpis.style.display = "flex";
kpis.style.gap = "16px";
kpis.style.margin = "8px 0 16px";
app.insertBefore(kpis, zoneBarres);

const kpiTotal = document.createElement("div");
const kpiMoyenne = document.createElement("div");
[kpiTotal, kpiMoyenne].forEach(k => {
  k.style.background = "#fff";
  k.style.border = "1px solid #eee";
  k.style.borderRadius = "10px";
  k.style.padding = "10px 12px";
  k.style.boxShadow = "0 2px 8px rgba(0,0,0,0.05)";
});
kpis.append(kpiTotal, kpiMoyenne);

function majKPIs() {
  const total = valeurs.reduce((a,b) => a+b, 0);
  const moyenne = total / valeurs.length;
  kpiTotal.innerHTML = `<strong>Total :</strong> ${total}`;
  kpiMoyenne.innerHTML = `<strong>Moyenne :</strong> ${moyenne.toFixed(1)}`;
  console.log("Moyenne actuelle :", moyenne.toFixed(2));
}
majKPIs();

// Recalcule les KPI aussi quand on clique sur "Mettre à jour"
btn.addEventListener("click", majKPIs);
```

---

# 📦 Version complète (tout-en-un)

Copie-colle ce fichier pour avoir une **démo complète** prête pour le 1er cours (sans D3, 100% DOM) :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <title>Test de niveau JS + DOM (pré-DataViz)</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    body { font-family: system-ui, Arial, sans-serif; margin: 0; padding: 20px; background:#f7f7fb; color:#111; }
    #app { background:#fff; border:1px solid #eee; border-radius:14px; padding:16px; box-shadow:0 4px 16px rgba(0,0,0,0.05); }
  </style>
</head>
<body>
  <div id="app"></div>

  <script>
    console.log("Bienvenue !");
    const app = document.getElementById("app");
    app.textContent = "Bienvenue dans la Data Visualisation !";

    // Exo 2
    for (let i = 1; i <= 5; i++) {
      const div = document.createElement("div");
      div.textContent = `Bloc ${i}`;
      app.appendChild(div);
    }

    // Exo 3
    const couleurs = ["red", "blue", "green", "orange", "purple"];
    const blocs = app.querySelectorAll("div");
    blocs.forEach((div, i) => {
      div.style.width = "100px";
      div.style.height = "50px";
      div.style.margin = "6px 0";
      div.style.display = "flex";
      div.style.alignItems = "center";
      div.style.justifyContent = "center";
      div.style.backgroundColor = couleurs[i % couleurs.length];
      div.style.color = "white";
      div.style.borderRadius = "8px";
    });

    // Titre (Exo 10)
    const h1 = document.createElement("h1");
    h1.textContent = "Mini-dashboard JS (sans D3)";
    h1.style.fontSize = "20px";
    h1.style.margin = "16px 0";
    app.prepend(h1);

    // Données (Exo 4)
    const valeurs = [10, 30, 60, 20, 50];

    // KPIs (Exo 10)
    const kpis = document.createElement("div");
    kpis.style.display = "flex";
    kpis.style.gap = "16px";
    kpis.style.margin = "8px 0 16px";
    app.insertBefore(kpis, blocs[blocs.length - 1].nextSibling);

    const kpiTotal = document.createElement("div");
    const kpiMoyenne = document.createElement("div");
    [kpiTotal, kpiMoyenne].forEach(k => {
      k.style.background = "#fff";
      k.style.border = "1px solid #eee";
      k.style.borderRadius = "10px";
      k.style.padding = "10px 12px";
      k.style.boxShadow = "0 2px 8px rgba(0,0,0,0.05)";
    });
    kpis.append(kpiTotal, kpiMoyenne);

    function majKPIs() {
      const total = valeurs.reduce((a,b) => a+b, 0);
      const moyenne = total / valeurs.length;
      kpiTotal.innerHTML = `<strong>Total :</strong> ${total}`;
      kpiMoyenne.innerHTML = `<strong>Moyenne :</strong> ${moyenne.toFixed(1)}`;
      console.log("Moyenne actuelle :", moyenne.toFixed(2));
    }

    // Zone de barres
    const zoneBarres = document.createElement("div");
    zoneBarres.id = "zone-barres";
    zoneBarres.style.display = "flex";
    zoneBarres.style.alignItems = "flex-end";
    zoneBarres.style.gap = "8px";
    zoneBarres.style.marginTop = "12px";
    app.appendChild(zoneBarres);

    // Fonction couleur (Exo 7)
    function couleurParValeur(v) {
      if (v < 20) return "#ef4444";       // rouge
      if (v <= 50) return "#f59e0b";      // orange
      return "#22c55e";                   // vert
    }

    // Dessin initial
    valeurs.forEach(v => {
      const bar = document.createElement("div");
      bar.className = "bar";
      bar.style.width = "40px";
      bar.style.height = (v * 3) + "px";
      bar.style.background = couleurParValeur(v);
      bar.style.borderRadius = "6px 6px 0 0";
      bar.style.position = "relative";
      bar.style.cursor = "pointer";

      const label = document.createElement("span");
      label.textContent = v;
      label.style.position = "absolute";
      label.style.bottom = "100%";
      label.style.left = "50%";
      label.style.transform = "translate(-50%, -4px)";
      label.style.fontSize = "12px";
      label.style.color = "#111";
      bar.appendChild(label);

      bar.addEventListener("click", () => {
        bar.style.background = "#f97316";
        alert(`Valeur : ${v}`);
      });

      zoneBarres.appendChild(bar);
    });

    // Bouton de mise à jour (Exo 8)
    const btn = document.createElement("button");
    btn.textContent = "Mettre à jour";
    btn.style.marginTop = "12px";
    btn.style.padding = "6px 10px";
    btn.style.borderRadius = "6px";
    btn.style.border = "1px solid #ddd";
    btn.style.cursor = "pointer";
    app.appendChild(btn);

    btn.addEventListener("click", () => {
      const bars = zoneBarres.querySelectorAll(".bar");
      for (let i = 0; i < valeurs.length; i++) {
        valeurs[i] = Math.floor(10 + Math.random() * 91); // 10..100
        const bar = bars[i];
        bar.style.height = (valeurs[i] * 3) + "px";
        bar.style.background = couleurParValeur(valeurs[i]);
        bar.querySelector("span").textContent = valeurs[i];
      }
      majKPIs();
    });

    // Légende (Exo 9)
    const legende = document.createElement("div");
    legende.style.marginTop = "12px";
    legende.innerHTML = `
      <strong>Légende :</strong>
      <span style="color:#ef4444">Rouge</span> : valeur < 20 |
      <span style="color:#f59e0b">Orange</span> : 20–50 |
      <span style="color:#22c55e">Vert</span> : > 50
    `;
    app.appendChild(legende);

    // Maj KPIs initiale
    majKPIs();
  </script>
</body>
</html>
```

---

Si tu veux, je peux aussi te préparer **une feuille “corrigé enseignant”** (PDF propre) avec des captures d’écran attendues pour chaque exercice, et une **grille d’observation** rapide à cocher pendant le cours.
