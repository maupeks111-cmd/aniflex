<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body{margin:0;background:#0b0b0b;color:white;font-family:Arial;}

header{
display:flex;
justify-content:space-between;
padding:10px;
background:black;
}

.logo{color:red;font-weight:bold;}

.links a{
color:white;
margin-left:10px;
text-decoration:none;
font-size:14px;
}

.hero{
height:180px;
background:#111;
display:flex;
align-items:center;
justify-content:center;
font-size:20px;
}

/* GRID */
.grid{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:10px;
padding:10px;
}

.card{
height:220px;
border-radius:12px;
background-size:cover;
position:relative;
cursor:pointer;
}

.card span{
position:absolute;
bottom:0;
width:100%;
background:rgba(0,0,0,0.7);
text-align:center;
padding:5px;
}

/* ANIME PAGE */
.poster{width:100%;border-radius:12px;}

.ep{
background:#1a1a1a;
margin:8px 0;
padding:10px;
border-radius:8px;
cursor:pointer;
}

.locked{opacity:0.4;cursor:default;}

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

video{
width:100%;
height:90%;
background:black;
}

/* CONTROLS */
.controls{
display:flex;
gap:10px;
padding:10px;
}

button{
flex:1;
background:red;
border:none;
color:white;
padding:10px;
border-radius:6px;
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

<div class="hero">🔥 Без рекламы. Чистый плеер</div>

<div id="home">
<div class="grid" id="homeList"></div>
</div>

<div id="animePage" style="display:none;padding:10px;"></div>

<div class="player" id="player">
<video id="video" controls></video>

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
{title:"1 серия",video:"PASTE_MP4"},
{title:"2 серия",video:"PASTE_MP4"},
{title:"3 серия",video:"PASTE_MP4"},
{title:"4 серия",video:"PASTE_MP4"},
{title:"5 серия",video:"PASTE_MP4"},
{title:"6 серия",video:"PASTE_MP4"},
{title:"7 серия",video:"PASTE_MP4"},
{title:"8 серия",video:"PASTE_MP4"},
{title:"9 серия",video:"PASTE_MP4"},
{title:"10 серия",video:"PASTE_MP4"},
{title:"11 серия",video:"PASTE_MP4"},
{title:"12 серия (СКОРО)",video:""}
]
};

let currentIndex=0;

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
<button onclick="goHome()">⬅ Назад</button>

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
currentIndex=i;

const video=document.getElementById("video");
video.src=anime.episodes[i].video;

document.getElementById("player").style.display="flex";
video.play();
}

/* FULLSCREEN */
function fullscreen(){
const video=document.getElementById("video");
if(video.requestFullscreen){
video.requestFullscreen();
}
}

/* CLOSE */
function closePlayer(){
const video=document.getElementById("video");
video.pause();
video.src="";
document.getElementById("player").style.display="none";
}

/* HOME BACK */
function goHome(){
document.getElementById("animePage").style.display="none";
document.getElementById("home").style.display="block";
}

</script>

</body>
</html>
