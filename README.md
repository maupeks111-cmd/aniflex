<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body{
margin:0;
font-family:Arial;
background:#2b2b2b;
color:white;
}

/* фон */
body::before{
content:"";
position:fixed;
inset:0;
background:url("https://img.freepik.com/premium-photo/japanese-torii-gate-sunset-with-silhouetted-landscape_1282444-100316.jpg");
background-size:cover;
background-position:center;
z-index:-2;
}
body::after{
content:"";
position:fixed;
inset:0;
background:rgba(0,0,0,0.5);
z-index:-1;
}

/* HEADER */
header{
display:flex;
justify-content:space-between;
align-items:center;
padding:12px;
background:white;
position:sticky;
top:0;
z-index:10;
border-radius:0 0 20px 20px;
box-shadow:0 4px 15px rgba(0,0,0,0.2);
}

.logo{
font-size:22px;
font-weight:bold;
color:black;
font-family:"Courier New", monospace;
text-transform:uppercase;
letter-spacing:4px;
}

.search{
width:40%;
padding:8px;
border-radius:8px;
border:none;
outline:none;
}

/* nav */
.nav{
display:flex;
flex-wrap:wrap;
gap:8px;
padding:10px;
}

.nav button{
background:#1f1f1f;
color:white;
border:none;
padding:7px 12px;
border-radius:10px;
cursor:pointer;
}

/* grid */
.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
gap:10px;
padding:10px;
}

/* анимация карточек */
.card{
height:220px;
border-radius:14px;
background-size:cover;
background-position:center;
display:flex;
align-items:flex-end;
padding:10px;
cursor:pointer;
position:relative;
overflow:hidden;
opacity:0;
transform:translateY(20px);
animation:fadeUp 0.4s ease forwards;
}

@keyframes fadeUp{
to{
opacity:1;
transform:translateY(0);
}
}

.card::before{
content:"";
position:absolute;
inset:0;
background:rgba(0,0,0,0.4);
}

.title{
position:relative;
background:rgba(0,0,0,0.7);
padding:6px;
border-radius:8px;
font-size:13px;
}

/* рейтинг */
.rating{
position:absolute;
top:8px;
right:8px;
background:rgba(0,0,0,0.7);
padding:4px 6px;
border-radius:6px;
font-size:12px;
}

/* page */
.page{
display:none;
padding:10px;
background-size:cover;
background-position:center;
animation:fadePage 0.4s ease;
}

@keyframes fadePage{
from{opacity:0; transform:scale(0.98);}
to{opacity:1; transform:scale(1);}
}

.page::before{
content:"";
position:fixed;
inset:0;
background:rgba(0,0,0,0.7);
z-index:-1;
}

/* описание */
.info{
background:#1c1c1c;
padding:15px;
border-radius:15px;
margin-bottom:15px;
box-shadow:0 5px 15px rgba(0,0,0,0.5);
display:flex;
gap:15px;
flex-wrap:wrap;
}

.info img{
width:120px;
border-radius:10px;
}

.info-text{
flex:1;
font-size:14px;
line-height:1.4;
color:#ddd;
}

/* ep */
.ep{
background:#1a1a1a;
padding:10px;
margin:6px 0;
border-radius:10px;
cursor:pointer;
transition:0.2s;
}

.ep:hover{
background:#2a2a2a;
}

.lock{
opacity:0.4;
}

