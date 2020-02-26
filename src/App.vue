<template>
  <div id="app">
    <Header />
    <div class="app-content">
      <HomeHero />
      <div class="slider-uploader-div">
        <Slider
          title="Brightness"
          :BrRange="BrRange"
          @updateBrRange="updateBrRange"
          v-if="imageLoaded"
        />
        <Slider
          title="Contrast"
          :CoRange="CoRange"
          @updateCoRange="updateCoRange"
          v-if="imageLoaded" 
        />
        <FileUploader
          imageLoaded
          @updateImageLoaded="updateImageLoaded"
          @updateCoRange="updateCoRange"
          @updateBrRange="updateBrRange"
          :BrRange="BrRange"
          :CoRange="CoRange"
        />
      </div>
    </div>
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
    return {
      BrRange: "0",
      CoRange: "0",
      imageLoaded: false
    };
  },
  methods: {
    updateBrRange(newVal) {
      this.BrRange = newVal;
    },
    updateCoRange(newVal) {
      this.CoRange = newVal;
    },
    updateImageLoaded(newVal) {
      this.imageLoaded = newVal;
    }
  },
};
</script>

<style lang="scss">
@import '../public/scss/styles.scss';
</style>
