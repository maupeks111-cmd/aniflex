<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>ANIFLEX</title>

<style>
* { box-sizing: border-box; }

:root {
    --bg: #05030b;
    --panel: rgba(12, 10, 24, .82);
    --text: #f8f7ff;
    --muted: #b9b4cc;
    --pink: #ff2bd6;
    --cyan: #00f5ff;
    --violet: #8b5cff;
    --green: #58ff9a;
}

html, body {
    margin: 0;
    padding: 0;
    min-height: 100%;
}

body {
    font-family: Arial, sans-serif;
    background: var(--bg);
    color: var(--text);
    overflow-x: hidden;
    position: relative;
}

body::before {
    content: "";
    position: fixed;
    inset: 0;
    background:
        radial-gradient(circle at 15% 20%, rgba(255, 43, 214, .20), transparent 30%),
        radial-gradient(circle at 85% 15%, rgba(0, 245, 255, .18), transparent 28%),
        radial-gradient(circle at 50% 100%, rgba(139, 92, 255, .20), transparent 38%),
        linear-gradient(rgba(5,3,11,.72), rgba(5,3,11,.92)),
        url("https://img.freepik.com/premium-photo/japanese-torii-gate-sunset-with-silhouetted-landscape_1282444-100316.jpg");
    background-size: cover;
    background-position: center;
    background-attachment: fixed;
    z-index: -2;
}

body::after {
    content: "";
    position: fixed;
    inset: 0;
    background-image:
        linear-gradient(rgba(0,245,255,.035) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,43,214,.035) 1px, transparent 1px);
    background-size: 35px 35px;
    pointer-events: none;
    z-index: -1;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 15px;
    padding: 14px 18px;
    margin: 0;
    background: rgba(7, 5, 16, .90);
    border-bottom: 1px solid rgba(0,245,255,.55);
    box-shadow: 0 0 25px rgba(0,245,255,.14), 0 0 45px rgba(255,43,214,.10);
    backdrop-filter: blur(14px);
    position: sticky;
    top: 0;
    z-index: 100;
}

.logo {
    font-weight: 900;
    font-family: monospace;
    color: #fff;
    letter-spacing: 4px;
    white-space: nowrap;
    text-shadow: 0 0 7px var(--cyan), 0 0 18px var(--cyan), 0 0 30px var(--pink);
}

.owner-phone {
    display: inline-flex;
    align-items: center;
    gap: 7px;
    padding: 7px 11px;
    border: 1px solid rgba(255,43,214,.75);
    border-radius: 12px;
    color: #fff;
    background: rgba(255,43,214,.08);
    box-shadow: inset 0 0 12px rgba(255,43,214,.08), 0 0 14px rgba(255,43,214,.18);
    font-size: 12px;
    white-space: nowrap;
}

.owner-phone a { color: var(--cyan); text-decoration: none; font-weight: 700; }

.search {
    padding: 11px 14px;
    border-radius: 13px;
    border: 1px solid rgba(0,245,255,.45);
    width: 40%;
    min-width: 120px;
    outline: none;
    font-size: 14px;
    color: white;
    background: rgba(0,0,0,.45);
    box-shadow: inset 0 0 12px rgba(0,245,255,.08), 0 0 10px rgba(0,245,255,.08);
}

.search::placeholder { color: #8e89a1; }
.search:focus { border-color: var(--cyan); box-shadow: 0 0 18px rgba(0,245,255,.22); }

.nav {
    display: flex;
    flex-wrap: wrap;
    gap: 9px;
    padding: 12px;
    justify-content: center;
}

.nav button, .btn {
    background: rgba(12,10,24,.84);
    color: white;
    border: 1px solid rgba(0,245,255,.45);
    padding: 9px 13px;
    border-radius: 11px;
    cursor: pointer;
    transition: .2s;
    box-shadow: 0 0 10px rgba(0,245,255,.08);
}

.nav button:hover, .btn:hover {
    border-color: var(--pink);
    background: rgba(255,43,214,.10);
    transform: translateY(-2px);
    box-shadow: 0 0 18px rgba(255,43,214,.25), 0 0 10px rgba(0,245,255,.15);
}

.nav a { text-decoration: none; }

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(175px, 1fr));
    gap: 18px;
    padding: 18px;
    max-width: 1500px;
    margin: auto;
}

.card {
    height: 260px;
    border-radius: 18px;
    background-size: cover;
    background-position: center;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition: transform .25s, box-shadow .25s, border-color .25s;
    border: 2px solid rgba(0,245,255,.72);
    box-shadow:
        0 0 0 1px rgba(255,43,214,.35),
        0 0 14px rgba(0,245,255,.28),
        0 0 30px rgba(255,43,214,.12);
}

.card:nth-child(3n) {
    border-color: rgba(255,43,214,.78);
    box-shadow:
        0 0 0 1px rgba(0,245,255,.30),
        0 0 14px rgba(255,43,214,.30),
        0 0 30px rgba(139,92,255,.16);
}

