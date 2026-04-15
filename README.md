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

/* BANNER */
.banner{
height:200px;
background:url('https://avatars.mds.yandex.net/i?id=4860fda7eb409a1b1179e9239913ff1f3dd36462-5877782-images-thumbs&n=13') center/cover;
display:flex;
align-items:flex-end;
padding:15px;
font-size:20px;
}

/* GRID */
.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
gap:12px;
padding:12px;
}

.card{
height:230px;
border-radius:14px;
background-size:cover;
background-position:center;
position:relative;
cursor:pointer;
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
}

/* PAGE */
.poster{
width:100%;
border-radius:12px;
}

.ep{
background:#1b1b25;
padding:12px;
margin:6px 0;
border-radius:8px;
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

video{
width:100%;
height:100%;
object-fit:contain;
background:black;
}

/* CONTROLS */
.controls{
position:absolute;
top:10px;
right:10px;
display:flex;
gap:10px;
}

.btn{
background:rgba(0,0,0,0.6);
border:none;
color:white;
padding:8px;
border-radius:6px;
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
</header>

<div class="banner">🔥 Гяруко — все серии</div>

<div id="home">
<div class="grid" id="homeList"></div>
</div>

<div id="animePage" style="display:none;padding:12px;"></div>

<div class="player" id="player">

<video id="video" controls playsinline></video>

<div class="controls">
<button class="btn" onclick="fullscreen()">⛶</button>
<button class="btn" onclick="closePlayer()">✖</button>
</div>

</div>

<script>

const anime = {
title:"Гяруко",
poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_FMjpg_UX1000_.jpg",

episodes:[
{title:"1 серия",video:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/1_серия_Расскажи_нам_Гяруко_is6ti6.mp4"},
{title:"2 серия",video:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254679/2_серия_Расскажи_нам_Гяруко_eroylf.mp4"},
{title:"3 серия",video:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254741/3_серия_Расскажи_нам_Гяруко_ibivet.mp4"},
{title:"4 серия",video:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254759/4_серия_Расскажи_нам_Гяруко_qzigwl.mp4"},
{title:"5 серия",video:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254740/5_серия_Расскажи_нам_Гяруко_crtolw.mp4"},
{title:"6 серия",video:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254747/6_серия_Расскажи_нам_Гяруко_jhnztd.mp4"},
{title:"7 серия",video:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254735/7_серия_Расскажи_нам_Гяруко_qhbmlj.mp4"},
{title:"8 серия",video:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254751/8_серия_Расскажи_нам_Гяруко_wsdrnn.mp4"},
{title:"9 серия (нет mp4)",video:""},
{title:"10 серия (нет mp4)",video:""},
{title:"11 серия (нет mp4)",video:""},
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
<div class="ep ${!ep.video?'locked':''}" ${ep.video?`onclick="play(${i})"`:''}>
${ep.title}
</div>
`).join("")}
`;
}

/* PLAYER */
function play(i){
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
}else if(video.webkitEnterFullscreen){
video.webkitEnterFullscreen(); // iPhone
}
}

/* CLOSE */
function closePlayer(){
const video=document.getElementById("video");
video.pause();
video.src="";
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
