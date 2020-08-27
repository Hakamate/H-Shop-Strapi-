<template>
  <div v-if="error">
    {{ error }}
  </div>
  <ul v-else>
    <li v-for="product in products" :key="product.id">
      {{ product.title }}
      <ul>
        <li>{{ product.price }}</li>
        <li>{{ product.description }}</li>
        <li v-for="image in product.image" :key="image.id">
          <img
            width="100"
            :src="'http://localhost:1337' + image.url"
            :alt="image.name"
          />
        </li>
      </ul>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      products: [],
      error: '',
    }
  },
  // async mounted(){
  //   try {
  //     const products = await this.$strapi.find('products')
  //     this.products = products;
  //     console.log(products);
  //   } catch (error) {
  //     console.log(error);
  //   }
  // }
}
</script>
