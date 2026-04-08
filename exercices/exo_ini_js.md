Bien sûr ! Voici les solutions avec des explications pour chaque exercice.

### Solutions des exercices de base en JavaScript

1. **Calculatrice simple** :
   ```javascript
   function calculatrice(a, b, operation) {
       switch (operation) {
           case '+':
               return a + b;
           case '-':
               return a - b;
           case '*':
               return a * b;
           case '/':
               return b !== 0 ? a / b : 'Erreur : division par zéro';
           default:
               return 'Opération non valide';
       }
   }
   ```
   **Explication** :
   - La fonction prend trois paramètres : `a`, `b` (les nombres), et `operation` (le type d'opération).
   - Un `switch` est utilisé pour déterminer quelle opération effectuer.
   - Pour la division, une vérification est faite pour éviter la division par zéro.
   - Si l'opération n'est pas valide, un message d'erreur est renvoyé.

2. **Inverser une chaîne** :
   ```javascript
   function inverserChaine(str) {
       return str.split('').reverse().join('');
   }
   ```
   **Explication** :
   - La fonction prend une chaîne `str` en entrée.
   - `split('')` transforme la chaîne en tableau de caractères.
   - `reverse()` inverse l'ordre des éléments du tableau.
   - `join('')` combine les caractères inversés en une nouvelle chaîne.

3. **Vérification de palindrome** :
   ```javascript
   function estPalindrome(str) {
       const normalizedStr = str.toLowerCase().replace(/[^a-z0-9]/g, '');
       return normalizedStr === normalizedStr.split('').reverse().join('');
   }
   ```
   **Explication** :
   - La fonction normalise la chaîne en la convertissant en minuscules et en supprimant les caractères non alphanumériques.
   - Elle compare la chaîne normalisée à sa version inversée pour déterminer si c'est un palindrome.

4. **Tableau de carrés** :
   ```javascript
   function carreTableau(arr) {
       return arr.map(num => num * num);
   }
   ```
   **Explication** :
   - La fonction utilise `map()` pour créer un nouveau tableau.
   - Pour chaque élément `num` du tableau `arr`, le carré de `num` est calculé et ajouté au nouveau tableau.

### Solutions des exercices sur le DOM

1. **Changer le texte d'un élément** :
   ```html
   <button id="monBouton">Cliquez-moi</button>
   <p id="monTexte">Texte original</p>
   <script>
       document.getElementById('monBouton').addEventListener('click', function() {
           document.getElementById('monTexte').innerText = 'Texte modifié';
       });
   </script>
   ```
   **Explication** :
   - Un écouteur d'événements est ajouté au bouton pour réagir au clic.
   - Lorsque le bouton est cliqué, le texte de l'élément `<p>` est modifié en "Texte modifié".

2. **Ajouter une liste d'éléments** :
   ```html
   <button id="ajouter">Ajouter un élément</button>
   <ul id="maListe"></ul>
   <script>
       document.getElementById('ajouter').addEventListener('click', function() {
           const li = document.createElement('li');
           li.innerText = 'Nouvel élément';
           document.getElementById('maListe').appendChild(li);
       });
   </script>
   ```
   **Explication** :
   - Lorsque le bouton est cliqué, un nouvel élément `<li>` est créé.
   - Le texte "Nouvel élément" est ajouté à cet élément.
   - L'élément est ensuite ajouté à la liste `<ul>`.

3. **Changer la couleur d'un élément** :
   ```html
   <div id="monDiv" style="width: 200px; height: 200px; background-color: lightgray;">
       Survolez-moi
   </div>
   <script>
       const div = document.getElementById('monDiv');
       div.addEventListener('mouseover', function() {
           div.style.backgroundColor = 'lightblue';
       });
       div.addEventListener('mouseout', function() {
           div.style.backgroundColor = 'lightgray';
       });
   </script>
   ```
   **Explication** :
   - Deux écouteurs d'événements sont ajoutés : `mouseover` et `mouseout`.
   - Lorsqu'on survole le div, sa couleur de fond change en bleu clair.
   - Lorsqu'on sort du survol, la couleur de fond revient à gris clair.

4. **Compteur de clics** :
   ```html
   <button id="compteurBouton">Cliquez-moi</button>
   <p id="compteurTexte">Vous avez cliqué 0 fois</p>
   <script>
       let compteur = 0;
       document.getElementById('compteurBouton').addEventListener('click', function() {
           compteur++;
           document.getElementById('compteurTexte').innerText = `Vous avez cliqué ${compteur} fois`;
       });
   </script>
   ```
   **Explication** :
   - Une variable `compteur` est initialisée à 0.
   - Chaque fois que le bouton est cliqué, le compteur est incrémenté.
   - Le texte du paragraphe est mis à jour pour refléter le nombre de clics.

### Conclusion

Ces explications devraient vous permettre de mieux comprendre le fonctionnement de chaque solution. N'hésitez pas à expérimenter avec le code pour approfondir vos connaissances !