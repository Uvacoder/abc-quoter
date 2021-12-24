<script setup lang="ts">
import { onMounted } from 'vue'
import useTheme from '../composables/useTheme'
import { isFavoriteShow, toggleFavoriteShow } from '../composables/useFavorite'

const { theme, titleTheme, isThemeMounted, toggleTheme, updateTheme } = useTheme()

onMounted(() => {
  updateTheme()
  isThemeMounted.value = true
})
</script>

<template>
  <div class="relative pt-12 pb-4 md:py-12 flex flex-col items-center">
    <div class="absolute right-4 top-4 md:right-8 md:top-8 space-x-3">
      <button
        aria-label="Show Favorite Quotes"
        class="button-toggle-fav p-2 border rounded-full"
        :class="`${isFavoriteShow ? 'text-red-500' : 'text-gray-900 dark:text-gray-100'}`"
        @click="toggleFavoriteShow"
      >
        <i-ri-heart-2-fill v-if="isFavoriteShow" />
        <i-ri-heart-2-line v-else />
      </button>
      <button
        aria-label="Toggle Theme"
        class="button-toggle-theme p-2 border rounded-full text-gray-900 dark:text-gray-100"
        :title="titleTheme"
        @click="toggleTheme"
      >
        <span :class="{ 'invisible': !isThemeMounted }">
          <i-mdi-circle-half-full v-if="theme === 'system'" />
          <i-ri-sun-line v-else-if="theme === 'light'" />
          <i-ri-moon-clear-line v-else />
        </span>
      </button>
    </div>

    <h1 class="mt-4 md:mt-0 text-6xl font-bold mb-4 text-transparent bg-clip-text bg-gradient-to-br from-pink-400 to-purple-600">
      #Quote's
    </h1>
    <p class="w-11/12 md:w-1/2 mb-4 text-sm md:text-xl text-center text-gray-500 dark:text-gray-50">
      Quotes **************************.
    </p>

    
  </div>
</template>

<style>
.button-toggle-theme, .button-toggle-fav {
  -webkit-tap-highlight-color: transparent;
}
</style>
