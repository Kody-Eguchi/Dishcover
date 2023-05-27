<template>
  <div class="p-8 pb-0">
    <input 
      type="text" 
      v-model="keyword"
      class="rounded border-2 border-gray-200 w-full mb-3" 
      placeholder="Search for Meals"
      @change="searchMeals"
    >
  </div>

  
  <Meals :meals="meals"/>
  
</template>

<script setup>
import { onMounted, ref } from 'vue';
import store from '../store';
import { computed } from '@vue/reactivity';
import { useRoute } from 'vue-router';
import Meals from '../components/Meals.vue'

const route = useRoute();
const keyword = ref('')
const meals = computed(()=>
  store.state.searchedMeals
)

function searchMeals(){
  if (keyword.value) {
    store.dispatch("searchMeals", keyword.value);
  } else {
    store.commit("setSearchedMeals", []);
  }
}

onMounted(()=>{
  keyword.value = route.params.name
  if ( keyword.value) {
    searchMeals()
  }
})

</script>

<style>
</style>