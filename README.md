<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Ελλάδα Weather</title>

<style>
*{box-sizing:border-box}

body{
  margin:0;
  font-family:Arial,sans-serif;
  background:linear-gradient(135deg,#eaf7ff,#fff);
  color:#12344d;
}

header{
  background:linear-gradient(135deg,#06477d,#079ed9);
  color:white;
  text-align:center;
  padding:30px 15px;
}

header h1{margin:0;font-size:36px}
header p{margin:8px 0 0}

main{
  max-width:1150px;
  margin:auto;
  padding:20px;
}

.page{display:none}
.page.active{display:block}

.menu{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(230px,1fr));
  gap:16px;
}

.card{
  border:0;
  border-radius:18px;
  background:white;
  padding:25px;
  text-align:left;
  cursor:pointer;
  box-shadow:0 7px 24px #0002;
}

.card:hover{
  transform:translateY(-2px);
}

.card h2{color:#087fc5}

.panel{
  background:white;
  border-radius:18px;
  padding:20px;
  margin-bottom:18px;
  box-shadow:0 7px 24px #0002;
}

.back{
  border:0;
  border-radius:10px;
  padding:12px 18px;
  background:#087fc5;
  color:white;
  cursor:pointer;
  margin-bottom:18px;
}

.controls{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(190px,1fr));
  gap:12px;
}

select{
  width:100%;
  padding:12px;
  border:1px solid #aac5d5;
  border-radius:10px;
  margin-top:7px;
}

#weatherMap{
  width:100%;
  height:auto;
  display:block;
  background:#bfe5f5;
  border-radius:16px;
  margin-top:15px;
}

.status{
  color:#557386;
  margin:10px 0;
}

.legend{
  display:flex;
  flex-wrap:wrap;
  gap:8px;
  margin-top:12px;
}

.legend span{
  padding:8px 11px;
  border-radius:8px;
  color:white;
  font-size:13px;
}

.forecast{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(145px,1fr));
  gap:12px;
}

.day{
  background:#eaf7ff;
  border-radius:13px;
  padding:13px;
  text-align:center;
}

.day h2{margin:8px}

.max{
  color:#df4b35;
  font-weight:bold;
}

.min{
  color:#087fc5;
  font-weight:bold;
}

.small{
  font-size:12px;
  color:#688092;
}
</style>
</head>

<body>

<header>
  <h1>🌦️ Ελλάδα Weather</h1>
  <p>Χάρτες και πρόγνωση καιρού Ελλάδας</p>
</header>

<main>

<!-- ΑΡΧΙΚΗ -->
<section id="home" class="page active">

<div class="panel">
  <h2>Μετεωρολογικό κέντρο</h2>
  <p>
    Επίλεξε χάρτη ή δες την αναλυτική πρόγνωση.
  </p>
</div>

<div class="menu">

<button class="card" onclick="openMap('rain')">
  <h2>🌧️ Βροχή / χιόνι</h2>
  <p>
    Χάρτης Ελλάδας με χρωματική απεικόνιση
    της αναμενόμενης έντασης υετού.
  </p>
</button>

<button class="card" onclick="openMap('wind')">
  <h2>💨 Άνεμοι</h2>
  <p>
    Χάρτης με την αναμενόμενη ταχύτητα ανέμου.
  </p>
</button>

<button class="card" onclick="openMap('temp850')">
  <h2>🌡️ Θερμοκρασία 850 hPa</h2>
  <p>
    Χάρτης θερμοκρασίας αερίων μαζών στα 850 hPa.
  </p>
</button>

<button class="card" onclick="openPage('forecast')">
  <h2>📅 15ήμερη πρόγνωση</h2>
  <p>
    Αναλυτική πρόγνωση για ελληνικές πόλεις.
  </p>
</button>

</div>
</section>


<!-- ΧΑΡΤΗΣ -->
<section id="maps" class="page">

<button class="back" onclick="openPage('home')">
← Πίσω
</button>

<div class="panel">

<h2 id="mapTitle">🌧️ Χάρτης βροχής / χιονιού</h2>

