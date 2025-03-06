<template>
  <div class="container">
    <div class="max-w-md mx-auto bg-white rounded-lg shadow-lg p-8">
      <h2 class="text-2xl font-bold mb-6 text-center">Sign Up for Recipe Updates</h2>
      <form @submit.prevent="handleSubmit" class="space-y-4">
        <div>
          <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
          <input
            v-model="email"
            type="email"
            id="email"
            required
            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-apple-green focus:ring focus:ring-apple-green focus:ring-opacity-50"
            placeholder="your@email.com"
          >
        </div>
        <button
          type="submit"
          class="w-full bg-apple-green text-white py-2 px-4 rounded-md hover:bg-opacity-90 transition-colors"
        >
          Subscribe
        </button>
      </form>
      <p v-if="message" class="mt-4 text-center" :class="{'text-green-600': !error, 'text-red-600': error}">
        {{ message }}
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const email = ref('')
const message = ref('')
const error = ref(false)

const handleSubmit = async () => {
  try {
    message.value = 'Thanks for subscribing!'
    error.value = false
    email.value = ''
  } catch (e) {
    message.value = 'Something went wrong. Please try again.'
    error.value = true
  }
}
</script> 