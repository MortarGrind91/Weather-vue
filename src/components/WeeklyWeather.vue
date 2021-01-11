<script>
import { format, fromUnixTime } from "date-fns";

export default {
  props: ["weeklyWeather"],
  methods: {
    checkCurrentDay(date) {
      if (date) {
        return format(fromUnixTime(date), "dd.MM HH:mm");
      }
    },
    getImage(iconId) {
      return `http://openweathermap.org/img/w/${iconId}.png`;
    }
  }
};
</script>

<template>
  <div class="weather-weekly">
    <div class="weather-weekly__item" v-for="(item, index) in weeklyWeather.list" :key="index">
      <div class="weather-weekly__time">{{ checkCurrentDay(item.dt) }}</div>
      <div className="weather-weekly__icon">
        <img :src="getImage(item.weather[0].icon)" />
      </div>
      <div class="weather-weekly__temp">{{ Math.round(item.main.temp) }} &#176;</div>
    </div>
  </div>
</template>
