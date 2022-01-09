<template>
  <div class="container">
    <div class="query">
      <p class="query-title">Bellow you can calculate your daily calories</p>
      <input
        type="number"
        class="query-input"
        placeholder="Calories(e.g. 2000)"
        v-model="enteredValue"
      />
      <div>
        <button class="query-btn" @click="getData">Generate Meal plan</button>
      </div>
    </div>
    <transition name="error">
      <div class="error" v-if="error">
        <h3>Calories can't be empty and must be number!</h3>
      </div>
    </transition>

    <GeneratedMeals
      v-if="fetchedData"
      :meals-data="mealsData"
      :calories="calories"
      :protein="protein"
      :carbs="carbs"
      :fat="fat"
    />
  </div>
</template>

<script>
import GeneratedMeals from "./components/GeneratedMeals.vue";
export default {
  name: "App",
  components: {
    GeneratedMeals,
  },
  data() {
    return {
      enteredValue: null,
      error: false,
      baseApi: "https://api.spoonacular.com/mealplanner/generate?",
      apiKey: "apiKey=bd4c41228c8b472ebc37a402291d010d",
      fetchedData: false,
      calories: "",
      protein: "",
      carbs: "",
      fat: "",
      mealsData: [],
    };
  },
  methods: {
    async getData() {
      if (this.enteredValue === null) {
        this.error = true;
      } else {
        const baseUrl = `${this.baseApi}${this.apiKey}&timeFrame=day&targetCalories=${this.enteredValue}`;
        const response = await fetch(baseUrl);
        const data = await response.json();
        this.error = false;
        this.fetchedData = true;
        this.enteredValue = null;
        this.mealsData = data.meals;
        this.calories = data.nutrients.calories;
        this.protein = data.nutrients.protein;
        this.carbs = data.nutrients.carbohydrates;
        this.fat = data.nutrients.fat;
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  @import url("https://fonts.googleapis.com/css2?family=Lato&display=swap");
  height: 100vh;
  font-family: "Lato", sans-serif;
  background-color: #f9d29d;
  background-image: linear-gradient(315deg, #f9d29d 0%, #ffd8cb 74%);
}
.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 50px 0;
}
.query {
  text-align: center;
  padding: 10px;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  border: 1px solid transparent;
  border-radius: 10px;
  margin-bottom: 20px;
}
.query .query-title {
  font-size: 25px;
  margin-bottom: 10px;
}
.query .query-input {
  font-size: 20px;
  padding: 3px 5px;
  border: none;
  border-radius: 5px;
  outline: none;
  background: salmon;
  margin-bottom: 10px;
}
.query .query-btn {
  font-size: 20px;
  padding: 2px 5px;
  border: none;
  border-radius: 5px;
  margin-bottom: -10px;
  cursor: pointer;
  background: #a9a9a9;
}
.query .query-btn:hover {
  background-color: #909090;
}
.error {
  text-align: center;
  font-size: 20px;
  padding: 10px 0;
  border: 1px solid red;
  background-color: red;
  border-radius: 10px;
}
.error-enter-active,
.error-leave-active {
  transition: opacity 0.5s ease;
}

.error-enter-from,
.error-leave-to {
  opacity: 0;
}
</style>
