<template>
  <header id="header">
    <p id="header-title">{{ title }}</p>
    <p id="header-subtitle">{{ subTitle }}</p>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      title: "Brightness & Contrast Developer Test",
      subTitle: "14 Feb, 2020 - 17th Feb, 2020"
    };
  }
};
</script>

<style scoped>
header#header {
  background-color: #7344c0;
  text-align: center;
  color: #ffffff;
  padding: 20px;
}
p#header-title {
  margin: 0;
  padding-bottom: 10px;
  font-size: 15px;
  font-weight: 500;
}
p#header-subtitle {
  margin: 0;
  font-size: 13px;
  font-weight: 400;
}
</style>
