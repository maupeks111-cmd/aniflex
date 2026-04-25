<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body{margin:0;font-family:Arial;background:#000;color:white;overflow-x:hidden;}

body::before{
content:"";position:fixed;inset:0;
background:url("https://img.freepik.com/premium-photo/japanese-torii-gate-sunset-with-silhouetted-landscape_1282444-100316.jpg");
background-size:cover;
z-index:-2;
}
body::after{
content:"";position:fixed;inset:0;
background:rgba(0,0,0,0.6);
z-index:-1;
}

header{
display:flex;justify-content:space-between;
padding:12px;background:white;
border-radius:0 0 20px 20px;
}
.logo{color:black;font-weight:bold;}
.search{padding:8px;border-radius:8px;border:none;width:40%;}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
gap:10px;
padding:10px;
}

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
transition:0.3s;
}
.card:hover{transform:scale(1.05);}
.card::before{
content:"";position:absolute;inset:0;
background:rgba(0,0,0,0.4);
border-radius:14px;
}
.title{
position:relative;
background:rgba(0,0,0,0.7);
padding:6px;
border-radius:8px;
font-size:13px;
}

.page{display:none;padding:10px;}

.ep{
background:#1a1a1a;
margin:6px 0;
padding:10px;
border-radius:10px;
cursor:pointer;
}
.lock{opacity:0.4;}

.player{
position:fixed;inset:0;
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
}
</style>
</head>

<body>

<header>
<div class="logo">ANIFLEX</div>
<input class="search" placeholder="Поиск..." oninput="search(this.value)">
</header>

<div id="home" class="grid"></div>
<div id="page" class="page"></div>

<div id="player" class="player">
<video id="video" controls></video>
<button class="btn" onclick="closePlayer()">Закрыть</button>
</div>

<script>

const data = [

{
title:"Клинок рассекающих демонов",
poster:"https://i.pinimg.com/originals/95/cf/8d/95cf8d3c3a0e41844941259f4247dc6f.jpg",
episodes:Array.from({length:26},(_,i)=>({
t:`${i+1} серия (скоро)`,
v:""
}))
},

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
{t:"9 серия (вк)",v:""},
{t:"10 серия (вк)",v:""},
{t:"11 серия (вк)",v:""},
{t:"12 серия (скоро)",v:""}
]
},

{
title:"Фарфоровая кукла (1 сезон)",
poster:"https://basket-29.wbbasket.ru/vol5784/part578411/578411360/images/big/1.webp",
episodes:[
{t:"1 серия",v:"https://player.cloudinary.com/embed/?cloud_name=ds3njxeoe&public_id=VID_20260416_110510_423_o8ndmt"},
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

{
title:"Вечера с кошкой",
poster:"https://shikimori.io/uploads/poster/animes/51692/main-8f221f4b0e5d093ed375a5f6c8f62a6f.webp",
episodes:Array.from({length:30},(_,i)=>({
t:`${i+1} серия (скоро)`,
v:""
}))
},

{
title:"Сенко-сан",
poster:"https://i.pinimg.com/736x/64/97/89/649789acb22b072a7fb783ca173d6408.jpg",
episodes:Array.from({length:12},(_,i)=>({
t:`${i+1} серия (скоро)`,
v:""
}))
},

{
title:"Форма голоса (фильм)",
poster:"https://i.pinimg.com/originals/7f/0d/27/7f0d27d155877e62b2be68952401f329.jpg",
episodes:[{t:"Фильм (скоро)",v:""}]
}

];

let currentData = data;

const home=document.getElementById("home");
const page=document.getElementById("page");
const player=document.getElementById("player");
const video=document.getElementById("video");

/* render */
function render(list){
home.innerHTML="";
currentData=list;

list.forEach(item=>{
const i=data.indexOf(item);

const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${item.poster})`;
div.innerHTML=`<div class="title">${item.title}</div>`;
div.onclick=()=>openAnime(i);
home.appendChild(div);
});
}

render(data);

/* open */
function openAnime(i){
home.style.display="none";
page.style.display="block";

let html=`<button class="btn" onclick="back()">⬅ Назад</button>`;
html+=`<h2>${data[i].title}</h2>`;

data[i].episodes.forEach((ep,idx)=>{
html+=`<div class="ep ${ep.v?'':'lock'}">${ep.t}</div>`;
});

page.innerHTML=html;
}

/* play (если добавишь позже видео) */
function play(i,ep){
const item=data[i].episodes[ep];
if(!item.v) return;

video.src=item.v;
player.style.display="flex";
video.play();
}

function closePlayer(){
video.pause();
video.src="";
player.style.display="none";
}

function back(){
page.style.display="none";
home.style.display="grid";
}

/* search FIX (не ломает индексы) */
function search(t){
const filtered = data.filter(a=>a.title.toLowerCase().includes(t.toLowerCase()));
render(filtered);
}

</script>

</body>
</html>
