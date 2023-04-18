<script>
export default {
  data() {
    return {
      forecast: [], // to store the forecast data
    };
  },
  async created() {
    try {
      const response = await fetch(
        'https://api.openweathermap.org/data/2.5/forecast?q=London,ca&units=metric&appid=9a057b8df457f494562d119c6d8bacd4
'
      );
      const data = await response.json();
      this.forecast = data.list.slice(0, 8); // get the first 8 items for the next 24 hours
    } catch (error) {
      console.error('Failed to fetch forecast data:', error);
    }
  },
};
</script>

<template>
  <div>
    <div v-for="item in forecast" :key="item.dt">
      <div id="w-header">Prediction's timestamp: {{ item.dt }}</div>
      <div id="w-condition">Condition: {{ item.weather[0].description }}</div>
      <div id="w-temperature">Temperature: {{ item.main.temp }} &#8451;</div>
    </div>
  </div>
</template>


<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
