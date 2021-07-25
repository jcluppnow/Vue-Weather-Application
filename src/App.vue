<template>
  <div id="app">
    <main>
      <div class="search-box"> 
        <!-- Use a v-model for two way binding on this input to the data element query. -->
        <input type="text" class="search-bar" placeholder="Search..." v-model="query"/>
        {{ query }}
      </div>

      <div class="weather-wrap">
        <div class="location-box">
          <div class="location">Perth, WA</div>
          <div class="date">Sunday 27 July 2021</div>
        </div>

        <div class="weather-box">
          <div class='temperature'>15°c</div>
          <div class="weather">Sunny</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import * as myKey from './config.js'

export default {
  name: 'App',
  data () {
    return {
      api_key: myKey.MY_KEY,
      url_base: 'https://api.tomorrow.io/v4/',
      query: '',
      weather: {}
    }
  },
  methods: {

  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }


  body {
    font-family: 'montserrat', sans-serif;
  }

  #app {
    background-image: url('./assets/cold-bg.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }

  main {
    min-height: 100vh;
    padding: 25px;

    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
  }

  .search-box {
    width: 100%;
    margin-bottom: 30px;
  }

  .search-box .search-bar {
    display: block;
    width: 100%;
    padding: 14px;

    color: #313131;
    font-size: 20px;

    appearance: none;
    border: none;
    outline: none;
    background: none;

    box-shadow: 0px 0xpx 16px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.15);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
  }

  .search-box .search-bar:focus {
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.75);
    border-radius: 16px 0px 16px 0px;
  }

  .location-box .location {
    color: #FFFFFF;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 2px rgba(0, 0, 0, 0.25);
  }

  .location-box .date {
    color: #FFFFFF;
    font-size: 20px;
    font-weight: 300;
    font-style: italic;
    text-align: center;
  }

  .weather-box {
    text-align: center;
  }

  .weather-box .temperature {
    display: inline-block;
    padding: 10px 25px;
    color: #FFF;
    font-size: 102px;
    font-weight: 900;
    
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.25);
    border-radius: 16px;
    margin: 30px 0px;

    box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }

  .weather-box .weather {
    color: #FFF;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }
</style>

