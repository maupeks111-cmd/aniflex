<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>ANIFLEX — EDWIN</title>

<style>
* {
    box-sizing: border-box;
}

:root {
    --bg: #05030b;
    --panel: rgba(9, 6, 20, .88);
    --cyan: #00f5ff;
    --pink: #ff2bd6;
    --purple: #9b5cff;
    --green: #4dff9b;
    --orange: #ffb84d;
    --red: #ff4f81;
    --white: #ffffff;
    --muted: #aaa4c0;
}

html,
body {
    margin: 0;
    padding: 0;
    min-height: 100%;
}

body {
    font-family: Arial, sans-serif;
    color: var(--white);
    background: var(--bg);
    overflow-x: hidden;
}

/* =====================================================
   АНИМЕШНЫЙ НЕОНОВЫЙ ФОН
===================================================== */

body::before {
    content: "";
    position: fixed;
    inset: 0;
    z-index: -3;

    background:
        linear-gradient(
            rgba(3, 1, 12, .40),
            rgba(3, 1, 12, .88)
        ),
        url("https://images.unsplash.com/photo-1578632767115-351597cf2477?auto=format&fit=crop&w=2200&q=85");

    background-size: cover;
    background-position: center;
    background-attachment: fixed;
}

body::after {
    content: "";
    position: fixed;
    inset: 0;
    z-index: -2;
    pointer-events: none;

    background:
        radial-gradient(
            circle at 10% 15%,
            rgba(0,245,255,.18),
            transparent 27%
        ),

        radial-gradient(
            circle at 90% 20%,
            rgba(255,43,214,.18),
            transparent 28%
        ),

        radial-gradient(
            circle at 50% 100%,
            rgba(155,92,255,.18),
            transparent 35%
        ),

        linear-gradient(
            rgba(0,245,255,.025) 1px,
            transparent 1px
        ),

        linear-gradient(
            90deg,
            rgba(255,43,214,.025) 1px,
            transparent 1px
        );

    background-size:
        auto,
        auto,
        auto,
        38px 38px,
        38px 38px;
}

/* =====================================================
   ШАПКА
===================================================== */

header {
    position: sticky;
    top: 0;
    z-index: 100;

    display: flex;
    align-items: center;
    gap: 15px;

    padding: 13px 18px;

    background: rgba(5,3,13,.92);
    backdrop-filter: blur(18px);

    border-bottom: 1px solid rgba(0,245,255,.55);

    box-shadow:
        0 0 25px rgba(0,245,255,.14),
        0 0 45px rgba(255,43,214,.08);
}

.logo {
    font-family: monospace;
    font-size: 24px;
    font-weight: 900;

    letter-spacing: 4px;
    white-space: nowrap;

    text-shadow:
        0 0 7px var(--cyan),
        0 0 18px var(--cyan),
        0 0 30px var(--pink);
}

.search {
    flex: 1;
    max-width: 520px;

    padding: 11px 14px;

    color: white;
    background: rgba(0,0,0,.45);

    border:
        1px solid rgba(0,245,255,.45);

    border-radius: 13px;

    outline: none;
}

.search:focus {
    border-color: var(--cyan);

    box-shadow:
        0 0 15px rgba(0,245,255,.25);
}

.owner-mini {
    font-size: 11px;
    color: var(--muted);
    text-align: right;
    white-space: nowrap;
}

.owner-mini strong {
    color: white;
}

.owner-mini a {
    color: var(--cyan);
    text-decoration: none;
    font-weight: bold;
}

/* =====================================================
   НАВИГАЦИЯ
===================================================== */

.nav {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;

    gap: 9px;
    padding: 13px;
}

.nav a {
    text-decoration: none;
}

.nav button,
.btn {
    padding: 10px 14px;

    color: white;
    background: rgba(10,7,24,.90);

    border:
        1px solid rgba(0,245,255,.42);

    border-radius: 12px;

    cursor: pointer;

    font-weight: 700;

    transition: .2s;

    box-shadow:
        0 0 12px rgba(0,245,255,.07);
}

.nav button:hover,
.btn:hover {
    transform: translateY(-2px);

    border-color: var(--pink);

    box-shadow:
        0 0 18px rgba(255,43,214,.25),
        0 0 12px rgba(0,245,255,.15);
}

/* =====================================================
   ЗАГОЛОВОК
===================================================== */

.section-label {
    text-align: center;

    padding: 5px 15px 0;

    color: #c8c2d9;

    font-size: 12px;
    letter-spacing: 2px;
}

