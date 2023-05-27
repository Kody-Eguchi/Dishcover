<template>
  <Meals :meals="meals" class="mt-3"/>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import Meals from '../components/Meals.vue'

import axiosClient from '../axiosClient.js'

const meals = ref([]);

onMounted(async ()=>{
  for (let i = 0; i < 10; i++) {
    axiosClient
      .get(`random.php`)
      .then(({ data }) => meals.value.push(data.meals[0]));
  }
})

</script>

<style>
</style>