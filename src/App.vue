<template>
  <div id="app">
           <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="container">
  <div class="navbar-brand">
    <a class="navbar-item" href="#">
     <h1> Enye Frontend Trial</h1>
      </a>
    </div>
  </div>
</nav>
    <HelloWorld/>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import HelloWorld from "./components/HelloWorld.vue";

export default Vue.extend({
  name: "App",
  components: {
    HelloWorld
  }
});
</script>

<style lang="scss">
// Bulma css Import
@import "~bulma";
@import url('https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,200;0,300;0,400;0,600;0,700;0,800;0,900;1,200;1,300;1,400;1,600;1,700;1,800;1,900&display=swap');

* {
  background: transparent;
  padding: 0;
  margin: 0;
  border: 0;
  outline: none;
  text-decoration: none;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

body {
  position: relative;
  margin: 0;
  font-family:  'Nunito', sans-serif;;
  font-size: 14px;
  line-height: 1.5;
  color:#262b3f;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.navbar {
  background-color: #262b3f;
}

.navbar-item {
  color: #d6d7da;
  font-size: 1.4rem;
}

.loader-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background: #fff;
  z-index: 1;
  transition: opacity 0.3s;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 6px;

  .loader {
    height: 80px;
    width: 80px;
  }

  &.is-active {
    opacity: 1;
    z-index: 1;
  }
}


.button.is-loading::after, .loader, .select.is-loading::after, .control.is-loading::after {
    -webkit-animation: spinAround 500ms infinite linear;
    animation: spinAround 500ms infinite linear;
    border: 2px solid #49A73D;
    border-radius: 290486px;
    border-right-color: transparent;
    border-top-color: transparent;
    content: "";
    display: block;
    height: 1em;
    position: relative;
    width: 1em;
}
</style>
