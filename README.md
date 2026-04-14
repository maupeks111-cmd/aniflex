<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #0b0b0b;
  color: white;
}

/* HEADER */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px;
  background: #000;
}

.logo {
  color: red;
  font-size: 22px;
  font-weight: bold;
}

.search {
  width: 45%;
  padding: 8px;
  border-radius: 6px;
  border: none;
}

/* TITLE */
.hero {
  padding: 20px;
  font-size: 20px;
}

/* CARDS */
.cards {
  display: flex;
  gap: 10px;
  overflow-x: auto;
  padding: 10px;
}

.card {
  min-width: 150px;
  height: 160px;
  background: #222;
  border-radius: 12px;
  padding: 10px;
  cursor: pointer;
  display: flex;
  align-items: flex-end;
}

.card:active {
  transform: scale(0.97);
}

/* PLAYER */
.player {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.95);
  display: none;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.player iframe {
  width: 95%;
  height: 75%;
  border: none;
}

.close {
  margin-top: 10px;
  padding: 10px 20px;
  background: red;
  border: none;
  color: white;
  cursor: pointer;
}
</style>
</head>

<body>

<header>
  <div class="logo">ANIFLEX</div>
  <input class="search" placeholder="Поиск..." oninput="searchAnime(this.value)">
</header>

<div class="hero">
🔥 Смотри аниме как Netflix
</div>

<div class="cards" id="list"></div>

<div class="player" id="player">
  <iframe id="frame"></iframe>
  <button class="close" onclick="closePlayer()">Закрыть</button>
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
  },
  {
    title: "Гяруко 3 серия",
    video: "https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239023"
  }
];

const list = document.getElementById("list");

function render(data){
  list.innerHTML = "";

  data.forEach(a => {
    const card = document.createElement("div");
    card.className = "card";
    card.textContent = a.title;

    card.onclick = () => play(a.video);

    list.appendChild(card);
  });
}

function play(url){
  const frame = document.getElementById("frame");
  frame.src = url;
  document.getElementById("player").style.display = "flex";
}

function closePlayer(){
  const frame = document.getElementById("frame");
  frame.src = "";
  document.getElementById("player").style.display = "none";
}

function searchAnime(text){
  const filtered = anime.filter(a =>
    a.title.toLowerCase().includes(text.toLowerCase())
  );
  render(filtered);
}

render(anime);

</script>

</body>
</html>
