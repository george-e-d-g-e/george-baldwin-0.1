<template>
  <div id="app">
    <CV />
  </div>
</template>

<script>
import CV from "./components/CV.vue";

export default {
  name: "App",
  components: {
    CV
  }
};
</script>

<style lang="scss">
@import "./assets/scss/global-vars.scss";
@import url("https://fonts.googleapis.com/css?family=Karla:400,700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  // font-family: 'Avenir', Helvetica, Arial, sans-serif;
  font-family: "Karla", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: $default;
  font-size: 16px;
  margin-top: 2em;
}

.block {
  width: 100%;
}

.block-title {
  color: $highlight;
  position: absolute;
  transform-origin: top left;
  transform: translate(7vw, 10.2vh) rotate(90deg);
}

.sub-section {
  background: $background;
  width: 100%;
  padding: 10vh 10%;
  &.alt {
    background: $alt-background;
  }
}
</style>
