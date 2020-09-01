<template>
  <v-app dark>
    <Navigation/>
    <v-main>
      <v-container class="py-8">
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Navigation from "~/components/global/Navigation"

export default {
  components:{
    Navigation
  },
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  }
}
</script>
