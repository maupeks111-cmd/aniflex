<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body{
margin:0;
font-family:Arial;
background:#111;
color:white;
overflow-x:hidden;
}

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
background:rgba(0,0,0,0.55);
z-index:-1;
}

header{
display:flex;
justify-content:space-between;
align-items:center;
padding:12px;
background:white;
border-radius:0 0 20px 20px;
position:sticky;
top:0;
z-index:10;
}

.logo{
font-weight:bold;
font-family:monospace;
color:black;
letter-spacing:3px;
}

.search{
padding:8px;
border-radius:8px;
border:none;
width:40%;
outline:none;
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
padding:8px 12px;
border-radius:10px;
cursor:pointer;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
gap:12px;
padding:10px;
}

.card{
height:240px;
border-radius:16px;
background-size:cover;
background-position:center;
cursor:pointer;
position:relative;
overflow:hidden;
transition:0.3s;
box-shadow:0 8px 20px rgba(0,0,0,0.4);
}

.card::before{
content:"";
position:absolute;
inset:0;
background:linear-gradient(to top, rgba(0,0,0,0.85), transparent);
}

.card:hover{
transform:scale(1.05);
z-index:5;
}

.title{
position:absolute;
bottom:10px;
left:10px;
background:rgba(0,0,0,0.7);
padding:6px 10px;
border-radius:10px;
font-size:13px;
}

.badge{
position:absolute;
top:8px;
right:8px;
background:red;
font-size:10px;
padding:3px 6px;
border-radius:6px;
}

.page{
display:none;
padding:10px;
}

.ep{
background:#1c1c1c;
padding:10px;
margin:6px 0;
border-radius:10px;
cursor:pointer;
}

.lock{opacity:0.4;}

.player{
position:fixed;
inset:0;
background:black;
display:none;
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
{t:"9 (вк)",v:""},
{t:"10 (вк)",v:""},
{t:"11 (вк)",v:""},
{t:"12 (скоро)",v:""}
]
},

{
title:"Фарфоровая кукла",
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
title:"Сенко-сан",
poster:"https://i.pinimg.com/736x/64/97/89/649789acb22b072a7fb783ca173d6408.jpg",
episodes:Array.from({length:12},(_,i)=>({
t:`${i+1} серия (скоро)`,
v:""
}))
},

{
title:"Форма голоса",
poster:"https://i.pinimg.com/originals/7f/0d/27/7f0d27d155877e62b2be68952401f329.jpg",
episodes:[{t:"Фильм (скоро)",v:""}]
},

{
title:"Вечера с кошкой",
poster:"https://static.kinoafisha.info/k/series_posters/480/upload/series/posters/4/7/4/13474/338468001759996357.jpg",
episodes:Array.from({length:30},(_,i)=>({
t:`${i+1} серия (скоро)`,
v:""
}))
}

];

let home=document.getElementById("home");
let page=document.getElementById("page");
let player=document.getElementById("player");
let video=document.getElementById("video");

function render(list){
home.innerHTML="";
list.forEach(item=>{
let i=data.indexOf(item);

let div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${item.poster})`;
div.innerHTML=`
<div class="badge">ANIFLEX</div>
<div class="title">${item.title}</div>
`;
div.onclick=()=>open(i);
home.appendChild(div);
});
}

render(data);

function open(i){
home.style.display="none";
page.style.display="block";

let html=`<button class="btn" onclick="back()">Назад</button>`;
html+=`<h2>${data[i].title}</h2>`;

data[i].episodes.forEach(e=>{
html+=`<div class="ep ${e.v?'':'lock'}" onclick="play('${e.v}')">${e.t}</div>`;
});

page.innerHTML=html;
}

function play(v){
if(!v) return;
video.src=v;
player.style.display="block";
video.play();
}

function closePlayer(){
player.style.display="none";
video.pause();
}

function back(){
page.style.display="none";
home.style.display="grid";
}

function showAll(){render(data);}

function search(t){
render(data.filter(a=>a.title.toLowerCase().includes(t.toLowerCase())));
}

</script>

</body>
</html>