/* =====================================================
   КАРТОЧКИ АНИМЕ
===================================================== */

.grid {
    display: grid;

    grid-template-columns:
        repeat(
            auto-fit,
            minmax(175px, 1fr)
        );

    gap: 18px;

    padding: 18px;

    max-width: 1500px;

    margin: auto;
}

.card {
    position: relative;

    height: 265px;

    overflow: hidden;

    cursor: pointer;

    border-radius: 19px;

    background-size: cover;
    background-position: center;

    border: 2px solid rgba(0,245,255,.70);

    box-shadow:
        0 0 0 1px rgba(255,43,214,.25),
        0 0 18px rgba(0,245,255,.20);

    transition:
        transform .25s,
        box-shadow .25s,
        border-color .25s;
}

/* разные рамки */

.card:nth-child(3n) {
    border-color: rgba(255,43,214,.80);
}

.card:nth-child(3n + 2) {
    border-color: rgba(155,92,255,.85);
}

.card::before {
    content: "";

    position: absolute;
    inset: 5px;

    border:
        1px solid rgba(255,255,255,.18);

    border-radius: 14px;

    z-index: 2;
}

.card::after {
    content: "";

    position: absolute;
    inset: 0;

    background:
        linear-gradient(
            transparent 30%,
            rgba(2,1,8,.95) 100%
        );
}

.card:hover {
    transform:
        translateY(-7px)
        scale(1.025);

    border-color: white;

    box-shadow:
        0 0 8px white,
        0 0 22px var(--cyan),
        0 0 42px var(--pink);
}

.title {
    position: absolute;

    left: 10px;
    right: 10px;
    bottom: 10px;

    z-index: 3;

    padding: 9px 11px;

    background: rgba(4,2,12,.80);

    border-radius: 11px;

    border-left:
        3px solid var(--cyan);

    border-right:
        3px solid var(--pink);

    backdrop-filter: blur(8px);

    font-size: 13px;
}

/* =====================================================
   СТРАНИЦЫ
===================================================== */

.page {
    display: none;

    max-width: 1000px;

    margin: auto;

    padding: 18px;
}

.page h2 {
    text-align: center;

    text-shadow:
        0 0 10px var(--pink),
        0 0 22px var(--cyan);
}

.panel {
    padding: 20px;

    background:
        rgba(7,5,17,.88);

    border:
        1px solid rgba(0,245,255,.25);

    border-radius: 18px;

    box-shadow:
        0 0 28px rgba(0,0,0,.35);

    backdrop-filter: blur(12px);
}

/* =====================================================
   СЕРИИ
===================================================== */

.ep {
    margin: 9px 0;

    padding: 14px;

    background:
        linear-gradient(
            100deg,
            rgba(9,7,20,.94),
            rgba(23,8,34,.90)
        );

    border:
        1px solid rgba(0,245,255,.32);

    border-radius: 12px;

    cursor: pointer;

    transition: .2s;
}

.ep:hover:not(.lock) {
    transform: translateX(5px);

    border-color:
        var(--pink);

    box-shadow:
        0 0 18px
        rgba(255,43,214,.18);
}

.lock {
    opacity: .45;
    cursor: not-allowed;
}

/* =====================================================
   КОМАНДА
===================================================== */

.team-grid {
    display: grid;

    grid-template-columns:
        repeat(
            auto-fit,
            minmax(220px,1fr)
        );

    gap: 13px;

    margin-top: 18px;
}

.member {
    position: relative;

    padding: 16px;

    background:
        rgba(13,9,28,.94);

    border:
        1px solid rgba(155,92,255,.42);

    border-radius: 15px;

    overflow: hidden;
}

.member::before {
    content: "";

    position: absolute;

    left: 0;
    top: 0;
    bottom: 0;

    width: 4px;

    background:
        var(--purple);

    box-shadow:
        0 0 14px
        var(--purple);
}

.member.work::before {
    background: var(--green);

    box-shadow:
        0 0 14px
        var(--green);
}

.member.vacation::before {
    background: var(--orange);

    box-shadow:
        0 0 14px
        var(--orange);
}

.member-name {
    font-size: 16px;
    font-weight: 900;
}

.member-real {
    margin-top: 4px;

    color: #c3bdd0;

    font-size: 13px;
}

.badges {
    display: flex;
    flex-wrap: wrap;

    gap: 6px;

    margin-top: 10px;
}

.badge {
    padding: 5px 8px;

    border-radius: 8px;

    font-size: 11px;

    font-weight: 800;
}

