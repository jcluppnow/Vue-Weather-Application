<template>
  <!-- Sets class to warm or nothing depending on weather. -->
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
      <div class="search-box"> 
        <!-- Use a v-model for two way binding on this input to the data element query. -->
        <!-- v-on is used to fetch weather when any key is pressed. -->
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Search..." 
          v-model="query"
          v-on:keypress="fetchWeather"
          />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location"> {{ weather.name }}, {{ weather.sys.country }} </div>
          <div class="date"> {{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class='temperature'>{{ Math.round(weather.main.temp) }}°c</div>
          <div class="weather">{{ weather.weather[0].main }} </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import * as myKey from './config.json'
import Vue from 'vue'

export default {
  name: 'App',
  data () {
    return {
      api_key: myKey.MY_KEY,
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
      fetchWeather(e) {
        //If the event equates to the enter key, fetch the weather.
        if (e.key == "Enter")
        {
          Vue.axios.get(`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`)
          .then(response => {
            console.log(response);
            return response.data;
          }).then(this.setResults);
        }
      },
      setResults(results) {
        this.weather = results;
      },
      dateBuilder() {
        let d = new Date();
        let months = ["January", "February", "March", "April", "May", "June", "July", "August",
        "September", "October", "November", "December"];
        let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();

        return `${day} ${date} ${month} ${year}`;
      }
  }
}
</script>

<style>
  * {
    /*No margin on all sides.*/
    margin: 0;
    /*No padding on all sides.*/
    padding: 0;
    /*Width and height properties include content, padding and border.*/
    box-sizing: border-box;
  }


  body {
    /*Set the family-name to montserrat and the generic-family to sans-serif.*/
    font-family: 'montserrat', sans-serif;
  }

  #app {
    /*Adds a background image with the relevant file as the source.*/
    background-image: url('./assets/cold-bg.jpg');
    /*Resizes the background image to cover the entire container.*/
    background-size: cover;
    /*Positions image at the bottom.*/
    background-position: bottom;
    /*These changes will be applied after 0.4s to add a smooth effect.*/
    transition: 0.4s;
  }

  #app.warm {
    /*Adds a background image with the relevant file as the source.*/
    background-image: url('./assets/warm-bg.jpg');
  }

  main {
    /*Sets the minimum height of main to 100% of the viewport.*/
    min-height: 100vh;
    /*Add a padding of 25 pixels on all sides.*/
    padding: 25px;
    /*Adds a gradient mask effect over the image.*/
    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
  }

  .search-box {
    /*Sets the width to 100% of div.*/
    width: 100%;
    /*Add a margin of 30 pixel on all sides of the search box.*/
    margin-bottom: 30px;
  }

  .search-box .search-bar {
    /*Specifies how this div should be rendered, block displays an elements as a block element, starting on the new line and taking the whole width of said line.*/
    display: block;
    /*Sets the width to 100% of div.*/
    width: 100%;
    /*Add a padding of 14 pixels on all sides.*/
    padding: 14px;
    /*Sets the text color.*/
    color: #313131;
    /* Sets the font-size to the specified pixel size.*/
    font-size: 20px;

    /*Remove any forced styling.*/
    appearance: none;
    /*Remove borders.*/
    border: none;
    /*Remove outlines.*/
    outline: none;
    /*Remove background.*/
    background: none;
    /*Attaches a shadow to this div element - Horizontal offset, vertical offset, blur, color.*/
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    /*Sets the background color for this div.*/
    background-color: rgba(255, 255, 255, 0.15);
    /*Adds rounded corners to top right and bottom left corner.*/
    border-radius: 0px 16px 0px 16px;
    /*These changes will be applied after 0.4s to add a smooth effect.*/
    transition: 0.4s;
  }

  .search-box .search-bar:focus {
    /*Attaches a shadow to this div element - Horizontal offset, vertical offset, blur, color.*/
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    /*Sets the background color for this div.*/
    background-color: rgba(255, 255, 255, 0.75);
    /*Add rounded corners to top left and bottom right corners.*/
    border-radius: 16px 0px 16px 0px;
  }

  .location-box .location {
    /*Sets the text color.*/
    color: #FFFFFF;
    /*Sets the font-size to the specified pixel size.*/
    font-size: 32px;
    /*Sets the fonts weight to a value between 100 and 900 with 900 being the strongest/boldest.*/
    font-weight: 500;
    /*Horizontally alligns text in the center.*/
    text-align: center;
    /*Adds a shadow to text - Position of horizontal shadow, position of vertical shadow and color.*/
    text-shadow: 1px 2px rgba(0, 0, 0, 0.25);
  }

  .location-box .date {
    /*Sets the text color.*/
    color: #FFFFFF;
    /*Sets the font-size to the specified pixel size.*/
    font-size: 20px;
    /*Sets the fonts weight to a value between 100 and 900 with 900 being the strongest/boldest.*/
    font-weight: 300;
    /*Make the font style of the date text be in italics.*/
    font-style: italic;
    /*Horizontally alligns text in the center.*/
    text-align: center;
  }

  .weather-box {
    /*Horizontally alligns text in the center.*/
    text-align: center;
  }

  .weather-box .temperature {
    /*Specifies how this div should be rendered, in-line block formats as an inline element but you can apply height and width values.*/
    display: inline-block;
    /*Add a padding of 10px on top/bottom and a padding of 25 pixels on right/left.*/
    padding: 10px 25px;
    /*Sets the text color.*/    
    color: #FFF;
    /*Sets the font-size to the specified pixel size.*/
    font-size: 102px;
    /*Sets the fonts weight to a value between 100 and 900 with 900 being the strongest/boldest.*/
    font-weight: 900;
    
    /*Adds a shadow to text - Position of horizontal shadow, position of vertical shadow and color.*/
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    /*Sets the background color for this div.*/
    background-color: rgba(255, 255, 255, 0.25);
    /*Round all 4 corners evenly by 16px.*/
    border-radius: 16px;
    /*Add a margin of 30 pixels on the top/bottom and remove the margin on the right/left. */
    margin: 30px 0px;

    /*Attaches a shadow to this div element - Horizontal offset, vertical offset, color.*/
    box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }

  .weather-box .weather {
    /*Sets the text color.*/    
    color: #FFF;
    /*Sets the font-size to the specified pixel size.*/
    font-size: 48px;
    /*Sets the fonts weight to a value between 100 and 900 with 900 being the strongest/boldest.*/
    font-weight: 700;
    /*Make the font style of the weather text be in italics.*/
    font-style: italic;
    /*Adds a shadow to text - Position of horizontal shadow, position of vertical shadow and color.*/
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }
</style>

