<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Para Ti ❤️</title>
<style>
  :root{
    --bg-1: #6a0f3a;
    --bg-2: #d6006e;
    --card-bg: #f4ead9;
    --text-color: #3a2b20;
    --accent: #e0245e;
    --tronco: #6b4226;
  }
  *{ box-sizing: border-box; margin:0; padding:0; }
  body{
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    font-family: 'Segoe UI', Tahoma, Verdana, sans-serif;
    background: radial-gradient(circle at 50% 20%, var(--bg-2), var(--bg-1) 70%);
    overflow:hidden;
    position:relative;
  }
  .titulo{ color:#fff; font-size:1.4rem; text-align:center; margin-bottom:18px; }
  .contenedor{ width:92vw; max-width:520px; }
  .tarjeta{
    background: var(--card-bg);
    border-radius: 24px;
    padding: 30px 26px 20px;
    box-shadow: 0 20px 50px rgba(0,0,0,0.4);
    min-height: 480px;
    position:relative;
  }
  .mensaje{ color:var(--text-color); font-size:1.05rem; line-height:1.7; min-height:150px; }
  .escenario{ position:relative; width:100%; height:260px; margin-top:10px; }
  .suelo{ position:absolute; bottom:30px; width:100%; height:2px; background:var(--text-color); opacity:0.6; }
  .tronco{
    position:absolute; bottom:32px; left:50%; transform:translateX(-50%) scaleY(0);
    transform-origin:bottom; width:14px; height:140px; background:var(--tronco);
    border-radius:6px 6px 0 0; animation: crecerTronco 1.8s ease-out forwards; animation-delay:.3s;
  }
  .tronco::before,.tronco::after{
    content:""; position:absolute; bottom:20px; width:10px; height:60px; background:var(--tronco); border-radius:6px;
  }
  .tronco::before{ left:-8px; transform:rotate(25deg); transform-origin:bottom; }
  .tronco::after{ right:-8px; transform:rotate(-25deg); transform-origin:bottom; }
  @keyframes crecerTronco{ to{ transform:translateX(-50%) scaleY(1);} }
  .copa{ position:absolute; bottom:120px; left:50%; transform:translateX(-50%); width:260px; height:220px; }
  .copa span{ position:absolute; font-size:0; opacity:0; transform:scale(0); animation:florecer .6s ease-out forwards; }
  .copa span::before{ content:"❤️"; }
  @keyframes florecer{ to{ opacity:1; transform:scale(1); font-size:var(--tam,16px);} }
  .petalo{ position:absolute; color:var(--accent); font-size:14px; opacity:0.9; animation:caer 4s linear forwards; }
  @keyframes caer{ 0%{ transform:translate(0,0) rotate(0deg);} 100%{ transform:translate(-90px,180px) rotate(200deg); opacity:0;} }
  .contador-wrap{ margin-top:14px; color:var(--text-color); font-size:0.9rem; }
  .contador{ font-weight:bold; font-size:1rem; color:var(--accent); }
</style>
</head>
<body>

  <h1 class="titulo" id="tituloPersona"> ERIKA YULIANA  </h1>

  <div class="contenedor">
    <div class="tarjeta">
      <div class="mensaje" id="mensaje"></div>
      <div class="escenario">
        <div class="suelo"></div>
        <div class="tronco"></div>
        <div class="copa" id="copa"></div>
      </div>
      <div class="contador-wrap">
        Mi amor por ti comenzó hace...<br>
        <span class="contador" id="contador">calculando...</span>
      </div>
    </div>
  </div>

<script>
// Nombre arriba
document.getElementById('tituloPersona').textContent = "ERIKA YULIANA";

// Mensajes románticos
const mensajes = [
  "Para el amor de mi vida:",
  "",
  "Si pudiera elegir un lugar seguro, sería a tu lado.",
  "Cuanto más tiempo estoy contigo más te amo.",
  "",
  "Gracias por existir y por quererme como lo haces."
];
const contMensaje = document.getElementById('mensaje');
mensajes.forEach((texto, i)=>{
  const p = document.createElement('p');
  p.textContent = texto;
  contMensaje.appendChild(p);
});

// Copa del árbol en forma de corazón
const copa = document.getElementById('copa');
const centroX = 130, centroY = 110, escala = 6.2;
const colores = ['#e0245e','#ff6b81','#c81e4a','#ff98a8','#b8123f'];
for(let t=0;t<Math.PI*2;t+=0.28){
  const x=16*Math.pow(Math.sin(t),3);
  const y=-(13*Math.cos(t)-5*Math.cos(2*t)-2*Math.cos(3*t)-Math.cos(4*t));
  for(let r=0.3;r<=1;r+=0.22){
    const span=document.createElement('span');
    span.style.left=(centroX+x*escala*r+(Math.random()*10-5))+'px';
    span.style.top=(centroY+y*escala*r+(Math.random()*10-5))+'px';
    span.style.color=colores[Math.floor(Math.random()*colores.length)];
    span.style.setProperty('--tam',(14+Math.random()*12)+'px');
    span.style.animationDelay=(1.4+Math.random()*1.4)+'s';
    copa.appendChild(span);
  }
}
function crearPetalo(){
  const p=document.createElement('div');
  p.className='petalo'; p.textContent='❤️';
  p.style.left=(100+Math()*100)+"PX"
  p.style.top=(60+Math.random()*80)+'px';
  p.style.fontSize=(10+Math.random()*10)+'px';
  copa.appendChild(p);
  setTimeout(()=>p.remove(),4000);
}
setInterval(crearPetalo,900);

// Contador desde 5 mayo 2025
const fechaInicio=new Date(2025,4,5,0,0,0);
const elContador=document.getElementById('contador');
function actualizarContador(){
  const ahora=new Date();
  if(ahora<fechaInicio){ elContador.textContent="¡el gran día aún no llega!"; return; }
  let años=ahora.getFullYear()-fechaInicio.getFullYear();
  let meses=ahora.getMonth()-fechaInicio.getMonth();
  let dias=ahora.getDate()-fechaInicio.getDate();
  if(dias<0){ meses--; const ultimoMes=new Date(ahora.getFullYear(),ahora.getMonth(),0).getDate(); dias+=ultimoMes; }
  if(meses<0){ años--; meses+=12; }
  const diffMs=ahora-fechaInicio;
  const diffSegundos=Math.floor(diffMs/1000);
  const horas=Math.floor((diffSegundos%86400)/3600);
  const minutos=Math.floor((diffSegundos%3600)/60);
  const segundos=diffSegundos%60;
  elContador.textContent=`${años} años ${meses} meses ${dias} días ${horas} horas ${minutos} minutos ${segundos} segundos`;
}
actualizarContador();
setInterval(actualizarContador,1000);
</script>
</body>
</html>
