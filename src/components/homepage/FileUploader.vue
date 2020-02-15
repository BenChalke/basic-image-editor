<template>
  <div id="upload-div">
    <form enctype="multipart/form-data" novalidate>
      <h1>Upload images</h1>
      <div class="dropbox">
        <input
          id="imageLoader"
          name="imageLoader"
          type="file"
          @change="handleImg($event)"
          accept="image/*"
          class="input-file"
        />
        <!-- <img src="../../assets/home-hero.svg" id="theImage"> -->
        <canvas id="imageCanvas" width="300" height="300"></canvas>
        <p>
          Drag your file(s) here to begin<br />
          or click to browse
        </p>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "FileUploader",
  data() {
    return {
    };
  },
  mounted() {
    
  },
  methods: {
    async handleImg(event) {
      const canvas = document.getElementById("imageCanvas");
      let ctx = canvas.getContext("2d");
      var reader = new FileReader();
      reader.onload = function(event) {
        let img = new Image();
        img.onload = function() {
          img.width = canvas.width;
          // c.height = img.height;
          ctx.drawImage(img, 0, 0);
        };
        img.src = event.target.result;
      };
      reader.readAsDataURL(event.target.files[0]);
    }
  }
};
</script>

<style scoped>
canvas#imageCanvas{
  max-width: 300px;
}
</style>
