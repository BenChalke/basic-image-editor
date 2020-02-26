<template>
  <div class="slider-div" :class="title === 'Brightness' ? 'b-green' : 'c-blue'">
    <p class="slider-title">{{ title }}</p>
    <div class="range-div">
      <form action="">
        <input
          v-if="title === 'Brightness'"
          v-model="bRange"
          type="range"
          :id="title"
          :name="title"
          min="-100"
          max="100"
          class="slider-range b-green"
        />
        <input
          v-else-if="title === 'Contrast'"
          v-model="cRange"
          type="range"
          :id="title"
          :name="title"
          min="-100"
          max="100"
          class="slider-range c-blue"
        />
      </form>
    </div>
    <p class="slide-text">Slide to adjust the image {{ title }}!</p>
  </div>
</template>

<script>
export default {
  name: "Slider",
  props: {
    title: String,
    BrRange: String,
    CoRange: String,
  },
  data() {
    return {
      bRange: this.BrRange,
      cRange: this.CoRange,
    };
  },
  watch: {
    bRange() {
      // console.log(this.bRange);
      this.$emit("updateBrRange", this.bRange);
    },
    cRange() {
      // console.log(this.cRange);
      this.$emit("updateCoRange", this.cRange);
    }
  }
};
</script>
