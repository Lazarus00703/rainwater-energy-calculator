<html>
<head>
    <title>Rainwater Energy Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #0a1a44;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            position: relative;
        }
        .container {
            background-color: #3e85ce;
            padding: 30px;
            border-radius: 40px;
            box-shadow: 0 0px 80px rgba(0, 80, 100, 3);
            width: 100%;
            max-width: 600px;
        }
        h2 {
            text-align: center;
            color: #000000;
            margin-bottom: 20px;
        }
        label {
            font-weight: bold;
            margin: 10px 0;
            display: block;
            color: #000000;
        }
        input {
            width: 100%;
            padding: 10px;
            margin: 10px 0 20px 0;
            border-radius: 5px;
            border: 1px solid #ccc;
            box-sizing: border-box;
        }
        button {
            background-color: #5e17eb;
            color: white;
            padding: 15px 32px;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            width: 100%;
        }
        button:hover {
            background-color: #0a1a44;
        }
        h3 {
            color: #000000;
            text-align: center;
        }
        #output {
            font-size: 18px;
            font-weight: bold;
            color: #000000;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Rainwater Energy Calculator</h2>
        <label>Roof Area (m²):</label>
        <input type="number" id="roofArea" placeholder="Enter roof area">
        <label>Rainfall Depth (mm):</label>
        <input type="number" id="rainfall" placeholder="Enter rainfall depth in mm">
        <label>Time of Rainfall (hours, e.g. 1.2):</label>
        <input type="number" step="0.1" id="time" placeholder="Enter rainfall time in hours">
        <label>Height from Gutter to Ground (m):</label>
        <input type="number" id="height" placeholder="Enter height from gutter to ground">
        <button onclick="calculateEnergy()">Calculate</button>
        <h3>Result:</h3>
        <p id="output"></p>
    </div>
    <script>
        function calculateEnergy() {
            let eta_t = 0.85, eta_m = 0.90, eta_g = 0.90;
            let rho = 1000, g = 9.81;
            let A_roof = parseFloat(document.getElementById("roofArea").value);
            let Rainfall_mm = parseFloat(document.getElementById("rainfall").value);
            let time_hours = parseFloat(document.getElementById("time").value);
            let H_total = parseFloat(document.getElementById("height").value);
            // Convert Rainfall from mm to meters
            let Rainfall = Rainfall_mm / 1000;
            // Convert Time from hours to seconds (1 hour = 3600 seconds)
            let t = time_hours * 3600;
            // Height H = Height from Gutter to Ground - 1m
            let H = H_total - 1;
            // Calculate Electrical Power Output
            let P_electrical = eta_t * eta_m * eta_g * rho * g * ((A_roof * Rainfall) / t) * H;
            document.getElementById("output").innerHTML = 
                `Potential Electrical Power: <b>${P_electrical.toFixed(2)} Watts per hour</b>`;
        }
    </script>
</body>
</html>
