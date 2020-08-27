<template>
  <div v-if="error">
    {{ error }}
  </div>
  <div v-else>
    <v-row>
      <v-col cols="4" v-for="product in products" :key="product.id">
        <v-card class="mx-auto my-12 text-center" max-width="374">
          <v-card-title
            class="text-h4 font-weight-bold grey--text text--darken-3"
            >{{ product.title }}</v-card-title
          >
          <v-img
            height="250"
            :src="'http://localhost:1337' + product.image[0].url"
          ></v-img>

          <v-divider class="mx-4"></v-divider>

          <div class="d-flex justify-center">
            <div v-for="color in product.colors" :key="color.id">
              <div :class="color.value" class="pa-2 rounded-circle mt-4"></div>
            </div>
          </div>

          <v-card-text
            class="text-h4 font-weight-bold grey--text text-darken-2"
          >
            <p>{{ product.price }} €</p>
            <v-btn class="" rounded outlined color="primary" dark
              >Add to cart</v-btn
            >
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
      error: '',
    }
  },
  async mounted() {
    try {
      const products = await this.$strapi.find('products')
      this.products = products
      console.log(products)
    } catch (error) {
      console.log(error)
    }
  },
}
</script>
<style>
.theme--dark.v-card {
  background-color: #fefefe;
}
</style>
