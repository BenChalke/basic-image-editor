<template>
  <div id="slider-div" :class="title === 'Brightness' ? 'b-green' : 'c-blue'">
    <p id="slider-title">{{ title }}</p>
    <div id="range-div">
      <form action="">
        <input
          v-if="title === 'Brightness'"
          v-model="bRange"
          type="range"
          :id="title"
          :name="title"
          min="-100"
          max="100"
          class="b-green"
        />
        <input
          v-else-if="title === 'Contrast'"
          v-model="cRange"
          type="range"
          :id="title"
          :name="title"
          min="-100"
          max="100"
          class="c-blue"
        />
      </form>
    </div>
    <p id="slide-text">Slide to adjust the image {{ title }}!</p>
  </div>
</template>

<script>
export default {
  name: "Slider",
  props: {
    title: String,
    BrRange: String,
    CoRange: String
  },
  data() {
    return {
      bRange: this.BrRange,
      cRange: this.CoRange
    };
  },
  watch: {
    bRange() {
      console.log(this.bRange);
      this.$emit("updateBrRange", this.bRange);
    },
    cRange() {
      console.log(this.cRange);
      this.$emit("updateCoRange", this.cRange);
    }
  }
};
</script>

<style scoped>
div#slider-div {
  margin: 7px 20px 0 20px;
  background-color: #ffffff;
  box-shadow: 0 0 10px 0 #dddddd;
  display: block;
  text-align: center;
  border-radius: 10px;
}

p#slider-title {
  font-weight: 500;
  font-size: 18px;
  padding: 10px;
  margin: 0;
}

div#slider-div.b-green {
  color: #25a95b;
}

div#slider-div.c-blue {
  color: #4a90e2;
}

p#slide-text {
  margin: 0;
  padding-bottom: 10px;
  color: #000000 !important;
}
/* Slider Styling */
div#range-div {
  text-align: center;
}

input[type="range"] {
  -webkit-appearance: none;
  margin: 18px 0;
  width: 90%;
}
input[type="range"]:focus {
  outline: none;
}
input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  border-radius: 10px;
}
input[type="range"].b-green::-webkit-slider-runnable-track {
  background: #25a95b;
}
input[type="range"].c-blue::-webkit-slider-runnable-track {
  background: #4a90e2;
}
input[type="range"]::-webkit-slider-thumb {
  /* box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d; */
  border: 4px solid #ffffff;
  height: 30px;
  width: 30px;
  border-radius: 50%;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -10px;
}
input[type="range"].b-green::-webkit-slider-thumb {
  background: #25a95b;
}
input[type="range"].c-blue::-webkit-slider-thumb {
  background: #4a90e2;
}
/* input[type="range"]:focus::-webkit-slider-runnable-track {
  background: #367ebd;
} */
/* MOZ */
input[type="range"]::-moz-range-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  border-radius: 10px;
}
input[type="range"].b-green::-moz-range-track {
  background: #25a95b;
}
input[type="range"].c-blue::-moz-range-track {
  background: #4a90e2;
}
input[type="range"]::-moz-range-thumb {
  border: 4px solid #ffffff;
  height: 30px;
  width: 30px;
  border-radius: 50%;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -10px;
}
input[type="range"].b-green::-moz-range-thumb {
  background: #25a95b;
}
input[type="range"].c-blue::-moz-range-thumb {
  background: #4a90e2;
}
/* MS */
input[type="range"]::-ms-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  border-radius: 10px;
  overflow: visible;
}
input[type="range"].c-blue::-ms-track {
  background: #4a90e2;
}
input[type="range"].b-green::-ms-track {
  background: #25a95b;
}
input[type="range"]::-ms-thumb {
  border: 4px solid #ffffff;
  height: 15px;
  width: 15px;
  border-radius: 50%;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: 0px;
}
</style>
