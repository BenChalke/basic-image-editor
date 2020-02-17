<template>
  <div id="app">
    <Header />
    <HomeHero />
    <div v-if="imageLoaded">
      <Slider
        title="Brightness"
        :BrRange="BrRange"
        @updateBrRange="updateBrRange"
      />
      <Slider
        title="Contrast"
        :CoRange="CoRange"
        @updateCoRange="updateCoRange"
      />
    </div>
    <FileUploader
      imageLoaded
      @updateImageLoaded="updateImageLoaded"
      @updateCoRange="updateCoRange"
      @updateBrRange="updateBrRange"
      :BrRange="BrRange"
      :CoRange="CoRange"
    />
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
      console.log("parent", this.BrRange);
    },
    updateCoRange(newVal) {
      this.CoRange = newVal;
      console.log("parent", this.CoRange);
    },
    updateImageLoaded(newVal) {
      this.imageLoaded = newVal;
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
