<template>
  <div class="flex gap-2 mt-2 justify-center">
    <router-link :to="{name: 'byLetter', params: {letter}}" v-for="letter of letters" :key="letter">
      {{ letter }}
    </router-link>
  </div>

  
  <Meals :meals="meals"/>
  

</template>

<script setup>
import { computed } from '@vue/reactivity';
import store from '../store';
import { onMounted, watch } from 'vue';
import { useRoute } from 'vue-router';
import Meals from '../components/Meals.vue'



const route = useRoute();
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('')
const meals = computed(()=> store.state.mealsByLetter)

// UPDATE MEALS AS ROUTE CHANGES
watch(route, ()=>{
  store.dispatch('searchMealsByLetter', route.params.letter)
})

onMounted(()=>{
  store.dispatch('searchMealsByLetter', route.params.letter)
})


</script>

<style>
</style>