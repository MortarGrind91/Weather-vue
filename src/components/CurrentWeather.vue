<script>
import { format } from "date-fns";
import { ru } from "date-fns/locale";

export default {
  props: {
    currentWeather: Object
  },

  data() {
    return {
      currentDay: format(new Date(), "EEEE d MMMM", { locale: ru }),
      icon: `http://openweathermap.org/img/wn/${this.currentWeather?.weather[0]?.icon}@2x.png`
    };
  }
};
</script>

<template>
  <div class="weather-current">
    <div class="weather-current__col">
      <div class="weather-current__city">{{ currentWeather.name }}</div>
      <div class="weather-current__day">{{ currentDay }}</div>
      <div class="weather-current__box">
        <div class="weather-current__image">
          <img :src="icon" />
          <p>
            {{ currentWeather.weather[0].description }}
          </p>
        </div>
        <div class="weather-current__temp">{{ Math.ceil(currentWeather.main.temp) }} &#176;</div>
      </div>
    </div>
    <div class="weather-current__col">
      <div>
        <span>Вероятность осадков: </span>
        {{ currentWeather.clouds.all }} %
      </div>
      <div>
        <span>Влажность: </span>
        {{ currentWeather.main.humidity }} %
      </div>
      <div>
        <span>Ветер: </span>
        {{ currentWeather.wind.speed }} км/ч
      </div>
    </div>
  </div>
</template>
