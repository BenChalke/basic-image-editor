<template>
  <div id="upload-div">
    <form enctype="multipart/form-data" novalidate>
      <div id="upload-info">
        <div id="canvas-div">
          <canvas id="imageCanvas" width="100%" height="100%">
            <p>Canvas support needed!</p>
          </canvas>
        </div>
        <div id="name-div">
          <p id="nameLabel">Name</p>
          <p id="fileName">{{ fileName }}</p>
        </div>
        <div id="input-div">
          <label for="imageLoader" id="uploadBtn"
            >Upload
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
    <img id="hiddenImg" alt='hiddenImg'/>
    <img id="newImage" alt='newImage'/>
  </div>
</template>

<script>
export default {
  name: "FileUploader",
  props: {
    imageLoaded: Boolean,
    BrRange: String,
    CoRange: String
  },
  data() {
    return {
      fileName: "No File",
      brChanged: false,
      coChanged: false,
    };
  },
  mounted() {},
  methods: {
    handleImg(event) {
      // console.log(event);
      let getHiddenImg = document.getElementById("hiddenImg");
      getHiddenImg.src = URL.createObjectURL(event.target.files[0]);

      this.$emit("updateImageLoaded", true);
      const canvas = document.getElementById("imageCanvas");
      let ctx = canvas.getContext("2d");
      let reader = new FileReader();
      reader.onload = function(event) {
        let img = new Image();
        img.onload = function() {
          // console.log("cw", canvas.width);
          canvas.width = img.width;
          canvas.height = img.height;
          ctx.drawImage(img, 0, 0);
        };
        img.src = event.target.result;
      };
      reader.readAsDataURL(event.target.files[0]);

      canvas.style.width = "100%";
      canvas.width = canvas.offsetWidth;

      // console.log(event.srcElement.files[0].name);
      this.fileName = event.srcElement.files[0].name;
    },
    redrawImage() {
      const canvas = document.getElementById("hiddenImg");
      this.drawImage(canvas);
    },
    drawImage(image) {
      const canvas = document.getElementById("imageCanvas");
      let ctx = canvas.getContext("2d");
      ctx.drawImage(image, 0, 0);
    },
    applyBrightness(data, brightness) {
      for (let i = 0; i < data.length; i += 4) {
        data[i] += 255 * (brightness / 100);
        data[i + 1] += 255 * (brightness / 100);
        data[i + 2] += 255 * (brightness / 100);
      }
    },
    applyContrast(data, contrast) {
      var factor = (259.0 * (contrast + 255.0)) / (255.0 * (259.0 - contrast));

      for (var i = 0; i < data.length; i += 4) {
        data[i] = this.truncateColor(factor * (data[i] - 128.0) + 128.0);
        data[i + 1] = this.truncateColor(
          factor * (data[i + 1] - 128.0) + 128.0
        );
        data[i + 2] = this.truncateColor(
          factor * (data[i + 2] - 128.0) + 128.0
        );
      }
    },
    truncateColor(value) {
      if (value < 0) {
        value = 0;
      } else if (value > 255) {
        value = 255;
      }

      return value;
    }
  },
  watch: {
    BrRange(newVal) {

      this.brChanged = true;
      // console.log('brChanged', this.brChanged, 'coChanged', this.coChanged);
      if(this.brChanged && this.coChanged) {
        const getCanvas = document.getElementById("imageCanvas");
        let setChangedImg = document.getElementById("hiddenImg");
        setChangedImg.src = getCanvas.toDataURL();
      }
      this.coChanged = false;

      const canvas = document.getElementById("imageCanvas");
      let ctx = canvas.getContext("2d");

      let imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);

      this.redrawImage();

      imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
      this.applyBrightness(imageData.data, parseInt(newVal, 10));

      ctx.putImageData(imageData, 0, 0);

      let setNewImage = document.getElementById("newImage");
      setNewImage.src = canvas.toDataURL();
    },
    CoRange(newVal) {

      this.coChanged = true;
      // console.log('brChanged', this.brChanged, 'coChanged', this.coChanged);
      if(this.brChanged && this.coChanged) {
        const getCanvas = document.getElementById("imageCanvas");
        let setChangedImg = document.getElementById("hiddenImg");
        setChangedImg.src = getCanvas.toDataURL();
      }
      this.brChanged = false;

      const canvas = document.getElementById("imageCanvas");
      let ctx = canvas.getContext("2d");

      let imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);

      this.redrawImage();

      imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
      this.applyContrast(imageData.data, parseInt(newVal, 10));

      ctx.putImageData(imageData, 0, 0);

      let setNewImage = document.getElementById("newImage");
      setNewImage.src = canvas.toDataURL();
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
div#upload-info {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
div#name-div {
  flex: 1 1 100px;
  padding: 10px;
}
div#name-div p {
  display: inline-block;
  margin: 0;
}
p#nameLabel {
  color: #8392a6;
  border: 1px solid #dcdedc;
  background-color: #f6f8fa;
  padding: 10px 20px;
  font-weight: 500;
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
  text-transform: uppercase;
  position: relative;
}
p#fileName {
  padding: 10px;
  margin: 0;
  border-right: 1px solid #dcdedc;
  border-top: 1px solid #dcdedc;
  border-bottom: 1px solid #dcdedc;
  background-color: #f6f8fa;
  color: #25a95b;
  width: 50%;
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
div#canvas-div {
  flex: 1 0 100%;
}
#hiddenImg {
  display: none;
}
#newImage {
  display: none;
}
</style>
