<template>
  <div class="max-w-[800px] mx-auto p-8">
    <h1 class="text-5xl font-bold mb-5">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" alt="meal.strMeal" class="max-w-[100%]">
    <div class="grid grid-cols-1 sm:grid-cols-3 text-lg py-2">
      <div> <strong class="font-bold">Category: </strong>  {{ meal.strCartegory }}</div>
      <div> <strong class="font-bold">Area: </strong>  {{ meal.strArea }}</div>
      <div> <strong class="font-bold">Tags: </strong>  {{ meal.strTags }}</div>
    </div>
    <!-- INSTRUCTION -->
    <div class="my-3">
      <ol>
        <li v-for="(instruction, index) of instructions">
          <span v-if="instruction">{{ index + 1 }}. {{ instruction }}</span>
        </li>
      </ol>
    </div>


    <div class="grid grid-cols-1 sm:grid-cols-2">
      <!-- INGREDIENTS -->
      <div>
        <h2 class="text-2xl font-semibold mb-2 ">Ingredients</h2>
        <ul>
          <template v-for="(element, index) of new Array(20)">
            <li v-if="meal[`strIngredient${index + 1}`]">
              {{ index + 1 }}. {{ meal[`strIngredient${index + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <!-- MEASURES -->
      <div>
        <h2 class="text-2xl font-semibold mb-3 ">Measures</h2>
        <ul>
          <template v-for="(element, index) of new Array(20)">
            <li v-if="meal[`strMeasure${index + 1}`]">
              {{ meal[`strMeasure${index + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <!-- BUTTONS -->
      <div class="mt-4 ">
        <YouTubeButton :href="meal.strYoutube">Go to YouTube</YouTubeButton>
        <a 
          :href="meal.strSource" 
          target="_blank" 
          class="ml-3 px-3 py-2 rounded border-2 border-orange-600 bg-orange-500 hover:bg-orange-700 text-white transition-colors"
          >
            Source
          </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import axiosClient from '../axiosClient'
import YouTubeButton from '../components/YouTubeButton.vue';

const route = useRoute()
// ref({}) is useState() of React.js
const meal = ref({})
const instructions = ref({})

onMounted(()=>{
  axiosClient.get(`lookup.php?i=${route.params.id}`)
    .then(({data})=>{
      meal.value = data.meals[0] || {}
      instructions.value = data.meals[0].strInstructions.split(".")
    })
})




</script>