
<!DOCTYPE html>
<html lang="fi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>MAAILMALLA 2027 – Joulu-Beta</title>
<style>
:root {
  --green:#145c40;
  --dark:#0c3428;
  --red:#b52d3d;
  --gold:#f4d274;
  --cream:#fffaf0;
  --ice:#e5f2f2;
}
* { box-sizing:border-box; }
body {
  margin:0;
  padding:12px;
  font-family:system-ui, sans-serif;
  color:#173d2e;
  background:linear-gradient(145deg,#0e5039,#102e36);
}
button,input,select { font:inherit; }
button {
  padding:11px 14px;
  border:0;
  border-radius:12px;
  color:white;
  background:var(--green);
  font-weight:750;
  cursor:pointer;
  box-shadow:0 3px 0 #082d21;
}
button:disabled { opacity:.5; cursor:not-allowed; }
button:active { transform:translateY(2px); }
input,select {
  width:100%;
  padding:10px;
  border:2px solid #c8dfd0;
  border-radius:10px;
  margin:5px 0 10px;
}
.app { max-width:1100px; margin:auto; }
.hero {
  text-align:center;
  color:white;
  padding:22px 12px;
  border:2px solid var(--gold);
  border-radius:22px;
  background:linear-gradient(135deg,#176447,#0b3025);
  box-shadow:0 6px 0 #08271d;
}
.hero h1 { margin:5px 0; font-size:clamp(1.8rem,6vw,3rem); }
.hero p { color:#ffe9a7; }
.actions {
  display:flex;
  flex-wrap:wrap;
  gap:8px;
  justify-content:center;
}
.gold { background:var(--gold); color:#49340b; }
.red { background:var(--red); }
.ice { background:var(--ice); color:#173e35; }
.panel {
  background:var(--cream);
  padding:15px;
  border-radius:18px;
  margin-top:14px;
  box-shadow:0 4px 0 #082e22;
}
.hidden { display:none!important; }
.menu-grid,.items {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(140px,1fr));
  gap:10px;
}
.menu-grid button {
  min-height:78px;
  text-align:left;
  background:#e7f2e7;
  color:#174c35;
  border:1px solid #c5ddca;
  box-shadow:0 3px 0 #c0d6c4;
}
.menu-grid span { display:block; font-size:1.5rem; }
.game-layout {
  display:grid;
  grid-template-columns:minmax(0,1fr) 240px;
  gap:14px;
  align-items:start;
}
@media(max-width:760px) {
  .game-layout { grid-template-columns:1fr; }
}
.board-wrap {
  padding:7px;
  border-radius:16px;
  background:#d8eadc;
  border:2px solid var(--gold);
}
.board {
  display:grid;
  grid-template-columns:repeat(7,minmax(0,1fr));
  grid-template-rows:repeat(7,minmax(47px,1fr));
  gap:3px;
}
.tile {
  min-width:0;
  min-height:47px;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  overflow-wrap:anywhere;
  text-align:center;
  padding:2px;
  border:1px solid #b9d0c0;
  border-radius:7px;
  background:#fffdf6;
  color:#214638;
  font-size:clamp(.54rem,1.7vw,.76rem);
  line-height:1.15;
}
.tile .emoji { font-size:clamp(.9rem,2.8vw,1.4rem); }
.tile .name { font-weight:800; }
.tile .price { font-size:.85em; }
.tile.special { background:#f8e8b2; }
.tile.card { background:#d9eaff; }
.tile.start { background:#c8ead1; }
.tile.market { background:#f5d9df; }
.tile.owned { border:2px solid #378658; }
.tokens { font-size:.9rem; }
.center {
  grid-column:2/7;
  grid-row:2/7;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  text-align:center;
  border-radius:14px;
  color:white;
  background:linear-gradient(145deg,#176447,#0b3025);
  padding:6px;
  overflow:hidden;
}
.center h2 { color:#ffe19a; margin:4px; }
.center p { font-size:.8rem; margin:3px; }
.tree { font-size:clamp(2rem,7vw,4rem); }
.side { display:grid; gap:12px; }
.dice {
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  gap:5px;
  max-width:180px;
  min-height:115px;
  margin:12px auto;
  border:3px solid var(--gold);
  border-radius:22px;
  background:linear-gradient(145deg,#fff,#e0f2e5);
  box-shadow:0 5px 0 #b7d0bf;
  color:#164b35;
}
.dice span { font-size:55px; line-height:1.1; }
.dice.rolling span { animation:roll .16s infinite alternate; }
@keyframes roll {
  from { transform:rotate(-15deg); }
  to { transform:rotate(15deg); }
}
.player {
  display:flex;
  gap:8px;
  align-items:center;
  margin:6px 0;
  padding:8px;
  background:#eaf3e9;
  border-radius:10px;
}
.player.current { outline:3px solid #e5bd50; }
.stat-grid {
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:8px;
}
.stat { padding:10px; border-radius:10px; background:#eaf3e9; }
.stat strong { display:block; }
.item {
  padding:13px;
  border-radius:13px;
  background:#eaf3e9;
  border:1px solid #d1e2d3;
}
.item .big { font-size:2rem; }
.item button { width:100%; margin-top:8px; }
.tag {
  display:inline-block;
  border-radius:20px;
  background:#d3e7d7;
  padding:4px 8px;
  font-size:.8rem;
  font-weight:700;
}
.modal-backdrop {
  position:fixed;
  inset:0;
  z-index:100;
  display:flex;
  justify-content:center;
  align-items:center;
  padding:14px;
  background:#061d18c9;
}
.modal {
  width:min(440px,100%);
  padding:20px;
  border-radius:20px;
  text-align:center;
  background:var(--cream);
  box-shadow:0 8px 35px #0005;
}
.modal h2 { color:var(--green); }
.modal-actions {
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  gap:8px;
  margin-top:15px;
}
.small { font-size:.88rem; }
footer { text-align:center; color:#d7eee1; padding:20px 5px; }
.snow {
  position:fixed;
  top:-25px;
  z-index:50;
  pointer-events:none;
  color:white;
  animation:snowfall linear forwards;
}
@keyframes snowfall {
  to { transform:translateY(110vh) rotate(360deg); opacity:.2; }
}
body.no-motion * { animation:none!important; transition:none!important; }
@media(max-width:420px) {
  body { padding:7px; }
  .panel { padding:10px; }
  .board { gap:2px; grid-template-rows:repeat(7,minmax(39px,1fr)); }
  .tile { min-height:39px; border-radius:4px; }
}
</style>
</head>
<body>
<div class="app">
  <header class="hero">
    <div style="font-size:2rem">🎄 ❄️ 🎁</div>
    <h1>MAAILMALLA 2027</h1>
    <p>Joulu-Beta – lähde jouluiselle maailmanympärimatkalle!</p>
    <div class="actions">
      <button class="gold" onclick="showScreen('home')">🏠 Etusivu</button>
      <button id="music-button" class="gold" onclick="toggleMusic()">🎵 Käynnistä joulumusiikki</button>
    </div>
  </header>

  <section id="home" class="panel">
    <h2>🎅 Tervetuloa joulumaailmaan!</h2>
    <p>Heitä noppaa, osta kaupunkeja, kerää tähtiä ja avaa jouluhahmoja.</p>
    <div class="menu-grid">
      <button onclick="newGameForm()"><span>🎲</span>Uusi lautapeli</button>
      <button onclick="renderCharacters()"><span>🧑‍🎄</span>Hahmot</button>
      <button onclick="renderShop()"><span>🛍️</span>Joulukauppa</button>
      <button onclick="renderCollection()"><span>🌍</span>Kaupunkikokoelma</button>
      <button onclick="renderCalendar()"><span>🎁</span>Joulukalenteri</button>
      <button onclick="renderRiddle()"><span>🔔</span>Jouluarvoitus</button>
      <button onclick="renderAdventure()"><span>🗺️</span>Jouluseikkailu</button>
      <button onclick="renderStarGame()"><span>⭐</span>Tähtipeli</button>
      <button onclick="renderSettings()"><span>⚙️</span>Asetukset</button>
    </div>
    <div class="stat-grid" style="margin-top:12px">
      <div class="stat">Tähdet<strong id="home-stars">0 ⭐</strong></div>
      <div class="stat">Avatut hahmot<strong id="home-unlocked">1</strong></div>
    </div>
  </section>

  <section id="game-screen" class="panel hidden">
    <h2>🎄 Joulumatka</h2>
    <div class="game-layout">
      <div class="board-wrap"><div id="board" class="board"></div></div>
      <aside class="side">
        <div class="panel" style="margin:0">
          <h3>🎲 Nopanheitto</h3>
          <div id="turn-info"></div>
          <div id="dice" class="dice">
            <span>🎲</span><strong>Heitä noppaa!</strong>
          </div>
          <p id="dice-message" class="small" style="text-align:center">Valmiina matkaan!</p>
          <button id="roll-button" style="width:100%" onclick="rollDice()">🎲 Heitä noppaa</button>
          <button class="ice" style="width:100%;margin-top:8px" onclick="showScreen('home')">🏠 Valikkoon</button>
        </div>
        <div class="panel" style="margin:0">
          <h3>👥 Pelaajat</h3>
          <div id="player-list"></div>
        </div>
        <div class="panel" style="margin:0">
          <h3>📜 Tapahtumat</h3>
          <div id="log" class="small">Peli alkaa!</div>
        </div>
      </aside>
    </div>
  </section>

  <section id="content" class="panel hidden">
    <div class="actions" style="justify-content:space-between">
      <h2 id="content-title">Joulu</h2>
      <button class="ice" onclick="showScreen('home')">← Takaisin</button>
    </div>
    <div id="content-body"></div>
  </section>
  <footer>MAAILMALLA 2027 · Joulu-Beta</footer>
</div>
<div id="modal-root" class="hidden"></div>

<script>
"use strict";

/* LAUDALLA ON 24 RUUTUA.
   Koordinaattien, ruutujen ja liikkumisen määrä pidetään samana. */

const SAVE_KEY="maailmalla2027_fixed_movement";
const characters=[
  {id:"santa",name:"Joulupukki",emoji:"🎅",cost:0},
  {id:"elf",name:"Tonttu",emoji:"🧝",cost:15},
  {id:"snowman",name:"Lumiukko",emoji:"☃️",cost:25},
  {id:"reindeer",name:"Poro",emoji:"🦌",cost:35},
  {id:"penguin",name:"Pingviini",emoji:"🐧",cost:45},
  {id:"angel",name:"Joulun enkeli",emoji:"😇",cost:60},
  {id:"bear",name:"Jääkarhu",emoji:"🐻‍❄️",cost:75},
  {id:"queen",name:"Jääkuningatar",emoji:"👑",cost:100}
];

const cities=[
  {name:"Helsinki",emoji:"🇫🇮",price:180,fee:45},
  {name:"Rovaniemi",emoji:"🎅",price:220,fee:55},
  {name:"Tukholma",emoji:"🇸🇪",price:180,fee:45},
  {name:"Oslo",emoji:"🇳🇴",price:190,fee:48},
  {name:"Kööpenhamina",emoji:"🇩🇰",price:200,fee:50},
  {name:"Lontoo",emoji:"🇬🇧",price:250,fee:65},
  {name:"Pariisi",emoji:"🇫🇷",price:260,fee:70},
  {name:"Berliini",emoji:"🇩🇪",price:230,fee:60},
  {name:"Rooma",emoji:"🇮🇹",price:220,fee:55},
  {name:"Tokio",emoji:"🇯🇵",price:300,fee:80},
  {name:"New York",emoji:"🇺🇸",price:310,fee:85},
  {name:"Sydney",emoji:"🇦🇺",price:290,fee:78}
];

/* 24 ruutua: 12 kaupunkia ja 12 erikoisruutua. */
const spaces=[
  {type:"start",name:"LÄHTÖ",emoji:"🎄"},
  {type:"city",city:0},
  {type:"hupi",name:"Hupi-kortti",emoji:"🎉"},
  {type:"city",city:1},
  {type:"tax",name:"Joulumaksu",emoji:"🧾"},
  {type:"city",city:2},
  {type:"gift",name:"Lahjapaja",emoji:"🎁"},
  {type:"city",city:3},
  {type:"world",name:"Maailmalla",emoji:"🌍"},
  {type:"city",city:4},
  {type:"rest",name:"Kaakaotauko",emoji:"☕"},
  {type:"city",city:5},
  {type:"star",name:"Tähtipaikka",emoji:"⭐"},
  {type:"city",city:6},
  {type:"market",name:"Joulumarkkinat",emoji:"🎄"},
  {type:"city",city:7},
  {type:"hupi",name:"Hupi-kortti",emoji:"🎉"},
  {type:"city",city:8},
  {type:"tax",name:"Lahjakeräys",emoji:"🧾"},
  {type:"city",city:9},
  {type:"gift",name:"Lahjapaja",emoji:"🎁"},
  {type:"city",city:10},
  {type:"world",name:"Maailmalla",emoji:"🌍"},
  {type:"city",city:11}
];

let profile=loadProfile();
let game=null;
let audio=null;
let musicPlaying=false;
let musicTimer=null;
let noteIndex=0;
let snowTimer=null;

function defaultProfile(){
  return {
    stars:0,unlocked:["santa"],selected:"santa",
    cities:[],calendar:{},riddleSolved:false,
    tasks:[],adventureClaimed:false,
    items:[],settings:{sound:true,motion:true,snow:true}
  };
}
function loadProfile(){
  try{
    const saved=localStorage.getItem(SAVE_KEY);
    if(!saved)return defaultProfile();
    const base=defaultProfile(),data=JSON.parse(saved);
    return {...base,...data,settings:{...base.settings,...(data.settings||{})}};
  }catch(e){return defaultProfile();}
}
function saveProfile(){
  try{localStorage.setItem(SAVE_KEY,JSON.stringify(profile));}catch(e){}
}
function updateHome(){
  document.getElementById("home-stars").textContent=profile.stars+" ⭐";
  document.getElementById("home-unlocked").textContent=profile.unlocked.length;
}
function showScreen(screen){
  document.getElementById("home").classList.toggle("hidden",screen!=="home");
  document.getElementById("game-screen").classList.toggle("hidden",screen!=="game");
  document.getElementById("content").classList.toggle("hidden",screen!=="content");
  if(screen==="home")updateHome();
  if(screen==="game"&&game)renderGame();
}

/* MODAALI */
function modal(title,text,buttons=[{label:"Selvä"}]){
  const root=document.getElementById("modal-root");
  root.classList.remove("hidden");
  root.innerHTML="";
  const backdrop=document.createElement("div");
  backdrop.className="modal-backdrop";
  const box=document.createElement("div");
  box.className="modal";
  const h=document.createElement("h2");h.textContent=title;
  const p=document.createElement("p");p.textContent=text;
  const actions=document.createElement("div");actions.className="modal-actions";
  box.append(h,p,actions);
  buttons.forEach(item=>{
    const b=document.createElement("button");
    b.textContent=item.label;
    if(item.className)b.className=item.className;
    b.onclick=()=>{
      root.classList.add("hidden");root.innerHTML="";
      if(item.action)item.action();
    };
    actions.appendChild(b);
  });
  backdrop.appendChild(box);root.appendChild(backdrop);
}
function logMessage(message){
  if(!game)return;
  game.logs.unshift(message);
  game.logs=game.logs.slice(0,5);
  document.getElementById("log").textContent=game.logs.join(" • ");
}
function safeText(s){
  return String(s).replace(/[&<>"']/g,c=>({
    "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"
  }[c]));
}

/* UUSI PELI */
function newGameForm(){
  document.getElementById("content-title").textContent="🎲 Uusi peli";
  document.getElementById("content-body").innerHTML=`
    <div class="items">
      <div class="item">
        <h3>👤 Pelaaja 1</h3>
        <label>Nimi</label>
        <input id="p1" maxlength="18" value="Pelaaja 1">
      </div>
      <div class="item">
        <h3>👥 Vastustaja</h3>
        <label>Pelimuoto</label>
        <select id="mode">
          <option value="ai">Tietokonetta vastaan</option>
          <option value="local">Kaksi pelaajaa</option>
        </select>
        <label>Toisen pelaajan nimi</label>
        <input id="p2" maxlength="18" value="Pelaaja 2">
      </div>
      <div class="item">
        <h3>🏆 Voittoraja</h3>
        <select id="target">
          <option value="5000">5 000 € – lyhyt</option>
          <option value="10000" selected>10 000 € – tavallinen</option>
          <option value="15000">15 000 € – pitkä</option>
        </select>
      </div>
    </div>
    <button style="width:100%;margin-top:12px" onclick="startGame()">🎄 Aloita peli</button>`;
  showScreen("content");
}
function selectedEmoji(){
  return (characters.find(c=>c.id===profile.selected)||characters[0]).emoji;
}
function startGame(){
  const name1=(document.getElementById("p1").value||"Pelaaja 1").trim();
  const name2=(document.getElementById("p2").value||"Pelaaja 2").trim();
  const mode=document.getElementById("mode").value;
  game={
    current:0,turn:1,over:false,busy:false,
    target:Number(document.getElementById("target").value),
    mode,boardSize:spaces.length,owners:{},
    players:[
      {name:name1||"Pelaaja 1",money:1500,pos:0,ai:false,emoji:selectedEmoji(),stars:0},
      {name:mode==="ai"?"Joulu-AI":(name2||"Pelaaja 2"),money:1500,pos:0,ai:mode==="ai",emoji:"🧝",stars:0}
    ],
    logs:["🎄 Peli alkoi! Molemmilla pelaajilla on 1 500 €."]
  };
  document.getElementById("dice").innerHTML="<span>🎲</span><strong>Heitä noppaa!</strong>";
  document.getElementById("dice-message").textContent="Onnea matkaan!";
  showScreen("game");
  renderGame();
  if(game.players[0].ai)setTimeout(aiTurn,500);
}

/* LAUDAN 24 RUUTUA. */
function coordinates(){
  const result=[];
  for(let c=0;c<7;c++)result.push([0,c]);
  for(let r=1;r<7;r++)result.push([r,6]);
  for(let c=5;c>=0;c--)result.push([6,c]);
  for(let r=5;r>=1;r--)result.push([r,0]);
  return result;
}
function renderBoard(){
  const board=document.getElementById("board");
  board.innerHTML="";
  const coords=coordinates();
  const center=document.createElement("div");
  center.className="center";
  center.innerHTML=`
    <div class="tree">🎄</div>
    <h2>MAAILMALLA</h2>
    <p>Joulu-Beta 2027</p>
    <p>Matkusta · Osta · Kerää tähtiä</p>
    <p>Kierros ${game.turn}</p>`;
  board.appendChild(center);

  spaces.forEach((space,index)=>{
    const tile=document.createElement("div");
    tile.className="tile";
    const [row,col]=coords[index];
    tile.style.gridRow=String(row+1);
    tile.style.gridColumn=String(col+1);

    let emoji=space.emoji||"",name=space.name||"",price="";
    if(space.type==="city"){
      const city=cities[space.city];
      const owner=game.owners[space.city];
      emoji=city.emoji;name=city.name;
      price=owner===undefined?city.price+" €":game.players[owner].emoji;
      if(owner!==undefined)tile.classList.add("owned");
    }else{
      if(space.type==="start")tile.classList.add("start");
      if(space.type==="hupi"||space.type==="world")tile.classList.add("card");
      if(space.type==="market")tile.classList.add("market");
      if(["gift","tax","star","rest"].includes(space.type))tile.classList.add("special");
    }
    const em=document.createElement("div");em.className="emoji";em.textContent=emoji;
    const nm=document.createElement("div");nm.className="name";nm.textContent=name;
    const pr=document.createElement("div");pr.className="price";pr.textContent=price;
    const tokens=document.createElement("div");tokens.className="tokens";
    game.players.forEach(p=>{if(p.pos===index)tokens.textContent+=p.emoji;});
    tile.append(em,nm,pr,tokens);
    board.appendChild(tile);
  });
}
function renderGame(){
  if(!game)return;
  renderBoard();
  const p=game.players[game.current];
  document.getElementById("turn-info").innerHTML=
    `<strong>${safeText(p.name)}</strong><br>Rahat: ${p.money} €<br>Tähdet: ${p.stars} ⭐`;
  document.getElementById("roll-button").disabled=game.busy||game.over||p.ai;
  const list=document.getElementById("player-list");
  list.innerHTML="";
  game.players.forEach((player,index)=>{
    const div=document.createElement("div");
    div.className="player"+(index===game.current?" current":"");
    div.innerHTML=`<span style="font-size:1.5rem">${player.emoji}</span><div><strong>${safeText(player.name)}</strong><br><small>${player.money} € · ${player.stars} ⭐</small></div>`;
    list.appendChild(div);
  });
}

/* NOPPA.
   Liike etenee aina yhden ruudun kerrallaan.
   Askelten määrä on tarkalleen nopan tulos.
   Liikettä ei jatketa, kun tulos on saavutettu. */
const dieFaces=["⚀","⚁","⚂","⚃","⚄","⚅"];

function rollDice(){
  if(!game||game.over||game.busy||game.players[game.current].ai)return;
  throwDice(false);
}
function aiTurn(){
  if(!game||game.over||game.busy||!game.players[game.current].ai)return;
  throwDice(true);
}
function throwDice(isAI){
  if(!game||game.over||game.busy)return;
  game.busy=true;
  renderGame();

  const die=document.getElementById("dice");
  const message=document.getElementById("dice-message");
  const player=game.players[game.current];
  die.classList.add("rolling");
  message.textContent=player.name+" heittää noppaa...";
  let animationCount=0;

  function animate(){
    if(!game||game.over)return;
    if(profile.settings.motion&&animationCount<8){
      die.querySelector("span").textContent=dieFaces[Math.floor(Math.random()*6)];
      die.querySelector("strong").textContent="Heitetään...";
      animationCount++;
      setTimeout(animate,85);
      return;
    }
    const result=1+Math.floor(Math.random()*6);
    die.classList.remove("rolling");
    die.querySelector("span").textContent=dieFaces[result-1];
    die.querySelector("strong").textContent="Tulos: "+result;
    message.textContent=player.name+" etenee "+result+" ruutua.";
    diceSound();
    moveExactly(result);
  }
  animate();
}

function moveExactly(steps){
  if(!game||game.over)return;
  const player=game.players[game.current];
  const total=game.boardSize;
  let moved=0;

  function step(){
    if(!game||game.over)return;
    
  game.busy=true;
  renderGame();

  const die=document.getElementById("dice");
  const message=document.getElementById("dice-message");
  const player=game.players[game.current];
  die.classList.add("rolling");
  message.textContent=player.name+" heittää noppaa...";
  let animationCount=0;

  function animate(){
    if(!game||game.over)return;
    if(profile.settings.motion&&animationCount<8){
      die.querySelector("span").textContent=dieFaces[Math.floor(Math.random()*6)];
      die.querySelector("strong").textContent="Heitetään...";
      animationCount++;
      setTimeout(animate,85);
      return;
    }
    const result=1+Math.floor(Math.random()*6);
    die.classList.remove("rolling");
    die.querySelector("span").textContent=dieFaces[result-1];
    die.querySelector("strong").textContent="Tulos: "+result;
    message.textContent=player.name+" etenee "+result+" ruutua.";
    diceSound();
    moveExactly(result);
  }
  animate();
}

function moveExactly(steps){
  if(!game||game.over)return;
  const player=game.players[game.current];
  const total=game.boardSize;
  let moved=0;

  function step(){
    if(!game||game.over)return;

    /* Yksi kutsu = yksi ruutu. */
    player.pos=(player.pos+1)%total;
    moved++;

    /* Lähtöbonus vain silloin, kun lähtöruudun yli oikeasti kuljetaan. */
    if(player.pos===0){
      player.money+=200;
      logMessage("🎄 "+player.name+" kulki lähdön kautta: +200 €.");
    }

    renderBoard();

    /* Pysähdytään heti, kun nopan tulos on käytetty. */
    if(moved>=steps){
      document.getElementById("dice-message").textContent=
        player.name+" pysähtyi ruutuun "+(player.pos+1)+".";
      setTimeout(()=>resolveSpace(player.pos),180);
      return;
    }

    setTimeout(step,profile.settings.motion?230:20);
  }
  step();
}

/* VUORO VAIHTUU VASTA TAPAHTUMAN JÄLKEEN. */
function finishLanding(message){
  if(!game||game.over)return;
  if(message)logMessage(message);
  const player=game.players[game.current];

  if(player.money<0){
    endGame(game.players[1-game.current].name+" voittaa!");
    return;
  }
  if(player.money>=game.target){
    endGame(player.name+" saavutti voittorajan "+game.target+" €!");
    return;
  }

  saveProfile();
  renderGame();

  /* Viive tapahtuman jälkeen, sitten vuoro vaihtuu. */
  setTimeout(()=>{
    if(!game||game.over)return;
    game.current=(game.current+1)%game.players.length;
    if(game.current===0)game.turn++;
    game.busy=false;
    document.getElementById("dice").innerHTML="<span>🎲</span><strong>Heitä noppaa!</strong>";
    document.getElementById("dice-message").textContent="Seuraavan pelaajan vuoro.";
    renderGame();
    if(game.players[game.current].ai)setTimeout(aiTurn,500);
  },450);
}
function endGame(message){
  if(!game)return;
  game.over=true;game.busy=true;
  saveProfile();renderGame();
  modal("🏆 Peli päättyi!",message,[
    {label:"Uusi peli",action:newGameForm},
    {label:"Etusivu",action:()=>showScreen("home")}
  ]);
}

/* RUUTUJEN TAPAHTUMAT */
function resolveSpace(index){
  if(!game||game.over)return;
  const space=spaces[index];
  const player=game.players[game.current];

  if(space.type==="start"){
    modal("🎄 Lähtöruutu","Pääsit lähtöruutuun. Jatka joulumatkaa!",[
      {label:"Jatka",action:()=>finishLanding(player.name+" pysähtyi lähtöruutuun.")}
    ]);
    return;
  }
  if(space.type==="city"){
    const city=cities[space.city];
    const owner=game.owners[space.city];
    if(owner===undefined){
      const buttons=[
        {label:"Jätä väliin",className:"ice",action:()=>finishLanding(player.name+" kävi kaupungissa "+city.name+".")}
      ];
      if(player.money>=city.price){
        buttons.unshift({label:"Osta "+city.price+" €",action:()=>{
          player.money-=city.price;
          game.owners[space.city]=game.current;
          if(!profile.cities.includes(city.name))profile.cities.push(city.name);
          saveProfile();
          finishLanding(player.name+" osti kaupungin "+city.name+".");
        }});
      }
      modal(city.emoji+" "+city.name,
        "Kaupunki on vapaana. Hinta "+city.price+" €. Vierailumaksu "+city.fee+" €.",buttons);
      return;
    }
    if(owner===game.current){
      modal("🏙️ Oma kaupunki","Tämä kaupunki kuuluu sinulle.",[
        {label:"Jatka",action:()=>finishLanding(player.name+" vieraili omassa kaupungissaan.")}
      ]);
      return;
    }
    const fee=Math.min(city.fee,Math.max(0,player.money));
    player.money-=fee;
    game.players[owner].money+=fee;
    modal("🏙️ Vierailu: "+city.name,
      "Maksoit kaupungin omistajalle "+fee+" €.",[
        {label:"Jatka",action:()=>finishLanding(player.name+" maksoi vierailumaksun.")}
      ]);
    return;
  }
  if(space.type==="hupi"||space.type==="world"){
    drawCard(space.type);return;
  }
  if(space.type==="tax"){
    const fee=Math.min(100,Math.max(0,player.money));
    player.money-=fee;
    modal("🧾 Joulumaksu","Maksoit yhteiseen joulukassaan "+fee+" €.",[
      {label:"Jatka",action:()=>finishLanding(player.name+" maksoi joulumaksun.")}
    ]);
    return;
  }
  if(space.type==="gift"){
    const amount=50+Math.floor(Math.random()*101);
    player.money+=amount;
    modal("🎁 Lahjapaja!","Löysit yllätyslahjan ja sait "+amount+" €.",[
      {label:"Kiitos!",action:()=>finishLanding(player.name+" sai lahjan.")}
    ]);
    markTask("gift");
    return;
  }
  if(space.type==="rest"){
    modal("☕ Kaakaotauko","Nauti lämpimästä kaakaosta ennen seuraavaa siirtoa.",[
      {label:"Jatka",action:()=>finishLanding(player.name+" piti kaakaotauon.")}
    ]);
    return;
  }
  if(space.type==="star"){
    const amount=1+Math.floor(Math.random()*2);
    profile.stars+=amount;
    player.stars+=amount;
    saveProfile();
    markTask("star");
    modal("⭐ Tähtipaikka!","Keräsit "+amount+" tähteä!",[
      {label:"Kerää tähdet",action:()=>finishLanding(player.name+" keräsi tähtiä.")}
    ]);
    return;
  }
  if(space.type==="market"){
    player.money+=80;
    markTask("market");
    modal("🎄 Joulumarkkinat","Sait markkinoilta 80 € palkkion.",[
      {label:"Jatka",action:()=>finishLanding(player.name+" ansaitsi markkinoilla rahaa.")}
    ]);
  }
}

const hupiCards=[
  {text:"Autat tonttuja lahjojen pakkaamisessa. Saat 100 €.",fn:p=>p.money+=100},
  {text:"Löydät joululahjan. Saat 50 €.",fn:p=>p.money+=50},
  {text:"Reki tarvitsee huoltoa. Maksat 70 €.",fn:p=>p.money-=Math.min(70,p.money)},
  {text:"Järjestät pikkujoulut. Saat 120 €.",fn:p=>p.money+=120},
  {text:"Lumimyrsky aiheuttaa lisäkuluja: 40 €.",fn:p=>p.money-=Math.min(40,p.money)},
  {text:"Saat yllätyksen ja yhden tähden!",fn:p=>{p.stars++;profile.stars++;}},
  {text:"Löydät matkalompakon. Saat 90 €.",fn:p=>p.money+=90}
];
const worldCards=[
  {text:"Löydät uuden matkakumppanin. Saat 80 €.",fn:p=>p.money+=80},
  {text:"Näet revontulet ja saat yhden tähden!",fn:p=>{p.stars++;profile.stars++;}},
  {text:"Matkan vaihtomaksu on 60 €.",fn:p=>p.money-=Math.min(60,p.money)},
  {text:"Saat valokuvauspalkinnon. Saat 100 €.",fn:p=>p.money+=100},
  {text:"Saat matkailupalkinnon ja kaksi tähteä!",fn:p=>{p.stars+=2;profile.stars+=2;}},
  {text:"Löydät joulutorilta 40 €.",fn:p=>p.money+=40}
];
function drawCard(type){
  const player=game.players[game.current];
  const cards=type==="hupi"?hupiCards:worldCards;
  const card=cards[Math.floor(Math.random()*cards.length)];
  card.fn(player);saveProfile();markTask("card");
  modal(type==="hupi"?"🎉 Hupi-kortti!":"🌍 Maailmalla-kortti!",card.text,[
    {label:"Jatka",action:()=>finishLanding(player.name+" nosti kortin.")}
  ]);
}

/* HAHMOT */
function renderCharacters(){
  setContent("🧑‍🎄 Hahmot");
  const grid=document.createElement("div");grid.className="items";
  characters.forEach(c=>{
    const unlocked=profile.unlocked.includes(c.id);
    const card=document.createElement("div");card.className="item";
    card.innerHTML=`<div class="big">${c.emoji}</div><h3>${c.name}</h3><p>${unlocked?"Avattu":c.cost+" ⭐"}</p><button>${profile.selected===c.id?"Valittu ✓":unlocked?"Valitse":"Avaa hahmo"}</button>`;
    card.querySelector("button").onclick=()=>{
      if(unlocked){
        profile.selected=c.id;saveProfile();renderCharacters();return;
      }
      if(profile.stars<c.cost){
        modal("⭐ Tähtiä ei ole tarpeeksi","Tarvitset "+c.cost+" tähteä.",[{label:"Selvä"}]);return;
      }
      profile.stars-=c.cost;profile.unlocked.push(c.id);profile.selected=c.id;saveProfile();
      modal("🎉 Hahmo avattu!",c.name+" on nyt käytettävissäsi.",[
        {label:"Hienoa!",action:renderCharacters}
      ]);
    };
    grid.appendChild(card);
  });
  document.getElementById("content-body").appendChild(grid);
}

/* KAUPPA */
function renderShop(){
  setContent("🛍️ Joulukauppa");
  const products=[
    ["🎅","Joulupukin asu",10],
    ["🍪","Piparikoriste",15],
    ["❄️","Lumihiutale",20],
    ["🔔","Joulukello",25]
  ];
  const info=document.createElement("p");
  info.textContent="Tähtesi: "+profile.stars+" ⭐";
  document.getElementById("content-body").appendChild(info);
  const grid=document.createElement("div");grid.className="items";
  products.forEach(([emoji,name,cost])=>{
    const card=document.createElement("div");card.className="item";
    card.innerHTML=`<div class="big">${emoji}</div><h3>${name}</h3><p>${cost} ⭐</p><button>Osta</button>`;
    card.querySelector("button").onclick=()=>{
      if(profile.stars<cost){
        modal("Tähtiä ei ole tarpeeksi","Kerää lisää tähtiä laudalta tai tähtipelistä.",[{label:"Selvä"}]);return;
      }
      profile.stars-=cost;profile.items.push(name);saveProfile();
      modal("🎁 Ostos onnistui!","Ostit tuotteen: "+name+".",[
        {label:"Jatka",action:renderShop}
      ]);
    };
    grid.appendChild(card);
  });
  document.getElementById("content-body").appendChild(grid);
}

/* KAUPUNKIKOKOELMA */
function renderCollection(){
  setContent("🌍 Kaupunkikokoelma");
  const owned=profile.cities||[];
  const p=document.createElement("p");
  p.textContent="Kerätty "+owned.length+" / "+cities.length+" kaupunkia.";
  document.getElementById("content-body").appendChild(p);
  const grid=document.createElement("div");grid.className="items";
  cities.forEach(c=>{
    const card=document.createElement("div");card.className="item";
    card.innerHTML=`<div class="big">${c.emoji}</div><h3>${c.name}</h3><span class="tag">${owned.includes(c.name)?"Kerätty ✓":"Ei vielä kerätty"}</span>`;
    grid.appendChild(card);
  });
  document.getElementById("content-body").appendChild(grid);
}

/* JOULUKALENTERI */
function renderCalendar(){
  setContent("🎁 Joulukalenteri");
  const now=new Date();
  const december=now.getMonth()===11;
  const p=document.createElement("p");
  p.textContent=december?"Avaa tämän päivän tai aiempien päivien luukkuja.":"Joulukalenteri avautuu 1. joulukuuta.";
  document.getElementById("content-body").appendChild(p);
  const grid=document.createElement("div");grid.className="items";
  for(let day=1;day<=24;day++){
    const opened=!!profile.calendar[day];
    const available=december&&now.getDate()>=day;
    const card=document.createElement("div");card.className="item";
    card.innerHTML=`<div class="big">🎁</div><h3>Luukku ${day}</h3><p>${opened?"Avattu":available?"Valmis avattavaksi":"Lukittu"}</p><button ${(!available||opened)?"disabled":""}>Avaa</button>`;
    card.querySelector("button").onclick=()=>{
      if(!available||opened)return;
      profile.calendar[day]=true;
      const reward=day%5===0?3:1;
      profile.stars+=reward;saveProfile();
      modal("🎁 Luukku avattu!","Sait "+reward+" tähteä.",[
        {label:"Jatka",action:renderCalendar}
      ]);
    };
    grid.appendChild(card);
  }
  document.getElementById("content-body").appendChild(grid);
}

/* JOULUARVOITUS */
function renderRiddle(){
  setContent("🔔 Jouluarvoitus");
  const now=new Date();
  const unlocked=now.getMonth()===11&&now.getDate()>=1;
  const box=document.createElement("div");box.className="item";
  if(!unlocked){
    box.innerHTML="<div class='big'>🔒🎄</div><h3>Arvoitus on lukossa</h3><p>Jouluarvoitus avautuu 1. joulukuuta. Halloween-arvoitus on jouluteeman aikana lukittu.</p>";
  }else if(profile.riddleSolved){
    box.innerHTML="<div class='big'>🏆</div><h3>Arvoitus ratkaistu!</h3><p>Sait jo palkintosi.</p>";
  }else{
    box.innerHTML=`
      <div class="big">🎄</div><h3>Jouluarvoitus</h3>
      <p>Minulla on oksia, minut koristellaan jouluna ja lahjat ovat usein juurellani. Mikä olen?</p>
      <input id="riddle-answer" placeholder="Kirjoita vastaus">
      <button id="answer-button">Tarkista vastaus</button>`;
    box.querySelector("#answer-button").onclick=()=>{
      const answer=document.getElementById("riddle-answer").value.trim().toLowerCase();
      if(["kuusi","joulukuusi","joulupuu"].includes(answer)){
        profile.riddleSolved=true;profile.stars+=5;saveProfile();
        modal("🎉 Oikein!","Ratkaisit arvoituksen ja sait 5 tähteä.",[
          {label:"Jatka",action:renderRiddle}
        ]);
      }else{
        modal("❄️ Yritä uudelleen","Vinkki: siihen ripustetaan koristeita.",[{label:"Selvä"}]);
      }
    };
  }
  document.getElementById("content-body").appendChild(box);
}

/* JOULUSEIKKAILU */
const taskInfo=[
  ["city","Vieraile kaupungissa",2],
  ["gift","Löydä lahja",2],
  ["star","Kerää tähti",2],
  ["card","Nosta kortti",2],
  ["market","Käy joulumarkkinoilla",3]
];
function markTask(id){
  if(!profile.tasks.includes(id)){profile.tasks.push(id);saveProfile();}
}
function renderAdventure(){
  setContent("🗺️ Jouluseikkailu");
  const p=document.createElement("p");
  p.textContent="Suorita kaikki viisi tehtävää pelissä ja lunasta tähtipalkinto.";
  document.getElementById("content-body").appendChild(p);
  taskInfo.forEach(([id,name,reward])=>{
    const row=document.createElement("div");row.className="item";
    row.style.marginBottom="8px";
    row.innerHTML=`<strong>${profile.tasks.includes(id)?"✅":"🎯"} ${name}</strong><p>+${reward} ⭐</p>`;
    document.getElementById("content-body").appendChild(row);
  });
  const button=document.createElement("button");
  button.style.width="100%";
  button.textContent=profile.adventureClaimed?"Palkinto lunastettu ✓":"Lunasta palkinto";
  button.disabled=profile.adventureClaimed||taskInfo.some(t=>!profile.tasks.includes(t[0]));
  button.onclick=()=>{
    if(button.disabled)return;
    const total=taskInfo.reduce((sum,t)=>sum+t[2],0);
    profile.stars+=total;profile.adventureClaimed=true;saveProfile();
    modal("🏆 Seikkailu valmis!","Sait "+total+" tähteä!",[
      {label:"Jatka",action:renderAdventure}
    ]);
  };
  document.getElementById("content-body").appendChild(button);
}

/* TÄHTIPELI */
function renderStarGame(){
  setContent("⭐ Tähtipeli");
  const box=document.createElement("div");box.className="item";
  box.innerHTML=`
    <div class="big">⭐ 🎁 ⭐</div>
    <h3>Valitse lahja</h3>
    <p>Valitse yksi kolmesta lahjasta. Voit voittaa 0–3 tähteä.</p>
    <p>Tähtesi: ${profile.stars} ⭐</p>
    <div class="actions">
      <button class="gold" data-choice="0">🎁 A</button>
      <button class="red" data-choice="1">🎁 B</button>
      <button data-choice="2">🎁 C</button>
    </div>
    <p id="star-result"></p>`;
  document.getElementById("content-body").appendChild(box);
  let played=false;
  box.querySelectorAll("button").forEach(b=>{
    b.onclick=()=>{
      if(played)return;
      played=true;
      box.querySelectorAll("button").forEach(x=>x.disabled=true);
      const choice=Number(b.dataset.choice);
      const winner=Math.floor(Math.random()*3);
      const reward=choice===winner?3:(Math.random()<.5?1:0);
      profile.stars+=reward;saveProfile();
      document.getElementById("star-result").textContent=
        reward?"🎉 Sait "+reward+" tähteä!":"Tällä kertaa ei löytynyt tähtiä. Kokeile myöhemmin uudelleen.";
    };
  });
}

/* ASETUKSET */
function renderSettings(){
  setContent("⚙️ Asetukset");
  const body=document.getElementById("content-body");
  [
    ["sound","🔊 Äänitehosteet"],
    ["motion","✨ Animaatiot"],
    ["snow","❄️ Lumisade"]
  ].forEach(([key,label])=>{
    const row=document.createElement("div");row.className="item";
    row.style.marginBottom="9px";
    const button=document.createElement("button");
    button.textContent=label+": "+(profile.settings[key]?"Päällä":"Pois");
    button.onclick=()=>{
      profile.settings[key]=!profile.settings[key];
      saveProfile();
      document.body.classList.toggle("no-motion",!profile.settings.motion);
      setupSnow();
      renderSettings();
    };
    row.appendChild(button);body.appendChild(row);
  });
  const reset=document.createElement("button");reset.className="red";
  reset.textContent="Nollaa tallennus";
  reset.onclick=()=>modal("⚠️ Nollataanko tallennus?","Tämä poistaa tallennetut tähdet, hahmot ja kokoelman.",[
    {label:"Peruuta",className:"ice"},
    {label:"Nollaa",className:"red",action:()=>{
      localStorage.removeItem(SAVE_KEY);profile=defaultProfile();saveProfile();
      modal("Tallennus nollattu","Pelin tiedot on nollattu.",[{label:"Selvä",action:()=>showScreen("home")}]);
    }}
  ]);
  body.appendChild(reset);
}
function setContent(title){
  document.getElementById("content-title").textContent=title;
  document.getElementById("content-body").innerHTML="";
  showScreen("content");
}

/* JOULUMUSIIKKI – selain luo sävelet itse. */
function ensureAudio(){
  if(audio)return true;
  const AudioClass=window.AudioContext||window.webkitAudioContext;
  if(!AudioClass)return false;
  audio=new AudioClass();
  return true;
}
function tone(freq,duration,volume){
  if(!audio)return;
  const osc=audio.createOscillator();
  const gain=audio.createGain();
  const seconds=duration/1000;
  osc.type="sine";
  osc.frequency.setValueAtTime(freq,audio.currentTime);
  gain.gain.setValueAtTime(volume,audio.currentTime);
  gain.gain.exponentialRampToValueAtTime(.001,audio.currentTime+seconds);
  osc.connect(gain);gain.connect(audio.destination);
  osc.start();osc.stop(audio.currentTime+seconds);
}
function diceSound(){
  if(!profile.settings.sound)return;
  try{
    if(!ensureAudio())return;
    if(audio.state==="suspended")audio.resume();
    tone(440,80,.035);
    setTimeout(()=>tone(660,100,.035),80);
  }catch(e){}
}
const melody=[
  [659,250],[659,250],[659,500],[659,250],[659,250],[659,500],
  [659,250],[784,250],[523,350],[587,150],[659,650],
  [698,250],[698,250],[698,350],[698,250],[698,250],[659,250],
  [659,250],[659,150],[659,150],[587,250],[587,250],[659,250],[587,450],[784,450]
];
async function toggleMusic(){
  const button=document.getElementById("music-button");
  try{
    if(!ensureAudio()){
      modal("🎵 Ääntä ei tueta","Selaimesi ei tue musiikin luomista.",[{label:"Selvä"}]);return;
    }
    if(musicPlaying){
      musicPlaying=false;clearTimeout(musicTimer);
      button.textContent="🎵 Käynnistä joulumusiikki";return;
    }
    await audio.resume();
    musicPlaying=true;
    button.textContent="🔇 Pysäytä joulumusiikki";
    playNextNote();
  }catch(e){
    musicPlaying=false;
    button.textContent="🎵 Käynnistä joulumusiikki";
  }
}
function playNextNote(){
  if(!musicPlaying||!audio)return;
  const note=melody[noteIndex%melody.length];
  tone(note[0],note[1],.035);
  noteIndex++;
  musicTimer=setTimeout(playNextNote,note[1]+45);
}

/* LUMISADE */
function setupSnow(){
  clearInterval(snowTimer);
  document.querySelectorAll(".snow").forEach(x=>x.remove());
  if(!profile.settings.snow)return;
  snowTimer=setInterval(()=>{
    if(document.querySelectorAll(".snow").length>25)return;
    const flake=document.createElement("div");
    flake.className="snow";
    flake.textContent=["❄","❅","❆"][Math.floor(Math.random()*3)];
    flake.style.left=Math.random()*100+"vw";
    flake.style.fontSize=(10+Math.random()*14)+"px";
    flake.style.animationDuration=(5+Math.random()*6)+"s";
    document.body.appendChild(flake);
    setTimeout(()=>flake.remove(),12000);
  },500);
}
/* KÄYNNISTYS */
document.body.classList.toggle("no-motion",!profile.settings.motion);
setupSnow();
updateHome();
showScreen("home");
</script>
</body>
</html>
