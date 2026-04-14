<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANIFLEX FINAL 7.0</title>

<style>
body{
margin:0;
font-family:Arial;
background:#0b0b0b;
color:white;
}

header{
display:flex;
justify-content:space-between;
padding:10px;
background:black;
}

.logo{color:red;font-weight:bold}

/* LOGIN */
#login{
display:flex;
flex-direction:column;
gap:10px;
padding:20px;
}

input{
padding:10px;
border:none;
border-radius:6px;
}

button{
padding:10px;
border:none;
background:red;
color:white;
}

/* HOME */
#app{
display:none;
}

.grid{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:10px;
padding:10px;
}

.card{
height:250px;
border-radius:12px;
background-size:cover;
background-position:center;
position:relative;
cursor:pointer;
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

</style>
</head>

<body>

<header>
<div class="logo">ANIFLEX FINAL 7.0</div>
<button onclick="logout()">Выйти</button>
</header>

<!-- LOGIN -->
<div id="login">
<h3>Вход</h3>
<input id="user" placeholder="логин">
<input id="pass" type="password" placeholder="пароль">
<button onclick="login()">Войти / создать</button>
</div>

<!-- APP -->
<div id="app">

<h3 style="padding:10px">🔥 Популярное</h3>
<div class="grid" id="list"></div>

</div>

<!-- PLAYER -->
<div class="player" id="player">
<iframe id="frame"></iframe>
<button onclick="closePlayer()">Закрыть</button>
</div>

<script>

const anime = [
{
title:"Гяруко 1",
poster:"https://via.placeholder.com/400x600?text=Ep1",
video:"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239021"
},
{
title:"Гяруко 2",
poster:"https://via.placeholder.com/400x600?text=Ep2",
video:"https://vkvideo.ru/video_ext.php?oid=-229445104&id=456239022"
}
];

/* LOGIN SYSTEM (LOCAL) */
function login(){
let u=document.getElementById("user").value;
let p=document.getElementById("pass").value;

if(!u||!p) return;

localStorage.setItem("user",u);
document.getElementById("login").style.display="none";
document.getElementById("app").style.display="block";
render();
}

function logout(){
localStorage.removeItem("user");
location.reload();
}

if(localStorage.getItem("user")){
document.getElementById("login").style.display="none";
document.getElementById("app").style.display="block";
}

/* RENDER */
function render(){
const list=document.getElementById("list");
list.innerHTML="";

anime.forEach(a=>{
const div=document.createElement("div");
div.className="card";
div.style.backgroundImage=`url(${a.poster})`;
div.innerHTML=`<span>${a.title}</span>`;
div.onclick=()=>play(a.video);
list.appendChild(div);
});
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

</script>

</body>
</html>
