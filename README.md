<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body{
margin:0;
background:#0a0a0f;
color:white;
font-family:Arial;
}

/* HEADER */
header{
display:flex;
justify-content:space-between;
align-items:center;
padding:10px;
background:black;
}

.logo{
color:#ff2e63;
font-weight:bold;
font-size:22px;
}

.links a{
color:white;
margin-left:10px;
text-decoration:none;
font-size:14px;
}

/* BANNER */
.banner{
height:220px;
background:url('https://avatars.mds.yandex.net/i?id=4860fda7eb409a1b1179e9239913ff1f3dd36462-5877782-images-thumbs&n=13') center/cover;
display:flex;
align-items:flex-end;
padding:15px;
font-size:20px;
font-weight:bold;
}

/* GRID */
.grid{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:12px;
padding:12px;
}

.card{
height:240px;
border-radius:14px;
background-size:cover;
background-position:center;
position:relative;
cursor:pointer;
overflow:hidden;
}

.card::after{
content:"";
position:absolute;
inset:0;
background:linear-gradient(to top,rgba(0,0,0,0.9),transparent);
}

.card span{
position:absolute;
bottom:0;
width:100%;
text-align:center;
padding:10px;
z-index:2;
}

/* PAGE */
.poster{
width:100%;
border-radius:14px;
margin-bottom:10px;
}

.ep{
background:#1b1b25;
padding:12px;
margin:6px 0;
border-radius:10px;
cursor:pointer;
}

.ep:hover{
background:#2a2a3a;
}

.locked{
opacity:0.4;
}

/* PLAYER */
.player{
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:black;
display:none;
flex-direction:column;
z-index:999;
}

iframe{
width:100%;
height:90%;
border:none;
}

.controls{
display:flex;
gap:10px;
padding:10px;
}

button{
flex:1;
padding:10px;
background:#ff2e63;
border:none;
color:white;
border-radius:8px;
}

/* BACK */
.back{
margin:10px 0;
padding:10px;
background:#222;
border:none;
color:white;
border-radius:8px;
width:100%;
}
</style>
</head>

<body>

<header>
<div class="logo">ANIFLEX</div>

<div class="links">
<a href="https://vk.com/aniflex1" target="_blank">VK</a>
<a href="https://t.me/Animeflex1x" target="_blank">TG</a>
<a href="https://www.donationalerts.com/r/LaunchPlay" target="_blank">ДОНАТ</a>
</div>
</header>

<div class="banner">
🔥 Смотри аниме бесплатно
</div>

<div id="home">
<div class="grid" id="homeList"></div>
</div>

<div id="animePage" style="display:none;padding:12px;"></div>

<div class="player" id="player">
<iframe id="frame" allowfullscreen></iframe>

<div class="controls">
<button onclick="fullscreen()">⛶ Fullscreen</button>
<button onclick="closePlayer()">✖ Закрыть</button>
</div>
</div>

<script>

const anime = {
title:"Гяруко",
poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_FMjpg_UX1000_.jpg",

episodes:[
{title:"1 серия",video:"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239021"},
{title:"2 серия",video:"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239024"},
{title:"3 серия",video:"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239032"},
{title:"4 серия",video:"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239032"},
{title:"5 серия",video:"https://vkvideo.ru/video_ext.php?oid=-231918162&id=456239017"},
{title:"6 серия",video:"https://vkvideo.ru/video_ext.php?oid=-231918162&id=456239018"},
{title:"7 серия",video:"https://vkvideo.ru/video_ext.php?oid=-231918162&id=456239020"},
{title:"8 серия",video:"https://vkvideo.ru/video_ext.php?oid=-231918162&id=456239022"},
{title:"9 серия",video:"https://v3.animelib.org/ru/anime/11023--oshiete-galko-chan-anime/watch?episode=66990"},
{title:"10 серия",video:"https://vkvideo.ru/video_ext.php?oid=-231918162&id=456239026"},
{title:"11 серия",video:"https://vkvideo.ru/video_ext.php?oid=-231918162&id=456239028"},
{title:"12 серия (СКОРО)",video:""}
]
};

/* HOME */
const home=document.getElementById("homeList");
const card=document.createElement("div");

card.className="card";
card.style.backgroundImage=`url(${anime.poster})`;
card.innerHTML=`<span>${anime.title}</span>`;
card.onclick=openAnime;

home.appendChild(card);

/* OPEN */
function openAnime(){
document.getElementById("home").style.display="none";

const page=document.getElementById("animePage");
page.style.display="block";

page.innerHTML=`
<button class="back" onclick="goHome()">⬅ Назад</button>

<img class="poster" src="${anime.poster}">
<h2>${anime.title}</h2>

${anime.episodes.map((ep,i)=>`
<div class="ep ${!ep.video?'locked':''}" ${ep.video?`onclick="playEpisode(${i})"`:''}>
${ep.title}
${!ep.video?'<br>СКОРО':''}
</div>
`).join("")}
`;
}

/* PLAYER */
function playEpisode(i){
document.getElementById("frame").src=anime.episodes[i].video;
document.getElementById("player").style.display="flex";
}

/* FULLSCREEN */
function fullscreen(){
const iframe=document.getElementById("frame");
if(iframe.requestFullscreen){
iframe.requestFullscreen();
}
}

/* CLOSE */
function closePlayer(){
document.getElementById("frame").src="";
document.getElementById("player").style.display="none";
}

/* BACK */
function goHome(){
document.getElementById("animePage").style.display="none";
document.getElementById("home").style.display="block";
}

</script>

</body>
</html>