<div class="controls">

<div>
<label>Χάρτης</label>
<select id="mapType" onchange="loadMap()">
<option value="rain">Βροχή / χιόνι</option>
<option value="wind">Άνεμος</option>
<option value="temp850">850 hPa</option>
</select>
</div>

<div>
<label>Μοντέλο</label>
<select id="model" onchange="loadMap()">
<option value="best_match">Best Match</option>
<option value="ecmwf_ifs025">ECMWF</option>
<option value="gfs_seamless">GFS</option>
<option value="icon_seamless">ICON</option>
</select>
</div>

<div>
<label>Ώρα</label>
<select id="mapHour" onchange="loadMap()">
<option value="0">Τώρα</option>
<option value="3">+3 ώρες</option>
<option value="6">+6 ώρες</option>
<option value="12">+12 ώρες</option>
<option value="24">+24 ώρες</option>
<option value="48">+48 ώρες</option>
</select>
</div>

</div>

<div id="mapStatus" class="status">
Φόρτωση χάρτη...
</div>

<canvas id="weatherMap" width="1000" height="700"></canvas>

<div id="legend" class="legend"></div>

</div>
</section>


<!-- ΠΡΟΓΝΩΣΗ -->
<section id="forecast" class="page">

<button class="back" onclick="openPage('home')">
← Πίσω
</button>

<div class="panel">

<h2>📅 Πρόγνωση 15 ημερών</h2>

<select id="city" onchange="loadForecast()">
<option value="40.6401,22.9444,Θεσσαλονίκη">
Θεσσαλονίκη
</option>

<option value="37.9838,23.7275,Αθήνα">
Αθήνα
</option>

<option value="38.2466,21.7346,Πάτρα">
Πάτρα
</option>

<option value="39.639,22.419,Λάρισα">
Λάρισα
</option>

<option value="35.3387,25.1442,Ηράκλειο">
Ηράκλειο
</option>

<option value="39.665,20.8537,Ιωάννινα">
Ιωάννινα
</option>

<option value="40.9396,24.4018,Καβάλα">
Καβάλα
</option>

<option value="36.4349,28.2176,Ρόδος">
Ρόδος
</option>
</select>

<div id="forecastStatus" class="status">
Φόρτωση...
</div>

<div id="forecastBox" class="forecast"></div>

</div>
</section>

</main>


<script>

/* =========================
   ΓΕΩΓΡΑΦΙΚΑ ΟΡΙΑ ΕΛΛΑΔΑΣ
========================= */

const GREECE=[
[20.15,39.62],
[20.62,40.11],
[21.00,40.58],
[21.67,40.93],
[22.60,41.13],
[23.69,41.31],
[24.49,41.58],
[25.20,41.23],
[26.10,41.33],
[26.60,41.56],
[26.30,40.94],
[25.45,40.85],
[24.93,40.95],
[24.41,40.12],
[23.90,39.96],
[23.34,39.96],
[22.85,39.66],
[23.35,39.19],
[22.97,38.97],
[23.53,38.51],
[24.03,38.22],
[24.04,37.65],
[23.41,37.41],
[22.77,37.31],
[23.15,36.42],
[22.49,36.41],
[21.67,36.84],
[21.30,37.64],
[20.73,38.77],
[20.22,39.34],
[20.15,39.62]
];


/* =========================
   CANVAS
========================= */

const canvas=document.getElementById("weatherMap");
const ctx=canvas.getContext("2d");

const MIN_LON=19.7;
const MAX_LON=27.2;
const MIN_LAT=35.0;
const MAX_LAT=42.0;


/* =========================
   ΠΛΕΓΜΑ
========================= */

const grid=[];

for(let lat=35.25;lat<=41.75;lat+=0.5){
  for(let lon=20;lon<=27;lon+=0.5){

    grid.push({
      lat:Number(lat.toFixed(2)),
      lon:Number(lon.toFixed(2))
    });

  }
}


