<script setup>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/footer.vue"
import { reactive } from "vue";

const obj = reactive({
  logo_src: '/images/logo.png',
  app_name: 'Make your Burger',
})
</script>

<template>
  <div>
    <Navbar :logo="obj.logo_src" :alt="obj.app_name" />
    <div>
      <router-view></router-view>
    </div>
    <Footer />
  </div>
</template>


<style>
* {
  font-family: Helvetica;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  text-decoration: none;
}

.main-container {
  margin: 50px;
  min-height: 100vh;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}
</style>