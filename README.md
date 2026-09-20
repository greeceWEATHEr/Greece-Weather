<!DOCTYPE html>
<html lang="el">

<head>

<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>

<!-- LEAFLET CSS -->
<link
    rel="stylesheet"
    href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
/>


<style>

*{
    box-sizing:border-box;
}

body{
    margin:0;
    font-family:
        Arial,
        Helvetica,
        sans-serif;
    color:#fff;
    background:
        linear-gradient(
            180deg,
            #071d35,
            #0d3762
        );
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
    background:
        rgba(3,20,38,.72);
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
    background:
        rgba(57,85,117,.72);
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
}

.current-grid{
    display:grid;
    grid-template-columns:
        repeat(3,1fr);
    gap:12px;
}

.current-box{
    background:
        rgba(104,133,165,.48);
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
    border-bottom:
        2px solid
        rgba(255,255,255,.55);
    padding-bottom:12px;
    margin-bottom:15px;
}


/* =====================================
   15 ΗΜΕΡΕΣ
===================================== */

.forecast{
    display:grid;
    grid-template-columns:
        repeat(6,1fr);
    gap:12px;
}

.day{
    background:
        rgba(53,84,119,.78);
    border-radius:17px;
    padding:18px 8px;
    text-align:center;
    cursor:pointer;
    transition:.18s;
    border:
        1px solid
        transparent;
}

.day:hover{
    transform:
        translateY(-3px);
    background:
        rgba(72,105,143,.95);
    border-color:
        rgba(255,255,255,.25);
}

.day:active{
    transform:
        scale(.97);
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
    font-size:35px;
    margin:18px 0 12px;
    height:40px;
    display:flex;
    align-items:center;
    justify-content:center;
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
   ΝΥΧΤΕΡΙΝΑ ΕΙΚΟΝΙΔΙΑ
===================================== */

.night-moon{
    display:inline-block;
    filter:
        grayscale(1)
        brightness(.78)
        sepia(.10)
        hue-rotate(175deg);
    opacity:.90;
}

.night-partly-cloudy{
    width:38px;
    height:38px;
    display:inline-block;
    vertical-align:middle;
    background:
        url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Ccircle cx='25' cy='23' r='15' fill='%2395a9bd'/%3E%3Cpath d='M15 42c0-6.5 5.3-11.8 11.8-11.8 4.3 0 8.1 2.3 10.1 5.8 1.1-.4 2.3-.6 3.5-.6 6.3 0 11.4 5.1 11.4 11.4H15.8C15.3 45.6 15 43.8 15 42z' fill='%23c7d0d9'/%3E%3Cpath d='M20 38c1.5-4.6 5.8-7.9 10.9-7.9 4.1 0 7.7 2.1 9.8 5.3' fill='none' stroke='%23e2e7eb' stroke-width='2' stroke-linecap='round'/%3E%3C/svg%3E")
        center/
        contain
        no-repeat;
}


/* =====================================
   ΩΡΙΑΙΑ ΠΡΟΓΝΩΣΗ
===================================== */

.hourly-section{
    display:none;
    margin-top:28px;
    background:
        rgba(5,27,50,.72);
    border-radius:20px;
    padding:20px;
}

.hourly-header{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:10px;
    border-bottom:
        1px solid
        rgba(255,255,255,.3);
    padding-bottom:15px;
    margin-bottom:15px;
}

.hourly-header h3{
    margin:0;
    font-size:21px;
}

.close-hourly{
    background:
        rgba(255,255,255,.15);
    border:0;
    color:white;
    border-radius:10px;
    padding:8px 13px;
    cursor:pointer;
}


/* =====================================
   ΩΡΕΣ
===================================== */

.hourly{
    display:grid;
    gap:8px;
}

.hour{
    display:grid;
    grid-template-columns:
        70px
        50px
        1fr
        1fr
        1fr
        1fr;
    align-items:center;
    background:
        rgba(65,96,130,.62);
    border-radius:12px;
    padding:12px 10px;
    gap:8px;
}

.hour-time{
    font-weight:bold;
}

.hour-icon{
    font-size:25px;
    text-align:center;
    height:32px;
    display:flex;
    align-items:center;
    justify-content:center;
}

.hour-data{
    font-size:13px;
    color:#e4e8ed;
    line-height:1.5;
}


/* =====================================
   ΧΑΡΤΗΣ RADAR ΥΕΤΟΥ
===================================== */

.map-section{
    margin-top:28px;
    background:
        rgba(5,27,50,.72);
    border-radius:20px;
    padding:20px;
}

.map-title{
    font-size:21px;
    font-weight:bold;
    border-bottom:
        1px solid
        rgba(255,255,255,.3);
    padding-bottom:15px;
    margin-bottom:15px;
}

#precipitationMap{
    width:100%;
    height:380px;
    border-radius:15px;
    overflow:hidden;
    background:#dce8f2;
}

