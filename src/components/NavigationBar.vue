<!-- <template>
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
</template> -->


<template>
  <div>
    <v-app-bar
      color="bg-dark navbar-dark accent-4"
      dense
      dark
    >
      <!-- <v-app-bar-nav-icon></v-app-bar-nav-icon> 3 bars icon -->
    <!-- <a class="navbar-brand" href="/"><img src="images/pics/UNO_Logo.png" width="50"></a>-->
    <!-- <v-toolbar-title>UNO</v-toolbar-title> -->
    <v-toolbar-side-icon>
        <v-img src="../assets/pics/UNO_Logo.png" width="50" />
    </v-toolbar-side-icon> 

    <v-tabs align-with-title="true" background-color="#343a40" color="#000000"> 
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
        <!-- <template v-slot:activator="{ on, attrs }">
          <v-btn
            icon
            v-bind="attrs"
            v-on="on"
          >
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template> -->

        <!-- <v-list>
          <v-list-item
            v-for="n in 5"
            :key="n"
            @click="() => {}"
          >
            <v-list-item-title>Option {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list> -->
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


<!-- <style>
/* Helper classes */
.basil {
  background-color: #000000 !important;
}
.basil--text {
  color: #a81c33 !important;
}
</style> -->