<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OLMCMC NSD Medication and Fluids Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f9f6f1;
            color: #333;
        }
        h1 {
            color: maroon;
        }
        h2 {
            color: maroon;
            border-bottom: 2px solid maroon;
            padding-bottom: 5px;
        }
        h3 {
            color: maroon;
        }
        label {
            display: block;
            margin-top: 10px;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input[type="number"],
        select {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            background-color: maroon;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 10px;
        }
        button:hover {
            background-color: #b03030;
        }
        .section {
            margin-bottom: 30px;
            background-color: #f7e8e3;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .result {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            background-color: #f7f7f7;
        }
        .result p {
            margin: 0;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            border: 1px solid #ccc;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: maroon;
            color: white;
        }
        tfoot {
            background-color: #f7e8e3;
        }
        .footer {
            margin-top: 40px;
            padding: 10px;
            background-color: maroon;
            color: white;
            text-align: center;
            border-radius: 4px;
        }
        .footer a {
            color: yellow;
            text-decoration: none;
        }
        .footer a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <h1>OLMCMC NSD Medication and Fluids Calculator</h1>

    <!-- Tablet Calculation Section -->
    <div class="section">
        <h2>Tablet Calculation</h2>
        <label for="tabletDose">Desired dose:</label>
        <input type="number" id="tabletDose" name="tabletDose" required>
        <select id="tabletUnit" name="tabletUnit">
            <option value="mg">mg</option>
            <option value="mcg">mcg</option>
            <option value="g">g</option>
        </select>

        <label for="tabletStrength">Stock dose:</label>
        <input type="number" id="tabletStrength" name="tabletStrength" required>
        <select id="tabletStrengthUnit" name="tabletStrengthUnit">
            <option value="mg">mg</option>
            <option value="mcg">mcg</option>
            <option value="g">g</option>
        </select>

        <button type="button" onclick="calculateTablets()">Calculate Tablets</button>
        <div id="tabletResult" class="result"></div>
    </div>

    <!-- IV Medication Calculation Section -->
    <div class="section">
        <h2>IV Medication Calculation</h2>
        <label for="ivDose">Desired dose:</label>
        <input type="number" id="ivDose" name="ivDose" required>
        <select id="ivDoseUnit" name="ivDoseUnit">
            <option value="mg">mg</option>
            <option value="g">g</option>
        </select>

        <label for="ivStrength">Stock dose:</label>
        <input type="number" id="ivStrength" name="ivStrength" required>
        <select id="ivStrengthUnit" name="ivStrengthUnit">
            <option value="mg">mg</option>
            <option value="g">g</option>
        </select>

        <label for="ivVolume">Volume or diluent (mL):</label>
        <input type="number" id="ivVolume" name="ivVolume" required>

        <button type="button" onclick="calculateIV()">Calculate IV Medication</button>
        <div id="ivResult" class="result"></div>
    </div>

    <!-- Drops per Minute Calculation Section -->
    <div class="section">
        <h2>Drops per Minute Calculation (gtts/min)</h2>
        <label for="volumeGtts">Total volume (mL):</label>
        <input type="number" id="volumeGtts" name="volumeGtts" required>

        <label for="hoursGtts">Number of hours:</label>
        <input type="number" id="hoursGtts" name="hoursGtts" required>

        <button type="button" onclick="calculateDrops()">Calculate Drops per Minute</button>
        <div id="dropsResult" class="result"></div>
    </div>

    <!-- Microdrip Calculation Section -->
    <div class="section">
        <h2>Microdrip Calculation (ugtts/min)</h2>
        <label for="volumeMicro">Total volume (mL):</label>
        <input type="number" id="volumeMicro" name="volumeMicro" required>

        <label for="hoursMicro">Number of hours:</label>
        <input type="number" id="hoursMicro" name="hoursMicro" required>

        <button type="button" onclick="calculateMicrodrips()">Calculate Microdrips per Minute</button>
        <div id="microResult" class="result"></div>
    </div>

    <!-- IV Drip Rate Calculation Section -->
    <div class="section">
        <h2>IV Drip Rate Calculation (mL/hr)</h2>
        <label for="dripDose">Desired dose:</label>
        <input type="number" id="dripDose" name="dripDose" required>
        <select id="dripDoseUnit" name="dripDoseUnit">
            <option value="mcg/kg/min">mcg/kg/min</option>
            <option value="mg/kg/min">mg/kg/min</option>
        </select>

        <label for="patientWeight">Patient weight (kg):</label>
        <input type="number" id="patientWeight" name="patientWeight" required>

        <label for="dripStrength">Stock dose:</label>
        <input type="number" id="dripStrength" name="dripStrength" required>
        <select id="dripStrengthUnit" name="dripStrengthUnit">
            <option value="mg">mg</option>
            <option value="mcg">mcg</option>
        </select>

        <label for="dripVolume">Volume (mL):</label>
        <input type="number" id="dripVolume" name="dripVolume" required>

        <button type="button" onclick="calculateDripRate()">Calculate Drip Rate</button>
        <div id="dripResult" class="result"></div>
    </div>

    <h3>Common IV Drip Concentrations</h3>
    <table>
        <thead>
            <tr>
                <th>Medication</th>
                <th>Single Concentration</th>
                <th>Double Concentration</th>
                <th>Quad Concentration</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Dopamine</td>
                <td>200mg in 250mL D5W</td>
                <td>400mg in 500mL D5W</td>
                <td>N/A</td>
            </tr>
            <tr>
                <td>Dobutamine</td>
                <td>250mg in 250mL D5W</td>
                <td>500mg in 500mL D5W</td>
                <td>N/A</td>
            </tr>
            <tr>
                <td>Norepinephrine</td>
                <td>4mg in 100mL NSS or D5W</td>
                <td>8mg in 100mL NSS or D5W</td>
                <td>16mg in 100mL NSS or D5W</td>
            </tr>
            <tr>
                <td>Nicardipine</td>
                <td>10mg in 100mL NSS or D5W</td>
                <td>20mg in 100mL NSS or D 5W</td>
                <td>N/A</td>
            </tr>
        </tbody>
    </table>

    <div class="footer">
        <p>If you have any questions or concerns, please don't hesitate to send your queries to <a href="mailto:nsdtrainingolmcmc@gmail.com">nsdtrainingolmcmc@gmail.com</a>.</p>
    </div>

    <script>
        function convertUnits(value, fromUnit, toUnit) {
            const unitConversion = {
                mcg: 1,
                mg: 1000,
                g: 1000000
            };
            return value * (unitConversion[fromUnit] / unitConversion[toUnit]);
        }

        function calculateTablets() {
            var dose = parseFloat(document.getElementById('tabletDose').value);
            var doseUnit = document.getElementById('tabletUnit').value;
            var strength = parseFloat(document.getElementById('tabletStrength').value);
            var strengthUnit = document.getElementById('tabletStrengthUnit').value;

            if (doseUnit !== strengthUnit) {
                strength = convertUnits(strength, strengthUnit, doseUnit);
            }

            if (!isNaN(dose) && !isNaN(strength)) {
                var tablets = dose / strength;
                document.getElementById('tabletResult').innerHTML = "<p>Number of tablets: " + tablets.toFixed(2) + " tablets</p>";
            } else {
                document.getElementById('tabletResult').innerText = "Please fill out both fields.";
            }
        }

        function calculateIV() {
            var dose = parseFloat(document.getElementById('ivDose').value);
            var doseUnit = document.getElementById('ivDoseUnit').value;
            var strength = parseFloat(document.getElementById('ivStrength').value);
            var strengthUnit = document.getElementById('ivStrengthUnit').value;
            var volume = parseFloat(document.getElementById('ivVolume').value);

            if (doseUnit !== strengthUnit) {
                strength = convertUnits(strength, strengthUnit, doseUnit);
            }

            if (!isNaN(dose) && !isNaN(strength) && !isNaN(volume)) {
                var volumeRequired = (dose / strength) * volume;
                document.getElementById('ivResult').innerHTML = "<p>Volume of IV medication: " + volumeRequired.toFixed(2) + " mL</p>";
            } else {
                document.getElementById('ivResult').innerText = "Please fill out all fields.";
            }
        }

        function calculateDrops() {
            var volume = parseFloat(document.getElementById('volumeGtts').value);
            var hours = parseFloat(document.getElementById('hoursGtts').value);
            var dropFactor = 20;

            if (!isNaN(volume) && !isNaN(hours)) {
                var time = hours * 60; // convert hours to minutes
                var dropsPerMin = (volume * dropFactor) / time;
                document.getElementById('dropsResult').innerHTML = "<p>Drops per minute: " + dropsPerMin.toFixed(2) + " gtts/min</p>";
            } else {
                document.getElementById('dropsResult').innerText = "Please fill out all fields.";
            }
        }

        function calculateMicrodrips() {
            var volume = parseFloat(document.getElementById('volumeMicro').value);
            var hours = parseFloat(document.getElementById('hoursMicro').value);
            var microDropFactor = 60;

            if (!isNaN(volume) && !isNaN(hours)) {
                var time = hours * 60; // convert hours to minutes
                var microdripsPerMin = (volume * microDropFactor) / time;
                document.getElementById('microResult').innerHTML = "<p>Microdrips per minute: " + microdripsPerMin.toFixed(2) + " ugtts/min</p>";
            } else {
                document.getElementById('microResult').innerText = "Please fill out all fields.";
            }
        }

        function calculateDripRate() {
            var dose = parseFloat(document.getElementById('dripDose').value);
            var doseUnit = document.getElementById('dripDoseUnit').value;
            var weight = parseFloat(document.getElementById('patientWeight').value);
            var strength = parseFloat(document.getElementById('dripStrength').value);
            var strengthUnit = document.getElementById('dripStrengthUnit').value;
            var volume = parseFloat(document.getElementById('dripVolume').value);

            // Convert dose to mcg/min
            if (doseUnit === 'mcg/kg/min') {
                dose = dose * weight; // mcg/kg/min to mcg/min
            } else if (doseUnit === 'mg/kg/min') {
                dose = dose * weight * 1000; // mg/kg/min to mcg/min
            }

            // Convert strength to mcg
            if (strengthUnit === 'mg') {
                strength = strength * 1000; // mg to mcg
            }

            if (!isNaN(dose) && !isNaN(weight) && !isNaN(strength) && !isNaN(volume)) {
                var dripRate = (dose * 60 * volume) / strength;
                document.getElementById('dripResult').innerHTML = "<p>Drip rate: " + dripRate.toFixed(2) + " mL/hr</p>";
            } else {
                document.getElementById('dripResult').innerText = "Please fill out all fields.";
            }
        }
    </script>
</body>
</html>
