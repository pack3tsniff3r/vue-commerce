<template>
  <div class="container mx-auto p-4">
    <!-- Responsive Grid -->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
  
    <ProductCard
      v-for="product in products"
      :key="product.id"
      :product="product"
      @showDetails="showDetails"
    />
  </div>
  </div>
</template>

<script>
import ProductCard from "../components/ProductCard.vue";

export default {
  components: { ProductCard },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    fetchProducts() {
      fetch("/products.xml")
        .then((response) => response.text())
        .then((xmlText) => {
          const parser = new DOMParser();
          const xmlDoc = parser.parseFromString(xmlText, "application/xml");
          const productNodes = xmlDoc.getElementsByTagName("product");
          this.products = Array.from(productNodes).map((node) => ({
            id: node.getElementsByTagName("id")[0].textContent,
            mainImage: node.getElementsByTagName("mainImage")[0].textContent,
            thumbnails: Array.from(node.getElementsByTagName("image")).map(thumbnail=>thumbnail.textContent),
            title: node.getElementsByTagName("title")[0].textContent,
            description: node.getElementsByTagName("description")[0].textContent,
            price: node.getElementsByTagName("price")[0].textContent,
            measurements: node.getElementsByTagName("measurements")[0].textContent,
          }));
        })
        .catch((error) => console.error("Error fetching products:", error));
    },
    showDetails(productId) {
      this.$router.push({ name: "ProductDetails", params: { id: productId } });
    },
  },
  created() {
    this.fetchProducts();
  },
};
</script>