<template>
  <div class="p-8 pb-0 text-orange-500">
    <h1 class="text-4xl font-bold mb-4">Random Meals</h1>
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useMealStore } from "../stores/useMealStore"; // Import the Pinia store
import Meals from "../components/Meals.vue";
import axiosClient from "../axiosClient.js";

const mealStore = useMealStore(); // Use the Pinia store
const meals = ref([]); // Local ref to hold meals

onMounted(async () => {
  for (let i = 0; i < 10; i++) {
    const response = await axiosClient.get(`random.php`);
    meals.value.push(response.data.meals[0]); // Push each meal to the local meals ref
  }
});
</script>
