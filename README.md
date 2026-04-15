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

header{
display:flex;
justify-content:space-between;
align-items:center;
padding:10px;
background:black;
position:sticky;
top:0;
z-index:10;
}

.logo{
font-size:24px;
font-weight:bold;
background:linear-gradient(90deg,#ff2e63,#6a5af9);
-webkit-background-clip:text;
-webkit-text-fill-color:transparent;
}

.search{
width:40%;
padding:7px;
border-radius:6px;
border:none;
}

.nav{
display:flex;
flex-wrap:wrap;
gap:8px;
padding:10px;
}

.nav button{
background:#222;
color:white;
border:none;
padding:6px 10px;
border-radius:6px;
cursor:pointer;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
gap:10px;
padding:10px;
}

.card{
height:220px;
border-radius:12px;
background-size:cover;
background-position:center;
display:flex;
align-items:flex-end;
padding:10px;
cursor:pointer;
position:relative;
}

.title{
background:rgba(0,0,0,0.6);
padding:5px;
border-radius:6px;
font-size:13px;
}

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

.lock{
opacity:0.4;
cursor:not-allowed;
}

.player{
position:fixed;
top:0;left:0;
width:100%;height:100%;
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

.btn{
padding:8px;
background:#222;
color:white;
border:none;
border-radius:6px;
margin:5px;
}
</style>
</head>

<body>

<header>
<div class="logo">ANIFLEX</div>
<input class="search" placeholder="Поиск..." oninput="search(this.value)">
</header>

<div class="nav">
<button onclick="showAll()">🏠 Главная</button>
<button onclick="showFav()">❤️ Избранное</button>
<button onclick="resumeLast()">▶️ Продолжить</button>

<a href="https://vk.com/aniflex1"><button>VK</button></a>
<a href="https://t.me/Animeflex1x"><button>TG</button></a>
<a href="https://www.donationalerts.com/r/LaunchPlay"><button>💰 Донат</button></a>
</div>

<div id="home" class="grid"></div>
<div id="page" class="page"></div>

<div id="player" class="player">
<video id="video" controls playsinline></video>
<button class="btn" onclick="closePlayer()">Закрыть</button>
</div>

<script>

const data=[

/* ------------------ ГЯРУКО ------------------ */
{
title:"Гяруко",
poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_.jpg",
episodes:[
{t:"1 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/1_серия_Расскажи_нам_Гяруко_is6ti6.mp4"},
{t:"2 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254679/2_серия_Расскажи_нам_Гяруко_eroylf.mp4"},
{t:"3 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254741/3_серия_Расскажи_нам_Гяруко_ibivet.mp4"},
{t:"4 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254759/4_серия_Расскажи_нам_Гяруко_qzigwl.mp4"},
{t:"5 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254740/5_серия_Расскажи_нам_Гяруко_crtolw.mp4"},
{t:"6 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254747/6_серия_Расскажи_нам_Гяруко_jhnztd.mp4"},
{t:"7 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254735/7_серия_Расскажи_нам_Гяруко_qhbmlj.mp4"},
{t:"8 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254751/8_серия_Расскажи_нам_Гяруко_wsdrnn.mp4"},
{t:"9 (нет)",v:""},
{t:"10 (нет)",v:""},
{t:"11 (нет)",v:""},
{t:"12 (скоро)",v:""}
]
},

/* ------------------ КУКЛА ------------------ */
{
title:"Фарфоровая кукла (1 сезон)",
poster:"https://basket-29.wbbasket.ru/vol5784/part578411/578411360/images/big/1.webp",
episodes:[
{t:"1 серия (скоро)",v:""},
{t:"2-12 (в разработке)",v:""}
]
},

/* ------------------ СЕНКО САН ------------------ */
{
title:"Сенко-сан (1 сезон)",
poster:"https://i.pinimg.com/736x/64/97/89/649789acb22b072a7fb783ca173d6408.jpg",
episodes:[
{t:"1 серия (скоро)",v:""},
{t:"2 серия (скоро)",v:""},
{t:"3 серия (скоро)",v:""},
{t:"4 серия (скоро)",v:""},
{t:"5 серия (скоро)",v:""},
{t:"6 серия (скоро)",v:""},
{t:"7 серия (скоро)",v:""},
{t:"8 серия (скоро)",v:""},
{t:"9 серия (скоро)",v:""},
{t:"10 серия (скоро)",v:""},
{t:"11 серия (скоро)",v:""},
{t:"12 серия (скоро)",v:""}
]
},

/* ------------------ ФИЛЬМ ------------------ */
{
title:"Форма голоса (фильм)",
poster:"https://static.okko.tv/images/v4/258f2d40-cc36-4c79-a13f-a6ebe3ae6ea8?presetId=4000",
episodes:[
{t:"Фильм (скоро)",v:""}
]
}

];

let fav=JSON.parse(localStorage.getItem("fav"))||[];
let last=null;

const home=document.getElementById("home");
const page=document.getElementById("page");
const player=document.getElementById("player");
const video=document.getElementById("video");

/* ---------------- RENDER ---------------- */
function render(list){
home.innerHTML="";
list.forEach((a,i)=>{
let div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${a.poster})`;

div.innerHTML=`
<div class="title">${a.title}</div>
`;

div.onclick=()=>openAnime(i);
home.appendChild(div);
});
}
render(data);

/* ---------------- OPEN ---------------- */
function openAnime(i){
home.style.display="none";
page.style.display="block";

let html=`<button class="btn" onclick="back()">⬅ Назад</button>`;
html+=`<h2>${data[i].title}</h2>`;

data[i].episodes.forEach((ep,idx)=>{
html+=`<div class="ep ${ep.v?'':'lock'}" onclick="play(i=${i},ep=${idx})">${ep.t}</div>`;
});

page.innerHTML=html;
}

/* ---------------- PLAY ---------------- */
function play(i,ep){
if(!data[i].episodes[ep].v) return;

video.src=data[i].episodes[ep].v;
player.style.display="flex";
video.play();

last={i,ep};
localStorage.setItem("last",JSON.stringify(last));
}

/* ---------------- CLOSE ---------------- */
function closePlayer(){
video.pause();
video.src="";
player.style.display="none";
}

/* ---------------- BACK ---------------- */
function back(){
page.style.display="none";
home.style.display="grid";
}

/* ---------------- SEARCH ---------------- */
function search(t){
render(data.filter(a=>a.title.toLowerCase().includes(t.toLowerCase())));
}

/* ---------------- FAVORITES ---------------- */
function showFav(){
render(data.filter((_,i)=>fav.includes(i)));
}

function showAll(){
render(data);
}

/* ---------------- RESUME ---------------- */
function resumeLast(){
let l=JSON.parse(localStorage.getItem("last"));
if(!l) return;
play(l.i,l.ep);
}

</script>

</body>
</html>
