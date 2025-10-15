<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>AMCOIN Spinner</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body { margin:0; overflow:hidden; background:#041226; color:#fff; font-family:sans-serif; touch-action: none; }
canvas { display:block; background:#061024; }
#ui { position:absolute; top:10px; left:10px; z-index:10; }
#menu { position:absolute; top:50%; left:50%; transform:translate(-50%,-50%); background:rgba(0,0,0,0.6); padding:20px; border-radius:12px; text-align:center; }
#menu input { padding:6px 10px; border-radius:6px; border:none; margin-bottom:10px; width:120px; text-align:center;}
#menu button { padding:6px 12px; border-radius:6px; border:none; cursor:pointer; background:#4d96ff; color:#fff; font-weight:bold; }
</style>
</head>
<body>
<div id="ui">
  <div id="score">Очки: 0</div>
  <div id="leaderboard"><b>Топ:</b></div>
</div>
<div id="menu">
  <div>Введите имя:</div>
  <input id="nameInput" type="text" placeholder="Игрок">
  <br>
  <button id="startBtn">Старт</button>
</div>
<canvas id="game"></canvas>
<script>
const canvas=document.getElementById('game');
const ctx=canvas.getContext('2d');
let w=window.innerWidth,h=window.innerHeight;
canvas.width=w; canvas.height=h;
window.addEventListener('resize',()=>{w=window.innerWidth;h=window.innerHeight;canvas.width=w;canvas.height=h;});

function rand(a,b){return a+Math.random()*(b-a);}
function randomColor(){const c=['#ff6b6b','#ffd166','#06d6a0','#4d96ff','#c792ea','#ff8fab'];return c[Math.floor(Math.random()*c.length)];}

class Spinner {
  constructor(name,x,y,isPlayer=false){
    this.name=name; this.x=x; this.y=y;
    this.vx=0; this.vy=0;
    this.radius=30;  
    this.mass=this.radius*this.radius;
    this.color=randomColor();
    this.isPlayer=isPlayer;
    this.angle=Math.random()*Math.PI*2; 
    this.spinSpeed=15; 
    this.alive=true;
    this.trail=[];
  }
  update(dt){
    this.x+=this.vx*dt; this.y+=this.vy*dt;
    this.vx*=0.98; this.vy*=0.98;
    if(this.x<this.radius){this.x=this.radius;this.vx*=-0.4;}
    if(this.y<this.radius){this.y=this.radius;this.vy*=-0.4;}
    if(this.x>w-this.radius){this.x=w-this.radius;this.vx*=-0.4;}
    if(this.y>h-this.radius){this.y=h-this.radius;this.vy*=-0.4;}
    this.angle+=this.spinSpeed*dt;

    // добавляем позицию для следа
    this.trail.push({x:this.x, y:this.y, alpha:0.4});
    if(this.trail.length>30) this.trail.shift();
    this.trail.forEach(p=>p.alpha-=0.015);
    this.trail=this.trail.filter(p=>p.alpha>0);
  }
  draw(ctx){
    // рисуем след
    this.trail.forEach(p=>{
      ctx.beginPath();
      ctx.arc(p.x,p.y,this.radius*0.6,0,Math.PI*2);
      ctx.fillStyle=`rgba(255,255,255,${p.alpha})`;
      ctx.fill();
    });

    ctx.save();
    ctx.translate(this.x,this.y);
    ctx.rotate(this.angle);
    for(let i=0;i<3;i++){
      ctx.beginPath();
      ctx.moveTo(0,0);
      ctx.lineTo(this.radius,0);
      ctx.lineWidth=4;
      ctx.strokeStyle=this.color;
      ctx.stroke();
      ctx.rotate(Math.PI*2/3);
    }
    ctx.restore();

    ctx.fillStyle="#fff";
    ctx.font=`16px sans-serif`; ctx.textAlign='center';
    ctx.fillText(this.name,this.x,this.y-this.radius-8);
    ctx.fillText(Math.round(this.mass),this.x,this.y+this.radius+16);
  }
}

class Bonus {
  constructor(x,y,type){
    this.x=x; this.y=y; this.radius=10; this.type=type;
    this.color=type==='boost'?'#ffd166':'#06d6a0';
    this.alive=true;
  }
  draw(ctx){
    ctx.beginPath(); ctx.arc(this.x,this.y,this.radius,0,Math.PI*2);
    ctx.fillStyle=this.color; ctx.fill(); ctx.strokeStyle="#fff"; ctx.stroke();
  }
}

let player=null;
let bots=[];
let bonuses=[];
let pointer={x:0,y:0,down:false};
let leaderboard=[];

function spawnGame(name){
  player=new Spinner(name,w/2,h/2,true);
  bots=[]; for(let i=0;i<6;i++){bots.push(new Spinner('Bot'+(i+1),rand(50,w-50),rand(50,h-50)));}
  bonuses=[]; for(let i=0;i<5;i++){bonuses.push(new Bonus(rand(50,w-50),rand(50,h-50),Math.random()<0.5?'boost':'points'));}
  leaderboard=[];
}

function handleCollisions(arr){
  for(let i=0;i<arr.length;i++){
    for(let j=i+1;j<arr.length;j++){
      const a=arr[i],b=arr[j];
      const dx=b.x-a.x,dy=b.y-a.y,dist=Math.hypot(dx,dy);
      if(dist<a.radius+b.radius){
        let winner=a.mass>=b.mass?a:b; let loser=winner===a?b:a;
        let transfer=loser.mass*0.7; winner.mass+=transfer; winner.radius=Math.sqrt(winner.mass);
        loser.mass-=transfer; loser.radius=Math.sqrt(loser.mass);
        if(loser.mass<24)loser.alive=false;
        const overlap=(a.radius+b.radius)-dist;
        const nx=dx/dist,ny=dy/dist;
        a.x-=nx*overlap*0.5;a.y-=ny*overlap*0.5; b.x+=nx*overlap*0.5;b.y+=ny*overlap*0.5;
      }
    }
  }
}

function handleBonuses(){
  bonuses.forEach(b=>{
    if(!b.alive) return;
    const dx=player.x-b.x, dy=player.y-b.y, d=Math.hypot(dx,dy);
    if(d<player.radius+b.radius){
      if(b.type==='boost'){player.vx*=2; player.vy*=2;} 
      else{player.mass+=20; player.radius=Math.sqrt(player.mass);}
      b.alive=false;
    }
  });
  if(bonuses.filter(b=>b.alive).length<3){
    bonuses.push(new Bonus(rand(50,w-50),rand(50,h-50),Math.random()<0.5?'boost':'points'));
  }
}

function update(dt){
  if(!player) return;
  // движение по вектору к пальцу
  if(pointer.down){
    let dx=pointer.x-player.x, dy=pointer.y-player.y;
    let d=Math.hypot(dx,dy)||1;
    player.vx+=dx/d*300*dt;
    player.vy+=dy/d*300*dt;
  }
  player.update(dt);
  bots.forEach(b=>{
    if(!b.alive) return;
    let target=Math.random()<0.02?player:bots[Math.floor(Math.random()*bots.length)];
    let dx=target.x-b.x, dy=target.y-b.y, d=Math.hypot(dx,dy)||1;
    b.vx+=dx/d*80*dt; b.vy+=dy/d*80*dt; b.update(dt);
  });
  handleCollisions([player,...bots.filter(b=>b.alive)]);
  handleBonuses();
  document.getElementById('score').innerText='Очки: '+Math.round(player.mass);
  updateLeaderboard();
}

function draw(){
  if(!player) return;
  ctx.fillStyle='rgba(6,16,36,0.3)'; ctx.fillRect(0,0,w,h); // легкий "след" на фоне
  bonuses.forEach(b=>{if(b.alive)b.draw(ctx);});
  [player,...bots.filter(b=>b.alive)].forEach(sp=>sp.draw(ctx));
}

function updateLeaderboard(){
  const top=[player,...bots.filter(b=>b.alive)].sort((a,b)=>b.mass-a.mass).slice(0,5);
  const lbDiv=document.getElementById('leaderboard');
  lbDiv.innerHTML='<b>Топ:</b><br>'+top.map(sp=>sp.name+': '+Math.round(sp.mass)).join('<br>');
}

let last=performance.now();
function loop(t){ let dt=(t-last)/1000; last=t; update(dt); draw(); requestAnimationFrame(loop); }

document.getElementById('startBtn').
