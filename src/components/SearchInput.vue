<script>
export default {
  props: {
    fetchCurrentWeather: Function,
    fetchWeeklyWeather: Function
  },
  data() {
    return {
      city: ""
    };
  },
  methods: {
    onSearch: function(value) {
      if (value !== "") {
        this.fetchCurrentWeather(value);
        this.fetchWeeklyWeather(value);
        this.city = "";
      }
    }
  }
};
</script>

<template>
  <a-input-search
    class="weather-search"
    v-model="city"
    placeholder="Город"
    @search="onSearch"
    enterButton
  />
</template>