/* уровни */

.level1 {
    color: #c6ccd8;

    border: 1px solid #707889;

    background:
        rgba(112,120,137,.12);
}

.level2 {
    color: #61dfff;

    border: 1px solid #00a9cf;

    background:
        rgba(0,245,255,.08);
}

.level3 {
    color: #72ffb0;

    border: 1px solid #22d878;

    background:
        rgba(77,255,155,.08);
}

.level4 {
    color: #c694ff;

    border: 1px solid #9b5cff;

    background:
        rgba(155,92,255,.10);
}

.level5 {
    color: #ff80e6;

    border: 1px solid #ff2bd6;

    background:
        rgba(255,43,214,.10);
}

.level6 {
    color: #ffd36b;

    border: 1px solid #ffb84d;

    background:
        rgba(255,184,77,.10);
}

.level7 {
    color: white;

    border: 1px solid white;

    background:
        rgba(255,255,255,.08);

    text-shadow:
        0 0 8px var(--pink);
}

/* =====================================================
   ПОДДЕРЖКА
===================================================== */

.support-options {
    display: grid;

    grid-template-columns:
        repeat(
            auto-fit,
            minmax(240px,1fr)
        );

    gap: 15px;

    margin-top: 18px;
}

.support-card {
    padding: 22px;

    text-align: center;

    background:
        rgba(12,8,25,.92);

    border:
        1px solid rgba(255,43,214,.42);

    border-radius: 17px;

    box-shadow:
        0 0 20px
        rgba(255,43,214,.08);
}

.support-icon {
    font-size: 34px;
}

.tg-label {
    margin-top: 10px;

    color: #a8a2b9;

    font-size: 11px;
}

/* =====================================================
   ПОДВАЛ
===================================================== */

.footer {
    padding: 28px 15px 38px;

    text-align: center;

    color: #9690aa;

    font-size: 12px;
}

.footer strong {
    color: var(--cyan);

    text-shadow:
        0 0 8px var(--cyan);
}

.footer a {
    color: var(--cyan);

    text-decoration: none;
}

/* =====================================================
   ПЛЕЕР
===================================================== */

.player {
    position: fixed;

    inset: 0;

    display: none;

    flex-direction: column;

    background: black;

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

    background: black;
}

#iframePlayer {
    width: 100%;
    height: 100%;

    border: none;

    background: black;
}

/* =====================================================
   АДАПТАЦИЯ ТЕЛЕФОНА
===================================================== */

