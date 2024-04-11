<script setup>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/footer.vue"
</script>

<template>
  <div>
    <Navbar :logo="logo_src" :alt="app_name" />
    <div>
      <router-view></router-view>
    </div>
    <Footer />
  </div>
</template>


<style scoped>

</style>

