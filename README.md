<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body{margin:0;font-family:Arial;background:#000;color:white;overflow:hidden;}

#intro{
position:fixed;inset:0;background:black;
display:flex;justify-content:center;align-items:center;
z-index:9999;
animation:fadeOut 1s ease 3s forwards;
}

#intro h1{font-size:60px;color:red;letter-spacing:10px;}
@keyframes fadeOut{to{opacity:0;visibility:hidden;}}

#main{display:none;}
body.loaded #main{display:block;overflow:auto;}

body::before{
content:"";position:fixed;inset:0;
background:url("https://img.freepik.com/premium-photo/japanese-torii-gate-sunset-with-silhouetted-landscape_1282444-100316.jpg");
background-size:cover;z-index:-2;}

body::after{
content:"";position:fixed;inset:0;
background:rgba(0,0,0,0.6);z-index:-1;
}

header{
display:flex;justify-content:space-between;
padding:12px;background:white;
}
.logo{color:black;font-weight:bold;}
.search{padding:8px;border-radius:8px;border:none;}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
gap:10px;padding:10px;
}

.card{
height:220px;
background-size:cover;
border-radius:14px;
display:flex;
align-items:flex-end;
padding:10px;
cursor:pointer;
position:relative;
}

.card::before{
content:"";position:absolute;inset:0;
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
top:8px;right:8px;
background:black;
padding:4px 6px;
border-radius:6px;
font-size:12px;
}

.page{display:none;padding:10px;}

.info{
display:flex;gap:15px;
background:#1c1c1c;
padding:15px;
border-radius:15px;
}

.info img{width:140px;border-radius:10px;}
.ep{background:#1a1a1a;margin:6px 0;padding:10px;border-radius:10px;cursor:pointer;}
.lock{opacity:0.4;}
.btn{padding:8px;margin:5px;background:#222;color:white;border:none;border-radius:8px;cursor:pointer;}
</style>
</head>

<body>

<div id="intro"><h1>ANIFLEX</h1></div>

<audio id="startSound" src="https://assets.mixkit.co/active_storage/sfx/2204/2204-preview.mp3"></audio>

<div id="main">

<header>
<div class="logo">ANIFLEX</div>
<input class="search" placeholder="Поиск..." oninput="search(this.value)">
</header>

<div id="home" class="grid"></div>
<div id="page" class="page"></div>

</div>

<script>

setTimeout(()=>{
document.body.classList.add("loaded");
startSound.play();
},3000);

/* ===== ДАННЫЕ ===== */
const data=[

{
title:"Клинок рассекающих демонов",
poster:"https://i.pinimg.com/originals/95/cf/8d/95cf8d3c3a0e41844941259f4247dc6f.jpg",
rating:"⭐ 9.5",
desc:"1 сезон — 26 серий.",
episodes:Array.from({length:26},(_,i)=>({t:`${i+1} серия (скоро)`,v:""}))
},

{
title:"Вечера с кошкой",
poster:"https://shikimori.io/uploads/poster/animes/51692/main-8f221f4b0e5d093ed375a5f6c8f62a6f.webp",
rating:"⭐ 8.5",
desc:"1 сезон — 30 серий.",
episodes:Array.from({length:30},(_,i)=>({t:`${i+1} серия (скоро)`,v:""}))
},

{
title:"Гяруко",
poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_.jpg",
rating:"⭐ 7.5",
desc:"1 сезон — 12 серий.",
episodes:[
{t:"1 серия (наша озвучка)",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/1_серия_Расскажи_нам_Гяруко_is6ti6.mp4"},
{t:"2 серия (наша озвучка)",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254679/2_серия_Расскажи_нам_Гяруко_eroylf.mp4"},
{t:"3 серия (наша озвучка)",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254741/3_серия_Расскажи_нам_Гяруко_ibivet.mp4"},
{t:"4 серия (наша озвучка)",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254759/4_серия_Расскажи_нам_Гяруко_qzigwl.mp4"},
{t:"5 серия (наша озвучка)",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254740/5_серия_Расскажи_нам_Гяруко_crtolw.mp4"},
{t:"6 серия (наша озвучка)",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254747/6_серия_Расскажи_нам_Гяруко_jhnztd.mp4"},
{t:"7 серия (наша озвучка)",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254735/7_серия_Расскажи_нам_Гяруко_qhbmlj.mp4"},
{t:"8 серия (наша озвучка)",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254751/8_серия_Расскажи_нам_Гяруко_wsdrnn.mp4"},
{t:"9 серия (скоро)",v:""},
{t:"10 серия (скоро)",v:""},
{t:"11 серия (скоро)",v:""},
{t:"12 серия (скоро)",v:""}
]
},

{
title:"Фарфоровая кукла",
poster:"https://basket-29.wbbasket.ru/vol5784/part578411/578411360/images/big/1.webp",
rating:"⭐ 8.7",
desc:"12 серий сезон.",
episodes:[
{t:"1 серия (наша озвучка)",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/VID_20260416_110510_423_o8ndmt.mp4"},
...Array.from({length:11},(_,i)=>({t:`${i+2} серия (скоро)`,v:""}))
]
},

{
title:"Сенко-сан",
poster:"https://i.pinimg.com/736x/64/97/89/649789acb22b072a7fb783ca173d6408.jpg",
rating:"⭐ 8.0",
desc:"1 сезон — 12 серий.",
episodes:Array.from({length:12},(_,i)=>({t:`${i+1} серия (скоро)`,v:""}))
},

{
title:"Форма голоса",
poster:"https://i.pinimg.com/originals/7f/0d/27/7f0d27d155877e62b2be68952401f329.jpg",
rating:"⭐ 9.0",
desc:"Полнометражный фильм.",
episodes:[{t:"Фильм",v:""}]
}

];

const home=document.getElementById("home");
const page=document.getElementById("page");

function render(list){
home.innerHTML="";
list.forEach(item=>{
const i=data.indexOf(item);

const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${item.poster})`;
div.innerHTML=`
<div class="rating">${item.rating}</div>
<div class="title">${item.title}</div>
`;
div.onclick=()=>openAnime(i);
home.appendChild(div);
});
}

render(data);

/* ===== ОТКРЫТИЕ ===== */
function openAnime(i){
home.style.display="none";
page.style.display="block";

let html=`<button class="btn" onclick="back()">⬅ Назад</button>`;

html+=`
<div class="info">
<img src="${data[i].poster}">
<div>
<h2>${data[i].title}</h2>
<p>${data[i].desc}</p>
<div>${data[i].rating}</div>
</div>
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
render(data.filter(a=>a.title.toLowerCase().includes(t.toLowerCase())));
}

</script>

</body>
</html>
