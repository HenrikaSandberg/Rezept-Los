<!-- "API_KEY" :"922c1e63ff18a64052640b4aff6d54af",
"API_ID" :"bba371be",
"BASE_API_URL": "https://api.edamam.com/api/recipes/v2" -->

<template>
  
  <div id="app">
    <main>
      <h1 id="websiteTitle">Rezept-los</h1>
      <h4 id="slogan">Meals matching your calorie need</h4>

      <!-- Wenn showDetail false ist, zeige diese Komponenten an -->
      <div v-if="!showDetail">
        <MySearchbar @rezepts="getRezepts" @query="getQuery" :query="query" />
        <MyCalorieCalc :weather="weather" @forecastToShow="getForecast" />
        <MyRecipeCard :rezepts="rezepts" @detail="setDetail" @showDetails="showDetails" />
      </div>
      
      <!-- Wenn showDetail true ist, zeige diese Komponente an -->
      <MyRecipeDetail v-if="showDetail" :detail="detailToShow" @showDetail="showDetails" :query="query"
        @query="getQuery" />
    </main>
  </div>

</template>

<script>

// Import der Komponenten 
import MySearchbar from "./components/MySearchbar.vue";
import MyCalorieCalc from "./components/MyCalorieCalc.vue";
import MyRecipeCard from "./components/MyRecipeCard.vue";
import MyRecipeDetail from "./components/MyRecipeDetail.vue";

export default {
  name: 'app',
  components: {
    MySearchbar,
    MyCalorieCalc,
    MyRecipeCard,
    MyRecipeDetail
  },

  data() {
    return {
      query: '',
      rezepts: [],
      showDetail: false,
      detailToShow: {}
    }
  },

  methods: {
    // Holt sich Data aus den Komponenten
    getQuery(query_) {
      this.query = query_;
    },
    getRezepts(rezepts_) {
      this.rezepts = rezepts_;
    },
    showDetails(showDetails_) {
      this.showDetail = showDetails_;
    },
    setDetail(detail_) {
      console.log("detail:", detail_)
      this.detailToShow = detail_;
    }
  }
}
</script>

<style>
@font-face {
  font-family: 'Lemonada';
  src: url('./assets/fonts/Lemonada-Bold.ttf') format('truetype');
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Lemonada;
  background-image: url("./assets/BackgrounPattern.png");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
  background-color: rgba(88, 153, 13, 0.51);
}
main {
  min-height: 100vh;
  padding: 25px;
}

#websiteTitle {
  text-align: center;
  font-family: Lemonada;
  font-size: 60px;
  color:rgb(3, 54, 3);
}

#slogan { 
  text-align: center;
  font-family: montserrat;
  font-size: 22px;
  color: rgb(3, 54, 3);

  margin-top: -20px;
  margin-bottom: 3%;
 
}


</style>