# PRODIGY_TrackCode_TaskNumber3
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(135deg, #74ABE2, #5563DE);
    }

    .weather-container {
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      padding: 30px;
      border-radius: 20px;
      text-align: center;
      width: 320px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
      color: #fff;
    }

    h1 {
      margin-bottom: 20px;
      font-size: 1.8rem;
    }

    input {
      padding: 10px;
      width: 80%;
      border-radius: 8px;
      border: none;
      outline: none;
      margin-bottom: 15px;
      text-align: center;
    }

    button {
      padding: 10px 20px;
      background: #fff;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
      margin-bottom: 20px;
      transition: transform 0.2s ease, background 0.3s ease;
    }

    button:hover {
      background: #f0f0f0;
      transform: translateY(-2px);
    }

    .weather-info {
      font-size: 1.2rem;
    }

    .icon {
      width: 60px;
      height: 60px;
      margin: 10px auto;
    }
  </style>
</head>
<body>
  <div class="weather-container">
    <h1>Weather App</h1>
    <input type="text" id="city" placeholder="Enter city name">
    <button onclick="getWeather()">Get Weather</button>
    <div class="weather-info" id="weather-info"></div>
  </div>

  <script>
    async function getWeather() {
      const city = document.getElementById('city').value.trim();
      const apiKey = "YOUR_API_KEY"; // Replace with your OpenWeather API key

      if (city === "") {
        alert("Please enter a city name");
        return;
      }

      try {
        const response = await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`
        );

        if (!response.ok) {
          alert("City not found");
          return;
        }

        const data = await response.json();
        const weatherInfo = `
          <h2>${data.name}, ${data.sys.country}</h2>
          <img class="icon" src="https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png" alt="Weather icon">
          <p><strong>${data.main.temp}°C</strong></p>
          <p>${data.weather[0].description}</p>
        `;

        document.getElementById('weather-info').innerHTML = weatherInfo;
      } catch (error) {
        alert("Error fetching weather data");
      }
    }
  </script>
</body>
</html>
