<template>
  <header class="bg-white shadow-md h-16 flex justify-between items-stretch">
      <router-link :to="{name: 'home'}" class="inline-flex items-center h-full px-5">
        Home
      </router-link>
      <div class="flex items-center gap-1">
        <router-link :to="{name: 'byName'}" class="inline-flex items-center transition-color px-2 h-full hover:bg-orange-200">Search By Name</router-link>
        <router-link :to="{name: 'byLetter'}" class="inline-flex items-center transition-color px-2 h-full hover:bg-orange-200">Search By Letter</router-link>
        <router-link :to="{name: 'ingredients'}" class="inline-flex items-center transition-color px-2 h-full hover:bg-orange-200">Search By Ingredients</router-link>
      </div>
    </header>
</template>

<script></script>