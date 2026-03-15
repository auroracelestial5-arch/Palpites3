<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Liga de Palpites</title>

<style>

body{
font-family:Arial;
background:linear-gradient(135deg,#0f172a,#1e293b);
color:white;
margin:0;
text-align:center;
}

header{
background:#020617;
padding:20px;
font-size:24px;
font-weight:bold;
}

nav{
margin-top:10px;
}

nav button{
padding:10px 15px;
margin:5px;
border:none;
border-radius:8px;
background:#22c55e;
color:white;
font-weight:bold;
cursor:pointer;
}

nav button:hover{
background:#16a34a;
}

.section{
display:none;
padding:20px;
}

.active{
display:block;
}

.card{
background:#1e293b;
padding:20px;
border-radius:10px;
margin:auto;
max-width:700px;
}

table{
width:100%;
border-collapse:collapse;
margin-top:15px;
}

th,td{
padding:10px;
border-bottom:1px solid #334155;
}

input{
padding:8px;
border-radius:6px;
border:none;
margin:5px;
}

button.add{
background:#3b82f6;
}

button.point{
background:#22c55e;
}

button.remove{
background:#ef4444;
}

button{
padding:8px 12px;
border:none;
border-radius:6px;
color:white;
cursor:pointer;
}

</style>

</head>

<body>

<header>⚽ Liga de Palpites</header>

<nav>
<button onclick="mostrar('jogos')">Jogos</button>
<button onclick="mostrar('resultados')">Resultados</button>
<button onclick="mostrar('pontos')">Pontuação</button>
</nav>


<div id="jogos" class="section active">

<div class="card">

<h2>Adicionar Jogo</h2>

<input id="time1" placeholder="Time 1">
<input id="time2" placeholder="Time 2">

<br>

<button class="add" onclick="addJogo()">Adicionar</button>

<h3>Lista de Jogos</h3>

<table id="tabelaJogos"></table>

</div>

</div>


<div id="resultados" class="section">

<div class="card">

<h2>Confirmar Resultado</h2>

<table id="tabelaResultados"></table>

</div>

</div>


<div id="pontos" class="section">

<div class="card">

<h2>Ranking</h2>

<table>

<tr>
<th>Jogador</th>
<th>Pontos</th>
<th>+</th>
<th>-</th>
</tr>

<tr>
<td>Endrick</td>
<td id="p1">0</td>
<td><button class="point" onclick="addPonto(0)">+1</button></td>
<td><button class="remove" onclick="removerPonto(0)">-1</button></td>
</tr>

<tr>
<td>Vinicius</td>
<td id="p2">0</td>
<td><button class="point" onclick="addPonto(1)">+1</button></td>
<td><button class="remove" onclick="removerPonto(1)">-1</button></td>
</tr>

</table>

</div>

</div>


<script>

let jogos = JSON.parse(localStorage.getItem("jogos")) || []
let pontos = JSON.parse(localStorage.getItem("pontos")) || [0,0]


function mostrar(sec){

document.querySelectorAll(".section").forEach(s=>s.classList.remove("active"))
document.getElementById(sec).classList.add("active")

}


function addJogo(){

let t1=document.getElementById("time1").value
let t2=document.getElementById("time2").value

if(t1=="" || t2=="") return

jogos.push({t1,t2})

salvar()

}


function addPonto(j){

pontos[j]++

salvar()

}

function removerPonto(j){

if(pontos[j]>0){
pontos[j]--
}

salvar()

}


function salvar(){

localStorage.setItem("jogos",JSON.stringify(jogos))
localStorage.setItem("pontos",JSON.stringify(pontos))

render()

}


function render(){

let tabelaJogos=document.getElementById("tabelaJogos")

tabelaJogos.innerHTML=`
<tr>
<th>Jogo</th>
</tr>
`

jogos.forEach(j=>{

tabelaJogos.innerHTML+=`
<tr>
<td>${j.t1} x ${j.t2}</td>
</tr>
`

})


let tabelaResultados=document.getElementById("tabelaResultados")

tabelaResultados.innerHTML=`
<tr>
<th>Jogo</th>
<th>Dar ponto</th>
</tr>
`

jogos.forEach((j,i)=>{

tabelaResultados.innerHTML+=`
<tr>
<td>${j.t1} x ${j.t2}</td>
<td>
<button class="point" onclick="addPonto(0)">Endrick</button>
<button class="point" onclick="addPonto(1)">Vinicius</button>
</td>
</tr>
`

})


document.getElementById("p1").innerText=pontos[0]
document.getElementById("p2").innerText=pontos[1]

}

render()

</script>

</body>
</html>
