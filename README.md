<!DOCTYPE html>
<html lang="el">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Η Σελίδα Καιρού Μου</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #74b9ff, #0984e3);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #2d3436;
        }

        .weather-card {
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
            width: 100%;
            max-width: 400px;
            text-align: center;
            backdrop-filter: blur(10px);
        }

        h1 {
            font-size: 1.8rem;
            margin-bottom: 20px;
            color: #0984e3;
        }

        .search-box {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
        }

        input {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #dfe6e9;
            border-radius: 10px;
            outline: none;
            font-size: 1rem;
            transition: 0.3s;
        }

        input:focus {
            border-color: #0984e3;
        }

        button {
            background: #0984e3;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.3s;
        }

        button:hover {
            background: #0061b5;
        }

        .weather-info {
            display: none; /* Εμφανίζεται μετά την αναζήτηση */
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .city-name {
            font-size: 1.5rem;
            font-weight: 600;
            margin-bottom: 10px;
        }

        .temp {
            font-size: 3.5rem;
            font-weight: bold;
            margin-bottom: 10px;
            color: #2d3436;
        }

        .description {
            font-size: 1.1rem;
            text-transform: capitalize;
            color: #636e72;
            margin-bottom: 15px;
        }

        .details {
            display: flex;
            justify-content: space-around;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

    <div class="weather-card">
        <h1>Πρόγνωση Καιρού</h1>
        
        <div class="search-box">
            <input type="text" id="city-input" placeholder="Εισάγετε πόλη (π.χ. Αθήνα)...">
            <button id="search-btn">Αναζήτηση</button>
        </div>

        <!-- Τα δεδομένα θα εμφανιστούν εδώ -->
        <div class="weather-info" id="weather-info">
            <div class="city-name" id="city">Αθήνα</div>
            <div class="temp" id="temp">24°C</div>
            <div class="description" id="desc">Καθαρός Ουρανός</div>
            
            <div class="details">
                <div>💧 Υγρασία: <span id="humidity">45%</span></div>
                <div>💨 Άνεμος: <span id="wind">12 km/h</span></div>
            </div>
        </div>
    </div>

    <script>
        document.getElementById('search-btn').addEventListener('click', function() {
            const city = document.getElementById('city-input').value;
            if (city.trim() === "") {
                alert("Παρακαλώ εισάγετε μια πόλη!");
                return;
            }

            // Εδώ προσομοιώνουμε τη λήψη δεδομένων. 
            // Στο μέλλον μπορείτε να συνδέσετε ένα πραγματικό API (π.χ. OpenWeatherMap)
            document.getElementById('city').innerText = city;
            document.getElementById('temp').innerText = Math.floor(Math.random() * (35 - 10) + 10) + "°C";
            document.getElementById('desc').innerText = "Συννεφιά με διαστήματα ηλιοφάνειας";
            document.getElementById('humidity').innerText = Math.floor(Math.random() * (80 - 40) + 40) + "%";
            document.getElementById('wind').innerText = Math.floor(Math.random() * 30) + " km/h";

            // Εμφάνιση του κουτιού με τα αποτελέσματα
            document.getElementById('weather-info').style.display = 'block';
        });
    </script>

</body>
</html>