/* player */
.player{
position:fixed;
inset:0;
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
margin:5px;
background:#222;
color:white;
border:none;
border-radius:8px;
cursor:pointer;
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
<video id="video" controls></video>
<button class="btn" onclick="closePlayer()">Закрыть</button>
</div>

<!-- 🔊 ЗВУКИ -->
<audio id="cardSound" src="https://assets.mixkit.co/active_storage/sfx/2571/2571-preview.mp3"></audio>
<audio id="btnSound" src="https://assets.mixkit.co/active_storage/sfx/2568/2568-preview.mp3"></audio>
<audio id="epSound" src="https://assets.mixkit.co/active_storage/sfx/2570/2570-preview.mp3"></audio>

<script>

const data = [

{
title:"Вечера с кошкой (1 сезон)",
poster:"https://shikimori.io/uploads/poster/animes/51692/main-8f221f4b0e5d093ed375a5f6c8f62a6f.webp",
desc:"Уютное аниме про жизнь с милой кошкой.",
rating:"⭐ 8.5",
episodes:Array.from({length:30},(_,i)=>({t:`${i+1} серия (скоро)`,v:""}))
},

{
title:"Клинок рассекающих демонов (1 сезон)",
poster:"https://i.pinimg.com/originals/95/cf/8d/95cf8d3c3a0e41844941259f4247dc6f.jpg",
desc:"Тандзиро становится охотником на демонов.",
rating:"⭐ 9.5",
episodes:Array.from({length:26},(_,i)=>({t:`${i+1} серия (скоро)`,v:""}))
},

{
title:"Гяруко",
poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_.jpg",
desc:"Комедия про школьную жизнь.",
rating:"⭐ 7.5",
episodes:[
{t:"1 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/1_серия_Расскажи_нам_Гяруко_is6ti6.mp4"},
{t:"2 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254679/2_серия_Расскажи_нам_Гяруко_eroylf.mp4"},
{t:"3 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254741/3_серия_Расскажи_нам_Гяруко_ibivet.mp4"},
{t:"4 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254759/4_серия_Расскажи_нам_Гяруко_qzigwl.mp4"},
{t:"5 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254740/5_серия_Расскажи_нам_Гяруко_crtolw.mp4"},
{t:"6 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254747/6_серия_Расскажи_нам_Гяруко_jhnztd.mp4"},
{t:"7 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254735/7_серия_Расскажи_нам_Гяруко_qhbmlj.mp4"},
{t:"8 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254751/8_серия_Расскажи_нам_Гяруко_wsdrnn.mp4"},
{t:"9 серия (есть в вк)",v:""},
{t:"10 серия (есть в вк)",v:""},
{t:"11 серия (есть в вк)",v:""},
{t:"12 серия В РАЗРАБОДКЕ",v:""}
]
},

{
title:"Фарфоровая кукла (1 сезон)",
poster:"https://basket-29.wbbasket.ru/vol5784/part578411/578411360/images/big/1.webp",
desc:"Романтика и косплей.",
rating:"⭐ 8.7",
episodes:[
{t:"1 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/VID_20260416_110510_423_o8ndmt.mp4"},
...Array.from({length:11},(_,i)=>({t:`${i+2} серия (в разработке)`,v:""}))
]
},

{
title:"Сенко-сан",
poster:"https://i.pinimg.com/736x/64/97/89/649789acb22b072a7fb783ca173d6408.jpg",
desc:"Лисичка-дух помогает человеку.",
rating:"⭐ 8.0",
episodes:Array.from({length:12},(_,i)=>({t:`${i+1} серия (скоро)`,v:""}))
},

{
title:"Форма голоса (фильм)",
poster:"https://i.pinimg.com/originals/7f/0d/27/7f0d27d155877e62b2be68952401f329.jpg",
desc:"История искупления и дружбы.",
rating:"⭐ 9.0",
episodes:[{t:"Фильм (скоро)",v:""}]
}

];

const home = document.getElementById("home");
const page = document.getElementById("page");

function render(list){
home.innerHTML="";
list.forEach(item=>{
const index = data.indexOf(item);

const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${item.poster})`;
div.innerHTML=`
<div class="rating">${item.rating}</div>
<div class="title">${item.title}</div>
`;
div.onclick=()=>openAnime(index);

home.appendChild(div);
});
}

render(data);

function openAnime(i){
home.style.display="none";
page.style.display="block";
page.style.backgroundImage=`url(${data[i].poster})`;

let html=`<button class="btn" onclick="back()">⬅ Назад</button>`;
html+=`<h2>${data[i].title}</h2>`;
html+=`<div class="rating">${data[i].rating}</div>`;

html+=`
<div class="info">
<img src="${data[i].poster}">
<div class="info-text">${data[i].desc}</div>
</div>
`;

data[i].episodes.forEach(ep=>{
html+=`<div class="ep ${ep.v?'':'lock'}">${ep.t}</div>`;
});

page.innerHTML=html;
}

function back(){
page.style.display="none";
home.style.display="grid";
}

function search(t){
const filtered = data.filter(a =>
a.title.toLowerCase().includes(t.toLowerCase())
);
render(filtered);
}

function showAll(){render(data);}

/* 🔊 ЗВУКИ */
const cardSound = document.getElementById("cardSound");
const btnSound = document.getElementById("btnSound");
const epSound = document.getElementById("epSound");

document.addEventListener("mouseover", (e)=>{
if(e.target.closest(".card")){
cardSound.currentTime = 0;
cardSound.play();
}
if(e.target.closest(".btn") || e.target.closest(".nav button")){
btnSound.currentTime = 0;
btnSound.play();
}
if(e.target.closest(".ep")){
epSound.currentTime = 0;
epSound.play();
}
});

</script>

</body>
</html>
