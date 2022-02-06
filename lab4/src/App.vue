<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
  @font-face {
    font-family: 'Red Ring';
    src: url(../RedRing-Medium.ttf);
  }
#app {
  font-family: 'Red Ring';
  text-align: center;
  color: black;
  margin-top: 60px;
}
</style>

