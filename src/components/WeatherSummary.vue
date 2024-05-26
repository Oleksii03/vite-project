<script setup>
const props = defineProps({
  weatherInfo: Object,
});
</script>

<!-- -----template------- -->

<template>
  <div v-if="weatherInfo?.weather" class="summary">
    <div class="pic-main">{{ weatherInfo?.weather[0].main.toUpperCase() }}</div>
    <div class="weather">
      <div class="temp">{{ Math.round(weatherInfo?.main?.temp) }} °C</div>
      <div class="weather-desc text-block">
        {{ weatherInfo?.weather[0].description }}
      </div>
    </div>
    <div class="city text-block">
      {{ `${weatherInfo?.name} ${weatherInfo?.sys?.country}` }}
    </div>
    <br />
    <div class="date text-block">Thu, March 16, 2023</div>
  </div>
</template>

<!-- -----style------- -->

<style scoped lang="scss">
@import "../assets/styles/main.scss";

.pic-main {
  width: 60px;
  height: 60px;
  margin: 20px 0 12px;
  background-repeat: no-repeat;
  background-position: 50% 50%;
  background-size: contain;
  // background-image: url("../assets/img/weather-main/thunderstorm.png");
}

.city {
  font-size: 24px;
}

.weather {
  margin: 0 0 20px;
  padding: 20px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.4);
}

.temp {
  padding-bottom: 8px;
  font-size: 32px;
}

.text-block {
  position: relative;
  padding-left: 24px;
  padding-bottom: 8px;
  font-size: 14px;

  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 20px;
    height: 20px;
    margin-right: 6px;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    background-size: contain;
  }
}

.weather-desc {
  &::before {
    background-image: url("/src/assets/img/weather.svg");
  }

  &::first-letter {
    text-transform: uppercase;
  }
}

.city {
  &::before {
    background-image: url("/src/assets/img/location.svg");
  }
}

.date {
  &::before {
    left: 2px;
    width: 15px;
    height: 15px;
    background-image: url("/src/assets/img/calendar.svg");
  }
}
</style>
