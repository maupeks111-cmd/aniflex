<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX ULTRA 9.0</title>

<style>
body{
margin:0;
font-family:Arial;
background:#0b0b0b;
color:white;
}

/* HEADER */
header{
text-align:center;
padding:10px;
background:black;
color:red;
font-weight:bold;
}

/* NAV */
.nav{
position:fixed;
bottom:0;
width:100%;
display:flex;
background:black;
}

.nav div{
flex:1;
text-align:center;
padding:10px;
cursor:pointer;
}

/* PAGES */
.page{display:none;padding-bottom:60px;}
.active{display:block;}

/* GRID */
.grid{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:10px;
padding:10px;
}

.card{
height:240px;
border-radius:12px;
background-size:cover;
background-position:center;
position:relative;
}

.card span{
position:absolute;
bottom:0;
width:100%;
background:rgba(0,0,0,0.7);
text-align:center;
font-size:12px;
padding:5px;
}

/* ANIME PAGE */
.anime-page{
padding:10px;
}

.poster{
width:100%;
border-radius:12px;
}

.episodes{
margin-top:10px;
}

.ep{
background:#222;
padding:10px;
margin:5px 0;
border-radius:6px;
cursor:pointer;
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
}

button{
padding:10px;
background:red;
border:none;
color:white;
}

</style>
</head>

<body>

<header>ANIFLEX ULTRA 9.0 🚀</header>

<!-- HOME -->
<div id="home" class="page active">
<h3 style="padding:10px">🔥 Популярное</h3>
<div class="grid" id="homeList"></div>
</div>

<!-- FAVORITES -->
<div id="fav" class="page">
<h3 style="padding:10px">❤️ Избранное</h3>
<div class="grid" id="favList"></div>
</div>

<!-- SEARCH -->
<div id="search" class="page">
<input placeholder="Поиск..." oninput="search(this.value)" style="width:90%;margin:10px;padding:10px;">
<div class="grid" id="searchList"></div>
</div>

<!-- ANIME PAGE -->
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
poster:"https://via.placeholder.com/400x600?text=Gyaruko",
episodes:[
"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239021",
"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239022"
]
}
];

/* NAV */
function openPage(id){
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

/* RENDER HOME */
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

/* OPEN ANIME */
function openAnime(a){
openPage("animePage");

const box=document.getElementById("animeInfo");

box.innerHTML=`
<img class="poster" src="${a.poster}">
<h2>${a.title}</h2>
<button onclick='toggleFav(${JSON.stringify(a)})'>❤️ В избранное</button>
<div class="episodes">
${a.episodes.map((v,i)=>`<div class="ep" onclick="play('${v}')">Серия ${i+1}</div>`).join("")}
</div>
`;
}

/* PLAYER */
function play(url){
document.getElementById("frame").src=url;
document.getElementById("player").style.display="flex";
saveContinue(url);
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

/* CONTINUE */
function saveContinue(url){
localStorage.setItem("last",url);
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
