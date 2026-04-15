<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX</title>

<style>
body{
margin:0;
background:#0b0b0f;
color:white;
font-family:Arial;
}

header{
display:flex;
justify-content:space-between;
align-items:center;
padding:10px;
background:black;
position:sticky;
top:0;
z-index:10;
}

.logo{
color:#ff2e63;
font-weight:bold;
font-size:22px;
}

.search{
width:45%;
padding:7px;
border-radius:6px;
border:none;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
gap:10px;
padding:10px;
}

.card{
height:220px;
border-radius:12px;
background-size:cover;
background-position:center;
display:flex;
align-items:flex-end;
padding:10px;
cursor:pointer;
position:relative;
}

.title{
background:rgba(0,0,0,0.6);
padding:5px;
border-radius:6px;
font-size:13px;
}

.page{
display:none;
padding:10px;
}

.ep{
background:#1b1b25;
padding:10px;
margin:5px 0;
border-radius:6px;
}

.lock{
opacity:0.4;
}

.btn{
padding:8px;
background:#222;
color:white;
border:none;
border-radius:6px;
margin:5px;
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

<script>

const data=[
{
title:"Гяруко",
poster:"https://m.media-amazon.com/images/M/MV5BMDYzZGQ4NTUtZjBhNS00ZTJhLTljNDEtOGExOTg2NmJkNmUxXkEyXkFqcGc@._V1_.jpg",
episodes:[
{t:"1 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254283/1_серия_Расскажи_нам_Гяруко_is6ti6.mp4"},
{t:"2 серия",v:"https://res.cloudinary.com/ds3njxeoe/video/upload/v1776254679/2_серия_Расскажи_нам_Гяруко_eroylf.mp4"},
{t:"3 серия",v:""},
{t:"4 серия",v:""},
{t:"5 серия",v:""},
{t:"6 серия",v:""},
{t:"7 серия",v:""},
{t:"8 серия",v:""},
{t:"9 серия (скоро)",v:""},
{t:"10 серия (скоро)",v:""},
{t:"11 серия (скоро)",v:""},
{t:"12 серия (скоро)",v:""}
]
},

{
title:"Фарфоровая кукла (1 сезон)",
poster:"https://basket-29.wbbasket.ru/vol5784/part578411/578411360/images/big/1.webp",
episodes:[
{t:"1 серия (скоро)",v:""},
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
title:"Сенко-сан (1 сезон)",
poster:"https://i.pinimg.com/736x/64/97/89/649789acb22b072a7fb783ca173d6408.jpg",
episodes:[
{t:"1 серия (скоро)",v:""},
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
title:"Форма голоса (фильм)",
poster:"https://static.okko.tv/images/v4/258f2d40-cc36-4c79-a13f-a6ebe3ae6ea8?presetId=4000",
episodes:[
{t:"Фильм (скоро)",v:""}
]
}

];

const home=document.getElementById("home");
const page=document.getElementById("page");

function render(list){
home.innerHTML="";
list.forEach((a,i)=>{
let div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${a.poster})`;

div.innerHTML=`<div class="title">${a.title}</div>`;
div.onclick=()=>open(i);

home.appendChild(div);
});
}

function open(i){
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
let f=data.filter(a=>a.title.toLowerCase().includes(t.toLowerCase()));
render(f);
}

render(data);

</script>

</body>
</html>
