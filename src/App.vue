<script setup>
import { ref, onMounted } from 'vue' //вызов реактивности (ref) и вызов скрипта который сработает при загрузке страницы
import { API_KEY, BASE_URL } from './constants'
import WeatherSummary from './components/WeatherSummary.vue'


const city = ref('Novosibirsk')
const weatherInfo = ref(null)

function getWeather() {
  fetch(`${BASE_URL}?q=${city.value}&units=metric&appid=${API_KEY}`) //тут идёт вызов к серверу через API. "&units=metric" - вызов к градусам по цельсию, по умолчанию - кельвин
    .then((response) => response.json())
    .then((data) => weatherInfo.value = data)
}

onMounted(getWeather)
</script>

<template>
  <div class="page">
    <main>
      <section>
        <div class="info">
          <div>
            <input @keyup.enter="getWeather" v-model="city" type="text" class="search">
          </div>
          <WeatherSummary :weatherInfo="weatherInfo" />
        </div>
      </section>
      <div>
        <span>Введите название города или страны на английском</span>
      </div>
    </main>
  </div>
</template>

<style lang="sass" scoped>
@import './assets/styles/main'
.page
  position: relative
  display: flex
  justify-content: center
  align-items: left
  min-height: 100vh
  padding: 20px 
  background-color: #000000

.info
  height: 100%
  padding: 16px
  background: #a88116 
  


.search
  width: 100%
  padding: 16px
  font-family: 'Inter', Arial, sans-serif
  color: $white
  background-color: rgba(0, 0, 0, 0.75)
  border-radius: 16px
  border: none
  outline: none
  cursor: pointer


span
  padding-top: 15px
  font-size: 20px
</style>
