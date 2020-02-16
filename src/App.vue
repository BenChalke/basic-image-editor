<template>
  <div id="app">
    <Header />
    <HomeHero />
    <div v-if="imageLoaded">
      <Slider title="Brightness" :range=range  @updateRange="updateRange" />
      <Slider title="Contrast" />
    </div>
    <FileUploader imageLoaded @updateImageLoaded="updateImageLoaded" :range=range />
    <Footer />
  </div>
</template>

<script>
import Header from "../src/components/main/Header.vue";
import HomeHero from "../src/components/homepage/HomeHero.vue";
import Slider from "../src/components/homepage/Slider.vue";
import FileUploader from "../src/components/homepage/FileUploader.vue";
import Footer from "../src/components/main/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    HomeHero,
    Slider,
    FileUploader,
    Footer
  },
  data() {
    return{
      range: '127.5',
      imageLoaded: false,
    };
  },
  methods: {
    updateRange(newVal){
      this.range = newVal;
      console.log('parent',this.range);
    },
    updateImageLoaded(newVal){
      this.imageLoaded = newVal;
      console.log('parent',this.range);
    }
  },
  watch: {
    // bRange() {
    //   console.log('parent',this.bRange);
    //   this.range = this.bRange;
    // },
  }
};
</script>

<style scoped>
#app {
  margin: 0;
  padding: 0;
}
</style>
