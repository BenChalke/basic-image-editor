<template>
  <div id="app">
    <Header/>
    <div id="home-hero">
      <img src="../src/assets/home-hero.svg" alt="Home Hero" id="home-hero-img">
    </div>
    <Footer/>
  </div>
</template>

<script>
import Header from './components/main/Header.vue';
import Footer from './components/main/Footer.vue';

export default {
  name: 'App',
  components: {
    Header,
    Footer
  }
}
</script>

<style>
#app {
  margin: 0;
  padding: 0;
}
div#home-hero{

}
img#home-hero-img{
  width: 100%;
}
</style>
