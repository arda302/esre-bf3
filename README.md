<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<title>Esre Sürprizi</title>
<style>
body{
  margin:0;
  background:black;
  height:100vh;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  font-family:Arial;
  color:white;
  overflow:hidden;
  text-align:center;
}

#boot{
  font-size:60px;
  opacity:0;
  transform:scale(0.5);
  animation:boot 2s forwards;
}

#text{
  font-size:40px;
  margin-top:20px;
  opacity:0;
  transform:translateY(20px);
  animation:textAppear 2s forwards;
  animation-delay:2s;
}

button{
  margin-top:40px;
  padding:15px 35px;
  font-size:20px;
  border:none;
  border-radius:10px;
  background:#ff4d88;
  color:white;
  cursor:pointer;
  opacity:0;
  transform:translateY(20px);
  animation:showButton 2s forwards;
  animation-delay:4s;
}

canvas{
  position:fixed;
  top:0;
  left:0;
}

.heart{position:fixed;font-size:24px;animation:float 6s linear infinite;}
.rose{position:fixed;font-size:24px;animation:fall 7s linear infinite;}

@keyframes boot{
  from{opacity:0; transform:scale(0.5);}
  to{opacity:1; transform:scale(1);}
}

@keyframes textAppear{
  from{opacity:0; transform:translateY(20px);}
  to{opacity:1; transform:translateY(0);}
}

@keyframes showButton{
  from{opacity:0; transform:translateY(20px);}
  to{opacity:1; transform:translateY(0);}
}

@keyframes float{
  from{transform:translateY(100vh);}
  to{transform:translateY(-10vh);}
}

@keyframes fall{
  from{transform:translateY(-10vh);}
  to{transform:translateY(100vh);}
}
</style>
</head>
<body>

<div id="boot">💖 Esre BF 💖</div>
<div id="text">Esre Seni Seviyorum</div>
<button onclick="startParty()">Sürprizi Aç 🎆</button>

<audio id="music" loop src="https://cdn.pixabay.com/audio/2022/03/15/audio_7c6a67c6c4.mp3"></audio>
<canvas id="fireworks"></canvas>

<script>
const canvas = document.getElementById("fireworks");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
let particles = [];

function firework(){
  let x = Math.random()*canvas.width;
  let y = Math.random()*canvas.height/2;
  for(let i=0;i<80;i++){
    particles.push({
      x:x, y:y,
      angle:Math.random()*2*Math.PI,
      speed:Math.random()*5+2,
      life:100
    });
  }
}

function animate(){
  ctx.fillStyle="rgba(0,0,0,0.1)";
  ctx.fillRect(0,0,canvas.width,canvas.height);
  particles.forEach((p,i)=>{
    p.x += Math.cos(p.angle)*p.speed;
    p.y += Math.sin(p.angle)*p.speed;
    p.life--;
    ctx.beginPath();
    ctx.arc(p.x,p.y,2,0,Math.PI*2);
    ctx.fillStyle = `hsl(${Math.random()*360},100%,60%)`;
    ctx.fill();
    if(p.life<=0) particles.splice(i,1);
  });
  requestAnimationFrame(animate);
}

function createHeart(){
  const heart = document.createElement("div");
  heart.className = "heart";
  heart.innerHTML = "💖";
  heart.style.left = Math.random()*100 + "vw";
  document.body.appendChild(heart);
  setTimeout(()=>heart.remove(),6000);
}

function createRose(){
  const rose = document.createElement("div");
  rose.className = "rose";
  rose.innerHTML = "🌹";
  rose.style.left = Math.random()*100 + "vw";
  document.body.appendChild(rose);
  setTimeout(()=>rose.remove(),7000);
}

function startParty(){
  document.getElementById("music").play();
  setInterval(firework,700);
  setInterval(createHeart,500);
  setInterval(createRose,800);
}

animate();
</script>
</body>
</html>
