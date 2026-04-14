<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>ANIFLEX</title>

<style>
  * {
    box-sizing: border-box;
  }

  body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #141414;
    color: white;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px;
    background: #000;
  }

  .logo {
    color: red;
    font-size: 20px;
    font-weight: bold;
  }

  .search {
    width: 50%;
    padding: 8px;
    border-radius: 6px;
    border: none;
  }

  .banner {
    padding: 20px;
    text-align: center;
    font-size: 22px;
  }

  .row {
    padding: 10px;
  }

  .cards {
    display: flex;
    gap: 10px;
    overflow-x: auto;
    padding-bottom: 10px;
  }

  .card {
    min-width: 160px;
    background: #222;
    border-radius: 10px;
    padding: 10px;
    cursor: pointer;
  }

  .card:active {
    transform: scale(0.98);
  }

  /* ПЛЕЕР */
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

  /* адаптация */
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

<div class="banner">
  🔥 Смотри аниме бесплатно
</div>

<div class="row">
  <h3>Гяруко — серии</h3>
  <div class="cards" id="list"></div>
</div>

<div class="player" id="player">
  <iframe id="frame"></iframe>
  <button class="close" onclick="closePlayer()">Закрыть</button>
</div>

<script>
const anime = [
  {
    title: "Гяруко - 1 серия",
    video: "https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239021"
  },
  {
    title: "Гяруко - 2 серия",
    video: "https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239022"
  }
];

const list = document.getElementById("list");

function render(data){
  list.innerHTML = "";

  data.forEach(item => {
    const div = document.createElement("div");
    div.className = "card";
    div.innerHTML = item.title;

    div.onclick = () => play(item.video);

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
