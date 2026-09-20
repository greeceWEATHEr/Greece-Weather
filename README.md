<!DOCTYPE html>
<html lang="el">

<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Greece Weather</title>

<style>
*{
    box-sizing:border-box;
}

body{
    margin:0;
    font-family: Arial, Helvetica, sans-serif;
    color:#fff;
    background: linear-gradient(180deg, #071d35, #0d3762);
}

.container{
    width:min(100%,960px);
    margin:auto;
    padding:16px;
}

/* =====================================
   HEADER
===================================== */
.header{
    background: rgba(3,20,38,.72);
    padding:28px 20px;
    text-align:center;
    margin-bottom:25px;
}

.header h1{
    margin:0;
    font-size:30px;
}

.header p{
    margin:18px 0 0;
    color:#d6dce4;
    font-size:16px;
}

/* =====================================
   SEARCH
===================================== */
.search{
    display:flex;
    gap:10px;
    margin-bottom:25px;
}

.search input{
    flex:1;
    border:0;
    outline:0;
    border-radius:15px;
    padding:17px;
    font-size:16px;
}

.search button{
    border:0;
    border-radius:15px;
    padding:0 22px;
    font-weight:bold;
    font-size:15px;
    cursor:pointer;
}

/* =====================================
   CURRENT WEATHER
===================================== */
.current{
    background: rgba(57,85,117,.72);
    border-radius:20px;
    padding:25px;
    text-align:center;
    margin-bottom:25px;
}

.current h2{
    margin:0 0 20px;
    font-size:26px;
}

.temperature{
    font-size:60px;
    font-weight:300;
    margin-bottom:15px;
}

.condition{
    font-size:17px;
    margin-bottom:24px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

.current-grid{
    display:grid;
    grid-template-columns: repeat(3,1fr);
    gap:12px;
}

.current-box{
    background: rgba(104,133,165,.48);
    border-radius:14px;
    padding:16px 8px;
}

.current-box span{
    display:block;
    color:#e0e5ea;
    margin-bottom:5px;
}

.current-box strong{
    font-size:15px;
}

/* =====================================
   SECTION TITLE
===================================== */
.section-title{
    display:flex;
    align-items:center;
    gap:8px;
    font-size:24px;
    font-weight:bold;
    border-bottom: 2px solid rgba(255,255,255,.55);
    padding-bottom:12px;
    margin-bottom:15px;
}

/* =====================================
   15 ΗΜΕΡΕΣ
===================================== */
.forecast{
    display:grid;
    grid-template-columns: repeat(6,1fr);
    gap:12px;
}

.day{
    background: rgba(53,84,119,.78);
    border-radius:17px;
    padding:18px 8px;
    text-align:center;
    cursor:pointer;
    transition:.18s;
    border: 1px solid transparent;
}

.day:hover{
    transform: translateY(-3px);
    background: rgba(72,105,143,.95);
    border-color: rgba(255,255,255,.25);
}

.day:active{
    transform: scale(.97);
}

.day-name{
    font-weight:bold;
    font-size:15px;
}

.date{
    margin-top:9px;
    color:#e1e5e9;
    font-size:14px;
}

.icon{
    margin:18px 0 12px;
    height:45px;
    display:flex;
    align-items:center;
    justify-content:center;
}

.icon svg, .hour-icon svg, .condition svg {
    display: block;
    max-width: 100%;
    max-height: 100%;
}

.max{
    font-size:17px;
    font-weight:bold;
}

.min{
    margin-top:6px;
    color:#d0d7df;
}

.rain{
    margin-top:10px;
    font-size:12px;
    color:#c9e9ff;
}

/* =====================================
   ΩΡΙΑΙΑ ΠΡΟΓΝΩΣΗ
===================================== */
.hourly-section{
    display:none;
    margin-top:28px;
    background: rgba(5,27,50,.72);
    border-radius:20px;
    padding: 20px;
    width: 100%;
    overflow: hidden;
}

.hourly-header{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:10px;
    border-bottom: 1px solid rgba(255,255,255,.3);
    padding-bottom:15px;
    margin-bottom:15px;
}

.hourly-header h3{
    margin:0;
    font-size:21px;
}

.close-hourly{
    background: rgba(255,255,255,.15);
    border:0;
    color:white;
    border-radius:10px;
    padding:8px 13px;
    cursor:pointer;
}

.hourly{
    display:grid;
    gap:8px;
    width: 100%;
}

.hour{
    display:grid;
    grid-template-columns: 60px 45px repeat(4, 1fr);
    align-items:center;
    background: rgba(65,96,130,.62);
    border-radius:12px;
    padding:10px;
    gap:10px;
    width: 100%;
}

.hour-time{
    font-weight:bold;
    font-size: 14px;
}

.hour-icon{
    text-align:center;
    height:35px;
    width: 35px;
    display:flex;
    align-items:center;
    justify-content:center;
}

.hour-data{
    font-size:13px;
    color:#e4e8ed;
    line-height:1.4;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

/* =====================================
   MODEL INFO
===================================== */
.model-info{
    margin-top:18px;
    color:#bdc9d6;
    font-size:12px;
    line-height:1.5;
}

/* =====================================
   LOADING
===================================== */
.loading{
    text-align:center;
    padding:30px;
    font-size:16px;
}

/* =====================================
   TABLET / MOBILE RESPONSIVE
===================================== */
@media(max-width:750px){
    .forecast{
        grid-template-columns: repeat(3,1fr);
    }
    .current-grid{
        grid-template-columns: 1fr;
    }
    .hour{
        grid-template-columns: 55px 40px 1fr 1fr;
    }
    .hour-data:nth-child(5),
    .hour-data:nth-child(6){
        display:none;
    }
}

@media(max-width:430px){
    .container{
        padding:12px;
    }
    .header h1{
        font-size:26px;
    }
    .temperature{
        font-size:52px;
    }
    .forecast{
        grid-template-columns: repeat(3,1fr);
        gap:9px;
    }
    .day{
        padding:15px 5px;
    }
}
</style>
</head>

<body>

<div class="container">

    <!-- =================================
         HEADER
    ================================= -->
    <div class="header">
        <h1>🇬🇷 Greece Weather</h1>
        <p>Πρόγνωση καιρού για όλη την Ελλάδα</p>
    </div>

    <!-- =================================
         SEARCH
    ================================= -->
    <div class="search">
        <input id="cityInput" placeholder="Γράψε πόλη..." value="Θεσσαλονίκη">
        <button onclick="searchCity()">Αναζήτηση</button>
    </div>

    <!-- =================================
         CURRENT
    ================================= -->
    <div id="current"></div>

    <!-- =================================
         15 DAYS
    ================================= -->
    <div class="section-title">📅 Πρόγνωση 15 ημερών</div>
    <div id="forecast" class="forecast">
        <div class="loading">Φόρτωση πρόγνωσης...</div>
    </div>

    <!-- =================================
         HOURLY
    ================================= -->
    <div id="hourlySection" class="hourly-section">
        <div class="hourly-header">
            <h3 id="hourlyTitle"></h3>
            <button class="close-hourly" onclick="closeHourly()">✕ Κλείσιμο</button>
        </div>
        <div id="hourly" class="hourly"></div>
    </div>

    <!-- =================================
         INFO
    ================================= -->
    <div class="model-info">
        ECMWF IFS HRES • NOAA GFS • DWD ICON<br>
        Τα δεδομένα ανανεώνονται αυτόματα σύμφωνα με τους κύκλους έκδοσης των μοντέλων.
    </div>

</div>

<script>
/* =====================================
   GLOBAL
===================================== */
let weatherData = null;
let locationData = null;

/* =====================================
   ΣΗΜΑΙΑ ΧΩΡΑΣ
===================================== */
function countryFlag(countryCode){
    if(!countryCode) return "🌍";
    const code = countryCode.toUpperCase().trim();
    if(code.length !== 2) return "🌍";
    return String.fromCodePoint(...[...code].map(char => 127397 + char.charCodeAt(0)));
}

/* =====================================
   WEATHER ICON (ΑΚΡΙΒΩΣ ΟΠΩΣ ΟΙ ΕΙΚΟΝΕΣ ΣΟΥ)
===================================== */
function weatherIcon(code, isDay = true, precipitationProbability = 0, snowfall = 0){
    const rain = Number(precipitationProbability || 0);
    const snow = Number(snowfall || 0);

    const svgSun = `<svg viewBox="0 0 64 64" width="42" height="42"><circle cx="32" cy="32" r="22" fill="#F4D068"/></svg>`;
    const svgMoon = `<svg viewBox="0 0 64 64" width="42" height="42"><path d="M20 14 A20 20 0 1 0 52 46 A16 16 0 1 1 20 14 Z" fill="#F4D068"/></svg>`;
    const svgPartlyCloudyDay = `<svg viewBox="0 0 64 64" width="42" height="42"><circle cx="44" cy="24" r="14" fill="#F4D068"/><path d="M14 44c0-4.5 3.5-8 8-8 1.2 0 2.4.3 3.5.8C27.5 32 32 29 37 29c6 0 11 4.5 11.8 10.3 1.2-.8 2.5-1.3 4.2-1.3 4 0 7 3 7 7s-3 7-7 7H14V44z" fill="#CCCCCC"/></svg>`;
    const svgPartlyCloudyNight = `<svg viewBox="0 0 64 64" width="42" height="42"><path d="M38 16 A12 12 0 1 0 54 32 A10 10 0 1 1 38 16 Z" fill="#F4D068"/><path d="M12 44c0-4.5 3.5-8 8-8 1.2 0 2.4.3 3.5.8C25.5 32 30 29 35 29c6 0 11 4.5 11.8 10.3 1.2-.8 2.5-1.3 4.2-1.3 4 0 7 3 7 7s-3 7-7 7H12V44z" fill="#CCCCCC"/></svg>`;

    const svgClouds = `<svg viewBox="0 0 64 64" width="42" height="42">
        <path d="M12 30c0-4 3-7 7-7 1 0 2 .2 3 .6C24 20 28 17 33 17c5 0 9.5 3.5 10.3 8.5 1-.7 2.2-1.1 3.7-1.1 3.5 0 6 2.5 6 6s-2.5 6-6 6H12V30z" fill="#B0B0B0"/>
        <path d="M22 38c0-3.5 2.5-6.5 6-6.5 1 0 1.8.3 2.6.7C32 29 36 26 40 26c4.5 0 8 3 8.8 7.5 1-.6 2-.9 3.2-.9 3 0 5 2 5 5s-2 5-5 5H22V38z" fill="#C0C0C0"/>
        <path d="M28 44c0-3 2-5 5-5 .7 0 1.5.2 2 .5C36 37 39 35 43 35c3.5 0 6.5 2.5 7 6 .7-.4 1.5-.6 2.5-.6 2.5 0 4 1.5 4 4s-1.5 4-4 4H28V44z" fill="#D0D0D0"/>
    </svg>`;

    const svgLightRain = `<svg viewBox="0 0 64 64" width="42" height="42">
        <path d="M12 26c0-4 3-7 7-7 1 0 2 .2 3 .6C24 16 28 13 33 13c5 0 9.5 3.5 10.3 8.5 1-.7 2.2-1.1 3.7-1.1 3.5 0 6 2.5 6 6s-2.5 6-6 6H12V26z" fill="#B0B0B0"/>
