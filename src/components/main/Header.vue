<template>
    <header id="header">
        <p id="header-title">{{ title }}</p>
        <p id="header-subtitle">{{ subTitle }}</p>
    </header>
</template>


<script>
export default {
  name: 'Header',
  data() {
      return{
          title: 'Brightness & Contrast Developer Test',
          subTitle: '14 Feb, 2020 - Present',
      };
  }
}
</script>

<style scoped>
header#header{
    background-color: #7344C0;
    text-align: center;
    color: #ffffff;
    padding: 10px;
}
p#header-title{
    margin: 0;
    font-weight: 500;
}
p#header-subtitle{
    margin: 0;
    font-weight: 400;
}

</style>