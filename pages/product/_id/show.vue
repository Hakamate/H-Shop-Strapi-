<template>
  <div v-if="error">
    {{ error }}
  </div>
  <!-- <v-row v-else>
    <v-col cols="1" class="redc">
      <v-row>
        <v-col class="py-0" v-for="image in product.image" :key="image.id">
          <v-img
            :id="selectedImage == image.id ? 'selectedImage' : ''"
            @click="selectedImage = image.id"
            :src="'http://localhost:1337' + image.url"
          ></v-img>
        </v-col>
      </v-row>
    </v-col>
    <v-col cols="6" class="bluec">
      <v-img
        v-if="product.image"
        :src="
          'http://localhost:1337' +
          product.image[product.image.findIndex((x) => x.id == selectedImage)]
            .url
        "
      ></v-img>
    </v-col>
    <v-col cols="5" class="greenc">
      <h1>{{ product.title }}</h1>
      <p>{{ product.description }}</p>
      <div class="d-flex mb-6">
        <div v-for="color in product.colors" :key="color.id">
          <div :class="color.value" class="pa-2 rounded-circle mt-4"></div>
        </div>
      </div>
      <p class="text-h2">{{ product.price }} €</p>
      <v-btn rounded outlined color="primary">
        <v-icon class="mr-2">mdi-cart</v-icon>
        <span> Add to cart </span>
      </v-btn>
    </v-col>
  </v-row> -->
  <v-row v-else>
    <v-col cols="1">
      <v-row v-if="product.product_images">
        <v-col
          class="py-0"
          v-for="image in product.product_images[
            product.product_images.findIndex(
              (x) => x.id == selectedProductColor
            )
          ].images"
          :key="image.id"
        >
          <v-img
            :id="selectedImage == image.id ? 'selectedImage' : ''"
            @click="selectedImage = image.id"
            :src="'http://localhost:1337' + image.url"
          ></v-img>
        </v-col>
      </v-row>
    </v-col>
    <v-col cols="6">
      <v-img
        v-if="product.product_images"
        :src="
          'http://localhost:1337' +
          product.product_images[
            product.product_images.findIndex(
              (x) => x.id == selectedProductColor
            )
          ].images[
            product.product_images[
              product.product_images.findIndex(
                (x) => x.id == selectedProductColor
              )
            ].images.findIndex((x) => x.id == selectedImage)
          ].url
        "
      ></v-img>
    </v-col>
    <v-col cols="5">
      <h1 class="mb-2">{{ product.title }}</h1>
      <p class="mb-0">{{ product.description }}</p>
      <p class="font-weight-bold mt-4 mb-0">
        Price :
        <span class="text-h4 font-weight-bold light-green--text text--darken-1"
          >{{ product.price }}<sup class="expo ml-1">€</sup></span
        >
      </p>
      <div class="d-flex align-center pb-2">
        <p class="font-weight-bold mb-0">Available colors :</p>
        <div class="d-flex ml-2 ma-0 justify-center" v-if="product.product_images">
          <div
            v-for="productColor in product.product_images"
            :key="productColor.id"
          >
            <div
              v-bind:style="{
                background: productColor.color,
              }"
              @click="changeProductColor(productColor.id)"
              class="pa-3 mr-1 rounded-circle"
            ></div>
          </div>
        </div>
      </div>
      <v-btn color="primary">
        <v-icon class="mr-2">mdi-cart</v-icon>
        <span> Add to cart </span>
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      product: {},
      error: '',
      selectedProductColor: 0,
      selectedImage: 0,
    }
  },
  async mounted() {
    try {
      const product = await this.$strapi.findOne(
        'products',
        this.$route.params.id
      )
      console.log(product.product_images)
      this.product = product
      this.selectedProductColor = product.product_images[0].id
      this.selectedImage = product.product_images[0].images[0].id
    } catch (error) {
      console.log(error)
    }
  },
  methods: {
    changeProductColor(newID) {
      console.log(
        this.product.product_images[
          this.product.product_images.findIndex(
            (x) => x.id == this.selectedProductColor
          )
        ].images[0].id
      )
      this.selectedProductColor = newID
      this.selectedImage = this.product.product_images[
        this.product.product_images.findIndex(
          (x) => x.id == this.selectedProductColor
        )
      ].images[0].id
    },
  },
}
</script>
<style>
#selectedImage {
  border: 2px solid orange;
}
h1 {
  line-height: 0.9;
}
p {
  line-height: 1.2;
}
.expo {
  font-size: initial;
}
</style>
