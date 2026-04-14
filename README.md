<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

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
height:220px;
background:url('https://avatars.mds.yandex.net/i?id=4860fda7eb409a1b1179e9239913ff1f3dd36462-5877782-images-thumbs&n=13') center/cover;
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
.page{display:none;padding-bottom:80px;}
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
background:linear-gradient(to top, rgba(0,0,0,0.9), transparent);
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
padding:10px;
margin:8px 0;
border-radius:10px;
}

/* FOOTER LINKS */
.links{
padding:15px;
text-align:center;
}

.links a{
display:block;
margin:6px 0;
color:#ff4444;
text-decoration:none;
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

<header>ANIFLEX 🔥</header>

<div class="hero">
🔥 Смотри аниме бесплатно
</div>

<!-- HOME -->
<div id="home" class="page active">
<div class="grid" id="homeList"></div>

<div class="links">
<a href="https://vk.com/aniflex1" target="_blank">📺 ВКонтакте</a>
<a href="https://t.me/Animeflex1x" target="_blank">📱 Telegram</a>
<a href="https://www.donationalerts.com/r/LaunchPlay" target="_blank">💰 Поддержать проект</a>
</div>

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
title:"Гяруко",
poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_FMjpg_UX1000_.jpg",
episodes:[
{
title:"1 серия",
video:"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239021",
cover:"https://yandex-images.clstorage.net/Ii9c8C399/d60fcciCh/rQqUhoSLel_Ps7xkurUsfpd0sRARpT-IKj96nVQsjrwEFwiMS4lhyDuYNnp51gWxLzt-dmS1MYmJOPBQo-IozOgP9ZPZmgNDz6ftSJOFRE7XIYFlHfA37DoiHq1RmHY8kdKpeeZsuXXn7X8XLJc0mDoK194x6OkptAXRoHs7tbGJ3kTCUMv_Q0tz2WS-rTg2K6HtzKFkOzVa30tciTBKZNF6SQVi7Pl9841PMxyr0azGPvszGVipsSihFVQXM4mtrf6chrjno0NfC224nmV8QotVERzVSBd93h9bXFE80pghekXdsiixVQOdx_s0xxEMbm6Te42AvRWc5Zksm9_JobUGWPLcV5e3769ZEE5p2Ia_qR2cJdyjccYXz9BFYLZQfZYR6W4MgYnHkbs3kBsx7BI6e4uJfA0VxDGFZGMXgd2NyizatEtva1vz7cwKVSTOt1HRNMnEa8X2348otYDebFnisdXm-B2V-ykrSwSfybB24kMnZURdZYwl8dAba1GViRZMRtRzC09TQ1GEWqnY0tMJIXgRnJ-dytuPiMXYvuQ1_t0ZsoxFnZutt2e0v7UAzgITl-F4RcXErd0EhwcpkbXuoLYIRwu_6wfhFEaNfLKHNR045XzD6WIPe9SFJBo0fcZFcXJ4Zf2bOfOjLJ-FJCZWn7OFtHUtiKWJkG_H3ZGV1qRuLNufgz9jJTiaCXRm4z1B9GHQuzFmM3e8EaAWtJ2CDfHmQAGBfx1TB1xDSbzOxp8n9XBVoSBpcZADD3VJjeqwllRHo3v3g8GQcomI4gfJXWRJKBchFktjqF1o0qjJ9kWlnpC9XcOls4_w2zHEbsK_S9lwbe3wZVXMl2c9fYWK9Fqc-_9Lk3-lDMrVfN5Lhb04LXwffYLLq6iV_AJoAZ4FTX6YKdlTEWtH1K8ZCN7aM69RfDUlnMk5RJ-3WdUZlqTSQFu_Sy8ndbgaNUjKyzGtJKl8UyEGp_vwtXC4"
},
{
title:"2 серия",
video:"https://vkvideo.ru/video-229445104_456239024?list=ln-plbjQjvrGCiaeNiuek",
cover:"http://avatars.mds.yandex.net/get-vthumb/4568404/7d84b187d1b46b6320f74b6789f9b2ed/800x450"
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

</script>

</body>
</html>
