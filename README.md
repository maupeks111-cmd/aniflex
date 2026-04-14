<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX FINAL</title>

<style>
body{margin:0;background:#0b0b0b;color:white;font-family:Arial;}

/* HEADER */
header{
display:flex;
justify-content:space-between;
align-items:center;
padding:10px;
background:black;
}

.logo{color:red;font-weight:bold;font-size:20px;}

/* LINKS */
.links a{
color:white;
margin-left:10px;
text-decoration:none;
font-size:14px;
}

/* HERO */
.hero{
height:180px;
background:url('https://avatars.mds.yandex.net/i?id=4860fda7eb409a1b1179e9239913ff1f3dd36462-5877782-images-thumbs&n=13') center/cover;
display:flex;
align-items:flex-end;
padding:15px;
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

.ep:hover{background:#2a2a2a;}

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

iframe{
width:100%;
height:90%;
border:none;
}

.progress{
height:4px;
background:red;
width:0%;
}

/* BUTTON */
button{
background:red;
border:none;
color:white;
padding:10px;
margin-top:10px;
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

<div class="hero">🔥 Смотри аниме бесплатно</div>

<div id="home">
<div class="grid" id="homeList"></div>
</div>

<div id="animePage" style="display:none;padding:10px;"></div>

<div class="player" id="player">
<div class="progress" id="progress"></div>
<iframe id="frame" allowfullscreen></iframe>
<button onclick="closePlayer()">Закрыть</button>
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
{title:"9 серия",video:"https://v3.animelib.org/ru/anime/11023--oshiete-galko-chan-anime/watch?episode=66990&player=Animelib"},
{title:"10 серия",video:"https://vkvideo.ru/video_ext.php?oid=-231918162&id=456239026"},
{title:"11 серия",video:"https://vkvideo.ru/video_ext.php?oid=-231918162&id=456239028"},
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

/* OPEN ANIME */
function openAnime(){
document.getElementById("home").style.display="none";
const page=document.getElementById("animePage");
page.style.display="block";

page.innerHTML=`
<img class="poster" src="${anime.poster}">
<h2>${anime.title}</h2>

<button onclick="playEpisode(0)">▶ Смотреть с 1 серии</button>

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
document.getElementById("frame").src=anime.episodes[i].video;
document.getElementById("player").style.display="flex";

/* авто-прогресс */
let p=0;
const bar=document.getElementById("progress");
const interval=setInterval(()=>{
p+=1;
bar.style.width=p+"%";
if(p>=100){
clearInterval(interval);
nextEpisode();
}
},300);
}

/* NEXT */
function nextEpisode(){
if(currentIndex<anime.episodes.length-1){
currentIndex++;
if(anime.episodes[currentIndex].video){
playEpisode(currentIndex);
}
}
}

/* CLOSE */
function closePlayer(){
document.getElementById("frame").src="";
document.getElementById("player").style.display="none";
}

</script>

</body>
</html>
