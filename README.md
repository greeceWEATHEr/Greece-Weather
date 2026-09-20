Greece Weather

*{box-sizing:border-box;}
body{margin:0;font-family:Arial,sans-serif;color:#fff;background:linear-gradient(180deg,#071d35,#0d3762);}
.container{width:min(100%,960px);margin:auto;padding:16px;}
.header{background:rgba(3,20,38,.72);padding:28px 20px;text-align:center;margin-bottom:25px;}
.header h1{margin:0;font-size:30px;}
.header p{margin:18px 0 0;color:#d6dce4;font-size:16px;}
.search{display:flex;gap:10px;margin-bottom:25px;}
.search input{flex:1;border:0;outline:0;border-radius:15px;padding:17px;font-size:16px;}
.search button{border:0;border-radius:15px;padding:0 22px;font-weight:bold;font-size:15px;cursor:pointer;}
.current{background:rgba(57,85,117,.72);border-radius:20px;padding:25px;text-align:center;margin-bottom:25px;}
.current h2{margin:0 0 20px;font-size:26px;}
.temperature{font-size:60px;font-weight:300;margin-bottom:15px;}
.condition{font-size:17px;margin-bottom:24px;display:flex;align-items:center;justify-content:center;gap:10px;}
.current-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;}
.current-box{background:rgba(104,133,165,.48);border-radius:14px;padding:16px 8px;}
.current-box span{display:block;color:#e0e5ea;margin-bottom:5px;}
.current-box strong{font-size:15px;}
.section-title{display:flex;align-items:center;gap:8px;font-size:24px;font-weight:bold;border-bottom:2px solid rgba(255,255,255,.55);padding-bottom:12px;margin-bottom:15px;}
.forecast{display:grid;grid-template-columns:repeat(6,1fr);gap:12px;}
.day{background:rgba(53,84,119,.78);border-radius:17px;padding:18px 8px;text-align:center;cursor:pointer;transition:.18s;border:1px solid transparent;}
.day:hover{transform:translateY(-3px);background:rgba(72,105,143,.95);border-color:rgba(255,255,255,.25);}
.day:active{transform:scale(.97);}
.day-name{font-weight:bold;font-size:15px;}
.date{margin-top:9px;color:#e1e5e9;font-size:14px;}
.icon{margin:18px 0 12px;height:45px;display:flex;align-items:center;justify-content:center;}
.icon svg,.hour-icon svg,.condition svg{display:block;max-width:100%;max-height:100%;}
.max{font-size:17px;font-weight:bold;}
.min{margin-top:6px;color:#d0d7df;}
.rain{margin-top:10px;font-size:12px;color:#c9e9ff;}
.hourly-section{display:none;margin-top:28px;background:rgba(5,27,50,.72);border-radius:20px;padding:20px;width:100%;overflow:hidden;}
.hourly-header{display:flex;align-items:center;justify-content:space-between;gap:10px;border-bottom:1px solid rgba(255,255,255,.3);padding-bottom:15px;margin-bottom:15px;}
.hourly-header h3{margin:0;font-size:21px;}
.close-hourly{background:rgba(255,255,255,.15);border:0;color:white;border-radius:10px;padding:8px 13px;cursor:pointer;}
.hourly{display:grid;gap:8px;width:100%;}
.hour{display:grid;grid-template-columns:60px 45px repeat(4, 1fr);align-items:center;background:rgba(65,96,130,.62);border-radius:12px;padding:10px;gap:10px;width:100%;}
.hour-time{font-weight:bold;font-size:14px;}
.hour-icon{text-align:center;height:35px;width:35px;display:flex;align-items:center;justify-content:center;}
.hour-data{font-size:13px;color:#e4e8ed;line-height:1.4;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.model-info{margin-top:18px;color:#bdc9d6;font-size:12px;line-height:1.5;}
.loading{text-align:center;padding:30px;font-size:16px;}
@media(max-width:750px){.forecast{grid-template-columns:repeat(3,1fr);}.current-grid{grid-template-columns:1fr;}.hour{grid-template-columns:55px 40px 1fr 1fr;}.hour-data:nth-child(5),.hour-data:nth-child(6){display:none;}}
@media(max-width:430px){.container{padding:12px;}.header h1{font-size:26px;}.temperature{font-size:52px;}.forecast{grid-template-columns:repeat(3,1fr);gap:9px;}.day{padding:15px 5px;}}




🇬🇷 Greece WeatherΠρόγνωση καιρού για όλη την Ελλάδα
Αναζήτηση

📅 Πρόγνωση 15 ημερών
Φόρτωση πρόγνωσης...
✕ Κλείσιμο
ECMWF IFS HRES • NOAA GFS • DWD ICON
Τα δεδομένα ανανεώνονται αυτόματα σύμφωνα με τους κύκλους έκδοσης των μοντέλων.


let weatherData=null,locationData=null;
function countryFlag(c){if(!c)return"🌍";const code=c.toUpperCase().trim();if(code.length!==2)return"🌍";return String.fromCodePoint(...[...code].map(char=>127397+char.charCodeAt(0)));}
function weatherIcon(code,isDay=true,precipitationProbability=0,snowfall=0){
const rain=Number(precipitationProbability||0),snow=Number(snowfall||0);
const svgSun=<svg viewBox="0 0 64 64" width="42" height="42"><circle cx="32" cy="32" r="22" fill="#F4D068"/></svg>;
const svgMoon=<svg viewBox="0 0 64 64" width="42" height="42"><path d="M20 14 A20 20 0 1 0 52 46 A16 16 0 1 1 20 14 Z" fill="#F4D068"/></svg>;
const svgPartlyCloudyDay=<svg viewBox="0 0 64 64" width="42" height="42"><circle cx="44" cy="24" r="14" fill="#F4D068"/><path d="M14 44c0-4.5 3.5-8 8-8 1.2 0 2.4.3 3.5.8C27.5 32 32 29 37 29c6 0 11 4.5 11.8 10.3 1.2-.8 2.5-1.3 4.2-1.3 4 0 7 3 7 7s-3 7-7 7H14V44z" fill="#CCCCCC"/></svg>;
const svgPartlyCloudyNight=<svg viewBox="0 0 64 64" width="42" height="42"><path d="M38 16 A12 12 0 1 0 54 32 A10 10 0 1 1 38 16 Z" fill="#F4D068"/><path d="M12 44c0-4.5 3.5-8 8-8 1.2 0 2.4.3 3.5.8C25.5 32 30 29 35 29c6 0 11 4.5 11.8 10.3 1.2-.8 2.5-1.3 4.2-1.3 4 0 7 3 7 7s-3 7-7 7H12V44z" fill="#CCCCCC"/></svg>;
const svgClouds=<svg viewBox="0 0 64 64" width="42" height="42"><path d="M12 30c0-4 3-7 7-7 1 0 2 .2 3 .6C24 20 28 17 33 17c5 0 9.5 3.5 10.3 8.5 1-.7 2.2-1.1 3.7-1.1 3.5 0 6 2.5 6 6s-2.5 6-6 6H12V30z" fill="#B0B0B0"/><path d="M22 38c0-3.5 2.5-6.5 6-6.5 1 0 1.8.3 2.6.7C32 29 36 26 40 26c4.5 0 8 3 8.8 7.5 1-.6 2-.9 3.2-.9 3 0 5 2 5 5s-2 5-5 5H22V38z" fill="#C0C0C0"/><path d="M28 44c0-3 2-5 5-5 .7 0 1.5.2 2 .5C36 37 39 35 43 35c3.5 0 6.5 2.5 7 6 .7-.4 1.5-.6 2.5-.6 2.5 0 4 1.5 4 4s-1.5 4-4 4H28V44z" fill="#D0D0D0"/></svg>;
const svgLightRain=<svg viewBox="0 0 64 64" width="42" height="42"><path d="M12 26c0-4 3-7 7-7 1 0 2 .2 3 .6C24 16 28 13 33 13c5 0 9.5 3.5 10.3 8.5 1-.7 2.2-1.1 3.7-1.1 3.5 0 6 2.5 6 6s-2.5 6-6 6H12V26z" fill="#B0B0B0"/><path d="M22 34c0-3.5 2.5-6.5 6-6.5 1 0 1.8.3 2.6.7C32 25 36 22 40 22c4.5 0 8 3 8.8 7.5 1-.6 2-.9 3.2-.9 3 0 5 2 5 5s-2 5-5 5H22V34z" fill="#C0C0C0"/><path d="M28 40c0-3 2-5 5-5 .7 0 1.5.2 2 .5C36 33 39 31 43 31c3.5 0 6.5 2.5 7 6 .7-.4 1.5-.6 2.5-.6 2.5 0 4 1.5 4 4s-1.5 4-4 4H28V40z" fill="#D0D0D0"/><line x1="22" y1="46" x2="14" y2="58" stroke="#50B4E6" stroke-width="4.5" stroke-linecap="round"/><line x1="34" y1="46" x2="26" y2="58" stroke="#50B4E6" stroke-width="4.5" stroke-linecap="round"/></svg>;
const svgRain=<svg viewBox="0 0 64 64" width="42" height="42"><path d="M16 36c0-5 4-9 9-9 1.2 0 2.5.3 3.6.9C30.5 22 35 19 41 19c6.5 0 12 5 12.8 11.5 1.2-.8 2.8-1.3 4.5-1.3 4.5 0 8 3.5 8 8s-3.5 8-8 8H16V36z" fill="#CCCCCC"/><line x1="24" y1="46" x2="18" y2="56" stroke="#50B4E6" stroke-width="4" stroke-linecap="round"/><line x1="34" y1="46" x2="28" y2="56" stroke="#50B4E6" stroke-width="4" stroke-linecap="round"/><line x1="44" y1="46" x2="38" y2="56" stroke="#50B4E6" stroke-width="4" stroke-linecap="round"/><line x1="54" y1="46" x2="48" y2="56" stroke="#50B4E6" stroke-width="4" stroke-linecap="round"/></svg>;
const svgSnow=<svg viewBox="0 0 64 64" width="42" height="42"><path d="M12 26c0-4 3-7 7-7 1 0 2 .2 3 .6C24 16 28 13 33 13c5 0 9.5 3.5 10.3 8.5 1-.7 2.2-1.1 3.7-1.1 3.5 0 6 2.5 6 6s-2.5 6-6 6H12V26z" fill="#B0B0B0"/><path d="M22 34c0-3.5 2.5-6.5 6-6.5 1 0 1.8.3 2.6.7C32 25 36 22 40 22c4.5 0 8 3 8.8 7.5 1-.6 2-.9 3.2-.9 3 0 5 2 5 5s-2 5-5 5H22V34z" fill="#C0C0C0"/><path d="M28 40c0-3 2-5 5-5 .7 0 1.5.2 2 .5C36 33 39 31 43 31c3.5 0 6.5 2.5 7 6 .7-.4 1.5-.6 2.5-.6 2.5 0 4 1.5 4 4s-1.5 4-4 4H28V40z" fill="#D0D0D0"/><path d="M20 46h6M23 43v6" stroke="#E5E8EB" stroke-width="3"/><path d="M34 46h6M37 43v6" stroke="#E5E8EB" stroke-width="3"/><path d="M13 54h6M16 51v6" stroke="#E5E8EB" stroke-width="3"/><path d="M27 54h6M30 51v6" stroke="#E5E8EB" stroke-width="3"/></svg>;
const svgStorm=<svg viewBox="0 0 64 64" width="42" height="42"><path d="M16 36c0-5 4-9 9-9 1.2 0 2.5.3 3.6.9C30.5 22 35 19 41 19c6.5 0 12 5 12.8 11.5 1.2-.8 2.8-1.3 4.5-1.3 4.5 0 8 3.5 8 8s-3.5 8-8 8H16V36z" fill="#CCCCCC"/><polygon points="42,38 52,38 40,52 48,52 34,64 46,47 38,47" fill="#F4D068"/></svg>;
const svgFog=<svg viewBox="0 0 64 64" width="42" height="42"><path d="M14 24c5-3 10-3 15 0s10 3 15 0 10-3 15 0M14 34c5-3 10-3 15 0s10 3 15 0 10-3 15 0M14 44c5-3 10-3 15 0s10 3 15 0 10-3 15 0" fill="none" stroke="#CCCCCC" stroke-width="3.5"/></svg>;
if(rain < 30){
if(code === 0) return isDay ? svgSun : svgMoon;
if(code === 1 || code === 2) return isDay ? svgPartlyCloudyDay : svgPartlyCloudyNight;
if(code === 3) return svgClouds;
if([45,48].includes(code)) return svgFog;
return svgClouds;
}
if([95,96,99].includes(code)) return svgStorm;
if(snow > 0 || [71,73,75,77,85,86].includes(code)) return svgSnow;
if([51,53,55,56,57].includes(code)) return svgLightRain;
return svgRain;
}
function weatherText(c){
if(c===0)return"Αίθριος";if(c===1)return"Κυρίως αίθριος";if(c===2)return"Λίγες νεφώσεις";if(c===3)return"Συννεφιά";
if([45,48].includes(c))return"Ομίχλη";if([51,53,55,56,57].includes(c))return"Ψιλόβροχο";if([61,63,65].includes(c))return"Βροχή";
if([66,67].includes(c))return"Χιονόνερο";if([71,73,75,77].includes(c))return"Χιόνι";if([80,81,82].includes(c))return"Μπόρες";
if([85,86].includes(c))return"Χιονομπόρες";if([95,96,99].includes(c))return"Καταιγίδα";return"Μεταβλητός καιρός";
}
function windDirection(d){if(d===null||d===undefined||isNaN(d))return"—";const dirs=["Β","ΒΒΑ","ΒΑ","ΑΒΑ","Α","ΑΝΑ","ΝΑ","ΝΝΑ","Ν","ΝΝΔ","ΝΔ","ΔΝΔ","Δ","ΔΒΔ","ΒΔ","ΒΒΔ"];return dirs[Math.round(d/22.5)%16];}
const greekDays=["Κυρ","Δευ","Τρί","Τετ","Πέμ","Παρ","Σάβ"];
function formatDate(s){const d=new Date(s+"T12:00:00");return{day:greekDays[d.getDay()],date:d.getDate()+"/"+(d.getMonth()+1)};}
async function searchCity(){
const city=document.getElementById("cityInput").value.trim();if(!city)return;
document.getElementById("forecast").innerHTML=<div class="loading">Αναζήτηση πόλης...</div>;
try{
const res=await fetch("open-meteo.com"+encodeURIComponent(city)+"&count=1&language=el&format=json");
const geo=await res.json();
if(!geo.results||!geo.results.length){alert("Δεν βρέθηκε η πόλη.");return;}
const place=geo.results[0];
locationData={name:place.name,latitude:place.latitude,longitude:place.longitude,country:place.country,countryCode:place.country_code};
await loadWeather();
}catch(e){console.error(e);document.getElementById("forecast").innerHTML=<div class="loading">Σφάλμα φόρτωσης.</div>;}
}
async function loadWeather(){
const lat=locationData.latitude,lon=locationData.longitude;
const common=latitude=${lat}&longitude=${lon}&timezone=auto&forecast_days=15;
const cur="temperature_2m,relative_humidity_2m,apparent_temperature,weather_code,wind_speed_10m,wind_direction_10m,is_day";
const hour="temperature_2m,relative_humidity_2m,apparent_temperature,precipitation,precipitation_probability,snowfall,weather_code,cloud_cover,wind_speed_10m,wind_direction_10m,wind_gusts_10m,is_day";
const day="temperature_2m_max,temperature_2m_min,weather_code,precipitation_sum,precipitation_probability_max,snowfall_sum,wind_speed_10m_max,sunrise,sunset";
try{
const [ecRes,gfsRes]=await Promise.all([fetch(https://open-meteo.com{common}&current=${cur}&hourly=${hour}&daily=${day}&models=ecmwf_ifs025),fetch(https://open-meteo.com{common}&current=${cur}&hourly=${hour}&daily=${day}&models=gfs_seamless)]);
const [ecmwf,gfs]=await Promise.all([ecRes.json(),gfsRes.json()]);
weatherData={ecmwf:ecmwf,gfs:gfs,icon:ecmwf};renderCurrent();renderForecast();
}catch(e){
const ecRes=await fetch(https://open-meteo.com{common}&current=${cur}&hourly=${hour}&daily=${day}&models=ecmwf_ifs025);
const ecmwf=await ecRes.json();weatherData={ecmwf:ecmwf,gfs:ecmwf,icon:ecmwf};renderCurrent();renderForecast();
}
}
function renderCurrent(){
const d=weatherData.ecmwf,c=d.current;
document.getElementById("current").innerHTML=<div class="current"><h2>${locationData.name}<div style="font-size:16px;font-weight:normal;color:#dce5ee;margin-top:7px;">${countryFlag(locationData.countryCode)} ${locationData.country}</div></h2><div class="temperature">${Math.round(c.temperature_2m)}°C</div><div class="condition">${weatherIcon(c.weather_code,c.is_day===1)}<span>${weatherText(c.weather_code)}</span></div><div class="current-grid"><div class="current-box"><span>💧 Υγρασία</span><strong>${Math.round(c.relative_humidity_2m)}%</strong></div><div class="current-box"><span>🌬️ Άνεμος</span>strong>${Math.round(c.wind_speed_10m)} km/h — ${windDirection(c.wind_direction_10m)}</strong></div><div class="current-box"><span>🌡️ Αίσθηση</span>strong>${Math.round(c.apparent_temperature)}°C</strong></div></div></div>;
}
function renderForecast(){
const d=weatherData.ecmwf.daily;let html="";
for(let i=0;i<d.time.length;i++){
const date=formatDate(d.time[i]),rain=Number(d.precipitation_probability_max[i]||0),snow=Number(d.snowfall_sum[i]||0);
html+=<div class="day" onclick="showHourly(${i})"><div class="day-name">${date.day}</div><div class="date">${date.date}</div><div class="icon">${weatherIcon(d.weather_code[i],true,rain,snow)}</div><div class="max">${Math.round(d.temperature_2m_max[i])}°</div><div class="min">${Math.round(d.temperature_2m_min[i])}°</div><div class="rain">💧 ${Math.round(rain)}%</div></div>;
}
document.getElementById("forecast").innerHTML=html;
}
function showHourly(dayIndex){
const d=weatherData.ecmwf.hourly,date=weatherData.ecmwf.daily.time[dayIndex],rows=[];
for(let i=0;i<d.time.length;i++){if(d.time[i].startsWith(date)){rows.push(i);}}
const formatted=formatDate(date);document.getElementById("hourlyTitle").innerText="Πρόγνωση ανά ώρα — "+formatted.day+" "+formatted.date;let html="";
rows.forEach(i=>{
const hour=d.time[i].substring(11,16),temp=Math.round(d.temperature_2m[i]),feels=Math.round(d.apparent_temperature[i]),rain=Math.round(d.precipitation_probability[i]||0),snow=Number(d.snowfall[i]||0),wind=Math.round(d.wind_speed_10m[i]),windDir=windDirection(d.wind_direction_10m[i]),clouds=Math.round(d.cloud_cover[i]),isDay=d.is_day[i]===1;
html+=<div class="hour"><div class="hour-time">${hour}</div><div class="hour-icon">${weatherIcon(d.weather_code[i],isDay,rain,snow)}</div><div class="hour-data">🌡️ <b>${temp}°</b><br>Αίσθ. ${feels}°</div><div class="hour-data">${snow>0?❄️:💧} ${rain}%</div><div class="hour-data">☁️ ${clouds}%</div><div class="hour-data">🌬️ ${wind} km/h<br><b>${windDir}</b></div></div>;
});
document.getElementById("hourly").innerHTML=html;const section=document.getElementById("hourlySection");section.style.display="block";section.scrollIntoView({behavior:"smooth",block:"start"});
}
function closeHourly(){document.getElementById("hourlySection").style.display="none";}
document.getElementById("cityInput").addEventListener("keydown",function(e){if(e.key==="Enter"){searchCity();}});
searchCity();