.card:nth-child(3n+1)::before,
.card:nth-child(3n+2)::before,
.card:nth-child(3n)::before {
    content: "";
    position: absolute;
    inset: 5px;
    border-radius: 13px;
    pointer-events: none;
    z-index: 2;
    border: 1px solid rgba(255,255,255,.18);
}

.card::after {
    content: "";
    position: absolute;
    inset: 0;
    background: linear-gradient(transparent 35%, rgba(3,2,9,.08) 48%, rgba(3,2,9,.94) 100%);
}

.card:hover {
    transform: translateY(-7px) scale(1.025);
    border-color: #fff;
    box-shadow:
        0 0 8px #fff,
        0 0 20px var(--cyan),
        0 0 38px var(--pink);
}

.title {
    position: absolute;
    bottom: 10px;
    left: 10px;
    right: 10px;
    background: rgba(4,3,10,.78);
    padding: 9px 11px;
    border-radius: 11px;
    font-size: 13px;
    z-index: 3;
    border-left: 3px solid var(--cyan);
    border-right: 3px solid var(--pink);
    backdrop-filter: blur(8px);
    box-shadow: 0 0 14px rgba(0,245,255,.13);
}

.page {
    display: none;
    padding: 18px;
    max-width: 900px;
    margin: auto;
}

.page h2 {
    margin: 12px 0 18px;
    text-shadow: 0 0 10px var(--pink), 0 0 22px var(--cyan);
}

.ep {
    background: linear-gradient(100deg, rgba(9,8,18,.94), rgba(22,10,30,.86));
    padding: 14px;
    margin: 9px 0;
    border-radius: 12px;
    cursor: pointer;
    transition: .2s;
    border: 1px solid rgba(0,245,255,.34);
    box-shadow: 0 0 12px rgba(0,245,255,.06);
}

.ep:hover:not(.lock) {
    border-color: var(--pink);
    background: rgba(255,43,214,.09);
    transform: translateX(5px);
    box-shadow: 0 0 18px rgba(255,43,214,.18), 0 0 12px rgba(0,245,255,.10);
}

.lock {
    opacity: .45;
    cursor: not-allowed;
}

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

.empty {
    text-align: center;
    padding: 50px 10px;
    color: var(--muted);
}

.footer {
    text-align: center;
    padding: 25px 15px 35px;
    color: #9e99b0;
    font-size: 12px;
}

.footer strong {
    color: var(--cyan);
    text-shadow: 0 0 8px var(--cyan);
}

@media (max-width: 600px) {
    header {
        flex-direction: column;
        align-items: stretch;
    }
    .logo { text-align: center; }
    .owner-phone { justify-content: center; }
    .search { width: 100%; }
    .grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 10px;
        padding: 10px;
    }
    .card { height: 225px; }
}
</style>
</head>

<body>

<header>

    <div class="logo">
        ANIFLEX
    </div>

    <div class="owner-phone">
        👤 Владелец:
        <a href="tel:+79233500539">8 923 350-05-39</a>
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

    <a href="https://www.donationalerts.com/r/LaunchPlay"
       target="_blank"
       rel="noopener">
        <button type="button">💰 Донат</button>
    </a>

</div>

<!-- Главная -->
<div style="text-align:center;padding:8px 15px 0;color:#b9b4cc;font-size:12px;letter-spacing:1px;">
    ✦ ANIFLEX NEON · твоя аниме-озвучка ✦
</div>
<div id="home" class="grid"></div>

<!-- Страница аниме -->
<div id="page" class="page"></div>

<div class="footer">
    <strong>ANIFLEX</strong> · Аниме с неоновым настроением · Владелец:
    <a href="tel:+79233500539" style="color:#00f5ff;text-decoration:none;">8 923 350-05-39</a>
</div>


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

            { t: "2 серия",
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

            { t: "2 серия (скоро)",
             v: "" 
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
              v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=4_%D1%81%D0%B5%D1%80%D0%B8%D1%8F_wrehoz" 
            },
            { 
                t: "5 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=5%D1%81_%D0%BA%D0%BE%D1%82_r3dack" 
            },
            { t: "6 серия",
             v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=6%D1%81_%D0%BA%D0%BE%D1%82_x1fjrt" 
            },
            { t: "7 серия (скоро)", v: "" },
            { t: "8 серия (скоро)", v: "" },
            { t: "9 серия (скоро)", v: "" },
            { t: "10 серия (скоро)", v: "" },
            { t: "11 серия (скоро)", v: "" },
            { t: "12 серия (скоро)", v: "" },
            { t: "13 серия (скоро)", v: "" },
            { t: "14 серия (скоро)", v: "" },
            { t: "15 серия (скоро)", v: "" },
            { t: "16 серия (скоро)", v: "" },
            { t: "17 серия (скоро)", v: "" },
            { t: "18 серия (скоро)", v: "" },
            { t: "19 серия (скоро)", v: "" },
            { t: "20 серия (скоро)", v: "" },
            { t: "21 серия (скоро)", v: "" },
            { t: "22 серия (скоро)", v: "" },
            { t: "23 серия (скоро)", v: "" },
            { t: "24 серия (скоро)", v: "" },
            { t: "25 серия (скоро)", v: "" },
            { t: "26 серия (скоро)", v: "" },
            { t: "27 серия (скоро)", v: "" },
            { t: "28 серия (скоро)", v: "" },
            { t: "29 серия (скоро)", v: "" },
            { t: "30 серия (скоро)", v: "" }

        ]
    }

];


