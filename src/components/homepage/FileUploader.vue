<template>
  <div id="upload-div">
    <form enctype="multipart/form-data" novalidate>
      <div id="upload-info">
        <div id="canvas-div">
          <canvas id="imageCanvas" width="100%" height="100%"></canvas>
        </div>
        <div id="name-div">
          <p id="nameLabel">Name</p>
          <p id="fileName">{{ fileName }}</p>
        </div>
        <div id="input-div">
          <label for="imageLoader" id="uploadBtn">Upload
          <div id="arrow-up"></div>
          <input
            id="imageLoader"
            name="imageLoader"
            type="file"
            @change="handleImg($event)"
            accept="image/*"
            class="input-file"
          />
          </label>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "FileUploader",
  data() {
    return {
      fileName: 'No File',
    };
  },
  mounted() {},
  methods: {
    async handleImg(event) {
      // this.$emit("imageLoaded", true);
      const canvas = document.getElementById("imageCanvas");
      let ctx = canvas.getContext("2d");
      var reader = new FileReader();
      reader.onload = function(event) {
        let img = new Image();
        img.onload = function() {
          console.log('cw', canvas.width);
          canvas.width = img.width;
          canvas.height = img.height;
          ctx.drawImage(img, 0, 0);
        };
        img.src = event.target.result;
      };
      reader.readAsDataURL(event.target.files[0]);

      canvas.style.width ='100%';
      // ...then set the internal size to match
      canvas.width  = canvas.offsetWidth;
      
      console.log(event.srcElement.files[0].name);
      this.fileName = event.srcElement.files[0].name;
    }
  }
};
</script>

<style scoped>
div#upload-div {
  margin: 20px;
  background-color: white;
  border-radius: 10px;
  border: 1px solid #dcdedc;
  overflow: hidden;
}
div#upload-info{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
div#name-div{
  flex: 1 1 100px;
  padding: 10px;
}
div#name-div p{
  display: inline-block;
  margin: 0;
}
p#nameLabel{
  color: #8392A6;
  border: 1px solid #dcdedc;
  background-color: #f6f8fa;
  padding: 10px 20px;
  font-weight: 500;
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
  text-transform: uppercase;
  position: relative;
}
p#fileName{
  padding: 10px;
  margin: 0;
  border-right: 1px solid #dcdedc;
  border-top: 1px solid #dcdedc;
  border-bottom: 1px solid #dcdedc;
  background-color: #f6f8fa;
  color: #25a95b;
  width: 60%;
  display: inline-block;
  position: absolute;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  text-transform: uppercase;
}
div#input-div {
  background-color: #ffffff;
  padding: 10px;
  position: relative;
  flex: 0 1 100px;
  display: inline-block;
  text-align: right;
}
input#imageLoader {
  display: none;
}
label#uploadBtn {
  color: #4a90e2;
  border-radius: 5px;
  border: 1px solid #dcdedc;
  background-color: #f6f8fa;
  padding: 10px 20px 10px 30px;
  font-weight: 500;
  text-transform: uppercase;
  position: relative;
  display: inline-block;
}
div#arrow-up {
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 15px solid #4a90e2;
  position: absolute;
  border-radius: 5px;
  top: 50%;
  left: 5px;
  transform: translateY(-50%);
}
div#canvas-div{
  flex: 1 0 100%;
}
canvas#imageCanvas {
}
</style>
