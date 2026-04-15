<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body{
margin:0;
background:#0b0b0f;
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
position:sticky;
top:0;
z-index:100;
}

.logo{
color:#ff2e63;
font-size:22px;
font-weight:bold;
}

.search{
padding:6px;
border-radius:6px;
border:none;
width:40%;
}

/* GRID */
.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(140px,1fr));
gap:10px;
padding:10px;
}

.card{
height:200px;
border-radius:12px;
background-size:cover;
background-position:center;
display:flex;
align-items:flex-end;
padding:10px;
cursor:pointer;
position:relative;
}

.fav{
position:absolute;
top:5px;
right:5px;
background:rgba(0,0,0,0.6);
padding:5px;
border-radius:50%;
cursor:pointer;
}

/* PAGE */
.page{
display:none;
padding:10px;
}

.ep{
background:#1b1b25;
padding:10px;
margin:5px 0;
border-radius:6px;
cursor:pointer;
}

.locked{
opacity:0.4;
cursor:default;
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
}

/* FOOTER */
.footer{
padding:10px;
text-align:center;
background:#111;
}

.footer a{
color:#ff2e63;
display:block;
margin:5px 0;
text-decoration:none;
}
</style>
</head>

<body>

<header>
<div class="logo">ANIFLEX</div>
<input class="search" placeholder="Поиск..." oninput="searchAnime(this.value)">
</header>

<div id="home" class="grid"></div>

<div id="page" class="page"></div>

<div id="player" class="player">
<video id="video" controls></video>
<button onclick="closePlayer()">Закрыть</button>
</div>

<div class="footer">
<a href="https://vk.com/aniflex1" target="_blank">VK</a>
<a href="https://t.me/Animeflex1x" target="_blank">Telegram</a>
<a href="https://www.donationalerts.com/r/LaunchPlay" target="_blank">Донат</a>
</div>

<script>

const data = [
{
title:"Гяруко",
poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_FMjpg_UX1000_.jpg",
episodes:[
{t:"1 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/1_серия_Расскажи_нам_Гяруко_is6ti6.mp4"},
{t:"2 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254679/2_серия_Расскажи_нам_Гяруко_eroylf.mp4"},
{t:"3 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254741/3_серия_Расскажи_нам_Гяруко_ibivet.mp4"},
{t:"4 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254759/4_серия_Расскажи_нам_Гяруко_qzigwl.mp4"},
{t:"5 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254740/5_серия_Расскажи_нам_Гяруко_crtolw.mp4"},
{t:"6 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254747/6_серия_Расскажи_нам_Гяруко_jhnztd.mp4"},
{t:"7 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254735/7_серия_Расскажи_нам_Гяруко_qhbmlj.mp4"},
{t:"8 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254751/8_серия_Расскажи_нам_Гяруко_wsdrnn.mp4"},
{t:"9 серия (нет)",v:""},
{t:"10 серия (нет)",v:""},
{t:"11 серия (нет)",v:""},
{t:"12 серия (Скоро)",v:""}
]
},

{
title:"Фарфоровая кукла влюбилась",
poster:"https://basket-29.wbbasket.ru/vol5784/part578411/578411360/images/big/1.webp",
episodes:[
{t:"1 серия (Скоро)",v:""},
{t:"2-12 (в разработке)",v:""}
]
}
];

let favorites = JSON.parse(localStorage.getItem("fav")) || [];

const home = document.getElementById("home");

/* РЕНДЕР */
function render(list){
home.innerHTML="";

list.forEach((a,i)=>{
const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${a.poster})`;

div.innerHTML=`
<div class="fav" onclick="toggleFav(event,${i})">
${favorites.includes(i)?"❤️":"🤍"}
</div>
<b>${a.title}</b>
`;

div.onclick=()=>openAnime(i);

home.appendChild(div);
});
}

render(data);

/* ИЗБРАННОЕ */
function toggleFav(e,i){
e.stopPropagation();

if(favorites.includes(i)){
favorites = favorites.filter(x=>x!==i);
}else{
favorites.push(i);
}

localStorage.setItem("fav",JSON.stringify(favorites));
render(data);
}

/* ПОИСК */
function searchAnime(text){
const filtered = data.filter(a =>
a.title.toLowerCase().includes(text.toLowerCase())
);
render(filtered);
}

/* СТРАНИЦА */
function openAnime(i){
home.style.display="none";
const page=document.getElementById("page");
page.style.display="block";

let html=`<button onclick="back()">⬅ Назад</button>`;
html+=`<h2>${data[i].title}</h2>`;

data[i].episodes.forEach((ep,index)=>{
html+=`
<div class="ep ${!ep.v?'locked':''}" ${ep.v?`onclick="play(${i},${index})"`:''}>
${ep.t}
</div>`;
});

page.innerHTML=html;
}

/* ПЛЕЕР */
function play(a,ep){
const video=document.getElementById("video");
video.src=data[a].episodes[ep].v;

document.getElementById("player").style.display="flex";
video.play();
}

/* ЗАКРЫТЬ */
function closePlayer(){
const video=document.getElementById("video");
video.pause();
video.src="";
document.getElementById("player").style.display="none";
}

/* НАЗАД */
function back(){
document.getElementById("page").style.display="none";
home.style.display="grid";
}

</script>

</body>
</html>
