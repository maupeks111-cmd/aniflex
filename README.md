<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body{margin:0;font-family:Arial;background:#000;color:white;overflow:hidden;}

/* интро */
#intro{
position:fixed;inset:0;background:black;
display:flex;justify-content:center;align-items:center;
z-index:9999;flex-direction:column;
animation:fadeOut 1s ease 3s forwards;
}
#intro h1{font-size:50px;color:red;letter-spacing:8px;animation:zoom 2s;}
@keyframes zoom{from{transform:scale(0.5);opacity:0;}to{transform:scale(1);opacity:1;}}
@keyframes fadeOut{to{opacity:0;visibility:hidden;}}

#main{display:none;}
body.loaded #main{display:block;overflow:auto;}

/* фон */
body::before{
content:"";position:fixed;inset:0;
background:url("https://img.freepik.com/premium-photo/japanese-torii-gate-sunset-with-silhouetted-landscape_1282444-100316.jpg");
background-size:cover;z-index:-2;}
body::after{content:"";position:fixed;inset:0;background:rgba(0,0,0,0.6);z-index:-1;}

/* header */
header{display:flex;justify-content:space-between;padding:12px;background:white;border-radius:0 0 20px 20px;}
.logo{color:black;font-weight:bold;}
.search{padding:8px;border-radius:8px;border:none;}

/* grid */
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px;padding:10px;}

.card{
height:220px;border-radius:14px;background-size:cover;
display:flex;align-items:flex-end;padding:10px;
cursor:pointer;position:relative;
}

.card:hover{transform:scale(1.05);}

.title{background:rgba(0,0,0,0.7);padding:5px;border-radius:6px;}
.rating{position:absolute;top:5px;right:5px;background:black;padding:4px;border-radius:6px;font-size:12px;}

/* page */
.page{display:none;padding:10px;}
.ep{background:#1a1a1a;margin:5px;padding:10px;border-radius:10px;cursor:pointer;}
.lock{opacity:0.4;}

/* кнопки */
.btn{padding:8px;margin:5px;background:#222;color:white;border:none;border-radius:8px;cursor:pointer;}
.music-btn{position:fixed;top:10px;right:10px;background:black;padding:10px;border-radius:10px;cursor:pointer;}
.sound-btn{position:fixed;top:60px;right:10px;background:black;padding:10px;border-radius:10px;cursor:pointer;}
</style>
</head>

<body>

<!-- интро -->
<div id="intro"><h1>ANIFLEX</h1></div>

<!-- звуки -->
<audio id="startSound" src="https://assets.mixkit.co/active_storage/sfx/2204/2204-preview.mp3"></audio>
<audio id="bgMusic" loop src="https://cdn.pixabay.com/audio/2022/03/15/audio_c8a1a3c3d3.mp3"></audio>

<audio id="katana" src="https://assets.mixkit.co/active_storage/sfx/2203/2203-preview.mp3"></audio>
<audio id="cat" src="https://assets.mixkit.co/active_storage/sfx/209/209-preview.mp3"></audio>
<audio id="cute" src="https://assets.mixkit.co/active_storage/sfx/2571/2571-preview.mp3"></audio>
<audio id="romance" src="https://assets.mixkit.co/active_storage/sfx/2568/2568-preview.mp3"></audio>
<audio id="drama" src="https://assets.mixkit.co/active_storage/sfx/2570/2570-preview.mp3"></audio>

<div class="music-btn" onclick="toggleMusic()">🎵</div>
<div class="sound-btn" onclick="toggleSound()">🔊</div>

<div id="main">

<header>
<div class="logo">ANIFLEX</div>
<input class="search" placeholder="Поиск..." oninput="search(this.value)">
</header>

<div id="home" class="grid"></div>
<div id="page" class="page"></div>

</div>

<script>

/* запуск */
setTimeout(()=>{
document.body.classList.add("loaded");
startSound.play();
bgMusic.volume=0.3;
bgMusic.play();
},3000);

let musicOn=true;
let soundOn=true;

function toggleMusic(){
musicOn=!musicOn;
musicOn?bgMusic.play():bgMusic.pause();
}

function toggleSound(){
soundOn=!soundOn;
}

/* ДАННЫЕ ВСЕ ВЕРНУЛ */
const data=[

{title:"Клинок рассекающих демонов",poster:"https://i.pinimg.com/originals/95/cf/8d/95cf8d3c3a0e41844941259f4247dc6f.jpg",rating:"⭐9.5",sound:"katana",episodes:Array.from({length:26},(_,i)=>({t:`${i+1} серия (скоро)`,v:""}))},

{title:"Вечера с кошкой",poster:"https://shikimori.io/uploads/poster/animes/51692/main-8f221f4b0e5d093ed375a5f6c8f62a6f.webp",rating:"⭐8.5",sound:"cat",episodes:Array.from({length:30},(_,i)=>({t:`${i+1} серия (скоро)`,v:""}))},

{title:"Гяруко",poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_.jpg",rating:"⭐7.5",sound:"cute",episodes:[{t:"1 серия",v:""}]},

{title:"Фарфоровая кукла",poster:"https://basket-29.wbbasket.ru/vol5784/part578411/578411360/images/big/1.webp",rating:"⭐8.7",sound:"romance",episodes:[{t:"1 серия",v:""}]},

{title:"Сенко-сан",poster:"https://i.pinimg.com/736x/64/97/89/649789acb22b072a7fb783ca173d6408.jpg",rating:"⭐8.0",sound:"cute",episodes:Array.from({length:12},(_,i)=>({t:`${i+1} серия (скоро)`,v:""}))},

{title:"Форма голоса",poster:"https://i.pinimg.com/originals/7f/0d/27/7f0d27d155877e62b2be68952401f329.jpg",rating:"⭐9.0",sound:"drama",episodes:[{t:"Фильм (скоро)",v:""}]}

];

const home=document.getElementById("home");
const page=document.getElementById("page");

function playSound(id){
if(!soundOn)return;
let s=document.getElementById(id);
if(s){s.currentTime=0;s.play();}
}

function render(list){
home.innerHTML="";
list.forEach(item=>{
const i=data.indexOf(item);
const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${item.poster})`;
div.innerHTML=`<div class="rating">${item.rating}</div><div class="title">${item.title}</div>`;
div.onmouseover=()=>playSound(item.sound);
div.onclick=()=>{playSound(item.sound);openAnime(i);};
home.appendChild(div);
});
}

render(data);

function openAnime(i){
home.style.display="none";
page.style.display="block";

let html=`<button class="btn" onclick="back()">⬅ Назад</button>`;
html+=`<h2>${data[i].title}</h2>`;

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
render(data.filter(a=>a.title.toLowerCase().includes(t.toLowerCase())));
}

</script>

</body>
</html>
