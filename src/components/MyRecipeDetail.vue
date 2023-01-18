<template>

  <!-- Back Button, durch setShowDetails wird showDetails auf false gesetzt und die anderen Komponenten angzeigt -->
  <button class="backButton" v-on:click="setShowDetail"><img id="back" src="../assets/backButton.png"
      alt="backButton"></button>

  <div class="recipe">
    <div id="recipeImage" v-html="this.getImage(this.detail.image)" />

    <div class="gap">
      <h2 id="title">{{ this.detail.label }}</h2>
      <p class="servings">Servings: {{ this.detail.yield }}</p>
      <!-- Button öffnet neues Fenster, in dem das Rezept steht -->
      <a id="relocateButton"  target="__blank" :href="this.detail.url">Cook now</a>
    </div>

    <div class="divIngredients">
      <h3 class="headline">Ingredients</h3>
      <!-- Geht alle Zutaten durch die die API als Array übergibt und zeigt sie an. -->
      <div v-for="ingredient in this.detail.ingredientLines" :key="ingredient">
        <input class="checkbox" type="checkbox">
        <label class="ingredientsText">{{ ingredient }}</label>
      </div>
    </div>

    <div class="gap">
      <h3 class="headline">Nutritions</h3>
      <p class="caloriesMeal"> Calories of the meal: {{ Math.round(this.detail.calories) }} kcal</p>

      <!-- Zeigt Nährwerte nur an, wenn show false ist. -->
      <button @click="show = !show" class="nutritionsShow">Show Nutritions</button>
      <div class="nutritionBox">
        <!-- Wenn show true ist, wird nichts unter dem Button angezeigt -->
        <div v-if="show">
        </div>
        <!-- Alle Nährwerte in dem Array totalNutritions der API werden durchlaufen und ausgegeben. -->
        <div v-else v-for="totalNutrients in this.detail.totalNutrients" :key="totalNutrients">
          <ul class="data">{{ totalNutrients.label }} : {{ Math.round(totalNutrients.quantity) }} {{totalNutrients.unit}}</ul>
        </div>
      </div>
    
    </div>

  </div>

</template>

<script>

export default {
  props: ['detail', 'query'],

  // Funktion um Nutritions anzuzeigen
  data: function () {
    return {
      show: true
    }
  },

  methods: {
    getImage(imgsrc) {
      return `<img id="image" src=${imgsrc} alt="Picture of delicious food.">`
    },

    // Daten werden an die App hochgereicht (showDetails wird auf false gesetzt, damit Komponente wieder ausgeblendet wird, wenn Klick auf Button)
    setShowDetail() {
      this.$emit("query", this.query);
      this.$emit("showDetail", false);
    }
  }
}

</script>

<!-- Styling wird nur in dieser Komponente verwendet -->
<style scoped>

@font-face {
  font-family: 'Lemonada';
  src: url('../assets/fonts/Lemonada-Bold.ttf') format('truetype');
}

h1,
h2 {
  text-align: center;
  font-family: Lemonada;
  color: rgb(3, 54, 3);
}
.backButton {
  cursor: pointer;

  margin-left:8.5%;
  margin-bottom:2%;
  
  font-size: 16px;
  color: rgb(3, 54, 3);
  border: none;
  background: none;
}
#back {
  width: 3vw;
}
.recipe {
  display: grid;
  grid-template-columns: 50% 50%;
  grid-template-rows: auto auto;
}

#recipeImage{
  margin-left:18%;
  margin-right: auto;
  width: 47%;
  height: auto;
}
.gap {
  margin-left: 10%;
}

#title {
  text-align: left;
  font-size: 36px;
}
.servings{
  margin-bottom: 2%;

  font-family: montserrat;
  font-size: 18px;
  font-weight: bold;
  color:rgb(3, 54, 3);
}

#relocateButton{
  margin-top: 2%;
  padding: 5px;
  width: 30%;
  
  font-family: montserrat;
  font-size: 16px;
  font-weight: bold;
  color: white;
  background-color: orange;
  border-radius: 16px;
  border-style: solid;
  border-color: rgb(255, 255, 255);
  box-shadow: 1px 3px rgba(52, 52, 52, 0.25);
  text-decoration: none;

  transition: 0.3s;
}
#relocateButton:hover{
  background-color: rgb(255, 255, 255);
  color: orange;
  border-color: orange;
  box-shadow: 2px 5px rgba(52, 52, 52, 0.25);
}
.divIngredients {
  margin-left: 18%;
}
.headline {
  margin-top: 2%;
  margin-bottom: 2%;

  font-family: Lemonada;
  font-size: 26px;
  color: rgb(3, 54, 3);
}
.checkbox {
  cursor: pointer;
  width: 5%;
}
.ingredientsText {
  font-family: montserrat;
  font-size: 18px;
  font-weight: bold;
  color: rgb(3, 54, 3);
}
.caloriesMeal {
  margin-bottom: 2%;

  font-family: montserrat;
  font-size: 18px;
  font-weight: bold;
  color: rgb(3, 54, 3);
}
.nutritionsShow {
  cursor: pointer;

  padding: 5px;
  width: 30%;

  font-weight: bold;
  font-size: 16px;
  color: white;
  background-color: orange;
  border-style: solid;
  border-radius: 20px;
  border-color: rgb(255, 255, 255);
  box-shadow: 1px 3px rgba(52, 52, 52, 0.25);

  transition: 0.3s;
}
.nutritionsShow:focus {
  border-radius: 20px 20px 0px 0px;
}
.nutritionsShow:hover{
  color: orange;
  background-color: rgb(255, 255, 255);
  border-color: orange;
  box-shadow: 2px 5px rgba(52, 52, 52, 0.25);
}

.nutritionBox {
  margin-top: -5px;

  width: 50%;
  color: rgb(3, 54, 3);
  background-color: rgba(255, 252, 243, 0.5);
  border-radius: 0px 16px 16px 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.data {
  margin-top: 3%;
  margin-left: 5%;

  text-align: left;
  font-family: montserrat;
  font-weight: bold;
}

</style>