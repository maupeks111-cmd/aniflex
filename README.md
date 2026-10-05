<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>ANIFLEX</title>

<style>
* {
    box-sizing: border-box;
}

html,
body {
    margin: 0;
    padding: 0;
    min-height: 100%;
}

body {
    font-family: Arial, sans-serif;
    background: #111;
    color: white;
    overflow-x: hidden;
}

/* Фон */
body::before {
    content: "";
    position: fixed;
    inset: 0;
    background-image: url("https://img.freepik.com/premium-photo/japanese-torii-gate-sunset-with-silhouetted-landscape_1282444-100316.jpg");
    background-size: cover;
    background-position: center;
    background-attachment: fixed;
    z-index: -2;
}

body::after {
    content: "";
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.65);
    z-index: -1;
}

/* Шапка */
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 15px;
    padding: 12px 15px;
    background: rgba(255, 255, 255, 0.96);
    border-radius: 0 0 20px 20px;
    position: sticky;
    top: 0;
    z-index: 100;
}

.logo {
    font-weight: bold;
    font-family: monospace;
    color: #000;
    letter-spacing: 3px;
    white-space: nowrap;
}

.search {
    padding: 10px 12px;
    border-radius: 10px;
    border: none;
    width: 40%;
    min-width: 120px;
    outline: none;
    font-size: 14px;
}

/* Навигация */
.nav {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    padding: 10px;
}

.nav button {
    background: #222;
    color: white;
    border: none;
    padding: 9px 13px;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.2s;
}

.nav button:hover {
    background: #444;
    transform: translateY(-1px);
}

.nav a {
    text-decoration: none;
}

/* Карточки */
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 12px;
    padding: 10px;
}

.card {
    height: 240px;
    border-radius: 16px;
    background-size: cover;
    background-position: center;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition: transform 0.25s, box-shadow 0.25s;
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
}

.card:hover {
    transform: scale(1.04);
    box-shadow: 0 12px 30px rgba(0, 0, 0, 0.7);
}

.card::after {
    content: "";
    position: absolute;
    inset: 0;
    background: linear-gradient(
        transparent 45%,
        rgba(0, 0, 0, 0.8)
    );
}

.title {
    position: absolute;
    bottom: 10px;
    left: 10px;
    right: 10px;
    background: rgba(0, 0, 0, 0.75);
    padding: 7px 10px;
    border-radius: 10px;
    font-size: 13px;
    z-index: 2;
}

.page {
    display: none;
    padding: 10px;
}

.page h2 {
    margin-top: 10px;
}

/* Серии */
.ep {
    background: rgba(28, 28, 28, 0.95);
    padding: 12px;
    margin: 7px 0;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.2s;
}

.ep:hover:not(.lock) {
    background: #333;
    transform: translateX(3px);
}

.lock {
    opacity: 0.45;
    cursor: not-allowed;
}

/* Кнопки */
.btn {
    padding: 9px 13px;
    margin: 5px 0;
    background: #222;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
}

.btn:hover {
    background: #444;
}

/* Плеер */
.player {
    position: fixed;
    inset: 0;
    background: #000;
    display: none;
    flex-direction: column;
    z-index: 9999;
}

.player-top {
    position: absolute;
    top: 10px;
    left: 10px;
    z-index: 10;
}

#video {
    width: 100%;
    height: 100%;
    object-fit: contain;
    background: #000;
}

#iframePlayer {
    width: 100%;
    height: 100%;
    border: none;
    background: #000;
}

/* Сообщение */
.empty {
    text-align: center;
    padding: 40px 10px;
    color: #bbb;
}

/* Телефон */
@media (max-width: 600px) {

    header {
        flex-direction: column;
        align-items: stretch;
    }

    .logo {
        text-align: center;
    }

    .search {
        width: 100%;
    }

    .grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 8px;
    }

    .card {
        height: 220px;
    }
}
</style>
</head>

<body>

<header>

    <div class="logo">
        ANIFLEX
    </div>

    <input
        id="searchInput"
        class="search"
        type="search"
        placeholder="Поиск..."
        autocomplete="off"
    >

</header>

<div class="nav">

    <button type="button" onclick="showAll()">
        🏠 Главная
    </button>

    <a href="https://vk.com/aniflex1" target="_blank" rel="noopener">
        <button type="button">VK</button>
    </a>

    <a href="https://t.me/Animeflex1x" target="_blank" rel="noopener">
        <button type="button">TG</button>
    </a>

    <a
        href="https://www.donationalerts.com/r/LaunchPlay"
        target="_blank"
        rel="noopener"
    >
        <button type="button">💰 Донат</button>
    </a>

</div>

<!-- Главная -->
<div id="home" class="grid"></div>

<!-- Страница аниме -->
<div id="page" class="page"></div>

