<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Weather App</title>

  <style>
    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
      font-family: Arial, sans-serif;
    }

    body{
      height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;
      background:linear-gradient(135deg,#00c6ff,#0072ff);
    }

    .weather-box{
      width:350px;
      background:white;
      padding:25px;
      border-radius:20px;
      text-align:center;
      box-shadow:0 10px 25px rgba(0,0,0,0.2);
    }

    .search-box{
      display:flex;
      gap:10px;
      margin-bottom:20px;
    }

    .search-box input{
      flex:1;
      padding:12px;
      border:none;
      outline:none;
      border-radius:10px;
      background:#f1f1f1;
      font-size:16px;
    }

    .search-box button{
      padding:12px 16px;
      border:none;
      background:#0072ff;
      color:white;
      border-radius:10px;
      cursor:pointer;
      font-size:16px;
    }

    .weather-icon{
      width:120px;
      margin:10px auto;
    }

    .temp{
      font-size:50px;
      font-weight:bold;
    }

    .city{
      font-size:28px;
      margin-top:5px;
    }

    .details{
      display:flex;
      justify-content:space-between;
      margin-top:25px;
    }

    .details div{
      text-align:center;
    }

    .details h3{
      font-size:18px;
    }

    .details p{
      color:gray;
      margin-top:5px;
    }
  </style>
</head>

<body>

  <div class="weather-box">

    <div class="search-box">
      <input type="text" id="cityInput" placeholder="Enter city name">
      <button onclick="getWeather()">Search</button>
    </div>

    <img src="https://cdn-icons-png.flaticon.com/512/869/869869.png" class="weather-icon">

    <div class="temp" id="temp">--°C</div>
    <div class="city" id="city">Weather App</div>

    <div class="details">
      <div>
        <h3 id="humidity">--%</h3>
        <p>Humidity</p>
      </div>

      <div>
        <h3 id="wind">-- km/h</h3>
        <p>Wind Speed</p>
      </div>
    </div>

  </div>

<script>

async function getWeather(){

  const city = document.getElementById("cityInput").value;

  const apiKey = "YOUR_API_KEY";

  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiKey}`;

  try{

    const response = await fetch(url);
    const data = await response.json();

    document.getElementById("temp").innerHTML =
      Math.round(data.main.temp) + "°C";

    document.getElementById("city").innerHTML =
      data.name;

    document.getElementById("humidity").innerHTML =
      data.main.humidity + "%";

    document.getElementById("wind").innerHTML =
      data.wind.speed + " km/h";

  }

  catch(error){
    alert("City not found");
  }

}

</script>

</body>
</html>
