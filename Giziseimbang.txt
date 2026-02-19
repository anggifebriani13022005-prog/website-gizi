<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gizi Seimbang Interaktif</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',sans-serif}
body{background:#f4f7fa;scroll-behavior:smooth}

/* ================= LOADER ================= */
#loader{
position:fixed;
width:100%;
height:100vh;
background:linear-gradient(120deg,#2e8b57,#ff8c00);
display:flex;
justify-content:center;
align-items:center;
z-index:9999;
color:white;
font-size:22px;
flex-direction:column;
}
.spinner{
width:60px;
height:60px;
border:6px solid rgba(255,255,255,0.3);
border-top:6px solid white;
border-radius:50%;
animation:spin 1s linear infinite;
margin-bottom:15px;
}
@keyframes spin{
100%{transform:rotate(360deg)}
}

/* NAVBAR */
nav{
position:fixed;width:100%;top:0;
background:rgba(46,139,87,0.9);
backdrop-filter:blur(10px);
padding:15px;text-align:center;z-index:1000}
nav a{color:white;text-decoration:none;margin:0 20px;font-weight:600}
nav a:hover{color:#ffd700}

/* HERO */
.hero{
height:100vh;
background:linear-gradient(120deg,#2e8b57,#ff8c00);
display:flex;justify-content:center;align-items:center;
text-align:center;color:white;padding:20px}
.hero h1{font-size:3rem}

/* SECTION */
section{padding:100px 20px;max-width:1100px;margin:auto}
h2{text-align:center;margin-bottom:40px;color:#2e8b57}

/* CARD */
.card{
background:white;padding:25px;margin:20px 0;
border-radius:15px;
box-shadow:0 8px 20px rgba(0,0,0,0.08);
transition:.4s}
.card:hover{
transform:translateY(-10px);
box-shadow:0 15px 30px rgba(0,0,0,0.15)}

/* ================= 3D PLATE ================= */
.plate-container{
display:flex;justify-content:center;align-items:center;
perspective:1000px;
}
.plate{
width:350px;height:350px;border-radius:50%;
background:radial-gradient(circle at 50% 50%, #fff 60%, #ddd 100%);
box-shadow:0 20px 40px rgba(0,0,0,0.3);
position:relative;
transform-style:preserve-3d;
transition:1s;
}
.plate:hover{
transform:rotateX(15deg) rotateY(15deg);
}

.food{
position:absolute;
width:50%;height:50%;
border-radius:50%;
}

.sayur{
background:linear-gradient(145deg,#66bb6a,#2e7d32);
top:0;left:0;
}
.buah{
background:linear-gradient(145deg,#ef5350,#c62828);
top:0;right:0;
}
.karbo{
background:linear-gradient(145deg,#ffa726,#ef6c00);
bottom:0;left:0;
}
.protein{
background:linear-gradient(145deg,#42a5f5,#1565c0);
bottom:0;right:0;
}

/* QUIZ */
.quiz-question{
font-weight:bold;margin-bottom:15px}
.quiz-options button{
display:block;width:100%;
margin:8px 0;
background:#2e8b57;color:white;border:none;
padding:10px;border-radius:8px;
cursor:pointer;transition:.3s}
.quiz-options button:hover{
background:#1b5e20}

.result{
margin-top:15px;font-weight:bold}

/* FOOTER */
footer{
background:#2e8b57;color:white;text-align:center;padding:20px}
</style>
</head>

<body>

<!-- LOADER -->
<div id="loader">
<div class="spinner"></div>
Memuat Edukasi Gizi...
</div>

<nav>
<a href="#piring">Isi Piringku</a>
<a href="#quiz">Quiz Gizi</a>
</nav>

<div class="hero">
<div>
<h1>Gizi Seimbang Interaktif</h1>
<p>Edukasi Digital Modern</p>
</div>
</div>

<!-- ================= 3D ISI PIRINGKU ================= -->
<section id="piring">
<h2>Ilustrasi “Isi Piringku” 3D</h2>
<div class="plate-container">
<div class="plate">
<div class="food sayur"></div>
<div class="food buah"></div>
<div class="food karbo"></div>
<div class="food protein"></div>
</div>
</div>
<p style="text-align:center;margin-top:20px">
Hijau: Sayur | Merah: Buah | Oranye: Karbohidrat | Biru: Protein
</p>
</section>

<!-- ================= QUIZ ================= -->
<section id="quiz">
<h2>Quiz Edukasi Gizi</h2>

<div class="card">
<div class="quiz-question" id="question"></div>
<div class="quiz-options" id="options"></div>
<div class="result" id="result"></div>
</div>

</section>

<footer>
<p>© 2026 Edukasi Gizi Seimbang Interaktif</p>
</footer>

<script>
/* LOADER */
window.addEventListener("load",()=>{
setTimeout(()=>{
document.getElementById("loader").style.display="none";
},1500);
});

/* QUIZ DATA */
const quizData=[
{
question:"Apa yang termasuk sumber protein?",
options:["Nasi","Tempe","Gula","Minyak"],
correct:1
},
{
question:"Berapa menit aktivitas fisik dianjurkan per hari?",
options:["10 menit","15 menit","30 menit","5 menit"],
correct:2
},
{
question:"Setengah isi piring dianjurkan berisi?",
options:["Protein","Karbohidrat","Sayur dan buah","Gula"],
correct:2
}
];

let currentQuestion=0;
let score=0;

function loadQuiz(){
const q=quizData[currentQuestion];
document.getElementById("question").innerText=q.question;

const optionsDiv=document.getElementById("options");
optionsDiv.innerHTML="";

q.options.forEach((option,index)=>{
const btn=document.createElement("button");
btn.innerText=option;
btn.onclick=()=>checkAnswer(index);
optionsDiv.appendChild(btn);
});
}

function checkAnswer(index){
if(index===quizData[currentQuestion].correct){
score++;
}
currentQuestion++;

if(currentQuestion<quizData.length){
loadQuiz();
}else{
document.getElementById("question").innerText="Quiz Selesai!";
document.getElementById("options").innerHTML="";
document.getElementById("result").innerText=
"Skor Anda: "+score+" dari "+quizData.length;
}
}

loadQuiz();
</script>

</body>
</html>
