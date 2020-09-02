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
          @click="getProductByCategory()"
        ></v-radio>
      </v-radio-group>
    </v-col>
    <v-col cols="3" v-for="product in productsFiltered" :key="product.id">
      <CardProduct
        v-if="
          selectedCategoryID == null ||
          product.category.id == selectedCategoryID
        "
        :product="product"
      />
    </v-col>
    <!-- <v-btn @click="test">t</v-btn>
    <Paginate
      :page-count="5"
      :page-range="3"
      :margin-pages="2"
      :click-handler="clickCallback"
      :prev-text="'Prev'"
      :next-text="'Next'"
      :container-class="'pagination'"
      :page-class="'page-item'"
    >
    </Paginate> -->
  </v-row>
</template>

<script>
import CardProduct from '~/components/product/CardProduct'
// import Paginate from 'vuejs-paginate/src/components/Paginate';

export default {
  components: {
    CardProduct,
    // Paginate,
  },
  data() {
    return {
      products: [],
      error: '',
      categories: [],
      All: 'All',
      selectedCategoryID: null,
      productsFiltered: null,
    }
  },
  async mounted() {
    this.getAllProducts()

    try {
      const categories = await this.$strapi.find('categories')
      this.categories = categories
    } catch (error) {
      console.log(error)
    }
  },
  methods: {
    async getAllProducts() {
      // const products = await this.$strapi.find('products')
      const products = await this.$axios.get('products?_start=0&_limit=10')
      console.log(products.data);
      this.products = products.data
      this.productsFiltered = products.data
    },
    async getProductByCategory(id = null) {
      if (id == null) this.selectedCategoryID = null
      this.selectedCategoryID = await id
      this.productsWithCategoryFilter()
    },
    productsWithCategoryFilter() {
      if (this.selectedCategoryID == null)
        return (this.productsFiltered = this.products)

      this.productsFiltered = this.products.filter(
        (p) => p.category.id == this.selectedCategoryID
      )
    },
    // async test() {
    //   const log = await this.$axios.get('products?category=1')
    //   console.log(log)
    // },

    // async clickCallback(pageNum) {
    //   console.log(pageNum)
    // },
  },
}
</script>
<style lang="css">
/* .pagination {
}
.page-item {
} */
</style> 