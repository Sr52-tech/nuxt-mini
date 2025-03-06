<script setup lang="ts">
import { type RecipeResponse } from "../../types/types";
// to set a layout other than the default
    // definePageMeta({
    // layout: 'login',
    // });

//    const { data, error} = await useAsyncData('recipes', () => 
//     $fetch('https://dummyjson.com/recipes?limit=12')
//    );

const { data, pending, error } = await useAsyncData<RecipeResponse>('recipes',
  () => $fetch('https://dummyjson.com/recipes', {
    params: {
      limit: 12
    }
  })
);

const recipes = computed(() => data.value?.recipes || []);

// Debug log to see what we're getting
console.log('Processed data:', recipes.value);
</script>

<template>
    <main>
      <section class="bg-[#f1f1f1]">
        <div class="container flex flex-col lg:flex-row items-center py-20 gap-10">
          <div class="flex-1 order-2 lg:order-1 text-center lg:text-left">
            <h1 class="text-4xl lg:text-6xl font-extrabold mb-6 text-balance">
              Master the Kitchen with Ease: Unleash Your Inner Chef Today!
            </h1>
            <p class="text-xl lg:text-2xl mb-8 text-balance">
              Discover recipes helping you to find the easiest way to cook.
            </p>
            <UButton to="#recipes" label="Browse Recipes" />
          </div>
          <div class="flex-1 order-1 lg:order-2">
            <NuxtImg
              sizes="xs:100vw sm:667px"
              src="/nuxt-course-hero.png"
              format="webp"
              densities="x1"
              alt="Chef cooking in kitchen"
            />
          </div>
        </div>
      </section>
      <section id="recipes" class="py-20 container mx-auto px-4">
        <h2 class="text-3xl lg:text-5xl mb-2">Our Recipes</h2>
        <p class="text-lg lg:text-xl mb-8">Check out our most popular recipes!</p>
        
        <!-- Loading state -->
        <div v-if="pending" class="text-center py-10">
          <p class="text-xl">Loading recipes...</p>
        </div>
        
        <!-- Error state -->
        <div v-else-if="error" class="text-center py-10">
          <p class="text-xl text-red-600">Failed to load recipes</p>
          <p class="text-sm text-gray-600 mt-2">{{ error }}</p>
        </div>
        
        <!-- Success state -->
        <div v-else-if="recipes.length" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div v-for="recipe in recipes" :key="recipe.id" class="bg-white rounded-lg shadow-lg overflow-hidden hover:shadow-xl transition-shadow">
            <NuxtLink :to="`/recipes/${recipe.id}`" class="block">
              <img :src="recipe.image" :alt="recipe.name" class="w-full h-48 object-cover">
              <div class="p-4">
                <h3 class="text-xl font-semibold mb-2">{{ recipe.name }}</h3>
                <div class="flex items-center gap-4 text-sm text-gray-600">
                  <span>{{ recipe.cuisine }}</span>
                  <span>{{ recipe.difficulty }}</span>
                </div>
              </div>
            </NuxtLink>
          </div>
        </div>
        
        <!-- No data state -->
        <div v-else class="text-center py-10">
          <p class="text-xl">No recipes found</p>
        </div>
      </section>
      <section class="bg-[#f1f1f1] py-20">
        <!-- <SignupForm /> -->
      </section>
    </main>
</template>