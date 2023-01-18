<template>

  <div class="container">
    <!-- Geht Ausgabe der API durch und erzeugt für jeden "hit" eine Card -->
    <!-- Durch Klick auf die Karte kommt man zur Detailseite (die Methode setDetails wird aufgerufen und Infos der API übergeben, mit dessen das Rezept identifiziert werden kann -->
    <div class="recipes-card" v-for="rezept in this.rezepts" :key="rezept.recipe.uri"
    v-on:click="setDetail(rezept._links.self.href)">
      <div v-html="this.getImage(rezept.recipe.image)" />
      <p class="recipesname">{{ rezept.recipe.label }}
      </p>
      <p id="calories"> Calories:
        {{ Math.round(rezept.recipe.calories) }} kcal
      </p>
      <button class="toRecipes" v-on:click="setDetail(rezept._links.self.href)">To Recipe</button>
    </div>
  </div>

</template>

<script>

export default {
  props: ['rezepts'],
  data() {
    return {
    }
  },
  methods: {
    // Bekommt die Infos für das Rezeptbild
    getImage(imgsrc) {
      return `<img class="rezeptbild" src=${imgsrc} alt="thumbnail">`
    },

    async setDetail(url) {
      let result = await fetch(url);
      result = await result.json();
      console.log("result: ", result);

      // Reicht das Ergebnis an die App hoch und setzt showDetails auf true
      this.$emit("detail", result.recipe);
      this.$emit("showDetails", true);
    }
  }
}

</script>

<style>

.container {
  cursor: pointer;

  display: grid;
  grid-template-columns: auto auto auto auto;
  gap: 10px 5px;
  margin-top: 5%;
  margin-right: 150px;
  margin-left: 150px;
}

.recipes-card {
  margin: 0.5rem;
  padding: 0%;
  max-width: 20vw;
  min-height: 35vh;

  color: rgb(3, 54, 3);
  background-color: rgba(255, 252, 243, 0.5);
  border-radius: 16px;
  
  transition: 0.3s;
}
.recipes-card:hover{
  box-shadow: 6px 6px rgba(57, 57, 57, 0.25);
  transform: translateY(-0.25em);
}

.rezeptbild {
  overflow: hidden;
  object-fit: cover;
  width: 100%;
  height: 250px;

  border-radius: 16px 16px 0px 0px;
}

.recipesname {
  margin-top: 3%;

  font-size: 20px;
  text-align: center;
}

#calories {
  margin-top: 3%;

  text-align: center;
  font-family: montserrat;
  font-size: 18px;
  font-weight: bold;
}

/* Button */
.toRecipes {
  cursor: pointer;

  margin: 10% 20% 5% 30%;
  padding: 5px;
  width: 40%;

  color: rgb(255, 255, 255);
  font-weight: bold;
  background-color: orange;
  
  border-style: solid;
  border-radius: 16px;
  border-color: rgb(255, 255, 255);
  box-shadow: 1px 3px rgba(52, 52, 52, 0.25);

  transition-duration: 0.4s;
}
.toRecipes:hover{
  background-color: rgb(255, 255, 255);
  color: orange;
  border-color: orange;
  box-shadow: 2px 5px rgba(52, 52, 52, 0.25);
}








</style>