@media (max-width: 700px) {

    header {
        flex-wrap: wrap;
    }

    .logo {
        width: 100%;
        text-align: center;
    }

    .search {
        order: 3;

        flex-basis: 100%;

        max-width: none;
    }

    .owner-mini {
        margin-left: auto;
    }

    .grid {
        grid-template-columns:
            repeat(2,1fr);

        gap: 10px;

        padding: 10px;
    }

    .card {
        height: 225px;
    }

    .team-grid,
    .support-options {
        grid-template-columns: 1fr;
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
        placeholder="Поиск аниме..."
        autocomplete="off"
    >

    <div class="owner-mini">
        Создатель: <strong>EDWIN</strong><br>

        <a href="tel:+79233500539">
            8 923 350-05-39
        </a>
    </div>

</header>


<!-- =====================================================
     МЕНЮ
===================================================== -->

<div class="nav">

    <button onclick="showAll()">
        🏠 Главная
    </button>

    <button onclick="showTeam()">
        👥 Команда
    </button>

    <button onclick="showSupport()">
        💜 Поддержать
    </button>

    <button onclick="showApplication()">
        🎙️ Подать заявку
    </button>

    <a
        href="https://vk.com/aniflex1"
        target="_blank"
        rel="noopener"
    >
        <button>
            🔵 VK
        </button>
    </a>

    <a
        href="https://t.me/Animeflex1x"
        target="_blank"
        rel="noopener"
    >
        <button>
            ✈️ TG
        </button>
    </a>

</div>


<div class="section-label">
    ✦ ANIFLEX NEON · АНИМЕ И ТВОЯ ОЗВУЧКА ✦
</div>


<!-- =====================================================
     ГЛАВНАЯ
===================================================== -->

<div
    id="home"
    class="grid">
</div>


<!-- =====================================================
     СТРАНИЦА АНИМЕ
===================================================== -->

<div
    id="page"
    class="page">
</div>


<!-- =====================================================
     КОМАНДА
===================================================== -->

<div
    id="teamPage"
    class="page">

    <div class="panel">

        <button
            class="btn"
            onclick="showAll()">
            ⬅ Назад
        </button>

        <h2>
            👥 Команда ANIFLEX
        </h2>

        <p
            style="
                text-align:center;
                color:#aaa4c0;
            ">
            Уровни, привилегии и текущий статус участников.
        </p>


        <div class="panel">

            <h3>
                🎖️ Система уровней
            </h3>

            <div class="badges">

                <span class="badge level1">
                    Новичок · 1 уровень
                </span>

                <span class="badge level2">
                    Актёр · 2 уровень
                </span>

                <span class="badge level3">
                    Опытный · 3 уровень
                </span>

                <span class="badge level4">
                    Профи · 4 уровень
                </span>

                <span class="badge level5">
                    Мастер · 5 уровень
                </span>

                <span class="badge level6">
                    Ведущий · 6 уровень
                </span>

                <span class="badge level7">
                    Звезда · 7 уровень
                </span>

            </div>

        </div>


        <div class="team-grid">


            <!-- KATAKINA -->

            <div class="member vacation">

                <div class="member-name">
                    KATAKINA
                </div>

                <div class="member-real">
                    Катя
                </div>

                <div class="badges">

                    <span class="badge level2">
                        Актёр · 2 уровень
                    </span>

                    <span class="badge">
                        🟠 В отпуске
                    </span>

                </div>

            </div>


            <!-- CAUSSADER -->

            <div class="member work">

                <div class="member-name">
                    CAUSSADER
                </div>

                <div class="member-real">
                    Илья
                </div>

                <div class="badges">

                    <span class="badge level1">
                        Новичок · 1 уровень
                    </span>

                    <span class="badge">
                        🟢 В работе
                    </span>

                </div>

            </div>


            <!-- POZITIVNO -->

            <div class="member work">

                <div class="member-name">
                    POZITIVNO
                </div>

                <div class="member-real">
                    Ярик
                </div>

                <div class="badges">

                    <span class="badge level1">
                        Новичок · 1 уровень
                    </span>

                    <span class="badge">
                        🟢 В работе
                    </span>

                </div>

            </div>


            <!-- КОТИК -->

            <div class="member work">

                <div class="member-name">
                    Котик
                </div>

                <div class="member-real">
                    Даша
                </div>

                <div class="badges">

                    <span class="badge level1">
                        Новичок · 1 уровень
                    </span>

                    <span class="badge">
                        🟢 В работе
                    </span>

                </div>

            </div>


            <!-- ХРАНИТЕЛЬ ТЬМЫ -->

            <div class="member work">

                <div class="member-name">
                    Хранитель тьмы
                </div>

                <div class="member-real">
                    Ира
                </div>

                <div class="badges">

                    <span class="badge level2">
                        Актёр · 2 уровень
                    </span>

                    <span class="badge">
                        🟢 В работе
                    </span>

                </div>

            </div>


            <!-- ФИЯ -->

            <div class="member work">

                <div class="member-name">
                    Фия
                </div>

                <div class="member-real">
                    София
                </div>

                <div class="badges">

                    <span class="badge level1">
                        Новичок · 1 уровень
                    </span>

                    <span class="badge">
                        🟢 В работе
                    </span>

                </div>

            </div>


            <!-- KITSEY -->

            <div class="member vacation">

                <div class="member-name">
                    KITSEY
                </div>

                <div class="member-real">
                    Вика
                </div>

                <div class="badges">

                    <span class="badge level1">
                        Новичок · 1 уровень
                    </span>

                    <span class="badge">
                        🟠 В отпуске
                    </span>

                </div>

            </div>


            <!-- ЮЛИК -->

            <div class="member vacation">

                <div class="member-name">
                    Юлик
                </div>

                <div class="member-real">
                    Юля
                </div>

                <div class="badges">

                    <span class="badge level1">
                        Новичок · 1 уровень
                    </span>

                    <span class="badge">
                        🟠 В отпуске
                    </span>

                </div>

            </div>

        </div>

    </div>

</div>


<!-- =====================================================
     ПОДДЕРЖАТЬ
===================================================== -->

<div
    id="supportPage"
    class="page">

    <div class="panel">

        <button
            class="btn"
            onclick="showAll()">
            ⬅ Назад
        </button>

        <h2>
            💜 Поддержать ANIFLEX
        </h2>

        <p
            style="
                text-align:center;
                color:#aaa4c0;
            ">
            Выбери удобный способ поддержки проекта.
        </p>


        <div class="support-options">


            <!-- DONATIONALERTS -->

            <div class="support-card">

                <div class="support-icon">
                    💰
                </div>

                <h3>
                    DonationAlerts
                </h3>

                <p
                    style="color:#aaa4c0">
                    Поддержать проект через DonationAlerts.
                </p>

                <a
                    href="https://www.donationalerts.com/r/LaunchPlay"
                    target="_blank"
                    rel="noopener">

                    <button class="btn">
                        💜 Поддержать
                    </button>

                </a>

                <div class="tg-label">
                    🔗 DonationAlerts
                </div>

            </div>


            <!-- СБЕР -->

            <div class="support-card">

                <div class="support-icon">
                    🏦
                </div>

                <h3>
                    СберБанк
                </h3>

                <p
                    style="color:#aaa4c0">
                    Поддержка по номеру телефона.
                </p>

                <a href="tel:+79233500539">

                    <button class="btn">
                        📞 8 923 350-05-39
                    </button>

                </a>

                <div class="tg-label">
                    📱 Номер владельца
                </div>

            </div>

        </div>

    </div>

</div>


<!-- =====================================================
     ПОДАТЬ ЗАЯВКУ
===================================================== -->

<div
    id="applicationPage"
    class="page">

    <div
        class="panel"
        style="text-align:center">

        <button
            class="btn"
            onclick="showAll()">
            ⬅ Назад
        </button>

        <h2>
            🎙️ Подать заявку в озвучку
        </h2>

        <p
            style="color:#aaa4c0">
            Хочешь присоединиться к команде?
            Напиши владельцу проекта.
        </p>


        <a
            href="https://t.me/launchplay228"
            target="_blank"
            rel="noopener">

            <button class="btn">

                ✈️ Написать владельцу

            </button>

        </a>

        <div class="tg-label">
            Telegram: @launchplay228
        </div>

    </div>

</div>


<!-- =====================================================
     ПЛЕЕР
===================================================== -->

<div
    id="player"
    class="player">

    <div class="player-top">

        <button
            class="btn"
            onclick="closePlayer()">

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
        style="display:none"
        allow="autoplay; fullscreen; picture-in-picture"
        allowfullscreen>
    </iframe>

</div>


<!-- =====================================================
     ПОДВАЛ
===================================================== -->

<div class="footer">

    <strong>
        ANIFLEX
    </strong>

    · Создатель:
    <strong>
        EDWIN
    </strong>

    · Иванов Эрик Юрьевич

    ·

    <a href="tel:+79233500539">
        8 923 350-05-39
    </a>

</div>
```

### JavaScript

```html
<script>

/* =====================================================
   ДАННЫЕ АНИМЕ
===================================================== */

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
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=4_%D1%81%D0%B5%D1%80%D0%B8%D1%8F_wrehoz"
            },

            {
                t: "5 серия",
                v: "https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=5%D1%81_%D0%BA%D0%BE%D1%82_r3dack"
            },

            {
                t: "6 серия",
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


/* =====================================================
   ЭЛЕМЕНТЫ
===================================================== */

const home =
    document.getElementById("home");

const page =
    document.getElementById("page");

const player =
    document.getElementById("player");

const video =
    document.getElementById("video");

const iframe =
    document.getElementById("iframePlayer");

const searchInput =
    document.getElementById("searchInput");

const teamPage =
    document.getElementById("teamPage");

const supportPage =
    document.getElementById("supportPage");

const applicationPage =
    document.getElementById("applicationPage");


/* =====================================================
   ДОПОЛНИТЕЛЬНЫЕ СТРАНИЦЫ
===================================================== */

function hideExtraPages() {

    teamPage.style.display = "none";

    supportPage.style.display = "none";

    applicationPage.style.display = "none";
}


function showTeam() {

    closePlayer();

    home.style.display = "none";
    page.style.display = "none";

    hideExtraPages();

    teamPage.style.display = "block";

    window.scrollTo({
        top: 0,
        behavior: "smooth"
    });
}


function showSupport() {

    closePlayer();

    home.style.display = "none";
    page.style.display = "none";

    hideExtraPages();

    supportPage.style.display = "block";

    window.scrollTo({
        top: 0,
        behavior: "smooth"
    });
}


function showApplication() {

    closePlayer();

    home.style.display = "none";
    page.style.display = "none";

    hideExtraPages();

    applicationPage.style.display = "block";

    window.scrollTo({
        top: 0,
        behavior: "smooth"
    });
}


/* =====================================================
   ЭКРАН ГЛАВНОЙ
===================================================== */

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

        const index =
            data.indexOf(item);

        const card =
            document.createElement("div");

        card.className =
            "card";

        card.style.backgroundImage =
            `url("${item.poster}")`;

        card.innerHTML = `
            <div class="title">
                ${escapeHTML(item.title)}
            </div>
        `;

        card.addEventListener(
            "click",
            () => openAnime(index)
        );

        home.appendChild(card);

    });
}


