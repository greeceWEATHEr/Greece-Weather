
<!DOCTYPE html>
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Ελλάδα Weather</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg, #e7f5ff, #f8fcff);
  color: #123047;
}

header {
  background: linear-gradient(135deg, #0879c9, #063d78);
  color: white;
  text-align: center;
  padding: 35px 18px;
}

header h1 {
  margin: 0;
  font-size: 36px;
}

header p {
  margin: 10px 0 0;
  font-size: 17px;
}

main {
  max-width: 1100px;
  margin: auto;
  padding: 25px 18px;
}

h2 {
  text-align: center;
  margin-bottom: 22px;
}

.menu {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
  gap: 18px;
}

.menu-button {
  border: none;
  border-radius: 18px;
  padding: 28px 18px;
  background: white;
  box-shadow: 0 5px 20px #00000012;
  cursor: pointer;
  color: #123047;
  transition: transform 0.2s, box-shadow 0.2s;
  font-size: 17px;
}

.menu-button:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 25px #00000025;
}

.menu-icon {
  font-size: 48px;
  display: block;
  margin-bottom: 12px;
}

.menu-button strong {
  display: block;
  font-size: 20px;
  margin-bottom: 8px;
  color: #0879c9;
}

.menu-button span {
  font-size: 14px;
  line-height: 1.5;
}

.page {
  display: none;
}

.page.active {
  display: block;
}

.back-button {
  background: #0879c9;
  color: white;
  border: none;
  padding: 12px 18px;
  border-radius: 10px;
  cursor: pointer;
  font-size: 15px;
  margin-bottom: 20px;
}

.map-box {
  background: white;
  border-radius: 18px;
  padding: 20px;
  box-shadow: 0 5px 20px #00000012;
  margin-bottom: 18px;
}

.map-box h3 {
  margin-top: 0;
}

.map-box a {
  display: inline-block;
  background: #0879c9;
  color: white;
  text-decoration: none;
  padding: 12px 16px;
  border-radius: 9px;
  margin-top: 8px;
}

.map-box p {
  line-height: 1.6;
}

.selector {
  background: white;
  padding: 18px;
  border-radius: 16px;
  box-shadow: 0 5px 20px #00000012;
  margin-bottom: 20px;
}

select {
  width: 100%;
  padding: 13px;
  border-radius: 10px;
  border: 1px solid #aac5d8;
  font-size: 16px;
}

.status {
  margin-top: 12px;
  color: #527084;
}

.current {
  background: white;
  border-radius: 18px;
  padding: 24px;
  box-shadow: 0 5px 20px #00000012;
  margin-bottom: 20px;
}

.temperature {
  font-size: 58px;
  font-weight: bold;
  color: #0879c9;
}

.details,
.forecast {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(145px, 1fr));
  gap: 12px;
}

.detail,
.day {
  background: #edf8ff;
  padding: 14px;
  border-radius: 12px;
}

.day {
  text-align: center;
  background: white;
  box-shadow: 0 4px 15px #0000000d;
}

.icon {
  font-size: 30px;
  margin: 8px;
}

.max {
  color: #df4b35;
  font-weight: bold;
}

.min {
  color: #0879c9;
  font-weight: bold;
}

.note {
  background: #fff8df;
  border-left: 5px solid #d9a51e;
  padding: 14px;
  border-radius: 10px;
  line-height: 1.5;
  margin-top: 20px;
}

footer {
  text-align: center;
  padding: 25px;
  color: #527084;
  font-size: 13px;
}
</style>
</head>

<body>

<header>
  <h1>🌦️ Ελλάδα Weather</h1>
  <p>Μετεωρολογικοί χάρτες και αναλυτική πρόγνωση Ελλάδας</p>
</header>

<main>

