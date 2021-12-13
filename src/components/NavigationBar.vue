<template>
  <div>
    <v-app-bar
      color="bg-dark navbar-dark accent-4"
      dense
      dark
    >

    <v-app-bar-nav-icon href="http://localhost:8080/">
        <v-img src="../assets/pics/UNO_Logo.png" width="50" />
    </v-app-bar-nav-icon> 

    <v-tabs background-color="#343a40" color="#000000"> 
    <!-- <v-tabs color="#343a40 black-4"> -->
      <v-tab v-for="item in items" :id="item.title" :key="item.title" :to="item.to">
        {{ item.title }}
      </v-tab>
    </v-tabs>
      

      <v-spacer></v-spacer>

      <v-btn icon href="https://github.com/konstantinz001/UNO_WebApplication" target="_blank">
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <!-- <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn> -->

      <v-menu
        left
        bottom
      >

      </v-menu>
    </v-app-bar>
  </div>
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