/* =====================================================
   ОТКРЫТЬ АНИМЕ
===================================================== */

function openAnime(index) {

    hideExtraPages();

    const anime =
        data[index];

    if (!anime) {
        return;
    }

    home.style.display =
        "none";

    page.style.display =
        "block";


    let html = `

        <button
            class="btn"
            onclick="showAll()">

            ⬅ Назад

        </button>

        <h2>
            ${escapeHTML(anime.title)}
        </h2>

    `;


    anime.episodes.forEach(
        (episode, episodeIndex) => {

            const available =
                Boolean(episode.v);

            html += `

                <div
                    class="ep ${available ? "" : "lock"}"

                    ${
                        available
                        ? `onclick="playEpisode(${index}, ${episodeIndex})"`
                        : ""
                    }
                >

                    ${escapeHTML(episode.t)}

                </div>

            `;
        }
    );


    page.innerHTML =
        html;


    window.scrollTo({
        top: 0,
        behavior: "smooth"
    });
}


/* =====================================================
   ЗАПУСК СЕРИИ
===================================================== */

function playEpisode(
    animeIndex,
    episodeIndex
) {

    const anime =
        data[animeIndex];

    if (!anime) {
        return;
    }


    const episode =
        anime.episodes[episodeIndex];

    if (!episode || !episode.v) {
        return;
    }


    const url =
        episode.v;


    player.style.display =
        "flex";


    video.pause();

    video.removeAttribute("src");

    iframe.removeAttribute("src");


    video.style.display =
        "none";

    iframe.style.display =
        "none";


    /* Cloudinary */

    if (
        url.includes(
            "player.cloudinary.com/embed"
        )
    ) {

        iframe.src =
            url;

        iframe.style.display =
            "block";

        return;
    }


    /* MP4 */

    video.src =
        url;

    video.style.display =
        "block";

    video.load();

    const playPromise =
        video.play();


    if (
        playPromise !== undefined
    ) {

        playPromise.catch(
            () => {}
        );
    }
}


