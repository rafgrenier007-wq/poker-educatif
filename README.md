# poker-educatif
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Poker Éducatif</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<h1>♠️ Poker Éducatif</h1>
<p>Site 100 % éducatif – aucun jeu d'argent</p>

<a href="simulateur.html">👉 Accéder au simulateur</a>






</body>
</html>
const cartes = [
  "2♠","3♠","4♠","5♠","6♠","7♠","8♠","9♠","10♠","J♠","Q♠","K♠","A♠",
  "2♥","3♥","4♥","5♥","6♥","7♥","8♥","9♥","10♥","J♥","Q♥","K♥","A♥",
  "2♦","3♦","4♦","5♦","6♦","7♦","8♦","9♦","10♦","J♦","Q♦","K♦","A♦",
  "2♣","3♣","4♣","5♣","6♣","7♣","8♣","9♣","10♣","J♣","Q♣","K♣","A♣"
];

function distribuer() {
  let deck = [...cartes].sort(() => Math.random() - 0.5);

  let main = deck.slice(0, 2);
  let board = deck.slice(2, 7);
  let toutesCartes = main.concat(board);

  document.getElementById("main").innerText = main.join(" ");
  document.getElementById("board").innerText = board.join(" ");

  let resultat = analyserMain(toutesCartes);
  document.getElementById("resultat").innerText = resultat;
}

// Analyse simple des paires / brelans / carrés
function analyserMain(cartes) {
  let valeurs = cartes.map(c => c.slice(0, -1));
  let compteur = {};

  valeurs.forEach(v => compteur[v] = (compteur[v] || 0) + 1);

  let occurrences = Object.values(compteur);

  if (occurrences.includes(4)) return "Carré";
  if (occurrences.includes(3) && occurrences.includes(2)) return "Full";
  if (occurrences.includes(3)) return "Brelan";
  if (occurrences.filter(v => v === 2).length === 2) return "Double paire";
  if (occurrences.includes(2)) return "Paire";

  return "Carte haute";
}

<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Simulateur de Poker</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<h2>🎮 Simulateur de main</h2>

<button onclick="distribuer()">Distribuer une main</button>

<h3>Ta main :</h3>
<p id="main"></p>

<h3>Board :</h3>
<p id="board"></p>

<script src="script.js"></script>
</body>
</html>

