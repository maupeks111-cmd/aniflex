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

/* TOP BAR */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  background: #000;
  position: sticky;
  top: 0;
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

/* HERO */
.hero {
  padding: 20px;
  font-size: 22px;
  font-weight: bold;
}

/* ROW */
.row {
  padding: 10px 16px;
}

.row h3 {
  margin-bottom: 10px;
}

/* CARDS */
.cards {
  display: flex;
  gap: 10px;
  overflow-x: auto;
  padding-bottom: 10px;
}

.card {
  min-width: 140px;
  height: 180px;
  background: #222;
  border-radius: 12px;
  display: flex;
  align-items: flex-end;
  padding: 10px;
  cursor: pointer;
  position: relative;
  transition: 0.2s;
}

.card:active {
  transform: scale(0.97);
}

.card-title {
  font-size: 13px;
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
  height: 70%;
  border: none;
}

.close {
  margin-top: 10px;
  padding: 10px 20px;
  background: red;
  border: none;
  color: white;
}

/* MOBILE */
@media (max-width: 600px) {
  .search {
    width: 40%;
  }
}
</style>
</head>

<body>

<header>
  <div class="logo">ANIFLEX</div>
  <input class="search" placeholder="Поиск..." oninput="searchAnime(this.value)">
</header>

<div class="hero">
🔥 Смотри аниме как в Netflix
</div>

<div class="row">
  <h3>Гяруко</h3>
  <div class="cards" id="list"></div>
</div>

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
    const div = document.createElement("div");
    div.className = "card";

    div.innerHTML = `<div class="card-title">${a.title}</div>`;

    div.onclick = () => play(a.video);

    list.appendChild(div);
  });
}

function play(url){
  document.getElementById("frame").src = url;
  document.getElementById("player").style.display = "flex";
}

function closePlayer(){
  document.getElementById("frame").src = "";
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
