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
}

/* затемнение страницы */
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
<video id="video" controls playsinline webkit-playsinline></video>
<button class="btn" onclick="closePlayer()">Закрыть</button>
</div>

<script>

const data = [

{
title:"Вечера с кошкой (1 сезон)",
poster:"https://shikimori.io/uploads/poster/animes/51692/main-8f221f4b0e5d093ed375a5f6c8f62a6f.webp",
desc:"Уютное аниме о повседневной жизни с милой кошкой и тёплых вечерах дома.",
rating:"⭐ 8.5",
episodes:Array.from({length:30},(_,i)=>({
t:`${i+1} серия (скоро)`,
v:""
}))
},

{
title:"Клинок рассекающих демонов (1 сезон)",
poster:"https://i.pinimg.com/originals/95/cf/8d/95cf8d3c3a0e41844941259f4247dc6f.jpg",
desc:"История Тандзиро, ставшего охотником на демонов ради спасения сестры.",
rating:"⭐ 9.5",
episodes:Array.from({length:26},(_,i)=>({
t:`${i+1} серия (скоро)`,
v:""
}))
},

{
title:"Сенко-сан",
poster:"https://i.pinimg.com/736x/64/97/89/649789acb22b072a7fb783ca173d6408.jpg",
desc:"Лисичка-дух помогает уставшему офисному работнику.",
rating:"⭐ 8.0",
episodes:Array.from({length:12},(_,i)=>({
t:`${i+1} серия (скоро)`,
v:""
}))
},

{
title:"Форма голоса (фильм)",
poster:"https://i.pinimg.com/originals/7f/0d/27/7f0d27d155877e62b2be68952401f329.jpg",
desc:"История о дружбе, ошибках и искуплении.",
rating:"⭐ 9.0",
episodes:[{t:"Фильм (скоро)",v:""}]
}

];

let fav = [];
let last = null;

const home = document.getElementById("home");
const page = document.getElementById("page");
const player = document.getElementById("player");
const video = document.getElementById("video");

function render(list){
home.innerHTML="";
list.forEach(item=>{
const index = data.indexOf(item);

const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${item.poster})`;
div.innerHTML=`
<div class="rating">${item.rating || ""}</div>
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

/* фон страницы */
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

data[i].episodes.forEach((ep,idx)=>{
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

</script>

</body>
</html>
