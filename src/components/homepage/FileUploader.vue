<template>
  <div class="upload-div">
    <form enctype="multipart/form-data" novalidate>
      <div class="upload-info">
        <div class="canvas-div">
          <canvas id="imageCanvas" class="imageCanvas" width="100%" height="100%">
            <p>Canvas support needed!</p>
          </canvas>
        </div>
        <div class="canvas-info-div">
          <div class="name-div">
            <p class="nameLabel">Name</p>
            <p class="fileName">{{ fileName }}</p>
          </div>
          <div class="input-div">
            <label for="imageLoader" class="uploadBtn"
              >Upload
              <div class="arrow-up"></div>
              <input
                class="imageLoader"
                id="imageLoader"
                name="imageLoader"
                type="file"
                @change="handleImg($event)"
                accept="image/*"
              />
            </label>
          </div>
        </div>
      </div>
    </form>
    <img id="hiddenImg" class="hiddenImg" alt='hiddenImg'/>
    <img id="newImage" class="newImage" alt='newImage'/>
    <img id="modifiedImage" class="modifiedImage" alt='modifiedImage'/>
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
      offsetX: '',
      offsetY: '',
      pixelRatio: '',
      scaledWidth: '',
      scaledHeight: '',
      canvasSize: 400,
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
          
          let imageRatio = img.width / img.height;
          let offsetX = 0;
          let offsetY = 0;
          let scaledWidth = 1000;
          let scaledHeight = 1000;
          let pixelRatio = Math.round(window.devicePixelRatio || window.screen.deviceXDPI / window.screen.logicalXDPI);
          ctx.scale(pixelRatio, pixelRatio);
          const previewRatio = 1000 / 1000;
          
          if (imageRatio >= previewRatio) {
            scaledHeight = scaledWidth / imageRatio;
            offsetY = (1000 - scaledHeight) / 2;
          } else {
            scaledWidth = scaledHeight * imageRatio;
            offsetX = (1000 - scaledWidth) / 2;
          }

          canvas.style.background = 'none';
          canvas.width = 1000 * pixelRatio;
          canvas.height = 1000 * pixelRatio;
          ctx.setTransform(1, 0, 0, 1, 0, 0);
          ctx.clearRect(0, 0, canvas.width, canvas.height);

          this.offsetX = offsetX;
          this.offsetY = offsetY;
          this.pixelRatio = pixelRatio;
          this.scaledWidth = scaledWidth;
          this.scaledHeight = scaledHeight;
          
          ctx.drawImage(img,
            offsetX * pixelRatio,
            offsetY * pixelRatio,
            scaledWidth * pixelRatio,
            scaledHeight * pixelRatio);

        };
        img.src = event.target.result;
      };
      reader.readAsDataURL(event.target.files[0]);

      // canvas.style.width = "100%";
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
      ctx.drawImage(image,
            this.offsetX * this.pixelRatio,
            this.offsetY * this.pixelRatio,
            this.scaledWidth * this.pixelRatio,
            this.scaledHeight * this.pixelRatio);
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