/* =====================================================
   ЗАКРЫТЬ ПЛЕЕР
===================================================== */

function closePlayer() {

    player.style.display =
        "none";


    video.pause();

    video.removeAttribute(
        "src"
    );

    video.load();


    iframe.removeAttribute(
        "src"
    );


    video.style.display =
        "none";

    iframe.style.display =
        "none";
}


/* =====================================================
   ГЛАВНАЯ
===================================================== */

function showAll() {

    closePlayer();

    hideExtraPages();

    page.style.display =
        "none";

    home.style.display =
        "grid";

    render(data);

    searchInput.value =
        "";

    window.scrollTo({
        top: 0,
        behavior: "smooth"
    });
}


/* =====================================================
   ПОИСК
===================================================== */

function search(text) {

    hideExtraPages();

    const query =
        text
            .trim()
            .toLowerCase();


    page.style.display =
        "none";

    home.style.display =
        "grid";


    if (!query) {

        render(data);

        return;
    }


    const result =
        data.filter(
            anime =>
                anime.title
                    .toLowerCase()
                    .includes(query)
        );


    render(result);
}


/* =====================================================
   ЗАЩИТА HTML
===================================================== */

function escapeHTML(text) {

    return String(text)

        .replaceAll(
            "&",
            "&amp;"
        )

        .replaceAll(
            "<",
            "&lt;"
        )

        .replaceAll(
            ">",
            "&gt;"
        )

        .replaceAll(
            '"',
            "&quot;"
        )

        .replaceAll(
            "'",
            "&#039;"
        );
}


/* =====================================================
   ПОИСК
===================================================== */

searchInput.addEventListener(
    "input",
    function () {

        search(
            this.value
        );

    }
);


/* =====================================================
   ESC
===================================================== */

document.addEventListener(
    "keydown",
    function(event) {

        if (
            event.key === "Escape"
        ) {

            closePlayer();

        }

    }
);


/* =====================================================
   ЗАПУСК
===================================================== */

render(data);

</script>

</body>
</html>