<!-- ΑΡΧΙΚΗ ΣΕΛΙΔΑ -->
<section id="homePage" class="page active">

  <h2>Επίλεξε τι θέλεις να δεις</h2>

  <div class="menu">

    <button class="menu-button" onclick="showPage('temperaturePage')">
      <span class="menu-icon">🌡️</span>
      <strong>Θερμοκρασία 850 hPa</strong>
      <span>
        Χάρτες αερίων μαζών και θερμοκρασίας
        περίπου στα 1.500 μέτρα ύψος.
      </span>
    </button>

    <button class="menu-button" onclick="showPage('rainPage')">
      <span class="menu-icon">🌧️</span>
      <strong>Βροχή και χιόνι</strong>
      <span>
        Χάρτες υετού, βροχοπτώσεων και
        χιονοπτώσεων.
      </span>
    </button>

    <button class="menu-button" onclick="showPage('windPage')">
      <span class="menu-icon">💨</span>
      <strong>Άνεμος</strong>
      <span>
        Χάρτες διεύθυνσης και ταχύτητας
        ανέμων στην Ελλάδα και την Ευρώπη.
      </span>
    </button>

    <button class="menu-button" onclick="showPage('forecastPage')">
      <span class="menu-icon">📅</span>
      <strong>Αναλυτικός καιρός Ελλάδας</strong>
      <span>
        Πρόγνωση 15 ημερών με επιλογή πόλης
        και διαθέσιμα πολυμοντελικά δεδομένα.
      </span>
    </button>

  </div>

</section>


<!-- ΧΑΡΤΕΣ ΘΕΡΜΟΚΡΑΣΙΑΣ 850 hPa -->
<section id="temperaturePage" class="page">

  <button class="back-button" onclick="showPage('homePage')">
    ← Επιστροφή στην αρχική
  </button>

  <h2>🌡️ Χάρτες θερμοκρασίας 850 hPa</h2>

  <div class="map-box">
    <h3>ECMWF – Θερμοκρασία αερίων μαζών</h3>
    <p>
      Δες χάρτες θερμοκρασίας στα 850 hPa,
      χρήσιμους για την εκτίμηση των θερμών
      και ψυχρών αερίων μαζών.
    </p>
    <a href="https://www.meteologix.com/" target="_blank">
      Άνοιγμα χαρτών
    </a>
  </div>

  <div class="map-box">
    <h3>GFS – Θερμοκρασία 850 hPa</h3>
    <p>
      Σύγκρινε την πρόγνωση του GFS με άλλα
      παγκόσμια μοντέλα.
    </p>
    <a href="https://www.windy.com/" target="_blank">
      Άνοιγμα Windy
    </a>
  </div>

</section>


<!-- ΧΑΡΤΕΣ ΒΡΟΧΗΣ ΚΑΙ ΧΙΟΝΙΟΥ -->
<section id="rainPage" class="page">

  <button class="back-button" onclick="showPage('homePage')">
    ← Επιστροφή στην αρχική
  </button>

  <h2>🌧️ Χάρτες βροχής και χιονιού</h2>

  <div class="map-box">
    <h3>Χάρτες υετού</h3>
    <p>
      Δες την πρόγνωση βροχής, χιονιού και
      συνολικού υετού για την Ελλάδα.
    </p>
    <a href="https://www.meteologix.com/" target="_blank">
      Άνοιγμα χαρτών υετού
    </a>
  </div>

  <div class="map-box">
    <h3>Ραντάρ βροχής</h3>
    <p>
      Δες την τρέχουσα κίνηση των βροχοπτώσεων
      και των καταιγίδων.
    </p>
    <a href="https://www.rainviewer.com/" target="_blank">
      Άνοιγμα ραντάρ
    </a>
  </div>

</section>


<!-- ΧΑΡΤΕΣ ΑΝΕΜΟΥ -->
<section id="windPage" class="page">

  <button class="back-button" onclick="showPage('homePage')">
    ← Επιστροφή στην αρχική
  </button>

  <h2>💨 Χάρτες ανέμου</h2>

  <div class="map-box">
    <h3>Windy – Άνεμος και ριπές</h3>
    <p>
      Δες την ταχύτητα, τις ριπές και τη
      διεύθυνση των ανέμων.
    </p>
    <a href="https://www.windy.com/" target="_blank">
      Άνοιγμα χαρτών ανέμου
    </a>
  </div>

  <div class="map-box">
    <h3>Earth Nullschool</h3>
    <p>
      Διαδραστική απεικόνιση της κυκλοφορίας
      των ανέμων στην ατμόσφαιρα.
    </p>
    <a href="https://earth.nullschool.net/" target="_blank">
      Άνοιγμα Earth Nullschool
    </a>
  </div>

</section>


