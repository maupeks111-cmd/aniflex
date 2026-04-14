<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body {
  margin: 0;
  font-family: Arial;
  background: #141414;
  color: white;
}

header {
  display: flex;
  justify-content: space-between;
  padding: 15px 30px;
  background: black;
}

.logo {
  color: red;
  font-size: 24px;
  font-weight: bold;
}

.cards {
  display: flex;
  gap: 10px;
  padding: 20px;
  overflow-x: auto;
}

.card {
  min-width: 180px;
  background: #222;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
}

.card:hover {
  transform: scale(1.05);
}

.player {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.95);
  display: none;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

iframe {
  width: 90%;
  height: 80%;
}

button {
  margin-top: 10px;
  padding: 10px 20px;
  background: red;
  color: white;
  border: none;
}
</style>
</head>

<body>

<header>
  <div class="logo">ANIFLEX</div>
</header>

<h2 style="padding:20px;">Гяруко — серии</h2>

<div class="cards" id="list"></div>

<div class="player" id="player">
  <div id="frame"></div>
  <button onclick="closePlayer()">Закрыть</button>
</div>

<script>
const anime = [
  {
    title: "Гяруко 1 серия",
    video: "https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239021"
  },
  {
    title: "Гяруко 2 серия",
    video: "https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239022"
  }
];

const list = document.getElementById("list");

anime.forEach(a => {
  let div = document.createElement("div");
  div.className = "card";
  div.innerHTML = a.title;
  div.onclick = () => play(a.video);
  list.appendChild(div);
});

function play(url) {
  document.getElementById("player").style.display = "flex";
  document.getElementById("frame").innerHTML =
    `<iframe src="${url}" allowfullscreen></iframe>`;
}

function closePlayer() {
  document.getElementById("player").style.display = "none";
  document.getElementById("frame").innerHTML = "";
}
</script>

</body>
</html>
