<template>
  <div id="app">
    <Header />
    <HomeHero />
    <Slider title="Brightness" :range=range  @updateRange="updateRange" />
    <Slider title="Contrast" />
    <Footer />
  </div>
</template>

<script>
import Header from "../src/components/main/Header.vue";
import HomeHero from "../src/components/homepage/HomeHero.vue";
import Slider from "../src/components/homepage/Slider.vue";
import Footer from "../src/components/main/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    HomeHero,
    Slider,
    Footer
  },
  data() {
    return{
      range: '100',
    };
  },
  methods: {
    updateRange(newVal){
      this.range = newVal;
      console.log('parent',this.range);
    }
  },
  watch: {
    bRange() {
      console.log('parent',this.bRange);
      this.range = this.bRange;
    },
  }
};
</script>

<style scoped>
#app {
  margin: 0;
  padding: 0;
}
</style>
