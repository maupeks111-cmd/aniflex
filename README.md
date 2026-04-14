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

    .cards {
      display: flex;
      gap: 10px;
      overflow-x: auto;
    }

    .card {
      min-width: 180px;
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
      background: rgba(0,0,0,0.95);
      display: none;
      justify-content: center;
      align-items: center;
      flex-direction: column;
    }

    #videoPlayer {
      width: 90%;
      height: 80%;
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
  <h2>Гяруко — серии</h2>
  <div class="cards" id="animeList"></div>
</div>

<div class="player" id="player">
  <div id="videoPlayer"></div>
  <button class="close" onclick="closePlayer()">Закрыть</button>
</div>

<script>
  const anime = [
    {
      title: "Гяруко - 1 серия",
      video: "https://drive.google.com/file/d/1KbOa3HH80a5lkAI7tB35ZPIPQ8c7BTAs/view?usp=sharing"
    },
    {
      title: "Гяруко - 2 серия",
      video: "https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239022"
    }
  ];

  const list = document.getElementById("animeList");

  function render
