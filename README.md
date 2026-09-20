<!DOCTYPE html>
<html lang="el">

<head>

<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>


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
    position:relative;
    background:
        rgba(3,20,38,.72);
    padding:28px 60px 28px 20px;
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
   MENU
===================================== */

.menu-button{
    position:absolute;
    top:18px;
    right:18px;
    width:43px;
    height:43px;
    border:0;
    border-radius:12px;
    background:rgba(255,255,255,.12);
    color:#fff;
    font-size:25px;
    cursor:pointer;
    display:flex;
    align-items:center;
    justify-content:center;
    transition:.18s;
}

.menu-button:hover{
    background:rgba(255,255,255,.22);
}

.menu{
    display:none;
    position:absolute;
    top:68px;
    right:18px;
    width:240px;
    max-height:70vh;
    overflow-y:auto;
    background:rgba(5,27,50,.97);
    border:1px solid rgba(255,255,255,.18);
    border-radius:15px;
    padding:8px;
    z-index:1000;
    box-shadow:0 10px 30px rgba(0,0,0,.35);
}

.menu.open{
    display:block;
}

.menu-item{
    width:100%;
    border:0;
    background:transparent;
    color:#fff;
    text-align:left;
    padding:13px 12px;
    border-radius:10px;
    font-size:14px;
    cursor:pointer;
}

