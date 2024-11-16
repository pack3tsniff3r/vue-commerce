<template>
  <div class="container mx-auto p-4">
    <!-- Responsive Grid -->
    <div class="grid grid-cols-1  gap-6">
      <div class="border-4 border-slate padding-5">
        <!-- Product ID -->
        <div class="text-xs text-gray-500 mb-1 text-center">
          Product ID: {{ product.id }}
        </div>

        <!-- Product Title -->
        <div class="text-base font-bold text-gray-800 mb-1 text-center">
          {{ product.title }}
        </div>

        <!-- Product Measurements -->
        <div class="text-xs text-gray-600 mb-2 text-center">
        <div class="border-t border-black">
          Dimensions (LWH): {{ product.measurements }}
        </div>
        </div>

        <!-- Main Product Image -->
        <div class="mb-3 relative">
          <img
            :src="product.mainImage"
            alt="Main Image"
            class="w-full h-42 object-cover rounded-md"
          />
          <!-- Thumbnail Overlay -->
          <div
            v-if="selectedThumbnail"
            class="absolute inset-0 bg-black bg-opacity-75 flex items-center justify-center"
          >
            <img
              :src="selectedThumbnail"
              alt="Enlarged Thumbnail"
              class="w-3/4 h-3/4 object-cover rounded-md"
            />
            <button
              @click="selectedThumbnail = null"
              class="absolute top-2 right-2 bg-gray-700 text-white rounded-full p-1"
            >
              ✕
            </button>
          </div>
        </div>

        <!-- Thumbnails Section -->
        <div class="flex justify-center space-x-2 mb-3">
          <img
            v-for="(thumbnail, index) in product.thumbnails"
            :key="index"
            :src="thumbnail"
            alt="Thumbnail"
            class="w-8 h-8 object-cover rounded-md cursor-pointer hover:opacity-75"
            @click="selectedThumbnail = thumbnail"
          />
        </div>

 <!-- Product Measurements -->
        <div class="text-xs text-gray-600 mb-2 text-center">
        <div class="border-t border-black">
          Dimensions (LWH): {{ product.measurements }}
        </div>
        </div>

        <!-- Product Description -->
        <div class="text-xs text-gray-600 mb-3">
          <p class="px-50">
            {{ product.description.slice(0, 80) }}<span
              v-if="product.description.length > 80"
              >...</span
            >
          </p>
          <div
            class="bg-purple-500 text-white px-4 py-2 rounded-full text-center block mt-2 hover:bg-purple-600"
          >
            <button @click="$emit('showDetails', product.id)">More Info</button>
          </div>
        </div>

        <!-- Price Section -->
        <div class="font-semibold text-sm text-gray-800 mt-auto text-center">
          ${{ parseFloat(product.price).toFixed(2) }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
defineProps({
  product: Object,
});

// Holds the currently selected thumbnail image URL
const selectedThumbnail = ref(null);
</script>
