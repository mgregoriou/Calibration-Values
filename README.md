# Calibration-Values
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Temperature Lookup</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    label { display: block; margin: 10px 0 5px; }
    select, input, button { padding: 6px; font-size: 14px; }
    #output { margin-top: 20px; font-weight: bold; }
  </style>
</head>
<body>
  <h2>Temperature Lookup Tool</h2>
  <label for="mm">Enter Shrinkage (mm):</label>
  <input type="number" id="mm" step="0.01" placeholder="e.g., 25.50">

  <label for="minutes">Select Minutes:</label>
  <select id="minutes">
    <option value="10">10 Minutes</option>
    <option value="30">30 Minutes</option>
    <option value="60">60 Minutes</option>
    <option value="120">120 Minutes</option>
    <option value="240">240+ Minutes</option>
  </select>

  <button onclick="lookupTemp()">Get Temperature</button>

  <div id="output"></div>

  <script>
    // Example data structure extracted from your PDF reference
    const tempTable = {
      25.50: {10: null, 30: 1733, 60: 1692, 120: 1649, 240: 1623},
      25.70: {10: 1750, 30: 1710, 60: 1661, 120: 1631, 240: 1607},
      26.00: {10: 1711, 30: 1651, 60: 1625, 120: 1615, 240: 1584},
      27.00: {10: 1582, 30: 1558, 60: 1537, 120: 1514, 240: 1502},
      28.00: {10: 1445, 30: null, 60: null, 120: null, 240: null}
      // You would continue filling in values here from your table
    };

    function lookupTemp() {
      const mm = parseFloat(document.getElementById("mm").value).toFixed(2);
      const minutes = document.getElementById("minutes").value;
      const outputDiv = document.getElementById("output");

      if (tempTable[mm] && tempTable[mm][minutes] !== undefined) {
        const temp = tempTable[mm][minutes];
        if (temp) {
          outputDiv.textContent = `At ${mm} mm and ${minutes} minutes, the temperature is ${temp} °C.`;
        } else {
          outputDiv.textContent = `No data available for ${mm} mm at ${minutes} minutes.`;
        }
      } else {
        outputDiv.textContent = "Shrinkage value not found in table.";
      }
    }
  </script>
</body>
</html>
