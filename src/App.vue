<template>
  <div id="app">
    <Header />
    <div id="app-content">
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
      // console.log("parent", this.BrRange);
    },
    updateCoRange(newVal) {
      this.CoRange = newVal;
      // console.log("parent", this.CoRange);
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
@media screen and (min-width: 1024px) {
  #app-content{
    background: rgb(136,92,209);
    background: -moz-linear-gradient(90deg, rgba(136,92,209,1) 0%, rgba(177,130,255,1) 100%);
    background: -webkit-linear-gradient(90deg, rgba(136,92,209,1) 0%, rgba(177,130,255,1) 100%);
    background: linear-gradient(90deg, rgba(136,92,209,1) 0%, rgba(177,130,255,1) 100%);
    filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#885cd1",endColorstr="#b182ff",GradientType=1);
    padding: 30px 10%;
  }
}
</style>