.precipitation-info{
    margin-top:10px;
    font-size:12px;
    color:#cbd8e5;
    line-height:1.5;
}


/* =====================================
   MOBILE MAP
===================================== */

@media(max-width:750px){

    #precipitationMap{
        height:330px;
    }

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
   TABLET / MOBILE
===================================== */

@media(max-width:750px){

    .forecast{
        grid-template-columns:
            repeat(3,1fr);
    }

    .current-grid{
        grid-template-columns:
            1fr;
    }

    .hour{
        grid-template-columns:
            55px
            40px
            1fr
            1fr;
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
        grid-template-columns:
            repeat(3,1fr);
        gap:9px;
    }

    .day{
        padding:15px 5px;
    }

    .icon{
        font-size:30px;
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

        <h1>
            🇬🇷 Greece Weather
        </h1>

        <p>
            Πρόγνωση καιρού για όλη την Ελλάδα
        </p>

    </div>


    <!-- =================================
         SEARCH
    ================================= -->

    <div class="search">

        <input
            id="cityInput"
            placeholder="Γράψε πόλη..."
            value="Θεσσαλονίκη"
        >

        <button
            onclick="searchCity()">

            Αναζήτηση

        </button>

    </div>


    <!-- =================================
         CURRENT
    ================================= -->

    <div id="current"></div>


    <!-- =================================
         15 DAYS
    ================================= -->

    <div class="section-title">

        📅 Πρόγνωση 15 ημερών

    </div>


    <div
        id="forecast"
        class="forecast">

        <div class="loading">

            Φόρτωση πρόγνωσης...

        </div>

    </div>


    <!-- =================================
         HOURLY
    ================================= -->

    <div
        id="hourlySection"
        class="hourly-section">


        <div class="hourly-header">

            <h3 id="hourlyTitle"></h3>


            <button
                class="close-hourly"
                onclick="closeHourly()">

                ✕ Κλείσιμο

            </button>

        </div>


        <div
            id="hourly"
            class="hourly">
        </div>


    </div>


    <!-- =================================
         RADAR ΥΕΤΟΥ
    ================================= -->

    <div class="map-section">


        <div class="map-title">

            🌧️ Radar υετού

        </div>


        <div id="precipitationMap"></div>


        <div class="precipitation-info">

            🌧️ Πρόσφατο radar υετού.
            <br>
            Τα χρώματα δείχνουν τα πραγματικά
            ανιχνευμένα φαινόμενα βροχής και χιονιού.

        </div>


    </div>


    <!-- =================================
         INFO
    ================================= -->

    <div class="model-info">

        ECMWF IFS HRES • NOAA GFS • DWD ICON

        <br>

        Τα δεδομένα ανανεώνονται αυτόματα
        σύμφωνα με τους κύκλους έκδοσης
        των μοντέλων.

    </div>


</div>


<!-- LEAFLET JS -->

<script
    src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js">
</script>



<script>


/* =====================================
   RADAR MAP
===================================== */

let precipitationMap =

    L.map(
        "precipitationMap",
        {
            zoomControl:true,
            minZoom:2,
            maxZoom:18
        }
    ).setView(

        [40.6401,22.9444],

        6

    );


/* =====================================
   ΒΑΣΙΚΟΣ ΧΑΡΤΗΣ
===================================== */

L.tileLayer(

    "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",

    {

        attribution:
            "&copy; OpenStreetMap contributors",

        maxZoom:19

    }

).addTo(

    precipitationMap

);



/* =====================================
   MARKER
===================================== */

let precipitationMarker =

    L.marker(

        [40.6401,22.9444]

    )

    .addTo(

        precipitationMap

    )

    .bindPopup(

        "Θεσσαλονίκη"

    );


let precipitationRadar = null;



/* =====================================
   ΦΟΡΤΩΣΗ ΠΡΟΣΦΑΤΟΥ RADAR
===================================== */

async function loadPrecipitationRadar(){

    try{

        const response =

            await fetch(

                "https://api.rainviewer.com/public/weather-maps.json?" +
                Date.now()

            );


        if(!response.ok){

            throw new Error(
                "RainViewer API error"
            );

        }


        const data =

            await response.json();


        if(

            !data.radar ||
            !data.radar.past ||
            !data.radar.past.length

        ){

            console.log(
                "Δεν υπάρχει διαθέσιμο radar."
            );

            return;

        }


        /*
           Παίρνουμε το πιο πρόσφατο
           διαθέσιμο radar frame.
        */

        const latest =

            data.radar.past[
                data.radar.past.length - 1
            ];


        /*
           Πραγματικό RainViewer radar.

           0_1:
           χωρίς smoothing,
           με εμφάνιση χιονιού.

           Το 2 είναι το διαθέσιμο
           Universal Blue χρωματικό
           scheme του public API.
        */

        const radarUrl =

            data.host +

            latest.path +

            "/512/{z}/{x}/{y}/2/0_1.png";


        /*
           Αφαιρούμε το προηγούμενο
           frame πριν μπει το καινούργιο.
        */

        if(precipitationRadar){

            precipitationMap.removeLayer(

                precipitationRadar

            );

        }


        precipitationRadar =

            L.tileLayer(

                radarUrl,

                {

                    opacity:.92,

                    minZoom:2,

                    maxZoom:18,

                    maxNativeZoom:7,

                    tileSize:512,

                    attribution:
                        'Weather data by <a href="https://www.rainviewer.com/" target="_blank">RainViewer</a>'

                }

            );


        precipitationRadar.addTo(

            precipitationMap

        );


    }catch(error){

        console.error(

            "Σφάλμα radar:",

            error

        );

    }

}



/* =====================================
   ΕΝΗΜΕΡΩΣΗ RADAR
===================================== */

function updatePrecipitationMap(

    latitude,

    longitude,

    name

){

    precipitationMap.setView(

        [

            latitude,
            longitude

        ],

        7

    );


    precipitationMarker.setLatLng(

        [

            latitude,
            longitude

        ]

    );


    precipitationMarker

        .bindPopup(name)

        .openPopup();

}



/* =====================================
   ΑΡΧΙΚΟ RADAR
===================================== */

loadPrecipitationRadar();


/*
   Νέο radar frame
   κάθε 10 λεπτά.
*/

setInterval(

    loadPrecipitationRadar,

    10 * 60 * 1000

);



/* =====================================
   GLOBAL
===================================== */

let weatherData = null;

let locationData = null;



/* =====================================
   ΣΗΜΑΙΑ ΧΩΡΑΣ
===================================== */

function countryFlag(countryCode){

    if(!countryCode){

        return "🌍";

    }


    const code =
        countryCode
        .toUpperCase()
        .trim();


    if(code.length !== 2){

        return "🌍";

    }


    return String
        .fromCodePoint(
            ...[...code].map(
                char =>
                    127397 +
                    char.charCodeAt(0)
            )
        );

}



/* =====================================
   WEATHER ICON
===================================== */

function weatherIcon(
    code,
    isDay = true,
    precipitationProbability = 0,
    snowfall = 0
){

    const rain =
        Number(
            precipitationProbability || 0
        );

    const snow =
        Number(
            snowfall || 0
        );


    if(rain < 30){

        if(code === 0){

            if(isDay){

                return "☀️";

            }

            return '<span class="night-moon">🌙</span>';

        }


        if(code === 1){

            if(isDay){

                return "🌤️";

            }

            return '<span class="night-moon">🌙</span>';

        }


        if(code === 2){

            if(isDay){

                return "🌤️";

            }

            return `
                <span
                    class="night-partly-cloudy"
                    aria-label="Λίγες νεφώσεις τη νύχτα">
                </span>
            `;

        }


        if(code === 3){

            return "☁️";

        }


        if(
            [45,48].includes(code)
        ){

            return "🌫️";

        }


        if(
            [
                51,53,55,56,57,
                61,63,65,66,67,
                71,73,75,77,
                80,81,82,
                85,86,
                95,96,99
            ].includes(code)
        ){

            return "☁️";

        }


        if(isDay){

            return "🌤️";

        }

        return '<span class="night-moon">🌙</span>';

    }


    if(
        [95,96,99].includes(code)
    ){

        return "⛈️";

    }


    if(
        snow > 0 ||
        [
            71,73,75,77,
            85,86
        ].includes(code)
    ){

        return "🌨️";

    }


    if(
        [
            51,53,55,56,57,
            61,63,65,66,67,
            80,81,82
        ].includes(code)
    ){

        return "🌧️";

    }


    return "🌧️";

}



/* =====================================
   WEATHER TEXT
===================================== */

function weatherText(code){

    if(code === 0)
        return "Αίθριος";

    if(code === 1)
        return "Κυρίως αίθριος";

    if(code === 2)
        return "Λίγες νεφώσεις";

    if(code === 3)
        return "Συννεφιά";

    if(
        [45,48].includes(code)
    )
        return "Ομίχλη";

    if(
        [51,53,55,56,57].includes(code)
    )
        return "Ψιλόβροχο";

    if(
        [61,63,65].includes(code)
    )
        return "Βροχή";

    if(
        [66,67].includes(code)
    )
        return "Χιονόνερο";

    if(
        [71,73,75,77].includes(code)
    )
        return "Χιόνι";

    if(
        [80,81,82].includes(code)
    )
        return "Μπόρες";

    if(
        [85,86].includes(code)
    )
        return "Χιονομπόρες";

    if(
        [95,96,99].includes(code)
    )
        return "Καταιγίδα";

    return "Μεταβλητός καιρός";

}



/* =====================================
   WIND DIRECTION
===================================== */

function windDirection(degrees){

    if(
        degrees === null ||
        degrees === undefined ||
        isNaN(degrees)
    ){

        return "—";

    }


    const directions = [

        "Β",
        "ΒΒΑ",
        "ΒΑ",
        "ΑΒΑ",
        "Α",
        "ΑΝΑ",
        "ΝΑ",
        "ΝΝΑ",
        "Ν",
        "ΝΝΔ",
        "ΝΔ",
        "ΔΝΔ",
        "Δ",
        "ΔΒΔ",
        "ΒΔ",
        "ΒΒΔ"

    ];


    const index =
        Math.round(
            degrees / 22.5
        ) % 16;


    return directions[index];

}



/* =====================================
   DATE
===================================== */

const greekDays = [

    "Κυρ",
    "Δευ",
    "Τρί",
    "Τετ",
    "Πέμ",
    "Παρ",
    "Σάβ"

];


function formatDate(dateString){

    const d =
        new Date(
            dateString +
            "T12:00:00"
        );


    return {

        day:
            greekDays[d.getDay()],

        date:
            d.getDate() +
            "/" +
            (d.getMonth() + 1)

    };

}



/* =====================================
   SEARCH CITY
===================================== */

async function searchCity(){


    const city =
        document
        .getElementById("cityInput")
        .value
        .trim();


    if(!city)
        return;


    document
        .getElementById("forecast")
        .innerHTML =

        `<div class="loading">

            Αναζήτηση πόλης...

         </div>`;


    try{


        const geoUrl =

            "https://geocoding-api.open-meteo.com/v1/search" +

            "?name=" +
            encodeURIComponent(city) +

            "&count=1" +

            "&language=el" +

            "&format=json";


        const response =
            await fetch(geoUrl);


        const geo =
            await response.json();


        if(
            !geo.results ||
            !geo.results.length
        ){

            alert(
                "Δεν βρέθηκε η πόλη."
            );

            return;

        }


        const place =
            geo.results[0];


        locationData = {

            name:
                place.name,

            latitude:
                place.latitude,

            longitude:
                place.longitude,

            country:
                place.country,

            countryCode:
                place.country_code

        };


        /* ΕΝΗΜΕΡΩΣΗ RADAR */

        updatePrecipitationMap(

            locationData.latitude,

            locationData.longitude,

            locationData.name

        );


        await loadWeather();


    }catch(error){


        console.error(error);


        document
            .getElementById("forecast")
            .innerHTML =

            `<div class="loading">

                Σφάλμα φόρτωσης δεδομένων.

             </div>`;

    }

}



/* =====================================
   LOAD WEATHER
===================================== */

async function loadWeather(){


    const lat =
        locationData.latitude;


    const lon =
        locationData.longitude;



    const common =

        "latitude=" +
        lat +

        "&longitude=" +
        lon +

        "&timezone=auto" +

        "&forecast_days=15";



    const current =

        "temperature_2m," +

        "relative_humidity_2m," +

        "apparent_temperature," +

        "weather_code," +

        "wind_speed_10m," +

        "wind_direction_10m," +

        "is_day";



    const hourly =

        "temperature_2m," +

        "relative_humidity_2m," +

        "apparent_temperature," +

        "precipitation," +

        "precipitation_probability," +

        "snowfall," +

        "weather_code," +

        "cloud_cover," +

        "wind_speed_10m," +

        "wind_direction_10m," +

        "wind_gusts_10m," +

        "is_day";



    const daily =

        "temperature_2m_max," +

        "temperature_2m_min," +

        "weather_code," +

        "precipitation_sum," +

        "precipitation_probability_max," +

        "snowfall_sum," +

        "wind_speed_10m_max," +

        "sunrise," +

        "sunset";



    const ecmwfUrl =

        "https://api.open-meteo.com/v1/forecast?" +

        common +

        "&current=" +
        current +

        "&hourly=" +
        hourly +

        "&daily=" +
        daily +

        "&models=ecmwf_ifs025";



    const gfsUrl =

        "https://api.open-meteo.com/v1/forecast?" +

        common +

        "&current=" +
        current +

        "&hourly=" +
        hourly +

        "&daily=" +
        daily +

        "&models=gfs_seamless";



    const iconUrl =

        "https://api.open-meteo.com/v1/forecast?" +

        common +

        "&current=" +
        current +

        "&hourly=" +
        hourly +

        "&daily=" +
        daily +

        "&models=icon_seamless";



    const [

        ecmwfRes,
        gfsRes,
        iconRes

    ] = await Promise.all([

        fetch(ecmwfUrl),

        fetch(gfsUrl),

        fetch(iconUrl)

    ]);



    const [

        ecmwf,
        gfs,
        icon

    ] = await Promise.all([

        ecmwfRes.json(),

        gfsRes.json(),

        iconRes.json()

    ]);



    weatherData = {

        ecmwf:
            ecmwf,

        gfs:
            gfs,

        icon:
            icon

    };


    renderCurrent();

    renderForecast();

}



/* =====================================
   CURRENT
===================================== */

function renderCurrent(){


    const d =
        weatherData.ecmwf;


    const temp =
        d.current.temperature_2m;


    const humidity =
        d.current.relative_humidity_2m;


    const wind =
        d.current.wind_speed_10m;


    const windDir =
        windDirection(
            d.current.wind_direction_10m
        );


    const feels =
        d.current.apparent_temperature;


    const code =
        d.current.weather_code;


    const isDay =
        d.current.is_day === 1;



    document
        .getElementById("current")
        .innerHTML = `

        <div class="current">

            <h2>

                ${locationData.name}

                <div style="
                    font-size:16px;
                    font-weight:normal;
                    color:#dce5ee;
                    margin-top:7px;
                ">

                    ${countryFlag(
                        locationData.countryCode
                    )}

                    ${locationData.country}

                </div>

            </h2>


            <div class="temperature">

                ${Math.round(temp)}°C

            </div>


            <div class="condition">

                ${weatherIcon(
                    code,
                    isDay
                )}

                ${weatherText(code)}

            </div>


            <div class="current-grid">


                <div class="current-box">

                    <span>
                        💧 Υγρασία
                    </span>

                    <strong>

                        ${Math.round(humidity)}%

                    </strong>

                </div>


                <div class="current-box">

                    <span>
                        🌬️ Άνεμος
                    </span>

                    <strong>

                        ${Math.round(wind)}
                        km/h
                        —
                        ${windDir}

                    </strong>

                </div>


                <div class="current-box">

                    <span>
                        🌡️ Αίσθηση
                    </span>

                    <strong>

                        ${Math.round(feels)}°C

                    </strong>

                </div>


            </div>

        </div>

    `;

}



/* =====================================
   DAILY FORECAST
===================================== */

function renderForecast(){


    const d =
        weatherData.ecmwf.daily;


    let html = "";


    for(
        let i = 0;
        i < d.time.length;
        i++
    ){


        const date =
            formatDate(
                d.time[i]
            );


        const rain =
            Number(
                d.precipitation_probability_max[i]
                || 0
            );


        const snow =
            Number(
                d.snowfall_sum[i]
                || 0
            );


        let precipitationInfo =
            `💧 ${Math.round(rain)}%`;


        html += `

        <div
            class="day"
            onclick="showHourly(${i})"
        >

            <div class="day-name">

                ${date.day}

            </div>


            <div class="date">

                ${date.date}

            </div>


            <div class="icon">

                ${weatherIcon(
                    d.weather_code[i],
                    true,
                    rain,
                    snow
                )}

            </div>


            <div class="max">

                ${Math.round(
                    d.temperature_2m_max[i]
                )}°

            </div>


            <div class="min">

                ${Math.round(
                    d.temperature_2m_min[i]
                )}°

            </div>


            <div class="rain">

                ${precipitationInfo}

            </div>


        </div>

        `;

    }


    document
        .getElementById("forecast")
        .innerHTML =
        html;

}



/* =====================================
   HOURLY
===================================== */

function showHourly(dayIndex){


    const d =
        weatherData.ecmwf.hourly;


    const date =
        weatherData
        .ecmwf
        .daily
        .time[dayIndex];


    const rows = [];


    for(
        let i = 0;
        i < d.time.length;
        i++
    ){

        if(
            d.time[i].startsWith(date)
        ){

            rows.push(i);

        }

    }


    const formatted =
        formatDate(date);


    document
        .getElementById("hourlyTitle")
        .innerText =

        "Πρόγνωση ανά ώρα — " +

        formatted.day +

        " " +

        formatted.date;


    let html = "";


    rows.forEach(i => {


        const hour =
            d.time[i]
            .substring(11,16);


        const temp =
            Math.round(
                d.temperature_2m[i]
            );


        const feels =
            Math.round(
                d.apparent_temperature[i]
            );


        const rain =
            Math.round(
                d.precipitation_probability[i]
                || 0
            );


        const snowfall =
            Number(
                d.snowfall[i]
                || 0
            );


        const wind =
            Math.round(
                d.wind_speed_10m[i]
            );


        const windDir =
            windDirection(
                d.wind_direction_10m[i]
            );


        const clouds =
            Math.round(
                d.cloud_cover[i]
            );


        const isDay =
            d.is_day[i] === 1;



        const icon =
            weatherIcon(
                d.weather_code[i],
                isDay,
                rain,
                snowfall
            );



        let precipitationHTML = "";


        if(snowfall > 0){

            precipitationHTML = `

                ❄️ ${rain}%

            `;

        }else{

            precipitationHTML = `

                💧 ${rain}%

            `;

        }



        html += `

        <div class="hour">


            <div class="hour-time">

                ${hour}

            </div>


            <div class="hour-icon">

                ${icon}

            </div>


            <div class="hour-data">

                🌡️

                <b>
                    ${temp}°
                </b>

                <br>

                Αίσθηση
                ${feels}°

            </div>


            <div class="hour-data">

                ${precipitationHTML}

            </div>


            <div class="hour-data">

                ☁️
                ${clouds}%

            </div>


            <div class="hour-data">

                🌬️
                ${wind} km/h

                <br>

                Διεύθυνση:
                <b>
                    ${windDir}
                </b>

            </div>


        </div>

        `;

    });


    document
        .getElementById("hourly")
        .innerHTML =
        html;


    const section =
        document
        .getElementById(
            "hourlySection"
        );


    section.style.display =
        "block";


    section.scrollIntoView({

        behavior:"smooth",

        block:"start"

    });

}



/* =====================================
   CLOSE HOURLY
===================================== */

function closeHourly(){

    document
        .getElementById(
            "hourlySection"
        )
        .style.display =
        "none";

}



/* =====================================
   ENTER SEARCH
===================================== */

document
    .getElementById("cityInput")
    .addEventListener(
        "keydown",
        function(e){

            if(e.key === "Enter"){

                searchCity();

            }

        }
    );



/* =====================================
   INITIAL LOAD
===================================== */

searchCity();


</script>


</body>

</html>