<!-- ΑΝΑΛΥΤΙΚΟΣ ΚΑΙΡΟΣ -->
<section id="forecastPage" class="page">

  <button class="back-button" onclick="showPage('homePage')">
    ← Επιστροφή στην αρχική
  </button>

  <h2>📅 Αναλυτικός καιρός Ελλάδας</h2>

  <div class="selector">
    <label for="city">
      <strong>Επίλεξε πόλη:</strong>
    </label>

    <select id="city">
      <option value="40.6401,22.9444,Θεσσαλονίκη">Θεσσαλονίκη</option>
      <option value="37.9838,23.7275,Αθήνα">Αθήνα</option>
      <option value="38.2466,21.7346,Πάτρα">Πάτρα</option>
      <option value="39.639,22.4191,Λάρισα">Λάρισα</option>
      <option value="35.3387,25.1442,Ηράκλειο">Ηράκλειο</option>
      <option value="39.665,20.8537,Ιωάννινα">Ιωάννινα</option>
      <option value="40.5244,22.2053,Βέροια">Βέροια</option>
      <option value="40.9396,24.4018,Καβάλα">Καβάλα</option>
      <option value="40.2686,22.5061,Κατερίνη">Κατερίνη</option>
      <option value="38.6214,21.4078,Αγρίνιο">Αγρίνιο</option>
      <option value="36.4349,28.2176,Ρόδος">Ρόδος</option>
      <option value="35.5138,24.018,Χανιά">Χανιά</option>
    </select>

    <div class="status" id="status">
      Πάτησε την επιλογή για να φορτώσει η πρόγνωση.
    </div>
  </div>

  <div class="current">
    <h2 id="cityName">Θεσσαλονίκη</h2>
    <p id="description">--</p>
    <div class="temperature" id="currentTemp">--°C</div>

    <div class="details">
      <div class="detail">
        🌡️ Μέση μέγιστη:
        <strong id="avgMax">--</strong>
      </div>

      <div class="detail">
        🌡️ Μέση ελάχιστη:
        <strong id="avgMin">--</strong>
      </div>

      <div class="detail">
        🌧️ Πιθανότητα βροχής:
        <strong id="rain">--</strong>
      </div>

      <div class="detail">
        🧮 Διαθέσιμα μοντέλα:
        <strong id="modelCount">--</strong>
      </div>
    </div>
  </div>

  <h2>Πρόγνωση 15 ημερών</h2>
  <div class="forecast" id="forecast"></div>

  <div class="note">
    Οι προβλέψεις είναι εκτιμήσεις από διαθέσιμα
    μετεωρολογικά μοντέλα. Η αβεβαιότητα αυξάνεται
    όσο απομακρυνόμαστε από τη σημερινή ημέρα.
  </div>

</section>

</main>

<footer>
  Ελλάδα Weather
</footer>


<script>
function showPage(pageId) {
  const pages = document.querySelectorAll(".page");

  pages.forEach(page => {
    page.classList.remove("active");
  });

  document.getElementById(pageId).classList.add("active");

  window.scrollTo({
    top: 0,
    behavior: "smooth"
  });

  if (pageId === "forecastPage") {
    loadWeather();
  }
}

const citySelect = document.getElementById("city");
const statusBox = document.getElementById("status");

const models = [
  { name: "ECMWF", id: "ecmwf_ifs025" },
  { name: "GFS", id: "ncep_gfs_global" },
  { name: "ICON", id: "icon_global" },
  { name: "UKMO", id: "ukmo_global_deterministic_10km" },
  { name: "ARPEGE", id: "meteofrance_arpege_world" }
];

function weatherText(code) {
  const texts = {
    0: "☀️ Αίθριος",
    1: "🌤️ Κυρίως αίθριος",
    2: "⛅ Μερική συννεφιά",
    3: "☁️ Συννεφιά",
    45: "🌫️ Ομίχλη",
    48: "🌫️ Παγωμένη ομίχλη",
    51: "🌦️ Ψιλόβροχο",
    53: "🌦️ Ψιλόβροχο",
    55: "🌧️ Έντονο ψιλόβροχο",
    61: "🌦️ Ασθενής βροχή",
    63: "🌧️ Βροχή",
    65: "🌧️ Ισχυρή βροχή",
    71: "🌨️ Ασθενές χιόνι",
    73: "🌨️ Χιονόπτωση",
    75: "❄️ Ισχυρή χιονόπτωση",
    80: "🌦️ Μπόρες",
    81: "🌧️ Ισχυρές μπόρες",
    82: "⛈️ Πολύ ισχυρές μπόρες",
    95: "⛈️ Καταιγίδα",
    96: "⛈️ Καταιγίδα με χαλάζι",
    99: "⛈️ Ισχυρή καταιγίδα με χαλάζι"
  };

  return texts[code] || "Άγνωστος καιρός";
}

