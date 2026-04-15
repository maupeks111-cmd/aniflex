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

.banner{
height:220px;
background:url('https://avatars.mds.yandex.net/i?id=4860fda7eb409a1b1179e9239913ff1f3dd36462-5877782-images-thumbs&n=13') center/cover;
display:flex;
align-items:flex-end;
padding:15px;
font-size:20px;
font-weight:bold;
}

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

.locked{
opacity:0.4;
}

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

/* ДВА АНИМЕ */
const animeList = [

{
title:"Гяруко",
poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_FMjpg_UX1000_.jpg",
episodes:[
{title:"1 серия",https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/1_серия_Расскажи_нам_Гяруко_is6ti6.mp4"},
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
},

{
title:"Эта фарфоровая влюбилась",
poster:"https://basket-29.wbbasket.ru/vol5784/part578411/578411360/images/big/1.webp",
episodes:[
{title:"1 серия (СКОРО)",video:""},
{title:"2 серия (В РАЗРАБОТКЕ)",video:""},
{title:"3 серия (В РАЗРАБОТКЕ)",video:""},
{title:"4 серия (В РАЗРАБОТКЕ)",video:""},
{title:"5 серия (В РАЗРАБОТКЕ)",video:""},
{title:"6 серия (В РАЗРАБОТКЕ)",video:""},
{title:"7 серия (В РАЗРАБОТКЕ)",video:""},
{title:"8 серия (В РАЗРАБОТКЕ)",video:""},
{title:"9 серия (В РАЗРАБОТКЕ)",video:""},
{title:"10 серия (В РАЗРАБОТКЕ)",video:""},
{title:"11 серия (В РАЗРАБОТКЕ)",video:""},
{title:"12 серия (В РАЗРАБОТКЕ)",video:""}
]
}

];

/* HOME */
const home=document.getElementById("homeList");

animeList.forEach((anime,index)=>{
const card=document.createElement("div");

card.className="card";
card.style.backgroundImage=`url(${anime.poster})`;
card.innerHTML=`<span>${anime.title}</span>`;

card.onclick=()=>openAnime(index);

home.appendChild(card);
});

/* OPEN */
function openAnime(id){
const anime=animeList[id];

document.getElementById("home").style.display="none";

const page=document.getElementById("animePage");
page.style.display="block";

page.innerHTML=`
<button class="back" onclick="goHome()">⬅ Назад</button>

<img class="poster" src="${anime.poster}">
<h2>${anime.title}</h2>

${anime.episodes.map((ep,i)=>`
<div class="ep ${!ep.video?'locked':''}" ${ep.video?`onclick="play('${ep.video}')"`:''}>
${ep.title}
</div>
`).join("")}
`;
}

/* PLAYER */
function play(url){
document.getElementById("frame").src=url;
document.getElementById("player").style.display="flex";
}

function fullscreen(){
document.getElementById("frame").requestFullscreen();
}

function closePlayer(){
document.getElementById("frame").src="";
document.getElementById("player").style.display="none";
}

function goHome(){
document.getElementById("animePage").style.display="none";
document.getElementById("home").style.display="block";
}

</script>

</body>
</html>
