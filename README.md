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
      background: #141414;
      color: white;
    }

    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 15px 30px;
      background: #000;
    }

    .logo {
      color: red;
      font-size: 24px;
      font-weight: bold;
    }

    .search {
      padding: 5px;
      border-radius: 5px;
      border: none;
    }

    .banner {
      height: 300px;
      background: url('https://via.placeholder.com/1200x300') center/cover;
      display: flex;
      align-items: center;
      padding: 20px;
    }

    .banner h1 {
      font-size: 40px;
    }

    .row {
      padding: 20px;
    }

    .row h2 {
      margin-bottom: 10px;
    }

    .cards {
      display: flex;
      gap: 10px;
      overflow-x: auto;
    }

    .card {
      min-width: 150px;
      background: #222;
      border-radius: 10px;
      padding: 10px;
      cursor: pointer;
      transition: 0.3s;
    }

    .card:hover {
      transform: scale(1.05);
    }

    .player {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.9);
      display: none;
      justify-content: center;
      align-items: center;
      flex-direction: column;
    }

    video {
      width: 80%;
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

<div class="banner">
  <h1>Смотри аниме бесплатно 🔥</h1>
</div>

<div class="row">
  <h2>Популярное</h2>
  <div class="cards" id="animeList"></div>
</div>

<div class="player" id="player">
  <video controls id="videoPlayer"></video>
  <button class="close" onclick="closePlayer()">Закрыть</button>
</div>

<script>
  const anime = [
    { title: "Гяруко 1 серия", video: "https://vkvideo.ru/video-229445104_456239021?list=ln-synXZZvTuZOD2Kzh9y" },
    { title: "Demo Anime 2", video: "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8" },
    { title: "Demo Anime 3", video: "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8" }
  ];

  const list = document.getElementById("animeList");

  function render(data) {
    list.innerHTML = "";
    data.forEach(a => {
      const card = document.createElement("div");
      card.className = "card";
      card.innerHTML = `<p>${a.title}</p>`;
      card.onclick = () => play(a.video);
      list.appendChild(card);
    });
  }

  function play(url) {
    const player = document.getElementById("player");
    const video = document.getElementById("videoPlayer");

    video.src = url;
    player.style.display = "flex";
  }

  function closePlayer() {
    const player = document.getElementById("player");
    const video = document.getElementById("videoPlayer");

    video.pause();
    player.style.display = "none";
  }

  function searchAnime(text) {
    const filtered = anime.filter(a => a.title.toLowerCase().includes(text.toLowerCase()));
    render(filtered);
  }

  render(anime);
</script>

</body>
</html>