function formatDate(dateString) {
  return new Date(dateString + "T12:00:00").toLocaleDateString(
    "el-GR",
    {
      weekday: "short",
      day: "numeric",
      month: "short"
    }
  );
}

async function getModelForecast(lat, lon, model) {
  const params = new URLSearchParams({
    latitude: lat,
    longitude: lon,
    daily: "temperature_2m_max,temperature_2m_min,precipitation_probability_max,weather_code",
    forecast_days: "15",
    timezone: "auto",
    models: model.id
  });

  const response = await fetch(
    "https://api.open-meteo.com/v1/forecast?" + params.toString()
  );

  if (!response.ok) {
    throw new Error(model.name + " δεν είναι διαθέσιμο");
  }

  const data = await response.json();

  if (!data.daily || !data.daily.time) {
    throw new Error("Μη έγκυρα δεδομένα");
  }

  return {
    name: model.name,
    daily: data.daily
  };
}

async function loadWeather() {
  if (!citySelect) return;

  const [lat, lon, cityName] = citySelect.value.split(",");

  document.getElementById("cityName").textContent = cityName;
  statusBox.textContent = "Λήψη δεδομένων από τα διαθέσιμα μοντέλα...";

  const results = await Promise.allSettled(
    models.map(model => getModelForecast(lat, lon, model))
  );

  const successful = results
    .filter(result => result.status === "fulfilled")
    .map(result => result.value);

  if (successful.length === 0) {
    statusBox.textContent =
      "Δεν ήταν δυνατή η λήψη των δεδομένων.";
    return;
  }

  const average = values =>
    values.reduce((sum, value) => sum + value, 0) / values.length;

  const days = successful[0].daily.time.length;
  const forecastBox = document.getElementById("forecast");

  forecastBox.innerHTML = "";

  for (let day = 0; day < days; day++) {
    const maxValues = successful
      .map(item => item.daily.temperature_2m_max[day])
      .filter(value => typeof value === "number");

    const minValues = successful
      .map(item => item.daily.temperature_2m_min[day])
      .filter(value => typeof value === "number");

    const rainValues = successful
      .map(item => item.daily.precipitation_probability_max?.[day])
      .filter(value => typeof value === "number");

    const codes = successful
      .map(item => item.daily.weather_code[day])
      .filter(value => typeof value === "number");

    if (!maxValues.length || !minValues.length) continue;

    const maxAverage = average(maxValues);
    const minAverage = average(minValues);
    const rainAverage = rainValues.length
      ? average(rainValues)
      : null;

    const card = document.createElement("div");
    card.className = "day";

    card.innerHTML = `
      <strong>${formatDate(successful[0].daily.time[day])}</strong>
      <div class="icon">${weatherText(codes[0]).split(" ")[0]}</div>
      <div>${weatherText(codes[0]).substring(2)}</div>
      <p class="max">⬆️ ${maxAverage.toFixed(1)}°C</p>
      <p class="min">⬇️ ${minAverage.toFixed(1)}°C</p>
      <p>🌧️ ${
        rainAverage === null
          ? "—"
          : rainAverage.toFixed(0) + "%"
      }</p>
    `;

    forecastBox.appendChild(card);
  }

  const todayMax = successful
    .map(item => item.daily.temperature_2m_max[0])
    .filter(value => typeof value === "number");

  const todayMin = successful
    .map(item => item.daily.temperature_2m_min[0])
    .filter(value => typeof value === "number");

  document.getElementById("currentTemp").textContent =
    ((average(todayMax) + average(todayMin)) / 2).toFixed(1) + "°C";

  document.getElementById("avgMax").textContent =
    average(todayMax).toFixed(1) + "°C";

  document.getElementById("avgMin").textContent =
    average(todayMin).toFixed(1) + "°C";

  const rainToday = successful
    .map(item => item.daily.precipitation_probability_max?.[0])
    .filter(value => typeof value === "number");

  document.getElementById("rain").textContent =
    rainToday.length
      ? average(rainToday).toFixed(0) + "%"
      : "—";

  document.getElementById("modelCount").textContent =
    successful.length + "/" + models.length;

  document.getElementById("description").textContent =
    "Μέσος όρος των διαθέσιμων μοντέλων για " + cityName;

  statusBox.textContent =
    "Η πρόγνωση φορτώθηκε από " +
    successful.length +
    " διαθέσιμα μοντέλα.";
}

if (citySelect) {
  citySelect.addEventListener("change", loadWeather);
}
</script>

</body>
</html>