.menu-item:hover{
    background:rgba(255,255,255,.12);
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
   ΙΣΤΟΡΙΚΟ
===================================== */

.history-section{
    display:none;
    margin-top:28px;
    background:
        rgba(5,27,50,.72);
    border-radius:20px;
    padding:20px;
}

.history-header{
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

.history-header h3{
    margin:0;
    font-size:21px;
}

.close-history{
    background:
        rgba(255,255,255,.15);
    border:0;
    color:white;
    border-radius:10px;
    padding:8px 13px;
    cursor:pointer;
}

.history{
    display:grid;
    gap:9px;
}


/* =====================================
   ΙΣΤΟΡΙΚΟ ΕΤΩΝ
===================================== */

.history-years{
    display:grid;
    grid-template-columns:
        repeat(2,1fr);
    gap:12px;
}

.history-year-button,
.history-month-button,
.history-back-button{
    border:0;
    color:#fff;
    background:
        rgba(65,96,130,.72);
    border-radius:14px;
    padding:17px 12px;
    font-size:15px;
    font-weight:bold;
    cursor:pointer;
    transition:.18s;
}

.history-year-button:hover,
.history-month-button:hover,
.history-back-button:hover{
    background:
        rgba(72,105,143,.95);
    transform:
        translateY(-2px);
}

.history-months{
    display:grid;
    grid-template-columns:
        repeat(3,1fr);
    gap:10px;
}

.history-navigation{
    display:flex;
    gap:10px;
    margin-bottom:15px;
    flex-wrap:wrap;
}

.history-back-button{
    padding:10px 14px;
    font-size:14px;
}


/* =====================================
   ΗΜΕΡΕΣ ΙΣΤΟΡΙΚΟΥ
===================================== */

.history-days{
    display:grid;
    grid-template-columns:
        repeat(6,minmax(0,1fr));
    gap:9px;
}

.history-day{
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    min-width:0;
    min-height:88px;
    background:
        rgba(65,96,130,.62);
    border-radius:13px;
    padding:10px 6px;
    gap:5px;
    cursor:pointer;
    transition:.18s;
    border:1px solid transparent;
}

.history-day:hover{
    background:
        rgba(72,105,143,.90);
    border-color:
        rgba(255,255,255,.20);
    transform:translateY(-2px);
}

.history-day:active{
    transform:scale(.98);
}

.history-date{
    font-weight:bold;
    font-size:14px;
    text-align:center;
    white-space:nowrap;
}

.history-icon{
    font-size:25px;
    text-align:center;
    height:32px;
    display:flex;
    align-items:center;
    justify-content:center;
}

.history-temperature{
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    gap:2px;
    font-size:12px;
    line-height:1.25;
    text-align:center;
}

.history-temperature .day-temp{
    font-weight:bold;
}

.history-temperature .night-temp{
    color:#d0d7df;
}

.history-data{
    font-size:12px;
    color:#e4e8ed;
    line-height:1.4;
    text-align:center;
}


/* =====================================
   ΙΣΤΟΡΙΚΗ ΩΡΙΑΙΑ
   ΙΔΙΟ ΣΧΗΜΑ ΜΕ ΤΗΝ ΚΑΝΟΝΙΚΗ
===================================== */

.history-hourly{
    grid-column:1 / -1;
    width:100%;
    margin-top:4px;
    margin-bottom:4px;
    background:
        rgba(5,27,50,.72);
    border-radius:20px;
    padding:20px;
}

.history-hourly-header{
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

.history-hourly-header h3{
    margin:0;
    font-size:21px;
}

.close-history-hourly{
    background:
        rgba(255,255,255,.15);
    border:0;
    color:white;
    border-radius:10px;
    padding:8px 13px;
    cursor:pointer;
}

.history-hourly-list{
    display:grid;
    gap:8px;
}

.history-hour{
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

.history-hour-time{
    font-weight:bold;
}

.history-hour-icon{
    font-size:25px;
    text-align:center;
    height:32px;
    display:flex;
    align-items:center;
    justify-content:center;
}

.history-hour-data{
    font-size:13px;
    color:#e4e8ed;
    line-height:1.5;
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

    .history-years{
        grid-template-columns:
            1fr;
    }

    .history-months{
        grid-template-columns:
            repeat(3,1fr);
    }

    .history-days{
        grid-template-columns:
            repeat(6,minmax(0,1fr));
        gap:7px;
    }

    .history-day{
        min-height:78px;
        padding:8px 3px;
    }

    .history-date{
        font-size:13px;
    }

    .history-icon{
        font-size:22px;
    }

    .history-data{
        font-size:11px;
    }

    .history-temperature{
        font-size:10px;
    }

    .history-hourly{
        padding:20px;
    }

    .history-hour{
        grid-template-columns:
            55px
            40px
            1fr
            1fr;
    }

    .history-hour-data:nth-child(5),
    .history-hour-data:nth-child(6){
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

    .menu{
        right:10px;
        width:225px;
    }

    .history-months{
        grid-template-columns:
            repeat(2,1fr);
    }

    .history-days{
        grid-template-columns:
            repeat(6,minmax(0,1fr));
        gap:5px;
    }

    .history-day{
        min-height:70px;
        border-radius:10px;
        padding:7px 2px;
    }

    .history-date{
        font-size:12px;
    }

    .history-icon{
        font-size:20px;
        height:27px;
    }

    .history-data{
        font-size:10px;
    }

    .history-temperature{
        font-size:9px;
    }

    .history-hourly{
        padding:15px;
        border-radius:16px;
    }

    .history-hourly-header h3{
        font-size:17px;
    }

    .history-hour{
        grid-template-columns:
            48px
            36px
            1fr
            1fr;
        padding:10px 7px;
        gap:6px;
    }

    .history-hour-data{
        font-size:11px;
    }

    .history-hour-icon{
        font-size:22px;
    }

}


/* =====================================
   HISTORY DATE — COMPACT
===================================== */

.history-date{
    line-height:1.1;
}

.history-date .history-day-number{
    display:block;
    font-size:14px;
    font-weight:bold;
}

.history-date .history-month-year{
    display:block;
    font-size:10px;
    color:#d0d7df;
    margin-top:2px;
}

@media(max-width:750px){

    .history-date .history-day-number{
        font-size:13px;
    }

    .history-date .history-month-year{
        font-size:9px;
    }

}

@media(max-width:430px){

    .history-date .history-day-number{
        font-size:12px;
    }

    .history-date .history-month-year{
        font-size:8px;
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


        <button
            class="menu-button"
            onclick="toggleMenu()"
            aria-label="Μενού">

            ☰

        </button>


        <div
            id="menu"
            class="menu">

            <button class="menu-item"
                    onclick="loadHistory(1)">
                📜 Ιστορικό καιρού — τελευταίο 1 έτος
            </button>

            <button class="menu-item"
                    onclick="loadHistory(2)">
                📜 Ιστορικό καιρού — τελευταία 2 χρόνια
            </button>

            <button class="menu-item"
                    onclick="loadHistory(3)">
                📜 Ιστορικό καιρού — τελευταία 3 χρόνια
            </button>

            <button class="menu-item"
                    onclick="loadHistory(4)">
                📜 Ιστορικό καιρού — τελευταία 4 χρόνια
            </button>

            <button class="menu-item"
                    onclick="loadHistory(5)">
                📜 Ιστορικό καιρού — τελευταία 5 χρόνια
            </button>

            <button class="menu-item"
                    onclick="loadHistory(6)">
                📜 Ιστορικό καιρού — τελευταία 6 χρόνια
            </button>

            <button class="menu-item"
                    onclick="loadHistory(7)">
                📜 Ιστορικό καιρού — τελευταία 7 χρόνια
            </button>

            <button class="menu-item"
                    onclick="loadHistory(8)">
                📜 Ιστορικό καιρού — τελευταία 8 χρόνια
            </button>

            <button class="menu-item"
                    onclick="loadHistory(9)">
                📜 Ιστορικό καιρού — τελευταία 9 χρόνια
            </button>

            <button class="menu-item"
                    onclick="loadHistory(10)">
                📜 Ιστορικό καιρού — τελευταία 10 χρόνια
            </button>

        </div>

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
         ΙΣΤΟΡΙΚΟ
    ================================= -->

    <div
        id="historySection"
        class="history-section">

        <div class="history-header">

            <h3 id="historyTitle">
                📜 Ιστορικό καιρού
            </h3>

            <button
                class="close-history"
                onclick="closeHistory()">

                ✕ Κλείσιμο

            </button>

        </div>

        <div
            id="history"
            class="history">
        </div>

    </div>


    <!-- =================================
         INFO
    ================================= -->

    <div class="model-info">

        ECMWF IFS HRES • NOAA GFS • DWD ICON

        <br>

        Ιστορικό: ECMWF ERA5 Reanalysis
        μέσω Open-Meteo — διαθέσιμο από το 1940.

        <br>

        Τα δεδομένα ανανεώνονται αυτόματα
        σύμφωνα με τους κύκλους έκδοσης
        των μοντέλων.

    </div>


</div>



<script>


/* =====================================
   GLOBAL
===================================== */

let weatherData = null;

let locationData = null;

let historyYears = 1;



/* =====================================
   MENU
===================================== */

function toggleMenu(){

    const menu =
        document.getElementById("menu");

    menu.classList.toggle("open");

}


function closeMenu(){

    document
        .getElementById("menu")
        .classList.remove("open");

}


function refreshWeather(){

    closeMenu();

    closeHistory();

    if(locationData){

        loadWeather();

    }else{

        searchCity();

    }

}


function goTop(){

    window.scrollTo({

        top:0,

        behavior:"smooth"

    });

}



/* =====================================
   ΙΣΤΟΡΙΚΟ — 1 ΕΩΣ 10 ΧΡΟΝΙΑ
===================================== */

async function loadHistory(years){

    closeMenu();

    closeHourly();

    closeHistoryHourly();

    if(!locationData){

        alert(
            "Πρώτα αναζήτησε μία τοποθεσία."
        );

        return;

    }

    historyYears = years;


    const historySection =
        document.getElementById(
            "historySection"
        );


    historySection.style.display =
        "block";


    const history =
        document.getElementById(
            "history"
        );


    history.innerHTML = `

        <div class="loading">

            Φόρτωση διαθέσιμων ετών...

        </div>

    `;


    historySection.scrollIntoView({

        behavior:"smooth",

        block:"start"

    });


    renderHistoryYears(years);

}



/* =====================================
   ΕΤΗ
===================================== */

function renderHistoryYears(
    years
){

    const history =
        document.getElementById(
            "history"
        );


    let html = `

        <div class="history-navigation">

            <button
                class="history-back-button"
                onclick="closeHistory()">

                ✕ Κλείσιμο

            </button>

        </div>

        <div class="history-years">

    `;


    const currentYear =
        new Date().getFullYear();


    for(
        let i = 0;
        i < years;
        i++
    ){

        const year =
            currentYear - i;


        html += `

            <button
                class="history-year-button"
                onclick="loadHistoryMonths(${year})">

                📅 ${year}

            </button>

        `;

    }


    html += `

        </div>

    `;


    history.innerHTML =
        html;


    document
        .getElementById("historyTitle")
        .innerText =

        "📜 Ιστορικό καιρού — " +
        locationData.name +
        " — επίλεξε έτος";

}



/* =====================================
   ΜΗΝΕΣ ΕΤΟΥΣ
===================================== */

function loadHistoryMonths(
    year
){

    const history =
        document.getElementById(
            "history"
        );


    const months = [

        "Ιανουάριος",
        "Φεβρουάριος",
        "Μάρτιος",
        "Απρίλιος",
        "Μάιος",
        "Ιούνιος",
        "Ιούλιος",
        "Αύγουστος",
        "Σεπτέμβριος",
        "Οκτώβριος",
        "Νοέμβριος",
        "Δεκέμβριος"

    ];


    let html = `

        <div class="history-navigation">

            <button
                class="history-back-button"
                onclick="showHistoryYearsFromMenu()">

                ← Έτη

            </button>

        </div>

        <div class="history-months">

    `;


    for(
        let month = 1;
        month <= 12;
        month++
    ){

        html += `

            <button
                class="history-month-button"
                onclick="loadHistoryMonth(${year},${month})">

                📅 ${months[month - 1]}

            </button>

        `;

    }


    html += `

        </div>

    `;


    history.innerHTML =
        html;


    document
        .getElementById("historyTitle")
        .innerText =

        "📜 Ιστορικό καιρού — " +
        locationData.name +
        " — " +
        year;

}



function showHistoryYearsFromMenu(){

    renderHistoryYears(historyYears);

}



/* =====================================
   ΦΟΡΤΩΣΗ ΜΗΝΑ ΙΣΤΟΡΙΚΟΥ
   ECMWF ERA5 — ΣΤΑΘΕΡΟ DATASET
===================================== */

async function loadHistoryMonth(
    year,
    month
){

    if(!locationData){

        return;

    }


    const history =
        document.getElementById(
            "history"
        );


    history.innerHTML = `

        <div class="loading">

            Φόρτωση ιστορικού
            ${month}/${year}...

        </div>

    `;


    const monthNames = [

        "Ιανουάριος",
        "Φεβρουάριος",
        "Μάρτιος",
        "Απρίλιος",
        "Μάιος",
        "Ιούνιος",
        "Ιούλιος",
        "Αύγουστος",
        "Σεπτέμβριος",
        "Οκτώβριος",
        "Νοέμβριος",
        "Δεκέμβριος"

    ];


    try{

        const startDate =
            `${year}-${String(month).padStart(2,"0")}-01`;


        const lastDay =
            new Date(
                year,
                month,
                0
            ).getDate();


        const endDate =
            `${year}-${String(month).padStart(2,"0")}-${String(lastDay).padStart(2,"0")}`;


        /*
         * ΣΗΜΑΝΤΙΚΟ:
         *
         * Χρησιμοποιούμε ERA5 και όχι
         * ERA5-Seamless ώστε όλα τα χρόνια
         * του ιστορικού να βασίζονται στο
         * ίδιο συνεπές ιστορικό dataset.
         *
         * Το ERA5 του ECMWF διαθέτει
         * ιστορικά δεδομένα από το 1940.
         */

        const url =

            "https://archive-api.open-meteo.com/v1/archive" +

            "?latitude=" +
            encodeURIComponent(locationData.latitude) +

            "&longitude=" +
            encodeURIComponent(locationData.longitude) +

            "&start_date=" +
            startDate +

            "&end_date=" +
            endDate +

            "&daily=" +
            "weather_code," +
            "temperature_2m_max," +
            "temperature_2m_min," +
            "precipitation_sum," +
            "precipitation_hours," +
            "snowfall_sum" +

            "&models=era5" +

            "&timezone=auto";


        const response =
            await fetch(url);


        if(!response.ok){

            throw new Error(
                "History request failed"
            );

        }


        const data =
            await response.json();


        if(
            !data.daily ||
            !data.daily.time ||
            !data.daily.time.length
        ){

            throw new Error(
                "No history data"
            );

        }


        renderHistoryMonth(
            data,
            year,
            month,
            monthNames[month - 1]
        );


    }catch(error){

        console.error(error);


        history.innerHTML = `

            <div class="loading">

                Δεν ήταν δυνατή η φόρτωση
                του ιστορικού.

                <br><br>

                <button
                    class="history-back-button"
                    onclick="loadHistoryMonths(${year})">

                    ← Επιστροφή στους μήνες

                </button>

            </div>

        `;

    }

}



/* =====================================
   RENDER ΜΗΝΑ
===================================== */

function renderHistoryMonth(
    data,
    year,
    month,
    monthName
){

    const d =
        data.daily;


    const history =
        document.getElementById(
            "history"
        );


    let html = `

        <div class="history-navigation">

            <button
                class="history-back-button"
                onclick="loadHistoryMonths(${year})">

                ← ${year}

            </button>

        </div>

        <div class="history-days">

    `;


    for(
        let i = 0;
        i < d.time.length;
        i++
    ){

        /*
         * Η ημερομηνία χρησιμοποιείται
         * αυτούσια από το API.
         *
         * Δεν γίνεται new Date() για να
         * αποφύγουμε οποιαδήποτε μετατόπιση
         * ημέρας λόγω timezone.
         */

        const rawDate =
            d.time[i];


        const dateParts =
            rawDate.split("-");


        const dayNumber =
            Number(dateParts[2]);


        const monthNumber =
            Number(dateParts[1]);


        const yearNumber =
            Number(dateParts[0]);


        const date =
            `${dayNumber}/${monthNumber}/${yearNumber}`;


        const code =
            Number(
                d.weather_code[i] ?? 0
            );


        const max =
            Math.round(
                Number(
                    d.temperature_2m_max[i]
                )
            );


        const min =
            Math.round(
                Number(
                    d.temperature_2m_min[i]
                )
            );


        /*
         * Ιστορικός υετός:
         *
         * Το historical API δεν παρέχει
         * forecast probability.
         *
         * Επομένως το ποσοστό είναι το
         * ποσοστό των ωρών της ημέρας
         * με καταγεγραμμένο υετό.
         */

        const precipitationHours =
            Number(
                d.precipitation_hours[i] ?? 0
            );


        const rain =
            Math.max(
                0,
                Math.min(
                    100,
                    Math.round(
                        (precipitationHours / 24) * 100
                    )
                )
            );


        /*
         * ΧΙΟΝΙ:
         *
         * Εδώ δεν χρησιμοποιούμε πλέον
         * weather_code ως μοναδικό κριτήριο.
         *
         * Αν snowfall_sum = 0,
         * ΔΕΝ γράφουμε χιόνι.
         */

        const snowfall =
            Number(
                d.snowfall_sum[i] ?? 0
            );


        const hasSnow =
            snowfall > 0;


        /*
         * Για το ιστορικό χρησιμοποιούμε
         * το πραγματικό snowfall_sum.
         */

        const icon =
            weatherIcon(
                code,
                true,
                rain,
                snowfall
            );


        const precipitationIcon =
            hasSnow
                ? "❄️"
                : "💧";


        html += `

            <div
                class="history-day"
                onclick="showHistoryHourly('${rawDate}', this)"
                title="${date}"
            >

                <div class="history-date">

                    <span class="history-day-number">

                        ${dayNumber}

                    </span>

                    <span class="history-month-year">

                        ${String(monthNumber).padStart(2,"0")}/${yearNumber}

                    </span>

                </div>


                <div class="history-icon">

                    ${icon}

                </div>


                <div class="history-temperature">

                    <div class="day-temp">

                        ${max}°

                    </div>

                    <div class="night-temp">

                        ${min}°

                    </div>

                </div>


                <div class="history-data">

                    ${precipitationIcon} ${rain}%

                </div>

            </div>

        `;

    }


    html += `

        </div>

    `;


    history.innerHTML =
        html;


    document
        .getElementById("historyTitle")
        .innerText =

        "📜 Ιστορικό καιρού — " +

        locationData.name +

        " — " +

        monthName +

        " " +

        year;

}



/* =====================================
   ΙΣΤΟΡΙΚΗ ΩΡΙΑΙΑ
   ECMWF ERA5
===================================== */

async function showHistoryHourly(
    date,
    dayElement
){

    const historyDays =
        dayElement.parentElement;


    const oldHourly =
        historyDays.querySelector(
            ".history-hourly"
        );


    if(oldHourly){

        oldHourly.remove();

    }


    const historyHourly =
        document.createElement("div");


    historyHourly.className =
        "history-hourly";


    historyHourly.innerHTML = `

        <div class="history-hourly-header">

            <h3>

                Ωριαία πρόγνωση — ${date}

            </h3>

            <button
                class="close-history-hourly"
                onclick="this.closest('.history-hourly').remove()">

                ✕ Κλείσιμο

            </button>

        </div>

        <div class="history-hourly-list">

            <div class="loading">

                Φόρτωση ιστορικής ωριαίας
                ανάλυσης...

            </div>

        </div>

    `;


    /*
     * Μπαίνει ως ξεχωριστό στοιχείο
     * που πιάνει και τις 6 στήλες.
     */

    historyDays.appendChild(
        historyHourly
    );


    try{

        const url =

            "https://archive-api.open-meteo.com/v1/archive" +

            "?latitude=" +
            encodeURIComponent(locationData.latitude) +

            "&longitude=" +
            encodeURIComponent(locationData.longitude) +

            "&start_date=" +
            date +

            "&end_date=" +
            date +

            "&hourly=" +
            "temperature_2m," +
            "relative_humidity_2m," +
            "apparent_temperature," +
            "precipitation," +
            "snowfall," +
            "weather_code," +
            "cloud_cover," +
            "wind_speed_10m," +
            "wind_direction_10m," +
            "wind_gusts_10m," +
            "is_day" +

            "&models=era5" +

            "&timezone=auto";


        const response =
            await fetch(url);


        if(!response.ok){

            throw new Error(
                "Historical hourly request failed"
            );

        }


        const data =
            await response.json();


        if(
            !data.hourly ||
            !data.hourly.time
        ){

            throw new Error(
                "No hourly history data"
            );

        }


        renderHistoryHourly(
            data,
            historyHourly,
            date
        );


        historyHourly.scrollIntoView({

            behavior:"smooth",

            block:"start"

        });


    }catch(error){

        console.error(error);


        const list =
            historyHourly.querySelector(
                ".history-hourly-list"
            );


        list.innerHTML = `

            <div class="loading">

                Δεν ήταν δυνατή η φόρτωση
                της ιστορικής ωριαίας
                ανάλυσης.

            </div>

        `;

    }

}



/* =====================================
   RENDER ΙΣΤΟΡΙΚΗΣ ΩΡΙΑΙΑΣ
===================================== */

function renderHistoryHourly(
    data,
    container,
    date
){

    const d =
        data.hourly;


    const list =
        container.querySelector(
            ".history-hourly-list"
        );


    let html = "";


    for(
        let i = 0;
        i < d.time.length;
        i++
    ){

        const hour =
            d.time[i]
            .substring(11,16);


        const temp =
            Math.round(
                Number(
                    d.temperature_2m[i]
                )
            );


        const feels =
            Math.round(
                Number(
                    d.apparent_temperature[i]
                )
            );


        const precipitation =
            Number(
                d.precipitation[i] ?? 0
            );


        const snowfall =
            Number(
                d.snowfall[i] ?? 0
            );


        const clouds =
            Math.round(
                Number(
                    d.cloud_cover[i] ?? 0
                )
            );


        const wind =
            Math.round(
                Number(
                    d.wind_speed_10m[i] ?? 0
                )
            );


        const windDir =
            windDirection(
                d.wind_direction_10m[i]
            );


        const windGust =
            Math.round(
                Number(
                    d.wind_gusts_10m[i] ?? 0
                )
            );


        const isDay =
            Number(
                d.is_day[i]
            ) === 1;


        const code =
            Number(
                d.weather_code[i] ?? 0
            );


        const hasSnow =
            snowfall > 0;


        const hasPrecipitation =
            precipitation > 0 ||
            snowfall > 0;


        const icon =
            weatherIcon(
                code,
                isDay,
                hasPrecipitation ? 100 : 0,
                snowfall
            );


        /*
         * Στην ιστορική ωριαία δεν υπάρχει
         * forecast probability.
         *
         * Εμφανίζουμε την πραγματική ποσότητα
         * που καταγράφηκε εκείνη την ώρα.
         */

        let precipitationHTML = "";


        if(hasSnow){

            precipitationHTML = `

                ❄️ ${snowfall.toFixed(1)} cm

            `;

        }else{

            precipitationHTML = `

                💧 ${precipitation.toFixed(1)} mm

            `;

        }


        html += `

            <div class="history-hour">


                <div class="history-hour-time">

                    ${hour}

                </div>


                <div class="history-hour-icon">

                    ${icon}

                </div>


                <div class="history-hour-data">

                    🌡️

                    <b>
                        ${temp}°
                    </b>

                    <br>

                    Αίσθηση
                    ${feels}°

                </div>


                <div class="history-hour-data">

                    ${precipitationHTML}

                </div>


                <div class="history-hour-data">

                    ☁️
                    ${clouds}%

                </div>


                <div class="history-hour-data">

                    🌬️
                    ${wind} km/h

                    <br>

                    Διεύθυνση:
                    <b>
                        ${windDir}
                    </b>

                    <br>

                    Ριπές:
                    ${windGust} km/h

                </div>


            </div>

        `;

    }


    list.innerHTML =
        html;

}



/* =====================================
   CLOSE HISTORY HOURLY
===================================== */

function closeHistoryHourly(){

    document
        .querySelectorAll(
            ".history-hourly"
        )
        .forEach(
            element =>
                element.remove()
        );

}



/* =====================================
   CLOSE HISTORY
===================================== */

function closeHistory(){

    const section =
        document.getElementById(
            "historySection"
        );


    closeHistoryHourly();


    if(section){

        section.style.display =
            "none";

    }

}



/* =====================================
   ΚΛΕΙΣΙΜΟ MENU ΟΤΑΝ ΠΑΤΑΜΕ ΕΞΩ
===================================== */

document.addEventListener(
    "click",
    function(event){

        const menu =
            document.getElementById("menu");

        const button =
            document.querySelector(".menu-button");


        if(
            menu.classList.contains("open") &&
            !menu.contains(event.target) &&
            !button.contains(event.target)
        ){

            menu.classList.remove("open");

        }

    }
);



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


function formatDate(
    dateString,
    includeYear = false
){

    const d =
        new Date(
            dateString +
            "T12:00:00"
        );


    let formattedDate =

        String(d.getDate()) +
        "/" +
        String(d.getMonth() + 1);


    if(includeYear){

        formattedDate +=

            "/" +
            String(d.getFullYear());

    }


    return {

        day:
            greekDays[d.getDay()],

        date:
            formattedDate

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


    closeHistory();


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


        if(snow > 0){

            precipitationInfo =
                `❄️ ${Math.round(rain)}%`;

        }


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