/* =========================
   ΜΕΤΑΤΡΟΠΗ ΣΥΝΤΕΤΑΓΜΕΝΩΝ
========================= */

function X(lon){
  return (lon-MIN_LON)/(MAX_LON-MIN_LON)*canvas.width;
}

function Y(lat){
  return (MAX_LAT-lat)/(MAX_LAT-MIN_LAT)*canvas.height;
}


/* =========================
   POINT IN POLYGON
========================= */

function insidePolygon(x,y,poly){

  let inside=false;

  for(
    let i=0,j=poly.length-1;
    i<poly.length;
    j=i++
  ){

    const xi=poly[i][0];
    const yi=poly[i][1];

    const xj=poly[j][0];
    const yj=poly[j][1];

    const intersect=
      ((yi>y)!==(yj>y)) &&
      (x < (xj-xi)*(y-yi)/(yj-yi)+xi);

    if(intersect)inside=!inside;
  }

  return inside;
}


/* =========================
   ΒΑΣΗ ΧΑΡΤΗ
========================= */

function drawBase(){

  ctx.clearRect(0,0,canvas.width,canvas.height);

  ctx.fillStyle="#bfe5f5";
  ctx.fillRect(0,0,canvas.width,canvas.height);

  /* θάλασσα */

  ctx.strokeStyle="#ffffff55";
  ctx.lineWidth=1;

  for(let lon=20;lon<=27;lon++){

    ctx.beginPath();
    ctx.moveTo(X(lon),0);
    ctx.lineTo(X(lon),canvas.height);
    ctx.stroke();

  }

  for(let lat=35;lat<=42;lat++){

    ctx.beginPath();
    ctx.moveTo(0,Y(lat));
    ctx.lineTo(canvas.width,Y(lat));
    ctx.stroke();

  }
}


/* =========================
   ΠΟΛΥΓΩΝΟ ΕΛΛΑΔΑΣ
========================= */

function drawGreece(){

  ctx.beginPath();

  GREECE.forEach((p,i)=>{

    if(i===0)
      ctx.moveTo(X(p[0]),Y(p[1]));
    else
      ctx.lineTo(X(p[0]),Y(p[1]));

  });

  ctx.closePath();

  ctx.fillStyle="#9ed0e3";
  ctx.fill();

  ctx.strokeStyle="#315d73";
  ctx.lineWidth=3;
  ctx.stroke();
}


/* =========================
   ΧΡΩΜΑ ΥΕΤΟΥ
========================= */

function rainColor(mm){

  if(mm<0.1)
    return null;

  if(mm<0.5)
    return "#69b9ef";

  if(mm<1)
    return "#478fe1";

  if(mm<2)
    return "#536bd9";

  if(mm<5)
    return "#684fd0";

  if(mm<10)
    return "#7d38c7";

  if(mm<20)
    return "#9828c4";

  return "#c019b7";
}


/* =========================
   ΧΡΩΜΑ ΑΝΕΜΟΥ
========================= */

function windColor(v){

  if(v<10)return "#8bd4f2";
  if(v<20)return "#4eb2e5";
  if(v<30)return "#3981dc";
  if(v<40)return "#654fd1";
  if(v<60)return "#9235c9";
  return "#c51fb4";
}


/* =========================
   ΘΕΡΜΟΚΡΑΣΙΑ
========================= */

function tempColor(v){

  if(v<0)return "#263bbd";
  if(v<5)return "#287ee0";
  if(v<10)return "#36b6e8";
  if(v<15)return "#f0df50";
  if(v<20)return "#f39436";
  if(v<25)return "#e94d36";

  return "#c9233c";
}


/* =========================
   ΣΧΕΔΙΑΣΗ ΧΡΩΜΑΤΙΣΜΕΝΩΝ ΚΥΨΕΛΩΝ
========================= */

