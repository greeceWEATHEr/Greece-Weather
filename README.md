
<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Ελλάδα Weather</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial;background:#eef8ff;color:#12344d}
header{background:linear-gradient(135deg,#06477d,#08a5df);color:white;text-align:center;padding:30px 15px}
header h1{margin:0;font-size:36px}
main{max-width:1150px;margin:auto;padding:20px}
.page{display:none}.active{display:block}
.menu{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:16px}
.card,.panel{background:white;border-radius:18px;box-shadow:0 6px 22px #0002}
.card{border:0;padding:25px;text-align:left;cursor:pointer}
.card h2{color:#087fc5}
.panel{padding:20px;margin-bottom:18px}
.back{border:0;border-radius:10px;padding:12px 18px;background:#087fc5;color:white;cursor:pointer}
select{width:100%;padding:12px;border:1px solid #aac5d5;border-radius:10px;margin:8px 0 15px}
.controls{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:12px}
#map{width:100%;aspect-ratio:1.25;background:#d9effb;border-radius:15px;display:block}
.status{color:#557386;margin:10px 0}
.legend{display:flex;flex-wrap:wrap;gap:8px;margin-top:12px}
.legend span{padding:8px;border-radius:8px;color:white;font-size:13px}
.forecast{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:12px}
.day{background:#eaf7ff;border-radius:12px;padding:12px;text-align:center}
</style>
</head>

<body>
<header>
<h1>🌦️ Ελλάδα Weather</h1>
<p>Μετεωρολογικοί χάρτες και πρόγνωση Ελλάδας</p>
</header>

<main>

<section id="home" class="page active">
<div class="panel">
<h2>Επίλεξε υπηρεσία</h2>
<p>Όλοι οι χάρτες εμφανίζονται μέσα στη δική σου ιστοσελίδα.</p>
</div>

<div class="menu">
<button class="card" onclick="openPage('maps');changeType('temp')">
<h2>🌡️ Θερμοκρασία 850 hPa</h2>
<p>Θερμοκρασία αερίων μαζών περίπου στα 1.500 μέτρα.</p>
</button>

<button class="card" onclick="openPage('maps');changeType('rain')">
<h2>🌧️ Βροχή και χιόνι</h2>
<p>Πραγματικά δεδομένα υετού από το μοντέλο.</p>
</button>

<button class="card" onclick="openPage('maps');changeType('wind')">
<h2>💨 Άνεμος</h2>
<p>Ταχύτητα ανέμου σε σημεία της Ελλάδας.</p>
</button>

<button class="card" onclick="openPage('forecast')">
<h2>📅 Πρόγνωση 15 ημερών</h2>
<p>Αναλυτική πρόγνωση για ελληνικές πόλεις.</p>
</button>
</div>
</section>

<section id="maps" class="page">
<button class="back" onclick="openPage('home')">← Πίσω</button>

<div class="panel">
<h2 id="mapTitle">🌡️ Θερμοκρασία 850 hPa</h2>

<div class="controls">
<div>
<label>Τύπος χάρτη</label>
<select id="type" onchange="loadMap()">
<option value="temp">Θερμοκρασία 850 hPa</option>
<option value="rain">Βροχή και χιόνι</option>
<option value="wind">Άνεμος</option>
</select>
</div>

<div>
<label>Μοντέλο</label>
<select id="model" onchange="loadMap()">
<option value="ecmwf_ifs025">ECMWF IFS</option>
<option value="gfs_global">GFS</option>
<option value="icon_global">ICON</option>
</select>
</div>

<div>
<label>Χρονικό βήμα</label>
<select id="hour" onchange="loadMap()">
<option value="0">Τώρα</option>
<option value="6">+6 ώρες</option>
<option value="12">+12 ώρες</option>
<option value="24">+24 ώρες</option>
<option value="48">+48 ώρες</option>
</select>
</div>
</div>

<div id="mapStatus" class="status">Φόρτωση δεδομένων...</div>
<canvas id="map" width="900" height="720"></canvas>
<div class="legend" id="legend"></div>
</div>
</section>

<section id="forecast" class="page">
<button class="back" onclick="openPage('home')">← Πίσω</button>

<div class="panel">
<h2>📅 Πρόγνωση 15 ημερών</h2>
<select id="city" onchange="loadForecast()">
<option value="40.6401,22.9444,Θεσσαλονίκη">Θεσσαλονίκη</option>
<option value="37.9838,23.7275,Αθήνα">Αθήνα</option>
<option value="38.2466,21.7346,Πάτρα">Πάτρα</option>
<option value="39.639,22.419,Λάρισα">Λάρισα</option>
<option value="35.3387,25.1442,Ηράκλειο">Ηράκλειο</option>
<option value="39.665,20.8537,Ιωάννινα">Ιωάννινα</option>
</select>
<div id="forecastStatus" class="status"></div>
<div id="forecastBox" class="forecast"></div>
</div>
</section>

</main>

<script>
const canvas=document.getElementById("map");
const ctx=canvas.getContext("2d");

const points=[];
for(let lat=35;lat<=41;lat+=1){
  for(let lon=20;lon<=28;lon+=1){
    points.push({lat,lon});
  }
}

let currentType="temp";
let currentData=[];

function openPage(id){
  document.querySelectorAll(".page").forEach(x=>x.classList.remove("active"));
  document.getElementById(id).classList.add("active");

  if(id==="maps")loadMap();
  if(id==="forecast")loadForecast();
}

function changeType(type){
  document.getElementById("type").value=type;
  currentType=type;
  loadMap();
}

function getVariable(){
  if(currentType==="temp")return "temperature_850hPa";
  if(currentType==="rain")return "precipitation";
  return "wind_speed_10m";
}

function color(value,min,max){
  let r=(value-min)/(max-min||1);
  r=Math.max(0,Math.min(1,r));

  if(currentType==="rain"){
    if(r<.2)return "#d8f6ff";
    if(r<.4)return "#70c8f2";
    if(r<.6)return "#3288d8";
    if(r<.8)return "#7047c8";
    return "#d72dc8";
  }

  if(r<.2)return "#244bc7";
  if(r<.4)return "#36a9e8";
  if(r<.6)return "#f2df54";
  if(r<.8)return "#f28b35";
  return "#d62e36";
}

function drawMap(){
  ctx.clearRect(0,0,900,720);
  ctx.fillStyle="#cce9f7";
  ctx.fillRect(0,0,900,720);

  const left=20,right=28,top=41,bottom=35;
  const x=lon=>(lon-left)/(right-left)*900;
  const y=lat=>(top-lat)/(top-bottom)*720;

  ctx.strokeStyle="#ffffffaa";
  ctx.lineWidth=1;

  for(let lon=20;lon<=28;lon++){
    ctx.beginPath();
    ctx.moveTo(x(lon),0);
    ctx.lineTo(x(lon),720);
    ctx.stroke();
  }

  for(let lat=35;lat<=41;lat++){
    ctx.beginPath();
    ctx.moveTo(0,y(lat));
    ctx.lineTo(900,y(lat));
    ctx.stroke();
  }

  if(!currentData.length)return;

  const values=currentData.map(p=>p.value).filter(v=>Number.isFinite(v));
  if(!values.length)return;

  const min=Math.min(...values);
  const max=Math.max(...values);

  currentData.forEach(p=>{
    if(!Number.isFinite(p.value))return;

    const px=x(p.lon);
    const py=y(p.lat);

    ctx.beginPath();
    ctx.arc(px,py,42,0,Math.PI*2);
    ctx.fillStyle=color(p.value,min,max);
    ctx.globalAlpha=.78;
    ctx.fill();
    ctx.globalAlpha=1;

    ctx.fillStyle="#102b42";
    ctx.font="bold 13px Arial";
    ctx.textAlign="center";

    let text;
    if(currentType==="rain")text=p.value.toFixed(1)+" mm";
    else if(currentType==="wind")text=p.value.toFixed(1)+" km/h";
    else text=p.value.toFixed(1)+"°C";

    ctx.fillText(text,px,py+4);
  });

  ctx.textAlign="left";
}

async function loadMap(){
  currentType=document.getElementById("type").value;

  const model=document.getElementById("model").value;
  const hour=Number(document.getElementById("hour").value);
  const variable=getVariable();

  document.getElementById("mapTitle").textContent=
    currentType==="temp"?"🌡️ Θερμοκρασία 850 hPa":
    currentType==="rain"?"🌧️ Βροχή και χιόνι":"💨 Άνεμος";

  document.getElementById("mapStatus").textContent=
    "Λήψη δεδομένων για "+points.length+" σημεία...";

  currentData=[];
  drawMap();

  try{
    const results=await Promise.all(points.map(async p=>{
      const url=
        "https://api.open-meteo.com/v1/forecast"+
        "?latitude="+p.lat+
        "&longitude="+p.lon+
        "&hourly="+variable+
        "&forecast_days=3"+
        "&timezone=UTC"+
        "&models="+model;

      const response=await fetch(url);
      if(!response.ok)throw new Error("HTTP "+response.status);

      const data=await response.json();
      const values=data.hourly&&data.hourly[variable];

      return {
        lat:p.lat,
        lon:p.lon,
        value:values?Number(values[hour]):NaN
      };
    }));

    currentData=results;
    drawMap();

    document.getElementById("mapStatus").textContent=
      "Ο χάρτης φορτώθηκε επιτυχώς.";

    document.getElementById("legend").innerHTML=`
      <span style="background:#244bc7">Χαμηλές τιμές</span>
      <span style="background:#36a9e8">Μέτριες–χαμηλές</span>
      <span style="background:#f2df54;color:#123">Μέτριες</span>
      <span style="background:#f28b35">Υψηλές</span>
      <span style="background:#d62e36">Πολύ υψηλές</span>
    `;

  }catch(error){
    console.error(error);
    document.getElementById("mapStatus").textContent=
      "Το μοντέλο δεν επέστρεψε δεδομένα για αυτόν τον χάρτη. Δοκίμασε άλλο μοντέλο.";
  }
}

function icon(code){
  if(code===0)return"☀️";
  if(code<=3)return"⛅";
  if(code<=48)return"🌫️";
  if(code<=67)return"🌧️";
  if(code<=77)return"❄️";
  if(code<=82)return"🌦️";
  return"⛈️";
}

async function loadForecast(){
  const [lat,lon,name]=document.getElementById("city").value.split(",");
  const status=document.getElementById("forecastStatus");
  const box=document.getElementById("forecastBox");

  status.textContent="Φόρτωση πρόγνωσης...";
  box.innerHTML="";

  const url=
    "https://api.open-meteo.com/v1/forecast"+
    "?latitude="+lat+
    "&longitude="+lon+
    "&daily=temperature_2m_max,temperature_2m_min,precipitation_probability_max,weather_code"+
    "&forecast_days=15"+
    "&timezone=auto";

  try{
    const response=await fetch(url);
    if(!response.ok)throw new Error("HTTP "+response.status);

    const data=await response.json();

    for(let i=0;i<data.daily.time.length;i++){
      const date=new Date(data.daily.time[i]+"T12:00:00")
        .toLocaleDateString("el-GR",{
          weekday:"short",
          day:"numeric",
          month:"short"
        });

      const div=document.createElement("div");
      div.className="day";
      div.innerHTML=`
        <strong>${date}</strong>
        <h2>${icon(data.daily.weather_code[i])}</h2>
        <div>⬆️ ${data.daily.temperature_2m_max[i]}°C</div>
        <div>⬇️ ${data.daily.temperature_2m_min[i]}°C</div>
        <div>🌧️ ${data.daily.precipitation_probability_max[i]??"—"}%</div>
      `;
      box.appendChild(div);
    }

    status.textContent="Πρόγνωση για "+name;

  }catch(error){
    console.error(error);
    status.textContent="Δεν φορτώθηκε η πρόγνωση. Έλεγξε τη σύνδεση.";
  }
}
</script>
</body>
</html>
