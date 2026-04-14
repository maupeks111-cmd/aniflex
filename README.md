<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX GOD MODE 10.0</title>

<style>
body{
margin:0;
font-family:Arial;
background:#0b0b0b;
color:white;
}

/* HEADER */
header{
padding:10px;
background:black;
color:red;
font-weight:bold;
text-align:center;
}

/* HERO */
.hero{
height:200px;
background:url('https://i.imgur.com/1ZQZ1Zm.jpeg') center/cover;
display:flex;
align-items:flex-end;
padding:20px;
font-size:22px;
font-weight:bold;
}

/* NAV */
.nav{
position:fixed;
bottom:0;
width:100%;
display:flex;
background:#111;
border-top:1px solid #222;
}

.nav div{
flex:1;
text-align:center;
padding:12px;
cursor:pointer;
}

/* PAGES */
.page{display:none;padding-bottom:70px;}
.active{display:block;}

/* GRID */
.grid{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:12px;
padding:12px;
}

.card{
height:250px;
border-radius:14px;
background-size:cover;
background-position:center;
position:relative;
box-shadow:0 0 10px rgba(0,0,0,0.5);
overflow:hidden;
}

.card::after{
content:"";
position:absolute;
inset:0;
background:linear-gradient(to top, rgba(0,0,0,0.8), transparent);
}

.card span{
position:absolute;
bottom:0;
width:100%;
text-align:center;
padding:6px;
font-size:13px;
z-index:2;
}

/* ANIME PAGE */
.poster{
width:100%;
border-radius:14px;
}

.anime-page{
padding:12px;
}

.ep{
background:#1a1a1a;
padding:12px;
margin:6px 0;
border-radius:8px;
}

/* PLAYER */
.player{
position:fixed;
inset:0;
background:black;
display:none;
flex-direction:column;
}

iframe{
width:100%;
height:90%;
border:none;
}

button{
padding:10px;
background:red;
border:none;
color:white;
margin-top:10px;
}

input{
width:90%;
margin:10px;
padding:10px;
border-radius:6px;
border:none;
}

</style>
</head>

<body>

<header>ANIFLEX GOD MODE 🔥</header>

<div class="hero">
🔥 Смотри аниме как в Netflix
</div>

<!-- HOME -->
<div id="home" class="page active">
<div class="grid" id="homeList"></div>
</div>

<!-- FAVORITES -->
<div id="fav" class="page">
<h3 style="padding:10px">❤️ Избранное</h3>
<div class="grid" id="favList"></div>
</div>

<!-- SEARCH -->
<div id="search" class="page">
<input placeholder="Поиск..." oninput="search(this.value)">
<div class="grid" id="searchList"></div>
</div>

<!-- ANIME -->
<div id="animePage" class="page">
<div class="anime-page" id="animeInfo"></div>
</div>

<!-- NAV -->
<div class="nav">
<div onclick="openPage('home')">🏠</div>
<div onclick="openPage('fav')">❤️</div>
<div onclick="openPage('search')">🔍</div>
</div>

<!-- PLAYER -->
<div class="player" id="player">
<iframe id="frame"></iframe>
<button onclick="closePlayer()">Закрыть</button>
</div>

<script>

const anime = [
{
id:1,
title:"Гяруко",
poster:"https://i.imgur.com/jx17oHT.jpeg",
episodes:[
{
title:"1 серия",
video:"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239021",
cover:"https://i.imgur.com/zYIlgBl.jpeg"
},
{
title:"2 серия",
video:"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239022",
cover:"https://i.imgur.com/fHyEMsl.jpeg"
}
]
}
];

/* NAV */
function openPage(id){
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

/* HOME */
function renderHome(){
const list=document.getElementById("homeList");
list.innerHTML="";

anime.forEach(a=>{
const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${a.poster})`;
div.innerHTML=`<span>${a.title}</span>`;
div.onclick=()=>openAnime(a);
list.appendChild(div);
});
}

/* ANIME PAGE */
function openAnime(a){
openPage("animePage");

const box=document.getElementById("animeInfo");

box.innerHTML=`
<img class="poster" src="${a.poster}">
<h2>${a.title}</h2>
<button onclick='toggleFav(${JSON.stringify(a)})'>❤️ В избранное</button>

<h3>Серии:</h3>

${a.episodes.map(ep=>`
<div class="ep" onclick="play('${ep.video}')">
<img src="${ep.cover}" style="width:100%;border-radius:8px;">
<p>${ep.title}</p>
</div>
`).join("")}
`;
}

/* PLAYER */
function play(url){
document.getElementById("frame").src=url;
document.getElementById("player").style.display="flex";
}

function closePlayer(){
document.getElementById("frame").src="";
document.getElementById("player").style.display="none";
}

/* FAVORITES */
function toggleFav(item){
let fav=JSON.parse(localStorage.getItem("fav"))||[];
const exists=fav.find(x=>x.id===item.id);

if(exists){
fav=fav.filter(x=>x.id!==item.id);
}else{
fav.push(item);
}

localStorage.setItem("fav",JSON.stringify(fav));
renderFav();
}

function renderFav(){
const box=document.getElementById("favList");
let fav=JSON.parse(localStorage.getItem("fav"))||[];

box.innerHTML="";
fav.forEach(a=>{
const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${a.poster})`;
div.innerHTML=`<span>${a.title}</span>`;
div.onclick=()=>openAnime(a);
box.appendChild(div);
});
}

/* SEARCH */
function search(text){
const res=anime.filter(a=>a.title.toLowerCase().includes(text.toLowerCase()));
const box=document.getElementById("searchList");

box.innerHTML="";
res.forEach(a=>{
const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${a.poster})`;
div.innerHTML=`<span>${a.title}</span>`;
div.onclick=()=>openAnime(a);
box.appendChild(div);
});
}

renderHome();
renderFav();

</script>

</body>
</html>