/* ==========================================
   ЭЛЕМЕНТЫ
========================================== */

const home = document.getElementById("home");
const page = document.getElementById("page");
const player = document.getElementById("player");

const video = document.getElementById("video");
const iframe = document.getElementById("iframePlayer");

const searchInput = document.getElementById("searchInput");


/* ==========================================
   ГЛАВНАЯ
========================================== */

function render(list) {

    home.innerHTML = "";

    if (list.length === 0) {

        home.innerHTML = `
            <div class="empty">
                Ничего не найдено 😔
            </div>
        `;

        return;
    }

    list.forEach(item => {

        const index = data.indexOf(item);

        const card = document.createElement("div");

        card.className = "card";

        card.style.backgroundImage =
            `url("${item.poster}")`;

        card.innerHTML = `
            <div class="title">
                ${escapeHTML(item.title)}
            </div>
        `;

        card.addEventListener("click", () => {
            openAnime(index);
        });

        home.appendChild(card);
    });
}


/* ==========================================
   ОТКРЫТЬ АНИМЕ
========================================== */

function openAnime(index) {

    const anime = data[index];

    if (!anime) return;

    home.style.display = "none";
    page.style.display = "block";

    let html = `
        <button
            class="btn"
            type="button"
            onclick="showAll()">
            ⬅ Назад
        </button>

        <h2>${escapeHTML(anime.title)}</h2>
    `;

    anime.episodes.forEach((episode, episodeIndex) => {

        const available = Boolean(episode.v);

        html += `
            <div
                class="ep ${available ? "" : "lock"}"
                ${available
                    ? `onclick="playEpisode(${index}, ${episodeIndex})"`
                    : ""}
            >
                ${escapeHTML(episode.t)}
            </div>
        `;
    });

    page.innerHTML = html;

    window.scrollTo({
        top: 0,
        behavior: "smooth"
    });
}


/* ==========================================
   ЗАПУСК СЕРИИ
========================================== */

function playEpisode(animeIndex, episodeIndex) {

    const anime = data[animeIndex];

    if (!anime) return;

    const episode = anime.episodes[episodeIndex];

    if (!episode || !episode.v) {
        return;
    }

    const url = episode.v;

    /* Открываем плеер */
    player.style.display = "flex";

    /* Останавливаем всё старое */
    video.pause();
    video.removeAttribute("src");

    iframe.removeAttribute("src");

    video.style.display = "none";
    iframe.style.display = "none";


    /*
       Cloudinary Embed
    */

    if (url.includes("player.cloudinary.com/embed")) {

        iframe.src = url;
        iframe.style.display = "block";

        return;
    }


    /*
       Обычное видео MP4
    */

    video.src = url;
    video.style.display = "block";

    video.load();

    const playPromise = video.play();

    if (playPromise !== undefined) {

        playPromise.catch(() => {
            /*
             Браузер может запретить
             автоматический запуск.
             Пользователь просто нажмёт Play.
            */
        });
    }
}


/* ==========================================
   ЗАКРЫТЬ ПЛЕЕР
========================================== */

function closePlayer() {

    player.style.display = "none";

    /* Останавливаем MP4 */
    video.pause();
    video.removeAttribute("src");
    video.load();

    /* Останавливаем iframe */
    iframe.removeAttribute("src");

    video.style.display = "none";
    iframe.style.display = "none";
}


/* ==========================================
   ГЛАВНАЯ
========================================== */

function showAll() {

    closePlayer();

    page.style.display = "none";
    home.style.display = "grid";

    render(data);

    searchInput.value = "";

    window.scrollTo({
        top: 0,
        behavior: "smooth"
    });
}


/* ==========================================
   ПОИСК
========================================== */

function search(text) {

    const query = text
        .trim()
        .toLowerCase();

    page.style.display = "none";
    home.style.display = "grid";

    if (!query) {

        render(data);

        return;
    }

    const result = data.filter(anime =>
        anime.title
            .toLowerCase()
            .includes(query)
    );

    render(result);
}


/* ==========================================
   ЗАЩИТА ТЕКСТА
========================================== */

function escapeHTML(text) {

    return String(text)
        .replaceAll("&", "&amp;")
        .replaceAll("<", "&lt;")
        .replaceAll(">", "&gt;")
        .replaceAll('"', "&quot;")
        .replaceAll("'", "&#039;");
}


/* ==========================================
   ОБРАБОТЧИК ПОИСКА
========================================== */

searchInput.addEventListener("input", function () {

    search(this.value);

});


/* ==========================================
   ESC — ЗАКРЫТЬ ПЛЕЕР
========================================== */

document.addEventListener("keydown", function(event) {

    if (event.key === "Escape") {
        closePlayer();
    }

});


/* ==========================================
   ЗАПУСК
========================================== */

render(data);

</script>

</body>
</html>
