<template>
    <div id="app">
        <main>
                <div class="search-box">
                    <input type="text" class="search-bar" placeholder="Введите название города..." v-model="inputCity" @keydown="Weather" />
                </div>

            <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">

                <div class="weather-additionally-box">
                    <div class="overcast">{{weather.weather[0].description}}</div>
                    <div class="temp">{{ Math.round(weather.main.temp) - 273 }}°</div>
                    <div class="temp-values">Min temp: {{Math.round(weather.main.temp_min) - 273 }}°
                      <br> Max temp: {{ Math.round(weather.main.temp_max) - 273 }}°</div>
                </div>
                    <div class="info-box">
                      <div class="Humidity">Humidity: {{ weather.main.humidity }}%</div>
                      <div class="Pressure">Pressure: {{ weather.main.pressure }}mm</div>
                    <div class="Speed">Speed:  {{ weather.wind.speed }}m/s</div>
                    <div class="Sunrise">Sunrise: {{new Date(weather.sys.sunrise * 1000).toLocaleTimeString().slice(0, 5)}}</div>
                    <div class="Sunset">Sunset: {{new Date(weather.sys.sunset * 1000).toLocaleTimeString().slice(0, 5)}}</div>
                    </div>
            </div>
        </main>
    </div>
</template>





<script>
    export default {
        name: 'app',

        data() {
            return {
                url: 'https://api.openweathermap.org/data/2.5/', key: '6787da7b9818dce19a11feb79e91ca86',
                inputCity: '', weather: {}
            }
        },

        methods: {

            Weather(c) {
                if (c.key == "Enter")
                {
                  fetch(`${this.url}weather?q=${this.inputCity}&appid=${this.key}`).then(result => { return result.json(); }).then(this.Info);
                }
            },

            Info(results) {
                this.weather = results;
            },

        }
    }
</script>






<style>

    #app {
      background-image: url('assets/fontan.jpg');
        background-position: bottom;
        background-size: cover;
    }

    * {
    margin: 0;
    padding: 0;
    }

    main {
        min-height: 100vh;
        padding: 60px;

    }

    .search-box {
        width: 25%;

            }

        .search-box .search-bar {
            display: block;
            width: 100%;
            padding: 10px;
            font-size: 25px;
            border: none;
            outline: none;
            box-shadow: 0px 0px 8px rgba(0, 0, 0, 255);
            background-color: rgba(255, 255, 255, 0.5);
        }

         .weather-additionally-box{
            display: inline-block;
            text-align: center;
            color: #FFF;
            font-size: 60px;
            font-weight: 300;
            background-color: rgba(255, 255, 255, 0.05);
            border-radius: 16px;
            margin: -50px 600px;
         }

       .weather-additionally-box .temp {
         display: inline-block;
        padding: 10px 25px;
        color: #FFF;
        font-size: 160px;
        font-weight: 900;
        text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
        background-color: rgba(255, 255, 255, 0.25);
        border-radius: 16px;
        margin: 40px;
        box-shadow: 3px 6px rgba(0, 0, 0, 0.25);

      }

    .weather-additionally-box .overcast {
      padding: 25px;
      vertical-align: middle;

    }

        .weather-additionally-box .temp-values {
          color: #FFF;
          font-size: 48px;
          font-weight: 700;
          font-style: italic;
          text-shadow: 3px 6px rgba(0, 0, 0, 0.25);

        }

    .info-box {
      display: inline-block;
      text-align: center;
      color: #FFF;
      font-size: 40px;
      font-weight: 100;
      background-color: rgba(255, 255, 255, 0);
      border-radius: 16px;
      margin: -300px 100px;
    }


</style>

