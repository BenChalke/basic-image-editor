<template>
  <div id="home-hero-content">
    <div id="home-hero">
      <img
        src="../../assets/home-hero.svg"
        alt="Home Hero"
        id="home-hero-img"
      />
    </div>
    <div id="selfie">
      <img
        src="../../assets/ben.png"
        alt="Ben Chalke"
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
@media screen and (max-width: 1023px) {
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
}
@media screen and (min-width: 1024px) {
  div#home-hero{
    padding-bottom: 10px;
    text-align: center;
  }
  img#home-hero-img {
    width: 97%;
    margin: 0 auto;
    display: inline-block;
    border-radius: 35px;
    padding: 20px;
  }
  div#selfie{
    position: absolute;
    right: 70px;
    background-color: #ffffff;
    border-radius: 50%; 
    top: 70px;
    /* transform: translateY(-50%); */
    width: 100px;
    height: 100px;
  }

  div#selfie img{
    width: 100%;
    border: 2px solid #ffffff;
    border-radius: 50%; 
    overflow: hidden;
  }
}
</style>
