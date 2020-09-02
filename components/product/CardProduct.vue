<template>
  <div class="mx-auto text-left" max-width="374">
    <nuxt-link class="nuxt-link" :to="'/product/' + product.id + '/show'">
      <v-img
        height="250"
        :src="'http://localhost:1337' + product.product_images[0].images[0].url"
      ></v-img>
      <p class="caption ma-0 mt-2 grey--text text--darken-1">
        {{ product.gender }} {{ product.category.name }}
      </p>
      <p class="pb-0 ma-0 font-weight-bold grey--text text--darken-2">
        {{ product.title }}
      </p>
      <p
        class="pt-0 ma-0 mb-2 font-weight-bold light-green--text text--darken-1"
      >
        {{ product.price }} €
      </p>

      <div class="d-flex justify-start">
        <div
          v-for="product_images in product.product_images"
          :key="product_images.id"
        >
          <div
            v-bind:style="{
              background: product_images.color,
            }"
            class="pa-2 rounded-circle"
          ></div>
        </div>
      </div>
    </nuxt-link>
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  methods: {
  },
}
</script>
