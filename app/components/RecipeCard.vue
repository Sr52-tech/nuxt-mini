<template>
  <div class="bg-white rounded-lg shadow-lg overflow-hidden">
    <img :src="recipe.image" :alt="recipe.name" class="w-full h-48 object-cover">
    <div class="p-4">
      <h3 class="text-xl font-semibold mb-2">{{ recipe.name }}</h3>
      
      <!-- Recipe metadata -->
      <div class="flex items-center gap-4 text-sm text-gray-600 mb-3">
        <span class="flex items-center">
          <span class="mr-1">⏱️</span>
          {{ recipe.prepTimeMinutes + recipe.cookTimeMinutes }} mins
        </span>
        <span class="flex items-center">
          <span class="mr-1">👥</span>
          {{ recipe.servings }} servings
        </span>
      </div>

      <!-- Difficulty and cuisine -->
      <div class="flex gap-2 mb-4">
        <span class="px-2 py-1 bg-gray-100 rounded-full text-sm">{{ recipe.difficulty }}</span>
        <span class="px-2 py-1 bg-gray-100 rounded-full text-sm">{{ recipe.cuisine }}</span>
      </div>

      <!-- Rating -->
      <div class="flex items-center gap-2">
        <div class="flex">
          <span v-for="i in 5" :key="i" class="text-yellow-400">
            {{ i <= recipe.rating ? '★' : '☆' }}
          </span>
        </div>
        <span class="text-sm text-gray-600">({{ recipe.reviewCount }} reviews)</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { type Recipe } from '../../types/types'

defineProps<{
  recipe: Recipe
}>();
</script> 