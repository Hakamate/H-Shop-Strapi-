<template>
  <div v-if="error">
    {{ error }}
  </div>
  <v-row v-else>
    <v-col cols="3">
      <div style="background: #375e86" class="white--text">
        <span class="ml-2">Categories</span>
      </div>
      <v-radio-group v-model="All">
        <v-radio
          v-for="categorie in categories"
          :key="categorie.id"
          :label="categorie.name"
          :value="categorie.name"
          @click="getProductByCategory(categorie.id)"
        ></v-radio>
                <v-radio
          :key="-1"
          label="All"
          value="All"
          @click="getAllProducts"
        ></v-radio>
      </v-radio-group>
    </v-col>
    <v-col cols="3" v-for="product in products" :key="product.id">
      <CardProduct :product="product" />
    </v-col>
  </v-row>
</template>

<script>
import CardProduct from '~/components/product/CardProduct'

export default {
  components: {
    CardProduct,
  },
  data() {
    return {
      products: [],
      error: '',
      categories: [],
      All: 'All',
    }
  },
  async mounted() {
    this.getAllProducts()

    try {
      const categories = await this.$strapi.find('categories')
      this.categories = categories
      console.log(categories)
    } catch (error) {
      console.log(error)
    }
  },
  methods: {
    async getAllProducts() {
      try {
        const products = await this.$strapi.find('products')
        this.products = products
        console.log(products)
      } catch (error) {
        console.log(error)
      }
    },
    async getProductByCategory(id) {
      try {
        const products = await this.$axios.get(`products?category=${id}`)
        console.log(products.data)
        this.products = products.data
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>
