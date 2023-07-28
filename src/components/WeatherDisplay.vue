<template>
  <section>
    <div v-if="doneLoading">
      <h3>Today's weather in <input type="text" @change="fetchWeather" v-model="desiredCity"/> is:</h3>
      <h4>{{ temperatureF }}&deg; F</h4>
      <h4>{{ temperatureC }}&deg; C</h4>
      <h3>It is {{ description }}!</h3>
      <h4 id="weatherIcon">{{ weatherIcon }}</h4>
    </div>

    <div v-else>
      <img src="../assets/loading.gif" />
    </div>
  </section>
</template>

<script>
export default {
    name: 'weather-display',
    data() {
        return {
            desiredCity: 'Tokyo',
            doneLoading: false,
            temperature: 0,
            description: ''
        };
    },
    computed: {
        temperatureC() {
            return this.temperature.toFixed(1)
        },
        temperatureF() {
            return ((this.temperature * 1.8) + 32).toFixed(1);
        },
        weatherIcon() {
            if(this.description === 'Sunny') {
                return '☀️';
            } else if (this.description === 'Cloudy' || this.description === 'Partly cloudy') {
                return '☁️';
            } else if (this.description === 'Raining') {
                return '🌧️';
            }
            return '';
        }
    },
    methods: {
        // Vue Lifecycle Hook
        // API Call
        fetchWeather() {
        // default is a GET request to the URL (string)
        fetch('https://goweather.herokuapp.com/weather/' + this.desiredCity)
        .then((httpResponse) => {
            return httpResponse.json();
        })
        .then((data) => {
            // this happens in the future
            console.log(data)

            this.temperature = parseInt(data.temperature.substring(1, 3));
            this.description = data.description;
            this.doneLoading = true;
        })
        .catch((errorObject) => {
            this.temperature = 0;
            this.description = "Unknown";
            this.doneLoading = true;
            alert("Server Error");
            console.error(errorObject);
        })
        }
    },

    created() {
        this.fetchWeather();
    }
}
</script>

<style scoped>
#weatherIcon {
  font-size: 200px;
  margin-top: -50px;
}
</style>