<!-- Плеер -->
<div id="player" class="player">

    <div class="player-top">
        <button class="btn" type="button" onclick="closePlayer()">
            ⬅ Назад
        </button>
    </div>

    <video
        id="video"
        controls
        playsinline
        preload="metadata">
    </video>

    <iframe
        id="iframePlayer"
        style="display:none;"
        allow="autoplay; fullscreen; picture-in-picture"
        allowfullscreen>
    </iframe>

</div>

<script>

/* ==========================================
   ДАННЫЕ
========================================== */

const data = [

    {
        title: "Клинок рассекающих демонов",

        poster:
        "https://i.pinimg.com/originals/95/cf/8d/95cf8d3c3a0e41844941259f4247dc6f.jpg",

        episodes: Array.from(
            { length: 26 },
            (_, i) => ({
                t: `${i + 1} серия (скоро)`,
                v: ""
            })
        )
    },

    {
        title: "Гяруко",

        poster:
        "https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_.jpg",

        episodes: [

            {
                t: "1 серия",
                v: "https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/1_серия_Расскажи_нам_Гяруко_is6ti6.mp4"
            },

            {
                t: "2 серия",
                v: "https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254679/2_серия_Расскажи_нам_Гяруко_eroylf.mp4"
            },

            {
                t: "3 серия",
                v: "https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254741/3_серия_Расскажи_нам_Гяруко_ibivet.mp4"
            },

            {
                t: "4 серия",
                v: "https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254759/4_серия_Расскажи_нам_Гяруко_qzigwl.mp4"
            },

            {
                t: "5 серия",
                v: "https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254740/5_серия_Расскажи_нам_Гяруко_crtolw.mp4"
            },

            {
                t: "6 серия",
                v: "https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254747/6_серия_Расскажи_нам_Гяруко_jhnztd.mp4"
            },

            {
                t: "7 серия",
                v: "https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254735/7_серия_Расскажи_нам_Гяруко_qhbmlj.mp4"
            },

            {
                t: "8 серия",
                v: "https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254751/8_серия_Расскажи_нам_Гяруко_wsdrnn.mp4"
            },

            {
                t: "9 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=9_dxhyvm"
            },

            {
                t: "10 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=12_ud4aum"
            },

            {
                t: "11 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=11_px4jiv"
            },

            {
                t: "12 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=10_neqyxr"
            }

        ]
    },

    {
        title: "Фарфоровая кукла",

        poster:
        "https://basket-29.wbbasket.ru/vol5784/part578411/578411360/images/big/1.webp",

        episodes: [

            {
                t: "1 серия",
                v: "https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/VID_20260416_110510_423_o8ndmt.mp4"
            },

            {
                t: "2 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=20393775401637-compressed_e1ixjv"
            },

            { t: "3 серия (скоро)", v: "" },
            { t: "4 серия (скоро)", v: "" },
            { t: "5 серия (скоро)", v: "" },
            { t: "6 серия (скоро)", v: "" },
            { t: "7 серия (скоро)", v: "" },
            { t: "8 серия (скоро)", v: "" },
            { t: "9 серия (скоро)", v: "" },
            { t: "10 серия (скоро)", v: "" },
            { t: "11 серия (скоро)", v: "" },
            { t: "12 серия (скоро)", v: "" }

        ]
    },

    {
        title: "Сенко-сан",

        poster:
        "https://i.pinimg.com/736x/64/97/89/649789acb22b072a7fb783ca173d6408.jpg",

        episodes: [

            {
                t: "1 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=%D1%81%D0%B5%D0%BD%D0%BA%D0%BE_1_%D1%81%D0%B5%D1%80%D0%B8%D1%8F_isvv4w"
            },

            { t: "2 серия (скоро)", v: "" },
            { t: "3 серия (скоро)", v: "" },
            { t: "4 серия (скоро)", v: "" },
            { t: "5 серия (скоро)", v: "" },
            { t: "6 серия (скоро)", v: "" },
            { t: "7 серия (скоро)", v: "" },
            { t: "8 серия (скоро)", v: "" },
            { t: "9 серия (скоро)", v: "" },
            { t: "10 серия (скоро)", v: "" },
            { t: "11 серия (скоро)", v: "" },
            { t: "12 серия (скоро)", v: "" }

        ]

    },

    {
        title: "Форма голоса",

        poster:
        "https://i.pinimg.com/originals/7f/0d/27/7f0d27d155877e62b2be68952401f329.jpg",

        episodes: [
            {
                t: "Фильм (скоро)",
                v: ""
            }
        ]
    },

    {
        title: "Вечера с кошкой",

        poster:
        "https://static.kinoafisha.info/k/series_posters/480/upload/series/posters/4/7/4/13474/338468001759996357.jpg",

        episodes: [

            {
                t: "1 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=17869717768793_pusgyk"
            },

            {
                t: "2 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=16553542945455_hpd1zn"
            },

            {
                t: "3 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=17027855223413_ormpod"
            },

            {
                t: "4 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id
