<template>
  <div id="main">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style lang="scss">
@import "./assets/styles";

body {
  background: url("./assets/images/background.jpg") no-repeat center center
    fixed;
  background-size: cover;
  &:after {
    content: "";
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    background-color: $background-tint;
    opacity: 0.5;
    z-index: -1;
  }
}
</style>
