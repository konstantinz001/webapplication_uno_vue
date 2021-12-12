<template>
  <div class="about">
    <HomeComponent></HomeComponent>
  </div>
</template>

<script>
// @ is an alias to /src
import HomeComponent from "@/components/HomeComponent.vue";
export default {
  name: "Home",
  components: {
    HomeComponent,
  },
};
</script>

