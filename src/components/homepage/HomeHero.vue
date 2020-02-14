<template>
  <div>
    <div id="home-hero">
      <img
        src="../../assets/home-hero.svg"
        alt="Home Hero"
        id="home-hero-img"
      />
    </div>
    <div id="selfie">
      <img
        src="../../assets/homer.jpg"
        alt="Homer Simpson"
        id="selfie-img"
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeHero"
};
</script>

<style scoped>
div#home-hero{
  padding-bottom: 10px;
}
img#home-hero-img {
  width: 100%;
}
div#selfie{
  position: absolute;
  bottom: 0;
  background-color: #ffffff;
  border-radius: 50%; 
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 60px;
}

div#selfie img{
  width: 100%;
  border: 2px solid #ffffff;
  border-radius: 50%; 
  overflow: hidden;
}
</style>
