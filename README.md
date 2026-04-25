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

.rating{
position:absolute;
top:8px;
right:8px;
background:rgba(0,0,0,0.7);
padding:4px 6px;
border-radius:6px;
font-size:12px;
}

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

/* кнопка звука */
.sound-toggle{
position:fixed;
bottom:15px;
right:15px;
background:#111;
padding:10px;
border-radius:10px;
cursor:pointer;
z-index:1000;
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

<!-- 🔊 звуки -->
<audio id="cardSound" src="https://assets.mixkit.co/active_storage/sfx/2571/2571-preview.mp3"></audio>
<audio id="btnSound" src="https://assets.mixkit.co/active_storage/sfx/2568/2568-preview.mp3"></audio>
<audio id="epSound" src="https://assets.mixkit.co/active_storage/sfx/2570/2570-preview.mp3"></audio>

<div class="sound-toggle" onclick="toggleSound()">🔊</div>

<script>

let soundEnabled = true;
let gameMode = false;

const cardSound = document.getElementById("cardSound");
const btnSound = document.getElementById("btnSound");
const epSound = document.getElementById("epSound");

/* громкость режимов */
function updateVolume(){
let vol = gameMode ? 1 : 0.5;
cardSound.volume = vol;
btnSound.volume = vol;
epSound.volume = vol;
}
updateVolume();

function toggleSound(){
soundEnabled = !soundEnabled;
document.querySelector(".sound-toggle").innerText = soundEnabled ? "🔊" : "🔇";
}

/* двойной клик = игровой режим */
document.querySelector(".sound-toggle").ondblclick = ()=>{
gameMode = !gameMode;
updateVolume();
};

/* hover */
document.addEventListener("mouseover", (e)=>{
if(!soundEnabled) return;

if(e.target.closest(".card")){
cardSound.currentTime=0; cardSound.play();
}
if(e.target.closest(".btn") || e.target.closest(".nav button")){
btnSound.currentTime=0; btnSound.play();
}
if(e.target.closest(".ep")){
epSound.currentTime=0; epSound.play();
}
});

/* click */
document.addEventListener("click", (e)=>{
if(!soundEnabled) return;

if(e.target.closest(".card")){
cardSound.currentTime=0; cardSound.play();
}
if(e.target.closest(".btn") || e.target.closest(".nav button")){
btnSound.currentTime=0; btnSound.play();
}
if(e.target.closest(".ep")){
epSound.currentTime=0; epSound.play();
}
});

</script>

</body>
</html>
