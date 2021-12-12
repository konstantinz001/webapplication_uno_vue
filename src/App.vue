<template>
  <v-app>
    <v-img src="./assets/pics/UNO_Background.png">
      <NavigationBar></NavigationBar>
      <v-main>
        <router-view />
      </v-main>
    </v-img>
  </v-app>
</template>


<script>
import NavigationBar from "@/components/NavigationBar.vue";
export default {
  name: "App",
  components: {
    NavigationBar,
  },
};
</script>
