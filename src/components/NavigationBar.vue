<template>
  <v-card color="basil">
    <v-card-title class="text-center justify-center py-0">
      <h1 class="font-weight-bold text-h2 basil--text">
        UNO - WEB APPLICATION
      </h1>
    </v-card-title>

    <v-tabs background-color="#ECF0F1" color="basil" grow>
      <v-tab v-for="item in items" :id="item.title" :key="item.title" :to="item.to">
        {{ item.title }}
      </v-tab>
    </v-tabs>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      items: [
          { title: 'Home', icon: 'mdi-home', to: '/' },
          { title: 'New Game', icon: 'mdi-microsoft-xbox-controller', to: '/game' },
          { title: 'About', icon: 'mdi-information', to: '/about' },
        ],
    };
  },
};
</script>


<style>
/* Helper classes */
.basil {
  background-color: #000000 !important;
}
.basil--text {
  color: #a81c33 !important;
}
</style>