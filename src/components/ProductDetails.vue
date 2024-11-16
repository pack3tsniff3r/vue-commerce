<template>
  <div v-if="product" class="border border-gray-300 rounded-lg p-3 hover:shadow-lg flex flex-col max-w-full sm:max-w-xs mx-auto bg-white">
   
    <!-- Product ID -->
    <div class="text-sm text-gray-500 mb-1 text-center">
      Product ID: {{ product.id }}
    </div>

    <!-- Product Title -->
    <div class="text-lg font-bold text-gray-800 mb-2 text-center">
      {{ product.title }}
    </div>

      <!-- Product Measurements -->
    <div class="text-lg font-bold text-gray-800 mb-2 text-center">
      {{ product.measurements }}
    </div>

    <!-- Product Description -->
    <div class="text-sm text-gray-600 mb-3">
      {{ product.description }}
      </div>
    
    <!-- Price Section -->
    <div class="font-semibold text-lg text-gray-800 mt-auto text-center">
      ${{ parseFloat(product.price).toFixed(2) }}
    </div>
  </div>

</template>

<script>
export default {
  data() {
    return {
      product: null,
    };
  },
  methods: {
    fetchProductDetails(productId) {
      fetch("/products.xml")
        .then((response) => response.text())
        .then((xmlText) => {
          const parser = new DOMParser();
          const xmlDoc = parser.parseFromString(xmlText, "application/xml");
          const productNode = Array.from(
            xmlDoc.getElementsByTagName("product")
          ).find((node) => node.getElementsByTagName("id")[0].textContent === productId);
          if (productNode) {
            this.product = {
              id: productNode.getElementsByTagName("id")[0].textContent,
              title: productNode.getElementsByTagName("title")[0].textContent,
              description: productNode.getElementsByTagName("description")[0].textContent,
              price: productNode.getElementsByTagName("price")[0].textContent,
              measurements: productNode.getElementsByTagName("measurements")[0].textContent,
              // Add other fields as needed
            };
          }
        })
        .catch((error) => console.error("Error fetching product details:", error));
    },
  },
  created() {
    const productId = this.$route.params.id;
    this.fetchProductDetails(productId);
  },
};
</script>
