
<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ελλάδα Weather</title>

<style>
* { box-sizing: border-box; }

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #eef4fa;
  color: #17324d;
}

header {
  background: #1264a3;
  color: white;
  padding: 22px;
  text-align: center;
}

main {
  max-width: 1100px;
  margin: 25px auto;
  padding: 0 16px;
}

select {
  width: 100%;
  padding: 14px;
  border-radius: 12px;
  border: 1px solid #ccdbe7;
  font-size: 16px;
  background: white;
}

.card {
  background: white;
  border-radius: 20px;
  padding: 22px;
  margin: 18px 0;
  box-shadow: 0 4px 15px #0000000d;
}

.current {
  background: linear-gradient(135deg, #1264a3, #53acd9);
  color: white;
}

.temp {
  font-size: 60px;
  font-weight: bold;
  margin: 12px 0;
}

h2 { margin-top: 0; }

.forecast {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
  gap: 10px;
}

.day {
  background: #f1f6fa;
  padding: 14px 8px;
  border-radius: 14px;
  text-align: center;
}

.day strong {
  display: block;
  margin-bottom: 10px;
}

.day .icon {
  font-size: 28px;
  margin-bottom: 10px;
}

.hourly {
  display: flex;
  gap: 10px;
  overflow-x: auto;
}

.hour {
  min-width: 85px;
  background: #f1f6fa;
  border-radius: 12px;
  padding: 12px 8px;
  text-align: center;
}

.info {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.info div { flex: 1; min-width: 120px; }

.muted { color: #657f94; }

#status {
  margin-top: 15px;
  color: #1264a3;
}

@media (max-width: 500px) {
  .temp { font-size: 48px; }
}
</style>
</head>

<body>

<header>
  <h1>🌤️ Ελλάδα Weather</h1>
  <p>Ο καιρός σε όλη την Ελλάδα</p>
</header>

<main>

  <div class="card">
    <h2>📍 Επίλεξε πόλη</h2>
    <select id="city">
      <option value="40.6401,22.9444,Θεσσαλονίκη">Θεσσαλονίκη</option>
      <option value="37.9838,23.7275,Αθήνα">Αθήνα</option>
      <option value="38.2466,21.7346,Πάτρα">Πάτρα</option>
      <option value="39.6390,22.4191,Λάρισα">Λάρισα</option>
      <option value="35.3387,25.1442,Ηράκλειο">Ηράκλειο</option>
      <option value="39.6650,20.8537,Ιωάννινα">Ιωάννινα</option>
      <option value="40.5193,22.2030,Βέροια">Βέροια</option>
      <option value="40.9396,24.4018,Καβάλα">Καβάλα</option>
      <option value="40.2719,22.5120,Κατερίνη">Κατερίνη</option>
      <option value="38.3700,21.4290,Αγρίνιο">Αγρίνιο</option>
      <option value="36.4349,28.2176,Ρόδος">Ρόδος</option>
      <option value="35.5138,24.0180,Χανιά">Χανιά</option>
    </select>
  </div>

  <div id="status">Φόρτωση καιρού...</div>

  <section class="card current">
    <h2 id="place">Θεσσαλονίκη</h2>
    <p id="date">Σήμερα</p>
    <div class="temp" id="temperature">--°C</div>
    <h3 id="condition">Φόρτωση...</h3>

    <div class="info">
      <div>💨 Άνεμος<br><strong id="wind">--</strong></div>
      <div>💧 Υγρασία<br><strong id="humidity">--</strong></div>
      <div>🌅 Ανατολή<br><strong id="sunrise">--</strong></div>
      <div>🌇 Δύση<br><strong id="sunset">--</strong></div>
    </div>
  </section>

  <section class="card">
    <h2>📅 Πρόγνωση 15 ημερών</h2>
    <div class="forecast" id="forecast"></div>
  </section>

  <section class="card">
    <h2>🕒 Ωριαία πρόγνωση</h2>
    <div class="hourly" id="hourly"></div>
  </section>

</main>

<script>
const citySelect = document.getElementById("city");

const weatherText = {
  0: ["☀️", "Καθαρός ουρανός"],
  1: ["🌤️", "Κυρίως αίθριος"],
  2: ["⛅", "Μερική συννεφιά"],
  3: ["☁️", "Συννεφιά"],
  45: ["🌫️", "Ομίχλη"],
  48: ["🌫️", "Ομίχλη"],
  51: ["🌦️", "Ψιλή βροχή"],
  53: ["🌦️", "Ψιλή βροχή"],
  55: ["🌧️", "Ψιλή βροχή"],
  61: ["🌧️", "Βροχή"],
  63: ["🌧️", "Βροχή"],
  65: ["🌧️", "Ισχυρή βροχή"],
  71: ["🌨️", "Χιονόπτωση"],
  73: ["🌨️", "Χιονόπτωση"],
  75: ["❄️", "Ισχυρή χιονόπτωση"],
  80: ["🌦️", "Μπόρες"],
  81: ["🌦️", "Μπόρες"],
  82: ["⛈️", "Ισχυρές μπόρες"],
  95: ["⛈️", "Καταιγίδα"],
  96: ["⛈️", "Καταιγίδα με χαλάζι"],
  99: ["⛈️", "Καταιγίδα με χαλάζι"]
};

function describe(code) {
  return weatherText[code] || ["🌤️", "Άγνωστες συνθήκες"];
}

function formatDate(date) {
  return new Date(date + "T12:00:00").toLocaleDateString("el-GR", {
    weekday: "short",
    day: "numeric",
    month: "short"
  });
}

function formatTime(date) {
  return new Date(date).toLocaleTimeString("el-GR", {
    hour: "2-digit",
    minute: "2-digit"
  });
}

async function loadWeather() {
  const [lat, lon, name] = citySelect.value.split(",");
  document.getElementById("status").textContent = "Φόρτωση δεδομένων...";

  const url =
    "https://api.open-meteo.com/v1/forecast" +
    "?latitude=" + lat +
    "&longitude=" + lon +
    "&current=temperature_2m,relative_humidity_2m,weather_code,wind_speed_10m" +
    "&hourly=temperature_2m,weather_code" +
    "&daily=weather_code,temperature_2m_max,temperature_2m_min,sunrise,sunset" +
    "&forecast_days=15" +
    "&timezone=auto";

  try {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error("Αποτυχία λήψης δεδομένων");
    }

    const data = await response.json();

    const current = data.current;
    const daily = data.daily;

    const [icon, condition] = describe(current.weather_code);

    document.getElementById("place").textContent = name;
    document.getElementById("date").textContent = "Τρέχουσες συνθήκες";
    document.getElementById("temperature").textContent =
      Math.round(current.temperature_2m) + "°C";
    document.getElementById("condition").textContent =
      icon + " " + condition;
    document.getElementById("wind").textContent =
      Math.round(current.wind_speed_10m) + " km/h";
    document.getElementById("humidity").textContent =
      current.relative_humidity_2m + "%";
    document.getElementById("sunrise").textContent =
      formatTime(daily.sunrise[0]);
    document.getElementById("sunset").textContent =
      formatTime(daily.sunset[0]);

    const forecast = document.getElementById("forecast");
    forecast.innerHTML = "";

    for (let i = 0; i < 15; i++) {
      const [dayIcon, dayCondition] = describe(daily.weather_code[i]);

      const card = document.createElement("div");
      card.className = "day";

      card.innerHTML =
        "<strong>" + formatDate(daily.time[i]) + "</strong>" +
        "<div class='icon'>" + dayIcon + "</div>" +
        "<b>" + Math.round(daily.temperature_2m_max[i]) + "°</b>" +
        " / " + Math.round(daily.temperature_2m_min[i]) + "°" +
        "<p class='muted'>" + dayCondition + "</p>";

      forecast.appendChild(card);
    }

    const hourly = document.getElementById("hourly");
    hourly.innerHTML = "";

    const now = new Date();
    let shown = 0;

    for (let i = 0; i < data.hourly.time.length && shown < 24; i++) {
      const time = new Date(data.hourly.time[i]);

      if (time >= now) {
        const [hourIcon] = describe(data.hourly.weather_code[i]);

        const card = document.createElement("div");
        card.className = "hour";

        card.innerHTML =
          "<strong>" + formatTime(data.hourly.time[i]) + "</strong>" +
          "<div>" + hourIcon + "</div>" +
          "<b>" + Math.round(data.hourly.temperature_2m[i]) + "°C</b>";

        hourly.appendChild(card);
        shown++;
      }
    }

    document.getElementById("status").textContent =
      "Τα δεδομένα ενημερώθηκαν.";

  } catch (error) {
    document.getElementById("status").textContent =
      "Δεν ήταν δυνατή η φόρτωση του καιρού. Δοκίμασε ξανά.";
    console.error(error);
  }
}

citySelect.addEventListener("change", loadWeather);
loadWeather();
</script>

</body>
</html>
