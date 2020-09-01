<template>
  <v-app-bar color="#293847" fixed app dark>
    <v-navigation-drawer
      fixed
      app
      absolute
      temporary
      v-model="drawer"
      hide-overlay
      class="d-flex flex-column"
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title d-flex">
            <v-icon class="mr-2">mdi-account-circle</v-icon>Hello Customer
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>
      <v-list dense nav>
        <v-list-item
          v-for="item in explorePages"
          :key="item.title"
          link
          :to="item.to"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
      <v-list dense nav>
        <v-list-item
          v-for="item in userPages"
          :key="item.title"
          link
          :to="item.to"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar-nav-icon @click.stop="drawer = !drawer" />

    <v-toolbar-title>H-Shop</v-toolbar-title>

    <v-spacer></v-spacer>

    <div
      background-color="rgb(0,0,0,0)"
      width="auto"
      style="box-shadow: none"
      class="d-flex"
    >
      <div
        class="d-flex align-center"
        v-for="page in navigationShortcut"
        :key="page.title"
      >
        <v-btn icon class="ml-2" :value="page.title" :to="page.to">
          <v-icon>{{ page.icon }}</v-icon>
        </v-btn>
      </div>
    </div>
  </v-app-bar>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      fixed: false,
      explorePages: [
        {
          icon: 'mdi-basket',
          title: 'Shop',
          to: '/',
        },
      ],
      userPages: [
        {
          icon: 'mdi-cart',
          title: 'Cart',
          to: '/user/cart',
        },
      ],
      navigationShortcut: [
        {
          icon: 'mdi-basket',
          title: 'Shop',
          to: '/',
        },
        {
          icon: 'mdi-cart',
          title: 'Cart',
          to: '/user/cart',
        },
      ],
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js',
    }
  },
  methods: {
    async logout() {
      await this.$auth.logout()
    },
  },
}
</script>
<style>
.v-toolbar__content {
  padding-left: 0;
  padding-right: 0;
}
</style>