function drawData(data,type){

  const step=0.5;

  data.forEach(p=>{

    if(!Number.isFinite(p.value))return;

    if(!insidePolygon(p.lon,p.lat,GREECE))
      return;

    let fill;

    if(type==="rain")
      fill=rainColor(p.value);

    if(type==="wind")
      fill=windColor(p.value);

    if(type==="temp850")
      fill=tempColor(p.value);

    if(!fill)return;

    const x=X(p.lon-step/2);
    const y=Y(p.lat+step/2);

    const w=
      X(p.lon+step/2)-X(p.lon-step/2);

    const h=
      Y(p.lat-step/2)-Y(p.lat+step/2);

    ctx.fillStyle=fill;
    ctx.globalAlpha=.78;

    ctx.fillRect(x,y,w+1,h+1);

    ctx.globalAlpha=1;

  });

  drawGreece();
}


/* =========================
   ΧΑΡΤΗΣ
========================= */

async function loadMap(){

  const type=document.getElementById("mapType").value;
  const model=document.getElementById("model").value;
  const hour=Number(document.getElementById("mapHour").value);

  document.getElementById("mapTitle").textContent=
    type==="rain"
    ?"🌧️ Βροχή / χιόνι"
    :type==="wind"
    ?"💨 Άνεμος"
    :"🌡️ Θερμοκρασία 850 hPa";

  drawBase();
  drawGreece();

  document.getElementById("mapStatus").textContent=
    "⏳ Φορτώνω πραγματικά δεδομένα...";

  let variable;

  if(type==="rain")
    variable="precipitation";

  if(type==="wind")
    variable="wind_speed_10m";

  if(type==="temp850")
    variable="temperature_850hPa";


  const lats=grid.map(p=>p.lat).join(",");
  const lons=grid.map(p=>p.lon).join(",");

  let endpoint=
    "https://api.open-meteo.com/v1/forecast";

  /*
    Για τον 850 hPa χρησιμοποιούμε το μοντέλο
    που υποστηρίζει pressure-level δεδομένα.
  */

  if(type==="temp850"){
    endpoint=
      "https://api.open-meteo.com/v1/chmi";
  }


  const params=new URLSearchParams();

  params.set("latitude",lats);
  params.set("longitude",lons);
  params.set("hourly",variable);
  params.set("forecast_days","3");
  params.set("timezone","UTC");

  if(type!=="temp850"){
    params.set("models",model);
  }


  try{

    const response=
      await fetch(endpoint+"?"+params.toString());

    if(!response.ok)
      throw new Error("HTTP "+response.status);

    const json=await response.json();

    const locations=
      Array.isArray(json)
      ?json
      :Array.isArray(json.data)
      ?json.data
      :[json];

    const result=[];

    locations.forEach((loc,i)=>{

      if(!loc.hourly)return;

      const values=loc.hourly[variable];

      if(!values)return;

      result.push({
        lat:grid[i]?.lat,
        lon:grid[i]?.lon,
        value:Number(values[hour])
      });

    });


    drawBase();
    drawData(result,type);


    document.getElementById("mapStatus").textContent=
      "✅ Ο χάρτης φορτώθηκε.";

    makeLegend(type);

  }
  catch(error){

    console.error(error);

    document.getElementById("mapStatus").textContent=
      "⚠️ Δεν ήταν δυνατή η λήψη αυτού του μοντέλου. Δοκίμασε ECMWF / Best Match.";

  }

}


/* =========================
   LEGEND
========================= */

function makeLegend(type){

  const legend=document.getElementById("legend");

  if(type==="rain"){

    legend.innerHTML=`
      <span style="background:#69b9ef">0.1–0.5 mm</span>
      <span style="background:#478fe1">0.5–1 mm</span>
      <span style="background:#536bd9">1–2 mm</span>
      <span style="background:#684fd0">2–5 mm</span>
      <span style="background:#7d38c7">5–10 mm</span>
      <span style="background:#9828c4">10–20 mm</span>
      <span style="background:#c019b7">20+ mm</span>
    `;

  }

  if(type==="wind"){

    legend.innerHTML=`
      <span style="background:#8bd4f2">0–10 km/h</span>
      <span style="background:#4eb2e5">10–20</span>
      <span style="background:#3981dc">20–30</span>
      <span style="background:#654fd1">30–40</span>
      <span style="background:#9235c9">40–60</span>
      <span style="background:#c51fb4">60+</span>
    `;

  }

  if(type==="temp850"){

    legend.innerHTML=`
      <span style="background:#263bbd">&lt;0°C</span>
      <span style="background:#287ee0">0–5°C</span>
      <span style="background:#36b6e8">5–10°C</span>
      <span style="background:#f0df50;color:#123">10–15°C</span>
      <span style="background:#f39436">15–20°C</span>
      <span style="background:#e94d36">20–25°C</span>
      <span style="background:#c9233c">25°C+</span>
    `;

  }
}


