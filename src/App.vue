<template>
  <div id="app">
    <Header/>
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Footer/>
  </div>
</template>

<script>
import Header from './components/main/Header.vue';
// import HelloWorld from './components/HelloWorld.vue';
import Footer from './components/main/Footer.vue';

export default {
  name: 'App',
  components: {
    // HelloWorld,
    Header,
    Footer
  }
}
</script>

<style>
#app {
  /* Global Styles */
  margin: 0;
  padding: 0;
}
</style>
