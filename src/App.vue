<script setup>
import { ref, onMounted } from "vue";
import { API_KEY, BASE_URL } from "./constants";
import WeatherSummary from "./components/WeatherSummary.vue";
import Highlights from "./components/Highlights.vue";

const city = ref(" ");
const weatherInfo = ref(null);

function getWeather() {
  fetch(`${BASE_URL}?q=${city.value}&appid=${API_KEY}&units=metric`)
    .then((response) => {
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      return response.json();
    })
    .then((data) => (weatherInfo.value = data))
    .catch((error) => console.log(error));
}

function getCurrentWeather() {
  let geo = navigator.geolocation;
  console.log(geo);
  geo.getCurrentPosition((pos) => {
    fetch(
      `${BASE_URL}?lat=${pos.coords.latitude}&lon=${pos.coords.longitude}&appid=${API_KEY}&units=metric`
    )
      .then((response) => {
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        return response.json();
      })
      .then((data) => (weatherInfo.value = data))
      .catch((error) => console.log(error));
  });
}

onMounted(getCurrentWeather);
</script>

<template>
  <div class="page">
    <main class="main">
      <div class="container">
        <div class="laptop">
          <div class="sections">
            <section class="section section-left">
              <div class="info">
                <div class="city-inner">
                  <input
                    @keyup.enter="getWeather"
                    v-model.trim="city"
                    type="text"
                    class="search"
                  />
                </div>

                <WeatherSummary :weatherInfo="weatherInfo" />
              </div>
            </section>
            <section class="section section-right">
              <Highlights />
            </section>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<style scoped lang="scss">
@import "./assets/styles/main.scss";

.page {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px 0;
  background-color: #59585d;
}

.laptop {
  width: 100%;
  padding: 20px;
  background-color: #0e100f;
  border-radius: 25px;
}

.sections {
  display: flex;
  width: 100%;

  @media (max-width: 767px) {
    flex-direction: column;
  }
}

.section-left {
  width: 30%;
  padding-right: 10px;

  @media (max-width: 767px) {
    width: 100%;
    padding-right: 0;
  }
}

.section-right {
  width: 70%;
  padding-left: 10px;

  @media (max-width: 767px) {
    width: 100%;
    margin-top: 16px;
    padding-left: 0;
  }
}

.city-inner {
  position: relative;
  display: inline-block;
  width: 100%;

  &::after {
    content: "";
    position: absolute;
    top: 0;
    right: 10px;
    width: 25px;
    height: 25px;
    background: url("./assets/img/search.svg") no-repeat 50% 50%;
    background-size: contain;
    transform: translateY(50%);
    cursor: pointer;
  }
}

.info {
  height: 100%;
  padding: 16px;
  background: url("./assets/img/gradient-1.jpg") no-repeat 50% 50%;
  background-size: cover;
  border-radius: 25px;
}

.search {
  width: 100%;
  padding: 16px;
  font-family: "Inter", Arial, sans-serif;
  color: #fff;
  background-color: rgba(0, 0, 0, 0.75);
  border-radius: 16px;
  border: none;
  outline: none;
  cursor: pointer;
}

.section-bottom {
  width: 50%;
  margin-top: 16px;

  @media (max-width: 767px) {
    width: 100%;
  }
}
</style>
