<template>
  <div id="app">
    <!-- Navbar or Header (you can customize this part as needed) -->
    <nav class="bg-gray-800 text-white p-4">
      <div class="container mx-auto">
        <router-link to="/" class="text-xl font-bold">My Store</router-link>
      </div>
    </nav>

    <!-- Main Content Area: Dynamically loaded via router-view -->
    <router-view></router-view>

    <!-- Footer (you can customize this part as needed) -->
    <footer class="bg-gray-800 text-white p-4 mt-6">
      <div class="container mx-auto text-center">
        <p>&copy; 2024 My Store. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>