/* =========================
   ΑΝΟΙΓΜΑ ΧΑΡΤΗ
========================= */

function openMap(type){

  document.getElementById("mapType").value=type;

  openPage("maps");

}


/* =========================
   ΣΕΛΙΔΕΣ
========================= */

function openPage(id){

  document.querySelectorAll(".page")
    .forEach(p=>p.classList.remove("active"));

  document.getElementById(id)
    .classList.add("active");

  window.scrollTo(0,0);

  if(id==="maps")
    loadMap();

  if(id==="forecast")
    loadForecast();

}


/* =========================
   ICONS
========================= */

function weatherIcon(code){

  if(code===0)return"☀️";
  if(code===1)return"🌤️";
  if(code===2)return"⛅";
  if(code===3)return"☁️";
  if(code<=48)return"🌫️";
  if(code<=55)return"🌦️";
  if(code<=65)return"🌧️";
  if(code<=75)return"❄️";
  if(code<=82)return"🌦️";
  return"⛈️";

}


/* =========================
   15ΗΜΕΡΗ ΠΡΟΓΝΩΣΗ
========================= */

async function loadForecast(){

  const [lat,lon,name]=
    document.getElementById("city")
    .value.split(",");

  const status=
    document.getElementById("forecastStatus");

  const box=
    document.getElementById("forecastBox");

  status.textContent="⏳ Φόρτωση 15 ημερών...";
  box.innerHTML="";


  const url=
    "https://api.open-meteo.com/v1/forecast"+
    "?latitude="+lat+
    "&longitude="+lon+
    "&daily="+
    "temperature_2m_max,"+
    "temperature_2m_min,"+
    "precipitation_sum,"+
    "precipitation_probability_max,"+
    "weather_code,"+
    "wind_speed_10m_max"+
    "&forecast_days=15"+
    "&timezone=auto";


  try{

    const response=await fetch(url);

    if(!response.ok)
      throw new Error("HTTP "+response.status);

    const data=await response.json();

    const d=data.daily;

    for(let i=0;i<d.time.length;i++){

      const date=
        new Date(d.time[i]+"T12:00:00")
        .toLocaleDateString("el-GR",{
          weekday:"short",
          day:"numeric",
          month:"short"
        });


      const card=
        document.createElement("div");

      card.className="day";

      card.innerHTML=`

        <strong>${date}</strong>

        <h2>
          ${weatherIcon(d.weather_code[i])}
        </h2>

        <div class="max">
          ⬆️ ${Math.round(d.temperature_2m_max[i])}°C
        </div>

        <div class="min">
          ⬇️ ${Math.round(d.temperature_2m_min[i])}°C
        </div>

        <p>
          🌧️ ${d.precipitation_probability_max[i] ?? 0}%
        </p>

        <p>
          💧 ${Number(d.precipitation_sum[i]||0).toFixed(1)} mm
        </p>

        <p>
          💨 ${Math.round(d.wind_speed_10m_max[i])} km/h
        </p>

      `;

      box.appendChild(card);

    }


    status.textContent=
      "Πρόγνωση 15 ημερών για "+name+".";

  }
  catch(error){

    console.error(error);

    status.textContent=
      "⚠️ Δεν ήταν δυνατή η φόρτωση της πρόγνωσης.";

  }

}


/* αρχική φόρτωση */
loadForecast();

</script>

</body>
</html>
