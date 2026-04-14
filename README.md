<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX 3.0</title>

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
  padding: 15px;
  font-size: 18px;
}

/* GRID */
.grid {
  display: flex;
  gap: 10px;
  overflow-x: auto;
  padding: 10px;
}

/* CARD (ПОСТЕРЫ) */
.card {
  min-width: 140px;
  height: 200px;
  border-radius: 12px;
  background-size: cover;
  background-position: center;
  position: relative;
  cursor: pointer;
  display: flex;
  align-items: flex-end;
  transition: 0.2s;
}

.card:active {
  transform: scale(0.97);
}

.card span {
  background: rgba(0,0,0,0.6);
  width: 100%;
  font-size: 12px;
  padding: 5px;
  text-align: center;
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
}
</style>
</head>

<body>

<header>
  <div class="logo">ANIFLEX 3.0</div>
  <input class="search" placeholder="Поиск..." oninput="searchAnime(this.value)">
</header>

<div class="hero">
🔥 Аниме как Netflix (версия 3.0)
</div>

<div class="grid" id="list"></div>

<div class="player" id="player">
  <iframe id="frame"></iframe>
  <button class="close" onclick="closePlayer()">Закрыть</button>
</div>

<script>

const anime = [
  {
    title: "Гяруко 1 серия",
    poster: "https://via.placeholder.com/300x400?text=Gyaruko+1",
    video: "https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239021"
  },
  {
    title: "Гяруко 2 серия",
    poster: "https://via.placeholder.com/300x400?text=Gyaruko+2",
    video: "https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239022"
  },
  {
    title: "Гяруко 3 серия",
    poster: "https://via.placeholder.com/300x400?text=Gyaruko+3",
    video: "https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239023"
  }
];

const list = document.getElementById("list");

function render(data){
  list.innerHTML = "";

  data.forEach(a => {
    const div = document.createElement("div");
    div.className = "card";
    div.style.backgroundImage = `url(${a.poster})`;

    div.innerHTML = `<span>${a.title}</span>`;

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
