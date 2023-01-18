<template>

  <div class="caloriesCalculator">
    <h2 class="title">Calorie Calculator</h2>
    <div>
      <form>
        <fieldset>
          <div>
            <div><label for="bodyWeight">Body weight</label></div>
            <div> <input id="bodyWeight" type="number" v-model="bodyWeightKg" step="any" min=0>
               <span>kg</span>
            </div>
          </div>
          <div>
            <div><label for="bodySize">Body size</label></div>
            <div><input id="bodySize" type="number" v-model="bodySize" step="any">
              <span>cm</span>
            </div>
          </div>
          <div>
            <div><label for="age">Age</label></div>
            <div><input id="age" type="number" v-model="age" step="1" min=0.0></div>
          </div>
          <div></div>
          <div class="genderButton">
            <div> <p>Female</p> </div>
            <div>
              <label class="switch" for="toggle_button">
                <input type="checkbox" id="toggle_button" v-model="checkedValue">
                <span v-if="isActive" class="slider round"></span>
                <span v-if="!isActive" class="slider round"></span>
                <span class="toggle__switch"></span>
              </label>
            </div>
            <div> <p>Male</p> </div>
          </div>

        </fieldset>
      </form>
    </div>
    <div class="result">
      <!-- Anzeige nur, wenn alle Felder ausgefüllt sind -->
      <div v-if="bodyWeightKg!=0&&bodySize!=0&&age!=0">
        <!-- Berechnung für Männer -->
        <h3 v-if="isActive">Your calorie needs: {{ Math.round(parseFloat( 655.1 + (9.6 * bodyWeightKg) + (1.8 * bodySize) - (4.7 *
        age)))}} kcal</h3>
        <!-- Berechnung für Frauen -->
        <h3 v-else>Your calorie needs: {{ Math.round(parseFloat( 66.5 + (13.7 * bodyWeightKg) + (5.0 * bodySize) - (6.8 * age))) }}
        kcal</h3>
      </div>
      <!-- Ausgabe, wenn nicht alle Werte ausgefüllt sind -->
      <div v-else>
        <h3>Your calorie needs: ____ kcal</h3>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  props: [],

  data() {
    return {
      bodyWeightKg: 0,
      bodySize: 0,
      age: 0,
      currentState: false
    }
  },

  // Funktionen für den ToggleButton:
  computed: {
    isActive() {
      return this.currentState;
    },

    checkedValue: {
      get() {
        return this.defaultState
      },
      set(newValue) {
        this.currentState = newValue;
      }
    }
  },

  methods: {
  }
}
</script>

<style>

.caloriesCalculator {
  display: grid;
  justify-content: center;
  width: 50%;
  margin-left: 25%;

  color: rgb(3, 54, 3);
  background-color: rgba(255, 252, 243, 0.5);
  border-radius: 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.title {
  font-family: Lemonada;
  font-size: 30px;
  text-align: center;
  margin-bottom: 3%;
  margin-top: 2%;
}

form {
  text-align: left;
}

fieldset {
  display: grid;
  grid-template-columns: auto auto auto;
  grid-template-rows: auto auto auto;
  column-gap: 20px;

  font-family: montserrat;
  font-weight: bold;
  font-size: 20px;
  border-style: none;
}

input {
  width: 70%;
  margin-right: 3%;

  background-color: rgba(255, 255, 255, 0.765);
  border-style: none;
}

.result {
  margin-top: 2em;
  margin-left: 4em;
  margin-bottom: 2rem;

  font-family: Lemonada; 
  font-size: 18px;
}

/* Switch Gender Button */
.genderButton {
  display: grid;
  grid-template-columns: 25% 50% 25%;
  text-align: center;
  margin-top: 15%;
}
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
  margin-left: 1em;
}
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}
.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}
input:checked+.slider {
  background-color: #f3bb21;
}
input:focus+.slider {
  box-shadow: 0 0 1px #f3bb21;
}
input:checked+.slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}
.slider.round {
  background-color: #f3bb21;
  border-radius: 34px;
}
.slider.round:before {
  border-radius: 50%;
}

</style>