<template>
  <div class="p-8 pb-0">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">Search Meals by Name</h1>
  </div>
  <div class="px-8 pb-3">
    <input
      type="text"
      v-model="keyword"
      class="rounded border-2 bg-white border-gray-200 focus:ring-orange-500 focus:border-orange-500 w-full"
      placeholder="Search for Meals"
      @change="searchMeals"
    />
  </div>

  <Meals :meals="meals" />
</template>

<script setup>
import { computed, ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import Meals from '../components/Meals.vue'
import { useMealStore } from "../stores/useMealStore";

const store = useMealStore();
const route = useRoute();
const keyword = ref("");

onMounted(() => {
  keyword.value = route.params.name || "";
  if (keyword.value) {
    searchMeals();
  }
});

const meals = computed(() => store.searchedMeals);

function searchMeals() {
  if (keyword.value) {
    store.searchMeals(keyword.value);
  } else {
    store.searchedMeals = []; // Directly reset the meals list if no keyword
  }
}
</script>
