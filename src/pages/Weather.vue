<script>
import SearchInput from "@/components/SearchInput";
import CurrentWeather from "@/components/CurrentWeather";
import WeeklyWeather from "@/components/WeeklyWeather";

//utils
import { apiMethods } from "@/utils/apiMethods";
import { openNotification } from "@/utils/openNotification";

//images
import drizzle from "@/assets/images/Drizzle.jpg";

//video
import weatherVideo from "@/assets/video/weather.mp4";
import sunVideo from "@/assets/video/Sun.mp4";
import cloudsVideo from "@/assets/video/Clouds.mp4";
import rainVideo from "@/assets/video/Rain.mp4";
import snowVideo from "@/assets/video/Snow.mp4";
import mistVideo from "@/assets/video/Mist.mp4";

export default {
  components: {
    SearchInput,
    CurrentWeather,
    WeeklyWeather
  },
  data() {
    return {
      currentWeather: {},
      weeklyWeather: [],
      show: false
    };
  },
  methods: {
    async fetchCurrentWeather(city) {
      try {
        const { data } = await apiMethods.getCurrentWeather(city);
        this.currentWeather = data;
        this.show = true;
      } catch (error) {
        const { data } = error.response;

        openNotification({ type: "error", title: data.cod, text: data.message });
      }
    },
    async fetchWeeklyWeather(city) {
      try {
        const { data } = await apiMethods.getWeeklyWeather(city);
        this.weeklyWeather = data;
      } catch (error) {
        console.log(error.response);
      }
    },
    currentWeatherVideoBg(weather) {
      switch (weather) {
        case "Clear": {
          return sunVideo;
        }
        case "Rain": {
          return rainVideo;
        }
        case "Sun": {
          return sunVideo;
        }
        case "Drizzle": {
          return drizzle;
        }
        case "Clouds": {
          return cloudsVideo;
        }
        case "Snow": {
          return snowVideo;
        }
        case "Mist": {
          return mistVideo;
        }
        default: {
          return weatherVideo;
        }
      }
    }
  }
};
</script>

<template>
  <div class="weather">
    <div class="overlay"></div>
    <video
      autoPlay
      muted
      loop
      id="video"
      :key="currentWeather.weather && currentWeather.weather[0].main"
    >
      <source
        :src="currentWeatherVideoBg(currentWeather.weather && currentWeather.weather[0].main)"
        type="video/mp4"
      />
    </video>
    <a-layout-content class="weather-container">
      <div class="weather-search__container" :class="{ animation: show }">
        <SearchInput
          :fetchCurrentWeather="fetchCurrentWeather"
          :fetchWeeklyWeather="fetchWeeklyWeather"
        />
      </div>
      <div class="weather-info" :class="{ animation: show }" v-if="show">
        <CurrentWeather :currentWeather="currentWeather" />
        <WeeklyWeather :weeklyWeather="weeklyWeather" />
      </div>
    </a-layout-content>
  </div>
</template>
