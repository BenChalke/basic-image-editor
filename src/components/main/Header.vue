<template>
  <header class="header">
    <p class="header-title">{{ title }}</p>
    <p class="header-subtitle">{{ subTitle }}</p>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      title: "Brightness & Contrast Developer Test",
      subTitle: "14th Feb, 2020 - 17th Feb, 2020"
    };
  }
};
</script>
