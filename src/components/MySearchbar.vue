<template>

  <div class="search-box">
    <!-- Eingegebener Text wird in currentQuery gespeichert, durch bestätigen wird die Methode fetchRecipes aufgerufen -->
    <input type="text" class="search-bar" placeholder="Search for recipes..." v-model="currentQuery"
      @keypress="fetchRecipes" />
  </div>

</template>


<script>

// In der config steht die BASE URL drin
import config from "../config.json"

export default {
  props: ['query'],

  data() {
    return {
      currentQuery: "",
      rezepts: [],
    }
  },

  methods: {
    // Holt Rezepte
    async fetchRecipes(e) {
      if (e.key === "Enter") {
        let result = await fetch(config.BASE_API_URL + `q=${this.currentQuery}`)
        let json = await result.json();
        this.rezepts = json.hits;
        // Reicht die Daten (Sucheingabe und somit indirekt die Rezeptinfos) an die App
        this.$emit("rezepts", this.rezepts);
      }
    },
  },
}

</script>

<style>

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  margin: auto;
  padding: 15px;  
  max-width: 40vw;
  max-height: 10vh;

  appearance: none;
  border: none;
  outline: none;
  background: none;
  color: rgb(3, 54, 3);
  font-size: 20px;
  font-weight: bold;
  background-color: rgba(255, 252, 243, 0.5);
  border-radius: 30px 30px 30px 30px;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);

  transition: 0.4s;
}
.search-box .search-bar:focus {
  background-color: rgba(255, 252, 243, 0.5);
  border-radius: 30px 30px 30px 30px;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
}

::placeholder {
  text-align: center;
  font-family: montserrat;
  font-weight: bold;
  color: rgb(3, 54, 3);
}

</style>