<script>
import Weather from "@/pages/Weather";
import "@/styles/weather.scss";

export default {
  name: "App",
  components: {
    Weather
  }
};
</script>

<template>
  <div id="app">
    <Weather />
  </div>
</template>
