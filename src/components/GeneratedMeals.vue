<template>
  <div class="meals-wrapper">
    <p class="macros-title">Daily Macros</p>
    <div class="macros-categories">
      <span
        >Calories: <strong> {{ Math.round(calories) }} </strong></span
      >
      <span
        >Protein: <strong>{{ Math.round(protein) }}</strong></span
      >
      <span
        >Carbohydrates: <strong>{{ Math.round(carbs) }}</strong></span
      >
      <span
        >Fat: <strong>{{ Math.round(fat) }}</strong></span
      >
    </div>
    <div>
      <ul class="flex">
        <li class="meal-item" v-for="meal in mealsData" :key="meal.id">
          <h3 class="meal-title">{{ meal.title }}</h3>
          <p class="meal-servings">Servings: <strong>{{ meal.servings }}</strong></p>
          <p class="meal-prep-time">
            Preparation time: <strong>{{ meal.readyInMinutes }}</strong> minutes 
          </p>
          <a :href="meal.sourceUrl">Go to recepie</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ["mealsData", "calories", "protein", "carbs", "fat"],
};
</script>

<style scoped>
.meals-wrapper {
  padding: 20px 0;
}
.meals-wrapper .macros-title {
  font-size: 30px;
  text-align: center;
  margin-bottom: 20px;
}
.macros-categories {
  padding: 15px 0;
  text-align: center;
  margin-bottom: 10px;
}
.macros-categories span {
  font-size: 20px;
  padding: 0px 3px;
}
.flex {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.meal-item {
  list-style: none;
  padding: 50px 10px;
  margin-left: 10px;
  box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px,
    rgba(60, 64, 67, 0.15) 0px 2px 6px 2px;
  background: #fff;
  border-radius: 5px;
}
.meal-item:first-of-type {
  margin-left: 0px;
}
.meal-item .meal-title {
  font-size: 20px;
  margin-bottom: 10px;
}
.meal-item .meal-servings {
  font-size: 17px;
  margin-bottom: 5px;
}
.meal-item .meal-prep-time {
  font-size: 17px;
  margin-bottom: 15px;
}
.meal-item a {
  text-decoration: none;
  border: 1px solid #ccc;
  padding: 3px 5px;
  color: #000;
  background-color: #ccc;
}
</style>